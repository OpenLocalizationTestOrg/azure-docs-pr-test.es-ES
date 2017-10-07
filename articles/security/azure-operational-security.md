---
title: aaaAzure seguridad operativa | Documentos de Microsoft
description: "Aprenda sobre Microsoft Operations Management Suite (OMS), sus servicios y cómo funciona."
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
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Seguridad operativa de Azure
## <a name="introduction"></a>Introducción

### <a name="overview"></a>Información general
Somos conscientes de que la seguridad es trabajo en la nube de Hola y la importancia que tiene que buscar información precisa y oportuna sobre la seguridad de Azure. Uno de hello mejor motivos toouse Azure para las aplicaciones y servicios es tootake aprovechar la amplia gama de Hola de herramientas de seguridad y las funciones disponibles. Estas herramientas y capacidades que esté soluciones seguras toocreate posibles en la plataforma Windows Azure segura de Hola. Microsoft Azure debe proporcionar confidencialidad, integridad y disponibilidad de los datos del cliente, al mismo tiempo que hace posible una responsabilidad transparente.

toohelp clientes comprenden mejor la matriz de Hola de controles de seguridad que se implementa en Microsoft Azure desde ambos clientes de Hola y se escribe perspectivas operativas de Microsoft, este documento, "Seguridad operativa de Azure", que proporciona un información completa sobre seguridad operativa de hello disponible con Windows Azure.

### <a name="azure-platform"></a>Plataforma Azure
Azure es una plataforma de servicios en la nube pública que admite una amplia selección de sistemas operativos, lenguajes de programación, plataformas, herramientas, bases de datos y dispositivos. Puede ejecutar contenedores de Linux con integración de Docker, compilar aplicaciones con JavaScript, Python, .NET, PHP, Java, Node.js y crear back-ends para dispositivos iOS, Android y Windows. Servicio de nube de Azure admite Hola mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza.

Al compilar en, o migrar los activos de TI a, un proveedor de servicios de nube pública depende de tooprotect de capacidades de la organización sus aplicaciones y datos con controles de Hola y de servicios de hello proporcionan seguridad de hello toomanage de basados en la nube activos.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus requisitos de seguridad. Además, Azure le proporciona una amplia gama de toocontrol de capacidad de hello y opciones de seguridad configurables usarlas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones de su organización. Este documento explica cómo las funcionalidades de seguridad de Azure pueden ayudarle a cumplir estos requisitos.

### <a name="abstract"></a>Descripción breve
Seguridad operativa de Azure hace referencia toohello servicios, los controles y características disponibles toousers para proteger sus datos, aplicaciones y otros activos de Microsoft Azure. Seguridad operativa de Azure se basa en un marco que incorpora el conocimiento de hello adquirido a través de varias funciones que son único tooMicrosoft, incluidos Hola del ciclo de vida de desarrollo de seguridad de Microsoft (SDL), Hola Microsoft Security Response Center programa y conocimiento profundo del panorama de amenazas de ciberseguridad de Hola.

Estas notas del producto se describen tooAzure de enfoque de Microsoft seguridad operativa dentro de plataforma de nube de Microsoft Azure hello y abarca siguientes servicios:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) es la solución de administración de TI para la nube híbrida de Hola Hola. Por sí solas o tooextend le ofrece la implementación existente de System Center, OMS Hola obtener la máxima flexibilidad y control para la administración basada en la nube de su infraestructura.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Con OMS, puede administrar cualquier instancia en cualquier nube, incluidas las locales o de Azure, AWS, Windows Server, Linux, VMware y OpenStack, con un costo menor que las soluciones de la competencia. Creado para Hola a todos en la nube en primer lugar, OMS ofrece un nuevo toomanaging enfoque su empresa que la forma hello más rápido y más rentable toomeet nuevos negocios desafíos y adaptarse a nuevas cargas de trabajo, aplicaciones y entornos de nube.

### <a name="oms-services"></a>Servicios de OMS

un conjunto de servicios que se ejecutan en Azure proporciona funcionalidad básica de Hola de OMS. Cada servicio proporciona una función de administración específico y puede combinar escenarios de administración diferente de tooachieve de servicios.

