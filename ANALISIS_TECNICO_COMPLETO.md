# ANÁLISIS TÉCNICO COMPLETO - SOLUCIONES .NET XM.RAG

**Fecha del análisis:** 8 de Febrero, 2026  
**Alcance:** Dos soluciones .NET principales  
**Total de proyectos analizados:** 28  

---

## 1. RESUMEN GENERAL

| Solución | Proyectos | Framework | Tipo Principal |
|----------|-----------|-----------|-----------------|
| **XM.RAG** | 6 | v3.5 / v4.0 | SharePoint + Framework |
| **XM.RAG.Servicios** | 22 | v4.0 | Servicios WCF + Datos + Negocio |
| **TOTAL** | **28** | Mixtos | Arquitectura multicapa |

---

## 2. LISTADO COMPLETO DE PROYECTOS - SOLUCIÓN XM.RAG

### 2.1 Proyecto: XM.RAG

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG\XM.RAG.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v3.5 |
| **RootNamespace** | XM.RAG |
| **AssemblyName** | XM.RAG |
| **Archivo .csproj** | XM.RAG.csproj |
| **Líneas en .csproj** | 4451 |

**Configuración:**
- **SignAssembly:** true
- **AssemblyOriginatorKeyFile:** key.snk
- **ProjectTypeGuids:** SharePoint project (BB1F664B-9266-4fd6-B973-E1E44974B511)

**Estadísticas:**
- **Archivos .cs:** 229 archivos
- **Archivos .ascx:** 45 (User Controls)
- **Archivos .aspx:** 56 (Páginas)
- **Archivos de configuración:** 2 (app.config, packages.config)

**Estructura de directorios principales:**
- `Util/` - Clases utilitarias
- `Layouts/RAG/` - Páginas de SharePoint
  - `Solicitud/` - Formularios de solicitud (14 páginas)
  - `Revision/` - Páginas de revisión (9 páginas)
  - `Parametros/` - Páginas de parametrización (10 páginas)
  - `Administracion/` - Consolas administrativas (6 páginas)
  - `Certificados/` - Generación de certificados (1 página)
  - `Informes/` - Reportes (3 páginas)
  - `Intervencion/` - Intervención de empresas (3 páginas)
  - `Comun/Util/` - Utilidades comunes (1 página)
- `ControlTemplates/RAG/` - Controles reutilizables (34 .ascx)
  - `Comun/` - Controles comunes (12 .ascx)
  - `Solicitud/` - Controles de solicitud (15 .ascx)
  - `Revision/` - Controles de revisión (3 .ascx)
  - `Logs/` - Log utilities
  - `ValidacionesSDAO/` - Validaciones
  - `DocumentoSPDAO/` - Documentos en SharePoint
- `Provisioning/` - Configuración de SharePoint
  - `WebParts/` - WebParts personalizados (2 WebParts)
  - `Features/RAG/` - Feature de RAG
  - `Listas/` - Definiciones de listas (7 listas)
  - `Bibliotecas/` - Bibliotecas de documentos (3 bibliotecas)
- `Helper/` - Clases auxiliares
  - `Parametros/` - Clases de parámetros (4 clases)
  - `Eventos/` - Event Receivers
- `Service References/` - Referencias a servicios WCF (7 referencias)
  - ServiceGeneral
  - ServiceIntegracionMID (2 versiones)
  - ServiceAdministracion
  - ServiceRevisionSolicitudes
  - ServiceRealizacionSolicitudes (3 versiones)
  - CertificadoDigitalService
- `Web References/` - Referencias legadas web services
  - Reporting

**Referencias principales en .csproj:**
- `itextsharp` v5.5.0.0 (PDF generation)
- `itextsharp.xmlworker` v5.5.0.0
- `Microsoft.ReportViewer.WebForms` v10.0.0.0
- `Microsoft.SharePoint` v14.0.0.0 (SharePoint 2010)
- `Microsoft.SharePoint.Security` v14.0.0.0
- `Microsoft.Web.CommandUI` v14.0.0.0
- `Telerik.Web.UI` v2016.1.225.35 (UI controls)
- `System.Web.Extensions`, `System.ServiceModel`, `System.Runtime.Serialization`

---

### 2.2 Proyecto: XM.RAG.Framework

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG.Framework\XM.RAG.Framework.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v3.5 |
| **RootNamespace** | XM.RAG.Framework |
| **AssemblyName** | XM.RAG.Framework |
| **AssemblyOriginatorKeyFile** | KeyRAGFramework.snk |
| **Líneas en .csproj** | 270 |

**Características:**
- Contiene clases base de framework para XM.RAG
- Incluye utilidades de SharePoint
- Manejo de configuración y exceptions

**Referencias principales:**
- `itextsharp`
- `itextsharp.xmlworker`
- `Microsoft.Practices` Enterprise Library (Logging, Caching, etc.)
- `Microsoft.SharePoint`

---

### 2.3 Proyecto: XM.RAG.TimerJobs

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG.TimerJobs\XM.RAG.TimerJobs.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v3.5 |
| **RootNamespace** | XM.RAG.TimerJobs |
| **AssemblyName** | XM.RAG.TimerJobs |
| **AssemblyOriginatorKeyFile** | key.snk |
| **Líneas en .csproj** | 880 |

**Propósito:**
- Timer Jobs para SharePoint (tareas programadas)
- Ejecución de Jobs en segundo plano

**Referencias:**
- `Microsoft.Practices.SharePoint.Common` v2.0.0.0
- `Microsoft.SharePoint`
- Enterprise Library references

