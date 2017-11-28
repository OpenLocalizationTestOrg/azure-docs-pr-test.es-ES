---
title: "comportamiento de almacenamiento en caché de CDN de Azure con cadenas de consulta aaaControl | Documentos de Microsoft"
description: "Cadena de consulta CDN Azure controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché."
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
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="68fec-103">Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="68fec-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68fec-104">Standard</span><span class="sxs-lookup"><span data-stu-id="68fec-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="68fec-105">Red CDN premium de Azure de Verizon</span><span class="sxs-lookup"><span data-stu-id="68fec-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="68fec-106">Información general</span><span class="sxs-lookup"><span data-stu-id="68fec-106">Overview</span></span>
<span data-ttu-id="68fec-107">Cadena de consulta controla cómo archivos están almacenados en memoria caché cuando contienen cadenas de consulta de toobe el almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="68fec-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68fec-108">productos Standard y Premium CDN Hola proporcionan Hola misma funcionalidad de almacenamiento en caché de cadenas de consulta, pero difiere de la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="68fec-109">Este documento describe la interfaz de Hola de **estándar de red CDN de Azure de Akamai** y **estándar de red CDN de Azure de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="68fec-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="68fec-110">Para más información sobre el almacenamiento en caché de cadenas de consulta con la **red CDN premium de Azure de Verizon**, consulte [Control del comportamiento del almacenamiento en caché de las solicitudes de CDN con cadenas de consultas - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="68fec-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="68fec-111">Hay tres modos disponibles:</span><span class="sxs-lookup"><span data-stu-id="68fec-111">Three modes are available:</span></span>

* <span data-ttu-id="68fec-112">**Pasar por alto las cadenas de consulta**: se trata de modo predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="68fec-113">nodo del borde CDN Hola pasará cadena de consulta de Hola de origen de toohello de solicitante de hello en la primera solicitud de Hola y activos de Hola de caché.</span><span class="sxs-lookup"><span data-stu-id="68fec-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="68fec-114">Todas las solicitudes posteriores para dicho activo que se atienden desde el nodo del borde de hello hará caso omiso cadena de consulta de hello hasta que expire el activo en caché Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="68fec-115">**Omitir almacenamiento en caché para la dirección URL con cadenas de consulta**: en este modo, las solicitudes con cadenas de consulta no se almacenan en el nodo del borde CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="68fec-116">nodo de Hello borde recupera asset Hola directamente desde el origen de hello y pasa toohello solicitante con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="68fec-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="68fec-117">**Almacenar en caché cada URL única**: este modo trata cada solicitud con una cadena de consulta como un activo único con su propia memoria caché.</span><span class="sxs-lookup"><span data-stu-id="68fec-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="68fec-118">Por ejemplo, Hola respuesta desde origen Hola para una solicitud de *foo.ashx?q=bar* se almacena en caché en el nodo del borde de Hola y devueltos para las cachés posteriores con esa misma cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="68fec-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="68fec-119">Una solicitud de *foo.ashx?q=somethingelse* podría almacenarse en memoria caché como un recurso independiente con su propio tiempo toolive.</span><span class="sxs-lookup"><span data-stu-id="68fec-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="68fec-120">Modificación de la configuración del almacenamiento en caché de cadenas de consultas para perfiles de red CDN estándar</span><span class="sxs-lookup"><span data-stu-id="68fec-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="68fec-121">En la hoja de perfil CDN Hola, haga clic en extremo de red CDN Hola desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="68fec-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Puntos de conexión de hoja del perfil de red CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="68fec-123">se abre la hoja de punto de conexión de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="68fec-124">Haga clic en hello **configurar** botón.</span><span class="sxs-lookup"><span data-stu-id="68fec-124">Click hello **Configure** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="68fec-126">se abre la hoja de configuración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="68fec-127">Seleccione una opción de hello **comportamiento almacenamiento en caché de cadena de consulta** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="68fec-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![Opciones del almacenamiento en caché de cadenas de consultas de CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="68fec-129">Después de realizar la selección, haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="68fec-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68fec-130">cambios de configuración de Hello no pueden ser inmediatamente visibles, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="68fec-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="68fec-131">Para <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completará en un minuto.</span><span class="sxs-lookup"><span data-stu-id="68fec-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="68fec-132">Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.</span><span class="sxs-lookup"><span data-stu-id="68fec-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

