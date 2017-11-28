---
title: "Información sobre la limitación en BizTalk Services | Microsoft Docs"
description: "Obtenga información acerca de los umbrales de limitación y comportamientos en tiempo de ejecución resultantes para los Servicios de BizTalk. La limitación se basa en el uso de la memoria y el número de mensajes. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="eb660-105">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="eb660-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="eb660-106">Los servicios de BizTalk de Azure implementan limitaciones del servicio según dos condiciones: uso de memoria y el número de mensajes simultáneos que se procesan.</span><span class="sxs-lookup"><span data-stu-id="eb660-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="eb660-107">En este tema se enumeran los umbrales de limitación y se describe el comportamiento del tiempo de ejecución cuando se produce una condición de limitación.</span><span class="sxs-lookup"><span data-stu-id="eb660-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="eb660-108">Umbrales de limitación</span><span class="sxs-lookup"><span data-stu-id="eb660-108">Throttling Thresholds</span></span>
<span data-ttu-id="eb660-109">La siguiente tabla muestra los orígenes y umbrales de limitación:</span><span class="sxs-lookup"><span data-stu-id="eb660-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="eb660-110">Description</span><span class="sxs-lookup"><span data-stu-id="eb660-110">Description</span></span> | <span data-ttu-id="eb660-111">Umbral bajo</span><span class="sxs-lookup"><span data-stu-id="eb660-111">Low Threshold</span></span> | <span data-ttu-id="eb660-112">Umbral alto</span><span class="sxs-lookup"><span data-stu-id="eb660-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eb660-113">Memoria</span><span class="sxs-lookup"><span data-stu-id="eb660-113">Memory</span></span> |<span data-ttu-id="eb660-114">% de memoria total del sistema disponible/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="eb660-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="eb660-115">La cantidad total disponible de PageFileBytes es de aproximadamente 2 veces la memoria RAM del sistema.</span><span class="sxs-lookup"><span data-stu-id="eb660-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="eb660-116">60%</span><span class="sxs-lookup"><span data-stu-id="eb660-116">60%</span></span> |<span data-ttu-id="eb660-117">70%</span><span class="sxs-lookup"><span data-stu-id="eb660-117">70%</span></span> |
| <span data-ttu-id="eb660-118">Procesamiento de mensajes</span><span class="sxs-lookup"><span data-stu-id="eb660-118">Message Processing</span></span> |<span data-ttu-id="eb660-119">Número de mensajes que se procesan simultáneamente</span><span class="sxs-lookup"><span data-stu-id="eb660-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="eb660-120">40 * número de núcleos</span><span class="sxs-lookup"><span data-stu-id="eb660-120">40 * number of cores</span></span> |<span data-ttu-id="eb660-121">100 * número de núcleos</span><span class="sxs-lookup"><span data-stu-id="eb660-121">100 * number of cores</span></span> |

