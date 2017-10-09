---
title: uso de aaaAdvanced de servicios de confianza | Documentos de Microsoft
description: "Obtenga información sobre el uso avanzado de Reliable Services de Service Fabric para obtener una mayor flexibilidad en los servicios."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>Uso del modelo de programación de servicios confiables Hola avanzado
Azure Service Fabric simplifica la escritura y administración de los servicios con y sin estado confiables. Esta guía habla de usos avanzados de servicios de confianza toogain mayor control y flexibilidad sobre los servicios. Tooreading anterior esta guía, familiarícese con [modelo de programación de servicios de confianza de hello](service-fabric-reliable-services-introduction.md).

Los servicios con y sin estado tienen dos puntos de entrada principal para el código de usuario:

* `RunAsync(C#) / runAsync(Java)` es un punto de entrada de propósito general para el código del servicio.
* `CreateServiceReplicaListeners(C#)` y `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` se usan con el fin de abrir agentes de escucha de comunicación para las solicitudes de cliente.

En la mayoría de los servicios, estos puntos de dos entradas son suficientes. En raras ocasiones, cuando se precisa más control sobre el ciclo de vida de un servicio, se encuentran disponibles eventos de ciclo de vida adicionales.

## <a name="stateless-service-instance-lifecycle"></a>Ciclo de vida de instancias de servicios sin estado
El ciclo de vida de un servicio sin estado es muy sencillo. Los servicios sin estado solo se pueden abrir, cerrar o anular. El elemento `RunAsync` incluido en un servicio sin estado se ejecuta cuando se abre una instancia de este y se cancela cuando se cierra o anula una instancia de dicho servicio.

Aunque `RunAsync` debería ser suficiente en casi todos los casos, Hola abrir, cerrar y eventos de anulación en un servicio sin estado también están disponibles:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync se llama una vez instancia de servicio sin estado Hola sobre toobe usa. En este momento, se pueden iniciar las tareas de inicialización del servicio ampliado.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync se llama cuando la instancia de servicio sin estado Hola va toobe cerrado correctamente. Esto puede ocurrir cuando se está actualizando el código de servicio de hello, instancia de servicio de Hola se traslada debido tooload equilibrio o se detecta un error transitorio. OnCloseAsync puede ser usado toosafely cerrar todos los recursos, detener cualquier procesamiento en segundo plano, terminar de guardar estado externo o cerrar conexiones existentes.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort se llama cuando la instancia de servicio sin estado de saludo se está cerrando forzosamente. Por lo general, esto se denomina cuando se detecta un error permanente en el nodo de hello, o cuando Service Fabric no se puede administrar de manera fiable del ciclo de vida de la instancia de servicio de hello debido a errores de toointernal.

## <a name="stateful-service-replica-lifecycle"></a>Ciclo de vida de réplicas de servicio con estado

> [!NOTE]
> Las instancias con estado de Reliable Services aún no se admiten en Java.
>
>

El ciclo de vida de una réplica de servicio con estado es mucho más complejo que una instancia de servicio sin estado. Además tooopen, cierre y anular los eventos, cambios de rol se somete a una réplica de servicio con estado durante su duración. Cuando una réplica de servicio con estado cambia de rol, Hola `OnChangeRoleAsync` se desencadena el evento:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync se llama cuando la réplica de servicio con estado de hello es cambiar el rol, por ejemplo tooprimary o base de datos secundaria. Las réplicas principales tienen estado de escritura (se permiten toocreate y escribir tooReliable colecciones). Las réplicas secundarias reciben el estado de lectura (solo pueden leer desde Reliable Collections existentes). Se realiza la mayor parte del trabajo en un servicio con estado en la réplica principal de Hola. Las réplicas secundarias pueden realizar validación de solo lectura, generación de informes, minería de datos u otros trabajos de solo lectura.

En un servicio con estado, sólo réplica principal de hello tiene toostate de acceso de escritura y, por tanto, generalmente es cuando el servicio de hello está realizando trabajo real. Hola `RunAsync` método en un servicio con estado se ejecuta solo cuando la réplica de servicio con estado de hello es principal. Hola `RunAsync` método se cancela cuando los cambios de rol de la réplica principal fuera principal, así como durante Hola cierre y anulación los eventos.

Con hello `OnChangeRoleAsync` evento le permite tooperform trabajo según el rol de réplica, así como en el cambio de toorole de respuesta.

Un servicio con estado también proporciona eventos de ciclo de vida de hello cuatro misma como un servicio sin estado, con Hola la misma semántica y casos de uso:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Pasos siguientes
Para más avanzados temas de tejido de tooService relacionados, vea Hola siguientes artículos:

* [Configuración de Reliable Services con estado](service-fabric-reliable-services-configuration.md)
* [Introducción al estado de Service Fabric](service-fabric-health-introduction.md)
* [Uso de informes de mantenimiento del sistema para solucionar problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Configuración de servicios con hello servicio Administrador de recursos del clúster de tejido](service-fabric-cluster-resource-manager-configure-services.md)
