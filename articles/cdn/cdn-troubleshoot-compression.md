---
title: "Solución de problemas de compresión de archivos en la red CDN de Azure | Microsoft Docs"
description: "Solucione los problemas con la compresión de archivos de la red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="02eb6-103">Solución de problemas de compresión de archivos de red CDN</span><span class="sxs-lookup"><span data-stu-id="02eb6-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="02eb6-104">Este artículo le ayudará a solucionar los problemas con la [compresión de archivos de red CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="02eb6-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="02eb6-105">Si necesita más ayuda en cualquier punto de este artículo, puede ponerse en contacto con los expertos de Azure en [los foros de MSDN Azure o de desbordamiento de pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="02eb6-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="02eb6-106">Como alternativa, también puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="02eb6-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="02eb6-107">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Obtener soporte**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="02eb6-108">Síntoma</span><span class="sxs-lookup"><span data-stu-id="02eb6-108">Symptom</span></span>
<span data-ttu-id="02eb6-109">Está habilitada la compresión para el punto de conexión, pero se devuelven archivos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="02eb6-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="02eb6-110">Para comprobar si los archivos se devuelven comprimidos, debe usar una herramienta como [Fiddler](http://www.telerik.com/fiddler) o las [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) del explorador.</span><span class="sxs-lookup"><span data-stu-id="02eb6-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="02eb6-111">Compruebe los encabezados de respuesta HTTP que se devuelven con el contenido CDN en caché.</span><span class="sxs-lookup"><span data-stu-id="02eb6-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="02eb6-112">Si hay un encabezado denominado `Content-Encoding` con un valor de **gzip**, **bzip2**, o **deflate**, el contenido se comprime.</span><span class="sxs-lookup"><span data-stu-id="02eb6-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Encabezado content-encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="02eb6-114">Causa</span><span class="sxs-lookup"><span data-stu-id="02eb6-114">Cause</span></span>
<span data-ttu-id="02eb6-115">Hay varias causas posibles, por nombrar algunas:</span><span class="sxs-lookup"><span data-stu-id="02eb6-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="02eb6-116">El contenido solicitado no es apto para la compresión.</span><span class="sxs-lookup"><span data-stu-id="02eb6-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="02eb6-117">La compresión no está habilitada para el tipo de archivo solicitado.</span><span class="sxs-lookup"><span data-stu-id="02eb6-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="02eb6-118">La solicitud HTTP no incluía un encabezado que solicitara un tipo de compresión válido.</span><span class="sxs-lookup"><span data-stu-id="02eb6-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="02eb6-119">Pasos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="02eb6-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="02eb6-120">Al igual que lo que ocurre cuando se implementan puntos de conexión nuevos, los cambios en la configuración de la red CDN demoran un tiempo en propagarse por la red.</span><span class="sxs-lookup"><span data-stu-id="02eb6-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="02eb6-121">Normalmente, los cambios se aplican en un plazo de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="02eb6-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="02eb6-122">Si esta es la primera vez que configura la compresión para su punto de conexión de la red CDN, debe considerar una espera de 1 o 2 horas para asegurarse de que la configuración de la compresión se propagó a los POP.</span><span class="sxs-lookup"><span data-stu-id="02eb6-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="02eb6-123">Comprobar la solicitud</span><span class="sxs-lookup"><span data-stu-id="02eb6-123">Verify the request</span></span>
<span data-ttu-id="02eb6-124">En primer lugar, se debe hacer una comprobación rápida en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="02eb6-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="02eb6-125">Puede usar las [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) del explorador para ver las solicitudes que se realizan.</span><span class="sxs-lookup"><span data-stu-id="02eb6-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="02eb6-126">Compruebe que la solicitud se envía a la dirección URL del punto de conexión, `<endpointname>.azureedge.net`, y no a su origen.</span><span class="sxs-lookup"><span data-stu-id="02eb6-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="02eb6-127">Compruebe que la solicitud contenga un encabezado **Accept-Encoding** y que el valor para el encabezado contenga **gzip**, **deflate** o **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="02eb6-128">Los perfiles de la **red CDN de Azure de Akamai** solo admiten la codificación **gzip**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Encabezados de solicitud de red CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="02eb6-130">Comprobar la configuración de compresión (perfil de red CDN estándar)</span><span class="sxs-lookup"><span data-stu-id="02eb6-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="02eb6-131">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN estándar de Azure de Verizon** o de **red CDN estándar de Azure de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="02eb6-132">Desplácese hasta el punto de conexión en [Azure Portal](https://portal.azure.com) y haga clic en el botón **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="02eb6-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="02eb6-133">Compruebe que la compresión está habilitada.</span><span class="sxs-lookup"><span data-stu-id="02eb6-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="02eb6-134">Compruebe que el tipo MIME del contenido que se va a comprimir se incluya en la lista de formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="02eb6-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Configuración de compresión de red CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="02eb6-136">Comprobar la configuración de compresión (perfil de red CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="02eb6-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="02eb6-137">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN Premium de Azure de Verizon** .</span><span class="sxs-lookup"><span data-stu-id="02eb6-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="02eb6-138">Desplácese hasta el punto de conexión en [Azure Portal](https://portal.azure.com) y haga clic en el botón **Administrar** .</span><span class="sxs-lookup"><span data-stu-id="02eb6-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="02eb6-139">Se abrirá el portal complementario.</span><span class="sxs-lookup"><span data-stu-id="02eb6-139">The supplemental portal will open.</span></span>  <span data-ttu-id="02eb6-140">Desplace el mouse sobre la pestaña **HTTP grande** y luego mantenga el mouse sobre el control flotante **Configuración de caché**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="02eb6-141">Haga clic en **Compresión**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-141">Click **Compression**.</span></span> 

* <span data-ttu-id="02eb6-142">Compruebe que la compresión está habilitada.</span><span class="sxs-lookup"><span data-stu-id="02eb6-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="02eb6-143">Compruebe que la lista de **Tipos de archivo** contiene una lista de tipos MIME separados por coma (sin espacios).</span><span class="sxs-lookup"><span data-stu-id="02eb6-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="02eb6-144">Compruebe que el tipo MIME del contenido que se va a comprimir se incluya en la lista de formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="02eb6-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Configuración de compresión de red CDN Premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="02eb6-146">Comprobar que el contenido se almacena en caché</span><span class="sxs-lookup"><span data-stu-id="02eb6-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="02eb6-147">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN de Verizon** (Estándar o Premium).</span><span class="sxs-lookup"><span data-stu-id="02eb6-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="02eb6-148">Con las herramientas para desarrolladores de su explorador, compruebe los encabezados de respuesta para asegurarse de que el archivo se almacena en caché en la región donde se solicita.</span><span class="sxs-lookup"><span data-stu-id="02eb6-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="02eb6-149">Compruebe el encabezado de respuesta **Server** .</span><span class="sxs-lookup"><span data-stu-id="02eb6-149">Check the **Server** response header.</span></span>  <span data-ttu-id="02eb6-150">El encabezado debe tener el formato **Plataforma (POP/id. de servidor)**, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="02eb6-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="02eb6-151">Compruebe el encabezado de respuesta **X-Cache** .</span><span class="sxs-lookup"><span data-stu-id="02eb6-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="02eb6-152">Debe poner **HIT**.</span><span class="sxs-lookup"><span data-stu-id="02eb6-152">The header should read **HIT**.</span></span>  

![Encabezados de respuesta de red CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="02eb6-154">Comprobar que el archivo cumple los requisitos de tamaño</span><span class="sxs-lookup"><span data-stu-id="02eb6-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="02eb6-155">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN de Verizon** (Estándar o Premium).</span><span class="sxs-lookup"><span data-stu-id="02eb6-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="02eb6-156">Para que un archivo sea apto para la compresión, debe cumplir los siguientes requisitos de tamaño:</span><span class="sxs-lookup"><span data-stu-id="02eb6-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="02eb6-157">Mayor que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="02eb6-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="02eb6-158">Menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="02eb6-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="02eb6-159">Compruebe la solicitud en el servidor de origen para un encabezado **Mediante**</span><span class="sxs-lookup"><span data-stu-id="02eb6-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="02eb6-160">El encabezado **Mediante** HTTP indica al servidor web que un servidor proxy pasará la solicitud.</span><span class="sxs-lookup"><span data-stu-id="02eb6-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="02eb6-161">De forma predeterminada, los servidores web de Microsoft IIS no comprimen las respuestas si la solicitud contiene un encabezado **Mediante** .</span><span class="sxs-lookup"><span data-stu-id="02eb6-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="02eb6-162">Para anular este comportamiento, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="02eb6-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="02eb6-163">**IIS 6**: [Establezca HcNoCompressionForProxies = "FALSE" en las propiedades de la metabase de IIS](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="02eb6-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="02eb6-164">**IIS 7 y posteriores**: [Establezca **noCompressionForHttp10** y **noCompressionForProxies** en False en la configuración del servidor](http://www.iis.net/configreference/system.webserver/httpcompression).</span><span class="sxs-lookup"><span data-stu-id="02eb6-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

