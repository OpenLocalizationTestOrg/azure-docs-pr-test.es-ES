---
title: aaaIntroduction tooAzure Monitor de red | Documentos de Microsoft
description: "Esta página proporciona una visión general de servicio de Monitor de red para la supervisión de hello y visualizar red conectada recursos de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Información general sobre la supervisión de red de Azure

Los clientes pueden crear una red integral en Azure mediante la orquestación y composición de varios recursos de red individuales como, por ejemplo, redes virtuales, ExpressRoute, Application Gateway, equilibradores de carga y muchos más. La supervisión está disponible en cada uno de los recursos de red de Hola. Nos referimos toothis supervisión como supervisión de nivel de recurso.

red de Hello end tooend puede tener configuraciones complejas y las interacciones entre los recursos, crear escenarios complejos que necesitan supervisión basada en escenario a través del Monitor de red.

Este artículo trata la supervisión en los niveles de escenario y de recurso. La supervisión de red en Azure es completa y cubre dos amplias categorías:

* [**Monitor de red** ](#network-watcher) -basadas en escenarios de supervisión se proporciona con características de hello en Monitor de red. Este servicio incluye captura de paquetes, próximo salto, comprobación de flujo de IP, vista de grupos de seguridad y registros de flujo de NSG. Supervisión del nivel de escenario, proporciona una vista de tooend de final de los recursos de red en la supervisión de recursos de red de tooindividual de contraste.
* [**Supervisión de recursos**](#network-resource-level-monitoring): la supervisión en el nivel de recurso consta de cuatro funciones: registros de diagnóstico, métricas, solución de problemas y mantenimiento de recursos. Todas estas características se crean al nivel de recursos de red de Hola.

## <a name="network-watcher"></a>Network Watcher

Monitor de red es un servicio regional que permite toomonitor y diagnosticar condiciones en un nivel de escenario de red, hacia y desde Azure. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure.

Monitor de red tiene actualmente Hola siguientes capacidades:

* **[Topología](network-watcher-topology-overview.md)**  -proporciona un Hola mostrando de vista de nivel de red diversas interconexiones y asociaciones entre los recursos de red en un grupo de recursos.
* **[Captura de paquetes variable](network-watcher-packet-capture-overview.md)**: captura datos de paquetes dentro y fuera de una máquina virtual. Opciones avanzadas de opciones de filtrado y ajustarse controles, como los que se va a tooset capaz de tiempo y las limitaciones de tamaño proporcionan versatilidad. datos de paquetes de saludo pueden almacenarse en un almacén de blobs o en el disco local de hello en formato CAP..
* **[Comprobación de flujo de IP](network-watcher-ip-flow-verify-overview.md)**: comprueba si un paquete está permitido o no en función de los parámetros de paquete de 5-tuplas de información del flujo (IP de destino, IP de origen, puerto de destino, puerto de origen y protocolo). Si se deniega el paquete de saludo por un grupo de seguridad, hello regla y el grupo que deniega el paquete de saludo se devuelve.
* **[Próximo salto](network-watcher-next-hop-overview.md)**  -determina Hola siguiente salto para los paquetes que se enrutan en hello tejido de red de Azure, permitiéndole rutas toodiagnose cualquier mala configuración definida por el usuario.
* **[Vista de grupo de seguridad](network-watcher-security-group-view-overview.md)**  -obtiene Hola seguridad eficaz y aplica reglas que se aplican en una máquina virtual.
* **[Registro de flujo de NSG](network-watcher-nsg-flow-logging-overview.md)**  -registros de flujo para los grupos de seguridad de red permiten toocapture registros tootraffic relacionados que se permitirán o denegarán según las reglas de seguridad de hello en el grupo de Hola. flujo de Hola se define mediante una información de tupla de 5: dirección IP de origen, dirección IP de destino, puerto de origen, puerto de destino y protocolo.
* **[La puerta de enlace de red virtual y la solución de problemas de conexión](network-watcher-troubleshoot-manage-rest.md)**  -proporciona Hola capacidad tootroubleshoot puertas de enlace de red Virtual y las conexiones.
* **[Los límites de suscripción de red](#network-subscription-limits)**  -habilita el uso de recursos de red de tooview con límites.
* **[Configurar el registro de diagnósticos](#diagnostic-logs)**  : proporciona un único panel tooenable o deshabilitar registros de diagnóstico para recursos de red en un grupo de recursos.
* **[Conectividad (versión preliminar)](network-watcher-connectivity-overview.md)**  -comprueba la posibilidad de Hola de establecer una conexión TCP directa de una tooa de máquina virtual tiene el punto de conexión.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Control de acceso basado en rol (RBAC) en Network Watcher

Monitor de red utiliza hello [modelo de Control de acceso de Azure Role-Based (RBAC)](../active-directory/role-based-access-control-what-is.md). Hola los siguientes permisos es necesarios para hello Monitor de red. Es importante toomake que ese rol hello usa para iniciar las API de Monitor de red o con el Monitor de red desde el portal de hello tenga acceso de hello necesario.

|Recurso| Permiso|
|---|---| 
|Microsoft.Storage/ |Lectura|
|Microsoft.Authorization/| Lectura| 
|Microsoft.Resources/subscriptions/resourceGroups/| Lectura|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Acción|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Acción|
|Microsoft.Storage/storageAccounts/listKeys/ | Acción|
|Microsoft.Compute/virtualMachines/ |Lectura|
|Microsoft.Compute/virtualMachines/ |Escritura|
|Microsoft.Compute/virtualMachineScaleSets/ |Lectura|
|Microsoft.Compute/virtualMachineScaleSets/ |Escritura|
|Microsoft.Network/networkWatchers/packetCaptures/ |Lectura|
|Microsoft.Network/networkWatchers/packetCaptures/| Escritura|
|Microsoft.Network/networkWatchers/packetCaptures/| Eliminar|
|Microsoft.Network/networkWatchers/ |Escritura |
|Microsoft.Network/networkWatchers/| Lectura |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Límites de suscripción de red

Los límites de suscripción de red proporcionan los detalles de uso de Hola de cada uno de los recursos de red de hello en una suscripción en una región con el número máximo de Hola de recursos disponibles.

![límite de suscripción de red][nsl]

## <a name="network-resource-level-monitoring"></a>Supervisión en el nivel de recursos de red

Hola siguientes características está disponible para la supervisión de nivel de recurso:

### <a name="audit-log"></a>Registro de auditoría

Se registran las operaciones realizadas como parte de la configuración de Hola de redes. Estos registros pueden verse en el portal de Azure de Hola o recuperan mediante herramientas de Microsoft como Power BI o herramientas de terceros. Los registros de auditoría están disponibles a través del portal de hello, PowerShell, CLI y API de Rest. Para más información sobre los registros de auditoría, consulte [Operaciones de auditoría con Resource Manager](../resource-group-audit.md).

Hay registros de auditoría disponibles para las operaciones realizadas en todos los recursos de red.

### <a name="metrics"></a>Métricas

Las métricas son medidas de rendimiento y contadores recopilados durante un período de tiempo. Las métricas están disponibles actualmente para Application Gateway. Las métricas pueden ser alertas tootrigger utilizados en función de umbral. Vea [puerta de enlace de Application Diagnostics](../application-gateway/application-gateway-diagnostics.md) tooview cómo las métricas pueden ser utilizados toocreate alertas.

![vista de métricas][metrics]

### <a name="diagnostic-logs"></a>Registros de diagnóstico

Eventos periódicos y espontáneos son creados por los recursos de red y se registra en las cuentas de almacenamiento, enviadas tooan concentrador de eventos o análisis de registros. Estos registros proporcionan información sobre el estado de saludo de un recurso. Estos registros se pueden ver en herramientas como Power BI y Log Analytics. toolearn cómo tooview registros de diagnóstico, visite [análisis de registros](../log-analytics/log-analytics-azure-networking-analytics.md).

Los registros de diagnóstico están disponibles para el [equilibrador de carga](../load-balancer/load-balancer-monitor-log.md), los [grupos de seguridad de red](../virtual-network/virtual-network-nsg-manage-log.md), las rutas y [Application Gateway](../application-gateway/application-gateway-diagnostics.md).

Network Watcher proporciona una vista de los registros de diagnóstico. Esta vista contiene todos los recursos de las redes que admiten el registro de diagnóstico. Desde esta vista, puede habilitar y deshabilitar los recursos de red de forma cómoda y rápida.

![logs][logs]

### <a name="troubleshooting"></a>Solución de problemas

Hola, solución de problemas de hoja, una experiencia en el portal de hello, se proporciona en los recursos de red hoy en día toodiagnose problemas comunes asociados a un recurso individual. Esta experiencia está disponible para hello después de recursos de red - ExpressRoute, puerta de enlace de VPN, puerta de enlace de aplicaciones, los registros de seguridad de red, rutas, DNS, equilibrador de carga y Traffic Manager. toolearn más acerca de la solución de nivel de recurso, visite [diagnosticar y resolver problemas con la solución de problemas de Azure](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![información de solución de problemas][TS]

### <a name="resource-health"></a>Estado de los recursos

estado de Hola de un recurso de red se proporciona de forma periódica. Estos recursos incluyen VPN Gateway y el túnel de VPN. Estado del recurso es accesible en hello portal de Azure. toolearn más información acerca del estado de los recursos, visite [información general de mantenimiento de recursos](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Pasos siguientes

Después de conocer Network Watcher, puede aprender a:

Realice una captura de paquetes en su máquina virtual visitando [captura de paquetes Variable Hola portal de Azure](network-watcher-packet-capture-manage-portal.md)

Realizar una supervisión y unos diagnósticos proactivos mediante la [captura de paquetes desencadenada mediante alertas](network-watcher-alert-triggered-packet-capture.md).

Detectar vulnerabilidades de seguridad con el [Análisis de captura de paquetes con Wireshark](network-watcher-deep-packet-inspection.md), mediante herramientas de código abierto.

Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











