---
title: Aspectos internos de Reliable State Manager y Reliable Collection de Azure Service Fabric | Microsoft Docs
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
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="2ebd8-103">Aspectos internos de Reliable State Manager y Reliable Collection de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2ebd8-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="2ebd8-104">Este documento analiza en profundidad Reliable State Manager y Reliable Collections para ver qué se esconde detrás del funcionamiento de los componentes principales.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="2ebd8-105">Este documento está en proceso de elaboración.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-105">This document is work in-progress.</span></span> <span data-ttu-id="2ebd8-106">Agregue comentarios a este artículo para decirnos sobre qué tema le gustaría obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="2ebd8-107">Modelo de persistencia local: registro y punto de comprobación</span><span class="sxs-lookup"><span data-stu-id="2ebd8-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="2ebd8-108">Reliable State Manager y Reliable Collections siguen un modelo de persistencia que se denomina Registro y punto de control.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="2ebd8-109">En este modelo, cada cambio de estado se registra primero en el disco y, a continuación, se aplica en memoria.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="2ebd8-110">El mismo estado completo se guarda en ocasiones (también conocido como</span><span class="sxs-lookup"><span data-stu-id="2ebd8-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="2ebd8-111">Punto de comprobación).</span><span class="sxs-lookup"><span data-stu-id="2ebd8-111">Checkpoint).</span></span>
<span data-ttu-id="2ebd8-112">La ventaja que proporciona es: que los deltas se convierten en escrituras de solo anexación secuenciales en disco para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="2ebd8-113">Para comprender mejor el modelo de registro y de punto de control, primero analicemos el escenario de discos infinitos.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="2ebd8-114">Reliable State Manager registra cada operación antes de replicarse.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="2ebd8-115">El registro permite que Reliable Collections aplique la operación solo en memoria.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="2ebd8-116">Dado que los registros se conservan, incluso cuando la réplica produce error y debe reiniciarse, Reliable State Manager tiene suficiente información en sus registros para reproducir todas las operaciones que ha perdido la réplica.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="2ebd8-117">Como el disco es infinito, las entradas de registro nunca deberán quitarse y Reliable Collection solo tiene que administrar el estado en memoria.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="2ebd8-118">Ahora veamos el escenario de disco finito.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="2ebd8-119">En un determinado momento, Reliable State Manager se quedará sin espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="2ebd8-120">Antes de que suceda, Reliable State Manager debe truncar su registro para liberar espacio para los registros más recientes.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="2ebd8-121">Reliable State Manager solicita las colecciones confiables para aplicar un punto de comprobación a su estado en memoria en el disco.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="2ebd8-122">En este momento, las colecciones confiables conservarían su estado en memoria.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="2ebd8-123">Una vez que las colecciones fiables completen sus puntos de control, el administrador de estado fiable puede truncar el registro para liberar espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="2ebd8-124">Cuando la réplica debe reiniciarse, Reliable Collections recuperará su estado de punto de comprobación y Reliable State Manager recupera y reproduce todos los cambios de estado que se han producido desde el último punto de control.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="2ebd8-125">Otro valor de agregar puntos de comprobación es que mejora los tiempos de recuperación en escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="2ebd8-126">El registro contiene todas las operaciones que se han producido desde el último punto de comprobación.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="2ebd8-127">Así que puede incluir varias versiones de un elemento, como varios valores para una fila determinada en Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="2ebd8-128">En cambio, Reliable Collections solo aplica puntos de comprobación a la última versión de cada valor de una clave.</span><span class="sxs-lookup"><span data-stu-id="2ebd8-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ebd8-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ebd8-129">Next steps</span></span>
* [<span data-ttu-id="2ebd8-130">Transacciones y bloqueos</span><span class="sxs-lookup"><span data-stu-id="2ebd8-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

