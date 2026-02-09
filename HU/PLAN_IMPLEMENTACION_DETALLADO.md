# Plan de Implementación Detallado - HU Retiro de Contacto

**Documento:** Plan Implementación  
**Fecha:** 09-02-2026  
**Versión:** 1.0

---

## I. MATRIZ DE CAMBIOS POR COMPONENTE

### 1. CAPA DE SERVICIOS (XM.RAG.Servicios.svc)

#### 1.1 Archivo: RevisionSolicitudes.svc.cs

**Método a Refactorizar:** `RetirarContacto(decimal idSolicitud, string usuarioBitacora)`  
**Ubicación:** Líneas 1729-2020  
**Cambios:**

| Cambio | Línea | Tipo | Descripción |
|--------|-------|------|-------------|
| CHG-001 | 1729 | Refactor | Modificar lógica de búsqueda de contactos |
| CHG-002 | 1762-1804 | Refactor | Cambiar de bucle simple a bucle iterativo |
| CHG-003 | 1790 | Delete | Eliminar cierre único del contacto actual |
| CHG-004 | 1799 | Add | Nuevo método privado: `CerrarTodosLosRegistrosDelContacto()` |
| CHG-005 | 1810-1890 | Refactor | Adaptar cierre de vigencias iterativo |
| CHG-006 | 1920 | Add | Llamada a nueva notificación C4 |
| CHG-007 | 2000 | Add | Nuevo método: `EnviarNotificacionRetiroContacto()` |

**Pseudocódigo de Cambios:**

```csharp
// CAMBIO CHG-001: Búsqueda mejorada
// Antes:
var contacto = realizacion.ObtenerContactoPorId((int)solicitud.IdInfoContacto);

// Después:
var todosLosContactos = realizacion
    .ObtenerTodosLosContactosPorIdentificacionYAgente(
        solicitud.InfoContacto.Identificacion,
        solicitud.Agente.IdAgente);

// CAMBIO CHG-002-005: Cierre iterativo
foreach (var contacto in todosLosContactos)
{
    CerrarTodosLosRegistrosDelContacto(contacto, fechaRetiroNow, solicitud);
}

// CAMBIO CHG-006: Notificación
EnviarNotificacionRetiroContacto(
    solicitud, 
    solicitud.InfoContacto, 
    fechaRetiroNow);
```

---

### 2. CAPA DE NEGOCIO (XM.RAG.RevisionSolicitudes.Negocio)

#### 2.1 Archivo: RealizacionSolicitudes.cs

**Nuevos Métodos a Crear:**

| Método | Parámetros | Retorno | Descripción |
|--------|-----------|---------|-------------|
| `ObtenerTodosLosContactosPorIdentificacionYAgente` | `string identificacion, int idAgente` | `List<InfoContacto>` | Busca TODAS las versiones históricas |
| `ObtenerContactosPorIdentificacionYEmpresa` | `string identificacion, int idEmpresa, bool incluirInactivos` | `List<InfoContacto>` | Busca por empresa |
| `ObtenerSolicitudTipoInfoContactoPorContacto` | `int idInfoContacto` | `List<SolicitudTipoInfoContacto>` | Todas las solicitudes asociadas |

**Pseudo-SQL:**

```sql
-- ObtenerTodosLosContactosPorIdentificacionYAgente
SELECT *
FROM [BDRAGXM].[RAG].[InfoContacto]
WHERE Identificacion = @identificacion
  AND IdAgente = @idAgente
ORDER BY FechaInicial DESC;
```

---

#### 2.2 Archivo: ControladoraRevisionSolicitudes.cs

**Nuevos Métodos a Crear/Modificar:**

| Método | Cambio | Descripción |
|--------|--------|-------------|
| `RetiroContactoInactivarPreinscripcionCompleto` | NEW | Cierra versión por identificación + empresa |
| `RetiroContactoInactivarInfoContactoCompleto` | NEW | Cierra todas las vigencias |
| `RetiroContactoInactivarTiposContactoCompleto` | NEW | Itera múltiples contactos |
| `RetiroContactoInactivarSolicitudTipoContactoCompleto` | NEW | Cierra todas las solicitudes |
| `RetiroContactoInactivarInfoContactoNegocioCompleto` | NEW | Cierra todas las asociaciones negocio |
| `RetiroContactoInactivarAplicacionesCompleto` | NEW | Cierra todas las aplicaciones |
| `RetiroContactoInactivarSolicitudAplicacionCompleto` | NEW | Cierra todas las solicitud-aplicación |

---

### 3. CAPA DE NEGOCIO (XM.RAG.IntegracionMID.Negocio)