---

### 2.4 Proyecto: Unisys.Controls

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\Unisys.Controls\Unisys.Controls.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v3.5 |
| **RootNamespace** | Unisys.Controls |
| **AssemblyName** | Unisys.Controls |
| **ProjectTypeGuids** | Web Application Project |
| **AssemblyOriginatorKeyFile** | key.snk |
| **Líneas en .csproj** | 151 |

**Propósito:**
- Biblioteca de controles web personalizados
- Incluye controles ASCX reutilizables

**Controles incluidos:**
- `Seccion.ascx` - Control de sección
- `Mensajes.ascx` - Control de mensajes
- `LineaTiempo.ascx` - Timeline component

**Referencias:**
- `Microsoft.SharePoint`
- `Microsoft.Web.CommandUI`
- System.Web.Extensions

**Archivos de configuración:**
- `Web.config`
- `Web.Debug.config`
- `Web.Release.config`

---

### 2.5 Proyecto: XM.RAG.SharePointDataAccess

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG.SharePointDataAcces\XM.RAG.SharePointDataAccess.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v3.5 |
| **RootNamespace** | XM.RAG.SharePointDataAccess |
| **AssemblyName** | XM.RAG.SharePointDataAccess |
| **AssemblyOriginatorKeyFile** | XM.RAG.SharePointDataAcces.snk |
| **Líneas en .csproj** | 93 |

**Propósito:**
- Capa de acceso a datos específica de SharePoint
- Interacción con listas y bibliotecas de SharePoint

**Referencias:**
- `Microsoft.SharePoint`

---

### 2.6 Proyecto: XM.RAG.Mensajes

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG.Mensajes\XM.RAG.Mensajes.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v3.5 |
| **RootNamespace** | XM.RAG.Mensajes |
| **AssemblyName** | XM.RAG.Mensajes |
| **AssemblyOriginatorKeyFile** | KeyRAGMensajes.snk |
| **Líneas en .csproj** | 95 |

**Propósito:**
- Gestión centralizada de mensajes
- Recursos localizados

**Referencias:**
- `Microsoft.SharePoint`
- `Microsoft.SharePoint.Publishing`
- `System.Runtime.Serialization`

---

## 3. LISTADO COMPLETO DE PROYECTOS - SOLUCIÓN XM.RAG.SERVICIOS

### 3.1 Propósito General
Arquitectura de servicios N-capas que implementa:
- **Capas de acceso a datos (AccesoDatos/)** - Conecta con BD (Oracle/SQL/MID)
- **Capas de negocio (Negocio/)** - Lógica de procesos
- **Servicios WCF (Servicios/)** - APIs para consumo
- **Framework base (Soporte/)** - Utilidades transversales

### 3.2 CAPA DE ACCESO A DATOS

#### 3.2.1 Proyecto: XM.RAG.DataAccess

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\AccesoDatos\XM.RAG.DataAccess\XM.RAG.DataAccess.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.DataAccess |
| **AssemblyName** | XM.RAG.DataAccess |
| **Líneas en .csproj** | 406 |

**Propósito:**
- Capa de datos genérica
- Acceso a SQL Server
- ORM Linq to SQL via `System.Data.Linq`

**Referencias:**
- `System.Data.Entity`
- `System.Data.Linq`
- `System.Transactions`
- `System.Configuration`

---

#### 3.2.2 Proyecto: XM.RAG.Oracle

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\AccesoDatos\XM.RAG.Oracle\XM.RAG.Oracle.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Oracle |
| **AssemblyName** | XM.RAG.Oracle |
| **Líneas en .csproj** | 168 |

**Propósito:**
- Acceso específico a Oracle Database
- Utiliza Oracle.DataAccess nativo

**Referencias:**
- `Oracle.DataAccess` v2.112.3.0 (ODP.NET)
- `System.Data.OracleClient`
- `System.Data.Entity`
- `System.Data.Linq`
- `System.Transactions`

---

#### 3.2.3 Proyecto: XM.RAG.LinQ2Mid

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\AccesoDatos\XM.RAG.LinQ2Mid\XM.RAG.LinQ2Mid.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **ProjectTypeGuids** | WCF Service Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.LinQ2Mid |
| **AssemblyName** | XM.RAG.LinQ2Mid |
| **Líneas en .csproj** | 180 |

**Propósito:**
- Capa de abstracción LINQ para servicios MID
- Usa framework LinqExtender personalizado

**Referencias principales:**
- `LinqExtender` (Custom framework)
- `Microsoft.Practices.EnterpriseLibrary.ExceptionHandling` v5.0.414.0

---

#### 3.2.4 Proyecto: XM.RAG.EntidadesOracle (XM.RAG.EntidadesPDN)

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\XM.RAG.EntidadesOracle\XM.RAG.EntidadesPDN.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.EntidadesOracle |
| **AssemblyName** | XM.RAG.EntidadesOracle |
| **Líneas en .csproj** | 76 |

**Propósito:**
- Clases de entidades para mapeo con PDN (Oracle)
- Modelos de datos

**Clases principales incluidas:**
- `DetAgnAtributo`
- `LatAgente`
- `LatAgnInformacion`

---

### 3.3 CAPA DE NEGOCIO

#### 3.3.1 Proyecto: XM.RAG.Entidades

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.Entidades\XM.RAG.Entidades.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Entidades |
| **AssemblyName** | XM.RAG.Entidades |
| **SignAssembly** | true |
| **AssemblyOriginatorKeyFile** | key.snk |
| **Líneas en .csproj** | 187 |

