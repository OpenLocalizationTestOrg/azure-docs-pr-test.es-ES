---
title: aaaTroubleshooting con seguimiento de eventos | Documentos de Microsoft
description: "problemas más comunes de Hello al implementar servicios en Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Solución de problemas comunes al implementar servicios en Azure Service Fabric
Si estás ejecutando los servicios en el equipo del desarrollador, resulta fácil toouse [herramientas de depuración de Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Para los clústeres remotos, [informes de mantenimiento](service-fabric-view-entities-aggregated-health.md) siempre son un buen lugar toostart. Hola tooaccess más fácil de formas son estos informes a través de PowerShell o [SFX](service-fabric-visualizing-your-cluster.md). En este artículo se da por supuesto que está depurando un clúster remoto y tener un conocimiento básico de cómo toouse cualquiera de estas herramientas.

## <a name="application-crash"></a>Bloqueo de aplicaciones
Hola "partición está por debajo de recuento de instancia o la réplica de destino" informe es una buena indicación de que el servicio está bloqueado. toofind out donde está bloqueando el servicio tarda un poco más investigación. Cuando el servicio se ejecuta a escala, su mejor amigo será un conjunto de seguimiento bien elaborados.  Le sugerimos que pruebe [diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) para recopilar esos seguimientos y con una solución como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para ver y buscar seguimientos de Hola.

![Estado de las particiones SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Durante la inicialización del actor o del servicio
Cualquier excepción antes de inicializa el tipo de servicio de hello provocará Hola proceso toocrash. Para estos tipos de bloqueos, registro de eventos de aplicación Hola mostrará error Hola de su servicio.
Se trata de toosee las excepciones más comunes de hello antes de inicializa el servicio de Hola.

***System.IO.FileNotFoundException***

Este error suele ser debido a las dependencias de ensamblado de toomissing. Compruebe la propiedad CopyLocal de hello en Visual Studio o la caché de ensamblados global de hello para el nodo de Hola.

***System.Runtime.InteropServices.COMException*** *en System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Esto indica que ese nombre de tipo de servicio registrado hello no coincide con el manifiesto del servicio Hola.

[Diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) puede ser configurado tooupload Hola el registro de eventos de aplicación para todos los nodos automáticamente.

### <a name="runasync-or-onactivateasync"></a>RunAsync() o OnActivateAsync()
Si se produce un bloqueo de Hola durante la inicialización de Hola o la ejecución de su tipo de servicio registrado o un actor, excepción de hello detectará Azure Service Fabric. Puede ver estas desde proveedores de hello EventSource detallados en la sección "Pasos siguientes" Hola.

## <a name="next-steps"></a>Pasos siguientes
Más información sobre el diagnóstico existente ofrecido por Service Fabric:

* [Diagnósticos de Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Diagnóstico de Reliable Services](service-fabric-reliable-services-diagnostics.md)

