---
title: Compatibilidad con HTTP/2 en la red CDN de Azure | Microsoft Docs
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
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="a9dac-103">Compatibilidad con HTTP/2 en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="a9dac-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="a9dac-104">HTTP/2 es una revisión principal en HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="a9dac-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="a9dac-105">Proporciona más rápido experimentan usuario mejorada, tiempo de respuesta reducido y rendimiento web, al tiempo que mantiene los métodos conocidos de HTTP, códigos de estado y semántica.</span><span class="sxs-lookup"><span data-stu-id="a9dac-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="a9dac-106">Aunque HTTP/2 está diseñado para trabajar con HTTP y HTTPS, muchos exploradores web de cliente solo admiten HTTP/2 sobre TLS.</span><span class="sxs-lookup"><span data-stu-id="a9dac-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="a9dac-107">Ventajas HTTP/2</span><span class="sxs-lookup"><span data-stu-id="a9dac-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="a9dac-108">Las ventajas de HTTP/2 incluyen:</span><span class="sxs-lookup"><span data-stu-id="a9dac-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="a9dac-109">**Multiplexación y simultaneidad**</span><span class="sxs-lookup"><span data-stu-id="a9dac-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="a9dac-110">Mediante HTTP 1.1, para realizar varias solicitudes de varios recursos se requieren varias conexiones TCP y cada conexión tiene asociada una sobrecarga de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a9dac-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="a9dac-111">HTTP/2 permite que se soliciten varios recursos en una única conexión TCP.</span><span class="sxs-lookup"><span data-stu-id="a9dac-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="a9dac-112">**Compresión de encabezados**</span><span class="sxs-lookup"><span data-stu-id="a9dac-112">**Header compression**</span></span>

    <span data-ttu-id="a9dac-113">Al comprimir los encabezados HTTP de los recursos atendidos, el tiempo en la red se reduce considerablemente.</span><span class="sxs-lookup"><span data-stu-id="a9dac-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="a9dac-114">**Dependencias de secuencias**</span><span class="sxs-lookup"><span data-stu-id="a9dac-114">**Stream dependencies**</span></span>

    <span data-ttu-id="a9dac-115">Las dependencias de secuencias permiten al cliente indicar al servidor qué recursos tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="a9dac-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="a9dac-116">Compatibilidad con exploradores HTTP/2</span><span class="sxs-lookup"><span data-stu-id="a9dac-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="a9dac-117">Todos los exploradores principales han implementado la compatibilidad con HTTP/2 en sus versiones actuales.</span><span class="sxs-lookup"><span data-stu-id="a9dac-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="a9dac-118">Los exploradores no compatibles conmutarán automáticamente a HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="a9dac-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="a9dac-119">Browser</span><span class="sxs-lookup"><span data-stu-id="a9dac-119">Browser</span></span>|<span data-ttu-id="a9dac-120">Versión mínima</span><span class="sxs-lookup"><span data-stu-id="a9dac-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="a9dac-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="a9dac-121">Microsoft Edge</span></span>| <span data-ttu-id="a9dac-122">12</span><span class="sxs-lookup"><span data-stu-id="a9dac-122">12</span></span>|
|<span data-ttu-id="a9dac-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="a9dac-123">Google Chrome</span></span>| <span data-ttu-id="a9dac-124">43</span><span class="sxs-lookup"><span data-stu-id="a9dac-124">43</span></span>|
|<span data-ttu-id="a9dac-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="a9dac-125">Mozilla Firefox</span></span>| <span data-ttu-id="a9dac-126">38</span><span class="sxs-lookup"><span data-stu-id="a9dac-126">38</span></span>|
|<span data-ttu-id="a9dac-127">Opera</span><span class="sxs-lookup"><span data-stu-id="a9dac-127">Opera</span></span>| <span data-ttu-id="a9dac-128">32</span><span class="sxs-lookup"><span data-stu-id="a9dac-128">32</span></span>|
|<span data-ttu-id="a9dac-129">Safari</span><span class="sxs-lookup"><span data-stu-id="a9dac-129">Safari</span></span>| <span data-ttu-id="a9dac-130">9</span><span class="sxs-lookup"><span data-stu-id="a9dac-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="a9dac-131">Habilitación de la compatibilidad con HTTP/2 en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="a9dac-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="a9dac-132">La compatibilidad con HTTP/2 se encuentra actualmente activa para los perfiles de **red CDN de Azure de Akamai** y la **red CDN de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="a9dac-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="a9dac-133">No es necesaria ninguna otra acción por parte de los clientes.</span><span class="sxs-lookup"><span data-stu-id="a9dac-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="a9dac-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9dac-134">Next Steps</span></span>

<span data-ttu-id="a9dac-135">Para ver las ventajas de HTTP/2 en acción, consulte [esta demostración de Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="a9dac-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="a9dac-136">Para más información sobre HTTP/2, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="a9dac-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="a9dac-137">Página principal de especificación de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="a9dac-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="a9dac-138">Preguntas más frecuentes oficiales de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="a9dac-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="a9dac-139">Información de HTTP/2 de Akamai</span><span class="sxs-lookup"><span data-stu-id="a9dac-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="a9dac-140">Para más información sobre las características disponibles de la red CDN de Azure, consulte la [información general sobre la red CDN de Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="a9dac-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>