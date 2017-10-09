---
title: "Agregación de eventos de servicio de Fabric con diagnósticos de Azure de Linux aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre la agregación y la recopilación de eventos con LAD para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Recopilación y agregación de eventos con Linux Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Cuando se ejecuta un clúster de Azure Service Fabric, es un buena idea toocollect Hola inicia una sesión de todos los nodos de hello en una ubicación central. Tener registros de hello en una ubicación central le ayuda a analizar y solucionar problemas en el clúster o problemas en aplicaciones de Hola y servicios que se ejecutan en ese clúster.

Tooupload de una forma y recopilar registros es la extensión de diagnósticos de Azure de Linux (LAD) de hello toouse, que carga tooAzure almacenamiento de registros pero también tiene Hola opción toosend registros tooAzure Application Insights o concentradores de eventos. También puede usar un proceso externo tooread Hola de eventos de almacenamiento y colocarlos en un producto de plataforma de análisis, como [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registro.

## <a name="log-and-event-sources"></a>Orígenes de eventos y registros

### <a name="service-fabric-platform-events"></a>Eventos de plataforma de Service Fabric
Service Fabric genera una serie de registros de serie a través de [LTTng](http://lttng.org), incluidos eventos de runtime o eventos operativos. Estos registros se almacenan en la ubicación de Hola que Hola plantilla especifica el Administrador de recursos del clúster. tooget o establecer detalles de cuenta de almacenamiento de hello, busque la etiqueta de hello **AzureTableWinFabETWQueryable** y busque **StoreConnectionString**.

### <a name="application-events"></a>Eventos de aplicación
 Eventos emitidos desde el código de los servicios y las aplicaciones especificados por el usuario al instrumentar el software. Puede utilizar cualquier solución de registro que escriba archivos de registro basados en texto, por ejemplo, LTTng. Para obtener más información, consulte la documentación de LTTng de hello en seguimiento de la aplicación.

[Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

## <a name="deploy-hello-diagnostics-extension"></a>Implementar la extensión de diagnósticos de Hola
Hola primer paso en la recopilación de registros es toodeploy extensión de diagnósticos de hello en cada una de las máquinas virtuales de hello en clúster de Service Fabric Hola. extensión de diagnósticos de Hello recopila registros en cada máquina virtual y los carga toohello cuenta de almacenamiento que especifique. pasos de Hello varían en función de si utiliza Hola portal de Azure o Azure Resource Manager.

establecer toodeploy Hola diagnósticos extensión toohello máquinas virtuales en clúster de hello como parte de la creación del clúster, **diagnósticos** demasiado**en**. Después de crear el clúster de hello, no se puede cambiar esta configuración mediante el portal de Hola.

A continuación, configurar los diagnósticos de Azure de Linux (LAD) toocollect Hola archivos y colocarlos en la cuenta de almacenamiento. Este proceso se explica como escenario 3 ("cargar sus propios archivos de registro") en el artículo hello [toomonitor LAD uso y diagnosticar máquinas virtuales de Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Siguiendo este obtiene proceso acceso toohello realiza un seguimiento. Puede cargar el visualizador de tooa Hola seguimientos de su elección.

También puede implementar la extensión de diagnósticos de hello mediante el Administrador de recursos de Azure. es similar para Windows y Linux Hello proceso y se documentan para los clústeres de Windows en [modo toocollect registra con diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md).

También puede usar Operations Management Suite, como se describe en [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) (Análisis de registros de Operations Management Suite con Linux).

Después de finalizar esta configuración, monitores de agente LAD Hola Hola archivos de registro especificados. Cada vez que una nueva línea es archivo toohello anexado, crea una entrada de syslog es toohello enviados de almacenamiento que especificó.

## <a name="next-steps"></a>Pasos siguientes

toounderstand con más detalle qué eventos se deben examinar si se intenta solucionar problemas, consulte [LTTng documentación](http://lttng.org/docs) y [LAD utilizando](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