<span data-ttu-id="eb660-122">Cuando se alcanza un umbral alto, Servicios de BizTalk de Azure empieza a limitarse.</span><span class="sxs-lookup"><span data-stu-id="eb660-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="eb660-123">La limitación se detiene cuando se alcanza el umbral bajo.</span><span class="sxs-lookup"><span data-stu-id="eb660-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="eb660-124">Por ejemplo, el servicio está utilizando un 65 % de la memoria del sistema.</span><span class="sxs-lookup"><span data-stu-id="eb660-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="eb660-125">En esta situación, el servicio no se limita.</span><span class="sxs-lookup"><span data-stu-id="eb660-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="eb660-126">El servicio empieza a usar un 70 % de la memoria del sistema.</span><span class="sxs-lookup"><span data-stu-id="eb660-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="eb660-127">En esta situación, el servicio se limita y sigue limitándose hasta que el servicio utiliza un 60 % de la memoria del sistema (umbral bajo).</span><span class="sxs-lookup"><span data-stu-id="eb660-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="eb660-128">Los servicios de BizTalk de Azure realizan un seguimiento del estado de las limitaciones (estado normal frente a estado limitado) y de la duración de la limitación.</span><span class="sxs-lookup"><span data-stu-id="eb660-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="eb660-129">Comportamiento del tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="eb660-129">Runtime Behavior</span></span>
<span data-ttu-id="eb660-130">Cuando los servicios de BizTalk de Azure entran en un estado de limitación, ocurre lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eb660-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="eb660-131">La limitación es por instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="eb660-131">Throttling is per role instance.</span></span> <span data-ttu-id="eb660-132">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eb660-132">For example:</span></span><br/>
  <span data-ttu-id="eb660-133">RoleInstanceA se está limitando.</span><span class="sxs-lookup"><span data-stu-id="eb660-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="eb660-134">RoleInstanceB no se está limitando.</span><span class="sxs-lookup"><span data-stu-id="eb660-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="eb660-135">En esta situación, los mensajes en RoleInstanceB se procesan según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="eb660-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="eb660-136">Los mensajes en RoleInstanceA se descartan y producen el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="eb660-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="eb660-137">
  **El servidor está ocupado. Vuelva a intentarlo.**</span><span class="sxs-lookup"><span data-stu-id="eb660-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="eb660-138">Ningún origen de extracción sondea ni descarga un mensaje.</span><span class="sxs-lookup"><span data-stu-id="eb660-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="eb660-139">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="eb660-139">For example:</span></span><br/>
  <span data-ttu-id="eb660-140">una canalización extrae los mensajes desde un origen FTP externo.</span><span class="sxs-lookup"><span data-stu-id="eb660-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="eb660-141">La instancia de rol que realiza la extracción entra en un estado de limitación.</span><span class="sxs-lookup"><span data-stu-id="eb660-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="eb660-142">En esta situación, la canalización deja de descargar mensajes adicionales hasta que la instancia de rol detiene la limitación.</span><span class="sxs-lookup"><span data-stu-id="eb660-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="eb660-143">Se envía una respuesta al cliente para que el cliente pueda volver a enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="eb660-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="eb660-144">Debe esperar a que se resuelva la limitación.</span><span class="sxs-lookup"><span data-stu-id="eb660-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="eb660-145">Específicamente, debe esperar hasta que se alcance el umbral bajo.</span><span class="sxs-lookup"><span data-stu-id="eb660-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="eb660-146">Notas importantes</span><span class="sxs-lookup"><span data-stu-id="eb660-146">Important notes</span></span>
* <span data-ttu-id="eb660-147">La limitación no se puede deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="eb660-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="eb660-148">Los umbrales de limitación no se pueden modificar.</span><span class="sxs-lookup"><span data-stu-id="eb660-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="eb660-149">La limitación está implementada en todo el sistema.</span><span class="sxs-lookup"><span data-stu-id="eb660-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="eb660-150">El servidor de Base de datos SQL de Azure también tiene limitaciones integradas.</span><span class="sxs-lookup"><span data-stu-id="eb660-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="eb660-151">Otros temas acerca de los servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="eb660-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="eb660-152">Instalación del SDK de Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="eb660-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="eb660-153">Tutoriales: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="eb660-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="eb660-154">¿Cómo puedo comenzar a utilizar el SDK de Servicios de BizTalk de Azure?</span><span class="sxs-lookup"><span data-stu-id="eb660-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="eb660-155">Servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="eb660-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="eb660-156">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="eb660-156">See Also</span></span>
* [<span data-ttu-id="eb660-157">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="eb660-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="eb660-158">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="eb660-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="eb660-159">Servicios de BizTalk: gráfico del estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="eb660-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="eb660-160">Servicios de BizTalk: pestañas Panel, Monitor y Escala</span><span class="sxs-lookup"><span data-stu-id="eb660-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="eb660-161">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="eb660-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="eb660-162">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="eb660-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