#### 3.1 Archivo: ControladoraTransaccion.cs (MID)

**Método a Refactorizar:** `IntegrarMIDRetirarPorInactivarContacto()`  
**Ubicación:** Líneas 873-923  

**Cambios:**

| Cambio | Línea | Tipo | Descripción |
|--------|-------|------|-------------|
| CHG-M001 | 883 | Refactor | Buscar TODOS los contactos en UNG |
| CHG-M002 | 890-910 | Refactor | Iterar múltiples contactos |
| CHG-M003 | 903-915 | Refactor | Cerrar Bir/Mrl para cada contacto |

**Pseudo-código:**

```csharp
// ANTES: Solo busca 1 contacto
var contactoMID = Broker.BrokerConsulta
    .ConsultarContactoPorIdentificacion(infoContacto.Identificacion);

// DESPUÉS: Busca TODAS las versiones en la UNG
var lstContactosMID = Broker.BrokerConsulta
    .ConsultarTodosLosContactosPorIdentificacionYUNG(
        infoContacto.Identificacion, 
        objIDUnidadNegocio);

// Loop para cerrar cada uno
foreach (var contactoMID in lstContactosMID)
{
    // Cerrar Birrelaciones
    Broker.BrokerTransaccion.RetiroPorInactivacionContacto
        CerrarVigenciaBirrelacionContacto(
            objIDUnidadNegocio, 
            contactoMID.ObjID, 
            fechaRetiro);
    
    // Cerrar Multirrelaciones
    Broker.BrokerTransaccion.CerrarVigenciaMultirrelacionContacto_Ung_InfoContacto(
        contactoMID.ObjID, 
        fechaRetiro);
    
    Broker.BrokerTransaccion.RetiroPorInactivacionContactoMultirrelacionContacto(
        contactoMID.ObjID, 
        fechaRetiro);
}
```

---

#### 3.2 Archivo: BrokerConsulta.cs (MID)

**Nuevos Métodos a Crear:**

| Método | Parámetros | Retorno | SQL Query |
|--------|-----------|---------|-----------|
| `ConsultarTodosLosContactosPorIdentificacionYUNG` | `identificacion, objIDUNG` | `List<Contacto>` | Busca con `DateEnd IS NULL` y `DateEnd IS NOT NULL` |
| `ConsultarTodosBirrelacionesDelContactoEnUNG` | `objIDContacto, objIDUNG` | `List<Relationship>` | Bir0036, Bir0064, Bir0491, Bir0119, Bir0025 |
| `ConsultarTodasMultirrelacionesDelContactoEnUNG` | `objIDContacto, objIDUNG` | `List<RelationshipMulti>` | Mrl0001-0005 |
| `ConsultarTodosInformacionContactoEnUNG` | `objIDContacto, objIDUNG` | `List<InformacionContacto>` | Todas las instancias |

---

### 4. CAPA DE NEGOCIO (XM.RAG.IntegracionPDN.Negocio)

#### 4.1 Archivo: ControladoraTransaccion.cs (Oracle)

**Método a Refactorizar:** `IntegrarPDNRetirarPorInactivarContacto()`  
**Ubicación:** Líneas 1880-1949  

**Cambios:**

| Cambio | Línea | Tipo | Descripción |
|--------|-------|------|-------------|
| CHG-O001 | 1890 | Refactor | Buscar TODOS los LAT_AGNPERSONA |
| CHG-O002 | 1905-1930 | Refactor | Iterar múltiples personas |
| CHG-O003 | 1915 | Refactor | Cierre de contactospersona |

**Pseudo-código:**

```csharp
// ANTES: Solo busca personas para 1 agente
var lstLatAgnPersona = BrokerConsulta
    .ConsultarInformacionPersonasNroIdentificacionAgente(
        identificacionContacto, 
        infoContactoRAG.Agente.ObtenerCodigoSicIntegracion());

// DESPUÉS: Busca TODAS las personas
var lstLatAgnPersona = BrokerConsulta
    .ConsultarTodosLosAgentesPersonaNroIdentificacion(
        identificacionContacto,
        infoContactoRAG.Agente.ObtenerCodigoSicIntegracion());

// Loop para cerrar cada uno
foreach (var latAgnPersona in lstLatAgnPersona)
{
    latAgnPersona.FechaFin = fechaRetiro;
    latAgnPersona.FechaModificacion = fechaRetiro;
    latAgnPersona.UsuarioModificacion = bitacora.Usuario;
    BrokerTransaccion.ActualizarInfoPersona(latAgnPersona);
}
```

---