**Propósito:**
- Modelo de datos centralizado
- DTOs y POCOs para toda la aplicación

**Referencias:**
- `Newtonsoft.Json` v4.5.0.0 (JSON serialization)

---

#### 3.3.2 Proyecto: XM.RAG.EntidadesMID

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.EntidadesMID\XM.RAG.EntidadesMID.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.EntidadesMID |
| **AssemblyName** | XM.RAG.EntidadesMID |
| **Líneas en .csproj** | 68 |

**Propósito:**
- Entidades específicas para MID (Master Información Database)

**Clases principales:**
- `UnidadNegocio`
- `Compania`
- `Contacto`

---

#### 3.3.3 Proyecto: XM.RAG.Administracion

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.Administracion\XM.RAG.Administracion.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Administracion |
| **AssemblyName** | XM.RAG.Administracion |
| **Líneas en .csproj** | 106 |

**Propósito:**
- Lógica de administración
- Exportación de datos (Excel via EPPlus)

**Referencias principales:**
- `EPPlus` v4.0.5.0 (Excel generation)
- `Microsoft.Practices.EnterpriseLibrary.Data` v5.0.414.0
- `Microsoft.Practices.EnterpriseLibrary.ExceptionHandling` v3.1.0.0

---

#### 3.3.4 Proyecto: XM.RAG.General

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.General\XM.RAG.General.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.General |
| **AssemblyName** | XM.RAG.General |
| **Líneas en .csproj** | 117 |

**Propósito:**
- Servicios de negocio generales
- Funcionalidad transversal

**Referencias:**
- `Newtonsoft.Json` v4.5.0.0

---

#### 3.3.5 Proyecto: XM.RAG.Reportes

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.Reportes\XM.RAG.Reportes.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Reportes |
| **AssemblyName** | XM.RAG.Reportes |
| **Líneas en .csproj** | 180 |

**Propósito:**
- Generación de reportes
- Integración con SQL Server Reporting Services (SSRS)

**Referencias principales:**
- `Microsoft.ReportViewer.WebForms` v10.0.0.0
- `System.Drawing`
- `System.EnterpriseServices`

**Archivos de configuración:**
- `app.config`

---

#### 3.3.6 Proyecto: XM.RAG.Actividades

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.Actividades\XM.RAG.Actividades.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0.1 |
| **ProjectTypeGuids** | Workflow Activity Library |
| **RootNamespace** | XM.RAG.Actividades |
| **AssemblyName** | XM.RAG.Actividades |
| **Líneas en .csproj** | 109 |

**Propósito:**
- Actividades para Windows Workflow Foundation (WF4)
- Componentes de procesos automatizados

**Referencias:**
- `System.Activities`
- `Microsoft.Practices.EnterpriseLibrary.ExceptionHandling` v5.0.414.0
- `Microsoft.Practices.EnterpriseLibrary.Logging` v5.0.414.0

---

#### 3.3.7 Proyecto: XM.RAG.ConsultasMID

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.ConsultasMID\XM.RAG.ConsultasMID.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **ProjectTypeGuids** | WCF Service Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.ConsultasMID |
| **AssemblyName** | XM.RAG.ConsultasMID |
| **Líneas en .csproj** | 113 |

**Propósito:**
- Servicios WCF para consultas a MID
- Interfaz: `IServicioConsultasMID`

---

#### 3.3.8 Proyecto: XM.RAG.IntegracionMID

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.IntegracionMID\XM.RAG.IntegracionMID.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.IntegracionMID |
| **AssemblyName** | XM.RAG.IntegracionMID |
| **Líneas en .csproj** | 105 |

**Propósito:**
- Lógica de integración con MID
- Sincronización de datos

**Referencias:**
- `LinqExtender` v2.5.0.0
- `Microsoft.Practices.EnterpriseLibrary` (Data, ExceptionHandling)

---

#### 3.3.9 Proyecto: XM.RAG.IntegracionPDN

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.IntegracionPDN\XM.RAG.IntegracionPDN.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.IntegracionPDN |
| **AssemblyName** | XM.RAG.IntegracionPDN |
| **Líneas en .csproj** | 117 |

**Propósito:**
- Integración con PDN (Oracle)
- Llamadas a bases de datos externas

**Referencias:**
- `Newtonsoft.Json` v4.5.0.0
- `Microsoft.Practices.EnterpriseLibrary` (Data, ExceptionHandling)

---

#### 3.3.10 Proyecto: XM.RAG.GestorArchivos

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.XMGestorArchivos\XM.RAG.GestorArchivos.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.GestorArchivos |
| **AssemblyName** | XM.RAG.GestorArchivos |
| **Líneas en .csproj** | 174 |

**Propósito:**
- Gestión de archivos y documentos
- Operaciones de sistema de archivos

**Referencias:**
- `System.ServiceModel`
- `System.Runtime.Serialization`

**Archivos de configuración:**
- `app.config`

---

#### 3.3.11 Proyecto: XM.RAG.RegistroSucesos

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.RegistroSucesos\XM.RAG.RegistroSucesos.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.RegistroSucesos |
| **AssemblyName** | XM.RAG.RegistroSucesos |
| **Líneas en .csproj** | 86 |

**Propósito:**
- Registro de auditoría y eventos
- Trazabilidad de acciones

**Referencias:**
- `LinqExtender` (Custom framework)
- `Microsoft.Practices.EnterpriseLibrary.ExceptionHandling` v3.1.0.0

---

