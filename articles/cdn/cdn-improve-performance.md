---
title: rendimiento de aaaImprove al comprimir los archivos de red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de la transferencia de archivos de tooimprove velocidad y aumenta el rendimiento de carga de la página mediante la compresión de los archivos de red CDN de Azure."
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
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="7f200-103">Mejora del rendimiento comprimiendo archivos en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="7f200-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="7f200-104">La compresión es la velocidad de transferencia de archivos de tooimprove método sencillo y eficaz y aumento del rendimiento de carga de página al reducir el tamaño del archivo antes de que se envía desde el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="7f200-105">Este método reduce los costos de ancho de banda y proporciona una mayor capacidad de respuesta para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7f200-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="7f200-106">Hay dos maneras de compresión de tooenable:</span><span class="sxs-lookup"><span data-stu-id="7f200-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="7f200-107">Puede habilitar la compresión en el servidor de origen, en cuyo caso hello CDN pasa a través de hello archivos comprimidos y entrega archivos comprimidos tooclients que las solicitan.</span><span class="sxs-lookup"><span data-stu-id="7f200-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="7f200-108">Puede habilitar la compresión directamente en servidores perimetrales CDN, en la que comprime CDN Hola mayúsculas Hola archivos y servir a los usuarios tooend, incluso si no se comprimen mediante el servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f200-109">Cambios de configuración de red CDN tienen algunas toopropagate tiempo a través de la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="7f200-110">Para los perfiles de la <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completa en menos de un minuto.</span><span class="sxs-lookup"><span data-stu-id="7f200-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="7f200-111">Para los perfiles de la <b>red CDN de Azure de Verizon</b> , normalmente verá que los cambios se aplican en un período de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="7f200-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="7f200-112">Si se trata de hello primera vez que se ha establecido la compresión para el punto de conexión, considere la posibilidad de espera 1 y 2 horas toobe seguro de los valores de compresión de hello propagaron POP toohello antes de la solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7f200-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="7f200-113">Habilitar la compresión</span><span class="sxs-lookup"><span data-stu-id="7f200-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="7f200-114">proporcionan Hello niveles Standard y Premium CDN Hola la misma funcionalidad de compresión, pero difiere de hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7f200-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="7f200-115">Para obtener más información acerca de las diferencias de hello entre niveles Standard y Premium CDN, vea [información general sobre la red CDN de Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f200-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="7f200-116">Nivel Standard</span><span class="sxs-lookup"><span data-stu-id="7f200-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="7f200-117">En esta sección se aplica demasiado**estándar de red CDN de Azure de Verizon** y **estándar de red CDN de Azure de Akamai** perfiles.</span><span class="sxs-lookup"><span data-stu-id="7f200-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="7f200-118">En la página de perfil CDN Hola, haga clic en extremo de red CDN Hola desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="7f200-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Puntos de conexión de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="7f200-120">Abre la página de punto de conexión de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="7f200-121">Haga clic en hello **configurar** botón.</span><span class="sxs-lookup"><span data-stu-id="7f200-121">Click hello **Configure** button.</span></span>
   
    ![Botón de administración de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="7f200-123">Abre la página de configuración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="7f200-124">Active la **Compresión**.</span><span class="sxs-lookup"><span data-stu-id="7f200-124">Turn on **Compression**.</span></span>
   
    ![Opciones de compresión de red CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="7f200-126">Utilizar tipos de valor predeterminado de hello, o modificar lista de hello quitando o agregando los tipos de archivo.</span><span class="sxs-lookup"><span data-stu-id="7f200-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7f200-127">Mientras sea posible, se recomienda no tooapply compresión toocompressed formatos, como ZIP, MP3, MP4, JPG, etcetera.</span><span class="sxs-lookup"><span data-stu-id="7f200-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="7f200-128">Después de realizar los cambios, haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="7f200-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="7f200-129">Nivel Premium</span><span class="sxs-lookup"><span data-stu-id="7f200-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="7f200-130">En esta sección se aplica demasiado**Premium de CDN de Azure de Verizon** perfiles.</span><span class="sxs-lookup"><span data-stu-id="7f200-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="7f200-131">En la página de perfil CDN Hola, haga clic en hello **administrar** botón.</span><span class="sxs-lookup"><span data-stu-id="7f200-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Botón de administración de la página de perfil de la red CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="7f200-133">se abre el portal de administración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="7f200-134">Mantenga el mouse sobre hello **HTTP grandes** ficha y, a continuación, mantenga el mouse sobre hello **configuración de la caché** ventana flotante.</span><span class="sxs-lookup"><span data-stu-id="7f200-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="7f200-135">Haga clic en **Compresión**.</span><span class="sxs-lookup"><span data-stu-id="7f200-135">Click on **Compression**.</span></span>

    ![Selección de compresión de archivos](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="7f200-137">Se muestran las opciones de compresión.</span><span class="sxs-lookup"><span data-stu-id="7f200-137">Compression options are displayed.</span></span>
   
    ![Compresión de archivos](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="7f200-139">Habilitar la compresión, haga clic en hello **compresión habilitada** botón de radio.</span><span class="sxs-lookup"><span data-stu-id="7f200-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="7f200-140">Escriba los tipos MIME Hola indeterminado toocompress como una lista delimitada por comas (sin espacios) en hello **tipos de archivo** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="7f200-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7f200-141">Mientras sea posible, se recomienda no tooapply compresión toocompressed formatos, como ZIP, MP3, MP4, JPG, etcetera.</span><span class="sxs-lookup"><span data-stu-id="7f200-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="7f200-142">Después de realizar los cambios, haga clic en hello **actualización** botón.</span><span class="sxs-lookup"><span data-stu-id="7f200-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="7f200-143">Reglas de compresión</span><span class="sxs-lookup"><span data-stu-id="7f200-143">Compression rules</span></span>
<span data-ttu-id="7f200-144">Estas tablas describen el comportamiento de la compresión CDN de Azure para cada escenario.</span><span class="sxs-lookup"><span data-stu-id="7f200-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f200-145">En el caso de la **red CDN de Azure de Verizon** (estándar y premium), solo se comprimen determinados archivos válidos.</span><span class="sxs-lookup"><span data-stu-id="7f200-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="7f200-146">un archivo de toobe apta para la compresión, debe:</span><span class="sxs-lookup"><span data-stu-id="7f200-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="7f200-147">Debe tener más de 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="7f200-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="7f200-148">Debe tener menos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7f200-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="7f200-149">En el caso de la **red CDN de Azure de Akamai**, todos los archivos son válidos para la compresión.</span><span class="sxs-lookup"><span data-stu-id="7f200-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="7f200-150">Para todos los productos de la red CDN de Azure, un archivo debe tener un tipo MIME [configurado para compresión](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="7f200-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="7f200-151">Los perfiles de **CDN de Azure de Verizon** (Standard y Premium) admiten la codificación **gzip** (GNU zip), **deflate**, **bzip2** o **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="7f200-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="7f200-152">Para la codificación Brotli, compresión de Hola se realiza solo en el perímetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f200-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="7f200-153">Hola/explorador del cliente debe enviar la solicitud de Hola de codificación Brotli y activos comprimido Hola deben se han comprimido en el lado de origen de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="7f200-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="7f200-154">Los perfiles de **CDN de Azure de Akamai** solo admiten la codificación **gzip**.</span><span class="sxs-lookup"><span data-stu-id="7f200-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="7f200-155">**Azure CDN de Akamai** puntos de conexión siempre solicitarán **gzip** archivos de origen de hello, independientemente de la solicitud de cliente hello codificados.</span><span class="sxs-lookup"><span data-stu-id="7f200-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="7f200-156">La compresión está deshabilitada o el archivo no es elegible para la compresión</span><span class="sxs-lookup"><span data-stu-id="7f200-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="7f200-157">Formato solicitado por el cliente (mediante el encabezado Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="7f200-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="7f200-158">Formato de archivo almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="7f200-158">Cached file format</span></span> | <span data-ttu-id="7f200-159">Cliente de red CDN respuesta toohello</span><span class="sxs-lookup"><span data-stu-id="7f200-159">CDN response toohello client</span></span> | <span data-ttu-id="7f200-160">Notas</span><span class="sxs-lookup"><span data-stu-id="7f200-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7f200-161">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-161">Compressed</span></span> |<span data-ttu-id="7f200-162">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-162">Compressed</span></span> |<span data-ttu-id="7f200-163">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-163">Compressed</span></span> | |
| <span data-ttu-id="7f200-164">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-164">Compressed</span></span> |<span data-ttu-id="7f200-165">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-165">Uncompressed</span></span> |<span data-ttu-id="7f200-166">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-166">Uncompressed</span></span> | |
| <span data-ttu-id="7f200-167">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-167">Compressed</span></span> |<span data-ttu-id="7f200-168">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="7f200-168">Not cached</span></span> |<span data-ttu-id="7f200-169">Comprimidos o sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="7f200-170">Depende de la respuesta de origen</span><span class="sxs-lookup"><span data-stu-id="7f200-170">Depends on origin response</span></span> |
| <span data-ttu-id="7f200-171">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-171">Uncompressed</span></span> |<span data-ttu-id="7f200-172">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-172">Compressed</span></span> |<span data-ttu-id="7f200-173">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-173">Uncompressed</span></span> | |
| <span data-ttu-id="7f200-174">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-174">Uncompressed</span></span> |<span data-ttu-id="7f200-175">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-175">Uncompressed</span></span> |<span data-ttu-id="7f200-176">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-176">Uncompressed</span></span> | |
| <span data-ttu-id="7f200-177">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-177">Uncompressed</span></span> |<span data-ttu-id="7f200-178">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="7f200-178">Not cached</span></span> |<span data-ttu-id="7f200-179">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="7f200-180">La compresión está habilitada y el archivo es elegible para la compresión</span><span class="sxs-lookup"><span data-stu-id="7f200-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="7f200-181">Formato solicitado por el cliente (mediante el encabezado Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="7f200-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="7f200-182">Formato de archivo almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="7f200-182">Cached file format</span></span> | <span data-ttu-id="7f200-183">Cliente de red CDN respuesta toohello</span><span class="sxs-lookup"><span data-stu-id="7f200-183">CDN response toohello client</span></span> | <span data-ttu-id="7f200-184">Notas</span><span class="sxs-lookup"><span data-stu-id="7f200-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7f200-185">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-185">Compressed</span></span> |<span data-ttu-id="7f200-186">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-186">Compressed</span></span> |<span data-ttu-id="7f200-187">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-187">Compressed</span></span> |<span data-ttu-id="7f200-188">La red CDN transcodifica entre los formatos admitidos</span><span class="sxs-lookup"><span data-stu-id="7f200-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="7f200-189">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-189">Compressed</span></span> |<span data-ttu-id="7f200-190">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-190">Uncompressed</span></span> |<span data-ttu-id="7f200-191">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-191">Compressed</span></span> |<span data-ttu-id="7f200-192">La red CDN realiza la compresión</span><span class="sxs-lookup"><span data-stu-id="7f200-192">CDN performs compression</span></span> |
| <span data-ttu-id="7f200-193">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-193">Compressed</span></span> |<span data-ttu-id="7f200-194">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="7f200-194">Not cached</span></span> |<span data-ttu-id="7f200-195">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-195">Compressed</span></span> |<span data-ttu-id="7f200-196">La red CDN realiza la compresión si el origen se devuelve sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="7f200-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="7f200-197">**Red CDN de Azure de Verizon** pasadas Hola archivo sin comprimir en la primera solicitud de hello y, a continuación, comprime y memorias caché Hola archivo para las solicitudes posteriores.</span><span class="sxs-lookup"><span data-stu-id="7f200-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="7f200-198">Los archivos con el encabezado `Cache-Control: no-cache` nunca se comprimirán.</span><span class="sxs-lookup"><span data-stu-id="7f200-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="7f200-199">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-199">Uncompressed</span></span> |<span data-ttu-id="7f200-200">Comprimidos</span><span class="sxs-lookup"><span data-stu-id="7f200-200">Compressed</span></span> |<span data-ttu-id="7f200-201">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-201">Uncompressed</span></span> |<span data-ttu-id="7f200-202">La red CDN realiza la descompresión</span><span class="sxs-lookup"><span data-stu-id="7f200-202">CDN performs decompression</span></span> |
| <span data-ttu-id="7f200-203">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-203">Uncompressed</span></span> |<span data-ttu-id="7f200-204">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-204">Uncompressed</span></span> |<span data-ttu-id="7f200-205">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-205">Uncompressed</span></span> | |
| <span data-ttu-id="7f200-206">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-206">Uncompressed</span></span> |<span data-ttu-id="7f200-207">No almacenado en caché</span><span class="sxs-lookup"><span data-stu-id="7f200-207">Not cached</span></span> |<span data-ttu-id="7f200-208">Sin comprimir</span><span class="sxs-lookup"><span data-stu-id="7f200-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="7f200-209">Compresión de red CDN de servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="7f200-209">Media Services CDN Compression</span></span>
<span data-ttu-id="7f200-210">Media Services CDN ha habilitado los extremos de streaming, está habilitada la compresión predeterminada para los siguientes tipos de contenido de hello: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, aplicación/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="7f200-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="7f200-211">No puede habilitar o deshabilitar la compresión de hello mencionados tipos mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f200-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="7f200-212">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7f200-212">See also</span></span>
* [<span data-ttu-id="7f200-213">Solución de problemas de compresión de archivos de red CDN</span><span class="sxs-lookup"><span data-stu-id="7f200-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