#### 4.2 Archivo: BrokerConsulta.cs (Oracle)

**Nuevos Métodos a Crear:**

| Método | Parámetros | Retorno | SQL Query |
|--------|-----------|---------|-----------|
| `ConsultarTodosLosAgentesPersonaNroIdentificacion` | `nroIdentificacion, codigoSic` | `List<LatAgnPersona>` | TODAS las LAT_AGNPERSONA |
| `ConsultarTodosLosContactosPersonaNroIdentificacion` | `nroIdentificacion, codigoSic` | `List<LatContactoPersona>` | TODAS las LAT_CONTACTOPERSONA |

---

### 5. CAPA DE ACCESO A DATOS (Data Access)

#### 5.1 DAO - RAG

**Tablas Afectadas:**
- `Preinscripcion` (Lectura/Actualización)
- `InfoContacto` (Lectura/Actualización)
- `TipoInfoContacto` (Lectura/Actualización)
- `SolicitudTipoInfoContacto` (Lectura/Actualización)
- `InfoContactoNegocio` (Lectura/Actualización)
- `AplicacionesPorContacto` (Lectura/Actualización)
- `SolicitudAplicacionContacto` (Lectura/Actualización)

**Queries a Crear:**

```sql
-- Q-RAG-001: Obtener todas las versiones del contacto
SELECT IdInfoContacto, Identificacion, IdAgente, IdEmpresa, Vigencia, Estado
FROM [BDRAGXM].[RAG].[InfoContacto]
WHERE Identificacion = @Identificacion 
  AND IdAgente = @IdAgente
ORDER BY FechaInicial DESC;

-- Q-RAG-002: Obtener tipos por contacto (todas las versiones)
SELECT IdTipoInfoContacto, IdInfoContacto, Vigencia
FROM [BDRAGXM].[RAG].[TipoInfoContacto]
WHERE IdInfoContacto IN (
    SELECT IdInfoContacto
    FROM [BDRAGXM].[RAG].[InfoContacto]
    WHERE Identificacion = @Identificacion AND IdAgente = @IdAgente
)
ORDER BY FechaInicial DESC;

-- Q-RAG-003: Actualizar vigencias (todas las versiones)
UPDATE [BDRAGXM].[RAG].[TipoInfoContacto]
SET Vigencia = 0, Editable = 0, FechaFinal = @FechaFinal
WHERE IdInfoContacto IN (
    SELECT IdInfoContacto
    FROM [BDRAGXM].[RAG].[InfoContacto]
    WHERE Identificacion = @Identificacion AND IdAgente = @IdAgente
)
AND Vigencia = 1;
```

---

## II. ROADMAP DE IMPLEMENTACIÓN

### Fase 1: Preparación (2 días)
```
DÍA 1:
  ├─ Análisis detallado flujos
  ├─ Diseño de nuevos métodos
  ├─ Validación reglas negocio
  └─ Creación de scripts de validación

DÍA 2:
  ├─ Setup ambiente de desarrollo
  ├─ Preparación de test data
  ├─ Creación de branches git
  └─ Documentación final diseño
```

### Fase 2: Desarrollo RAG (3 días)
```
DÍA 3:
  ├─ Crear métodos en RealizacionSolicitudes
  ├─ Refactor RetirarContacto() - Parte 1
  └─ Unit tests clase

DÍA 4:
  ├─ Refactor RetirarContacto() - Parte 2
  ├─ Crear método CerrarTodosLosRegistros()
  ├─ Validar lógica iterativa
  └─ Testing local RAG

DÍA 5:
  ├─ Correcciones por QA
  ├─ Optimización queries
  ├─ Documentation
  └─ Ready for integration
```

### Fase 3: Desarrollo MID (3 días)
```
DÍA 6:
  ├─ Crear nuevos métodos BrokerConsulta
  ├─ Refactor ControladoraTransaccion MID
  └─ Unit tests

DÍA 7:
  ├─ Validar Bir/Mrl closing
  ├─ Testing iterativo
  ├─ Correcciones
  └─ Integration testing

DÍA 8:
  ├─ Performance testing
  ├─ Edge cases
  └─ Ready for merge
```

### Fase 4: Desarrollo Oracle (3 días)
```
DÍA 9:
  ├─ Crear nuevos métodos BrokerConsulta
  ├─ Refactor ControladoraTransaccion PDN
  └─ Unit tests

DÍA 10:
  ├─ Validar LAT_AGNPERSONA closing
  ├─ Testing iterativo
  ├─ Correcciones
  └─ Validar integridad datos

DÍA 11:
  ├─ Implementar notificación C4
  ├─ Testing end-to-end
  ├─ Documentación
  └─ Code review
```