#### 3.3.12 Proyecto: XM.RAG.RevisionSolicitudes

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.RevisionSolicitudes\XM.RAG.RevisionSolicitudes.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.RevisionSolicitudes |
| **AssemblyName** | XM.RAG.RevisionSolicitudes |
| **Líneas en .csproj** | 93 |

**Propósito:**
- Lógica de revisión de solicitudes
- Flujos de aprobación

**Referencias:**
- `Microsoft.Practices.EnterpriseLibrary` (multiple)
- WCF Exception Handling

---

#### 3.3.13 Proyecto: XM.RAG.RealizacionSolicitudes

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.RealizacionSolicitudes\XM.RAG.RealizacionSolicitudes.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.RealizacionSolicitudes |
| **AssemblyName** | XM.RAG.RealizacionSolicitudes |
| **Líneas en .csproj** | 102 |

**Propósito:**
- Lógica de ejecución de solicitudes
- Procesamiento y realización de trámites

**Referencias:**
- `System.Activities`
- `System.ServiceModel`
- Enterprise Library (Data, ExceptionHandling)

---

#### 3.3.14 Proyecto: XM.RAG.RegFro

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Negocio\XM.RAG.RegFro\XM.RAG.RegFro.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.RegFro |
| **AssemblyName** | XM.RAG.RegFro |
| **Líneas en .csproj** | 79 |

**Propósito:**
- Registro de frontera
- Gestión de agentes en frontera

**Referencias:**
- `Microsoft.Practices.EnterpriseLibrary` (Data v5.0.414.0, ExceptionHandling v5.0.414.0)

---

### 3.4 CAPA DE SERVICIOS (WCF)

#### 3.4.1 Proyecto: XM.RAG.Servicios (WCF Host)

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Servicios\XM.RAG.Servicios\XM.RAG.Servicios.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **ProjectTypeGuids** | ASP.NET Web Application Project |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Servicios |
| **AssemblyName** | XM.RAG.Servicios |
| **UseIISExpress** | true |
| **Líneas en .csproj** | 291 |

**Propósito:**
- Host de servicios WCF
- Expone las interfaces de negocio como servicios web

**Archivos de configuración:**
- web.config
- web.Debug.config
- web.Release.config
- `Configuracion/entlib.config` (logging y exception handling)

**Configuración WCF:**
El archivo `app.config` del proyecto XM.RAG principal referencia múltiples endpoints WCF:

```
- http://localhost:81/XM.RAG.Servicios/General.svc
- http://localhost:81/XM.RAG.Servicios/IntegracionMID.svc
- http://localhost:3039/XM.RAG.Servicios/Administracion.svc
- http://mvmsw590:3032/XM.RAG.Servicios/RealizacionSolicitudes.svc
- http://localhost:3031/RevisionSolicitudes.svc
- http://localhost:3022/RealizacionSolicitudes.svc
- http://localhost:3022/General.svc
```

**Bindings configurados:**
- `basicHttpBinding` - General.svc
- `wsHttpBinding` - IntegracionMID, Administracion, RealizacionSolicitudes, RevisionSolicitudes

---

#### 3.4.2 Proyecto: XM.RAG.ContratosServicios

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Servicios\XM.RAG.ContratosServicios\XM.RAG.ContratosServicios.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **ProjectTypeGuids** | WCF Service Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.ContratosServicios |
| **AssemblyName** | XM.RAG.ContratosServicios |
| **Líneas en .csproj** | 121 |

**Propósito:**
- Define contratos (interfaces) WCF
- DataContracts y ServiceContracts

**Referencias:**
- Enterprise Library ExceptionHandling (v3.1.0.0, WCF)
- `System.ServiceModel`
- `System.Runtime.Serialization`

---

### 3.5 CAPA DE SOPORTE (Framework)

#### 3.5.1 Proyecto: XM.RAG.Servicios.Framework

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Soporte\XM.RAG.Servicios.Framework\XM.RAG.Servicios.Framework.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Servicios.Framework |
| **AssemblyName** | XM.RAG.Servicios.Framework |
| **Líneas en .csproj** | 149 |

**Propósito:**
- Framework base para servicios
- Manejo de excepciones, logging, utilidades

**Referencias principales:**
- `EntLibContrib.ExceptionHandling` v5.0.505.0
- `Microsoft.Practices.EnterpriseLibrary` (ExceptionHandling v5.0.414.0, Logging v5.0.414.0)

**Archivos de configuración:**
- `app.config`

---

#### 3.5.2 Proyecto: XM.RAG.Servicios.Mensajes

**Ruta:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Soporte\XM.RAG.Servicios.Mensajes\XM.RAG.Servicios.Mensajes.csproj`

| Propiedad | Valor |
|-----------|-------|
| **OutputType** | Library |
| **TargetFrameworkVersion** | v4.0 |
| **RootNamespace** | XM.RAG.Servicios.Mensajes |
| **AssemblyName** | XM.RAG.Servicios.Mensajes |
| **Líneas en .csproj** | 101 |

**Propósito:**
- Recursos de mensajes localizados
- Strings y recursos para los servicios

---

## 4. ARCHIVOS DE CONFIGURACIÓN

### 4.1 Configuración de XM.RAG Principal

**Ubicación:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG\app.config`

**Secciones configuradas:**
- **loggingConfiguration** (Enterprise Library 5.0)
  - Listener: FlatFileTraceListener
  - Archivo: `Log\RAG.log`
  - Categorías monitoreadas: Presentacion, Error, SeguridadFuncional
  
