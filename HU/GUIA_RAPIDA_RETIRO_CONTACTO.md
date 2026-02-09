# GUÍA RÁPIDA - HU RETIRO DE CONTACTO
## Checklist de Referencia Rápida

**Última Actualización:** 09-02-2026  
**Duración Lectura:** 5 minutos  

---

## ⚡ TL;DR (MUY RESUMIDO)

| Aspecto | Status |
|--------|--------|
| **Bugs Encontrados** | 5 CRÍTICOS |
| **Tiempo Estimado** | 152 horas (19 días) |
| **Recursos** | 4 personas |
| **Costo** | ~$10,280 USD |
| **Riesgo** | ALTO (integridad de datos) |
| **Prioridad** | 🔴 CRÍTICA |
| **ROI** | 3-4 meses |

---

## 🐛 LOS 5 BUGS EN 1 LÍNEA c/u

1. **RAG Bug #1:** No busca múltiples versiones del contacto
2. **RAG Bug #2:** No itera sobre todas las vigencias (7 tablas)
3. **MID Bug #3:** No busca múltiples contactos en la UNG
4. **Oracle Bug #4:** No busca múltiples personas por identificación
5. **Notif Bug #5:** No envía correos a stakeholders (C4)

---

## 📂 DOCUMENTACIÓN

### Status: ✅ COMPLETADA

```
c:\RAG\RAGV2\RAG\
├── ANALISIS_BUGS_RETIRO_CONTACTO.md         (Análisis técnico detallado)
├── PLAN_IMPLEMENTACION_DETALLADO.md         (Plan ejecutivo + roadmap)
├── RESUMEN_EJECUTIVO_ESTIMACION.md          (Resumen + timeline)
├── PRESENTACION_HALLAZGOS.md                (Para presentar a jefatura)
└── GUIA_RAPIDA_RETIRO_CONTACTO.md           (Este documento)
```

### Recomendación de Lectura

1. **Primero:** `PRESENTACION_HALLAZGOS.md` (5 min)
2. **Luego:** `RESUMEN_EJECUTIVO_ESTIMACION.md` (10 min)
3. **Detalle:** `ANALISIS_BUGS_RETIRO_CONTACTO.md` (30 min)
4. **Implementación:** `PLAN_IMPLEMENTACION_DETALLADO.md` (Al iniciar)

---

## 🎯 CRITERIOS DE ACEPTACIÓN (AC)

### AC1: RAG - Todas las vigencias cerradas
```
✓ Preinscripcion v1-v10 → Cierre
✓ InfoContacto v1-v10 → Cierre
✓ TipoInfoContacto v1-v10 → Cierre
✓ SolicitudTipoInfoContacto v1-v10 → Cierre
✓ InfoContactoNegocio v1-v10 → Cierre
✓ AplicacionesPorContacto v1-v10 → Cierre
✓ SolicitudAplicacionContacto v1-v10 → Cierre
```

### AC2: MID - Relaciones cerradas
```
✓ Bir0036, 0064, 0491, 0119, 0025 → Cierre
✓ Mrl0001, 0002, 0003, 0004, 0005 → Cierre
✓ InformacionContacto → Cierre
✓ Contacto (si es único) → Cierre
```

### AC3: Oracle - Personas cerradas
```
✓ LAT_AGNPERSONA (todas) → FechaFin = fecha retiro
✓ LAT_CONTACTOPERSONA (todas) → FechaFin = fecha retiro
```

### AC4: Notificación
```
✓ Email a: 73000@isa.com.co
✓ Email a: atencionorientacionclientesxm@xm.com.co
✓ Email a: Correos analistas
✓ Contenido: ID Solicitud, Contacto, Empresa, Fecha
```

---

## 📊 TIMELINE RESUMIDO

```
SEMANA 1: Análisis + RAG & MID          (40h - 2 devs)
SEMANA 2: MID + Oracle + Notif          (44h - 2 devs)
SEMANA 3: Testing E2E + Correcciones    (40h - QA + Dev)
SEMANA 4: Despliegue PRE → PROD         (28h - Dev + DBA)
─────────────────────────────────────────────────────
TOTAL: 152 horas | 19 días | 4 personas
```