### Fase 5: Testing Integrado (4 días)
```
DÍA 12:
  ├─ E2E RAG + MID + Oracle
  ├─ Validar vigencias
  ├─ Validar relaciones
  └─ Casos normales

DÍA 13:
  ├─ Edge cases (duplicados, históricos)
  ├─ Validar NO cierre otras UNG
  ├─ Regression testing
  └─ Performance load testing

DÍA 14:
  ├─ Validar notificaciones
  ├─ Testing con datos reales (sanitizados)
  ├─ Correcciones finales
  └─ Sign-off QA

DÍA 15:
  ├─ Despliegue PRE
  ├─ Smoke testing
  ├─ Ajustes PRE
  └─ Ready for PROD
```

### Fase 6: Despliegue (1 día)
```
DÍA 16:
  ├─ Backup PROD
  ├─ Despliegue PROD
  ├─ Validación post-deploy
  ├─ Monitoreo
  └─ Rollback plan ready
```

---

## III. LISTA DE VERIFICACIÓN PRE-DESPLIEGUE

### Validaciones Funcionales
- [ ] Contacto único en 1 UNG - Se cierra correctamente
- [ ] Contacto en múltiples UNG - Solo se cierra en UNG de la solicitud
- [ ] Múltiples versiones del contacto - Se cierran TODAS
- [ ] Contactos sin Bir/Mrl - Se inactivan correctamente
- [ ] Contactos con Bir/Mrl múltiples - Se cierran TODAS
- [ ] Notificación C4 enviada a todos los buzones
- [ ] Notificación incluye información correcta

### Validaciones Técnicas
- [ ] No hay breaking changes en métodos existentes
- [ ] Logs de auditoría registran cada cierre de vigencia
- [ ] Queries optimizadas (índices válidos)
- [ ] Transacciones ACID garantizadas
- [ ] Rollback scripts probados

### Validaciones de Datos
- [ ] RAG: 0 vigencias abiertas para contacto retirado
- [ ] MID: 0 Bir/Mrl abiertas para contacto retirado
- [ ] Oracle: 0 LAT_AGNPERSONA abiertas para persona retirada
- [ ] No hay inconsistencias entre las 3 BD

### Validaciones de Performance
- [ ] Tiempo promedio < 5 segundos
- [ ] Máximo de vigencias cerradas por solicitud: 100
- [ ] CPU utilization < 80%
- [ ] Memory utilization < 70%

---

## IV. SCRIPTS DE VALIDACIÓN POST-DESPLIEGUE

### Script 1: Verificar Vigencias Cerradas - RAG
```sql
-- Ejecutar 1 hora después del despliegue
SELECT 
    'ALERTA: Vigencias abiertas después de retiro' as Alerta,
    Count(*) as Cantidad
FROM [BDRAGXM].[RAG].[InfoContacto] ic
WHERE ic.Identificacion = @IdentificacionContactoRetirado
  AND ic.IdAgente = @IdAgenteRetiro
  AND ic.Vigencia = 1
  AND ic.FechaFinal IS NULL;
```

### Script 2: Verificar Birrelaciones Cerradas - MID
```sql
SELECT 
    'ALERTA: Birrelaciones abiertas después de retiro' as Alerta,
    Count(*) as Cantidad
FROM dbo.Relationship
WHERE ChildObjectID = @ContactoObjID
  AND RelationshipRule IN ('Bir0036','Bir0064','Bir0491','Bir0119','Bir0025')
  AND DateEnd IS NULL;
```

### Script 3: Verificar Personas Cerradas - Oracle
```sql
SELECT 
    'ALERTA: LAT_AGNPERSONA abiertas después de retiro' as Alerta,
    Count(*) as Cantidad
FROM LAC.LAT_AGNPERSONA
WHERE NRO_IDENTIFICACION = @NroIdentificacion
  AND CODSIC = @CodigoSIC
  AND FECHAFIN IS NULL;
```

---

## V. CONTINGENCIA Y ROLLBACK

### Plan Rollback
```
1. Identificar error en PROD
2. Ejecutar script de rollback (depositar vigencias=1)
3. Restaurar desde backup si aplicable
4. Notificar a stakeholders
5. Revert despliegue a versión anterior
6. Investigar en ambiente PRE
```

### Time to Rollback
- Detección: 15 minutos
- Decisión: 5 minutos
- Ejecución: 30 minutos
- Validación: 15 minutos
- **Total: ~65 minutos**

---

**Documento Completado:** 09-02-2026  
**Próximo paso:** Iniciar Fase 1 (Preparación)
