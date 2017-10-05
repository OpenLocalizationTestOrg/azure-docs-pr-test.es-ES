---
title: Mejora del rendimiento comprimiendo archivos en la red CDN de Azure | Microsoft Docs
description: "Este tema trata de cómo mejorar la velocidad de transferencia de archivos y aumentar el rendimiento de carga de páginas mediante la compresión de archivos en la red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="8c2d1-103">Mejora del rendimiento comprimiendo archivos en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="8c2d1-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="8c2d1-104">La compresión es un método sencillo y eficaz para mejorar la velocidad de transferencia de archivos y aumentar el rendimiento de carga de página al reducir el tamaño del archivo antes de que se envíe desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="8c2d1-105">Este método reduce los costos de ancho de banda y proporciona una mayor capacidad de respuesta para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="8c2d1-106">La compresión se puede habilitar de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="8c2d1-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="8c2d1-107">Puede habilitar la compresión en el servidor de origen, en cuyo caso la red CDN pasa los archivos comprimidos y los entrega a los clientes que los solicitan.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="8c2d1-108">Puede habilitar la compresión directamente en los servidores perimetrales de la red CDN, en cuyo caso esta red comprime los archivos y los entrega a los usuarios finales, aunque el servidor de origen no los haya comprimido.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c2d1-109">Los cambios en la configuración de la red CDN demoran un tiempo en propagarse por la red.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="8c2d1-110">Para los perfiles de la <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completa en menos de un minuto.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="8c2d1-111">Para los perfiles de la <b>red CDN de Azure de Verizon</b> , normalmente verá que los cambios se aplican en un período de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="8c2d1-112">Si esta es la primera vez que configura la compresión para su punto de conexión de la red CDN, debe considerar la posibilidad de esperar entre 1 y 2 horas para asegurarse de que la configuración de la compresión se haya propagado a los POP antes de realizar la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="8c2d1-113">Habilitar la compresión</span><span class="sxs-lookup"><span data-stu-id="8c2d1-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="8c2d1-114">Los niveles estándar y premium de CDN proporcionan la misma funcionalidad de compresión, pero la interfaz de usuario es distinta.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="8c2d1-115">Para obtener más información sobre las diferencias entre los niveles estándar y premium de CDN, consulte [Información general sobre la red CDN de Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c2d1-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="8c2d1-116">Nivel Standard</span><span class="sxs-lookup"><span data-stu-id="8c2d1-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="8c2d1-117">Esta sección es aplicable a perfiles de la **red CDN estándar de Azure de Verizon** y de la **red CDN estándar de Azure de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="8c2d1-118">En la página de perfil de la red CDN, haga clic en el punto de conexión de la red CDN que quiere administrar.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![Puntos de conexión de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="8c2d1-120">Se abre la página del punto de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="8c2d1-121">Elija el botón **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="8c2d1-121">Click the **Configure** button.</span></span>
   
    ![Botón de administración de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="8c2d1-123">Se abre la página de configuración de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="8c2d1-124">Active la **Compresión**.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-124">Turn on **Compression**.</span></span>
   
    ![Opciones de compresión de red CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="8c2d1-126">Use los tipos predeterminados o modifique la lista quitando o agregando los tipos de archivo.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8c2d1-127">Si bien es posible, no se recomienda aplicar compresión a formatos comprimidos, como ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="8c2d1-128">Tras efectuar los cambios, haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8c2d1-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="8c2d1-129">Nivel Premium</span><span class="sxs-lookup"><span data-stu-id="8c2d1-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="8c2d1-130">Esta sección es aplicable a perfiles de la **red CDN premium de Azure de Verizon** .</span><span class="sxs-lookup"><span data-stu-id="8c2d1-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="8c2d1-131">En la página de perfil de la red CDN, haga clic en el botón **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![Botón de administración de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="8c2d1-133">Se abre el portal de administración de CDN.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="8c2d1-134">Desplace el mouse sobre la pestaña **HTTP grande** y luego mantenga el mouse sobre el control flotante **Configuración de caché**.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="8c2d1-135">Haga clic en **Compresión**.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-135">Click on **Compression**.</span></span>

    ![Selección de compresión de archivos](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="8c2d1-137">Se muestran las opciones de compresión.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-137">Compression options are displayed.</span></span>
   
    ![Compresión de archivos](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="8c2d1-139">Habilite la compresión con un clic en el botón de selección **Compresión habilitada** .</span><span class="sxs-lookup"><span data-stu-id="8c2d1-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="8c2d1-140">Escriba los tipos de MIME que desea comprimir como una lista separada por comas (sin espacios) en el cuadro de texto **Tipos de archivo** .</span><span class="sxs-lookup"><span data-stu-id="8c2d1-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8c2d1-141">Si bien es posible, no se recomienda aplicar compresión a formatos comprimidos, como ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="8c2d1-142">Después de realizar los cambios, haga clic en el botón **Actualizar** .</span><span class="sxs-lookup"><span data-stu-id="8c2d1-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="8c2d1-143">Reglas de compresión</span><span class="sxs-lookup"><span data-stu-id="8c2d1-143">Compression rules</span></span>
<span data-ttu-id="8c2d1-144">Estas tablas describen el comportamiento de la compresión CDN de Azure para cada escenario.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c2d1-145">En el caso de la **red CDN de Azure de Verizon** (estándar y premium), solo se comprimen determinados archivos válidos.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="8c2d1-146">Para ser elegible para la compresión, un archivo debe cumplir con los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="8c2d1-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="8c2d1-147">Debe tener más de 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="8c2d1-148">Debe tener menos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="8c2d1-149">En el caso de la **red CDN de Azure de Akamai**, todos los archivos son válidos para la compresión.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="8c2d1-150">Para todos los productos de la red CDN de Azure, un archivo debe tener un tipo MIME [configurado para compresión](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="8c2d1-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="8c2d1-151">Los perfiles de **CDN de Azure de Verizon** (Standard y Premium) admiten la codificación **gzip** (GNU zip), **deflate**, **bzip2** o **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="8c2d1-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="8c2d1-152">En el caso de la codificación Brotli, la compresión se realiza únicamente en el servidor perimetral.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="8c2d1-153">El explorador o el cliente debe enviar la solicitud de codificación Brotli y el recurso comprimido debe haberse comprimido primero en el origen.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="8c2d1-154">Los perfiles de **CDN de Azure de Akamai** solo admiten la codificación **gzip**.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="8c2d1-155">Los puntos de conexión de la **red CDN de Azure de Akamai** siempre solicitan archivos codificados **gzip** al origen, independientemente de la solicitud del cliente.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="8c2d1-156">La compresión está deshabilitada o el archivo no es elegible para la compresión</span><span class="sxs-lookup"><span data-stu-id="8c2d1-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="8c2d1-157">Formato solicitado por el cliente (mediante el encabezado Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="8c2d1-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="8c2d1-158">Formato de archivo almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="8c2d1-158">Cached file format</span></span> | <span data-ttu-id="8c2d1-159">Respuesta de la red CDN al cliente</span><span class="sxs-lookup"><span data-stu-id="8c2d1-159">CDN response to the client</span></span> | <span data-ttu-id="8c2d1-160">Notas</span><span class="sxs-lookup"><span data-stu-id="8c2d1-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c2d1-161">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-161">Compressed</span></span> |<span data-ttu-id="8c2d1-162">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-162">Compressed</span></span> |<span data-ttu-id="8c2d1-163">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-163">Compressed</span></span> | |
| <span data-ttu-id="8c2d1-164">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-164">Compressed</span></span> |<span data-ttu-id="8c2d1-165">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-165">Uncompressed</span></span> |<span data-ttu-id="8c2d1-166">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-166">Uncompressed</span></span> | |
| <span data-ttu-id="8c2d1-167">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-167">Compressed</span></span> |<span data-ttu-id="8c2d1-168">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="8c2d1-168">Not cached</span></span> |<span data-ttu-id="8c2d1-169">Comprimidos o sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="8c2d1-170">Depende de la respuesta de origen</span><span class="sxs-lookup"><span data-stu-id="8c2d1-170">Depends on origin response</span></span> |
| <span data-ttu-id="8c2d1-171">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-171">Uncompressed</span></span> |<span data-ttu-id="8c2d1-172">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-172">Compressed</span></span> |<span data-ttu-id="8c2d1-173">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-173">Uncompressed</span></span> | |
| <span data-ttu-id="8c2d1-174">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-174">Uncompressed</span></span> |<span data-ttu-id="8c2d1-175">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-175">Uncompressed</span></span> |<span data-ttu-id="8c2d1-176">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-176">Uncompressed</span></span> | |
| <span data-ttu-id="8c2d1-177">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-177">Uncompressed</span></span> |<span data-ttu-id="8c2d1-178">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="8c2d1-178">Not cached</span></span> |<span data-ttu-id="8c2d1-179">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="8c2d1-180">La compresión está habilitada y el archivo es elegible para la compresión</span><span class="sxs-lookup"><span data-stu-id="8c2d1-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="8c2d1-181">Formato solicitado por el cliente (mediante el encabezado Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="8c2d1-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="8c2d1-182">Formato de archivo almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="8c2d1-182">Cached file format</span></span> | <span data-ttu-id="8c2d1-183">Respuesta de la red CDN al cliente</span><span class="sxs-lookup"><span data-stu-id="8c2d1-183">CDN response to the client</span></span> | <span data-ttu-id="8c2d1-184">Notas</span><span class="sxs-lookup"><span data-stu-id="8c2d1-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c2d1-185">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-185">Compressed</span></span> |<span data-ttu-id="8c2d1-186">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-186">Compressed</span></span> |<span data-ttu-id="8c2d1-187">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-187">Compressed</span></span> |<span data-ttu-id="8c2d1-188">La red CDN transcodifica entre los formatos admitidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="8c2d1-189">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-189">Compressed</span></span> |<span data-ttu-id="8c2d1-190">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-190">Uncompressed</span></span> |<span data-ttu-id="8c2d1-191">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-191">Compressed</span></span> |<span data-ttu-id="8c2d1-192">La red CDN realiza la compresión</span><span class="sxs-lookup"><span data-stu-id="8c2d1-192">CDN performs compression</span></span> |
| <span data-ttu-id="8c2d1-193">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-193">Compressed</span></span> |<span data-ttu-id="8c2d1-194">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="8c2d1-194">Not cached</span></span> |<span data-ttu-id="8c2d1-195">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-195">Compressed</span></span> |<span data-ttu-id="8c2d1-196">La red CDN realiza la compresión si el origen se devuelve sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="8c2d1-197">**CDN de Azure de Verizon** pasa el archivo descomprimido en la primera solicitud y luego lo comprime y lo almacena en caché para solicitudes posteriores.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="8c2d1-198">Los archivos con el encabezado `Cache-Control: no-cache` nunca se comprimirán.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="8c2d1-199">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-199">Uncompressed</span></span> |<span data-ttu-id="8c2d1-200">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="8c2d1-200">Compressed</span></span> |<span data-ttu-id="8c2d1-201">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-201">Uncompressed</span></span> |<span data-ttu-id="8c2d1-202">La red CDN realiza la descompresión</span><span class="sxs-lookup"><span data-stu-id="8c2d1-202">CDN performs decompression</span></span> |
| <span data-ttu-id="8c2d1-203">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-203">Uncompressed</span></span> |<span data-ttu-id="8c2d1-204">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-204">Uncompressed</span></span> |<span data-ttu-id="8c2d1-205">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-205">Uncompressed</span></span> | |
| <span data-ttu-id="8c2d1-206">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-206">Uncompressed</span></span> |<span data-ttu-id="8c2d1-207">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="8c2d1-207">Not cached</span></span> |<span data-ttu-id="8c2d1-208">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="8c2d1-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="8c2d1-209">Compresión de red CDN de servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="8c2d1-209">Media Services CDN Compression</span></span>
<span data-ttu-id="8c2d1-210">Para los puntos de conexión de streaming habilitados para la red CDN de Servicios multimedia, la compresión está habilitada de forma predeterminada para los siguientes tipos de contenido: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="8c2d1-211">No se puede habilitar o deshabilitar la compresión de los tipos mencionados mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2d1-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8c2d1-212">Consulte también</span><span class="sxs-lookup"><span data-stu-id="8c2d1-212">See also</span></span>
* [<span data-ttu-id="8c2d1-213">Solución de problemas de compresión de archivos de red CDN</span><span class="sxs-lookup"><span data-stu-id="8c2d1-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

