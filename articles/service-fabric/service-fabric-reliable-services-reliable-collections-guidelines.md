---
title: aaaGuidelines & recomendaciones para las colecciones confiable en Azure Service Fabric | Documentos de Microsoft
description: Directrices y recomendaciones para el uso de Reliable Collections de Service Fabric
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Directrices y recomendaciones de Reliable Collections en Azure Service Fabric
Esta sección proporciona directrices para el uso de Reliable State Manager y Reliable Collections. objetivo de Hello es toohelp a los usuarios evitar los errores comunes.

directrices de Hola se organizan como recomendaciones sencillas precedidas con términos de hello *hacer*, *considere la posibilidad de*, *evitar* y *no*.

* No modifique un objeto de tipo personalizado que hayan devuelto las operaciones de lectura (por ejemplo, `TryPeekAsync` o `TryGetValueAsync`). Las colecciones de confianza, al igual que las recolecciones simultáneas, devolución un objeto de toohello de referencia y no una copia.
* Hacer Hola de copia en profundidad devuelve el objeto de un tipo personalizado antes de modificarla. Puesto que las estructuras y los tipos integrados son pasada por valor, no es necesario toodo una copia en profundidad en ellos.
* No use `TimeSpan.MaxValue` para tiempos de espera. Los tiempos de espera deben ser usado toodetect interbloqueos.
* No utilice una transacción una vez que se haya confirmado, anulado o eliminado.
* No utilice una enumeración fuera del ámbito de transacción de Hola que se creó.
* No cree una transacción dentro de la instrucción `using` de otra transacción, ya que puede provocar interbloqueos.
* Asegúrese de que la implementación de `IComparable<TKey>` es correcta. sistema de Hello tiene dependencia en `IComparable<TKey>` para combinar los puntos de control y de filas.
* Utilice el bloqueo de actualización al leer un elemento con un tooupdate intención se tooprevent una clase determinada de interbloqueos.
* Considere la posibilidad de mantener los elementos (por ejemplo, TKey + TValue para diccionario confiable) por debajo de 80 KBytes: Hola menor mejor. Esto reduce la cantidad de Hola de los requisitos de E/S de red, así como disco y uso de montón de objetos grandes. A menudo, reduce replicar datos duplicados cuando se actualiza solo una pequeña parte del valor de Hola. Tooachieve comunes de manera confiable diccionario, se trata de toobreak sus filas en toomultiple filas.
* Considere el uso de copia de seguridad y restauración de recuperación ante desastres de funcionalidad toohave.
* Evite mezclar operaciones de varias entidades y operaciones de entidad única (por ejemplo `GetCountAsync`, `CreateEnumerableAsync`) en hello vencimiento toohello distintos niveles de aislamiento de la transacción misma.
* Controle la excepción InvalidOperationException. Las transacciones de usuario pueden anularse por sistema de Hola para diversos motivos. Por ejemplo, cuando cambia su rol de principal Hola el Administrador de estado confiable o cuando una transacción de larga duración está bloqueando el truncamiento del registro transaccional de Hola de. En tales casos, el usuario puede recibir la excepción InvalidOperationException, que indica que ya ha finalizado su transacción. Suponiendo que, terminación Hola de transacción de Hola no se ha solicitado por el usuario de Hola, mejor toohandle de manera esta excepción es la transacción de hello toodispose, compruebe si se ha señalado el token de cancelación de hello (o se ha cambiado el rol de Hola de réplica de hello) y si no crear una nueva transacción y vuelva a intentarlo.  

Estas son algunas cosas tookeep en cuenta:

* tiempo de espera de Hello predeterminado es cuatro segundos para hello todas las API de colección confiable. La mayoría de los usuarios deben utilizar el tiempo de espera de hello predeterminado.
* Hola token de cancelación predeterminado es `CancellationToken.None` en todas las API de colecciones confiable.
* Hola de parámetro de tipo de clave (*TKey*) para un diccionario confiable correctamente debe implementar `GetHashCode()` y `Equals()`. Las claves deben ser inmutables.
* tooachieve alta disponibilidad para hello colecciones confiable, cada servicio debe tener al menos un destino y la réplica mínimo establecer tamaño de 3.
* Las operaciones de lectura en hello secundaria pueden leer las versiones que no están confirmada de quórum.
  Esto significa que una versión de datos leída desde una única base de datos secundaria podría progresar como false.
  Las lecturas de la base de datos principal siempre son estables, es decir, que nunca pueden progresar como false.

### <a name="next-steps"></a>Pasos siguientes
* [Trabajo con Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transacciones y bloqueos](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Reliable State Manager y Reliable Collections internos](service-fabric-reliable-services-reliable-collections-internals.md)
* Administración de datos
  * [Copia de seguridad y restauración](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Serialización y actualización](service-fabric-application-upgrade-data-serialization.md)
  * [Configuración del administrador de estado confiable](service-fabric-reliable-services-configuration.md)
* Otros
  * [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
  * [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
