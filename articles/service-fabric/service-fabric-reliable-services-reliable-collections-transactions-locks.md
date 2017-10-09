---
title: aaaTransactions y modos de bloqueo en Azure Service Fabric confiable colecciones | Documentos de Microsoft
description: Transacciones y registros de Reliable State Manager y Reliable Collections de Azure Service Fabric.
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Transacciones y modos de bloqueo en Reliable Collections de Azure Service Fabric

## <a name="transaction"></a>Transacción
Una transacción es una secuencia de operaciones realizadas como una única unidad lógica de trabajo.
Una transacción debe exhibir Hola siguiendo las propiedades ACID. (consulte: https://technet.microsoft.com/en-us/library/ms190612)
* **Atomicidad**: una transacción debe ser una unidad atómica de trabajo. Es decir, o se modifican todos sus datos o ninguno de ellos.
* **Coherencia**: cuando ha finalizado, una transacción debe dejar todos los datos en un estado coherente. Todas las estructuras de datos internos deben estar correctas al final de Hola de transacción de Hola.
* **Aislamiento**: las modificaciones realizadas por transacciones simultáneas se deben aisladas de las modificaciones de hello realizadas por otras transacciones simultáneas. nivel de aislamiento de Hello usado para una operación dentro de un ITransaction se determina por hello IReliableState realizar operación de Hola.
* **Durabilidad**: una vez concluida una transacción, sus efectos son permanentes en su lugar en el sistema de Hola. modificaciones de Hello persisten incluso en caso de hello de un error del sistema.

### <a name="isolation-levels"></a>Niveles de aislamiento
Nivel de aislamiento define el grado de hello transacciones de hello toowhich deben estar aislado de las modificaciones realizadas por otras transacciones.
Hay dos niveles de aislamiento que se admiten en Colecciones confiables:

* **Lectura repetible**: Especifica que las instrucciones no pueden leer datos que hayan sido modificados, pero aún no confirmados por otras transacciones y que ninguna otra transacción puede modificar los datos que ha sido leídos por la transacción actual de hello hasta Hola actual finaliza la transacción. Para obtener más información, consulte [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Instantánea**: Especifica que los datos leídos por cualquier instrucción de una transacción están la versión transaccionalmente coherente de Hola de datos de Hola existentes al comienzo de Hola de transacción de Hola.
  transacción de Hello puede reconocer sólo las modificaciones de datos que se confirmaron antes del inicio de Hola de transacción de Hola.
  Modificaciones de datos realizadas por otras transacciones después de hello principio de la transacción actual de hello no son toostatements visible ejecutando en Hola de transacción actual.
  efecto de Hello es como si instrucciones de hello en una transacción obtuviesen una instantánea de datos de hello confirmada tal y como se encontraban al inicio de Hola de transacción de Hola.
  Las instantáneas son coherentes entre colecciones confiables.
  Para obtener más información, consulte [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Colecciones confiables automáticamente elija toouse de nivel de aislamiento de Hola para una operación de lectura determinada según operación hello y la función de Hola de réplica de hello en tiempo de presentación de la creación de la transacción.
Aquí te mostramos tabla Hola que describe los valores predeterminados de nivel de aislamiento para las operaciones de diccionario confiable y cola.

| Operación\rol | Principal | Secundario |
| --- |:--- |:--- |
| Lectura de una sola entidad |Repeatable Read |Instantánea |
| Enumeración, recuento |Instantánea |Instantánea |

> [!NOTE]
> Algunos ejemplos comunes de las operaciones de entidad única son `IReliableDictionary.TryGetValueAsync` y `IReliableQueue.TryPeekAsync`.
> 

Hola diccionario confiable y Hola cola confiable admiten lectura la escribe.
En otras palabras, cualquier escritura dentro de una transacción tooa visible siguiente leerá que pertenece toohello misma transacción.

## <a name="locks"></a>Bloqueos
En colecciones de confianza, implemente de todas las transacciones rigurosas de dos fase bloqueo: una transacción no liberar los bloqueos de hello ha adquirido hasta que la transacción de hello finaliza con una anulación o una confirmación.

Diccionario confiable utiliza el bloqueo de nivel de fila en todas las operaciones de entidad única.
Cola confiable equilibra la simultaneidad para la propiedad FIFO transaccional estricta.
Cola confiable utiliza bloqueos de nivel de operación que permite una transacción con `TryPeekAsync` o `TryDequeueAsync` y una transacción con `EnqueueAsync` a la vez.
Tenga en cuenta que toopreserve FIFO, si un `TryPeekAsync` o `TryDequeueAsync` alguna vez observa que Hola cola confiable está vacía, también bloqueará `EnqueueAsync`.

Las operaciones de escritura siempre tiene bloqueos exclusivos.
Para las operaciones de lectura, bloqueo de hello depende de un par de factores.
Cualquier operación de lectura realizada mediante aislamiento Snapshot no presenta bloqueo.
Cualquier operación Repeatable Read usa bloqueos compartidos de manera predeterminada.
Sin embargo, para cualquier operación de lectura que admite lectura repetible, usuario Hola puede solicitar un bloqueo de actualización en lugar de hello bloqueo compartido.
Un bloqueo de actualización es que un bloqueo asimétrico usa tooprevent una forma común de interbloqueo que se produce cuando varias transacciones bloquean recursos para las posibles actualizaciones en un momento posterior.

matriz de compatibilidad de bloqueos de Hello puede encontrarse en hello en la tabla siguiente:

| Solicitar \ concedido | None | Compartido | Actualizar | Exclusivo |
| --- |:--- |:--- |:--- |:--- |
| Compartido |Ningún conflicto |Ningún conflicto |Conflicto |Conflicto |
| Actualizar |Ningún conflicto |Ningún conflicto |Conflicto |Conflicto |
| Exclusivo |Ningún conflicto |Conflicto |Conflicto |Conflicto |

Argumento de tiempo de espera de hello confiable de las API de colecciones se utiliza la detección de interbloqueos.
Por ejemplo, dos transacciones (T1 y T2) están tratando de tooread y actualización K1.
Es posible que ellos toodeadlock, porque ambos acaban por tener Hola compartido bloqueo.
En este caso, una o ambas de las operaciones de hello agotará el tiempo.

Esta situación de interbloqueo es un buen ejemplo de cómo puede el bloqueo de actualización impedir interbloqueos.

## <a name="next-steps"></a>Pasos siguientes
* [Trabajo con Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notificaciones de Reliable Services](service-fabric-reliable-services-notifications.md)
* [Copia de seguridad y restauración de Reliable Services (recuperación ante desastres)](service-fabric-reliable-services-backup-restore.md)
* [Configuración del administrador de estado confiable](service-fabric-reliable-services-configuration.md)
* [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

