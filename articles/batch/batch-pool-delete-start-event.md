---
title: "aaa \"evento de inicio de eliminación de grupo de lote de Azure | Documentos de Microsoft\""
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="70c96-103">Evento de inicio de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="70c96-103">Pool delete start event</span></span>

 <span data-ttu-id="70c96-104">Este evento se genera cuando se inicia una operación de eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="70c96-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="70c96-105">Puesto que la eliminación de grupo de hello es un evento asíncrono, puede esperar un toobe de evento complete de eliminación de grupo genera una vez que la operación de eliminación de hello completa.</span><span class="sxs-lookup"><span data-stu-id="70c96-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="70c96-106">Hello en el ejemplo siguiente se muestra hello cuerpo de un evento de inicio de eliminación de grupo.</span><span class="sxs-lookup"><span data-stu-id="70c96-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="70c96-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="70c96-107">Element</span></span>|<span data-ttu-id="70c96-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="70c96-108">Type</span></span>|<span data-ttu-id="70c96-109">Notas</span><span class="sxs-lookup"><span data-stu-id="70c96-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="70c96-110">id</span><span class="sxs-lookup"><span data-stu-id="70c96-110">id</span></span>|<span data-ttu-id="70c96-111">String</span><span class="sxs-lookup"><span data-stu-id="70c96-111">String</span></span>|<span data-ttu-id="70c96-112">Hola Id. de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="70c96-112">hello id of hello pool.</span></span>|
