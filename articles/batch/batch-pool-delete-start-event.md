---
title: "Evento de inicio de eliminación de grupo de Azure Batch | Microsoft Docs"
description: "Referencia del evento de inicio de eliminación de grupo de Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="7bdee-103">Evento de inicio de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="7bdee-103">Pool delete start event</span></span>

 <span data-ttu-id="7bdee-104">Este evento se genera cuando se inicia una operación de eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="7bdee-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="7bdee-105">Puesto que la eliminación de grupo es un evento asincrónico, puede esperar que se genere un evento completo de eliminación del grupo cuando se haya completado la operación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="7bdee-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="7bdee-106">En el siguiente ejemplo, se muestra el cuerpo de un evento de inicio de eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="7bdee-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="7bdee-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="7bdee-107">Element</span></span>|<span data-ttu-id="7bdee-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="7bdee-108">Type</span></span>|<span data-ttu-id="7bdee-109">Notas</span><span class="sxs-lookup"><span data-stu-id="7bdee-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="7bdee-110">id</span><span class="sxs-lookup"><span data-stu-id="7bdee-110">id</span></span>|<span data-ttu-id="7bdee-111">String</span><span class="sxs-lookup"><span data-stu-id="7bdee-111">String</span></span>|<span data-ttu-id="7bdee-112">El identificador del grupo.</span><span class="sxs-lookup"><span data-stu-id="7bdee-112">The id of the pool.</span></span>|