---

## 🔄 CAMBIOS POR COMPONENTE

### Archivos a Modificar/Crear

| Componente | Archivo | Cambios | Est(h) |
|-----------|---------|---------|--------|
| Servicios | RevisionSolicitudes.svc.cs | 7 cambios | 10 |
| Negocio-RAG | RealizacionSolicitudes.cs | 3 nuevos | 6 |
| Negocio-RAG | ControladoraRevisionSolicitudes.cs | 7 nuevos | 8 |
| Negocio-MID | ControladoraTransaccion.cs | Refactor | 6 |
| Data-MID | BrokerConsulta.cs | 4 nuevos | 8 |
| Negocio-PDN | ControladoraTransaccion.cs | Refactor | 6 |
| Data-PDN | BrokerConsulta.cs | 2 nuevos | 6 |
| Notificación | EmailService.cs | Nuevo método | 4 |
| Testing | Test Suite | 26 casos | 16 |

**Total:** 13 archivos | 52 cambios | ~152h

---

## 🚀 GO/NO-GO CHECKLIST

### Funcional (Antes de PROD)
- [ ] AC1 validado ✓
- [ ] AC2 validado ✓
- [ ] AC3 validado ✓
- [ ] AC4 validado ✓
- [ ] 0 bugs críticos
- [ ] 0 bugs altos sin mitigación

### Técnico
- [ ] Code review 100%
- [ ] Test coverage > 80%
- [ ] Performance OK (< 5 seg)
- [ ] Logs habilitados

### Datos
- [ ] Validación RAG OK
- [ ] Validación MID OK
- [ ] Validación Oracle OK
- [ ] Backup PROD OK
- [ ] Scripts rollback probados

### Operacional
- [ ] Runbook listo
- [ ] On-call 24/7
- [ ] Alertas enabled
- [ ] Stakeholders notificados

---

## 🆘 ESCALACIÓN RÁPIDA

### Si algo falla en PROD

```
Minuto 0: Detectar error
  └─ Síntoma: Vigencias no cierran correctamente
  └─ Alert: Revisar logs de RetirarContacto()

Minuto 5: Notificar
  └─ Dev Lead → Activar rollback
  └─ DBA → Preparar scripts restore

Minuto 30: Ejecutar rollback
  └─ Revert deployment a versión anterior
  └─ Restaurar datos si es necesario

Minuto 65: Investigación
  └─ Post-mortem en PRE
  └─ Identificar root cause
  └─ Corregir y retesting
```

**Time to Resume Normal:** ~65 minutos

---

## 💾 SCRIPTS DE VALIDACIÓN RÁPIDA

### Script RAG: ¿Hay vigencias abiertas?
```sql
SELECT COUNT(*) as ViVigenciasAbiertas
FROM [BDRAGXM].[RAG].[InfoContacto]
WHERE Identificacion = '123456789'
  AND IdAgente = 100
  AND Vigencia = 1
  AND FechaFinal IS NULL;
-- Esperado: 0
```

### Script MID: ¿Hay Bir/Mrl abiertas?
```sql
SELECT COUNT(*) as BirMrlAbiertas
FROM dbo.Relationship
WHERE ChildObjectID = 'ObjID_Contacto'
  AND DateEnd IS NULL;
-- Esperado: 0
```

### Script Oracle: ¿Hay personas sin FechaFin?
```sql
SELECT COUNT(*) as PersonasSinFechaFin
FROM LAC.LAT_AGNPERSONA
WHERE NRO_IDENTIFICACION = '123456789'
  AND FECHAFIN IS NULL;
-- Esperado: 0
```

---

## 📞 CONTACTOS CLAVE

### Equipo de Desarrollo
- **Senior Dev**: [Responsable RAG/MID]
- **Mid Dev**: [Responsable MID/Oracle]
- **QA Lead**: [Testing]
- **DBA**: [Soporte BD]

### Stakeholders
- **Soporte**: 73000@isa.com.co
- **Atención Clientes**: atencionorientacionclientesxm@xm.com.co
- **Analistas**: [Correos equipo]

