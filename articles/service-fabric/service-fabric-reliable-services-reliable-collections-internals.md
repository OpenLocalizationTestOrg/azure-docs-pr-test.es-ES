---
title: "aaaAzure elementos internos de Service Fabric Manager confiable de estado y recopilación confiable | Documentos de Microsoft"
description: "Profundización en los conceptos y el diseño de Reliable Collection en Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Aspectos internos de Reliable State Manager y Reliable Collection de Azure Service Fabric
Este documento profundiza en el Administrador de estado confiable y colecciones confiable toosee cómo funcionan los componentes principales entre bastidores de Hola.

> [!NOTE]
> Este documento está en proceso de elaboración. Agregar comentarios toothis artículo tootell nos qué tema desea más información acerca de toolearn.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Modelo de persistencia local: registro y punto de comprobación
Hola, Administrador de estado confiable y colecciones confiable siguen un modelo de persistencia que se denomina punto de comprobación y de registro.
En este modelo, cada cambio de estado se registra primero en el disco y, a continuación, se aplica en memoria.
Hola completa sí se conserva el estado solo ocasionalmente (conocido como) Punto de comprobación).
ventaja de Hello es que deltas se convierten en Sólo anexar las escrituras secuenciales en disco para mejorar el rendimiento.

toobetter comprender Hola registro y el modelo de punto de comprobación, echemos un vistazo primero a un escenario de disco infinito Hola.
Hola, Administrador de estado confiable registra cada operación antes de que se replique.
El registro permite Hola colecciones confiable tooapply Hola únicamente en la memoria.
Puesto que los registros se conservan, incluso cuando réplica Hola se produce un error y necesita toobe reinicia, Hola confiable Administrador de estado tiene suficiente información en su tooreplay registro todas las operaciones de hello ha perdido la réplica de Hola.
Como disco de hello es infinito, entradas de registro nunca necesitan toobe quitado y colección confiable hello debe estado de toomanage solo hello en memoria.

Ahora Echemos un vistazo a un escenario de disco finito Hola.
Tal y como se acumulan entradas del registro, Hola confiable Administrador de estados se quedará sin espacio en disco.
Antes de que tenga lugar, Hola confiable Administrador de Estados debe tootruncate su espacio de toomake de registro para los registros más recientes de Hola.
Las solicitudes del Administrador de estado de confianza Hola colecciones confiable toocheckpoint su toodisk de estado en memoria.
En este momento, hello' colecciones confiable podría conservar su estado en memoria.
Una vez Hola confiable colecciones complete sus puntos de control, Hola confiable Administrador de estados puede truncar Hola registro toofree espacio en disco.
Cuando réplica Hola necesita toobe reinicia, colecciones confiable recuperar su estado de punto de comprobación y recupera hello el Administrador de estado confiable y reproduce todos los cambios de estado de hello producidos desde el último punto de comprobación de Hola.

Otro valor de agregar puntos de comprobación es que mejora los tiempos de recuperación en escenarios comunes. Registro contiene todas las operaciones que se han producido desde el último punto de comprobación Hola.
Así que puede incluir varias versiones de un elemento, como varios valores para una fila determinada en Reliable Dictionary.
En cambio, los puntos de control de una colección confiable Hola solo la versión más reciente de cada valor de una clave.

## <a name="next-steps"></a>Pasos siguientes
* [Transacciones y bloqueos](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