- **cachingConfiguration** (Enterprise Library 5.0)
  - Cache Manager: Null Backing Store
  - Max elementos: 1000

- **system.serviceModel**
  - Bindings: basicHttpBinding, wsHttpBinding
  - 9 endpoints de servicios WCF configurados
  - Máximo tamaño mensajes: 6553600 bytes
  - Timeout: 10 minutos (receiveTimeout)

### 4.2 Configuración de XM.RAG.Servicios

**Ubicación:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\Servicios\XM.RAG.Servicios\Configuracion\entlib.config`

**Secciones configuradas:**
- **loggingConfiguration**
  - Listeners: 5 rolling file trace listeners
    - Sistema Externo Listener → `Log\SistemaExterno.log`
    - Seguridad Funcional Listener → `Log\SeguridadFuncional.log`
    - Error Servicios Rolling → `Log\Servicios.log`
    - Error Negocio → `Log\Negocio.log`
    - Error Workflow → `Log\Workflow.log`
  - Rolling interval: Daily
  
- **exceptionHandling**
  - Policies: Data, Log
  - Exception wrappers
  - Custom NegocioExcepcion type

- **dataConfiguration** (No detallado en lectura)

- **cachingConfiguration** (No detallado en lectura)

---

## 5. ELEMENTOS DE SHAREPOINT (XM.RAG)

### 5.1 Módulos SharePoint

#### 5.1.1 Master Pages
- **Módulo:** RAG
- **Ubicación:** `_catalogs/masterpage`
- **Archivo:** `XM-MasterPage-HorizontalMenu.master`

#### 5.1.2 Scripts
- **Módulo:** Scripts
- **Ubicación:** `Script Library`
- **Librerías incluidas:**
  - jQuery 1.9.1 + jQuery UI 1.10.3
  - Spry Framework (menús)
  - Thickbox (lightbox)
  - Validación jQuery
  - Custom.js

#### 5.1.3 Images
- **Módulo:** Images
- **Ubicación:** `SiteCollectionImages`

### 5.2 WebParts Personalizados

#### 5.2.1 AccesoEmpresa
- **Ruta:** `Provisioning/WebParts/AccesoEmpresa/`
- **Clase base:** `AccesoEmpresa.cs`
- **User Control:** `AccesoEmpresaUserControl.ascx`
- **Ubicación en galerí:** `_catalogs/wp`
- **Grupo:** Custom

**Funcionalidad:**
- Control de acceso para empresas
- Redirección basada en roles

#### 5.2.2 AccesoAnalista
- **Ruta:** `Provisioning/WebParts/AccesoAnalista/`
- **Clase base:** `AccesoAnalista.cs`
- **User Control:** `AccesoAnalistaUserControl.ascx`

**Funcionalidad:**
- Control de acceso para analistas
- Validación de permisos

### 5.3 Listas SharePoint

| Lista | Tipo | Ubicación | Instancias |
|-------|------|-----------|-----------|
| DistribucionGrupos | Distribución | Provisioning/Listas/ | 1 |
| DistribucionNotificaciones | Distribución | Provisioning/Listas/ | 1 |
| DistribucionNotificacionesyGrupos | Distribución | Provisioning/Listas/ | 1 |
| DistribucionListaInterna | Distribución | Provisioning/Listas/ | 1 |
| DistribucionListaExterna | Distribución | Provisioning/Listas/ | 1 |
| DistribucionCopiaOculta | Distribución | Provisioning/Listas/ | 1 |

**Propósito:** Control de distribución de grupos y notificaciones

### 5.4 Bibliotecas de Documentos

| Biblioteca | Ubicación | Instancias | Propósito |
|-----------|-----------|-----------|-----------|
| DocumentosPreinscripcion | Provisioning/Bibliotecas/ | 1 | Documentos pre-inscritos |
| Documentos | Provisioning/Bibliotecas/ | 1 | Documentos generales |
| Plantillas | Provisioning/Bibliotecas/ | 1 | Plantillas para solicitudes |

### 5.5 Páginas ASPX (Layout) - 56 páginas

**Categorías de páginas:**

#### Solicitudes (14 páginas)
- RegistroAgente.aspx
- ActualizarAgente.aspx
- RetiroAgente.aspx
- RegistroContacto.aspx
- ActualizarContacto.aspx
- InactivarContacto.aspx
- CambioTipoActividad.aspx
- CambioTipoClasificacionActividades.aspx
- AgenteActividades.aspx
- RegistroAgenteActividades.aspx
- RetiroAgenteActividades.aspx
- Contactos.aspx
- CausalesRechazo.aspx
- FusionEmpresa.aspx
- RegistrarObjecion.aspx

#### Revisión (9 páginas)
- RevisionAgente.aspx
- RevisionCambioTipoActividad.aspx
- RevisionRegistroAgente.aspx
- RevisionRegistroContacto.aspx
- RevisionModificacionContacto.aspx
- RevisionInactivacionContacto.aspx
- RevisionFusion.aspx
- RevisionEncargoFiduciario.aspx
- RevisionRetiroAgente.aspx
- RevisarAgente.aspx
- RevisarObjecion.aspx
- RevisionClaves.aspx

#### Parámetros (10 páginas)
- Generales.aspx
- Aplicaciones.aspx
- Actividades.aspx
- TiposContacto.aspx
- ConceptosTributarios.aspx
- CausalesRechazoSolicitud.aspx
- Documentos.aspx
- DocumentosTipoSolicitud.aspx
- ParametrizarTiemposLimSolicitudes.aspx
- Periodos.aspx

#### Administración (6 páginas)
- AdministracionSolicitudes.aspx
- AdministracionContactos.aspx
- AdministracionIntervenidos.aspx
- GestionSolicitudes.aspx
- AgenteDeuda.aspx
- PreinscripcionUc.aspx

#### Certificados (1 página)
- GenerarCertificados.aspx

#### Informes (3 páginas)
- GenerarInformes.aspx
- GenerarInformesAgente.aspx
- GenerarInformesMid.aspx

#### Intervención (3 páginas)
- IntervenirEmpresa.aspx
- IntervenirEmpresaSeleccion.aspx
- RegistroContacto.aspx (en Intervencion/)

#### Utilidades (1 página)
- Download.aspx

#### Bibliotecas de documentos (6 páginas especiales)
- Upload.aspx (Plantillas)
- Repair.aspx (Plantillas)
- Upload.aspx (DocumentosPreinscripcion)
- Repair.aspx (DocumentosPreinscripcion)
- Upload.aspx (Documentos)
- Repair.aspx (Documentos)

### 5.6 User Controls ASCX (45 controls)

#### Controles Comunes (12 .ascx)
- GridDocumentos.ascx - Rejilla de documentos
- GridGenericoSolicitud.ascx - Rejilla genérica
- GridRevisarDocumentos.ascx - Rejilla de revisión
- GridDocumentosDeRechazo.ascx - Documentos rechazados
- InformacionBasicaContacto.ascx - Datos contacto
- InformacionBasicaEmpresa.ascx - Datos empresa
- InformacionBasicaValidacion.ascx - Validación
- InformacionAnalista.ascx - Info analista
- InformacionAdministrador.ascx - Info administrador
- InformacionEmpresa.ascx - Info empresa
- InformacionEmpresaFusion.ascx - Empresa fusionada
- InformacionTiposContacto.ascx - Tipos de contacto
- SeleccionarActividad.ascx - Selector actividades
- IntervenirEmpresaSeleccion.ascx - Selector para intervención

#### Controles de Solicitud (15 .ascx)
Grupos de controles para:
- **RegistroAgente:** InformacionBasica, InformacionConstitucion, InformacionCuenta, DocumentosRegistro, DocumentacionJuramentada, RegistroAgente
- **ActualizarAgente:** InformacionBasicaActualizar, DocumentosActualizar, DocumentacionJuramentadaActualizar, ActualizarAgente
- **RegistroContacto:** InformacionBasica, InformacionComplementaria, DocumentosRegistro, TipoContactoUc, CuentasAccesoAplicativos, AcreditacionLegal, InformacionFirmanteFrontera, RegistroContacto
- **RegistroContactoIntervenido:** InformacionBasica, InformacionComplementaria, Documentos, CuentasAccesoAplicativos, RegistroContacto, TipoContacto
- **InactivarContacto:** InactivarContacto

#### Controles de Revisión (3 .ascx)
- RevisionDocumentos.ascx (en RegistroAgente/)

#### Controles especiales (4 .ascx en Unisys.Controls/)
- Seccion.ascx - Control de sección
- Mensajes.ascx - Mensajes flotantes
- LineaTiempo.ascx - Timeline visual
- (GridRevisarDocumentos.ascx también en Comun/)

### 5.7 Feature SharePoint

**Feature ID:** RAG
**Ubicación:** `c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\XM.RAG\Features\RAG\`
**Archivo:** RAG.EventReceiver.cs

**Event Receiver:**
- Clase: `RAGEventReceiver`
- Herencia: SPFeatureReceiver (SharePoint)
- Métodos: FeatureActivated, FeatureDeactivating

### 5.8 Uso de SPContext, SPSite, SPWeb, SPList

**Ubicaciones encontradas:** 39 matches

**Patrones de uso:**

```csharp
// Lectura de contexto actual
Guid siteID = SPContext.Current.Site.ID;
Guid webID = SPContext.Current.Web.ID;

