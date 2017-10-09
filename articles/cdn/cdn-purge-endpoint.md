---
title: "aaaPurge un punto de conexión de red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopurge todos los almacena en caché contenido desde un punto de conexión de red CDN de Azure."
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
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="c5fa9-103">Purgar un punto de conexión de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="c5fa9-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="c5fa9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c5fa9-104">Overview</span></span>
<span data-ttu-id="c5fa9-105">Nodos de borde CDN de Azure almacenará en memoria caché activos hasta que expire el período de vida (TTL) del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="c5fa9-106">Después de que expire TTL del recurso de hello, cuando un cliente solicita asset Hola desde el nodo del borde de hello, nodo de hello borde recuperará una nueva copia actualizada de solicitud de cliente de hello asset tooserve hello y almacenar Hola de actualización de caché.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="c5fa9-107">toomake de prácticas recomendada de Hello seguro a los usuarios obtengan siempre la copia más reciente de Hola de sus activos es tooversion sus activos para cada actualización y publican como nuevas direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="c5fa9-108">CDN recuperará inmediatamente nuevos activos de Hola Hola siguiente las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="c5fa9-109">En ocasiones, es recomendable toopurge almacenado en caché contenido de todos los nodos de borde y hacer a todos los tooretrieve nuevos activos actualizados.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="c5fa9-110">Esto podría ser debido a la aplicación web de tooupdates tooyour, o los activos de la actualización de tooquickly que contengan información incorrecta.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="c5fa9-111">Tenga en cuenta que sólo purga borra Hola almacenado en caché contenido en los servidores de borde CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="c5fa9-112">Todas las cachés de nivel inferiores, como servidores proxy y cachés de explorador local, todavía pueden albergar una copia en caché de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="c5fa9-113">Es importante tooremember esto al establecer un archivo período de vida.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="c5fa9-114">Puede forzar una versión más reciente de cliente de nivel inferior toorequest Hola del archivo asignándole un nombre único cada vez que lo actualice o aprovechando las ventajas de [almacenamiento en memoria caché en la cadena de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="c5fa9-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="c5fa9-115">Este tutorial le guiará a través de purga de los recursos de todos los nodos perimetrales de un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="c5fa9-116">Tutorial</span><span class="sxs-lookup"><span data-stu-id="c5fa9-116">Walkthrough</span></span>
1. <span data-ttu-id="c5fa9-117">Hola [Portal de Azure](https://portal.azure.com), examinar el perfil de CDN toohello que contiene el punto de conexión de hello desea toopurge.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="c5fa9-118">Desde la hoja de perfil CDN Hola, haga clic en el botón de purga de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Hoja del perfil de red CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="c5fa9-120">se abre la hoja de purga de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-120">hello Purge blade opens.</span></span>
   
    ![Hoja de purga de red CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="c5fa9-122">En hello purgar hoja, seleccione la dirección del servicio Hola desea toopurge de lista desplegable de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Formulario para purgar](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="c5fa9-124">También puede obtener toohello purga hoja haciendo clic en hello **purgar** botón en la hoja de punto de conexión de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="c5fa9-125">En ese caso, Hola **URL** campo se rellenará automáticamente con la dirección de servicio de Hola de ese punto de conexión concreto.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="c5fa9-126">Seleccione qué activos desea toopurge de hello nodos perimetrales.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="c5fa9-127">Si desea que todos los activos tooclear, haga clic en hello **purgar todo** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="c5fa9-128">En caso contrario, ruta de acceso de tipo hello de cada recurso que se va toopurge Hola **ruta de acceso** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="c5fa9-129">Por debajo de los formatos son compatibles con la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="c5fa9-130">**Purga de dirección URL única**: purga activo individual especificando la dirección URL completa de hello, con o sin la extensión de archivo hello, p. ej.,`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="c5fa9-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="c5fa9-131">**Purga con carácter comodín**: se puede usar el asterisco (\*) como carácter comodín.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="c5fa9-132">Purgar todas las carpetas, subcarpetas y archivos en un punto de conexión con `/*` en Hola ruta de acceso o purgar todas las subcarpetas y archivos en una carpeta específica mediante la especificación de la carpeta de hello seguido de `/*`, p. ej.,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="c5fa9-133">Tenga en cuenta que, en estos momentos, la purga de carácter comodín no es compatible con la red CDN de Azure de Akamai.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="c5fa9-134">**Purga de dominio raíz**: raíz de Hola de purga de punto de conexión de hello con "/" en la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c5fa9-135">Las rutas de acceso debe especificarse para purgar y debe ser una dirección URL relativa que se ajusten a siguiente hello [expresión regular](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5fa9-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="c5fa9-136">**Purgar todo** y la **purga con carácter comodín** no son compatibles en estos momentos con la **red CDN de Azure de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="c5fa9-137">Purga con una sola URL `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="c5fa9-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="c5fa9-138">Cadena de consulta `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="c5fa9-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="c5fa9-139">Purga con carácter comodín `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`</span><span class="sxs-lookup"><span data-stu-id="c5fa9-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="c5fa9-140">Más **ruta de acceso** cuadros de texto que aparecerá después de escribir texto tooallow toobuild una lista de varios activos.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="c5fa9-141">Puede eliminar los activos de lista de hello haciendo clic en el botón de puntos suspensivos (...) de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="c5fa9-142">Haga clic en hello **purgar** botón.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-142">Click hello **Purge** button.</span></span>
   
    ![Botón Purgar](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="c5fa9-144">Purgar las solicitudes tardar aproximadamente 2 a 3 minutos tooprocess con **CDN de Azure de Verizon** (Standard y Premium) y aproximadamente 7 minutos con **Azure CDN de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="c5fa9-145">La red CDN de Azure tiene un límite de 50 solicitudes de purga simultáneas en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="c5fa9-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="c5fa9-146">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c5fa9-146">See also</span></span>
* [<span data-ttu-id="c5fa9-147">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="c5fa9-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="c5fa9-148">Referencia de la API de REST de red de CDN de Azure - purgar o cargar previamente un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="c5fa9-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

