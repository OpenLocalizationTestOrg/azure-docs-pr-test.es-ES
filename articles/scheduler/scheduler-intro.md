---
title: "¿Qué es el Programador de Azure? | Microsoft Docs"
description: "Programador de Azure le permite describir mediante declaración las acciones para ejecutar en la nube. A continuación, programa y ejecuta esas acciones de forma automática."
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
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="70f40-105">¿Qué es el Programador de Azure?</span><span class="sxs-lookup"><span data-stu-id="70f40-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="70f40-106">Programador de Azure le permite describir mediante declaración las acciones para ejecutar en la nube.</span><span class="sxs-lookup"><span data-stu-id="70f40-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span></span> <span data-ttu-id="70f40-107">A continuación, programa y ejecuta esas acciones de forma automática.</span><span class="sxs-lookup"><span data-stu-id="70f40-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="70f40-108">Para hacerlo, Programador usa [Azure Portal](scheduler-get-started-portal.md), código, [API de REST](https://msdn.microsoft.com/library/mt629143.aspx) o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70f40-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="70f40-109">El Programador crea, mantiene e invoca el trabajo programado.</span><span class="sxs-lookup"><span data-stu-id="70f40-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="70f40-110">El Programador no hospeda ninguna carga de trabajo ni ejecuta código.</span><span class="sxs-lookup"><span data-stu-id="70f40-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="70f40-111">Solo *invoca* código hospedado en cualquier otro lugar (en Azure, localmente o con otro proveedor).</span><span class="sxs-lookup"><span data-stu-id="70f40-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="70f40-112">Realiza la invocación mediante HTTP, HTTPS, una cola de almacenamiento, una cola de bus de servicio o un tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="70f40-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="70f40-113">El Programador programa [trabajos](scheduler-concepts-terms.md), mantiene un historial de los resultados de la ejecución de trabajos que se puede consultar y programa, de manera determinante y confiable, las cargas de trabajo que se ejecutarán.</span><span class="sxs-lookup"><span data-stu-id="70f40-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span></span> <span data-ttu-id="70f40-114">Azure WebJobs (parte de la característica de Aplicaciones web del Servicio de aplicaciones de Azure) y otras funcionalidades de programación de Azure usan el Programador en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="70f40-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span></span> <span data-ttu-id="70f40-115">La [API de REST de Programador](https://msdn.microsoft.com/library/mt629143.aspx) ayuda a administrar la comunicación para estas acciones.</span><span class="sxs-lookup"><span data-stu-id="70f40-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span></span> <span data-ttu-id="70f40-116">De ese modo, el Programador admite [programaciones complejas y periodicidad avanzada](scheduler-advanced-complexity.md) con facilidad.</span><span class="sxs-lookup"><span data-stu-id="70f40-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="70f40-117">Existen varios escenarios que se prestan para el uso del Programador.</span><span class="sxs-lookup"><span data-stu-id="70f40-117">There are several scenarios that lend themselves to the usage of Scheduler.</span></span> <span data-ttu-id="70f40-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="70f40-118">For example:</span></span>

* <span data-ttu-id="70f40-119">*Acciones de aplicaciones recurrentes*: recopilación periódica de datos desde Twitter en una fuente.</span><span class="sxs-lookup"><span data-stu-id="70f40-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="70f40-120">*Mantenimiento diario*: eliminación diaria de registros, realización de copias de seguridad y otras tareas de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="70f40-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="70f40-121">Por ejemplo, un administrador puede optar por hacer una copia de seguridad de su base de datos a la 1:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="70f40-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span></span> <span data-ttu-id="70f40-122">todos los días durante los próximos 9 meses.</span><span class="sxs-lookup"><span data-stu-id="70f40-122">every day for the next nine months.</span></span>

<span data-ttu-id="70f40-123">Programador permite crear, actualizar, eliminar, ver y administrar [colecciones de trabajos y trabajos](scheduler-concepts-terms.md) de manera programática, mediante scripts y en el portal.</span><span class="sxs-lookup"><span data-stu-id="70f40-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="70f40-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="70f40-124">See also</span></span>
 [<span data-ttu-id="70f40-125">Conceptos, terminología y jerarquía de entidades de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="70f40-126">Introducción al Programador de Azure en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-126">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="70f40-127">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="70f40-128">Creación de programaciones complejas y periodicidad avanzada con Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="70f40-129">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="70f40-130">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="70f40-131">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="70f40-132">Límites, valores predeterminados y códigos de error de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="70f40-133">Autenticación de salida de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="70f40-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