| Servicio  | Descripción|
| :------------- | :-------------|
| Log Analytics | Supervisar y analizar la disponibilidad de Hola y el rendimiento de los distintos recursos incluidos físicos y máquinas virtuales. |
|Automation | Automatización de procesos manuales y aplicación de configuraciones a máquinas físicas y virtuales. |
| Copia de seguridad | Realización de copias de seguridad y restauración de datos críticos. |
| Site Recovery | Provisión de una alta disponibilidad para las aplicaciones críticas. |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) proporciona servicios de supervisión para OMS recopilando datos de los recursos administrados en un repositorio central. Estos datos podrían incluir eventos, datos de rendimiento o datos personalizados proporcionadas a través de la API de Hola. Una vez recopilados, datos de hello están disponibles para las alertas, el análisis y la exportación.


Este método permite tooconsolidate datos procedentes de diversos orígenes, por lo que puede combinar datos de los servicios de Azure con el contenido existente en entorno local. Separa claramente también colección Hola de datos de Hola de acción de hello realizada en los datos para que todas las acciones están disponibles tooall tipos de datos.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

Hola servicio de análisis de registros administra los datos en la nube segura mediante el uso de hello siguientes métodos:
-   Segregación de datos
-   Retención de datos
-   Seguridad física
-   Administración de incidentes
-   Cumplimiento normativo
-   Certificaciones de estándares de seguridad

### <a name="azure-backup"></a>Azure Backup

