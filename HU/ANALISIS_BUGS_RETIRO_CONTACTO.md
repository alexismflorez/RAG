# Análisis de Bugs - HU: Retiro de Contacto (Inactivación por Retiro de Contacto)

**Fecha:** 09-02-2026  
**Analista:** Sistema de Análisis  
**Estado:** En Revisión  
**Prioridad:** Crítica

---

## 1. RESUMEN EJECUTIVO

El método `RetirarContacto()` en [RevisionSolicitudes.svc.cs](RevisionSolicitudes.svc.cs#L1729) presenta **5 bugs críticos** que impiden cerrar correctamente todos los registros asociados a un contacto cuando se aprueba una inactivación por retiro de contacto. El sistema cierra solo la información de la última solicitud de creación/modificación, dejando registros "huérfanos" activos en RAG, MID y Oracle.

**Impacto:** Inconsistencia de datos en las 3 bases de datos, violación de reglas de negocio, y posibles conflictos futuros.

---

## 2. BUGS IDENTIFICADOS

### BUG #1: Lógica Incompleta de Vigencias en RAG
**Ubicación:** [RevisionSolicitudes.svc.cs líneas 1762-1804](RevisionSolicitudes.svc.cs#L1762-L1804)  
**Severidad:** CRÍTICA  

#### Problema:
El código cierra vigencias solo de:
- `InfoContacto` (si está solo en 1 unidad de negocio)
- `TipoInfoContacto` (solo los vigentes del contacto actual)
- `InfoContactoNegocio` (solo vigentes del contacto actual)
- `AplicacionesPorContacto` (solo vigentes del contacto actual)

**Lo que falta:**
- NO cierra registros duplicados/antiguas versiones del mismo `InfoContacto` para el mismo agente/empresa
- NO valida si hay múltiples `IdInfoContacto` para identificación + agente
- NO aplica cierre de `Preinscripcion` para TODAS las versiones
- NO cierra `SolicitudTipoInfoContacto` de solicitudes anteriores
- NO cierra `AplicacionesPorContacto` de solicitudes anteriores

#### Código Actual:
```csharp
if (ocurrencias.Count == 1 && !tieneOtrasUnidadesActivas)
{
    // Solo cierra el contacto actual si es único
    FachadaRevisionSolicitudes.RetiroContactoInactivarPreinscripcion(
        contacto.Identificacion, 
        solicitud.Empresa.Identificacion);
    
    contacto.Vigencia = false;
    contacto.Estado = "I";
    contacto.Editable = false;
    contacto.FechaFinal = fechaRetiroNow;
    FachadaRevisionSolicitudes.ActualizarContacto(contacto);
}
```

#### Caso de Error:
Si existe:
- InfoContacto A (Vigencia=1, Generado por Solicitud X)
- InfoContacto B (Vigencia=1, Generado por Solicitud Y)

Ambos para: Juan López + Empresa XYZ + Agente 123

**Resultado actual:** Solo cierra B  
**Resultado esperado:** Cierra A y B

---

### BUG #2: Missing Loop para Cerrar Todas las Versiones del Contacto en RAG
**Ubicación:** [RevisionSolicitudes.svc.cs líneas 1808-1826](RevisionSolicitudes.svc.cs#L1808-L1826)  
**Severidad:** CRÍTICA  

#### Problema:
```csharp
var ltsTipoInfoContactos = contacto.TiposContacto
    .Where(x => x.Vigencia)
    .ToList();
```

Solo itera sobre `TiposContacto` del contacto actual. Si existen múltiples versiones del contacto en la misma empresa/agente, las anteriores NO se cierran.

#### Solución Requerida:
- Buscar TODAS las versiones del `InfoContacto` para esa identificación + agente + empresa
- Cerrar vigencias de:
  - Todos los `TipoInfoContacto` vigentes para cada versión
  - Todos los `SolicitudTipoInfoContacto` vigentes para cada versión
  - Todos los `InfoContactoNegocio` vigentes para cada versión
  - Todos los `AplicacionesPorContacto` vigentes para cada versión
  - Todos los `SolicitudAplicacionContacto` vigentes para cada versión

---

### BUG #3: MID - Lógica Incompleta de Cierre de Relaciones
**Ubicación:** [ControladoraTransaccion.cs líneas 873-923 (IntegrarMIDRetirarPorInactivarContacto)](ControladoraTransaccion.cs#L873-L923)  
**Severidad:** CRÍTICA  

#### Problema:
```csharp
// Solo busca el contacto actual por identificación
EntidadesMID.Contacto contactoMID = Broker.BrokerConsulta
    .ConsultarContactoPorIdentificacion(infoContacto.Identificacion);
```

**Falla porque:**
- Busca solo 1 contacto (el último activo)
- No busca contactos duplicados/antiguas versiones
- No busca contactos ya inactivos
- Las birrelaciones y multirrelaciones del contacto antiguo quedan vigentes

#### Caso de Error:
En MID existen:
- Contacto ID=1001, Identificación="123", UNG=100 (Vigente)
- Contacto ID=1002, Identificación="123", UNG=100 (Vigencia=Null, Contacto histórico)

Las birrelaciones de ID=1002 siguen vigentes → **BUG**

---

### BUG #4: Oracle (PDN) - Lógica Incompleta de Cierre de Personas
**Ubicación:** [ControladoraTransaccion.cs líneas 1880-1949 (IntegrarPDNRetirarPorInactivarContacto)](ControladoraTransaccion.cs#L1880-L1949)  
**Severidad:** CRÍTICA  

#### Problema:
```csharp
// Solo busca LAT_AGNPERSONA para la identificación + Código SIC del agente actual
List<EntidadesOracle.Persona.LatAgnPersona> lstLatAgnPersona = 
    BrokerConsulta.ConsultarInformacionPersonasNroIdentificacionAgente(
        identificacionContacto, 
        infoContactoRAG.Agente.ObtenerCodigoSicIntegracion());
```

**Falla porque:**
- Si el contacto fue creado con múltiples tipos de contacto pero algunos ya fueron inactivados
- Si la información de `LAT_AGNPERSONA` está asociada a múltiples agentes
- No busca TODAS las ocurrencias del contacto en Oracle
- Registros duplicados quedan activos

---

### BUG #5: Sin Implementación de Notificación C4
**Ubicación:** [RevisionSolicitudes.svc.cs línea 1729-2020](RevisionSolicitudes.svc.cs#L1729-L2020)  
**Severidad:** ALTA  

#### Problema:
El método NO implementa notificaciones a:
- `73000@isa.com.co` (Soporte)
- `atencionorientacionclientesxm@xm.com.co` (Atención clientes)
- Correos de analistas
- Notificación para finalizar en CRM

#### Requisito:
Enviar correo notificando:
- ID Solicitud
- Contacto retirado (Identificación, Nombre)
- Empresa (NIT, Razón Social)
- Agente/Unidad de Negocio
- Fecha de aprobación

---

## 3. IMPACTO EN BASES DE DATOS

### RAG (BDRAGXM)
| Tabla | Estado Actual | Estado Esperado |
|-------|---------------|-----------------|
| Preinscripcion | Vigentes (parcialmente) | Vigencias=0 para TODAS las versiones |
| InfoContacto | Vigencia incompleta | Vigencia=0 para TODAS las versiones |
| TipoInfoContacto | Vigencia parcial | Vigencia=0 para TODAS |
| SolicitudTipoInfoContacto | SIN CERRAR | Vigencia=0 para TODAS |
| InfoContactoNegocio | Vigencia parcial | Vigencia=0 para TODAS |
| AplicacionesPorContacto | Vigencia parcial | Vigencia=0 para TODAS |
| SolicitudAplicacionContacto | Vigencia parcial | Vigencia=0 para TODAS |

### MID (BDMIDXM)
| Tabla | Estado Actual | Estado Esperado |
|-------|---------------|-----------------|
| Contacto | Parcial | FechaFin para TODAS las versiones |
| Birrelacion | Solo agente actual | FechaFin para TODAS (Bir0036,Bir0064,Bir0491,Bir0119,Bir0025) |
| Multirrelacion | Solo agente actual | FechaFin para TODAS (Mrl0001-Mrl0005) |
| InformacionContacto | Parcial | FechaFin para TODAS |

### Oracle (BDPDN)
| Tabla | Estado Actual | Estado Esperado |
|-------|---------------|-----------------|
| LAT_AGNPERSONA | Parcial | FechaFin para TODAS |
| LAT_CONTACTOPERSONA | Parcial | FechaFinalContacto para TODAS |

---

## 4. REFACTORIZACIÓN REQUERIDA

### 4.1 Cambios en RevisionSolicitudes.RetirarContacto()

#### Paso 1: Buscar TODAS las versiones del contacto
```csharp
// Buscar TODOS los InfoContacto para esta identificación + agente
var todosLosContactos = realizacion
    .ObtenerTodosLosContactosPorIdentificacionYAgente(
        contacto.Identificacion, 
        solicitud.Agente.IdAgente)
    .ToList(); // Incluye vigentes e inactivos
```

#### Paso 2: Cerrar vigencias en bucle
```csharp
foreach (InfoContacto contactoAux in todosLosContactos)
{
    // Cerrar cada versión del contacto
    CerrarTodosLosRegistrosAsociadosAlContacto(contactoAux, fechaRetiroNow);
}
```

### 4.2 Nuevo Método Privado: CerrarTodosLosRegistrosAsociadosAlContacto()
```csharp
private void CerrarTodosLosRegistrosAsociadosAlContacto(
    InfoContacto contacto, 
    DateTime fechaRetiro)
{
    // 1. Cerrar Preinscripción
    // 2. Cerrar InfoContacto
    // 3. Cerrar TipoInfoContacto
    // 4. Cerrar SolicitudTipoInfoContacto
    // 5. Cerrar InfoContactoNegocio
    // 6. Cerrar AplicacionesPorContacto
    // 7. Cerrar SolicitudAplicacionContacto
}
```

### 4.3 Cambios en IntegrarMIDRetirarPorInactivarContacto()

**Antes:**
```csharp
EntidadesMID.Contacto contactoMID = 
    Broker.BrokerConsulta.ConsultarContactoPorIdentificacion(
        infoContacto.Identificacion);
```

**Después:**
```csharp
// Buscar TODOS los contactos para esa identificación EN LA UNG ESPECÍFICA
List<EntidadesMID.Contacto> lstContactosMID = 
    Broker.BrokerConsulta.ConsultarTodosLosContactosPorIdentificacionYUNG(
        infoContacto.Identificacion, 
        objIDUnidadNegocio);

// Iterar para cerrar cada uno
foreach (EntidadesMID.Contacto contactoMID in lstContactosMID)
{
    // Cerrar Birrelaciones
    // Cerrar Multirrelaciones
    // Cerrar Contacto
}
```

### 4.4 Cambios en IntegrarPDNRetirarPorInactivarContacto()

**Antes:**
```csharp
List<EntidadesOracle.Persona.LatAgnPersona> lstLatAgnPersona = 
    BrokerConsulta.ConsultarInformacionPersonasNroIdentificacionAgente(
        identificacionContacto, 
        infoContactoRAG.Agente.ObtenerCodigoSicIntegracion());
```

**Después:**
```csharp
// Buscar TODAS las personas (agentes) con esa identificación EN EL NEGOCIO
List<EntidadesOracle.Persona.LatAgnPersona> lstLatAgnPersona = 
    BrokerConsulta.ConsultarTodosLosAgentesPersonaNroIdentificacionTipoCodigo(
        identificacionContacto, 
        infoContactoRAG.Agente.ObtenerCodigoSicIntegracion());
```

### 4.5 Notificación C4 - Nuevo Método
```csharp
private void EnviarNotificacionRetiroContacto(
    Solicitud solicitud, 
    InfoContacto contacto, 
    DateTime fechaAprobacion)
{
    // Enviar a: 73000@isa.com.co, 
    //           atencionorientacionclientesxm@xm.com.co,
    //           correos de analistas
    
    // Contenido:
    // - ID Solicitud
    // - Contacto retirado
    // - Empresa
    // - Agente/UNG
    // - Fecha aprobación
}
```

---

## 5. MÉTODOS A CREAR/MODIFICAR EN DATA Access

### En RealizacionSolicitudes (Capa de Negocio):
1. `ObtenerTodosLosContactosPorIdentificacionYAgente()` - Busca TODAS las versiones
2. `ObtenerContactosPorIdentificacionEmpresaAgenteConVigencia()` - Incluye inactivos

### En BrokerConsulta (MID):
1. `ConsultarTodosLosContactosPorIdentificacionYUNG()` - TODAS las versiones
2. `ConsultarTodosLosBirrelacionesDelContactoEnUNG()` - TODAS las Bir
3. `ConsultarTodasLasMultirrelacionesDelContactoEnUNG()` - TODAS las Mrl
4. `ConsultarTodosLosInformacionesContactoEnUNG()` - TODAS las IC

### En BrokerConsulta (Oracle):
1. `ConsultarTodosLosAgentesPersonaNroIdentificacionTipoCodigo()` - TODAS las LAT_AGNPERSONA
2. `ConsultarTodosLosContactosPorIdentificacionYTipoCodigo()` - TODAS las LAT_CONTACTOPERSONA

---

## 6. MATRIZ DE CAMBIOS

| Componente | Archivo | Métodos | Cambios | Complejidad |
|-----------|---------|---------|---------|------------|
| Servicios | RevisionSolicitudes.svc.cs | RetirarContacto | Refactor lógica + nuevo método privado | ALTA |
| Negocio | ControladoraTransaccion.cs (MID) | IntegrarMIDRetirarPorInactivarContacto | Iterar múltiples contactos | MEDIA |
| Negocio | ControladoraTransaccion.cs (PDN) | IntegrarPDNRetirarPorInactivarContacto | Iterar múltiples personas | MEDIA |
| Data Access | BrokerConsulta (MID) | Nuevos métodos | 4 nuevos métodos query | MEDIA |
| Data Access | BrokerConsulta (PDN) | Nuevos métodos | 2 nuevos métodos query | MEDIA |
| Notificación | EmailService | EnviarNotificacionRetiroContacto | Nuevo servicio | BAJA |
| Tests | Test Suite | Múltiples | Crear tests unitarios | MEDIA |

---

## 7. ESTIMACIÓN DE TIEMPOS

### Desglose por Actividades

| # | Actividad | Horas | Notas |
|-|----------|-------|-------|
| **1** | **ANÁLISIS Y DISEÑO** | **16** | |
| 1.1 | Análisis detallado de flujos en 3 BD | 4 | RAG, MID, Oracle |
| 1.2 | Diseño de nuevos métodos de consulta | 3 | BrokerConsulta |
| 1.3 | Validación de reglas de negocio C1-C4 | 3 | Reuniones análisis |
| 1.4 | Documentación técnica de cambios | 2 | Wiki/Confluence |
| 1.5 | Diseño de casos de prueba | 4 | Matriz de pruebas |
| **2** | **DESARROLLO RAG** | **24** | |
| 2.1 | Refactor RetirarContacto() - lógica contactos | 6 | Múltiples versiones |
| 2.2 | Crear CerrarTodosLosRegistrosAsociadosAlContacto() | 5 | Cierre vigencias |
| 2.3 | Crear/Modificar métodos en RealizacionSolicitudes | 4 | Queries nuevas |
| 2.4 | Modificar Fachada (retiro contacto) | 3 | Nuevos métodos |
| 2.5 | Testing local RAG | 6 | QA scripts |
| **3** | **DESARROLLO MID** | **20** | |
| 3.1 | Refactor IntegrarMIDRetirarPorInactivarContacto() | 6 | Iterar múltiples |
| 3.2 | Crear nuevos métodos BrokerConsulta MID | 4 | 4 queries |
| 3.3 | Crear nuevos métodos BrokerTransaccion MID | 4 | Actualizar múltiples |
| 3.4 | Validar birrelaciones y multirrelaciones | 3 | Verificación lógica |
| 3.5 | Testing local MID | 3 | QA scripts |
| **4** | **DESARROLLO ORACLE (PDN)** | **20** | |
| 4.1 | Refactor IntegrarPDNRetirarPorInactivarContacto() | 6 | Iterar múltiples |
| 4.2 | Crear/Modificar BrokerConsulta Oracle | 4 | 2 queries nuevas |
| 4.3 | Crear nuevos métodos BrokerTransaccion Oracle | 3 | Actualizar LAT_AGNPERSONA, LAT_CONTACTOPERSONA |
| 4.4 | Validar cierre de personas | 3 | Verificación lógica |
| 4.5 | Testing local Oracle | 4 | QA scripts |
| **5** | **NOTIFICACIÓN C4** | **12** | |
| 5.1 | Crear método EnviarNotificacionRetiroContacto() | 4 | Servicio correo |
| 5.2 | Integrar en RetirarContacto() | 2 | Call al nuevo método |
| 5.3 | Validar plantilla correo | 2 | HTML/texto |
| 5.4 | Testing notificaciones | 4 | Envío correos |
| **6** | **TESTING INTEGRADO** | **32** | |
| 6.1 | Conducir prueba E2E completa (RAG+MID+Oracle) | 8 | Escenarios principales |
| 6.2 | Validar cierre de vigencias correctas | 6 | Data integrity |
| 6.3 | Validar NO cierre de otras unidades de negocio | 6 | Regla negocio |
| 6.4 | Validar notificaciones C4 | 4 | Correos + CRM |
| 6.5 | Testing casos edge (duplicados, históricos) | 5 | Casos problemáticos |
| 6.6 | Regresión de funcionalidades existentes | 3 | No breaking changes |
| **7** | **CORRECCIONES Y AJUSTES** | **16** | |
| 7.1 | Correcciones por bugs encontrados en QA | 8 | Iteración QA |
| 7.2 | Optimización de performance | 4 | Si aplica |
| 7.3 | Documentación de cambios JIRA | 2 | Cierre tickets |
| 7.4 | Preparación para producción | 2 | Scripts, rollback |
| **8** | **DESPLIEGUE Y VALIDACIÓN** | **12** | |
| 8.1 | Despliegue a ambiente PRE | 3 | DEV → PRE |
| 8.2 | Testing en PRE por equipo QA | 4 | Validación final |
| 8.3 | Ajustes por feedback PRE | 3 | Correcciones finales |
| 8.4 | Despliegue a PRODUCCIÓN | 2 | PRE → PROD |
| **TOTAL** | | **152 horas** | **~19 días (5 sprints de 8h)** |

---

### Cronograma Recomendado

```
Semana 1:
  - Lunes-Martes: Análisis y Diseño (16h) ✓
  - Miércoles-Viernes: Desarrollo RAG + MID (14h)

Semana 2:
  - Lunes-Miércoles: Desarrollo MID + Oracle (20h)
  - Jueves-Viernes: Desarrollo Oracle + Notificación (12h)

Semana 3:
  - Lunes-Jueves: Testing Integrado (24h)
  - Viernes: Correcciones menores (8h)

Semana 4:
  - Lunes-Martes: Correcciones QA (16h)
  - Miércoles: Despliegue PRE (3h)
  - Jueves: Testing PRE (4h)

Semana 5:
  - Lunes: Ajustes PRE (3h)
  - Martes: Despliegue PROD (2h)
```

---

### Recursos Requeridos

| Rol | Cantidad | Horas | Notas |
|-----|----------|-------|-------|
| Desarrollador Senior | 1 | 80 | Liderazgo + RAG/MID |
| Desarrollador Mid | 1 | 72 | MID/Oracle |
| QA Tester | 1 | 32 | Testing E2E |
| DBA/Soporte BD | 1 | 16 | Validación queries |
| **TOTAL** | **4** | **200h** | Más que codificación |

---

## 8. RECOMENDACIONES

### Críticas:
1. **NO** desplegar sin validar cierre de vigencias en las 3 BD
2. **Crear** scripts de validación post-deploy
3. **Implementar** logging detallado en cada cierre de vigencia
4. **Generar** reporte de validación antes de producción

### Mejoras Futuras:
1. Crear vista consolidada de ContactoVigencias (RAG)
2. Implementar auditoría de cambios en vigencias
3. Crear dashboard de inconsistencias
4. Automatizar validaciones diarias

---

## 9. ANEXOS

### A. Consultas SQL de Validación
```sql
-- RAG: Validar contactos duplicados vigentes
SELECT IdInfoContacto, Identificacion, IdAgente, IdEmpresa, Vigencia
FROM [BDRAGXM].[RAG].[InfoContacto]
WHERE Identificacion = @Identificacion 
  AND IdAgente = @IdAgente
  AND Vigencia = 1
ORDER BY FechaInicial DESC;

-- MID: Validar Bir duplicadas vigentes
SELECT ObjID, RelationshipName, DateEnd 
FROM dbo.Relationship
WHERE RelationshipRule IN ('Bir0036','Bir0064','Bir0491','Bir0119','Bir0025')
  AND ChildObjectID = @ContactoObjID
  AND DateEnd IS NULL;

-- Oracle: Validar LAT_AGNPERSONA vigentes
SELECT * FROM LAC.LAT_AGNPERSONA
WHERE NRO_IDENTIFICACION = @NroIdentificacion
  AND FECHAFIN IS NULL;
```

---

**Documento Generado:** 09-02-2026  
**Versión:** 1.0  
**Estado:** Análisis Completado
