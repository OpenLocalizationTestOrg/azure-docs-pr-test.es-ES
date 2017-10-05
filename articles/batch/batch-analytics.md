---
title: Azure Batch Analytics | Microsoft Docs
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
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="f63bd-103">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="f63bd-103">Batch Analytics</span></span>
<span data-ttu-id="f63bd-104">Los temas de análisis por lotes contienen información de referencia para los eventos y las alertas disponibles para los recursos del servicio de Batch.</span><span class="sxs-lookup"><span data-stu-id="f63bd-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="f63bd-105">Vea [Registro de diagnóstico de Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) para obtener más información sobre cómo habilitar y consumir los registros de diagnóstico por lotes.</span><span class="sxs-lookup"><span data-stu-id="f63bd-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="f63bd-106">Registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="f63bd-106">Diagnostic logs</span></span>

<span data-ttu-id="f63bd-107">El servicio de Azure Batch genera los siguientes eventos de registro de diagnóstico mientras duren determinados recursos de Batch.</span><span class="sxs-lookup"><span data-stu-id="f63bd-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="f63bd-108">**Eventos del registro del servicio**</span><span class="sxs-lookup"><span data-stu-id="f63bd-108">**Service Log events**</span></span>
* [<span data-ttu-id="f63bd-109">Creación del grupo</span><span class="sxs-lookup"><span data-stu-id="f63bd-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="f63bd-110">Inicio de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="f63bd-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="f63bd-111">Finalización de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="f63bd-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="f63bd-112">Inicio de cambio de tamaño del grupo</span><span class="sxs-lookup"><span data-stu-id="f63bd-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="f63bd-113">Finalización de cambio de tamaño del grupo</span><span class="sxs-lookup"><span data-stu-id="f63bd-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="f63bd-114">Inicio de tarea</span><span class="sxs-lookup"><span data-stu-id="f63bd-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="f63bd-115">Finalización de tarea</span><span class="sxs-lookup"><span data-stu-id="f63bd-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="f63bd-116">Error en la tarea</span><span class="sxs-lookup"><span data-stu-id="f63bd-116">Task fail</span></span>](batch-task-fail-event.md)