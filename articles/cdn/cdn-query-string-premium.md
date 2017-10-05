---
title: "Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta: Premium | Microsoft Docs"
description: "El almacenamiento en caché de las cadenas de consulta de la red CDN de Azure controla el modo en que se almacenan en caché los archivos cuando contienen cadenas de consulta."
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
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="9183a-103">Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta: Premium</span><span class="sxs-lookup"><span data-stu-id="9183a-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9183a-104">Standard</span><span class="sxs-lookup"><span data-stu-id="9183a-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="9183a-105">Red CDN premium de Azure de Verizon</span><span class="sxs-lookup"><span data-stu-id="9183a-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9183a-106">Información general</span><span class="sxs-lookup"><span data-stu-id="9183a-106">Overview</span></span>
<span data-ttu-id="9183a-107">El almacenamiento en caché de las cadenas de consultas controla la manera en que se almacenarán en caché los archivos cuando contienen cadenas de consulta.</span><span class="sxs-lookup"><span data-stu-id="9183a-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9183a-108">Los productos estándar y premium de CDN ofrecen la misma funcionalidad de almacenamiento en caché de cadenas de consultas, pero la interfaz de usuario es distinta.</span><span class="sxs-lookup"><span data-stu-id="9183a-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="9183a-109">En este documento se describe la interfaz de la **red CDN premium de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="9183a-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="9183a-110">Para obtener más información sobre el almacenamiento en caché de cadenas de consulta con la **red CDN estándar de Azure de Akamai** y la **red CDN estándar de Azure de Verizon**, consulte [Control del comportamiento del almacenamiento en caché de las solicitudes de red CDN con cadenas de consultas](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="9183a-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="9183a-111">Hay tres modos disponibles:</span><span class="sxs-lookup"><span data-stu-id="9183a-111">Three modes are available:</span></span>

* <span data-ttu-id="9183a-112">**standard-cache**: este es el modo predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9183a-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="9183a-113">El nodo perimetral de CDN pasará la cadena de consulta del solicitante al origen en la primera solicitud y almacenará en la memoria caché el activo.</span><span class="sxs-lookup"><span data-stu-id="9183a-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="9183a-114">Todas las solicitudes posteriores de ese activo que se ofrecen desde el nodo perimetral ignorarán la cadena de consulta hasta que expira el activo en caché.</span><span class="sxs-lookup"><span data-stu-id="9183a-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="9183a-115">**no-cache**: en este modo, las solicitudes con cadenas de consultas no están almacenadas en caché en el nodo perimetral de red CDN.</span><span class="sxs-lookup"><span data-stu-id="9183a-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="9183a-116">El nodo perimetral recupera el activo directamente del origen y lo pasa al solicitante con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="9183a-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="9183a-117">**unique-cache**: este modo trata cada solicitud con una cadena de consulta como un activo único con su propia memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9183a-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="9183a-118">Por ejemplo, la respuesta desde el origen para una solicitud de *foo.ashx?q=bar* se almacenaría en la memoria caché en el nodo perimetral y se devolvería para cachés posteriores con esa misma cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="9183a-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="9183a-119">Se almacenaría en caché una solicitud de *foo.ashx?q=somethingelse* como un activo independiente con su propio período de vida.</span><span class="sxs-lookup"><span data-stu-id="9183a-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="9183a-120">Modificación de la configuración del almacenamiento en caché de cadenas de consultas para perfiles de red CDN premium</span><span class="sxs-lookup"><span data-stu-id="9183a-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="9183a-121">En la hoja de perfil de CDN, haga clic en el botón **Administrar** .</span><span class="sxs-lookup"><span data-stu-id="9183a-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="9183a-123">Se abre el portal de administración de CDN.</span><span class="sxs-lookup"><span data-stu-id="9183a-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="9183a-124">Desplace el mouse sobre la pestaña **HTTP grande** y luego mantenga el mouse sobre el control flotante **Configuración de caché**.</span><span class="sxs-lookup"><span data-stu-id="9183a-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="9183a-125">Haga clic en **Almacenamiento en caché de cadenas de consultas**.</span><span class="sxs-lookup"><span data-stu-id="9183a-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="9183a-126">Aparecen las opciones del almacenamiento en caché de cadenas de consultas.</span><span class="sxs-lookup"><span data-stu-id="9183a-126">Query string caching options are displayed.</span></span>
   
    ![Opciones del almacenamiento en caché de cadenas de consultas de CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="9183a-128">Tras efectuar su selección, haga clic en el botón **Actualizar** .</span><span class="sxs-lookup"><span data-stu-id="9183a-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9183a-129">Es posible que los cambios en la configuración no sean visibles de forma inmediata, ya que el registro puede tardar en propagarse a través de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="9183a-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="9183a-130">Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.</span><span class="sxs-lookup"><span data-stu-id="9183a-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

