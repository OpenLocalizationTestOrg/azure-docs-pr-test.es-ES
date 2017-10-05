---
title: "Purga de un punto de conexión de red CDN de Azure| Microsoft Docs"
description: "Aprenda a purgar todo el contenido almacenado en caché en un punto de conexión de la red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="b4ff2-103">Purgar un punto de conexión de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="b4ff2-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="b4ff2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b4ff2-104">Overview</span></span>
<span data-ttu-id="b4ff2-105">Los nodos perimetrales de la red CDN almacenarán recursos en caché hasta que el período de vida de dichos recursos (TTL) expire.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="b4ff2-106">Tras la expiración del TTL del activo, cuando un cliente solicite el activo desde el nodo perimetral, este nodo recuperará una nueva copia actualizada del activo para atender la solicitud de cliente y almacenar actualizada la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="b4ff2-107">El procedimiento recomendado para asegurarse de que los usuarios siempre obtengan la copia más reciente de los recursos es crear versiones correspondientes a cada actualización y publicarlos como nuevas URL.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="b4ff2-108">La red CDN recuperará inmediatamente los nuevos recursos en las siguientes solicitudes de los clientes.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="b4ff2-109">A veces puede que quiera purgar contenido almacenado en caché de todos los nodos perimetrales y forzarlos todos para recuperar nuevos activos actualizados.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="b4ff2-110">Esto puede deberse a actualizaciones de la aplicación web o a actualizaciones rápidas de los activos de actualización que contienen información incorrecta.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="b4ff2-111">Tenga en cuenta que el purgado solo borra el contenido almacenado en caché de los servidores perimetrales de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="b4ff2-112">Es posible que las cachés de nivel inferior, como las cachés de servidores proxy y de explorador local, aún contengan una copia en caché del archivo.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="b4ff2-113">Es importante que recuerde esto cuando defina el período de vida de un archivo.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="b4ff2-114">Para hacer que un cliente de nivel inferior solicite la versión más reciente del archivo, asígnele un nombre único cada vez que lo actualice o use el [almacenamiento en caché de cadenas de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="b4ff2-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="b4ff2-115">Este tutorial le guiará a través de purga de los recursos de todos los nodos perimetrales de un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="b4ff2-116">Tutorial</span><span class="sxs-lookup"><span data-stu-id="b4ff2-116">Walkthrough</span></span>
1. <span data-ttu-id="b4ff2-117">En el [Portal de Azure](https://portal.azure.com), examine el perfil de red CDN que contiene el punto de conexión que quiera purgar.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="b4ff2-118">En la hoja Perfil de CDN, haga clic en el botón para purgar.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![Hoja del perfil de red CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="b4ff2-120">Abre la hoja para purgar.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-120">The Purge blade opens.</span></span>
   
    ![Hoja de purga de red CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="b4ff2-122">En la hoja para purgar, seleccione la dirección del servicio que quiera purgar en la lista desplegable de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Formulario para purgar](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="b4ff2-124">También puede obtener acceso a la hoja para purgar haciendo clic en el botón **Purgar** de la hoja del punto de conexión de red de CDN.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="b4ff2-125">En ese caso, el campo **URL** se rellenará previamente con la dirección del servicio de ese punto de conexión concreto.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="b4ff2-126">Seleccione los activos que quiera purgar de los nodos perimetrales.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="b4ff2-127">Si quiere borrar todos los recursos, haga clic en la casilla **Purgar todo** .</span><span class="sxs-lookup"><span data-stu-id="b4ff2-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="b4ff2-128">De lo contrario, escriba la ruta de acceso completa de cada recurso que quiera purgar en el cuadro de texto **Ruta de acceso**.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="b4ff2-129">Los siguientes formatos se pueden usar en las rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="b4ff2-130">**Purga con una sola URL**: purgue recursos concretos especificando la URL completa, con o sin la extensión de archivo; por ejemplo,`/pictures/strasbourg.png`; `/pictures/strasbourg`.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="b4ff2-131">**Purga con carácter comodín**: se puede usar el asterisco (\*) como carácter comodín.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="b4ff2-132">Purgue todas las carpetas, subcarpetas y archivos de un punto de conexión con `/*` en la ruta de acceso o todas las subcarpetas y archivos de una carpeta concreta especificando la carpeta seguido de `/*`; por ejemplo, `/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="b4ff2-133">Tenga en cuenta que, en estos momentos, la purga de carácter comodín no es compatible con la red CDN de Azure de Akamai.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="b4ff2-134">**Purga de dominio raíz**: purgue la raíz del punto de conexión con "/" en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b4ff2-135">Las rutas de acceso que se van a purgar deben especificarse y ser una URL relativa que se ajuste a la siguiente [expresión regular](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4ff2-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="b4ff2-136">**Purgar todo** y la **purga con carácter comodín** no son compatibles en estos momentos con la **red CDN de Azure de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="b4ff2-137">Purga con una sola URL `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="b4ff2-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="b4ff2-138">Cadena de consulta `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="b4ff2-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="b4ff2-139">Purga con carácter comodín `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`</span><span class="sxs-lookup"><span data-stu-id="b4ff2-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="b4ff2-140">Aparecerán más cuadros de texto de **Ruta de acceso** después de escribir texto para permitirle crear una lista de varios activos.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="b4ff2-141">Puede eliminar activos en la lista haciendo clic en el botón de puntos suspensivos (...).</span><span class="sxs-lookup"><span data-stu-id="b4ff2-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="b4ff2-142">Haga clic en el botón **Purgar** .</span><span class="sxs-lookup"><span data-stu-id="b4ff2-142">Click the **Purge** button.</span></span>
   
    ![Botón Purgar](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="b4ff2-144">Las solicitudes de purga tardan aproximadamente de 2 a 3 minutos en procesarse con la **red CDN de Azure de Verizon** (estándar y premium) y unos 7 minutos con la **red CDN de Azure de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="b4ff2-145">La red CDN de Azure tiene un límite de 50 solicitudes de purga simultáneas en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="b4ff2-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="b4ff2-146">Consulte también</span><span class="sxs-lookup"><span data-stu-id="b4ff2-146">See also</span></span>
* [<span data-ttu-id="b4ff2-147">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="b4ff2-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="b4ff2-148">Referencia de la API de REST de red de CDN de Azure - purgar o cargar previamente un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="b4ff2-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

