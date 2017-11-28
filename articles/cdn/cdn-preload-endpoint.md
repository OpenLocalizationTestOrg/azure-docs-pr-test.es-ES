---
title: "Carga previa de recursos en un punto de conexión de Azure CDN | Microsoft Docs"
description: "Aprenda a precargar el contenido almacenado en caché en un punto de conexión de la red CDN de Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="7e2da-103">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="7e2da-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="7e2da-104">De forma predeterminada, los recursos primero se almacenan en caché conforme se solicitan.</span><span class="sxs-lookup"><span data-stu-id="7e2da-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="7e2da-105">Esto significa que la primera solicitud de cada región puede tardar más tiempo, ya que los servidores perimetrales no tendrán el contenido almacenado en caché y deberán reenviar la solicitud al servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="7e2da-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="7e2da-106">La precarga del contenido evita esta latencia de primera visita.</span><span class="sxs-lookup"><span data-stu-id="7e2da-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="7e2da-107">Además de proporcionar una mejor experiencia de cliente, la precarga de los recursos almacenados en caché puede reducir el tráfico de red en el servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="7e2da-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="7e2da-108">La precarga de recursos es útil para grandes eventos o contenido que se pone a disposición de un gran número de usuarios simultáneamente, como el lanzamiento de una nueva película o una actualización de software.</span><span class="sxs-lookup"><span data-stu-id="7e2da-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="7e2da-109">Este tutorial le guiará a través de la precarga de contenido almacenado en la caché en todos los nodos perimetrales de CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2da-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="7e2da-110">Tutorial</span><span class="sxs-lookup"><span data-stu-id="7e2da-110">Walkthrough</span></span>
1. <span data-ttu-id="7e2da-111">En el [Portal de Azure](https://portal.azure.com), examine el perfil de CDN que contiene el punto de conexión que quiere precargar.</span><span class="sxs-lookup"><span data-stu-id="7e2da-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="7e2da-112">Se abre la hoja del perfil.</span><span class="sxs-lookup"><span data-stu-id="7e2da-112">The profile blade opens.</span></span>
2. <span data-ttu-id="7e2da-113">Haga clic en el punto de conexión de la lista.</span><span class="sxs-lookup"><span data-stu-id="7e2da-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="7e2da-114">Se abre la hoja del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="7e2da-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="7e2da-115">En la hoja del punto de conexión de CDN, haga clic en el botón Cargar.</span><span class="sxs-lookup"><span data-stu-id="7e2da-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Hoja Punto de conexión de CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="7e2da-117">Se abre la hoja Cargar.</span><span class="sxs-lookup"><span data-stu-id="7e2da-117">The Load blade opens.</span></span>
   
    ![Hoja Carga de CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="7e2da-119">Escriba la ruta de acceso completa de cada recurso que quiera cargar (por ejemplo, `/pictures/kitten.png`) en el cuadro de texto **Ruta de acceso** .</span><span class="sxs-lookup"><span data-stu-id="7e2da-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7e2da-120">Aparecerán más cuadros de texto de **Ruta de acceso** después de escribir texto para permitirle crear una lista de varios activos.</span><span class="sxs-lookup"><span data-stu-id="7e2da-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="7e2da-121">Puede eliminar activos en la lista haciendo clic en el botón de puntos suspensivos (...).</span><span class="sxs-lookup"><span data-stu-id="7e2da-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="7e2da-122">Las rutas de acceso deben ser una dirección URL relativa que se ajuste a la siguiente [expresión regular](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="7e2da-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="7e2da-123">Carga de un solo archivo `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="7e2da-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="7e2da-124">Carga de un único archivo con cadena de consulta `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="7e2da-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="7e2da-125">Cada recurso debe tener su propia ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="7e2da-125">Each asset must have its own path.</span></span>  <span data-ttu-id="7e2da-126">No hay ninguna funcionalidad comodín para la carga previa de recursos.</span><span class="sxs-lookup"><span data-stu-id="7e2da-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Botón Cargar](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="7e2da-128">Haga clic en el botón **Cargar** .</span><span class="sxs-lookup"><span data-stu-id="7e2da-128">Click the **Load** button.</span></span>
   
    ![Botón Cargar](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="7e2da-130">Hay una limitación de 10 solicitudes de carga por minuto por perfil de red CDN.</span><span class="sxs-lookup"><span data-stu-id="7e2da-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="7e2da-131">Se admiten 50 rutas por solicitud.</span><span class="sxs-lookup"><span data-stu-id="7e2da-131">50 paths are allowed per request.</span></span> <span data-ttu-id="7e2da-132">Cada ruta de acceso tiene un límite de longitud de 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7e2da-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="7e2da-133">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7e2da-133">See also</span></span>
* [<span data-ttu-id="7e2da-134">Purgar un punto de conexión de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="7e2da-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="7e2da-135">Referencia de la API de REST de red de CDN de Azure - purgar o cargar previamente un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="7e2da-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

