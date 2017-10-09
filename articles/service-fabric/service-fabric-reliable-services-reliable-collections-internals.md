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
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="07cfe-103">Aspectos internos de Reliable State Manager y Reliable Collection de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07cfe-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="07cfe-104">Este documento profundiza en el Administrador de estado confiable y colecciones confiable toosee cómo funcionan los componentes principales entre bastidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="07cfe-105">Este documento está en proceso de elaboración.</span><span class="sxs-lookup"><span data-stu-id="07cfe-105">This document is work in-progress.</span></span> <span data-ttu-id="07cfe-106">Agregar comentarios toothis artículo tootell nos qué tema desea más información acerca de toolearn.</span><span class="sxs-lookup"><span data-stu-id="07cfe-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="07cfe-107">Modelo de persistencia local: registro y punto de comprobación</span><span class="sxs-lookup"><span data-stu-id="07cfe-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="07cfe-108">Hola, Administrador de estado confiable y colecciones confiable siguen un modelo de persistencia que se denomina punto de comprobación y de registro.</span><span class="sxs-lookup"><span data-stu-id="07cfe-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="07cfe-109">En este modelo, cada cambio de estado se registra primero en el disco y, a continuación, se aplica en memoria.</span><span class="sxs-lookup"><span data-stu-id="07cfe-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="07cfe-110">Hola completa sí se conserva el estado solo ocasionalmente (conocido como)</span><span class="sxs-lookup"><span data-stu-id="07cfe-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="07cfe-111">Punto de comprobación).</span><span class="sxs-lookup"><span data-stu-id="07cfe-111">Checkpoint).</span></span>
<span data-ttu-id="07cfe-112">ventaja de Hello es que deltas se convierten en Sólo anexar las escrituras secuenciales en disco para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="07cfe-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="07cfe-113">toobetter comprender Hola registro y el modelo de punto de comprobación, echemos un vistazo primero a un escenario de disco infinito Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="07cfe-114">Hola, Administrador de estado confiable registra cada operación antes de que se replique.</span><span class="sxs-lookup"><span data-stu-id="07cfe-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="07cfe-115">El registro permite Hola colecciones confiable tooapply Hola únicamente en la memoria.</span><span class="sxs-lookup"><span data-stu-id="07cfe-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="07cfe-116">Puesto que los registros se conservan, incluso cuando réplica Hola se produce un error y necesita toobe reinicia, Hola confiable Administrador de estado tiene suficiente información en su tooreplay registro todas las operaciones de hello ha perdido la réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="07cfe-117">Como disco de hello es infinito, entradas de registro nunca necesitan toobe quitado y colección confiable hello debe estado de toomanage solo hello en memoria.</span><span class="sxs-lookup"><span data-stu-id="07cfe-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="07cfe-118">Ahora Echemos un vistazo a un escenario de disco finito Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="07cfe-119">Tal y como se acumulan entradas del registro, Hola confiable Administrador de estados se quedará sin espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="07cfe-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="07cfe-120">Antes de que tenga lugar, Hola confiable Administrador de Estados debe tootruncate su espacio de toomake de registro para los registros más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="07cfe-121">Las solicitudes del Administrador de estado de confianza Hola colecciones confiable toocheckpoint su toodisk de estado en memoria.</span><span class="sxs-lookup"><span data-stu-id="07cfe-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="07cfe-122">En este momento, hello' colecciones confiable podría conservar su estado en memoria.</span><span class="sxs-lookup"><span data-stu-id="07cfe-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="07cfe-123">Una vez Hola confiable colecciones complete sus puntos de control, Hola confiable Administrador de estados puede truncar Hola registro toofree espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="07cfe-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="07cfe-124">Cuando réplica Hola necesita toobe reinicia, colecciones confiable recuperar su estado de punto de comprobación y recupera hello el Administrador de estado confiable y reproduce todos los cambios de estado de hello producidos desde el último punto de comprobación de Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="07cfe-125">Otro valor de agregar puntos de comprobación es que mejora los tiempos de recuperación en escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="07cfe-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="07cfe-126">Registro contiene todas las operaciones que se han producido desde el último punto de comprobación Hola.</span><span class="sxs-lookup"><span data-stu-id="07cfe-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="07cfe-127">Así que puede incluir varias versiones de un elemento, como varios valores para una fila determinada en Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="07cfe-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="07cfe-128">En cambio, los puntos de control de una colección confiable Hola solo la versión más reciente de cada valor de una clave.</span><span class="sxs-lookup"><span data-stu-id="07cfe-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07cfe-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07cfe-129">Next steps</span></span>
* [<span data-ttu-id="07cfe-130">Transacciones y bloqueos</span><span class="sxs-lookup"><span data-stu-id="07cfe-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

