---
title: "aaaOverview de diagnósticos de Azure | Documentos de Microsoft"
description: "Use Diagnósticos de Azure para realizar tareas de depuración, medición de rendimiento, supervisión y análisis de tráfico en servicios en la nube, en máquinas virtuales y en Service Fabric"
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>¿Qué es Diagnósticos de Azure?
Diagnósticos de Azure es la capacidad de hello dentro de Azure que habilita la recopilación de Hola de datos de diagnóstico en una aplicación implementada. Puede usar la extensión de diagnósticos de Hola de una serie de orígenes diferentes. Actualmente se admiten los roles web y de trabajo del Servicio en la nube de Azure, las máquinas virtuales de Azure que ejecutan Microsoft Windows y Service Fabric. Otros servicios de Azure tienen su propio diagnóstico independiente.

## <a name="data-you-can-collect"></a>Datos que puede recopilar
Diagnósticos de Azure pueden recopilar Hola siguientes tipos de datos:

| Origen de datos | Description |
| --- | --- |
| Contadores de rendimiento |Sistema operativo y contadores de rendimiento personalizados |
| Registros de aplicación |Seguimiento de mensajes escritos por la aplicación |
| Registros de eventos de Windows |Información que se envía el sistema de registro de eventos de Windows toohello |
| Origen de eventos de .NET |Código escribir eventos mediante .NET hello [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) (clase) |
| Registros IIS |Información sobre los sitios web de IIS |
| ETW basado en manifiesto |Eventos de Seguimiento de eventos para Windows generados por cualquier proceso |
| Volcados de memoria |Información sobre estado de saludo del proceso de hello en caso de hello de bloqueo de una aplicación |
| Registros de errores personalizados |Registros creados por su aplicación o servicio |
| Registros de infraestructura de diagnóstico de Azure |Información sobre Diagnósticos |

Hola extensión de diagnósticos de Azure puede transferir esta cuenta de almacenamiento de Azure de datos tooan o enviarlo tooservices como [Application Insights](../application-insights/app-insights-cloudservices.md). Puede usar datos de Hola para depuración y solución de problemas, medir el rendimiento, uso de recursos, análisis del tráfico y planear la capacidad de supervisión y auditoría.

## <a name="versioning"></a>Control de versiones
Consulte el [historial de versiones de Diagnósticos de Azure](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Pasos siguientes
Elija el servicio que está tratando de diagnósticos de toocollect y usar Hola después tooget de artículos que se inició. Use los vínculos de diagnósticos de Azure generales de hello como referencia para tareas específicas.

## <a name="web-apps"></a>Web Apps
Tenga en cuenta que las aplicaciones web no utilizan Diagnósticos de Azure. Encontrar información equivalente de hello en [aplicaciones Web](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Servicios en la nube que usan Diagnósticos de Azure
* Si utiliza Visual Studio, consulte [tootrace utilice Visual Studio una aplicación de servicios en la nube](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget iniciado. De lo contrario, consulte
* [¿Cómo toomonitor nube servicios mediante Diagnósticos de Azure](../cloud-services/cloud-services-how-to-monitor.md)
* [Configuración de Diagnósticos de Azure una aplicación de Cloud Services](../cloud-services/cloud-services-dotnet-diagnostics.md)

Para temas más avanzados, consulte

* [Uso de Diagnósticos de Azure con Application Insights para Cloud Services](../application-insights/app-insights-cloudservices.md)
* [Flujo de Hola de seguimiento de una aplicación de servicios en la nube con diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Usar PowerShell tooset de diagnósticos en servicios en la nube](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Máquinas virtuales que usan Diagnósticos de Azure
* Si utiliza Visual Studio, consulte [tootrace utilice Visual Studio máquinas virtuales de Azure](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget iniciado. De lo contrario, consulte
* [Configuración de Diagnósticos de Azure en Azure Virtual Machine](../virtual-machines-dotnet-diagnostics.md)

Para temas más avanzados, consulte

* [Usar PowerShell tooset de diagnóstico en máquinas virtuales de Azure](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Creación de una máquina virtual de Windows con supervisión y diagnóstico mediante una plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric con Diagnósticos de Azure
Empiece por el artículo sobre la [supervisión de una aplicación de Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Muchos otros artículos de diagnósticos de tejido de servicio están disponibles en el árbol de navegación de hello en hello izquierda cuando obtenga toothis artículo.

## <a name="general-azure-diagnostics-articles"></a>Artículos generales de Diagnósticos de Azure
* [Configuración del esquema del diagnóstico de Azure](https://msdn.microsoft.com/library/azure/mt634524.aspx) : Obtenga información acerca de cómo toochange Hola toocollect del archivo de esquema y enrutar los datos de diagnóstico. Tenga en cuenta que también puede utilizar el archivo de esquema de Visual Studio toochange Hola.
* [Cómo se almacenan los datos de diagnóstico de Azure en almacenamiento de Azure](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -conocer Hola nombres de tablas de Hola y de blobs donde se escriben los datos de diagnóstico de saludo.
* Obtenga información acerca de demasiado[utilizar contadores de rendimiento en el diagnóstico de Azure](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* Obtenga información acerca de demasiado[tooApplication de información de diagnóstico de Azure de ruta visión](azure-diagnostics-configure-application-insights.md)
* Si tiene problemas al iniciar los diagnósticos o al buscar datos en las tablas de Azure Storage, consulte [Solución de problemas de Diagnósticos de Azure](azure-diagnostics-troubleshooting.md).