---

## ⚙️ CONFIGURACIÓN PRE-REQUISITOS

### Acceso Necesario
- [ ] DEV: RAG, MID, Oracle (full access)
- [ ] PRE: RAG, MID, Oracle (full access)
- [ ] PROD: RAG, MID, Oracle (ejecución scripts)

### Herramientas
- [ ] SSMS (SQL Server)
- [ ] SQL*Plus u otra herramienta Oracle
- [ ] Git (control de versiones)
- [ ] VS 2019+ (desarrollo C#)
- [ ] NUnit (testing)

### Datos Necesarios
- [ ] Script seed data (contactos de prueba)
- [ ] Query de contactos con múltiples versiones
- [ ] Lista de birrelaciones por tipo
- [ ] Mapeo tipos contacto → tablas

---

## 📈 MÉTRICAS POST-DESPLIEGUE

### Validar Después de Despliegue

| Métrica | Antes | Después | Target |
|---------|-------|---------|--------|
| Registros huérfanos | 85%+ | ? | 0% |
| Inconsistencias BD | Alto | ? | Bajo |
| Retrabajos/mes | 3-4 | ? | 0 |
| Tiempo retiro contacto | 2-3h | ? | <5min |

---

## 🎓 LECCIONES APRENDIDAS

### Error Principal
```
❌ Asumir que 1 búsqueda = todos los registros
✅ Correcto: Buscar TODOS, iterar, cerrar TODOS
```

### Patrón Correcto
```
Para cada versión del recurso:
  1. Buscar todas las asociaciones
  2. Cerrar todas las vigencias
  3. Validar 0 registros abiertos
```

---

## 🔐 SEGURIDAD Y AUDITORÍA

### Logging Requerido
- [ ] Cada cierre de vigencia debe registrarse
- [ ] Usuario y fecha de cierre
- [ ] ID de solicitud que generó el cierre
- [ ] Número de registros afectados

### Auditoría
- [ ] Bitácora de cambios en [BDRAGXM].[RAG].[Bitacora]
- [ ] Trazabilidad en MID
- [ ] Trazabilidad en Oracle

---

## ✅ LISTA DE VERIFICACIÓN FINAL

Antes de PRODUCCIÓN:

- [ ] Análisis completado y validado
- [ ] Diseño técnico aprobado
- [ ] Código revisado por 2+ seniors
- [ ] Tests 100% pass rate
- [ ] Performance validated
- [ ] Rollback probado
- [ ] Stakeholders notificados
- [ ] Cronograma confirmado
- [ ] Recursos reservados
- [ ] Window de despliegue definido

---

## 📝 NOTAS IMPORTANTES

1. **Crítico:** Este bug afecta integridad de 3 bases de datos
2. **Urgente:** Iniciar lo antes posible
3. **Testing:** Exhaustivo (26 casos de prueba)
4. **Rollback:** Plan activo y probado
5. **Comunicación:** Stakeholders informados

---

## 🎯 ACCIÓN REQUERIDA

### HOY
- [ ] Revisar `PRESENTACION_HALLAZGOS.md`
- [ ] Compartir con jefatura técnica
- [ ] Validar hallazgos

### ESTA SEMANA
- [ ] Aprobación presupuesto
- [ ] Reservar equipo
- [ ] Socializar cambios

### PRÓXIMA SEMANA
- [ ] Iniciar desarrollo
- [ ] Setup ambiente
- [ ] Comenzar Fase 1

---

## 📚 REFERENCIAS

1. **HU Original:** HU-303573 - Retiro Contacto por Inactivación
2. **Código Actual:** [RevisionSolicitudes.svc.cs](RevisionSolicitudes.svc.cs#L1729)
3. **Documento Análisis:** ANALISIS_BUGS_RETIRO_CONTACTO.md
4. **Plan Implementación:** PLAN_IMPLEMENTACION_DETALLADO.md

---

**Preparado por:** Análisis Técnico  
**Fecha:** 09-02-2026  
**Versión:** 1.0  
**Estado:** ✅ COMPLETADO

