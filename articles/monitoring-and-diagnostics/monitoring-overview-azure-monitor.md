---
title: "Introducción al Monitor de aaaAzure | Documentos de Microsoft"
description: "Azure Monitor recopila estadísticas para usarse en procesos de alertas, webhooks, escalado automático y automatización. En el artículo también se muestran otras opciones de supervisión de Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Información general sobre Azure Monitor
Este artículo proporciona información general de hello servicio de Monitor de Azure de Microsoft Azure. Describe lo que hace el Monitor de Azure y proporciona punteros tooadditional información acerca de cómo toouse Monitor de Azure.  Si prefiere un vídeo de introducción, consulte los vínculos de pasos siguientes final Hola de este artículo. 

## <a name="why-monitor-your-application-or-system"></a>¿Por qué supervisar la aplicación o el sistema?
Las aplicaciones de nube son complejas y tienen muchas partes móviles. La supervisión proporciona tooensure de datos que mantiene la aplicación y en ejecución en un estado correcto. También ayuda a toostave off posibles problemas o solucionar problemas más allá de los. Además, puede usar supervisión toogain profundo información sobre los datos acerca de la aplicación. Esa información puede ayudarle a rendimiento de la aplicación de tooimprove o mantenimiento o automatizar acciones que en caso contrario requerirían intervención manual.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure Monitor y otros productos de supervisión de Microsoft
Azure Monitor ofrece registros y métricas de infraestructuras a nivel básico para la mayoría de los servicios de Microsoft Azure. Servicios de Azure que no aún poner sus datos en el Monitor de Azure, se colocará allí en hello futuras.