[Copia de seguridad de Azure](http://azure.microsoft.com/documentation/services/backup) proporciona datos de copia de seguridad y restauración los servicios y forman parte del conjunto OMS Hola de productos y servicios.
Protege los datos de las aplicaciones y los conserva durante años sin necesidad de realizar ninguna inversión y afrontando unos costes operativos mínimos. Pueden realizar una copia datos de servidores Windows físicos y virtuales además tooapplication las cargas de trabajo como SQL Server y SharePoint. También se puede utilizar por [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate protegido tooAzure de datos para ofrecer redundancia y almacenamiento a largo plazo.


Los datos protegidos en Azure Backup se almacenan en un almacén de copia de seguridad ubicado en una región geográfica determinada. Hola datos se replican dentro Hola la misma región y, según tipo hello de almacén, también se puede tooanother replicada región para la resistencia adicional.

### <a name="management-solutions"></a>Soluciones de administración
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.


Las [soluciones de administración](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) son conjuntos de lógica preempaquetados que implementan un escenario de administración concreto usando uno o más servicios de OMS. Diferentes soluciones están disponibles de Microsoft y de asociados de negocios que puede agregar fácilmente tooyour suscripción de Azure tooincrease Hola valo su inversión de OMS. Como partner, puede crear su propias soluciones toosupport sus aplicaciones y servicios y proporcionarlos toousers a través de hello Azure Marketplace o plantillas de inicio rápido.


![Soluciones de administración](./media/azure-operational-security/azure-operational-security-fig4.png)

Un buen ejemplo de una solución que usa varios servicios tooprovide una funcionalidad adicional es hello [solución de administración de actualizaciones](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Esta solución usa hello [análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) agente para Windows y Linux toocollect obtener información acerca de las actualizaciones necesarias en cada agente. Escribe este repositorio de análisis de registros de toohello de datos donde se pueden analizar con un panel incluido.

Cuando se crea una implementación, runbooks en [automatización de Azure](https://docs.microsoft.com/azure/automation/automation-intro) tooinstall usado requerido actualizaciones. Administrar todo este proceso en el portal de hello y no es necesario tooworry acerca de los detalles subyacentes de Hola.

## <a name="azure-security-center"></a>Azure Security Center

Azure Security Center ayuda a proteger los recursos de Azure. Proporciona una supervisión de la seguridad y una administración de directivas integradas en suscripciones de Azure. En el servicio de hello, es posible toodefine directivas no solo en las suscripciones de Azure, sino también en [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), por lo que puede ser más específico.

### <a name="security-policies-and-recommendations"></a>Directivas de seguridad y recomendaciones

Una directiva de seguridad define el conjunto de Hola de controles, que se recomiendan para los recursos dentro de hello especificado suscripción o grupo de recursos.

En el centro de seguridad, define directivas según tooyour requisitos de seguridad y empresa tipo hello de aplicaciones o importancia de los datos de Hola.

![Directivas de seguridad y recomendaciones](./media/azure-operational-security/azure-operational-security-fig5.png)


Las directivas que se habilitarán automáticamente en el nivel de suscripción de hello propagan tooall los grupos de recursos dentro de la suscripción de hello tal y como se muestra en el diagrama, hello en el lado derecho de hello:


### <a name="data-collection"></a>Colección de datos

Centro de seguridad recopila los datos desde su tooassess de máquinas virtuales (VM), su estado de seguridad, proporcionar recomendaciones de seguridad y alerta toothreats. La primera vez que se accede a Security Center, la recopilación de datos está habilitada en todas las máquinas virtuales de la suscripción. Se recomienda utilizar el conjunto de datos, pero puede dejar de participar si se desactiva la recopilación de datos en hello directiva de centro de seguridad.

### <a name="data-sources"></a>Orígenes de datos

- Centro de seguridad de Azure analiza los datos de hello después de visibilidad de tooprovide orígenes en el estado de seguridad, identificar vulnerabilidades y recomienda las mitigaciones y detectar amenazas activas:

-   Los servicios de Azure: Utiliza la información sobre la configuración de hello de servicios de Azure implementados mediante la comunicación con el proveedor de recursos de dicho servicio.

- Tráfico de red: usa metadatos muestreados del tráfico de red de la infraestructura de Microsoft, como el IP o el puerto de origen o destino, el tamaño de paquete y el protocolo de red.

-   Soluciones de asociados: usa alertas de seguridad de las soluciones de asociados integradas, como firewalls y soluciones antimalware.

-   Sus Virtual Machines: usa información de configuración e información sobre eventos de seguridad, como los eventos y registros de auditoría de Windows, registros IIS, mensajes de Syslog y archivos de volcado de memoria de sus máquinas virtuales.

### <a name="data-protection"></a>Protección de datos

los clientes de toohelp evitarán, detectaron y responden toothreats, Azure Security Center recopila y procesa los datos relacionados con la seguridad, incluida la información de configuración, metadatos, registros de eventos, archivos de volcado y mucho más. Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio.

-   **Segregación de datos**: los datos se mantienen separados de forma lógica en cada componente en el servicio de Hola. Todos los datos se etiquetan por organización. Este etiquetado persiste a lo largo del ciclo de vida de datos de Hola y se aplica en cada nivel de servicio de Hola.

-   **Acceso a datos**: recomendaciones de seguridad de tooprovide e investigar posibles amenazas de seguridad, personal de Microsoft puede tener acceso a la información recopilada o analizar por servicios de Azure, incluidos los archivos de volcado, procesar eventos de creación de disco de máquina virtual las instantáneas y artefactos, que pueden incluir involuntariamente los datos del cliente o datos personales de las máquinas virtuales. Cumplimos toohello [declaración de privacidad y condiciones de Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), que el estado que no sea de Microsoft usa los datos del cliente o derivar la información de él para ningún propósito comercial publicitario o similar.

-   **Uso de datos**: Microsoft utiliza patrones e inteligencia sobre amenazas visto entre varios inquilinos tooenhance nuestras capacidades de detección y prevención; lo hacemos según se describe en los compromisos de privacidad de hello nuestro [privacidad Instrucción](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Ubicación de los datos

Azure Security Center recopila copias efímeras de los archivos de volcado de memoria y las analiza para buscar pruebas de intentos de vulnerabilidad y de riesgos ciertos. Centro de seguridad de Azure realiza este análisis dentro de Hola mismo geográfica como área de trabajo de Hola y eliminaciones Hola copias efímeros si se completa el análisis. Artefactos de la máquina se almacenan de forma centralizada en Hola la misma región como Hola máquina virtual.

-   **Sus cuentas de almacenamiento**: se especifica una cuenta de almacenamiento para cada región en la que se ejecutan máquinas virtuales. Esto permite toostore datos Hola misma región que la máquina virtual de Hola desde qué Hola se recopilan datos.

-   **Almacenamiento de Azure Security Center**: información sobre las alertas de seguridad, incluidas las alertas de socios comerciales, recomendaciones y estado de mantenimiento de seguridad se almacena centralmente, actualmente en Estados Unidos de Hola. Esta información puede incluir información de configuración relacionados y eventos de seguridad procedentes de las máquinas virtuales como sea necesario tooprovide con el estado de mantenimiento de seguridad, recomendación o alerta de seguridad de Hola.


## <a name="azure-monitor"></a>Azure Monitor

Hola [seguridad OMS](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) y habilita de solución de auditoría tooactively de TI supervisar todos los recursos, que pueden ayudar a minimizar el impacto de Hola de incidentes de seguridad. Auditoría y seguridad de OMS tiene dominios de seguridad que pueden utilizarse para la supervisión de recursos. dominio de seguridad de Hello proporciona acceso rápido toooptions, Hola de supervisión de seguridad dominios siguientes se tratan con más detalle:

-   Evaluación de malware
-   Evaluación de la actualización
-   Identidad y acceso

El Monitor de Azure proporciona punteros tooinformation en determinados tipos de recursos. Ofrece visualización, consulta, enrutamiento, alertas, escalado automático y automatización en datos de hello infraestructura de Azure (registro de actividad) y cada recurso de Azure individual (registros de diagnóstico).

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


Las aplicaciones de nube son complejas y tienen muchas partes móviles. La supervisión proporciona tooensure de datos que mantiene la aplicación y en ejecución en un estado correcto. También ayuda a toostave off posibles problemas o solucionar problemas más allá de los.

Además, puede usar supervisión toogain profundo información sobre los datos acerca de la aplicación. Esa información puede ayudarle a rendimiento de la aplicación de tooimprove o mantenimiento o automatizar acciones que en caso contrario requerirían intervención manual.

### <a name="azure-activity-log"></a>Azure Activity Log


Es un registro que proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción. Hola registro de actividad se conocía anteriormente como "Registros de auditoría" o "Registros operativos", ya que informa de plano de control de eventos para las suscripciones.

![Azure Activity Log](./media/azure-operational-security/azure-operational-security-fig7.png)

Gracias a Hola registro de actividad, puede determinar hello ' qué, quién y cuándo ' para las operaciones (PUT, POST, DELETE) realizadas en los recursos de hello en su suscripción de escritura. También puede entender el estado Hola de operación de Hola y otras propiedades relevantes. Hola registro de actividad no incluye read operaciones (GET) o las operaciones de recursos que usan el modelo clásico de Hola.

### <a name="azure-diagnostic-logs"></a>Registros de diagnóstico de Azure

Estos registros se emiten por un recurso y proporcionan datos enriquecidos y frecuentes acerca de la operación de Hola de ese recurso. contenido de Hola de estos registros varía según el tipo de recurso.

Por ejemplo, los registros del sistema de eventos de Windows son una categoría de registro de diagnóstico para máquinas virtuales y los registros de blob, tabla y cola son categorías de los registros de diagnóstico para cuentas de almacenamiento.

Registros de diagnósticos distinguirse hello [(anteriormente conocido como registro de auditoría o registro operativo) de registro de actividad](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). registro de actividad de Hello proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción. Los registros de diagnóstico proporcionan información detallada sobre las operaciones que el mismo recurso realiza.

### <a name="metrics"></a>Métricas

Monitor de Azure permite la visibilidad de toogain de telemetría de tooconsume en el rendimiento de Hola y el estado de las cargas de trabajo en Azure. Hola el tipo más importante de los datos de telemetría de Azure es métricas hello (también denominadas contadores de rendimiento) emitidas por Azure más recursos. Monitor de Azure proporciona tooconfigure de varias maneras y consumir estos [métricas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) para supervisar y solucionar problemas. Las métricas son una valiosa fuente de telemetría y habilitar hello toodo siguientes tareas:

-   **Un seguimiento del rendimiento de hello** del recurso (por ejemplo, una aplicación de la máquina virtual, sitio Web o lógica) al trazar sus métricas en un gráfico de portal y fijar ese tooa gráfico del panel.

-   **Recibir notificaciones de un problema** que impactos Hola rendimiento de su recurso cuando una métrica supera un umbral determinado.

-   **Configurar acciones automatizadas**, como escalar automáticamente un recurso o activar un runbook cuando una métrica cruza un umbral determinado.

-   **Realizar análisis avanzados** o elaborar informes de tendencias de rendimiento o de uso de los recursos.

-   **Archivo** Hola historial de rendimiento o mantenimiento de los recursos para el cumplimiento de normas o con fines de auditoría.

### <a name="azure-diagnostics"></a>Diagnóstico de Azure

Es la capacidad de hello dentro de Azure que habilita la recopilación de Hola de datos de diagnóstico en una aplicación implementada. Puede usar la extensión de diagnósticos de Hola de varios orígenes diferentes. Actualmente se admiten [roles web y de trabajo del servicio en la nube de Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/overview) que ejecutan Microsoft Windows, y [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Otros servicios de Azure tienen su propio diagnóstico independiente.

## <a name="azure-network-watcher"></a>Azure Network Watcher

La auditoría de la seguridad de la red es fundamental para detectar vulnerabilidades de red y asegurar el cumplimiento de la seguridad de TI y el modelo de gobierno reglamentario. Con la vista de grupo de seguridad, puede recuperar las reglas del grupo de seguridad de red y seguridad Hola configurado y Hola reglas de seguridad eficaz. Con hello obtener lista de reglas que se aplican, se pueden determinar los puertos de Hola que están abiertos y evaluación una vulnerabilidad de la red.

[Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) es un servicio regional que le permite toomonitor y diagnosticar condiciones en un nivel de red en, a y desde Azure. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure. Este servicio incluye captura de paquetes, próximo salto, comprobación de flujo de IP, vista de grupos de seguridad y registros de flujo de NSG. Supervisión del nivel de escenario, proporciona una vista de tooend de final de los recursos de red en la supervisión de recursos de red de tooindividual de contraste.

![Azure Network Watcher](./media/azure-operational-security/azure-operational-security-fig8.png)

Monitor de red tiene actualmente Hola siguientes capacidades:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Registros de auditoría</a>**-se registran las operaciones realizadas como parte de la configuración de Hola de redes. Estos registros pueden verse en el portal de Azure de Hola o recuperan mediante herramientas de Microsoft como Power BI o herramientas de terceros. Los registros de auditoría están disponibles a través del portal de hello, PowerShell, CLI y API de Rest. Para más información sobre los registros de auditoría, consulte Operaciones de auditoría con Resource Manager. Hay registros de auditoría disponibles para las operaciones realizadas en todos los recursos de red.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">Comprobaciones de flujo de IP</a>**: comprueba si un paquete está permitido o no en función de los parámetros de paquete de 5-tuplas de información del flujo (IP de destino, IP de origen, puerto de destino, puerto de origen y protocolo). Si el paquete de saludo ha sido denegado por un grupo de seguridad de red, se devuelve la regla de Hola y el grupo de seguridad de red que ha denegado el paquete de saludo.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Próximo salto</a>**  -determina Hola siguiente salto para los paquetes que se enrutan en hello tejido de red de Azure, permitiéndole rutas toodiagnose cualquier mala configuración definida por el usuario.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Vista de grupo de seguridad</a>**  -obtiene Hola seguridad eficaz y aplica reglas que se aplican en una máquina virtual.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">Registro de flujo de NSG</a>**  -registros de flujo para los grupos de seguridad de red permiten toocapture registros tootraffic relacionados que se permitirán o denegarán según las reglas de seguridad de hello en el grupo de Hola. flujo de Hola se define mediante una información de tupla de 5: dirección IP de origen, dirección IP de destino, puerto de origen, puerto de destino y protocolo.

## <a name="azure-storage-analytics"></a>Azure Storage Analytics

[Análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) puede almacenar métricas que incluyen datos de estadísticas y la capacidad de transacciones agregados acerca del servicio de almacenamiento de tooa de solicitudes. Las transacciones se notifican en ambos nivel de operación de API de Hola y en el nivel de servicio de almacenamiento de Hola y capacidad se notifica en el nivel de servicio de almacenamiento de Hola. Datos de métricas que pueden ser utilizados tooanalyze uso de servicios de almacenamiento, diagnosticar problemas con las solicitudes realizadas en el servicio de almacenamiento de Hola y el rendimiento de hello tooimprove de las aplicaciones que utilizan un servicio.

[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento. Puede utilizar este solicitudes de tootrace de datos, analizar las tendencias de uso y diagnosticar problemas con su cuenta de almacenamiento. Registro de análisis de almacenamiento está disponible para hello [servicios Blob, cola y tabla](https://docs.microsoft.com/azure/storage/storage-introduction). Análisis de almacenamiento registra información detallada acerca del servicio de almacenamiento de tooa de solicitudes correctas e incorrectas.

Esta información puede ser problemas de toodiagnose con un servicio de almacenamiento y las solicitudes individuales de toomonitor usado. Las solicitudes se registran en función de la mejor opción. Las entradas del registro se crean solo si hay las solicitudes realizadas en el extremo de servicio de Hola. Ejemplo si una cuenta de almacenamiento tiene actividad en su extremo de Blob pero no en sus puntos de conexión de la tabla o cola, solo para los registros de pertenecen toohello servicio Blob se crea.

toouse análisis de almacenamiento, debe habilitarla individualmente para cada servicio que desee toomonitor. Puede habilitarlo en hello [portal de Azure](https://portal.azure.com/); para obtener más información, consulte [supervisar una cuenta de almacenamiento en el portal de Azure hello](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). También puede habilitar el análisis de almacenamiento mediante programación a través de la API de REST de Hola o biblioteca de cliente de Hola. Utilizar Hola Set Service Properties operación tooenable análisis de almacenamiento por separado para cada servicio.

Hello datos agregados se almacenan en un blob conocido (para el registro) y en tablas conocidas (para las métricas), que pueden tener acceso mediante el servicio de Blob de Hola y API del servicio tabla.

Análisis de almacenamiento tiene un límite de 20 TB en la cantidad de Hola de datos almacenados, que son independientes del límite total de hello para la cuenta de almacenamiento. Todos los registros se almacenan en [blobs en bloques](https://docs.microsoft.com/azure/storage/storage-analytics) en un contenedor denominado $logs, que se crea automáticamente cuando se habilita Storage Analytics para una cuenta de almacenamiento.

Hola siguiendo las acciones realizadas por el análisis de almacenamiento es facturable:

-   Blobs de toocreate de solicitudes para el registro
-   Entidades de tabla de toocreate de solicitudes para las métricas.

> [!Note]
> Para más información sobre las directivas de facturación y retención de datos, consulte [Storage Analytics and Billing](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing) (Storage Analytics y facturación).
> Para obtener un rendimiento óptimo, desea número de Hola de toolimit de alta tasa de utilización discos adjuntos toohello máquina virtual tooavoid posible limitación. Si todos los discos no se se utilizan muy en hello mismo tiempo, cuenta de almacenamiento de hello puede admitir un disco número más grande.

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
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD también incluye un conjunto completo de funcionalidades de administración de identidades, entre ellas, Multi-Factor Authentication, registro de dispositivos, administración de contraseñas de autoservicio, administración de grupos de autoservicio, administración de cuentas con privilegios, control de acceso basado en rol, supervisión del uso de aplicaciones, auditoría enriquecida y supervisión y alertas de seguridad.

-   Mejore la seguridad de las aplicaciones con la autenticación multifactor y acceso condicional de Azure AD.

-   Supervise el uso de las aplicaciones y proteja su empresa contra amenazas avanzadas con informes y supervisión de seguridad.

Azure Active Directory (Azure AD) incluye informes de seguridad, actividad y auditoría para el directorio. [Informe de auditoría de Azure Active Directory Hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) ayuda a los clientes acciones tooidentify con privilegios que se ha producido en su Azure Active Directory. Las acciones con privilegios incluyen cambios de elevación (por ejemplo, creación de roles o los restablecimientos de contraseña), cambiar las configuraciones de directiva (por ejemplo las directivas de contraseña), o la configuración de toodirectory de cambios (por ejemplo, configuración de federación de cambios toodomain).

informes de Hello proporcionan registro de auditoría de Hola para nombre del evento hello, actor Hola que realiza la acción de hello, recurso de destino de hello afectado por el cambio de Hola y Hola fecha y hora (en UTC). Los clientes están lista de hello tooretrieve capaz de eventos de auditoría para su Azure Active Directory a través de hello [portal de Azure](https://portal.azure.com/), tal y como se describe en [ver los registros de auditoría](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Presentamos una lista de informes de hello incluidas:

| Informes de seguridad  | Informes de actividad| Informes de auditoría |
| :------------- | :-------------| :-------------|
|Inicios de sesión desde orígenes desconocidos | Uso de la aplicación: resumen | Informe de auditoría de directorio |
|Inicios de sesión tras varios errores | Uso de la aplicación: detallado |   |
|Inicios de sesión desde varias ubicaciones geográficas | Panel de la aplicación |  |
|Inicios de sesión desde direcciones IP con actividad sospechosa |Errores de aprovisionamiento de cuentas |  |
|Actividad de inicio de sesión irregular |Dispositivos de usuario individuales |  |
|Inicios de sesión desde dispositivos posiblemente infectados |Actividad de usuario individual |   |
|Usuarios con actividad de inicio de sesión anómala |Informe de actividad de grupos |   |
| |Informe de actividad de registro de restablecimiento de contraseña |   |
| |Actividad de restablecimiento de contraseña |   | |



datos de Hola de estos informes pueden ser aplicaciones de tooyour útil, como sistemas SIEM, auditoría y herramientas de business intelligence. reporting de Azure AD Hello [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) proporcionan acceso mediante programación toohello datos a través de un conjunto de API basadas en REST. Se puede llamar a estas API desde diversos lenguajes de programación y herramientas.

Eventos de hello informe de auditoría de AD de Azure se conservan durante 180 días.

> [!Note]
> Para obtener más información acerca de la retención de los informes, consulte [Directivas de retención de informes de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Para clientes interesados en almacenar sus [eventos de auditoría](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) durante largos periodos de retención hello API de informes pueden ser eventos de auditoría de extracción tooregularly usado en un almacén de datos independiente.

## <a name="summary"></a>Resumen

Este resúmenes de artículo proteger su privacidad y proteger los datos, al tiempo que ofrece software y los servicios que le ayudarán a administran Hola infraestructura de TI de su organización. Microsoft reconoce que, cuando confía sus datos tooothers, esa confianza requiere una seguridad rigurosa. Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio.  La seguridad y la protección de los datos son prioritarias en Microsoft.

Este artículo explica cómo

-   Cómo procesar los datos recopilados, y protegidos de hello Operations Management Suite (OMS).

-   Analizar rápidamente eventos en distintos orígenes de datos. Identificar los riesgos de seguridad y comprender el ámbito de Hola y el impacto de daños de hello toomitigate amenazas y ataques de una infracción de seguridad.

-   Identificar patrones de ataque visualizando tipos de amenazas malintencionadas y tráfico de IP malintencionado saliente. Comprender la postura de seguridad de Hola de todo el entorno independientemente de la plataforma.

-   Capturar todos los datos de eventos y registros de hello necesarios para una auditoría de seguridad o de cumplimiento. Barra diagonal Hola tiempo y recursos necesitan toosupply seguridad con un conjunto completo, exportable y permite realizar búsquedo de datos de eventos y registros de auditoría.

<ul>
<li>Recopilar eventos relacionados con la seguridad y auditoría, análisis de infracción tookeep un cierre de la vista los activos:</li>
<ul>
<li>Posición de seguridad</li>
<li>Problema importante</li>
<li>Resúmenes de amenazas</li>
</ul>
</ul>

## <a name="next-steps"></a>Pasos siguientes

- [Diseño y seguridad operativa](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft diseña sus servicios y software con la seguridad en mente toohelp Asegúrese de que su infraestructura de nube es resistente y protegido frente a ataques.

- [Operations Management Suite | Security &amp; Compliance](https://www.microsoft.com/cloud-platform/security-and-compliance)

Usar Microsoft security datos y análisis tooperform más inteligente y eficaz detección de amenazas.

- [Planificación de centro de seguridad de Azure y operaciones](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) un conjunto de pasos y tareas que puede seguir toooptimize el uso del centro de seguridad según los requisitos de seguridad y el modelo de administración de nube de su organización.

