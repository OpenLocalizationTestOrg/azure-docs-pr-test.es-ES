---
title: compatibilidad con aaaHTTP/2 en la red CDN de Azure | Documentos de Microsoft
description: Aprenda sobre la compatibilidad con HTTP/2 y la red CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="deadf-103">Compatibilidad con HTTP/2 en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="deadf-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="deadf-104">HTTP/2 es una tooHTTP/1.1\ revisión principal.</span><span class="sxs-lookup"><span data-stu-id="deadf-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="deadf-105">Proporciona más rápido experimentan usuario mejorada, tiempo de respuesta reducido y rendimiento web, al tiempo que mantiene los métodos HTTP conocidos de hello, códigos de estado y la semántica.</span><span class="sxs-lookup"><span data-stu-id="deadf-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="deadf-106">Aunque HTTP/2 es toowork diseñada con HTTP y HTTPS, muchos exploradores web de cliente solo son compatibles con HTTP/2 a través de TLS.</span><span class="sxs-lookup"><span data-stu-id="deadf-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="deadf-107">Ventajas HTTP/2</span><span class="sxs-lookup"><span data-stu-id="deadf-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="deadf-108">ventajas de Hola de HTTP/2 incluyen:</span><span class="sxs-lookup"><span data-stu-id="deadf-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="deadf-109">**Multiplexación y simultaneidad**</span><span class="sxs-lookup"><span data-stu-id="deadf-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="deadf-110">Mediante HTTP 1.1, para realizar varias solicitudes de varios recursos se requieren varias conexiones TCP y cada conexión tiene asociada una sobrecarga de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="deadf-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="deadf-111">HTTP/2 permite que varios toobe recursos solicitado en una sola conexión de TCP.</span><span class="sxs-lookup"><span data-stu-id="deadf-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="deadf-112">**Compresión de encabezados**</span><span class="sxs-lookup"><span data-stu-id="deadf-112">**Header compression**</span></span>

    <span data-ttu-id="deadf-113">Mediante la compresión de encabezados de hello HTTP para recursos atendidos, tiempo en conexión Hola se reduce significativamente.</span><span class="sxs-lookup"><span data-stu-id="deadf-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="deadf-114">**Dependencias de secuencias**</span><span class="sxs-lookup"><span data-stu-id="deadf-114">**Stream dependencies**</span></span>

    <span data-ttu-id="deadf-115">Dependencias de secuencia permiten a cliente hello tooindicate toohello server qué recursos tienen prioridad.</span><span class="sxs-lookup"><span data-stu-id="deadf-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="deadf-116">Compatibilidad con exploradores HTTP/2</span><span class="sxs-lookup"><span data-stu-id="deadf-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="deadf-117">Todos los exploradores principales de hello han implementado la compatibilidad con HTTP/2 en sus versiones actuales.</span><span class="sxs-lookup"><span data-stu-id="deadf-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="deadf-118">Los exploradores no compatibles tendrán automáticamente reserva tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="deadf-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="deadf-119">Browser</span><span class="sxs-lookup"><span data-stu-id="deadf-119">Browser</span></span>|<span data-ttu-id="deadf-120">Versión mínima</span><span class="sxs-lookup"><span data-stu-id="deadf-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="deadf-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="deadf-121">Microsoft Edge</span></span>| <span data-ttu-id="deadf-122">12</span><span class="sxs-lookup"><span data-stu-id="deadf-122">12</span></span>|
|<span data-ttu-id="deadf-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="deadf-123">Google Chrome</span></span>| <span data-ttu-id="deadf-124">43</span><span class="sxs-lookup"><span data-stu-id="deadf-124">43</span></span>|
|<span data-ttu-id="deadf-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="deadf-125">Mozilla Firefox</span></span>| <span data-ttu-id="deadf-126">38</span><span class="sxs-lookup"><span data-stu-id="deadf-126">38</span></span>|
|<span data-ttu-id="deadf-127">Opera</span><span class="sxs-lookup"><span data-stu-id="deadf-127">Opera</span></span>| <span data-ttu-id="deadf-128">32</span><span class="sxs-lookup"><span data-stu-id="deadf-128">32</span></span>|
|<span data-ttu-id="deadf-129">Safari</span><span class="sxs-lookup"><span data-stu-id="deadf-129">Safari</span></span>| <span data-ttu-id="deadf-130">9</span><span class="sxs-lookup"><span data-stu-id="deadf-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="deadf-131">Habilitación de la compatibilidad con HTTP/2 en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="deadf-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="deadf-132">La compatibilidad con HTTP/2 se encuentra actualmente activa para los perfiles de **red CDN de Azure de Akamai** y la **red CDN de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="deadf-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="deadf-133">No es necesaria ninguna otra acción por parte de los clientes.</span><span class="sxs-lookup"><span data-stu-id="deadf-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="deadf-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="deadf-134">Next Steps</span></span>

<span data-ttu-id="deadf-135">ventajas de hello toosee de HTTP/2 en acción, vea [esta demostración de Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="deadf-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="deadf-136">toolearn más información acerca de HTTP/2, visite Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="deadf-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="deadf-137">Página principal de especificación de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="deadf-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="deadf-138">Preguntas más frecuentes oficiales de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="deadf-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="deadf-139">Información de HTTP/2 de Akamai</span><span class="sxs-lookup"><span data-stu-id="deadf-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="deadf-140">toolearn más información acerca de funciones disponibles en de CDN de Azure, vea hello [información general sobre la red CDN de Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="deadf-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
