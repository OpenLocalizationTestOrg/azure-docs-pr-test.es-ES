---
title: "Introducción a la seguridad operativa aaaAzure | Documentos de Microsoft"
description: "Este artículo proporciona información general de hello Azure seguridad operativa."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Información general sobre la seguridad operativa de Azure
Seguridad operativa de Azure hace referencia toohello servicios, los controles y características disponibles toousers para proteger sus datos, aplicaciones y otros activos de Microsoft Azure. [Seguridad operativa Azure](https://docs.microsoft.com/azure/security/azure-operational-security) es un marco que incorpora el conocimiento de hello adquirido a través de una variedad de funcionalidades que son único tooMicrosoft, incluidos Hola del ciclo de vida de desarrollo de seguridad de Microsoft (SDL), Hola Microsoft Security Programa de centro de respuestas y conocimiento profundo del panorama de amenazas de seguridad de ciberseguridad de Hola.

En este artículo de información general de seguridad operativa de Azure se centra en hello siguientes áreas:

- Azure Operations Management Suite
-   Azure Security Center
-   Azure Monitor
-   Azure Network Watcher
-   Azure Storage Analytics
-   Azure Active Directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
Las operaciones de TI es responsable de administrar la infraestructura de centro de datos, aplicaciones y datos, incluida la estabilidad de Hola y seguridad de estos sistemas. Sin embargo, al obtener información de seguridad a través de aumentar los complejos entornos de TI a menudo requiere toocobble reúnen datos de varios sistemas de administración y la seguridad de las organizaciones.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.

OMS es una solución de administración de TI basada en la nube con muchas ofertas, como IT Automation, Security & Compliance, Log Analytics y Backup & Recovery. Por lo tanto, es un toomanage ayuda perfecta y proteger su infraestructura de TI, de forma local y en la nube de Hola.

un conjunto de servicios que se ejecutan en Azure proporciona funcionalidad básica de Hola de OMS. Cada servicio proporciona una función de administración específico y puede combinar escenarios de administración diferente de tooachieve de servicios. Incluye:

-   Log Analytics
-   Automation
-   Backup
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) proporciona servicios de supervisión para OMS recopilando datos de los recursos administrados en un repositorio central. Estos datos podrían incluir eventos, datos de rendimiento o datos personalizados proporcionadas a través de la API de Hola. Una vez recopilados, datos de hello están disponibles para las alertas, el análisis y la exportación. Este método le permite tooconsolidate datos desde una variedad de orígenes, por lo que puede combinar datos de los servicios de Azure con su entorno local existente. Separa claramente también colección Hola de datos de Hola de acción de hello realizada en los datos para que todas las acciones están disponibles tooall tipos de datos.

### <a name="automation"></a>Automation
Microsoft [automatización de Azure](https://docs.microsoft.com/azure/automation/automation-intro) proporciona una manera para los usuarios tooautomate hello, larga ejecución, propensas a errores, tareas manuales y repiten con frecuencia que se realizan normalmente en un entorno de nube y empresarial. Ahorra tiempo y aumenta la confiabilidad de Hola de tareas administrativas normales e incluso programa toobe automáticamente realiza a intervalos regulares. Puede automatizar procesos mediante runbooks o automatizar la administración de configuración mediante la configuración de estado deseado.

### <a name="backup"></a>Backup
[Copia de seguridad de Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) es Hola servicio basado en Azure puede consumir tooback (o proteger) y restaurar los datos en la nube de Microsoft Hola. Reemplaza su solución de copia de seguridad local o remota existente por una solución confiable, segura y rentable basada en la nube. Copia de seguridad de Azure ofrece varios componentes que descargar e implementar en el equipo adecuado que hello, server, o en la nube de Hola. componente de Hello, o el agente, que se implementa depende de qué desea tooprotect. Todos los componentes de copia de seguridad de Azure (con independencia de si va a proteger datos de forma local o en la nube de hello) pueden ser usado tooback el almacén de servicios de recuperación de datos tooa en Azure. Vea hello [tabla de componentes de copia de seguridad de Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) proporciona continuidad del negocio mediante la coordinación de la replicación de local virtuales y máquinas físicas tooAzure o tooa de sitio secundario. Si su sitio primario no está disponible, conmutación por error toohello de ubicación secundaria para que los usuarios pueden seguir trabajando y se producirá un error cuando sistemas tooworking de devolución. detección de amenazas inteligente y eficaz.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) es la solución completa de identidad como servicio (IDaaS) de Microsoft que:

