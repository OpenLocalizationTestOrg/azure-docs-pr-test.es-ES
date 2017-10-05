---
title: "Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta | Microsoft Docs"
description: "El almacenamiento en caché de las cadenas de consulta de la red CDN de Azure controla el modo en que se almacenan en caché los archivos cuando contienen cadenas de consulta."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="6e6b8-103">Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="6e6b8-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e6b8-104">Standard</span><span class="sxs-lookup"><span data-stu-id="6e6b8-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="6e6b8-105">Red CDN premium de Azure de Verizon</span><span class="sxs-lookup"><span data-stu-id="6e6b8-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6e6b8-106">Información general</span><span class="sxs-lookup"><span data-stu-id="6e6b8-106">Overview</span></span>
<span data-ttu-id="6e6b8-107">El almacenamiento en caché de las cadenas de consultas controla la manera en que se almacenarán en caché los archivos cuando contienen cadenas de consulta.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e6b8-108">Los productos estándar y premium de CDN ofrecen la misma funcionalidad de almacenamiento en caché de cadenas de consultas, pero la interfaz de usuario es distinta.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="6e6b8-109">En este documento se describe la interfaz de la **red CDN estándar de Azure de Akamai** y la **red CDN estándar de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="6e6b8-110">Para más información sobre el almacenamiento en caché de cadenas de consulta con la **red CDN premium de Azure de Verizon**, consulte [Control del comportamiento del almacenamiento en caché de las solicitudes de CDN con cadenas de consultas - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="6e6b8-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="6e6b8-111">Hay tres modos disponibles:</span><span class="sxs-lookup"><span data-stu-id="6e6b8-111">Three modes are available:</span></span>

* <span data-ttu-id="6e6b8-112">**Ignorar cadenas de consultas**: este es el modo predeterminado.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="6e6b8-113">El nodo perimetral de CDN pasará la cadena de consulta del solicitante al origen en la primera solicitud y almacenará en la memoria caché el activo.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="6e6b8-114">Todas las solicitudes posteriores de ese activo que se ofrecen desde el nodo perimetral ignorarán la cadena de consulta hasta que expira el activo en caché.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="6e6b8-115">**Omitir el almacenamiento en caché para dirección URL con cadenas de consultas**: en este modo, las solicitudes con cadenas de consultas no se almacenan en caché en el nodo perimetral de red CDN.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="6e6b8-116">El nodo perimetral recupera el activo directamente del origen y lo pasa al solicitante con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="6e6b8-117">**Almacenar en caché cada URL única**: este modo trata cada solicitud con una cadena de consulta como un activo único con su propia memoria caché.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="6e6b8-118">Por ejemplo, la respuesta desde el origen para una solicitud de *foo.ashx?q=bar* se almacenaría en la memoria caché en el nodo perimetral y se devolvería para cachés posteriores con esa misma cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="6e6b8-119">Se almacenaría en caché una solicitud de *foo.ashx?q=somethingelse* como un activo independiente con su propio período de vida.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="6e6b8-120">Modificación de la configuración del almacenamiento en caché de cadenas de consultas para perfiles de red CDN estándar</span><span class="sxs-lookup"><span data-stu-id="6e6b8-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="6e6b8-121">En la hoja de perfil de red CDN, haga clic en el punto de conexión de CDN que desea administrar.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![Puntos de conexión de hoja del perfil de red CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="6e6b8-123">Se abre la hoja del punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="6e6b8-124">Elija el botón **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="6e6b8-124">Click the **Configure** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="6e6b8-126">Se abre la hoja de configuración de CDN.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="6e6b8-127">Seleccione una opción en la lista desplegable **Comportamiento del almacenamiento en caché de cadenas de consultas** .</span><span class="sxs-lookup"><span data-stu-id="6e6b8-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![Opciones del almacenamiento en caché de cadenas de consultas de CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="6e6b8-129">Tras efectuar su selección, haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6e6b8-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e6b8-130">Es posible que los cambios en la configuración no sean visibles de forma inmediata, ya que el registro puede tardar en propagarse a través de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="6e6b8-131">Para <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completará en un minuto.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="6e6b8-132">Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.</span><span class="sxs-lookup"><span data-stu-id="6e6b8-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

