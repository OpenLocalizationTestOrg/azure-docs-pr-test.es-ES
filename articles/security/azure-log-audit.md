---
title: "aaaAzure de registro y auditoría | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar información de registro de datos toogain detallada acerca de la aplicación."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Registro y auditoría de Azure
## <a name="introduction"></a>Introducción
### <a name="overview"></a>Información general
tooassist actuales y potenciales Azure clientes comprender y usar Hola diferentes relacionadas con la seguridad capacidades disponibles en y que rodean Hola plataforma Azure, Microsoft ha desarrollado una serie de notas del producto, información general de seguridad, procedimientos recomendados y las listas de comprobación. temas de Hello en cuanto a la amplitud y la profundidad de intervalo y se actualizan periódicamente. Este documento es parte de esa serie como se resume en hello pasos de la sección abstracta.
### <a name="azure-platform"></a>Plataforma Azure
Azure es una plataforma de servicio de nube abierta y flexible que admite Hola selección más amplia de sistemas operativos, lenguajes de programación, marcos, herramientas, las bases de datos y dispositivos.

Por ejemplo, puede:
-   Ejecutar contenedores de Linux con integración de Docker.

-   Compilar aplicaciones con JavaScript, Python, .NET, PHP, Java y Node.js.

-   Crear back-end para dispositivos iOS, Android y Windows.

Servicios de nube pública de Azure admiten Hola mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza.

Al compilar en, o migrar los activos de TI a un proveedor de nube, está confiando en tooprotect de capacidades de la organización a las aplicaciones y datos con Hola controles hello y servicios proporcionan seguridad de hello toomanage de sus activos en la nube.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus necesidades de seguridad. Además, Azure le proporciona una amplia gama de toocontrol de capacidad de hello y opciones de seguridad configurables usarlas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones. Este documento le ayuda a cumplir estos requisitos.

### <a name="abstract"></a>Descripción breve
La auditoría y el registro de eventos y alertas relacionados con la seguridad son componentes importantes en una estrategia de protección de datos eficaz. Registros de seguridad y los informes proporcionan un registro electrónico de ayuda para detectar patrones que puedan indicar correcta o ha intentado penetración desde el exterior de la red de hello, así como los ataques internos y las actividades sospechosas. Puede utilizar la auditoría toomonitor actividad del usuario, cumplimiento de normas de documento, realizar un análisis forense y mucho más. Las alertas proporcionan notificación inmediata cuando se producen eventos de seguridad.

Productos y servicios de Microsoft Azure proporcionan a la auditoría de seguridad configurables y registro opciones toohelp identificar interrupciones en las directivas de seguridad y los mecanismos y los toohelp de espacios de direcciones evitar infracciones. Servicios de Microsoft ofrecen algunas (y en algunos casos, todos los) de hello siguientes opciones: supervisión, registro y análisis sistemas tooprovide una visibilidad continua; centralizada alertas oportunas; y toohelp informes que administrar Hola mucha información generada por dispositivos y servicios.

Datos de registro de Microsoft Azure pueden ser exportado tooSecurity sistemas de incidentes y administración de eventos (SIEM) para el análisis y se integran con soluciones de auditoría de terceros.

Estas notas del producto proporcionan una introducción a la generación, recopilación y análisis de los registros de seguridad de los servicios hospedados en Azure, y pueden ayudarle a conocer más detalladamente la seguridad de sus implementaciones de Azure. ámbito de Hola de estas notas del producto es tooapplications limitado y servicios compilado e implementado en Azure.

> [!Note]
> Algunas de las recomendaciones de este artículo pueden provocar un aumento del uso de datos, de la red o de recursos de proceso, lo que incrementará los costes de las licencias o suscripciones.

## <a name="types-of-logs-in-azure"></a>Tipos de registros de Azure
Las aplicaciones de nube son complejas y tienen muchas partes móviles. Registros ofrecen tooensure de datos que mantiene la aplicación y en ejecución en un estado correcto. También ayuda a toostave off posibles problemas o solucionar problemas más allá de los. Además, puede usar información detallada de toogain de datos de registro acerca de la aplicación. Esa información puede ayudarle a rendimiento de la aplicación de tooimprove o mantenimiento o automatizar acciones que en caso contrario requerirían intervención manual.

Azure genera gran cantidad de registros para cada servicio. Estos registros se clasifican en estos tipos principales:
-   **Registros de control/management** obtener una visibilidad en hello las operaciones de administrador de recursos de Azure cree, UPDATE y DELETE. Los [registros de actividad de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) son un ejemplo de este tipo de registro.

-   **Datos plano registros** obtener una visibilidad en los eventos de hello provoca como parte del uso de Hola de un recurso de Azure. Ejemplos de este tipo de registro son Hola eventos de Windows System, seguridad, y registros de aplicación en una máquina virtual y hello [registros de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) configurado a través del Monitor de Azure