Microsoft entrega productos y servicios adicionales que ofrecen funcionalidades de supervisión adicionales para desarrolladores, DevOps u operaciones de TI que también tienen instalaciones locales. Para obtener una introducción e información sobre cómo estos distintos productos y servicios funcionan de forma conjunta, vea [Supervisión en Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Orígenes de supervisión: Compute

![Modelo para la supervisión y el diagnóstico de recursos que no son de proceso](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

los servicios de proceso Hola incluyen 
- Cloud Services 
- Máquinas virtuales 
- Conjuntos de escalado de máquina virtual 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Aplicación: registros de diagnóstico, registros de aplicación y métricas
Pueden ejecutar aplicaciones en la parte superior Hola SO invitado en el modelo de proceso de Hola. Emiten su propio conjunto de registros y métricas. Monitor de Azure basa en la extensión de diagnósticos de Azure (Windows o Linux) toocollect de Hola la mayoría de los registros y las métricas de nivel de aplicación. incluyen tipos de Hola

* Contadores de rendimiento
* Registros de aplicación
* Registros de eventos de Windows
* Origen de eventos de .NET
* Registros IIS
* ETW basado en manifiesto
* Volcados de memoria
* Registros de errores personalizados

Sin la extensión de diagnósticos de hello, están disponibles solo algunas métricas como el uso de CPU. 

### <a name="host-and-guest-vm-metrics"></a>Métricas de máquinas virtuales host e invitadas
Hello recursos de proceso enumerados anteriormente tienen una máquina virtual del host dedicado y que interactúan con el SO invitado. máquina virtual del host de Hola y el sistema operativo invitado son equivalente de Hola de raíz virtual y máquina virtual invitada en el modelo de hipervisor de Hyper-V de Hola. Puede recopilar métricas en ambos. También puede recopilar registros de diagnóstico en el sistema operativo invitado de Hola.   

### <a name="activity-log"></a>Registro de actividad
Puede buscar hello (anteriormente denominados operativa o los registros de auditoría) de registro de actividad para obtener información sobre el recurso tal como lo ve Hola infraestructura de Azure. registro de Hello contiene información como veces cuando se crea o destruye recursos.  Para más información, vea [Información general sobre el registro de actividad de Azure](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Orígenes de supervisión: el resto

![Modelo para la supervisión y el diagnóstico de recursos que son de proceso](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Recurso: métricas y registros de diagnóstico
Registros de las métricas y diagnósticos recopilable varían en función de tipo de recurso de Hola. Por ejemplo, las aplicaciones Web proporciona estadísticas de hello E/S de disco y CPU de porcentaje. Esas métricas no existen para una cola de Service Bus, sino métricas como el tamaño de cola y el rendimiento de mensajes. Una lista de métricas que se pueden recopilar para cada recurso está disponible en [métricas admitidas](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Métricas de máquinas virtuales host e invitadas
No hay necesariamente una asignación 1:1 entre los recursos y una máquina virtual host o una máquina virtual invitada específica; por tanto, las métricas no están disponibles.

### <a name="activity-log"></a>Registro de actividad
registro de actividad de Hello es Hola igual que para los recursos de proceso.  

## <a name="uses-for-monitoring-data"></a>Usos de los datos de supervisión
Una vez que recopilar los datos, puede hacer Hola después con él en el Monitor de Azure

### <a name="route"></a>Enrutar
Puede transmitir supervisión ubicaciones de tooother de datos en tiempo real.

Algunos ejemplos son:

- Enviar tooApplication visión para poder utilizar las herramientas de visualización y análisis más completos.
- Enviar tooEvent concentradores para que pueda enrutar herramientas toothird fabricantes. 

### <a name="store-and-archive"></a>Almacenamiento y archivado
Algunos datos de supervisión ya están almacenados y disponibles en Azure Monitor durante un período de tiempo. 
- Las métricas se almacenan durante 30 días. 
- Las entradas de registros de actividad se almacenan durante 90 días. 
- Los registros de diagnóstico no se almacenan. 

Si desea toostore datos más allá Hola períodos de tiempo mencionados anteriormente, puede usar un almacenamiento de Azure. Los datos de supervisión se mantienen en la cuenta de almacenamiento en función de la directiva de retención definida. Es necesario toopay para Hola Hola de espacio datos ocupa el almacenamiento de Azure. 

Unos toouse formas estos datos:

- Una vez escritos, puede hacer que otras herramientas, dentro o fuera de Azure, los lean y los procesen.
- Descargar datos Hola localmente para un archivo local o cambiar la directiva de retención de datos en la nube tookeep Hola durante largos períodos de tiempo.  
- Dejar datos hello en el almacenamiento de Azure indefinidamente para archivarlo. 

### <a name="query"></a>Consultar
Puede usar Hola API de REST de Monitor de Azure, comandos de la interfaz de línea de comandos (CLI) de multiplataforma, cmdlets de PowerShell, o tooaccess del SDK de .NET de Hola Hola datos en el sistema de Hola o almacenamiento de Azure

Algunos ejemplos son:

* Obtener datos para una aplicación de supervisión personalizada que ha escrito.
* Crear consultas personalizadas y enviar esa aplicación de terceros de tooa de datos.

### <a name="visualize"></a>Visualizar
Visualizar los datos supervisados en gráficos y gráficos ayuda a identificar tendencias más rápida que la búsqueda a través de los propios datos de Hola.  

Algunos métodos de visualización incluyen:

* Usar hello portal de Azure
* Enrutar datos tooAzure Application Insights
* Enrutar datos tooMicrosoft Power BI
* Ruta Hola datos tooa terceros visualización herramienta mediante o streaming en directo o manteniendo herramienta Hola lee desde un archivo en el almacenamiento de Azure


### <a name="automate"></a>Automatizar
Puede usar alertas de supervisión datos tootrigger o incluso procesos enteros. Algunos ejemplos son:

* Utilice instancias de proceso de datos tooautoscale hacia arriba o hacia abajo según la carga de la aplicación.
* Enviar mensajes de correo electrónico cuando una métrica cruza un umbral predeterminado.
* Llamar a un tooexecute de dirección URL (webhook) web una acción en un sistema fuera de Azure
* Iniciar un runbook en automatización de Azure tooperform cualquier serie de tareas

## <a name="methods-of-accessing-azure-monitor"></a>Métodos de acceso a Azure Monitor
En general, puede manipular el seguimiento de los datos, el enrutamiento y la recuperación mediante uno de los siguientes métodos de Hola. No todos los métodos están disponibles para todas las acciones o tipos de datos.

* [Portal de Azure](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Interfaz de línea de comandos (CLI) multiplataforma](insights-cli-samples.md)
* [API DE REST](https://docs.microsoft.com/rest/api/monitor/)
* [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de
- Hay un tutorial en vídeo de Azure Monitor en  
[Introducción a Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor) Puede consultar un vídeo adicional donde se explica un escenario en el que puede usar Azure Monitor en [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) (Información sobre supervisión y Microsoft Azure Diagnostics) y en un [vídeo sobre Azure Monitor de Ignite 2016](https://myignite.microsoft.com/videos/4977)
- Ejecutar procesos a través de la interfaz del Monitor de Azure de hello en [introducción con el Monitor de Azure](monitoring-get-started.md)
- Configurar hello [extensiones de diagnóstico de Azure](../azure-diagnostics.md) si estás intentando toodiagnose problemas en el servicio de nube, Máquina Virtual, Máquina Virtual escalar conjuntos o aplicación de Service Fabric.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) si está tratando de toodiagnostic problemas en la aplicación Web de servicio de aplicación.
- [Solución de problemas de Azure Storage](../storage/common/storage-e2e-troubleshooting.md) : si usa Blob Storage, Table Storage o Queue Storage.
- [Análisis de registros](https://azure.microsoft.com/documentation/services/log-analytics/) hello y [Operations Management Suite](https://www.microsoft.com/oms/)
