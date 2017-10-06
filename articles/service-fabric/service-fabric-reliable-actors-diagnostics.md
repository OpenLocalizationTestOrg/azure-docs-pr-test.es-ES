---
title: "aaaActors diagnósticos y supervisión | Documentos de Microsoft"
description: "Este artículo describen características en tiempo de ejecución de servicio Fabric Reliable Actors hello, incluye eventos de Hola y emitidos por el los contadores de rendimiento de supervisión de rendimiento y diagnóstico de Hola."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnósticos y supervisión del rendimiento de Reliable Actors
tiempo de ejecución de Hello Reliable Actors emite [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos y [contadores de rendimiento](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Estos proporcionan información sobre cómo funciona en tiempo de ejecución de Hola y ayudarán con la solución de problemas y supervisión de rendimiento.

## <a name="eventsource-events"></a>Eventos EventSource
nombre del proveedor de EventSource de Hello en tiempo de ejecución de Reliable Actors hello es "Microsoft-ServiceFabric-actores". Eventos de este origen de eventos aparecen en hello [eventos de diagnósticos de](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) ventana cuando se va la aplicación de actor hello [depurar en Visual Studio](service-fabric-debugging-your-application.md).

Son ejemplos de herramientas y tecnologías que ayudan a recopilar y ver eventos EventSource [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md), [registro semántica](https://msdn.microsoft.com/library/dn774980.aspx), hello y[ Biblioteca de Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Palabras clave
Todos los eventos que pertenecen toohello confiable EventSource actores están asociados con una o más palabras clave. Esto habilita el filtrado de los eventos que se recopilan. Hola después de bits de la palabra clave se define.

| Bit | Descripción |
| --- | --- |
| 0x1 |Conjunto de eventos importantes que resuman operación Hola del tiempo de ejecución de hello actores de tejido. |
| 0x2 |Conjunto de eventos que describe las llamadas de método de actor. Para obtener más información, vea hello [tema de introducción en actores](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Conjunto de eventos relacionados tooactor estado. Para obtener más información, vea el tema de hello en [administración de estado de actor](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Conjunto de simultaneidad basada en tooturn relacionados con eventos de actor Hola. Para obtener más información, vea el tema de hello en [simultaneidad](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Contadores de rendimiento
en tiempo de ejecución de Hello Reliable Actors define Hola siguientes categorías de contador de rendimiento.

| Categoría | Descripción |
| --- | --- |
| Actor de Service Fabric |Contadores de actores de Service Fabric tooAzure específico, por ejemplo, tiempo toosave el estado de actor |
| Método del actor de Service Fabric |Contadores de toomethods específica implementada por actores de Service Fabric, por ejemplo, la frecuencia con la que se invoca un método de actor |

Cada uno de hello encima de las categorías tiene uno o varios contadores.

Hola [Monitor de rendimiento de Windows](https://technet.microsoft.com/library/cc749249.aspx) aplicación que está disponible de forma predeterminada en el sistema operativo de Windows hello puede ser usados datos del contador de rendimiento toocollect y vista. [Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) es otra opción para recopilar los datos del contador de rendimiento y cargarlos tooAzure tablas.

### <a name="performance-counter-instance-names"></a>Nombres de instancias de contador de rendimiento
Un clúster con un gran número de servicios de actor o particiones de servicios de actor tendrá una gran cantidad de instancias de contador de rendimiento de actor. Hello nombres de instancia de contador de rendimiento pueden ayudar a identificar específicos de hello [partición](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) y método de actor (si procede) esa instancia de contador de rendimiento de hello está asociada.

#### <a name="service-fabric-actor-category"></a>Categoría del actor de Service Fabric
De categoría de hello `Service Fabric Actor`, son nombres de instancia de contador de Hola Hola siguiendo el formato:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* es Hola representación de cadena de hello está asociado con Id. de partición de Service Fabric que Hola instancia del contador de rendimiento. Id. de partición de Hello es un GUID y su representación de cadena se genera a través de hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método con el especificador de formato "D".

*ActorRuntimeInternalID* es Hola representación de cadena de un entero de 64 bits que se genera en tiempo de ejecución de hello actores de tejido para su uso interno. Esto se incluye en la instancia de contador de rendimiento de hello, asigne un nombre tooensure su unicidad y evitar el conflicto con otros nombres de instancia de contador de rendimiento. Los usuarios no deben intentar toointerpret esta parte del nombre de instancia de contador de rendimiento de Hola.

Hello aquí te mostramos un ejemplo de un nombre de instancia de contador de un contador que pertenece toohello `Service Fabric Actor` categoría:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

En el ejemplo de Hola anterior, `2740af29-78aa-44bc-a20b-7e60fb783264` es Hola representación de cadena de Id. de partición de Service Fabric de hello, y `635650083799324046` es utilizar el Id. de 64 bits de hello generada para hello en tiempo de ejecución interno.

#### <a name="service-fabric-actor-method-category"></a>Categoría del método del actor de Service Fabric
De categoría de hello `Service Fabric Actor Method`, son nombres de instancia de contador de Hola Hola siguiendo el formato:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* es Hola nombre de método de actor Hola Hola instancia del contador de rendimiento asociado. formato de Hello del nombre de método de Hola se determina en función de alguna lógica en tiempo de ejecución de los actores de tejido de Hola que equilibre la legibilidad de hello del nombre de hello con restricciones en la longitud máxima de Hola de nombres de instancia de contador de rendimiento de hello en Windows.

*ActorsRuntimeMethodId* es Hola representación de cadena de un entero de 32 bits que se genera en tiempo de ejecución de hello actores de tejido para su uso interno. Esto se incluye en la instancia de contador de rendimiento de hello, asigne un nombre tooensure su unicidad y evitar el conflicto con otros nombres de instancia de contador de rendimiento. Los usuarios no deben intentar toointerpret esta parte del nombre de instancia de contador de rendimiento de Hola.

*ServiceFabricPartitionID* es Hola representación de cadena de hello está asociado con Id. de partición de Service Fabric que Hola instancia del contador de rendimiento. Id. de partición de Hello es un GUID y su representación de cadena se genera a través de hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método con el especificador de formato "D".

*ActorRuntimeInternalID* es Hola representación de cadena de un entero de 64 bits que se genera en tiempo de ejecución de hello actores de tejido para su uso interno. Esto se incluye en la instancia de contador de rendimiento de hello, asigne un nombre tooensure su unicidad y evitar el conflicto con otros nombres de instancia de contador de rendimiento. Los usuarios no deben intentar toointerpret esta parte del nombre de instancia de contador de rendimiento de Hola.

Hello aquí te mostramos un ejemplo de un nombre de instancia de contador de un contador que pertenece toohello `Service Fabric Actor Method` categoría:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

En el ejemplo de Hola anterior, `ivoicemailboxactor.leavemessageasync` es el nombre del método hello, `2` es hello usa el Id. de 32 bits generado para interno en tiempo de ejecución de hello, `89383d32-e57e-4a9b-a6ad-57c6792aa521` es Hola representación de cadena de Id. de partición de Service Fabric de hello, y `635650083804480486` es Id. de 64 bits de Hola se genera para uso interno de hello en tiempo de ejecución.

## <a name="list-of-events-and-performance-counters"></a>Lista de eventos y contadores de rendimiento
### <a name="actor-method-events-and-performance-counters"></a>Eventos de método de actor y contadores de rendimiento
en tiempo de ejecución de Reliable Actors Hello emite Hola después de eventos relacionados con demasiado[métodos actor](service-fabric-reliable-actors-introduction.md).

| Nombre del evento | Id. de evento | Nivel | Palabra clave | Descripción |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Detallado |0x2 |En tiempo de ejecución de actores es sobre tooinvoke un método de actor. |
| ActorMethodStop |8 |Detallado |0x2 |Un método de actor terminó de ejecutarse. Es decir, ha devuelto el método de hello en tiempo de ejecución llamada asincrónica toohello actor y tarea hello devuelto por el método de actor hello ha terminado. |
| ActorMethodThrewException |9 |Warning (Advertencia) |0x3 |Se inició una excepción durante la ejecución de Hola de un método de actor, ya sea durante el método de hello en tiempo de ejecución llamada asincrónica toohello actor o durante la ejecución de Hola de tarea hello devuelto por método de actor Hola. Este evento indica a algún tipo de error en el código de actor Hola precisa investigación. |

en tiempo de ejecución de Hello Reliable Actors publica Hola después de la ejecución de toohello relacionados de contadores de rendimiento de los métodos de actor.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Método del actor de Service Fabric |Invocaciones/seg. |Número de veces que se invoca el método de servicio de actor hello por segundo |
| Método del actor de Service Fabric |Promedio de milisegundos por invocación |Método de servicio de tiempo que tarda tooexecute Hola actor en milisegundos |
| Método del actor de Service Fabric |Excepciones generadas/seg. |Número de veces que Hola método de servicio de actor inició una excepción por segundo |

### <a name="concurrency-events-and-performance-counters"></a>Contadores de rendimiento y eventos de simultaneidad
en tiempo de ejecución de Reliable Actors Hello emite Hola después de eventos relacionados con demasiado[simultaneidad](service-fabric-reliable-actors-introduction.md#concurrency).

| Nombre del evento | Id. de evento | Nivel | Palabra clave | Descripción |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Detallado |0x8 |Este evento se escribirá en el inicio de Hola de cada turno nuevo en un actor. Contiene Hola número de llamadas de actor que esperan tooacquire Hola el bloqueo por actor que exige la simultaneidad basada en Activar pendientes. |

en tiempo de ejecución de Hello Reliable Actors publica Hola después tooconcurrency relacionados de contadores de rendimiento.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Actor de Service Fabric |Número de llamadas de actor en espera de un bloqueo de actor |Número de llamadas de actor espera tooacquire Hola el bloqueo por actor que exige la simultaneidad basada en Activar pendientes |
| Actor de Service Fabric |Tiempo de espera promedio de bloqueos en milisegundos |Tiempo tooacquire tomada (en milisegundos) Hola el bloqueo por actor que exige la simultaneidad basada en Active |
| Actor de Service Fabric |Duración promedia del bloqueo por actor en milisegundos |Tiempo (en milisegundos) para que Hola se mantiene el bloqueo por actor |

### <a name="actor-state-management-events-and-performance-counters"></a>Contadores de rendimiento y eventos de administración del estado de los actores
en tiempo de ejecución de Reliable Actors Hello emite Hola después de eventos relacionados con demasiado[administración de estado de actor](service-fabric-reliable-actors-state-management.md).

| Nombre del evento | Id. de evento | Nivel | Palabra clave | Descripción |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Detallado |0x4 |En tiempo de ejecución de actores es sobre el estado de actor toosave Hola. |
| ActorSaveStateStop |11 |Detallado |0x4 |En tiempo de ejecución de actores ha terminado de guardar el estado de actor Hola. |

en tiempo de ejecución de Hello Reliable Actors publica Hola después de la administración de Estados de tooactor relacionados de contadores de rendimiento.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Actor de Service Fabric |Promedio de milisegundos por operación de almacenamiento del estado |Tiempo que tarda toosave el estado de actor en milisegundos |
| Actor de Service Fabric |Promedio de milisegundos por operación de carga de estado |Tiempo que tarda el estado de actor tooload en milisegundos |

### <a name="events-related-tooactor-replicas"></a>Eventos relacionados tooactor réplicas
en tiempo de ejecución de Reliable Actors Hello emite Hola después de eventos relacionados con demasiado[réplicas actor](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Nombre del evento | Id. de evento | Nivel | Palabra clave | Descripción |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informativo |0x1 |Réplica de actor cambia tooPrimary de rol. Esto implica que los actores de Hola para esta partición se creará dentro de esta réplica. |
| ReplicaChangeRoleFromPrimary |2 |Informativo |0x1 |Réplica de actor cambia toonon el rol principal. Esto implica que ya no se creará actores de Hola para esta partición dentro de esta réplica. Ninguna nueva solicitud se entregará tooactors ya creados en esta réplica. actores Hola se destruirá cuando se completen las solicitudes en curso. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Eventos de activación y desactivación de actores y contadores de rendimiento
en tiempo de ejecución de Reliable Actors Hello emite Hola después de eventos relacionados con demasiado[actor activación y desactivación](service-fabric-reliable-actors-lifecycle.md).

| Nombre del evento | Id. de evento | Nivel | Palabra clave | Descripción |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informativo |0x1 |Se activó un actor. |
| ActorDeactivated |6 |Informativo |0x1 |Se desactivó un actor. |

en tiempo de ejecución de Hello Reliable Actors publica Hola siguiendo los contadores de rendimiento relacionados con tooactor activación y desactivación.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Actor de Service Fabric |Promedio de milisegundos de OnActivateAsync |Tiempo consumido tooexecute el método OnActivateAsync en milisegundos |

### <a name="actor-request-processing-performance-counters"></a>Contadores de rendimiento del procesamiento de solicitudes de actor
Cuando un cliente invoca un método a través de un objeto de proxy de actor, se produce un mensaje de solicitud que se envían a través del servicio de actor de hello red toohello. servicio de Hello procesa el mensaje de solicitud de saludo y envía a un cliente de toohello de espera de respuesta. en tiempo de ejecución de Hello Reliable Actors publica Hola después de procesamiento de solicitudes de tooactor relacionados de contadores de rendimiento.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Actor de Service Fabric |Número de solicitudes pendientes |Número de solicitudes que se procesan en el servicio de Hola |
| Actor de Service Fabric |Promedio de milisegundos por solicitud |Tiempo que demora (en milisegundos) Hola servicio tooprocess una solicitud |
| Actor de Service Fabric |Promedio de milisegundos para la deserialización de una solicitud |Mensaje de solicitud de actor de tiempo toodeserialize tomada (en milisegundos) cuando se recibe en el servicio de Hola |
| Actor de Service Fabric |Promedio de milisegundos para la deserialización de una respuesta |Mensaje de respuesta de tiempo tooserialize tomada (en milisegundos) Hola actor en servicio de hello antes de enviar respuesta hello toohello cliente |

## <a name="next-steps"></a>Pasos siguientes
* [Uso de Reliable Actors plataforma Service Fabric de Hola](service-fabric-reliable-actors-platform.md)
* [Documentación de referencia de la API de actor](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de ejemplo](https://github.com/Azure/servicefabric-samples)
* [Proveedores de EventSource en PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
