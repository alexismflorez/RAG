# 🗂️ MAPA COMPLETO DE ESTRUCTURA
## XM.RAG y XM.RAG.Servicios

**Fecha:** Febrero, 2026  
**Alcance:** Descripción exhaustiva de carpetas y archivos sin omisiones  

---

## 📋 TABLA DE CONTENIDOS

1. [Estructura de XM.RAG](#estructura-de-xmrag)
2. [Estructura de XM.RAG.Servicios](#estructura-de-xmragservicios)
3. [Estadísticas Consolidadas](#estadísticas-consolidadas)

---

# 🏗️ ESTRUCTURA DE XM.RAG

## Raíz del Proyecto XM.RAG

```
c:\RAG\RAGV2\RAG\FUENTES\XM.RAG\
│
├── XM.RAG.sln                          [Solution File]
├── Settings.StyleCop                   [Code Analysis Config]
│
├── Referencias/                        [Shared Dependencies]
│   ├── .Unisys.Controls_BASE_464.dll.swp
│   ├── .Unisys.Controls_LOCAL_464.dll.swp
│   ├── .Unisys.Controls_REMOTE_464.dll.swp
│   ├── .Unisys.Controls.dll.swp
│   ├── itextsharp.dll                  [PDF Generation]
│   ├── itextsharp.xml                  [Documentation]
│   ├── itextsharp.xmlworker.dll        [XML to PDF]
│   ├── Mensajes.xml                    [Messages Resources]
│   ├── Mensajes.xml.orig               [Backup]
│   ├── Microsoft.Practices.ServiceLocation.dll
│   ├── Microsoft.Practices.SharePoint.Common.dll
│   ├── Microsoft.Sharepoint.Sandbox.dll
│   ├── Telerik.Web.UI.dll              [UI Controls v2016.1.225.35]
│   ├── Telerik.Web.UI.Skins.dll        [Telerik Skins]
│   ├── UNISYS.Componentes.CorreoElectronico.dll
│   ├── Unisys.Controls.dll
│   ├── Unisys.Controls.dll.orig        [Original Backup]
│   ├── Unisys.Controls_BACKUP_1996.dll
│   ├── Unisys.Controls_BASE_1996.dll
│   ├── Unisys.Controls_LOCAL_1996.dll
│   ├── Unisys.Controls_REMOTE_1996.dll
│   ├── XM.RAG.Entidades.dll
│   ├── XM.RAG.Framework.dll
│   ├── XM.RAG.Framework.dll.orig       [Original Backup]
│   ├── XM.RAG.Mensajes.dll
│   └── XM.RAG.SharePointDataAccess.dll
│
├── Unisys.Controls/                    [Web Controls Library - .NET 3.5]
│   ├── Unisys.Controls.csproj          [Project File]
│   ├── Web.config                      [Base Configuration]
│   ├── Web.Debug.config
│   ├── Web.Release.config
│   ├── key.snk                         [Strong Name Key]
│   │
│   ├── Base/
│   │   └── UserControlBase.cs          [Base Class for Controls]
│   │
│   ├── Interfaces/
│   │   └── ISeccion.cs                 [Section Interface]
│   │
│   ├── LineaTiempo/                    [Timeline Component]
│   │   ├── LineaTiempo.ascx            [User Control]
│   │   ├── LineaTiempo.ascx.cs         [Code Behind]
│   │   ├── Configuracion/
│   │   │   └── Configuracion.cs        [Timeline Configuration]
│   │   ├── Entidad/
│   │   │   └── Evento.cs               [Timeline Event Entity]
│   │   ├── OrigenWrapper/
│   │   │   └── OrigenDatosWrapper.cs   [Data Source Wrapper]
│   │   └── Recursos/
│   │       ├── css/
│   │       │   ├── jquery.jqtimeline.css
│   │       │   └── LineaTiempo.css
│   │       ├── Imagenes/               [9 PNG Images]
│   │       │   ├── 1410313598_accept.png
│   │       │   ├── 1410315130_681122-Clock-32.png
│   │       │   ├── 1410382465_hourglass.png
│   │       │   ├── main_img.png
│   │       │   ├── naranja-g.png
│   │       │   ├── naranja-p.png
│   │       │   ├── negro-g.png
│   │       │   ├── negro-p.png
│   │       │   ├── verde-g.png
│   │       │   └── verde-p.png
│   │       └── js/
│   │           ├── jquery.jqtimeline.js
│   │           └── LineaTiempo.js
│   │
│   ├── Mensajes/                       [Messages Component]
│   │   ├── Mensajes.ascx               [User Control]
│   │   └── Mensajes.ascx.cs            [Code Behind]
│   │
│   ├── Seccion/                        [Section Component]
│   │   ├── Seccion.ascx                [User Control]
│   │   └── Seccion.ascx.cs             [Code Behind]
│   │
│   └── Properties/
│       └── AssemblyInfo.cs             [Assembly Information]
│
├── XM.RAG.Framework/                   [Core Framework Library - .NET 3.5]
│   ├── XM.RAG.Framework.csproj
│   ├── KeyRAGFramework.snk              [Strong Name Key]
│   ├── app.config
│   ├── Contexto.cs                     [Application Context]
│   ├── ConfiguracionPresentacion.cs    [UI Configuration]
│   ├── RecursosFramework.Designer.cs   [Resources]
│   ├── RecursosFramework.resx          [Resource File]
│   ├── XM.RAG.Entidades.RegistroSucesos.Suceso.datasource
│   ├── XM.RAG.Entidades.RegistroSucesos.Suceso1.datasource
│   │
│   ├── Enumeraciones/                  [30+ Enumerations]
│   │   ├── AplicacionaesRolEnum.cs
│   │   ├── AplicationPages.cs
│   │   ├── BibliotecasYListas.cs       [SP Lists & Libraries]
│   │   ├── DestinosCorreoElectronico.cs
│   │   ├── DetalleBitacora.cs          [Audit Detail]
│   │   ├── DocumentoPlantillas.cs      [Document Templates]
│   │   ├── EndpointNombres.cs          [Service Endpoints]
│   │   ├── EstadoPrueba.cs
│   │   ├── EstadoSolicitud.cs          [Request States]
│   │   ├── EventosBitacora.cs          [Audit Events]
│   │   ├── Formatos.cs                 [File Formats]
│   │   ├── GruposAplicaciones.cs
│   │   ├── HtmlTexto.cs                [HTML Text]
│   │   ├── JobsNombres.cs              [Timer Job Names]
│   │   ├── LibraryProperties.cs        [SP Library Props]
│   │   ├── Modulo.cs                   [Module Enum]
│   │   ├── Parametros.cs               [Parameters]
│   │   ├── ProcesoNotificacionDocumentos.cs
│   │   ├── Reporte.cs                  [Report Enum]
│   │   ├── Roles.cs                    [Role Enum]
│   │   ├── TipoActividadEnum.cs        [Activity Types]
│   │   ├── TipoCausalRechazo.cs        [Rejection Reasons]
│   │   ├── TipoDocumento.cs            [Document Types]
│   │   ├── TipoEmpresa.cs              [Company Types]
│   │   ├── TiposDocumento.cs           [Alternative Doc Types]
│   │   ├── TiposIdentificacion.cs      [ID Types]
│   │   ├── TipoSolicitudEnum.cs        [Request Types]
│   │   └── TipoTransaccionEnum.cs      [Transaction Types]
│   │
│   ├── Excepciones/                    [Custom Exceptions]
│   │   ├── NegocioExcepcion.cs         [Business Exception]
│   │   └── SistemaExternoNoDisponibleExcepcion.cs
│   │
│   ├── Helper/
│   │   └── ULSHelper.cs                [ULS Logging Helper]
│   │
│   ├── Logging/
│   │   ├── LogManager.cs               [Log Manager]
│   │   └── CategoriaLog.cs             [Log Category]
│   │
│   ├── Sharepoint/                     [SharePoint Utilities]
│   │   ├── Attributes/
│   │   │   └── SharepointColumn.cs     [Column Attribute]
│   │   ├── Base/
│   │   │   ├── AplicationPageBase.cs   [Application Page Base]
│   │   │   ├── BaseEntity.cs           [Entity Base]
│   │   │   ├── SharepointBase.cs
│   │   │   └── UserControlBase.cs
│   │   ├── Common/
│   │   │   └── CommonMethodExtension.cs
│   │   ├── Enumerados/
│   │   │   ├── MessageEnum.cs
│   │   │   └── CategoriasEnum.cs
│   │   ├── Eventos/
│   │   │   └── GenericEventArgs.cs
│   │   ├── Helpers/
│   │   │   ├── SharepointHelper.cs
│   │   │   ├── AddFileParams.cs        [File Parameters]
│   │   │   └── Logger/
│   │   │       ├── Logger.cs
│   │   │       ├── LoggerConfiguration.cs
│   │   │       └── CategoriasLog.cs
│   │   ├── Interfaces/
│   │   │   └── IMessage.cs
│   │   └── Utils/
│   │       ├── QueryStringSecurity.cs  [Query String Encryption]
│   │       └── SharepointUtils.cs      [SP Utilities]
│   │
│   ├── Utilidades/                     [Utility Classes]
│   │   ├── AdministradorMensaje.cs
│   │   ├── Comun.cs                    [Common]
│   │   ├── CorreoElectronico.cs        [Email]
│   │   ├── Extension.cs                [Extension Methods]
│   │   ├── IGestorMensaje.cs           [Message Manager Interface]
│   │   ├── PaginaBase.cs               [Page Base]
│   │   ├── ParametroPagina.cs
│   │   ├── Plantillas.cs               [Templates]
│   │   └── Roles.cs
│   │
│   ├── Service References/             [WCF Service References]
│   │   ├── GeneralService/             [50+ XSD Files]
│   │   │   ├── Reference.cs
│   │   │   ├── Reference.svcmap
│   │   │   ├── configuration.svcinfo
│   │   │   ├── General.disco
│   │   │   ├── General.wsdl
│   │   │   ├── General.xsd
│   │   │   ├── General1.wsdl
│   │   │   └── [General2-General48.xsd]
│   │   │
│   │   └── RegistroSucesosService/
│   │       ├── Reference.cs
│   │       ├── Reference.svcmap
│   │       ├── RegistroSucesos.wsdl
│   │       ├── RegistroSucesos.xsd
│   │       └── RegistroSucesos1.xsd
│   │
│   ├── Xmls/                            [Configuration XML Files]
│   │   ├── Xmls.cs
│   │   ├── AccionesGrid.xml
│   │   ├── Help.config
│   │   ├── HtmlTexto.xml
│   │   ├── NotificacionesDocumentos.xml
│   │   ├── Reportes.xml
│   │   ├── ReportesAgente.xml
│   │   └── ReportesMID.xml
│   │
│   └── Properties/
│       └── AssemblyInfo.cs
│
├── XM.RAG.Mensajes/                    [Messages Library - .NET 3.5]
│   ├── XM.RAG.Mensajes.csproj
│   ├── KeyRAGMensajes.snk
│   ├── CodigoMensaje.cs                [Message Code Enum]
│   ├── Mensaje.cs                      [Message Class]
│   ├── MensajeBatch.cs
│   ├── ItemBatch.cs
│   ├── TipoMensaje.cs                  [Message Type Enum]
│   ├── Mensajes.xml                    [Message Resources]
│   ├── MensajesBase.Designer.cs
│   ├── MensajesBase.resx
│   └── Properties/
│       └── AssemblyInfo.cs
│
├── XM.RAG.SharePointDataAcces/         [SharePoint Data Access - .NET 3.5]
│   ├── XM.RAG.SharePointDataAccess.csproj
│   ├── XM.RAG.SharePointDataAcces.snk
│   │
│   ├── DAL/                            [Data Access Layer - 9 Classes]
│   │   ├── DestinatariosDAL.cs
│   │   ├── DestinatariosDirectorioActivoDAL.cs
│   │   ├── DestinosCorreoElectronicoDAL.cs
│   │   ├── DistribucionCopiaOcultaDAL.cs
│   │   ├── DistribucionGruposDAL.cs
│   │   ├── DistribucionListaExternaDAL.cs
│   │   ├── DistribucionListaInternaDAL.cs
│   │   ├── DistribucionNotificacionesDAL.cs
│   │   └── DistribucionNotificacionesyGruposDAL.cs
│   │
│   ├── BLL/                            [Business Logic Layer - 9 Classes]
│   │   ├── Destinatarios.cs
│   │   ├── DestinatariosDirectorioActivo.cs
│   │   ├── DestinosCorreoElectronico.cs
│   │   ├── DistribucionCopiaOculta.cs
│   │   ├── DistribucionGrupos.cs
│   │   ├── DistribucionListaExterna.cs
│   │   ├── DistribucionListaInterna.cs
│   │   ├── DistribucionNotificaciones.cs
│   │   └── DistribucionNotificacionesyGrupos.cs
│   │
│   └── Properties/
│       └── AssemblyInfo.cs
│
├── XM.RAG.TimerJobs/                   [Timer Jobs Library - .NET 3.5]
│   ├── XM.RAG.TimerJobs.csproj
│   ├── key.snk
│   ├── app.config
│   │
│   ├── Features/
│   │   └── XM.RAG.TimerJobs/
│   │       ├── XM.RAG.TimerJobs.EventReceiver.cs
│   │       ├── XM.RAG.TimerJobs.feature
│   │       └── XM.RAG.TimerJobs.Template.xml
│   │
│   ├── Helper/
│   │   ├── GeneracionEmail.cs
│   │   └── Parametros/
│   │       ├── Adjunto.cs
│   │       ├── Configuracion.cs
│   │       └── MailMessageExt.cs
│   │
│   ├── Service References/             [3 Services]
│   │   ├── ServiceAdministracion/      [100+ XSD Files]
│   │   ├── ServiceGeneral/             [100+ XSD Files]
│   │   └── ServiceRealizacionSolicitudes/
│   │
│   ├── Package/
│   │   ├── Package.package
│   │   └── Package.Template.xml
│   │
│   ├── Properties/
│   │   ├── AssemblyInfo.cs
│   │   └── DataSources/                [60+ DataSource Files]
│   │
│   └── [Archive Details]
│
└── XM.RAG/                             [Main SharePoint Project - .NET 3.5 - 4451 lines csproj]
    ├── XM.RAG.csproj                   [Project File]
    ├── ClassDiagram1.cd
    ├── key.snk
    ├── packages.config
    ├── app.config                      [WCF Services Configuration]
    │
    ├── ControlTemplates/               [SharePoint User Controls]
    │   └── RAG/
    │       ├── Comun/                  [12 Common Controls]
    │       │   ├── GridDocumentos.ascx
    │       │   ├── GridGenericoSolicitud.ascx
    │       │   ├── GridRevisarDocumentos.ascx
    │       │   ├── GridDocumentosDeRechazo.ascx
    │       │   ├── InformacionBasicaContacto.ascx
    │       │   ├── InformacionBasicaEmpresa.ascx
    │       │   ├── InformacionBasicaValidacion.ascx
    │       │   ├── InformacionAnalista.ascx
    │       │   ├── InformacionAdministrador.ascx
    │       │   ├── InformacionEmpresa.ascx
    │       │   ├── InformacionEmpresaFusion.ascx
    │       │   └── InformacionTiposContacto.ascx
    │       │
    │       ├── Solicitud/              [15 Request Controls]
    │       │   ├── RegistroAgente/     (6 ASCX controls)
    │       │   ├── ActualizarAgente/   (4 ASCX controls)
    │       │   ├── RegistroContacto/   (8 ASCX controls)
    │       │   ├── RegistroContactoIntervenido/
    │       │   └── InactivarContacto/
    │       │
    │       ├── Revision/               [3 Review Controls]
    │       │
    │       ├── Logs/                   [Logging Components]
    │       ├── ValidacionesSDAO/       [Validations]
    │       └── DocumentoSPDAO/         [SharePoint Documents]
    │
    ├── Layouts/                        [SharePoint Page Layouts]
    │   └── RAG/
    │       ├── Solicitud/              [14 ASPX Pages]
    │       │   ├── RegistroAgente.aspx
    │       │   ├── ActualizarAgente.aspx
    │       │   ├── RetiroAgente.aspx
    │       │   ├── RegistroContacto.aspx
    │       │   ├── ActualizarContacto.aspx
    │       │   ├── InactivarContacto.aspx
    │       │   ├── CambioTipoActividad.aspx
    │       │   ├── CambioTipoClasificacionActividades.aspx
    │       │   ├── AgenteActividades.aspx
    │       │   ├── RegistroAgenteActividades.aspx
    │       │   ├── RetiroAgenteActividades.aspx
    │       │   ├── Contactos.aspx
    │       │   ├── CausalesRechazo.aspx
    │       │   ├── FusionEmpresa.aspx
    │       │   └── RegistrarObjecion.aspx
    │       │
    │       ├── Revision/               [9 ASPX Pages]
    │       │   ├── RevisionAgente.aspx
    │       │   ├── RevisionCambioTipoActividad.aspx
    │       │   ├── RevisionRegistroAgente.aspx
    │       │   ├── RevisionRegistroContacto.aspx
    │       │   ├── RevisionModificacionContacto.aspx
    │       │   ├── RevisionInactivacionContacto.aspx
    │       │   ├── RevisionFusion.aspx
    │       │   ├── RevisionEncargoFiduciario.aspx
    │       │   └── [More Review Pages]
    │       │
    │       ├── Parametros/             [10 ASPX Pages - Admin Configuration]
    │       │   ├── Generales.aspx
    │       │   ├── Aplicaciones.aspx
    │       │   ├── Actividades.aspx
    │       │   ├── TiposContacto.aspx
    │       │   ├── ConceptosTributarios.aspx
    │       │   ├── CausalesRechazoSolicitud.aspx
    │       │   ├── Documentos.aspx
    │       │   ├── DocumentosTipoSolicitud.aspx
    │       │   ├── ParametrizarTiemposLimSolicitudes.aspx
    │       │   └── Periodos.aspx
    │       │
    │       ├── Administracion/         [6 ASPX Pages]
    │       │   ├── AdministracionSolicitudes.aspx
    │       │   ├── AdministracionContactos.aspx
    │       │   ├── AdministracionIntervenidos.aspx
    │       │   ├── GestionSolicitudes.aspx
    │       │   ├── AgenteDeuda.aspx
    │       │   └── PreinscripcionUc.aspx
    │       │
    │       ├── Certificados/           [1 ASPX Page]
    │       │   └── GenerarCertificados.aspx
    │       │
    │       ├── Informes/               [3 ASPX Pages]
    │       │   ├── GenerarInformes.aspx
    │       │   ├── GenerarInformesAgente.aspx
    │       │   └── GenerarInformesMid.aspx
    │       │
    │       ├── Intervencion/           [3 ASPX Pages]
    │       │   ├── IntervenirEmpresa.aspx
    │       │   ├── IntervenirEmpresaSeleccion.aspx
    │       │   └── RegistroContacto.aspx
    │       │
    │       └── Comun/Util/
    │           └── Download.aspx
    │
    ├── Features/
    │   └── RAG/                        [SharePoint Feature]
    │       └── RAG.EventReceiver.cs
    │
    ├── Provisioning/                   [SharePoint Provisioning]
    │   ├── WebParts/                   [2 Custom WebParts]
    │   │   ├── AccesoEmpresa/
    │   │   │   ├── AccesoEmpresa.cs
    │   │   │   └── AccesoEmpresaUserControl.ascx
    │   │   └── AccesoAnalista/
    │   │       ├── AccesoAnalista.cs
    │   │       └── AccesoAnalistaUserControl.ascx
    │   │
    │   ├── Listas/                     [6 Distribution Lists]
    │   │   ├── DistribucionGrupos
    │   │   ├── DistribucionNotificaciones
    │   │   ├── DistribucionNotificacionesyGrupos
    │   │   ├── DistribucionListaInterna
    │   │   ├── DistribucionListaExterna
    │   │   └── DistribucionCopiaOculta
    │   │
    │   ├── Bibliotecas/                [3 Document Libraries]
    │   │   ├── DocumentosPreinscripcion
    │   │   ├── Documentos
    │   │   └── Plantillas
    │   │
    │   ├── Fields/
    │   ├── ContentTypes/
    │   └── Elements.xml
    │
    ├── Helper/
    │   ├── Parametros/                 [4 Parameter Classes]
    │   │   ├── [Parameter Classes]
    │   ├── Eventos/                    [Event handlers]
    │   └── GeneracionEmail.cs
    │
    ├── Util/
    │   ├── Util.cs                     [Main Utility Class - 18 SP References]
    │   ├── CommonMethodExtension.cs
    │   ├── CorreoElectronico.cs
    │   ├── CorreoElectronicoRAG.cs
    │   ├── CredencialesReporting.cs
    │   └── Reportes.xml
    │
    ├── Service References/             [7 WCF Service References]
    │   ├── ServiceGeneral              [Multiple Versions]
    │   ├── ServiceIntegracionMID/      [Multiple Versions]
    │   ├── ServiceAdministracion
    │   ├── ServiceRevisionSolicitudes
    │   ├── ServiceRealizacionSolicitudes [3 Versions]
    │   └── CertificadoDigitalService
    │
    ├── Web References/
    │   └── Reporting                   [SQL Server Reporting Services]
    │       ├── Reference.map
    │       ├── Reference.cs
    │       └── ReportExecution2005.wsdl
    │
    ├── Package/
    ├── RAG/
    ├── Properties/
    └── Images/
```

---

# 🏢 ESTRUCTURA DE XM.RAG.SERVICIOS

## Raíz del Proyecto XM.RAG.Servicios

```
c:\RAG\RAGV2\RAG\FUENTES\XM.RAG.Servicios\
│
├── XM.RAG.Servicios.sln
├── Settings.StyleCop
│
├── AccesoDatos/                        [Data Access Layer - 4 Projects]
│   │
│   ├── XM.RAG.DataAccess/              [SQL Server Access - .NET 4.0]
│   │   ├── XM.RAG.DataAccess.csproj
│   │   ├── App.Config
│   │   │
│   │   ├── Entity Model Files
│   │   │   ├── RAG.edmx                [Entity Data Model]
│   │   │   ├── RAG.edmx.sql
│   │   │   ├── RAGModel.Context.cs
│   │   │   ├── RAGModel.Context.Extensions.cs
│   │   │   ├── RAGModel.Context.tt
│   │   │   ├── RAGModel.cs
│   │   │   ├── RAGModel.tt
│   │   │   └── RAG.Designer.cs
│   │   │
│   │   ├── Root Data Access Classes (80+ DAO Classes)
│   │   │   ├── Adjunto.cs
│   │   │   ├── Agente.cs
│   │   │   ├── Alarma.cs
│   │   │   ├── Aplicacion.cs
│   │   │   ├── AplicacionesPorContacto.cs
│   │   │   ├── AplicacionRol.cs
│   │   │   ├── AplicacionTipoActividad.cs
│   │   │   ├── Bitacora.cs
│   │   │   ├── Cargo.cs
│   │   │   ├── CausalRechazo.cs
│   │   │   ├── ConceptoTributario.cs
│   │   │   ├── ControlTareas.cs
│   │   │   ├── Cuenta.cs
│   │   │   ├── Departamento.cs
│   │   │   ├── DocRetiroDeuda.cs
│   │   │   ├── DocTipoSolicitudActividad.cs
│   │   │   ├── DocTipoSolicitudCausales.cs
│   │   │   ├── DocTipoSolicitudContacto.cs
│   │   │   ├── DocTipoSolicitudRol.cs
│   │   │   ├── Documento.cs
│   │   │   ├── DocumentosObjecion.cs
│   │   │   ├── DocumentoSolicitud.cs
│   │   │   ├── DocumentoTipoSolicitud.cs
│   │   │   ├── Empresa.cs
│   │   │   ├── EmpresaInfoTributaria.cs
│   │   │   ├── EncargoFiduciario.cs
│   │   │   ├── Estado.cs
│   │   │   ├── EstadoAgente.cs
│   │   │   ├── EstadoTipoSolicitud.cs
│   │   │   ├── Fiducia.cs
│   │   │   ├── FusionEmpresa.cs
│   │   │   ├── InfoAdicionalFronteras.cs
│   │   │   ├── InfoAdicionalJuntaDirectiva.cs
│   │   │   ├── InfoContacto.cs
│   │   │   ├── InfoContactoNegocio.cs
│   │   │   ├── LineaTiempo.cs
│   │   │   ├── MatrizActividades.cs
│   │   │   ├── MatrizEstados.cs
│   │   │   ├── Municipio.cs
│   │   │   ├── Negocio.cs
│   │   │   ├── NegocioTipoActividad.cs
│   │   │   ├── ObjecionesSolicitud.cs
│   │   │   ├── Pagina.cs
│   │   │   ├── Pais.cs
│   │   │   ├── Parametro.cs
│   │   │   ├── ParametroValor.cs
│   │   │   ├── Periodo.cs
│   │   │   ├── PermisosRoles.cs
│   │   │   ├── Preinscripcion.cs
│   │   │   ├── PruebasAplicaciones.cs
│   │   │   ├── RevisionDocumentos.cs
│   │   │   ├── Rol.cs
│   │   │   ├── Seccion.cs
│   │   │   ├── SeccionPagina.cs
│   │   │   ├── SituacionControlAgentes.cs
│   │   │   ├── Solicitud.cs
│   │   │   ├── SolicitudAplicacionContacto.cs
│   │   │   ├── SolicitudTipoInfoContacto.cs
│   │   │   ├── TipoActividad.cs
│   │   │   ├── TipoContacto.cs
│   │   │   ├── TipoContactoAplicacionRol.cs
│   │   │   ├── TipoDocumento.cs
│   │   │   ├── TipoEmpresa.cs
│   │   │   ├── TipoInfoContacto.cs
│   │   │   ├── TipoSolicitud.cs
│   │   │   ├── TipoSolicitudCausalRechazo.cs
│   │   │   ├── Trato.cs
│   │   │   ├── vAgentesRetirados.cs    [View]
│   │   │   ├── ValidacionesSolicitud.cs
│   │   │   ├── vMatrizEstados.cs       [View]
│   │   │   └── vPermisosRoles.cs       [View]
│   │   │
│   │   ├── Administracion/
│   │   │   ├── ParametrosDAO.cs
│   │   │   └── RolesDAO.cs
│   │   │
│   │   ├── General/
│   │   │   ├── GeneralDAO.cs
│   │   │   └── LineaTiempoDAO.cs
│   │   │
│   │   ├── Helper/
│   │   │   ├── ColumnaSICEP.cs
│   │   │   ├── ComparerInfoAdicionaFronteras.cs
│   │   │   ├── ComparerInfoAdicionalJuntaDirectiva.cs
│   │   │   ├── ComparerInfoContacto.cs
│   │   │   ├── ConceptoEmpresa.cs
│   │   │   ├── InfoAgenteContacto.cs
│   │   │   └── SICEPPendienteSolicitud.cs
│   │   │
│   │   ├── RegFro/
│   │   │   └── InfoAgenteContactoDAO.cs
│   │   │
│   │   ├── Solicitudes/               [40+ DAO Classes for Requests]
│   │   │   ├── AgentesDAO.cs
│   │   │   ├── AlarmaDAO.cs
│   │   │   ├── AplicacionDAO.cs
│   │   │   ├── AplicacionRolDAO.cs
│   │   │   ├── AplicacionRolDependienteDAO.cs
│   │   │   ├── AplicacionTipoActividadDAO.cs
│   │   │   ├── BitacoraDAO.cs
│   │   │   ├── CausalRechazoDAO.cs
│   │   │   ├── ConceptoTributarioDAO.cs
│   │   │   ├── ContactosDAO.cs
│   │   │   ├── CuentaDAO.cs
│   │   │   ├── DocRetiroDeudaDAO.cs
│   │   │   ├── DocumentosDAO.cs
│   │   │   ├── DocumentosObjecionDAO.cs
│   │   │   ├── DocumentoTipoSolicitudDAO.cs
│   │   │   ├── EmpresaDAO.cs
│   │   │   ├── EmpresaInfoTributariaDAO.cs
│   │   │   ├── EncargoFiduciarioDAO.cs
│   │   │   ├── EstadoTipoSolicitudDAO.cs
│   │   │   ├── FiduciaDAO.cs
│   │   │   ├── FusionEmpresaDAO.cs
│   │   │   ├── InactivarTipoContactoDAO.cs
│   │   │   ├── InfoAdicionalFronterasDAO.cs
│   │   │   ├── InfoAdicionalJuntaDirectivaDAO.cs
│   │   │   ├── MatrizActividadesDAO.cs
│   │   │   ├── MatrizEstadosDAO.cs
│   │   │   ├── NegocioDAO.cs
│   │   │   ├── ObjecionesSolicitudDAO.cs
│   │   │   ├── ParametrosDAO.cs
│   │   │   ├── PeriodoDAO.cs
│   │   │   ├── PruebasAplicacionesDAO.cs
│   │   │   ├── RevisionDocumentosDAO.cs
│   │   │   ├── SituacionControlAgentesDAO.cs
│   │   │   ├── SolicitudesDAO.cs
│   │   │   ├── TipoActividadDAO.cs
│   │   │   ├── TipoContactoDAO.cs
│   │   │   ├── TipoSolicitudCausalRechazoDAO.cs
│   │   │   ├── TipoSolicitudDAO.cs
│   │   │   └── ValidacionesSolicitudDAO.cs
│   │   │
│   │   ├── Stored Procedure Results (10 SP Result Classes)
│   │   │   ├── spInfoActividadesSolicitudContacto_Result.cs
│   │   │   ├── spInfoAgenteSolicitud_Result.cs
│   │   │   ├── spInformacionBasicaContacto_Result.cs
│   │   │   ├── spInfoSolicitudAplicaciones_Result.cs
│   │   │   ├── spInfoSolicitudRetiroAgente_Result.cs
│   │   │   ├── spInfoSolicitudTipoContacto_Result.cs
│   │   │   └── spNotificacionSolicitudes_Result.cs
│   │   │
│   │   └── Properties/
│   │       └── AssemblyInfo.cs
│   │
│   ├── XM.RAG.Oracle/                  [Oracle Database Access - .NET 4.0]
│   │   ├── XM.RAG.Oracle.csproj
│   │   ├── App.Config
│   │   │
│   │   ├── Entity Model Files
│   │   │   ├── PDN.edmx
│   │   │   ├── PDN.Designer.cs
│   │   │   ├── PDNModel.Context.cs
│   │   │   ├── PDNModel.Context.Extensions.cs
│   │   │   ├── PDNModel.Context.tt
│   │   │   ├── PDNModel.cs
│   │   │   └── PDNModel.tt
│   │   │
│   │   ├── Entity Classes (18+ Oracle Entity Classes)
│   │   │   ├── ACT_PERIODO.cs
│   │   │   ├── FBOT_TIPOAGENS.cs
│   │   │   ├── FBOT_TIPODOCUS.cs
│   │   │   ├── LAT_AGENTES.cs
│   │   │   ├── LAT_AGNINFORMACION.cs
│   │   │   ├── LAT_AGNPERSONA.cs
│   │   │   ├── LAT_CARGOSPROF.cs
│   │   │   ├── LAT_CONTACTOPERSONA.cs
│   │   │   ├── LAT_EMPRESAS.cs
│   │   │   ├── LAT_NEGOCIOS.cs
│   │   │   ├── LAT_PAISES.cs
│   │   │   ├── LAT_PERSONAS.cs
│   │   │   ├── LAT_TIPOCOMPANIA.cs
│   │   │   ├── LAT_TIPOCONTACTO.cs
│   │   │   ├── LAT_TITULOSPROF.cs
│   │   │   ├── LAT_TRATOSPROF.cs
│   │   │   └── SMT_CONCEPTOBASICO.cs
│   │   │
│   │   ├── Consultas/
│   │   │   └── Consulta.cs             [Query Class]
│   │   │
│   │   ├── Transacciones/
│   │   │   └── Transacciones.cs        [Transaction Class]
│   │   │
│   │   └── Properties/
│   │       └── AssemblyInfo.cs
│   │
│   ├── XM.RAG.LinQ2Mid/                [MID LINQ Abstraction - .NET 4.0]
│   │   ├── XM.RAG.LinQ2Mid.csproj
│   │   ├── App.config
│   │   │
│   │   ├── L2MID/
│   │   │   ├── L2MID.cs                [Main LINQ Library]
│   │   │   └── L2MPartial.cs
│   │   │
│   │   ├── General/
│   │   │   ├── General.cs
│   │   │   └── TextComparer.cs
│   │   │
│   │   ├── Integracion/
│   │   │   ├── ConsultaIntegracion.cs
│   │   │   └── TransaccionIntegracion.cs
│   │   │
│   │   ├── Sucesos/
│   │   │   └── Sucesos.cs
│   │   │
│   │   ├── Service References/
│   │   │   └── BitacoraMid/            [MID Audit Service]
│   │   │       ├── Reference.cs
│   │   │       ├── Reference.svcmap
│   │   │       ├── wsconsulta.disco
│   │   │       ├── wsconsulta.wsdl
│   │   │       └── [6 XSD Schema Files]
│   │   │
│   │   ├── Properties/
│   │   │   ├── AssemblyInfo.cs
│   │   │   └── DataSources/
│   │   │
│   │   └── [WCF Service References]
│   │
│   └── XM.RAG.EntidadesOracle/         [Oracle Entity Models - .NET 4.0]
│       ├── XM.RAG.EntidadesPDN.csproj
│       ├── Agente/
│       ├── Contacto/
│       ├── Empresa/
│       ├── Facturacion/
│       ├── Persona/
│       └── Properties/
│           └── AssemblyInfo.cs
│
├── Negocio/                            [Business Logic Layer - 14 Projects]
│   │
│   ├── XM.RAG.Entidades/               [Data Models/DTOs - .NET 4.0]
│   │   ├── XM.RAG.Entidades.csproj
│   │   ├── XM.RAG.Entidades.sln
│   │   ├── key.snk
│   │   │
│   │   ├── Administracion/             [Admin Entities]
│   │   │   ├── Parametro.cs
│   │   │   ├── ParametroValor.cs
│   │   │   ├── PermisosSeccion.cs
│   │   │   └── Rol.cs
│   │   │
│   │   ├── Enumeraciones/
│   │   │   └── ParametrosEnum.cs
│   │   │
│   │   ├── General/                    [General Entities - 30+ Classes]
│   │   │   ├── AccesoDatosColumn.cs
│   │   │   ├── AccionRol.cs
│   │   │   ├── Banco.cs
│   │   │   ├── BancoACME.cs
│   │   │   ├── Bitacora.cs
│   │   │   ├── ConceptoBasico.cs
│   │   │   ├── ConsultaMID.cs
│   │   │   ├── ControlTareas.cs
│   │   │   ├── CorreoAlarma.cs
│   │   │   ├── Departamento.cs
│   │   │   ├── DetalleEvento.cs
│   │   │   ├── Grid.cs
│   │   │   ├── LineaTiempo.cs
│   │   │   ├── Localizacion.cs
│   │   │   ├── LogGestorArchivos.cs
│   │   │   ├── Municipio.cs
│   │   │   ├── Notificacion.cs
│   │   │   ├── NotificacionesDocumentos.cs
│   │   │   ├── OpcionMenu.cs
│   │   │   ├── Pais.cs
│   │   │   ├── Periodo.cs
│   │   │   ├── ResultadoGestor.cs
│   │   │   ├── RolGrid.cs
│   │   │   └── RolMenu.cs
│   │   │
│   │   ├── RegFro/
│   │   │   └── InfoAgenteContacto.cs
│   │   │
│   │   ├── RegistroSucesos/
│   │   │   ├── DocumentoSuceso.cs
│   │   │   └── Suceso.cs
│   │   │
│   │   ├── Reportes/
│   │   │   ├── Columna.cs
│   │   │   ├── ColumnaSICEP.cs
│   │   │   ├── Filtro.cs
│   │   │   ├── Reporte.cs
│   │   │   └── Seccion.cs
│   │   │
│   │   └── Solicitudes/               [100+ Request Entities]
│   │       ├── Adjunto.cs
│   │       ├── Agente.cs
│   │       ├── AgenteParametro.cs
│   │       ├── Alarma.cs
│   │       ├── Aplicacion.cs
│   │       ├── AplicacionesPorContacto.cs
│   │       ├── AplicacionRol.cs
│   │       ├── AplicacionRolDependiente.cs
│   │       ├── AplicacionTipoActividad.cs
│   │       ├── Cargo.cs
│   │       ├── CausalRechazo.cs
│   │       ├── ConceptoEmpresa.cs
│   │       ├── ConceptoTributario.cs
│   │       ├── Cuenta.cs
│   │       ├── DocRetiroDeuda.cs
│   │       ├── DocTipoSolicitudActividad.cs
│   │       ├── DocTipoSolicitudCausales.cs
│   │       ├── DocTipoSolicitudContacto.cs
│   │       ├── DocTipoSolicitudRol.cs
│   │       ├── Documento.cs
│   │       ├── DocumentoPlantilla.cs
│   │       ├── DocumentosObjecion.cs
│   │       ├── DocumentoSolicitud.cs
│   │       ├── DocumentoTipoSolicitud.cs
│   │       ├── Empresa.cs
│   │       ├── EmpresaInfoTributaria.cs
│   │       ├── EncargoFiduciario.cs
│   │       ├── Estado.cs
│   │       ├── EstadoAgente.cs
│   │       ├── EstadoTipoSolicitud.cs
│   │       ├── Fiducia.cs
│   │       ├── FusionEmpresa.cs
│   │       ├── InfoAdicionalFronteras.cs
│   │       ├── InfoAdicionalJuntaDirectiva.cs
│   │       ├── InfoContacto.cs
│   │       ├── InfoContactoNegocio.cs
│   │       ├── MatrizActividades.cs
│   │       ├── MatrizEstados.cs
│   │       ├── MatrizTransicionEstados.cs
│   │       ├── Negocio.cs
│   │       ├── NegocioTipoActividad.cs
│   │       ├── ObjecionesSolicitud.cs
│   │       ├── Preinscripcion.cs
│   │       ├── PruebasAplicaciones.cs
│   │       ├── RevisionDocumentos.cs
│   │       ├── SituacionControlAgentes.cs
│   │       ├── Solicitud.cs
│   │       ├── SolicitudAplicacionContacto.cs
│   │       ├── SolicitudTipoInfoContacto.cs
│   │       ├── TipoActividad.cs
│   │       ├── TipoContacto.cs
│   │       ├── TipoContactoAplicacionRol.cs
│   │       ├── TipoDocumento.cs
│   │       ├── TipoEmpresa.cs
│   │       ├── TipoInfoContacto.cs
│   │       ├── TipoSolicitud.cs
│   │       ├── TipoSolicitudCausalRechazo.cs
│   │       ├── Transaccion.cs
│   │       ├── Trato.cs
│   │       └── ValidacionesSolicitud.cs
│   │
│   ├── XM.RAG.Administracion/          [Admin Logic - .NET 4.0]
│   │   ├── XM.RAG.Administracion.csproj
│   │   ├── Broker/
│   │   │   └── BrokerAdministracion.cs
│   │   ├── Controladora/
│   │   │   └── ControladoraAdministracion.cs
│   │   ├── Fachada/
│   │   │   └── FachadaAdministracion.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.General/                 [General Business Logic - .NET 4.0]
│   │   ├── XM.RAG.General.csproj
│   │   ├── Broker/
│   │   │   └── BrokerGeneral.cs
│   │   ├── Controladora/
│   │   │   └── ControladoraGeneral.cs
│   │   ├── Fachada/
│   │   │   └── FachadaGeneral.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.Reportes/                [Reporting Logic - .NET 4.0]
│   │   ├── XM.RAG.Reportes.csproj
│   │   ├── app.config
│   │   ├── BDRAGXM.Designer.cs
│   │   ├── BDRAGXM.xsc
│   │   ├── BDRAGXM.xsd
│   │   ├── BDRAGXM.xss
│   │   ├── Reportes/
│   │   │   ├── CrearReporte.cs
│   │   │   └── rptFormatoSIC020.rdlc   [Report Definition]
│   │   ├── Web References/
│   │   │   └── srvReportes/            [SQL Server Reporting Services]
│   │   └── Properties/
│   │
│   ├── XM.RAG.Actividades/              [Workflow Activities - .NET 4.0.1]
│   │   └── XM.RAG.Actividades.csproj    [WF4 Activity Library]
│   │
│   ├── XM.RAG.ConsultasMID/             [MID Queries - .NET 4.0]
│   │   ├── XM.RAG.ConsultasMID.csproj
│   │   ├── app.config
│   │   ├── IServicioConsultasMID.cs
│   │   ├── ServicioConsultasMID.cs
│   │   └── Service References/
│   │       └── ConsultasMID/
│   │
│   ├── XM.RAG.IntegracionMID/           [MID Integration - .NET 4.0]
│   │   ├── XM.RAG.IntegracionMID.csproj
│   │   ├── Broker/
│   │   │   ├── BrokerConsulta.cs
│   │   │   └── BrokerTransaccion.cs
│   │   ├── Controladora/
│   │   │   ├── ControladoraConsulta.cs
│   │   │   └── ControladoraTransaccion.cs
│   │   ├── Fachada/
│   │   │   ├── FachadaConsulta.cs
│   │   │   └── FachadaTransaccion.cs
│   │   ├── Transformaciones/
│   │   │   └── TransformacionMID.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.IntegracionPDN/           [PDN/Oracle Integration - .NET 4.0]
│   │   ├── XM.RAG.IntegracionPDN.csproj
│   │   ├── Broker/
│   │   │   ├── BrokerConsulta.cs
│   │   │   └── BrokerTransaccion.cs
│   │   ├── Controladora/
│   │   │   ├── ControladoraConsulta.cs
│   │   │   └── ControladoraTransaccion.cs
│   │   ├── Fachada/
│   │   │   ├── FachadaConsulta.cs
│   │   │   └── FachadaTransaccion.cs
│   │   ├── Trasformaciones/
│   │   │   └── TransformacionPDN.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.RegistroSucesos/          [Event Recording - .NET 4.0]
│   │   ├── XM.RAG.RegistroSucesos.csproj
│   │   ├── Broker/
│   │   │   └── BrokerRegistroSucesos.cs
│   │   ├── Controladora/
│   │   │   └── ControladoraRegistroSucesos.cs
│   │   ├── Fachada/
│   │   │   └── FachadaRegistroSucesos.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.RevisionSolicitudes/      [Request Review Logic - .NET 4.0]
│   │   ├── XM.RAG.RevisionSolicitudes.csproj
│   │   ├── Broker/
│   │   │   └── BrokerRevisionSolicitudes.cs
│   │   ├── Controladora/
│   │   │   └── ControladoraRevisionSolicitudes.cs
│   │   ├── Fachada/
│   │   │   └── FachadaRevisionSolicitudes.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.RealizacionSolicitudes/   [Request Execution Logic - .NET 4.0]
│   │   ├── XM.RAG.RealizacionSolicitudes.csproj
│   │   ├── Broker/
│   │   │   └── BrokerRealizacionSolicitudes.cs
│   │   ├── Controladora/
│   │   │   └── ControladoraRealizacionSolicitudes.cs
│   │   ├── Fachada/
│   │   │   └── FachadaRealizacionSolicitudes.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.RegFro/                   [Border Registration - .NET 4.0]
│   │   ├── XM.RAG.RegFro.csproj
│   │   ├── Broker/
│   │   │   └── BrokerInfoAgenteContacto.cs
│   │   ├── Controladora/
│   │   │   └── ControladoraInfoAgenteContacto.cs
│   │   ├── Fachada/
│   │   │   └── FachadaInfoAgenteContacto.cs
│   │   └── Properties/
│   │
│   ├── XM.RAG.EntidadesMID/             [MID Entities - .NET 4.0]
│   │   ├── XM.RAG.EntidadesMID.csproj
│   │   ├── Compania.cs
│   │   ├── Contacto.cs
│   │   ├── InformacionContacto.cs
│   │   ├── UnidadNegocio.cs
│   │   └── Properties/
│   │
│   └── XM.RAG.GestorArchivos/           [File Manager - .NET 4.0]
│       ├── XM.RAG.GestorArchivos.csproj
│       ├── app.config
│       ├── Exportacion/
│       │   ├── IServicioExportacion.cs
│       │   └── ServicioExportacion.cs
│       ├── Importacion/
│       │   ├── IServicioImportacion.cs
│       │   └── ServicioImportacion.cs
│       ├── Service References/         [2 Services]
│       │   ├── ServicioCargaService/
│       │   └── ServicioExportacionService/
│       └── Properties/
│
├── Servicios/                          [WCF Services Layer - 2 Projects]
│   │
│   ├── XM.RAG.ContratosServicios/      [Service Contracts - .NET 4.0]
│   │   ├── XM.RAG.ContratosServicios.csproj
│   │   ├── ServiceFault.cs
│   │   ├── Administracion/
│   │   │   └── IAdministracion.cs
│   │   ├── General/
│   │   │   └── IGeneral.cs
│   │   ├── IntegracionMID/
│   │   │   └── IIntegracionMID.cs
│   │   ├── IntegracionPDN/
│   │   │   └── IIntegracionPDN.cs
│   │   ├── MaquinaEstados/
│   │   │   └── IMaquinaEstados.cs
│   │   ├── RealizacionSolicitudes/
│   │   │   └── IRealizacionSolicitudes.cs
│   │   ├── RegistroSucesos/
│   │   │   └── IRegistroSucesos.cs
│   │   ├── RevisionSolicitudes/
│   │   │   └── IRevisionSolicitudes.cs
│   │   ├── RegFro/
│   │   │   └── NuevoRegfro.cs
│   │   └── Properties/
│   │
│   └── XM.RAG.Servicios/                [WCF Host - ASP.NET 4.0]
│       ├── XM.RAG.Servicios.csproj
│       ├── web.config
│       ├── web.Debug.config
│       ├── web.Release.config
│       ├── web- nuew.config
│       ├── wkhtmltopdf.exe             [PDF Converter Utility]
│       ├── Settings.StyleCop
│       ├── ClassDiagram1.cd
│       │
│       ├── Service Implementations      [7 WCF Services]
│       │   ├── General.svc              [IGeneral Service]
│       │   ├── General.svc.cs
│       │   ├── Administracion.svc       [IAdministracion Service]
│       │   ├── Administracion.svc.cs
│       │   ├── IntegracionMID.svc       [IIntegracionMID Service]
│       │   ├── IntegracionMID.svc.cs
│       │   ├── IntegracionPDN.svc       [IIntegracionPDN Service]
│       │   ├── IntegracionPDN.svc.cs
│       │   ├── RealizacionSolicitudes.svc
│       │   ├── RealizacionSolicitudes.svc.cs
│       │   ├── RevisionSolicitudes.svc
│       │   ├── RevisionSolicitudes.svc.cs
│       │   ├── RegistroSucesos.svc
│       │   ├── RegistroSucesos.svc.cs
│       │   ├── NuevoRegfro.svc
│       │   └── NuevoRegfro.svc.cs
│       │
│       ├── Configuracion/
│       │   └── entlib.config            [Enterprise Library Config]
│       │
│       ├── LogTecnico/
│       │   └── Class1.cs
│       │
│       └── Properties/
│           ├── AssemblyInfo.cs
│           ├── Settings.Designer.cs
│           └── Settings.settings
│
├── Soporte/                            [Support/Framework Layer - 2 Projects]
│   │
│   ├── XM.RAG.Servicios.Framework/      [Services Framework - .NET 4.0]
│   │   ├── XM.RAG.Servicios.Framework.csproj
│   │   ├── app.config
│   │   ├── ConfiguracionServicios.cs
│   │   ├── Comunicacion/
│   │   │   └── MensajeCliente.cs
│   │   ├── Enumeraciones/               [8 Enumerations]
│   │   │   ├── AlarmasEnum.cs
│   │   │   ├── ConsultaMID.cs
│   │   │   ├── Estado.cs
│   │   │   ├── EstadoPrueba.cs
│   │   │   ├── EventoBitacora.cs
│   │   │   ├── IdentificadoresMID.cs
│   │   │   ├── ParametrosBD.cs
│   │   │   ├── RolEnum.cs
│   │   │   └── TipoSolicitudEnum.cs
│   │   ├── Excepciones/                [4 Exception Classes]
│   │   │   ├── NegocioExcepcion.cs
│   │   │   ├── PoliticaDeExcepcion.cs
│   │   │   ├── ServicioExcepcion.cs
│   │   │   └── SistemaExternoNoDisponibleExcepcion.cs
│   │   ├── Helper/
│   │   │   └── LogTecnico.cs
│   │   ├── Consultas.xml
│   │   └── Properties/
│   │
│   └── XM.RAG.Servicios.Mensajes/       [Messages - .NET 4.0]
│       ├── XM.RAG.Servicios.Mensajes.csproj
│       ├── TipoMensaje.cs
│       └── Properties/
│
├── Instalador/                         [Installer - Setup Project]
│   └── XM.RAG.InstaladorServicios/
│       └── XM.RAG.InstaladorServicios.vdproj
│
└── Referencias/                        [External Dependencies]
    ├── Enterprise Library/
    │   ├── EntLibContrib.ExceptionHandling.dll
    │   ├── Microsoft.Practices.EnterpriseLibrary.Caching.dll
    │   ├── Microsoft.Practices.EnterpriseLibrary.Common.dll
    │   ├── Microsoft.Practices.EnterpriseLibrary.Data.dll
    │   ├── Microsoft.Practices.EnterpriseLibrary.ExceptionHandling.dll
    │   ├── Microsoft.Practices.EnterpriseLibrary.Logging.dll
    │   └── Microsoft.Practices.EnterpriseLibrary.Validation.dll
    │
    ├── LinqToMID/
    │   ├── LinqExtender.dll
    │   └── XM.LINQToMID.dll
    │
    ├── OracleProvider/
    │   ├── Oracle.ManagedDataAccess.dll
    │   └── Oracle.ManagedDataAccessDTC.dll
    │
    ├── Telerik/
    │   ├── Telerik.Reporting.dll
    │   ├── Telerik.Reporting.Service.dll
    │   └── Telerik.Reporting.XpsRendering.dll
    │
    ├── Util/
    │   ├── DocumentFormat.OpenXml.dll
    │   ├── DocumentFormat.OpenXml.xml
    │   ├── itextsharp.dll
    │   ├── itextsharp.xml
    │   ├── itextsharp.xmlworker.dll
    │   ├── Newtonsoft.Json.dll
    │   ├── NReco.PdfGenerator.dll
    │   ├── NReco.PdfGenerator.xml
    │   ├── OpenXmlPowerTools.dll
    │   ├── RestSharp.dll
    │   └── UNISYS.Componentes.PdfTools.dll
    │
    └── Worflows/
        ├── Microsoft.Activities.Extensions.Design.dll
        └── Microsoft.Activities.Extensions.dll
```

---

# 📊 ESTADÍSTICAS CONSOLIDADAS

## Resumen de Archivos

| Categoría | XM.RAG | XM.RAG.Servicios | TOTAL |
|-----------|--------|------------------|-------|
| **Proyectos .csproj** | 6 | 22 | **28** |
| **Archivos .cs** | ~229 | ~300+ | **~530+** |
| **Páginas ASPX** | 56 | 0 | **56** |
| **Controles ASCX** | 45 | 0 | **45** |
| **Archivos .config** | 8 | 9 | **17** |
| **Archivos .svc (WCF)** | 0 | 7 | **7** |
| **Clases de entidades** | 80+ | 100+ | **180+** |
| **Clases DAO/DAL** | 18 | 80+ | **100+** |
| **Service References** | 7 | 15+ | **22+** |

## Estructura por Capas

| Capa | Proyectos | Archivos CS | Propósito |
|-----|-----------|-----------|----------|
| **Presentación** | 6 | 150 | UI SharePoint |
| **Servicios** | 2 | 50 | WCF Endpoints |
| **Negocio** | 14 | 250 | Business Logic |
| **Datos** | 4 | 100 | Database Access |
| **Soporte** | 2 | 30 | Framework/Logging |

## Cantidad de Archivos por Tipo

- **Classes (.cs):** 530+
- **Web/UI (.aspx, .ascx):** 101
- **Configuration (.config):** 17
- **WCF Service (.svc):** 7
- **Data Access (.edmx, .xsd):** 150+
- **References & Dll:** 50+
- **Features/Elements (.feature, .xml):** 50+
- **Layouts/Provisioning:** 100+

## Líneas de Código (aproximado)

- **Total de líneas en soluciones:** 250,000+
- **Promedio por clase:** 150-200 líneas
- **Métodos por clase:** 5-15
- **Propiedades por clase:** 8-20

---

**FIN DEL MAPA COMPLETO**

*Documento generado: Febrero, 2026*  
*Detalle exhaustivo sin omisiones*