-   **Eventos procesados**, que aportan información sobre eventos y alertas analizados que se han procesado en su nombre. Ejemplos de este tipo son las [alertas de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts), donde [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) ha procesado y analizado su suscripción, y proporciona unas alertas de seguridad concisas.

siguiente Hola tabla tipo más importante de lista de registros disponibles en Azure.

| Categoría del registro | Tipo de registro | Usos | Integración |
| ------------ | -------- | ------ | ----------- |
|[Registros de actividad](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Eventos de plano de control de los recursos de Azure Resource Manager| Proporcionar una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción.|   API de REST y [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Registros de diagnóstico de Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|datos frecuentes acerca de la operación Hola de recursos de Azure Resource Manager de suscripción| Proporcionan información detallada sobre las operaciones que el mismo recurso realiza.| Azure Monitor, [Stream](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[Informes de AAD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Registros e informes|Actividades de inicio de sesión de usuario e información de actividades del sistema acerca de la administración de grupos y usuarios|[API Graph](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Máquina virtual y servicios en la nube](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Registro de eventos de Windows y Syslog de Linux|  Captura de datos del sistema y datos de registro en máquinas virtuales de Hola y transfiere esos datos en una cuenta de almacenamiento de su elección.| Windows con [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (almacenamiento de Microsoft Azure Diagnostics) y Linux en Azure Monitor|
|[Storage Analytics](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Registro de almacenamiento y proporciona datos de métricas para una cuenta de almacenamiento.|Proporciona información detallada sobre seguimiento de solicitudes, análisis de tendencias de uso y diagnóstico de problemas con la cuenta de almacenamiento.|  API de REST o hello [biblioteca de cliente](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[Registros de flujos de NSG (grupo de seguridad de red)](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|Formato JSON y muestra flujos entrantes y salientes por cada regla|Consulte información sobre el tráfico IP de entrada y salida a través de un grupo de seguridad de red|[Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Registros, excepciones y diagnósticos personalizados|  Servicio de Application Performance Management (APM) para desarrolladores web en varias plataformas.| API de REST, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Datos de proceso/alerta de seguridad| Alerta de Azure Security Center, alerta de OMS| Información y alertas de seguridad|   API de REST, JSON|

### <a name="activity-log"></a>Registro de actividad
Hola [Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción. Hello registro de actividad se conocía anteriormente como "Registros de auditoría" o "Registros operativos", ya que informa de [plano de control de eventos](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) para las suscripciones. Gracias a Hola registro de actividad, puede determinar Hola "qué, quién y cuándo" para las operaciones (PUT, POST, DELETE) realizadas en los recursos de hello en su suscripción de escritura. También puede entender el estado Hola de operación de Hola y otras propiedades relevantes. Registro de actividad de Hola no incluye las operaciones de lectura (GET).

Aquí PUT, POST, DELETE hace referencia a las operaciones de escritura de hello tooall contiene el registro de actividad en los recursos de Hola. Por ejemplo, puede utilizar toofind de registros de actividad de hello un error para solucionar el problema o toomonitor cómo un usuario de su organización modifica un recurso.

![Registro de actividad](./media/azure-log-audit/azure-log-audit-fig1.png)


Puede recuperar eventos desde el registro de actividad mediante Hola portal de Azure, [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), cmdlets de PowerShell, y [API de REST de Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Los registros de actividad tienen un período de retención de datos de 19 días.

Escenarios de integración
-   [Crear una alerta de correo electrónico o webhook que se desencadene con un evento de registro de actividad.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Transmitir tooan concentrador de eventos](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) para ingesta por un servicio de otro fabricante o una solución de análisis personalizada como Power BI.

-   Analizar en Power BI con hello [paquete de contenido de Power BI.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Guárdelo tooa cuenta de almacenamiento para la inspección de archivado o manual.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Puede especificar el tiempo de retención de hello (en días) mediante perfiles de registro.

-   Consultar y ver en hello portal de Azure.

-   Consultarlo mediante un cmdlet de PowerShell, la CLI o la API de REST.

-   Exportar registro de actividad con los perfiles de registro de hello demasiado[análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Puede usar una cuenta de almacenamiento o [espacio de nombres de concentrador de eventos](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) que no está en Hola misma suscripción como Hola un registro de emisor. usuario de Hola que configura los valores de hello debe tener Hola adecuado [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) acceder a suscripciones tooboth
### <a name="azure-diagnostic-logs"></a>Registros de diagnóstico de Azure
Registros de diagnóstico de Azure se emiten por un recurso que proporcionan datos enriquecidos y frecuentes acerca de la operación de Hola de ese recurso. contenido de Hola de estos registros varía según el tipo de recurso (por ejemplo, [registros de sistema de eventos de Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)son una categoría de registro de diagnóstico para máquinas virtuales y [blob, tabla y los registros de cola](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) categorías de registros de diagnóstico las cuentas de almacenamiento) y se diferencian de hello registro de actividad, que proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción.

![Registros de diagnóstico de Azure](./media/azure-log-audit/azure-log-audit-fig2.png)

Los registros de diagnóstico de Azure ofrecen varias opciones de configuración: Azure Portal, con PowerShell, la interfaz de línea de comandos (CLI) y API de REST.

**Escenarios de integración**
-   Guardarlos tooa [cuenta de almacenamiento](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) para la inspección de auditoría o manual. Puede especificar el tiempo de retención de hello (en días) con la configuración de diagnóstico de Hola.

-   [Transmitirlos concentradores tooEvent](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) para ingesta por un servicio de otro fabricante o una solución de análisis personalizada como [Power BI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Analizarlos con [Log Analytics de OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

**Servicios admitidos, esquema para registros de diagnóstico y categorías de registro admitidas por tipo de recurso**


| Servicio | Esquema y documentos | Tipo de recurso | Categoría |
| ------- | ------------- | ------------- | -------- |
|Load Balancer| [Análisis del registros para el Equilibrador de carga de Azure (vista previa)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Grupos de seguridad de red|[Análisis del registro para grupos de seguridad de red (NSG)](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Puertas de enlace de aplicaciones|[Registro de diagnóstico para la Puerta de enlace de aplicaciones](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Key Vault|[Registro del Almacén de claves de Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Búsqueda de Azure|[Habilitación y uso de Análisis de tráfico de búsqueda](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Data Lake Store|[Acceso a los registros de diagnóstico de Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Auditoría|
|Data Lake Analytics|[Acceso a los registros de diagnóstico de Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Auditoría|
|||Microsoft.DataLakeAnalytics/accounts|Solicitudes|
|||Microsoft.DataLakeStore/accounts|Solicitudes|
|Logic Apps|[Esquema de seguimiento personalizado de Logic Apps B2B](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Registros de diagnósticos de Azure Batch](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Automatización de Azure|[Log Analytics para Azure Automation](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Event Hubs|[Registros de diagnóstico de Azure Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Stream Analytics|[Registros de diagnósticos de trabajos](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Ejecución|
|||Microsoft.StreamAnalytics/streamingjobs|Creación|
|Service Bus|[Registros de diagnóstico de Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Informes de Azure Active Directory
Azure Active Directory (Azure AD) incluye informes de seguridad, actividad y auditoría para el directorio. Hola [informe de auditoría de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) ayuda a los clientes acciones tooidentify con privilegios que se ha producido en su Azure Active Directory. Las acciones con privilegios incluyen cambios de elevación (por ejemplo, creación de roles o los restablecimientos de contraseña), cambiar las configuraciones de directiva (por ejemplo las directivas de contraseña), o la configuración de toodirectory de cambios (por ejemplo, configuración de federación de cambios toodomain).

informes de Hello proporcionan registro de auditoría de Hola para nombre del evento hello, actor Hola que realiza la acción de hello, recurso de destino de hello afectado por el cambio de Hola y Hola fecha y hora (en UTC). Los clientes están lista de hello tooretrieve capaz de eventos de auditoría para su Azure Active Directory a través de hello [portal de Azure](https://portal.azure.com/), tal y como se describe en [ver los registros de auditoría](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Presentamos una lista de informes de hello incluidas:

| Informes de seguridad | Informes de actividad | Informes de auditoría |
| :--------------- | :--------------- | :------------ |
|Inicios de sesión desde orígenes desconocidos| Uso de la aplicación: resumen| Informe de auditoría de directorio|
|Inicios de sesión tras varios errores|  Uso de la aplicación: detallado||
|Inicios de sesión desde varias ubicaciones geográficas|    Panel de la aplicación||
|Inicios de sesión desde direcciones IP con actividad sospechosa|   Errores de aprovisionamiento de cuentas||
|Actividad de inicio de sesión irregular|    Dispositivos de usuario individuales||
|Inicios de sesión desde dispositivos posiblemente infectados|   Actividad de usuario individual||
|Usuarios con actividad de inicio de sesión anómala| Informe de actividad de grupos||
||Informe de actividad de registro de restablecimiento de contraseña||
||Actividad de restablecimiento de contraseña|||

datos de Hola de estos informes pueden ser aplicaciones de tooyour útil, como sistemas SIEM, auditoría y herramientas de business intelligence. Hello Azure AD reporting que API proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST. Se puede llamar a estas [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) desde diversos lenguajes de programación y herramientas.

Eventos de hello informe de auditoría de AD de Azure se conservan durante 180 días.

> [!Note]
> Para más información sobre la retención de los informes, consulte [Directivas de retención de informes de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Para clientes interesados en almacenar sus eventos de auditoría durante largos períodos de retención, hello API de informes se pueden utilizar extracción tooregularly [eventos de auditoría](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) en un almacén de datos independiente.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Registros de máquinas virtuales que usan Diagnósticos de Azure
[Diagnósticos de Azure](https://docs.microsoft.com/azure/azure-diagnostics) es la capacidad de hello dentro de Azure que habilita la recopilación de Hola de datos de diagnóstico en una aplicación implementada. Puede usar la extensión de diagnósticos de Hola de varios orígenes diferentes. Actualmente se admiten [roles web y de trabajo del servicio en la nube de Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me).

![Registros de máquinas virtuales que usan Diagnósticos de Azure](./media/azure-log-audit/azure-log-audit-fig3.png)

[Azure Virtual Machines](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) con Microsoft Windows y [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Puede habilitar el Diagnóstico de Azure en una máquina virtual mediante las opciones siguientes:

-   Uso de Visual Studio, consulte [tootrace utilice Visual Studio máquinas virtuales de Azure](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Configuración de Diagnósticos de Azure en Azure Virtual Machine de forma remota](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Usar PowerShell tooset de diagnóstico en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Creación de una máquina virtual de Windows con supervisión y diagnóstico mediante una plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>Storage Analytics
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento. Puede utilizar este solicitudes de tootrace de datos, analizar las tendencias de uso y diagnosticar problemas con su cuenta de almacenamiento. Registro de análisis de almacenamiento está disponible para hello [servicios Blob, cola y tabla.](https://docs.microsoft.com/azure/storage/storage-introduction) Análisis de almacenamiento registra información detallada acerca del servicio de almacenamiento de tooa de solicitudes correctas e incorrectas.

Esta información puede ser problemas de toodiagnose con un servicio de almacenamiento y las solicitudes individuales de toomonitor usado. Las solicitudes se registran en función de la mejor opción. Las entradas del registro se crean solo si hay las solicitudes realizadas en el extremo de servicio de Hola. Por ejemplo, si una cuenta de almacenamiento tiene actividad en su extremo de Blob pero no en sus puntos de conexión de la tabla o cola, solamente registra pertenecen toohello servicio Blob se crea.

toouse análisis de almacenamiento, debe habilitarla individualmente para cada servicio que desee toomonitor. Puede habilitarlo en hello [portal de Azure](https://portal.azure.com/); para obtener más información, consulte [supervisar una cuenta de almacenamiento en hello portal de Azure.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) También puede habilitar el análisis de almacenamiento mediante programación a través de la API de REST de Hola o biblioteca de cliente de Hola. Utilizar Hola Set Service Properties operación tooenable análisis de almacenamiento por separado para cada servicio.

Hello datos agregados se almacenan en un blob conocido (para el registro) y en tablas conocidas (para las métricas), que pueden tener acceso mediante el servicio de Blob de Hola y API del servicio tabla.

Análisis de almacenamiento tiene un límite de 20 TB en la cantidad de Hola de datos almacenados, que son independientes del límite total de hello para la cuenta de almacenamiento. Todos los registros se almacenan en [blobs en bloques](https://docs.microsoft.com/azure/storage/storage-analytics) en un contenedor denominado $logs, que se crea automáticamente cuando se habilita Storage Analytics para una cuenta de almacenamiento.

> [!Note]
> Para más información sobre las directivas de facturación y retención de datos, consulte [Storage Analytics and Billing](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing) (Storage Analytics y facturación).
>
> [!Note]
> Para más información sobre los límites de las cuentas de almacenamiento, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage](https://docs.microsoft.com/azure/storage/storage-scalability-targets).

Hola siguientes tipos de solicitudes autenticadas y anónimas se registra.



| Autenticadas  | Anónimas|
| :------------- | :-------------|
| Solicitudes correctas | Solicitudes correctas |
|Solicitudes erróneas, incluidos errores de tiempo de espera, de limitación, de red, de autorización y de otro tipo | Solicitudes que usan una firma de acceso compartido (SAS), incluidas las correctas y las erróneas |
| Solicitudes que usan una firma de acceso compartido (SAS), incluidas las correctas y las erróneas |Errores de tiempo de espera para el cliente y el servidor |
|   Solicita tooanalytics datos |    Solicitudes GET erróneas con el código de error 304 (No modificado) |
| Las solicitudes realizadas por el propio análisis de almacenamiento, como la creación o eliminación del registro, no se registran. Una lista completa de los datos registrado de saludo se documenta en hello [operaciones de registro de análisis de almacenamiento y mensajes de estado](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) y [formato de registro de análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) temas. | El resto de solicitudes anónimas erróneas no se registran. Una lista completa de los datos registrado de saludo se documenta en hello [operaciones de registro de análisis de almacenamiento y mensajes de estado](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) y [formato de registro de análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Registros de redes de Azure
El registro y supervisión de redes en Azure es completa y cubre dos amplias categorías:

-   [Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -supervisión de red basada en escenario se proporciona con características de hello en Monitor de red. Este servicio incluye captura de paquetes, próximo salto, comprobación de flujo de IP, vista de grupos de seguridad y registros de flujo de NSG. Supervisión del nivel de escenario, proporciona una vista de tooend de final de los recursos de red en la supervisión de recursos de red de tooindividual de contraste.

-   [Supervisión de recursos](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) - la supervisión en el nivel de recurso consta de cuatro funciones: registros de diagnóstico, métricas, solución de problemas y mantenimiento de recursos. Todas estas características se crean al nivel de recursos de red de Hola.

![Registros de redes de Azure](./media/azure-log-audit/azure-log-audit-fig4.png)

Monitor de red es un servicio regional que permite toomonitor y diagnosticar condiciones en un nivel de escenario de red, hacia y desde Azure. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure.

**Registro de flujo de NSG** -registros de flujo para los grupos de seguridad de red permiten toocapture registros tootraffic relacionados que se permitirán o denegarán según las reglas de seguridad de hello en el grupo de Hola. Estos registros de flujo se escriben en formato JSON y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.

### <a name="network-security-group-flow-logging"></a>Registro de flujos de grupos de seguridad de red

[Registros de flujo de grupo de seguridad de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red. Estos registros de flujo se escriben en formato JSON y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.

Mientras el flujo de registros de grupos de seguridad de red de destino, no se muestran mismo Hola como Hola otros registros. Los registros de flujos solo se almacenan en una cuenta de almacenamiento.

Hola mismo tooflow registros aplican las directivas de retención, tal como se muestra en otros registros. Los registros tienen una directiva de retención que se pueden establecer en 1 día too365 días. Si no se establece una directiva de retención, Hola registros se mantienen indefinidamente.

**Registros de diagnóstico**

Eventos periódicos y espontáneos son creados por los recursos de red y se registra en las cuentas de almacenamiento, enviadas tooan concentrador de eventos o análisis de registros. Estos registros proporcionan información sobre el estado de saludo de un recurso. Estos registros se pueden ver en herramientas como Power BI y Log Analytics. toolearn cómo tooview registros de diagnóstico, visite [análisis de registros.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Registros de diagnóstico](./media/azure-log-audit/azure-log-audit-fig5.png)

Los registros de diagnóstico están disponibles para el [equilibrador de carga](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), los [grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), las rutas y [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Network Watcher proporciona una vista de los registros de diagnóstico. Esta vista contiene todos los recursos de las redes que admiten el registro de diagnóstico. Desde esta vista, puede habilitar y deshabilitar los recursos de red de forma cómoda y rápida.


En cuanto a características de registro de toopreceding de adición, Monitor de red tiene actualmente Hola siguientes capacidades:
- [Topología](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -proporciona un Hola mostrando de vista de nivel de red diversas interconexiones y asociaciones entre los recursos de red en un grupo de recursos.

- [Captura de paquetes variable](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview): captura datos de paquetes dentro y fuera de una máquina virtual. Avanzadas opciones de filtrado y ajustarse controles, como los que se va a tooset capaz de las limitaciones de tamaño y tiempo proporcionan datos del paquete versatility.hello pueden almacenarse en un almacén de blobs o en el disco local de hello en formato CAP..

-   [Comprobaciones de flujo de IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview): comprueba si un paquete está permitido o no en función de los parámetros de paquete de información de 5-tupla sobre el flujo (IP de destino, IP de origen, puerto de destino, puerto de origen y protocolo). Si se deniega el paquete de saludo por un grupo de seguridad, hello regla y el grupo que deniega el paquete de saludo se devuelve.

-   [Próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -determina Hola siguiente salto para los paquetes que se enrutan en hello tejido de red de Azure, permitiéndole rutas toodiagnose cualquier mala configuración definida por el usuario.

-   [Vista de grupo de seguridad](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -obtiene Hola seguridad eficaz y aplica reglas que se aplican en una máquina virtual.

-   [La puerta de enlace de red virtual y la solución de problemas de conexión](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -proporciona Hola capacidad tootroubleshoot puertas de enlace de red Virtual y las conexiones.

-   [Los límites de suscripción de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -habilita el uso de recursos de red de tooview con límites.

### <a name="application-insight"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) es un servicio de Application Performance Management (APM) extensible para desarrolladores web en varias plataformas. Usar toomonitor la aplicación web en directo. Se detectan automáticamente las anomalías de rendimiento. Incluye análisis eficaces herramientas toohelp que diagnosticar problemas y toounderstand lleva a cabo lo que los usuarios con la aplicación.

 Se ha diseñado toohelp continuamente mejorar el rendimiento y facilidad de uso.

 Funciona para las aplicaciones en una amplia variedad de plataformas como. NET, Node.js y J2EE, hospedado en local o en la nube de Hola. Se integra con el proceso de devOps y tiene las herramientas de desarrollo de toovarious de puntos de conexión.

![Application Insights](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights está dirigido al equipo de desarrollo de hello, toohelp comprender el rendimiento de la aplicación y cómo se usa. Supervisa:

-   **Tasas de solicitud, tiempos de respuesta y tasas de error** - Averigüe qué páginas que son las más conocidas, en qué momento del día y dónde están los usuarios. Vea qué páginas presentan mejor rendimiento. Si los tiempos de respuesta y las tasas de error aumentan cuando hay más solicitudes, quizás tiene un problema de recursos.

-   **Tasas de dependencia, tiempos de respuesta y tasa de error** - Averigüe si los servicios externos le ralentizan.

-   **Excepciones** : analizar Hola agregado las estadísticas, o seleccionar instancias concretas y profundizar en seguimiento de la pila de Hola y las solicitudes relacionadas. Se notifican tanto las excepciones de servidor como las de explorador.

-   **Vistas de página y rendimiento de carga** - Notificados por los exploradores de los usuarios.

-   **Llamadas AJAX** desde páginas web - Tasas, tiempos de respuesta y tasas de error.

-   **Número de usuarios y sesiones**.

-   **Contadores de rendimiento** de las máquinas de servidor de Windows o Linux, como CPU, memoria y uso de la red.

-   **Diagnóstico de host** de Docker o Azure.

-   **Registros de seguimiento de diagnóstico** de la aplicación - De esta forma puede correlacionar eventos de seguimiento con las solicitudes.

-   **Eventos personalizados y las métricas** que ha escrito en código de cliente o servidor de hello, tootrack eventos empresariales como elementos venden o juegos ganadas.

**Lista de escenarios de integración y descripción:**

| Escenarios de integración | Descripción |
| --------------------- | :---------- |
|[Mapa de aplicación](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|componentes de saludo de la aplicación, con alertas y las métricas clave.||
|[Búsqueda de diagnóstico para datos de instancia](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| Busque y filtre eventos como solicitudes, excepciones, llamadas de dependencia, seguimientos de registro y vistas de páginas.||
|[Explorador de métricas para datos agregados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|Explore, filtre y segmente datos agregados, como los índices de solicitudes, errores y excepciones; los tiempos de respuesta y los tiempos de carga de página.||
|[Paneles](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Combine datos de varios recursos y compártalos con otros. Ideal para aplicaciones de varios componentes y para su presentación continua en la sala de reuniones de Hola.||
|[Secuencia de métricas en directo](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Cuando se implementa una nueva compilación, vea estos toomake de indicadores de rendimiento en tiempo casi real seguro de que todo funciona según lo previsto.||
|[Analytics](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Responda preguntas complejas acerca del uso y el rendimiento de su aplicación mediante este eficaz lenguaje de consulta.||
|[Alertas automáticas y manuales](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Alertas automáticas adaptan patrones normal de la aplicación tooyour de telemetría y se desencadena cuando hay algún fuera patrón habitual de Hola. También puede establecer alertas sobre niveles de métricas estándares o personalizadas.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Ver datos de rendimiento en el código de hello. Vaya toocode de seguimientos de pila.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Integre métricas de uso con otra inteligencia empresarial.||
|[API DE REST](https://dev.applicationinsights.io/)|Escribir código toorun consultas sobre las métricas y los datos sin procesar.||
|[Exportación continua](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Exportación masiva de datos sin procesar toostorage cuando llega.||

### <a name="azure-security-center-alerts"></a>Alertas de Azure Security Center
[Centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) recopila automáticamente, analiza y se integra datos de registro de recursos de Azure, redes de Hola y soluciones de socios conectados, así como soluciones de protección firewall y de punto de conexión, toodetect reales amenazas y reducir falsos positivos. Se muestra una lista de alertas de seguridad con prioridades en el centro de seguridad junto con hello información que necesita tooquickly investigar el problema de Hola y recomendaciones sobre cómo tooremediate un ataque.

Detección de amenazas de centro de seguridad funciona mediante la recopilación automáticamente información de seguridad de los recursos de Azure, red de Hola y soluciones de socios conectados. Analiza esta información, a menudo correlacionar información procedente de varios orígenes, tooidentify amenazas. En el centro de seguridad se priorizan las alertas de seguridad junto con recomendaciones sobre cómo tooremediate Hola amenaza.

![Azure Security Center](./media/azure-log-audit/azure-log-audit-fig7.png)

Security Center utiliza análisis avanzados que superan con creces los enfoques basados en firmas. Avances en datos de gran tamaño y [aprendizaje automático](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologías son eventos tooevaluate aplicados a través de tejido de nube todo hello: detectar amenazas que serían imposible tooidentify usar métodos manuales y predecir Hola evolución de los ataques. Estas técnicas de análisis son:

-   **Integra inteligencia sobre amenazas:** parece para conocidos actores no válidos mediante la aplicación de inteligencia sobre amenazas global de productos y servicios, Microsoft Hola Microsoft Digital crímenes unidad (DCU), Hola Microsoft Security Response Center (MSRC) y external fuentes de distribución.

-   **Análisis de comportamiento:** se aplica un comportamiento malintencionado toodiscover patrones conocidos.

-   **Detección de anomalías:** utiliza estadística de generación de perfiles toobuild una línea de base histórica. Le avisa sobre desviaciones respecto a las líneas de base establecidas que se ajustan tooa vector de ataque potencial.


Muchas operaciones de seguridad y los equipos de respuesta a incidentes se basan en una solución de administración de eventos (SIEM) e información de seguridad como punto de partida para clasificación e investigación de alertas de seguridad de Hola. Gracias a la integración de registro de Azure, los clientes pueden sincronizar alertas de Azure Security Center, además de los eventos de seguridad de máquina virtual recopilados por Diagnósticos de Azure y los registros de auditoría de Azure, con sus análisis de registros o una solución SIEM casi en tiempo real.


## <a name="log-analytics"></a>Log Analytics

Log Analytics es un servicio de [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) que le ayuda a recopilar y analizar los datos generados por los recursos en los entornos locales o en la nube. Proporciona información en tiempo real mediante búsqueda integrada y paneles personalizados tooreadily analizar millones de registros en todos los servidores, independientemente de su ubicación física y las cargas de trabajo.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

En hello centro de análisis de registros es repositorio de OMS hello, que se hospeda en hello nube de Azure. Recopilar datos en el repositorio de Hola de orígenes conectados por configurar orígenes de datos y agregar suscripción de tooyour de soluciones. Soluciones y los orígenes de datos creará diferentes tipos de registros que tienen su propio conjunto de propiedades, pero pueden seguir analizando juntos en el repositorio de consultas toohello. Esto le permite hello toouse mismo toowork de herramientas y los métodos con distintos tipos de datos recopilado por diferentes orígenes.

Orígenes conectados son equipos de Hola y otros recursos que generan datos recopilados por el análisis de registro. Esto puede incluir agentes instalados en equipos [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) y [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) que se conectan directamente o agentes en un [grupo de administración de System Center Operations Manager conectado](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents). Log Analytics también puede recopilar datos desde [Azure Storage](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage).

[Orígenes de datos](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) sean Hola diferentes tipos de datos recopilados de cada origen conectado. Esto incluye los eventos y [los datos de rendimiento](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) de [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) y agentes de Linux en suma toosources como [registros de IIS](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), y [registros de texto personalizado.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Configure cada origen de datos que se desea toocollect, y configuración de hello es origen conectado tooeach automáticamente entregado.

Hay cuatro maneras diferentes de [recopilar registros y métricas para servicios de Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage):
1.  Diagnósticos de Azure directa tooLog Analytics (diagnósticos en hello en la tabla siguiente)

2.  Diagnósticos de Azure tooAzure almacenamiento tooLog Analytics (almacenamiento en hello en la tabla siguiente)

3.  Conectores para los servicios de Azure (conectores en hello en la tabla siguiente)

4.  Las secuencias de comandos toocollect y, a continuación, los datos de entrada en el análisis de registros (espacios en blanco en hello en la tabla siguiente y servicios que no aparecen)

| Servicio | Tipo de recurso | Registros | Métricas | Solución |
| :------ | :------------ | :--- | :------ | :------- |
|Puertas de enlace de aplicaciones|  Microsoft.Network/<br>applicationGateways|  Diagnóstico|Diagnóstico|    [Azure Application](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)[Gateway Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application Insights||     Conector|  Conector|  [Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)[Connector (versión preliminar)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Cuentas de automatización|   Microsoft.Automation/<br>AutomationAccounts|    Diagnóstico||       [Más información](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Cuentas de Batch|    Microsoft.Batch/<br>batchAccounts|  Diagnóstico|    Diagnóstico||
|Servicios en la nube clásica||       Almacenamiento||       [Más información](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Cognitive Services|    Microsoft.CognitiveServices/<br>accounts|       Diagnóstico|||
|Data Lake Analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   Diagnóstico|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>accounts|   Diagnóstico|||
|Espacio de nombres del Centro de eventos|   Microsoft.EventHub/<br>namespaces|  Diagnóstico|    Diagnóstico||
|IoT Hubs|  Microsoft.Devices/<br>IotHubs||     Diagnóstico||
|Key Vault| Microsoft.KeyVault/<br>vaults|  Diagnóstico  || [KeyVault Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Equilibradores de carga|    Microsoft.Network/<br>loadBalancers|    Diagnóstico|||
|Logic Apps|    Microsoft.Logic/<br>workflows|  Diagnóstico|    Diagnóstico||
||Microsoft.Logic/<br>integrationAccounts||||
|Grupos de seguridad de red|   Microsoft.Network/<br>networksecuritygroups|Diagnóstico||   [Azure Network Security Group Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Almacenes de recuperación|   Microsoft.RecoveryServices/<br>vaults|||[Azure Recovery Services Analytics (versión preliminar)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Servicios de búsqueda|   Microsoft.Search/<br>searchServices|    Diagnóstico|    Diagnóstico||
|Espacio de nombres de Bus de servicio| Microsoft.ServiceBus/<br>namespaces|    Diagnóstico|Diagnóstico|    [Service Bus Analytics (versión preliminar)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Almacenamiento||    [Service Fabric Analytics (versión preliminar)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>servers/<br>bases de datos||       Diagnóstico||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|Storage|||         Script| [Azure Storage Analytics (versión preliminar)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Máquinas virtuales|  Microsoft.Compute/<br>virtualMachines|  Extensión|  Extensión||
||||Diagnóstico||
|Conjuntos de escalado de máquinas virtuales|   Microsoft.Compute/<br>virtualMachines    ||Diagnóstico||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|Granjas de servidores web|Microsoft.Web/<br>serverfarms||   Diagnóstico
|Sitios web| Microsoft.Web/<br>sites ||      Diagnóstico|    [Más información](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slots|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Integración de registros con sistemas locales de SIEM
[Integración de Azure log](https://www.microsoft.com/download/details.aspx?id=53324) permite toointegrate sin procesar registros de los recursos de Azure en tooyour local **sistemas de información de seguridad y administración de eventos (SIEM)**.

![Integración de registros](./media/azure-log-audit/azure-log-audit-fig9.png)

La integración de registros de Azure recopila Diagnósticos de Azure de las máquinas virtuales de Windows (WAD), los registros de actividad de Azure, las alertas de Azure Security Center y los registros del proveedor de recursos de Azure. Esta integración proporciona un panel unificado para todos sus activos, local o en la nube de hello, para que pueda agregar, correlacionar, analizar y alertas para eventos de seguridad.



La integración de registros de Azure admite actualmente la integración de registros de actividad de Azure, registros de eventos de Windows de las máquinas virtuales Windows en su suscripción de Azure, alertas de Azure Security Center, registros de Diagnóstico de Azure y registros de auditoría de Azure Active Directory.

| Tipo de registro | Análisis de registros que admiten JSON (Splunk, ArcSight, Qradar) |
| :------- | :-------------------------------------------------------- |
|Registros de auditoría de AAD|    yes|
|Registros de actividad| Sí|
|Alertas de ASC |Sí|
|Registros de diagnóstico (registros de recursos)|  Sí|
|Registros de VM|   Sí, mediante eventos reenviados y no mediante JSON|


Hello siguiente tabla explica categoría de registro de hello y los detalles de la integración de SIEM.

[Introducción a la integración de registros de Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started): este tutorial lo guía a través de la instalación de la integración de registros de Azure y de almacenamiento de Azure WAD, de registros de actividad de Azure, de alertas de Azure Security Center, y de registros de auditoría de Azure Active Directory.

Escenarios de integración

-   [Pasos de configuración de socios comerciales](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) : esta entrada de blog muestra cómo tooconfigure Azure registro toowork integración con soluciones de socios Splunk y ArcSight de HP, IBM QRadar.

-   [Preguntas más frecuentes sobre la integración de registro de Azure (P+F)](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq). Este artículo de preguntas más frecuentes responde a preguntas sobre la integración de registro de Azure.

-   [Integración de centro de seguridad de integración de registro de alertas con Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) : este documento muestra cómo las alertas toosync centro de seguridad, junto con los eventos de seguridad de máquina virtual recopilados por diagnósticos de Azure y los registros de auditoría de Azure, con los análisis de registros o Solución SIEM.

## <a name="next-steps"></a>Pasos siguientes

- [Auditoría y registro](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Proteger los datos al mantenimiento de la visibilidad y responder rápidamente tootimely alertas de seguridad

- [Security Logging and Audit Log Collection within Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/) (Recopilación de registros de seguridad y de registros de auditoría dentro de Azure)

¿Qué configuración debe tooenforce toomake seguro de que las instancias de Azure están recopilando Hola seguridad correctas y los registros de auditoría.

- [Definir la configuración de auditoría de una colección de sitios](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Como un administrador de colección de sitios, uno puede recuperar el historial de Hola de las acciones realizadas por un usuario determinado y también puede recuperar el historial de Hola de acciones llevadas a cabo durante un intervalo de fechas determinado. 

- [Registro de auditoría de Hola de búsqueda en Office 365 seguridad Hola & Centro de cumplimiento](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Se pueden usar hello centro de cumplimiento y seguridad de Office 365 toosearch Hola auditoría unificado tooview usuario de registros y la actividad del Administrador de la organización de Office 365.


