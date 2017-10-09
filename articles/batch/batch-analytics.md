---
title: "aaaAzure análisis por lotes | Documentos de Microsoft"
description: Referencia de Azure Batch Analytics.
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
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="a32ff-103">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="a32ff-103">Batch Analytics</span></span>
<span data-ttu-id="a32ff-104">temas de Hello en el análisis por lotes contienen información de referencia de eventos de Hola y alertas disponibles para los recursos del servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="a32ff-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="a32ff-105">Vea [Registro de diagnóstico de Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) para obtener más información sobre cómo habilitar y consumir los registros de diagnóstico por lotes.</span><span class="sxs-lookup"><span data-stu-id="a32ff-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="a32ff-106">Registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="a32ff-106">Diagnostic logs</span></span>

<span data-ttu-id="a32ff-107">Hola servicio Azure Batch emite Hola después de los eventos de registro de diagnóstico durante la duración de Hola de determinados recursos de proceso por lotes.</span><span class="sxs-lookup"><span data-stu-id="a32ff-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="a32ff-108">**Eventos del registro del servicio**</span><span class="sxs-lookup"><span data-stu-id="a32ff-108">**Service Log events**</span></span>
* [<span data-ttu-id="a32ff-109">Creación del grupo</span><span class="sxs-lookup"><span data-stu-id="a32ff-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="a32ff-110">Inicio de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="a32ff-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="a32ff-111">Finalización de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="a32ff-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="a32ff-112">Inicio de cambio de tamaño del grupo</span><span class="sxs-lookup"><span data-stu-id="a32ff-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="a32ff-113">Finalización de cambio de tamaño del grupo</span><span class="sxs-lookup"><span data-stu-id="a32ff-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="a32ff-114">Inicio de tarea</span><span class="sxs-lookup"><span data-stu-id="a32ff-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="a32ff-115">Finalización de tarea</span><span class="sxs-lookup"><span data-stu-id="a32ff-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="a32ff-116">Error en la tarea</span><span class="sxs-lookup"><span data-stu-id="a32ff-116">Task fail</span></span>](batch-task-fail-event.md)