---
title: "carga aaaPre activos en un punto de conexión de red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopre carga almacena en caché el contenido en un punto de conexión de red CDN de Azure."
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="38a60-103">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="38a60-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="38a60-104">De forma predeterminada, los recursos primero se almacenan en caché conforme se solicitan.</span><span class="sxs-lookup"><span data-stu-id="38a60-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="38a60-105">Esto significa que la primera solicitud de cada región de hello puede tardar más tiempo, debido a que los servidores de hello borde no tendrán contenido Hola almacena en caché y deberá tooforward Hola solicitud enviada toohello origen al servidor.</span><span class="sxs-lookup"><span data-stu-id="38a60-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="38a60-106">La precarga del contenido evita esta latencia de primera visita.</span><span class="sxs-lookup"><span data-stu-id="38a60-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="38a60-107">Además tooproviding una mejor experiencia de cliente, Cargando previamente los recursos almacenados en memoria caché también puede reducir el tráfico de red en el servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="38a60-108">Cargando previamente activos es útil para los eventos de gran tamaño o contenido deja de estar disponible al mismo tiempo tooa gran número de usuarios, como una nueva versión de la película o una actualización de software.</span><span class="sxs-lookup"><span data-stu-id="38a60-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="38a60-109">Este tutorial le guiará a través de la precarga de contenido almacenado en la caché en todos los nodos perimetrales de CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="38a60-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="38a60-110">Tutorial</span><span class="sxs-lookup"><span data-stu-id="38a60-110">Walkthrough</span></span>
1. <span data-ttu-id="38a60-111">Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN toohello que contiene el extremo de hello desea toopre carga.</span><span class="sxs-lookup"><span data-stu-id="38a60-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="38a60-112">se abre la hoja de perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="38a60-113">Haga clic en el punto de conexión de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="38a60-114">se abre la hoja de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="38a60-115">Desde la hoja de punto de conexión de red CDN Hola, haga clic en el botón de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Hoja Punto de conexión de CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="38a60-117">se abre la hoja de la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-117">hello Load blade opens.</span></span>
   
    ![Hoja Carga de CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="38a60-119">Escriba la ruta de acceso completa de Hola de cada recurso que se va tooload (p. ej., `/pictures/kitten.png`) en hello **ruta de acceso** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="38a60-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="38a60-120">Más **ruta de acceso** cuadros de texto que aparecerá después de escribir texto tooallow toobuild una lista de varios activos.</span><span class="sxs-lookup"><span data-stu-id="38a60-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="38a60-121">Puede eliminar los activos de lista de hello haciendo clic en el botón de puntos suspensivos (...) de Hola.</span><span class="sxs-lookup"><span data-stu-id="38a60-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="38a60-122">Las rutas de acceso deben ser una dirección URL relativa que se ajuste a continuación hello [expresión regular](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="38a60-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="38a60-123">Carga de un solo archivo `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="38a60-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="38a60-124">Carga de un único archivo con cadena de consulta `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="38a60-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="38a60-125">Cada recurso debe tener su propia ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="38a60-125">Each asset must have its own path.</span></span>  <span data-ttu-id="38a60-126">No hay ninguna funcionalidad comodín para la carga previa de recursos.</span><span class="sxs-lookup"><span data-stu-id="38a60-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Botón Cargar](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="38a60-128">Haga clic en hello **carga** botón.</span><span class="sxs-lookup"><span data-stu-id="38a60-128">Click hello **Load** button.</span></span>
   
    ![Botón Cargar](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="38a60-130">Hay una limitación de 10 solicitudes de carga por minuto por perfil de red CDN.</span><span class="sxs-lookup"><span data-stu-id="38a60-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="38a60-131">Se admiten 50 rutas por solicitud.</span><span class="sxs-lookup"><span data-stu-id="38a60-131">50 paths are allowed per request.</span></span> <span data-ttu-id="38a60-132">Cada ruta de acceso tiene un límite de longitud de 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="38a60-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="38a60-133">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="38a60-133">See also</span></span>
* [<span data-ttu-id="38a60-134">Purgar un punto de conexión de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="38a60-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="38a60-135">Referencia de la API de REST de red de CDN de Azure - purgar o cargar previamente un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="38a60-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

