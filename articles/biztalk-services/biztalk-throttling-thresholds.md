---
title: "aaaLearn sobre limitación en servicios de BizTalk | Documentos de Microsoft"
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="81054-105">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="81054-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="81054-106">Servicios de BizTalk de Azure implementa el servicio limitación basada en dos condiciones: número de hello y uso de memoria de mensajes simultáneos que se procesan.</span><span class="sxs-lookup"><span data-stu-id="81054-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="81054-107">Este tema enumeran Hola umbrales de limitación y describe el comportamiento de hello en tiempo de ejecución cuando se produce una condición de limitación.</span><span class="sxs-lookup"><span data-stu-id="81054-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="81054-108">Umbrales de limitación</span><span class="sxs-lookup"><span data-stu-id="81054-108">Throttling Thresholds</span></span>
<span data-ttu-id="81054-109">Hola tabla siguiente se muestran Hola origen limitación y los umbrales:</span><span class="sxs-lookup"><span data-stu-id="81054-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="81054-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="81054-110">Description</span></span> | <span data-ttu-id="81054-111">Umbral bajo</span><span class="sxs-lookup"><span data-stu-id="81054-111">Low Threshold</span></span> | <span data-ttu-id="81054-112">Umbral alto</span><span class="sxs-lookup"><span data-stu-id="81054-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="81054-113">Memoria</span><span class="sxs-lookup"><span data-stu-id="81054-113">Memory</span></span> |<span data-ttu-id="81054-114">% de memoria total del sistema disponible/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="81054-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="81054-115">Total PageFileBytes disponible es aproximadamente 2 veces Hola RAM del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="81054-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="81054-116">60%</span><span class="sxs-lookup"><span data-stu-id="81054-116">60%</span></span> |<span data-ttu-id="81054-117">70%</span><span class="sxs-lookup"><span data-stu-id="81054-117">70%</span></span> |
| <span data-ttu-id="81054-118">Procesamiento de mensajes</span><span class="sxs-lookup"><span data-stu-id="81054-118">Message Processing</span></span> |<span data-ttu-id="81054-119">Número de mensajes que se procesan simultáneamente</span><span class="sxs-lookup"><span data-stu-id="81054-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="81054-120">40 * número de núcleos</span><span class="sxs-lookup"><span data-stu-id="81054-120">40 * number of cores</span></span> |<span data-ttu-id="81054-121">100 * número de núcleos</span><span class="sxs-lookup"><span data-stu-id="81054-121">100 * number of cores</span></span> |

<span data-ttu-id="81054-122">Cuando se alcanza un umbral alta, servicios de BizTalk de Azure inicia toothrottle.</span><span class="sxs-lookup"><span data-stu-id="81054-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="81054-123">La limitación se detiene cuando se alcanza el umbral inferior Hola.</span><span class="sxs-lookup"><span data-stu-id="81054-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="81054-124">Por ejemplo, el servicio está utilizando un 65 % de la memoria del sistema.</span><span class="sxs-lookup"><span data-stu-id="81054-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="81054-125">En esta situación, no limitar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="81054-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="81054-126">El servicio empieza a usar un 70 % de la memoria del sistema.</span><span class="sxs-lookup"><span data-stu-id="81054-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="81054-127">En esta situación, el servicio de hello limita y continúa toothrottle hasta que el servicio de hello utiliza memoria del sistema de 60% (umbral inferior).</span><span class="sxs-lookup"><span data-stu-id="81054-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="81054-128">Servicios de BizTalk de Azure realiza un seguimiento de hello duración de limitación y Hola limitación estado (estado normal frente a estado limitada).</span><span class="sxs-lookup"><span data-stu-id="81054-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="81054-129">Comportamiento del tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="81054-129">Runtime Behavior</span></span>
<span data-ttu-id="81054-130">Cuando los servicios de BizTalk de Azure entra en un estado de limitación, se produce el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="81054-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="81054-131">La limitación es por instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="81054-131">Throttling is per role instance.</span></span> <span data-ttu-id="81054-132">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="81054-132">For example:</span></span><br/>
  <span data-ttu-id="81054-133">RoleInstanceA se está limitando.</span><span class="sxs-lookup"><span data-stu-id="81054-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="81054-134">RoleInstanceB no se está limitando.</span><span class="sxs-lookup"><span data-stu-id="81054-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="81054-135">En esta situación, los mensajes en RoleInstanceB se procesan según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="81054-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="81054-136">Mensajes de RoleInstanceA se descartan y se producirá un error con hello siguiente error:</span><span class="sxs-lookup"><span data-stu-id="81054-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="81054-137">
  **El servidor está ocupado. Vuelva a intentarlo.**</span><span class="sxs-lookup"><span data-stu-id="81054-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="81054-138">Ningún origen de extracción sondea ni descarga un mensaje.</span><span class="sxs-lookup"><span data-stu-id="81054-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="81054-139">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="81054-139">For example:</span></span><br/>
  <span data-ttu-id="81054-140">una canalización extrae los mensajes desde un origen FTP externo.</span><span class="sxs-lookup"><span data-stu-id="81054-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="81054-141">instancia de rol de Hello realizar la extracción de hello pone en un estado de limitación.</span><span class="sxs-lookup"><span data-stu-id="81054-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="81054-142">En esta situación, detiene el Hola canalización descargar mensajes adicionales hasta que finaliza la instancia de rol de hello limitación.</span><span class="sxs-lookup"><span data-stu-id="81054-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="81054-143">Se envía una respuesta toohello cliente para que cliente hello puede volver a enviar los mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="81054-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="81054-144">Debe esperar hasta que se resuelva la limitación de Hola.</span><span class="sxs-lookup"><span data-stu-id="81054-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="81054-145">En concreto, debe esperar hasta que se alcanza el umbral inferior Hola.</span><span class="sxs-lookup"><span data-stu-id="81054-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="81054-146">Notas importantes</span><span class="sxs-lookup"><span data-stu-id="81054-146">Important notes</span></span>
* <span data-ttu-id="81054-147">La limitación no se puede deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="81054-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="81054-148">Los umbrales de limitación no se pueden modificar.</span><span class="sxs-lookup"><span data-stu-id="81054-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="81054-149">La limitación está implementada en todo el sistema.</span><span class="sxs-lookup"><span data-stu-id="81054-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="81054-150">Hola servidor de base de datos de SQL Azure también tiene la limitación integrados.</span><span class="sxs-lookup"><span data-stu-id="81054-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="81054-151">Otros temas acerca de los servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="81054-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="81054-152">Hola instalar SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="81054-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="81054-153">Tutoriales: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="81054-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="81054-154">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="81054-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="81054-155">Servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="81054-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="81054-156">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="81054-156">See Also</span></span>
* [<span data-ttu-id="81054-157">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="81054-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="81054-158">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="81054-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="81054-159">Servicios de BizTalk: gráfico del estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="81054-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="81054-160">Servicios de BizTalk: pestañas Panel, Monitor y Escala</span><span class="sxs-lookup"><span data-stu-id="81054-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="81054-161">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="81054-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="81054-162">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="81054-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