// Creación de nuevas instancias
using (SPSite site = new SPSite(SPContext.Current.Site.Url))
{
    using (SPWeb web = site.RootWeb) { ... }
}

// Acceso al usuario actual
SPContext.Current.Web.CurrentUser.Name
SPContext.Current.Web.CurrentUser.ToString()
SPContext.Current.Web.CurrentUser.Groups

// Navegación
SPContext.Current.Web.Site.Url
SPContext.Current.IsPopUI

// Redirecciones
Response.Redirect(SPContext.Current.Web.Site.Url, false);
```

**Archivos con mayor uso:**
1. `Util/Util.cs` - 18 referencias
2. `Provisioning/WebParts/AccesoEmpresa/AccesoEmpresaUserControl.ascx.cs` - 2 referencias
3. `Layouts/RAG/*/` - múltiples páginas (10+ referencias)

---

## 6. DEPENDENCIAS Y REFERENCIAS GLOBALES

### 6.1 Enterprise Library (Microsoft Practices)

| Componente | Versión | Ubicación | Propósito |
|-----------|---------|-----------|-----------|
| ExceptionHandling | 5.0.414.0 / 3.1.0.0 | GAC | Manejo de excepciones |
| ExceptionHandling.WCF | 3.1.0.0 | Referencias | Exceptions en WCF |
| Data | 5.0.414.0 | GAC | Acceso a datos |
| Logging | 5.0.414.0 | GAC | Logging |
| Caching | 5.0.414.0 | GAC | Caché distribuido |

### 6.2 SharePoint

| Componente | Versión | Origen |
|-----------|---------|--------|
| Microsoft.SharePoint | 14.0.0.0 | GAC (SharePoint 2010) |
| Microsoft.SharePoint.Security | 14.0.0.0 | GAC |
| Microsoft.SharePoint.Publishing | 14.0.0.0 | GAC |
| Microsoft.Web.CommandUI | 14.0.0.0 | GAC |
| Microsoft.Practices.SharePoint.Common | 2.0.0.0 | HintPath |

### 6.3 Base de Datos

| Componente | Versión | Propósito |
|-----------|---------|-----------|
| Oracle.DataAccess (ODP.NET) | 2.112.3.0 | Acceso Oracle |
| System.Data.OracleClient | - | Legacy Oracle client |
| System.Data.Linq | - | LINQ to SQL |
| System.Data.Entity | - | Entity Framework |
| System.Transactions | - | Transacciones distribuidas |

### 6.4 Servicios Web

| Componente | Versión | Propósito |
|-----------|---------|-----------|
| System.ServiceModel | - | WCF |
| System.Runtime.Serialization | - | Serialización |
| System.Web.Services | - | Web services legacy |

### 6.5 Librerías Personalizadas

| Librería | Versión | Origen | Propósito |
|----------|---------|--------|-----------|
| itextsharp | 5.5.0.0 | NuGet/Local | Generación PDF |
| itextsharp.xmlworker | 5.5.0.0 | NuGet/Local | XML a PDF |
| Telerik.Web.UI | 2016.1.225.35 | Local | Controles UI |
| Newtonsoft.Json | 4.5.0.0 | Local | JSON serialization |
| EPPlus | 4.0.5.0 | Local | Generación Excel |
| LinqExtender | 2.5.0.0 | Local | Framework LINQ custom |
| EntLibContrib.ExceptionHandling | 5.0.505.0 | Local | Extension handling |

### 6.6 Librerías de Terceros

| Librería | Ubicación | Propósito |
|----------|-----------|-----------|
| Microsoft.ReportViewer.WebForms | v10.0.0.0 | SQL Server Reporting Services |
| Microsoft.Activities.Extensions | Local | WF Extensions |

---

## 7. ESTADÍSTICAS GENERALES

### 7.1 Conteos de Archivos

| Tipo | XM.RAG | XM.RAG.Servicios | Total |
|------|---------|------------------|-------|
| Proyectos .csproj | 6 | 22 | **28** |
| Archivos .cs | ~229 | ~300+ | **~530+** |
| Archivos .ascx | 45 | 0 | **45** |
| Archivos .aspx | 56 | 0 | **56** |
| Archivos .config | 8 | 9 | **17** |
| Archivos Elements.xml | 21 | 0 | **21** |

### 7.2 Líneas de Código en .csproj

| Rango | Proyectos | Ejemplos |
|--------|-----------|----------|
| < 100 líneas | 9 | XM.RAG.SharePointDataAccess (93) |
| 100-200 líneas | 12 | XM.RAG.Mensajes (95), Unisys.Controls (151) |
| 200-500 líneas | 6 | XM.RAG.Framework (270), XM.RAG.Servicios (291) |
| > 500 líneas | 1 | XM.RAG (4451), XM.RAG.DataAccess (406), XM.RAG.TimerJobs (880) |

### 7.3 Distribución por Framework

| Framework | Proyectos | Descripción |
|-----------|-----------|-------------|
| **.NET 3.5** | 6 | XM.RAG principal + Framework + SharePoint |
| **.NET 4.0** | 15 | Servicios Windows + BD |
| **.NET 4.0.1** | 1 | XM.RAG.Actividades (Workflow) |

### 7.4 Distribución por Tipo

| Tipo | Cantidad | Ejemplos |
|------|----------|----------|
| Library (DLL) | 24 | Mayoría |
| Web (ASP.NET) | 2 | Unisys.Controls, XM.RAG.Servicios |
| WCF Service | 4 | ConsultasMID, LinQ2Mid, ContratosServicios, Actividades |
| Workflow Activity | 1 | XM.RAG.Actividades |
| SharePoint | 1 | XM.RAG |

---

## 8. CONEXIONES Y ENDPOINTS

### 8.1 Endpoints WCF Configurados

| Endpoint | Dirección | Binding | Versión |
|----------|-----------|---------|---------|
| CertificadoDigital | http://comde-xmtemp:81/... | basicHttpBinding | - |
| General | http://localhost:81/XM.RAG.Servicios/General.svc | wsHttpBinding | v1 + v2 |
| IntegracionMID | http://localhost:81/XM.RAG.Servicios/IntegracionMID.svc | wsHttpBinding | - |
| Administracion | http://localhost:3039/XM.RAG.Servicios/Administracion.svc | wsHttpBinding | - |
| RealizacionSolicitudes | http://mvmsw590:3032/... | wsHttpBinding | v1 + v2 + v3 |
| RevisionSolicitudes | http://localhost:3031/RevisionSolicitudes.svc | wsHttpBinding | - |

### 8.2 Parámetros de Comunicación

- **receiveTimeout:** 00:10:00 (10 minutos)
- **sendTimeout:** 00:01:00 (1 minuto)
- **openTimeout:** 00:01:00
- **closeTimeout:** 00:01:00
- **maxBufferPoolSize:** 524288 bytes
- **maxReceivedMessageSize:** 6553600 bytes (~6.25 MB)
- **maxDepth:** 32
- **maxStringContentLength:** 8192
- **maxArrayLength:** 16384

---

## 9. PATRÓN ARQUITECTÓNICO IDENTIFICADO

### 9.1 Arquitectura Multicapa

```
┌─────────────────────────────────────────────┐
│     PRESENTACIÓN (N-Tier)                   │
│  XM.RAG + Unisys.Controls (SharePoint)     │
│  + Páginas ASPX + User Controls            │
└──────────────┬──────────────────────────────┘
               │
┌──────────────▼──────────────────────────────┐
│     SERVICIOS WCF                           │
│  XM.RAG.Servicios (Host)                   │
│  XM.RAG.ContratosServicios (Contracts)    │
│  Endpoints: General, Administracion, etc   │
└──────────────┬──────────────────────────────┘
               │
┌──────────────▼──────────────────────────────┐
│     LÓGICA DE NEGOCIO (21 proyectos)       │
│  XM.RAG.Administracion                     │
│  XM.RAG.IntegracionMID/PDN                 │
│  XM.RAG.RealizacionSolicitudes             │
│  XM.RAG.RevisionSolicitudes                │
│  etc...                                     │
└──────────────┬──────────────────────────────┘
               │
┌──────────────▼──────────────────────────────┐
│     ACCESO A DATOS (4 proyectos)           │
│  XM.RAG.DataAccess (SQL Server)            │
│  XM.RAG.Oracle (Oracle PDN)                │
│  XM.RAG.LinQ2Mid (MID abstraction)        │
│  XM.RAG.EntidadesOracle (Oracle models)   │
└──────────────┬──────────────────────────────┘
               │
┌──────────────▼──────────────────────────────┐
│     BASES DE DATOS                          │
│  SQL Server (RAG)                           │
│  Oracle (PDN)                               │
│  MID (Master Information Database)          │
└─────────────────────────────────────────────┘
```

### 9.2 Patrones Usados

1. **Service-Oriented Architecture (SOA)** - WCF para servicios
2. **N-Tier Architecture** - Separación clara de capas
3. **Repository Pattern** - DataAccess projects
4. **DTO Pattern** - XM.RAG.Entidades
5. **Event-Driven** - SharePoint Event Receivers
6. **Plugin Architecture** - WebParts sharePoint
7. **Workflow-based** - Windows Workflow Foundation activities

---

## 10. CONFIGURACIONES ESPECIALES Y LOGGING

### 10.1 Logging Strategy

**Enterprise Library Logging** configurado con múltiples listeners:

**Para XM.RAG:**
- Categoría: "Presentacion", "Error", "SeguridadFuncional"
- Archivo: `Log\RAG.log`
- Rotation: No especificada (flat file)

**Para XM.RAG.Servicios:**
- Categorías: "Error Negocio", "Error Servicios", "SeguridadFuncional", "SistemaExterno", "Error Workflows"
- Archivos:
  - `Log\Negocio.log`
  - `Log\Servicios.log`
  - `Log\SeguridadFuncional.log`
  - `Log\SistemaExterno.log`
  - `Log\Workflow.log`
- Rotation: Daily (RollingFlatFileTraceListener)

### 10.2 Exception Handling

**Policies configuradas:**
1. **Data** - Para excepciones SqlException
2. **Log** - Log + Wrap a NegocioExcepcion
3. **NegocioExcepcion** - Custom exception type

**Handlers:**
- LoggingExceptionHandler
- WrapHandler
- XmlExceptionFormatter

---

## 11. SEGURIDAD Y AUDITORÍA

### 11.1 Signed Assemblies

Proyectos con strong naming:
- XM.RAG (key.snk)
- XM.RAG.Framework (KeyRAGFramework.snk)
- XM.RAG.TimerJobs (key.snk)
- Unisys.Controls (key.snk)
- XM.RAG.SharePointDataAccess (XM.RAG.SharePointDataAcces.snk)
- XM.RAG.Mensajes (KeyRAGMensajes.snk)
- XM.RAG.Entidades (key.snk)

### 11.2 SharePoint Security

- Uso de SPContext para validación de contexto
- Métodos para verificar roles: `IsUserInRole(user, web, roleName)`
- Validación de usuario actual en múltiples puntos
- Uso de QueryString encryption en redirecciones críticas

---

## 12. CONCLUSIONES TÉCNICAS

### 12.1 Fortalezas Identificadas

1. **Arquitectura bien definida** - Clara separación de capas
2. **Manejo de excepciones centralizado** - Enterprise Library
3. **Múltiples fuentes de datos** - BD SQL, Oracle, MID
4. **Servicios desacoplados** - WCF permite reutilización
5. **Logging transversal** - Auditoría completa

### 12.2 Tecnologías Utilizadas

- **Framework:** .NET 3.5 / 4.0
- **Patrón:** N-tier + SOA
- **Presentación:** SharePoint 2010 + ASP.NET
- **Datos:** LINQ to SQL + Oracle ODP.NET
- **Servicios:** WCF con wsHttpBinding/basicHttpBinding
- **Workflow:** Windows Workflow Foundation 4.0
- **Logging:** Enterprise Library 5.0
- **Reportes:** SQL Server Reporting Services 10.0

### 12.3 Complejidad General

- **228 archivos .csproj + código fuente**
- **28 proyectos organizados por responsabilidad**
- **Integración con 3 bases de datos diferentes**
- **56 páginas SharePoint + 45 controles reutilizables**
- **7 endpoints WCF públicos**
- **Soporte para múltiples versiones de servicios**

---

**FIN DEL ANÁLISIS TÉCNICO**  
*Documento generado: 8 de Febrero, 2026*

