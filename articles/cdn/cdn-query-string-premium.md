---
title: "comportamiento de almacenamiento en caché de CDN de Azure con cadenas de consulta - Premium aaaControl | Documentos de Microsoft"
description: "Cadena de consulta CDN Azure controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="170d1-103">Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta: Premium</span><span class="sxs-lookup"><span data-stu-id="170d1-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="170d1-104">Standard</span><span class="sxs-lookup"><span data-stu-id="170d1-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="170d1-105">Red CDN premium de Azure de Verizon</span><span class="sxs-lookup"><span data-stu-id="170d1-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="170d1-106">Información general</span><span class="sxs-lookup"><span data-stu-id="170d1-106">Overview</span></span>
<span data-ttu-id="170d1-107">Cadena de consulta controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="170d1-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="170d1-108">productos Standard y Premium CDN Hola proporcionan Hola misma funcionalidad de almacenamiento en caché de cadenas de consulta, pero difiere de la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="170d1-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="170d1-109">Este documento describe la interfaz de Hola de **Premium de CDN de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="170d1-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="170d1-110">Para obtener más información sobre el almacenamiento en caché de cadenas de consulta con la **red CDN estándar de Azure de Akamai** y la **red CDN estándar de Azure de Verizon**, consulte [Control del comportamiento del almacenamiento en caché de las solicitudes de red CDN con cadenas de consultas](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="170d1-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="170d1-111">Hay tres modos disponibles:</span><span class="sxs-lookup"><span data-stu-id="170d1-111">Three modes are available:</span></span>

* <span data-ttu-id="170d1-112">**caché estándar**: se trata de modo predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="170d1-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="170d1-113">nodo del borde CDN Hola pasará cadena de consulta de Hola de origen de toohello de solicitante de hello en la primera solicitud de Hola y activos de Hola de caché.</span><span class="sxs-lookup"><span data-stu-id="170d1-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="170d1-114">Todas las solicitudes posteriores para dicho activo que se atienden desde el nodo del borde de hello hará caso omiso cadena de consulta de hello hasta que expire el activo en caché Hola.</span><span class="sxs-lookup"><span data-stu-id="170d1-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="170d1-115">**sin caché**: en este modo, las solicitudes con cadenas de consulta no se almacenan en el nodo del borde CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="170d1-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="170d1-116">nodo de Hello borde recupera asset Hola directamente desde el origen de hello y pasa toohello solicitante con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="170d1-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="170d1-117">**unique-cache**: este modo trata cada solicitud con una cadena de consulta como un activo único con su propia memoria caché.</span><span class="sxs-lookup"><span data-stu-id="170d1-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="170d1-118">Por ejemplo, Hola respuesta desde origen Hola para una solicitud de *foo.ashx?q=bar* se almacena en caché en el nodo del borde de Hola y devueltos para las cachés posteriores con esa misma cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="170d1-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="170d1-119">Una solicitud de *foo.ashx?q=somethingelse* podría almacenarse en memoria caché como un recurso independiente con su propio tiempo toolive.</span><span class="sxs-lookup"><span data-stu-id="170d1-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="170d1-120">Modificación de la configuración del almacenamiento en caché de cadenas de consultas para perfiles de red CDN premium</span><span class="sxs-lookup"><span data-stu-id="170d1-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="170d1-121">En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.</span><span class="sxs-lookup"><span data-stu-id="170d1-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="170d1-123">se abre el portal de administración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="170d1-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="170d1-124">Mantenga el mouse sobre hello **HTTP grandes** ficha y, a continuación, mantenga el mouse sobre hello **configuración de la caché** ventana flotante.</span><span class="sxs-lookup"><span data-stu-id="170d1-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="170d1-125">Haga clic en **Almacenamiento en caché de cadenas de consultas**.</span><span class="sxs-lookup"><span data-stu-id="170d1-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="170d1-126">Aparecen las opciones del almacenamiento en caché de cadenas de consultas.</span><span class="sxs-lookup"><span data-stu-id="170d1-126">Query string caching options are displayed.</span></span>
   
    ![Opciones del almacenamiento en caché de cadenas de consultas de CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="170d1-128">Después de realizar la selección, haga clic en hello **actualización** botón.</span><span class="sxs-lookup"><span data-stu-id="170d1-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="170d1-129">cambios de configuración de Hello no pueden ser inmediatamente visibles, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="170d1-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="170d1-130">Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.</span><span class="sxs-lookup"><span data-stu-id="170d1-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

