---
title: "¿aaaWhat es el programador de Azure? | Microsoft Docs"
description: "El programador de Azure le permite toodeclaratively describen toorun de acciones en la nube de Hola. A continuación, programa y ejecuta esas acciones de forma automática."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="69406-105">¿Qué es el Programador de Azure?</span><span class="sxs-lookup"><span data-stu-id="69406-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="69406-106">El programador de Azure le permite toodeclaratively describen toorun de acciones en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="69406-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="69406-107">A continuación, programa y ejecuta esas acciones de forma automática.</span><span class="sxs-lookup"><span data-stu-id="69406-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="69406-108">Programador lo hace al utilizar [Hola portal de Azure](scheduler-get-started-portal.md), código, [API de REST](https://msdn.microsoft.com/library/mt629143.aspx), o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69406-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="69406-109">El Programador crea, mantiene e invoca el trabajo programado.</span><span class="sxs-lookup"><span data-stu-id="69406-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="69406-110">El Programador no hospeda ninguna carga de trabajo ni ejecuta código.</span><span class="sxs-lookup"><span data-stu-id="69406-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="69406-111">Solo *invoca* código hospedado en cualquier otro lugar (en Azure, localmente o con otro proveedor).</span><span class="sxs-lookup"><span data-stu-id="69406-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="69406-112">Realiza la invocación mediante HTTP, HTTPS, una cola de almacenamiento, una cola de bus de servicio o un tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="69406-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="69406-113">Programaciones de programador [trabajos](scheduler-concepts-terms.md), mantiene un historial de resultados de la ejecución de trabajo que uno puede revisar y ejecutar la toobe de las cargas de trabajo de programaciones determinista y confiable.</span><span class="sxs-lookup"><span data-stu-id="69406-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="69406-114">WebJobs de Azure (parte de la característica de las aplicaciones Web de hello en el servicio de aplicación de Azure) y otras capacidades de programación Azure utilizan el programador en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="69406-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="69406-115">Hola [API de REST de Scheduler](https://msdn.microsoft.com/library/mt629143.aspx) le ayuda a administrar las comunicaciones de Hola de estas acciones.</span><span class="sxs-lookup"><span data-stu-id="69406-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="69406-116">De ese modo, el Programador admite [programaciones complejas y periodicidad avanzada](scheduler-advanced-complexity.md) con facilidad.</span><span class="sxs-lookup"><span data-stu-id="69406-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="69406-117">Hay varios escenarios que se prestan toohello uso del programador.</span><span class="sxs-lookup"><span data-stu-id="69406-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="69406-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69406-118">For example:</span></span>

* <span data-ttu-id="69406-119">*Acciones de aplicaciones recurrentes*: recopilación periódica de datos desde Twitter en una fuente.</span><span class="sxs-lookup"><span data-stu-id="69406-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="69406-120">*Mantenimiento diario*: eliminación diaria de registros, realización de copias de seguridad y otras tareas de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="69406-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="69406-121">Por ejemplo, un administrador puede elegir tooback la base de datos de Hola a la 1:00 A.M.</span><span class="sxs-lookup"><span data-stu-id="69406-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="69406-122">todos los días para hello en los próximos meses nueve.</span><span class="sxs-lookup"><span data-stu-id="69406-122">every day for hello next nine months.</span></span>

<span data-ttu-id="69406-123">Programador permite toocreate, actualizar, eliminar, ver y administrar trabajos y [las colecciones de trabajos](scheduler-concepts-terms.md) mediante programación, mediante el uso de scripts y en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="69406-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="69406-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="69406-124">See also</span></span>
 [<span data-ttu-id="69406-125">Conceptos, terminología y jerarquía de entidades de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="69406-126">Empezar a usar a Scheduler en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="69406-127">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="69406-128">¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="69406-129">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="69406-130">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="69406-131">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="69406-132">Límites, valores predeterminados y códigos de error de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="69406-133">Autenticación de salida de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="69406-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