-   Habilita la IAM como un servicio en la nube.
-   Proporciona administración de acceso central, inicio de sesión único (SSO) y creación de informes.
-   Admite la administración de acceso integrado para [miles de aplicaciones](https://azure.microsoft.com/marketplace/active-directory/) en Galería de aplicaciones de hello, incluyendo Salesforce, Google Apps, Box, Concur e.

Azure AD también incluye una serie completa de [capacidades de administración de identidades](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports), incluida [Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), el [registro de dispositivos]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [la administración de contraseñas de autoservicio](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [la administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [la administración de cuentas con privilegios](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [el control de acceso basado en roles](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [la supervisión del uso de aplicaciones](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [la auditoría enriquecida](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) y la [supervisión y alertas de seguridad](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Con Azure Active Directory, todas las aplicaciones que publique la aplicación por los socios y los clientes (business o consumidor) tienen Hola mismas capacidades de administración de identidades y acceso. Esto permite toosignificantly reducir los costos operativos.

## <a name="azure-security-center"></a>Azure Security Center
[Centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started) Hola de ayuda a evitar, detectar y responder toothreats con una mayor visibilidad de y control sobre la seguridad de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

[Security Center](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) le ayuda a proteger los datos de máquinas virtuales en Azure proporcionando visibilidad en la configuración de seguridad de su máquina virtual y supervisando las amenazas. Security Center puede supervisar las máquinas virtuales con los siguientes fines:

-   Configuración de seguridad del sistema operativo (SO) con hello recomienda las reglas de configuración
-   Seguridad del sistema y actualizaciones críticas que faltan
-   Recomendaciones de protección de puntos de conexión
-   Validación de cifrado de disco
-   Ataques basados en la red

Centro de seguridad de Azure usa [Control de acceso basado en roles (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), lo que proporciona [roles integrados](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) que se puede asignar toousers, grupos y servicios de Azure.

Centro de seguridad evalúa la configuración de Hola de los problemas de seguridad de recursos tooidentify y vulnerabilidades. En el centro de seguridad, sólo verá información relacionada con recursos tooa cuando se le asigna Hola rol de propietario, Colaborador o lector de hello suscripción o grupo de recursos que pertenece el recurso.

>[!Note]
>Vea [permisos en el centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn más información acerca de los roles y las acciones permitidas en el centro de seguridad.

Centro de seguridad usa Hola Microsoft Monitoring Agent: se trata de hello mismo agente utilizado por servicio de Operations Management Suite y análisis de registros de Hola. Datos recopilados de este agente se almacenan en un análisis de registro existente [área de trabajo](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) asociada a su suscripción de Azure o áreas de trabajo nuevo, teniendo en cuenta Hola geolocation de hello máquina virtual.

## <a name="azure-monitor"></a>Azure Monitor
Los problemas de rendimiento de la aplicación en la nube pueden afectar a su negocio. Con varios componentes interconectados y versiones frecuentes, las degradaciones pueden ocurrir en cualquier momento. Y, si va a desarrollar una aplicación, los usuarios normalmente encuentran problemas que no se han detectado durante las pruebas. Debe saber acerca de estos problemas de inmediato y dispone de herramientas para diagnosticar y solucionar problemas de Hola.

[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) es una herramienta básica para la supervisión de servicios que se ejecutan en Azure. Proporciona datos de nivel de la infraestructura sobre rendimiento Hola de un servicio y Hola que rodea el entorno. Si va a administrar las aplicaciones en Azure, decida si tooscale hacia arriba o hacia abajo de recursos, a continuación, Monitor de Azure ofrece lo que usa toostart.

Además, puede usar supervisión toogain profundo información sobre los datos acerca de la aplicación. Esa información puede ayudarle a rendimiento de la aplicación de tooimprove o mantenimiento o automatizar acciones que en caso contrario requerirían intervención manual. Incluye:

-   Azure Activity Log
-   Registros de diagnóstico de Azure
-   Métricas
-   Diagnóstico de Azure

### <a name="azure-activity-log"></a>Azure Activity Log
Es un registro que proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción. Hola [registro de actividad](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) se conocía anteriormente como "Registros de auditoría" o "Registros operativos", ya que informa de plano de control de eventos para las suscripciones.

### <a name="azure-diagnostic-logs"></a>Registros de diagnóstico de Azure
[Registros de diagnóstico de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) se emiten por un recurso y proporcionar datos enriquecidos y frecuentes acerca de la operación de Hola de ese recurso. contenido de Hola de estos registros varía según el tipo de recurso.

Por ejemplo, los registros del sistema de eventos de Windows son una categoría de registro de diagnóstico para máquinas virtuales y los registros de blob, tabla y cola son categorías de los registros de diagnóstico para cuentas de almacenamiento.

Registros de diagnósticos distinguirse hello [(anteriormente conocido como registro de auditoría o registro operativo) de registro de actividad](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). registro de actividad de Hello proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción. Los registros de diagnóstico proporcionan información detallada sobre las operaciones que el mismo recurso realiza.

### <a name="metrics"></a>Métricas
Monitor de Azure permite la visibilidad de toogain de telemetría de tooconsume en el rendimiento de Hola y el estado de las cargas de trabajo en Azure. Hola el tipo más importante de los datos de telemetría de Azure es métricas hello (también denominadas contadores de rendimiento) emitidas por Azure más recursos. Monitor de Azure proporciona tooconfigure de varias maneras y consumir estos [métricas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) para supervisar y solucionar problemas.

### <a name="azure-diagnostics"></a>Diagnóstico de Azure
Es la capacidad de hello dentro de Azure que habilita la recopilación de Hola de datos de diagnóstico en una aplicación implementada. Puede usar la extensión de diagnósticos de Hola de varios orígenes diferentes. Actualmente se admiten [roles web y de trabajo del servicio en la nube de Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [máquinas virtuales de Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) que ejecutan Microsoft Windows, y [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Network Watcher
Los clientes pueden crear una red integral en Azure mediante la orquestación y composición de varios recursos de red individuales como, por ejemplo, redes virtuales, ExpressRoute, Application Gateway, equilibradores de carga y muchos más. La supervisión está disponible en cada uno de los recursos de red de Hola.

red de Hello end tooend puede tener configuraciones complejas y las interacciones entre los recursos, crear escenarios complejos que necesitan supervisión basada en escenario a través del Monitor de red.

[Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) simplificará la supervisión y diagnóstico de la red de Azure. Herramientas de diagnóstico y visualización disponibles con habilitar Monitor de red se tootake remoto captura de paquetes en una máquina Virtual de Azure, obtener información sobre el tráfico de red usando los registros de flujo y diagnosticar la puerta de enlace VPN y conexiones.

Monitor de red tiene actualmente Hola siguientes capacidades:

- [Topología](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -proporciona un Hola mostrando de vista de nivel de red diversas interconexiones y asociaciones entre los recursos de red en un grupo de recursos.
-   [Captura de paquetes variable](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview): captura datos de paquetes dentro y fuera de una máquina virtual. Opciones avanzadas de opciones de filtrado y ajustarse controles, como los que se va a tooset capaz de tiempo y las limitaciones de tamaño proporcionan versatilidad. datos de paquetes de saludo pueden almacenarse en un almacén de blobs o en el disco local de hello en formato CAP..
-   [Comprobación de flujos de IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview): comprueba si un paquete está permitido o no en función de los parámetros de paquete de 5-tuplas de información del flujo (IP de destino, IP de origen, puerto de destino, puerto de origen y protocolo). Si se deniega el paquete de saludo por un grupo de seguridad, hello regla y el grupo que deniega el paquete de saludo se devuelve.
-   [Próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -determina Hola siguiente salto para los paquetes que se enrutan en hello tejido de red de Azure, permitiéndole rutas toodiagnose cualquier mala configuración definida por el usuario.
-   [Vista de grupo de seguridad](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -obtiene Hola seguridad eficaz y aplica reglas que se aplican en una máquina virtual.
-   [Registro de flujo de NSG](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -registros de flujo para los grupos de seguridad de red permiten toocapture registros tootraffic relacionados que se permitirán o denegarán según las reglas de seguridad de hello en el grupo de Hola. flujo de Hola se define mediante una información de tupla de 5: dirección IP de origen, dirección IP de destino, puerto de origen, puerto de destino y protocolo.
-   [La puerta de enlace de red virtual y la solución de problemas de conexión](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -proporciona Hola capacidad tootroubleshoot puertas de enlace de red Virtual y las conexiones.
-   [Los límites de suscripción de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -habilita el uso de recursos de red de tooview con límites.
-   [Configurar el registro de diagnósticos](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) : proporciona un único panel tooenable o deshabilitar registros de diagnóstico para recursos de red en un grupo de recursos.

toolearn más cómo ver el Monitor de red de tooconfigure, [configurar el Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Developer Operations (DevOps)
Desarrollo de aplicaciones de tooDevOps anteriores, los equipos eran responsable de recopilar los requisitos de negocios para un programa de software y escribe el código. A continuación, un equipo independiente de QA prueba programa hello en un entorno de desarrollo aislado, si se cumplieron los requisitos y las versiones Hola código para las operaciones toodeploy. los equipos de implementación de Hola se dividen a su vez en grupos en silos tales como redes y base de datos. Cada vez que un programa de software se "produce a través de la pared de Hola" tooan equipo independiente agrega los cuellos de botella.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) permite a los equipos toodeliver soluciones más seguras y de mayor calidad más rápidas y baratas. Los clientes esperan una experiencia dinámica y confiable al consumir servicios y software.  Los equipos deben iterar rápidamente sobre actualizaciones de software, medir Hola el impacto de las actualizaciones de hello y responder rápidamente a nuevos problemas de tooaddress de iteraciones de desarrollo o para proporcionar más valor.  Las plataformas en la nube, como Microsoft Azure, han quitado los cuellos de botella tradicionales y ayudaron a homogeneizar la infraestructura. Software tan grande en todos los negocios como Hola diferenciador clave y el factor en los resultados empresariales. Ninguna organización, developer o trabajo de TI puede o debe evita los movimientos de DevOps Hola.

Los profesionales de DevOps maduros adoptarán varias Hola siguiendo los procedimientos recomendados. Estas prácticas [implican personas](https://www.visualstudio.com/learn/what-is-devops-culture/) tooform estrategias basan en los escenarios de negocio de Hola.  Herramientas pueden ayudar a automatizar Hola varios procedimientos:

-   [Administración ágil de planeación y el proyecto](https://www.visualstudio.com/learn/what-is-agile/) técnicas son tooplan usado y aislar el trabajo en sprints, administrar la capacidad del equipo y ayudan a los equipos de adaptarse rápidamente toochanging las necesidades del negocio.
-   [Control de versiones, normalmente con Git](https://www.visualstudio.com/learn/what-is-git/), permite que los equipos que se encuentran en cualquier lugar en el origen de hello world tooshare e integrar con canalización de versiones de Hola de tooautomate herramientas de desarrollo de software.
-   [Integración continua](https://www.visualstudio.com/learn/what-is-continuous-integration/) unidades Hola combinación en curso y las pruebas de código, lo que conduce al principio toofinding defectos.  Entre otras ventajas se incluye menos tiempo perdido en la lucha de problemas de fusión y comentarios rápidos para los equipos de desarrollo.
-   [La entrega continua](https://www.visualstudio.com/learn/what-is-continuous-delivery/) de soluciones de software tooproduction y entornos de pruebas ayudan a las organizaciones rápidamente corregir los errores y responder de negocio que cambian tooever requisitos.
-   La [supervisión](https://www.visualstudio.com/learn/what-is-monitoring/) de aplicaciones en ejecución, incluidos los entornos de producción para el estado de la aplicación, así como el uso del cliente, ayudan a las organizaciones a plantear una hipótesis y validar o refutar estrategias rápidamente.  Los datos enriquecidos se capturan y almacenan en distintos formatos de registro.
-   [Infraestructura como código (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) es una práctica, que permite la automatización de Hola y validación de la creación y destrucción de toohelp de redes y máquinas virtuales con la entrega de aplicaciones seguras, estables plataformas de hospedaje.
-   [Microservicios](https://www.visualstudio.com/learn/what-are-microservices/) arquitectura es tooisolate aprovechado casos de uso de negocio en servicios reutilizables pequeños.  Esta arquitectura permite la escalabilidad y la eficacia.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información sobre la seguridad de OMS y la solución de auditoría, vea Hola siguientes artículos:

- [Operations Management Suite | Security &amp; Compliance](https://www.microsoft.com/cloud-platform/security-and-compliance)
- [Supervisión y responde tooSecurity las alertas en Operations Management Suite solución de seguridad y auditoría](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Supervisión de los recursos en la solución Security and Audit de Operations Management Suite](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources)
