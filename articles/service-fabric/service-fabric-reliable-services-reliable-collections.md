---
title: aaaIntroduction tooReliable colecciones en servicios con estado de Azure Service Fabric | Documentos de Microsoft
description: Servicios con estado de Service Fabric proporcionan colecciones confiables que le permiten aplicaciones en la nube altamente disponible, escalable y baja latencia toowrite.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Introducción tooReliable colecciones en servicios con estado de Azure Service Fabric
Colecciones confiables le permiten aplicaciones en la nube altamente disponible, escalable y baja latencia toowrite, como si estuviera escribiendo aplicaciones de equipo único. Hola clases Hola **Microsoft.ServiceFabric.Data.Collections** espacio de nombres proporcionan un conjunto de colecciones que se realizan automáticamente el estado de la alta disponibilidad. Los desarrolladores necesitan tooprogram solo toohello confiable de las API de colección y deje que colecciones confiable a administrar Hola replica y el estado local.

Hola principal diferencia entre colecciones confiable y otras tecnologías de alta disponibilidad (por ejemplo, Redis, servicio de la tabla de Azure y el servicio de cola de Azure) es que estado Hola se guarda localmente en la instancia de servicio de hello al que se va a hacer alta disponibilidad. Esto significa que:

* Todas las lecturas son locales, lo que provoca una latencia baja y lecturas de alto rendimiento.
* Todas las escrituras acarrearán Hola un mínimo de operaciones de E/s de red, lo que da como resultado una latencia baja y alto rendimiento escribe.

![Imagen de la evolución de colecciones](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Colecciones confiables pueden considerarse como evolución natural de Hola de hello **System.Collections** clases: un nuevo conjunto de colecciones que están diseñados para aplicaciones de nube y varios equipos de hello sin aumentar la complejidad para desarrollador de Hola. De esta forma, Reliable Collections tienen los estados siguientes:

* Replicado: se replican los cambios de estado para obtener una alta disponibilidad.
* Persistente: Los datos son persistente toodisk para que la durabilidad contra interrupciones a gran escala (por ejemplo, un error de alimentación del centro de datos).
* Asincrónica: API son tooensure asincrónica que los subprocesos no se bloquean cuando incurrir en E/S.
* Transaccional: API usan abstracción Hola de transacciones para que pueda administrar fácilmente varias colecciones confiable dentro de un servicio.

Las colecciones confiables proporcionan coherencia fuerte garantiza fuera Hola cuadro toomake razonamiento sobre el estado de la aplicación sea más fácil.
Coherencia fuerte se consigue asegurándose de transacción confirmaciones fin solo después de que toda la transacción Hola se ha iniciado sesión en un quórum de mayoría de las réplicas, incluido el principal de Hola.
tooachieve coherencia más débil, las aplicaciones pueden reconocer toohello atrás cliente/solicitante antes de confirmación asincrónica Hola devuelve.

Hello confiable API de colecciones son una evolución de las API de colección simultáneas (se encuentra en hello **System.Collections.Concurrent** espacio de nombres):

* Asincrónica: Devuelve una tarea desde ese momento, a diferencia de las recolecciones simultáneas, se replican y se conservan las operaciones de Hola.
* Los parámetros out no: usa `ConditionalValue<T>` tooreturn a bool y un valor en lugar de los parámetros de salida. `ConditionalValue<T>`es similar a `Nullable<T>` , pero no requiere T toobe un struct.
* Transacciones: Usa un acciones transacciones objeto tooenable Hola usuario toogroup en varias colecciones confiable en una transacción.

Por el momento, el espacio de nombres **Microsoft.ServiceFabric.Data.Collections** contiene tres colecciones:

* [Diccionario confiable](https://msdn.microsoft.com/library/azure/dn971511.aspx): representa una colección replicada, transaccional y asincrónica de pares clave/valor. Similar demasiado**ConcurrentDictionary**, ambos Hola clave y valor de hello puede ser de cualquier tipo.
* [Cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx): representa una cola estricta replicada, transaccional y asincrónica de tipo primero en entrar primero en salir (FIFO). Similar demasiado**ConcurrentQueue**, Hola valor puede ser de cualquier tipo.
* [Cola simultánea confiable](service-fabric-reliable-services-reliable-concurrent-queue.md): representa una mejor cola de ordenación replicada, transaccional y asincrónica para obtener un alto rendimiento. Toohello similar **ConcurrentQueue**, Hola valor puede ser de cualquier tipo.

## <a name="next-steps"></a>Pasos siguientes
* [Recomendaciones y directrices de Reliable Collections](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Trabajo con Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transacciones y bloqueos](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Reliable State Manager y Reliable Collections internos](service-fabric-reliable-services-reliable-collections-internals.md)
* Administración de datos
  * [Copia de seguridad y restauración](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Serialización de colección confiable](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serialización y actualización](service-fabric-application-upgrade-data-serialization.md)
  * [Configuración del administrador de estado confiable](service-fabric-reliable-services-configuration.md)
* Otros
  * [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
  * [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
