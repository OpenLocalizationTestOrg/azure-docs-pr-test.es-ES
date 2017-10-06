---
title: "registros de aaaCollect con el diagnóstico de Azure de Linux | Documentos de Microsoft"
description: "Este artículo describe cómo se registra tooset seguridad toocollect de diagnósticos de Azure desde un clúster de Service Fabric Linux que se ejecuta en Azure."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Recopilación de registros con Diagnósticos de Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Cuando se ejecuta un clúster de Azure Service Fabric, es un buena idea toocollect Hola inicia una sesión de todos los nodos de hello en una ubicación central. Tener registros de hello en una ubicación central resulta fácil tooanalyze y solucionar problemas, independientemente de si están en los servicios, la aplicación o el propio clúster Hola. Tooupload de una forma y recopilar registros es extensión de diagnósticos de Azure hello toouse, qué cargas registra tooAzure almacenamiento, Azure Application Insights o concentradores de eventos de Azure. También puede leer los eventos de Hola de almacenamiento o concentradores de eventos y colocarlos en un producto como [análisis de registros](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registro. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) tiene integrado un servicio integral de análisis y búsqueda de registros.

## <a name="log-sources-that-you-might-want-toocollect"></a>Orígenes de registro que podría interesarle toocollect
* **Registros de Service Fabric**: emitidos a partir de la plataforma de Hola a través de [LTTng](http://lttng.org) y cargado tooyour cuenta de almacenamiento. Los registros pueden ser eventos operativos o eventos en tiempo de ejecución que Hola plataforma emite. Estos registros se almacenan en la ubicación de hello especifica dicho manifiesto de clúster Hola. (detalles de la cuenta de almacenamiento de tooget hello, Buscar etiqueta hello **AzureTableWinFabETWQueryable** y busque **StoreConnectionString**.)
* **Eventos de aplicación:** eventos emitidos desde el código de servicios. Puede utilizar cualquier solución de registro que escriba archivos de registro basados en texto, por ejemplo, LTTng. Para obtener más información, consulte la documentación de LTTng de hello en seguimiento de la aplicación.  

## <a name="deploy-hello-diagnostics-extension"></a>Implementar la extensión de diagnósticos de Hola
Hola primer paso en la recopilación de registros es toodeploy extensión de diagnósticos de hello en cada una de las máquinas virtuales de hello en clúster de Service Fabric Hola. extensión de diagnósticos de Hello recopila registros en cada máquina virtual y los carga toohello cuenta de almacenamiento que especifique. pasos de Hello varían en función de si utiliza Hola portal de Azure o Azure Resource Manager.

establecer toodeploy Hola diagnósticos extensión toohello máquinas virtuales en clúster de hello como parte de la creación del clúster, **diagnósticos** demasiado**en**. Después de crear el clúster de hello, no se puede cambiar esta configuración mediante el portal de Hola.

A continuación, configurar los diagnósticos de Azure de Linux (LAD) toocollect Hola archivos y colocarlos en la cuenta de almacenamiento. Este proceso se explica como escenario 3 ("cargar sus propios archivos de registro") en el artículo hello [toomonitor LAD uso y diagnosticar máquinas virtuales de Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Siguiendo este obtiene proceso acceso toohello realiza un seguimiento. Puede cargar el visualizador de tooa Hola seguimientos de su elección.

También puede implementar la extensión de diagnósticos de hello mediante el Administrador de recursos de Azure. es similar para Windows y Linux Hello proceso y se documentan para los clústeres de Windows en [modo toocollect registra con diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md).

También puede usar Operations Management Suite, como se describe en [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) (Análisis de registros de Operations Management Suite con Linux).

Después de finalizar esta configuración, monitores de agente LAD Hola Hola archivos de registro especificados. Cada vez que una nueva línea es archivo toohello anexado, crea una entrada de syslog es toohello enviados de almacenamiento que especificó.

## <a name="next-steps"></a>Pasos siguientes
toounderstand con más detalle qué eventos se deben examinar si se intenta solucionar problemas, consulte [LTTng documentación](http://lttng.org/docs) y [LAD utilizando](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

