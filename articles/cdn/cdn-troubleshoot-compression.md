---
title: "compresión de archivo aaaTroubleshooting en la red CDN de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="1ae0f-103">Solución de problemas de compresión de archivos de red CDN</span><span class="sxs-lookup"><span data-stu-id="1ae0f-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="1ae0f-104">Este artículo le ayudará a solucionar los problemas con la [compresión de archivos de red CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="1ae0f-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="1ae0f-105">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1ae0f-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1ae0f-106">Como alternativa, también puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="1ae0f-107">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="1ae0f-108">Síntoma</span><span class="sxs-lookup"><span data-stu-id="1ae0f-108">Symptom</span></span>
<span data-ttu-id="1ae0f-109">Está habilitada la compresión para el punto de conexión, pero se devuelven archivos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="1ae0f-110">toocheck si se devuelven los archivos comprimidos, necesita toouse una herramienta como [Fiddler](http://www.telerik.com/fiddler) o el explorador [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="1ae0f-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="1ae0f-111">Encabezados de respuesta de comprobación Hola HTTP devuelvan con la red CDN en caché contenidos.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="1ae0f-112">Si hay un encabezado denominado `Content-Encoding` con un valor de **gzip**, **bzip2**, o **deflate**, el contenido se comprime.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Encabezado content-encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="1ae0f-114">Causa</span><span class="sxs-lookup"><span data-stu-id="1ae0f-114">Cause</span></span>
<span data-ttu-id="1ae0f-115">Hay varias causas posibles, por nombrar algunas:</span><span class="sxs-lookup"><span data-stu-id="1ae0f-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="1ae0f-116">Hola solicitado no es elegible para la compresión de contenido.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="1ae0f-117">La compresión no está habilitada para hello solicita el tipo de archivo.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="1ae0f-118">solicitud HTTP de Hello no incluía un encabezado que solicita un tipo de compresión válidos.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="1ae0f-119">Pasos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="1ae0f-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="1ae0f-120">Al igual que con la implementación de nuevos puntos de conexión, los cambios de configuración de red CDN tienen algunos toopropagate tiempo a través de la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="1ae0f-121">Normalmente, los cambios se aplican en un plazo de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="1ae0f-122">Si se trata de hello primera vez que se ha establecido la compresión para el punto de conexión, considere la posibilidad de 1 y 2 horas toobe seguro de los valores de compresión de hello propagaron toohello POP en espera.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="1ae0f-123">Comprobar la solicitud Hola</span><span class="sxs-lookup"><span data-stu-id="1ae0f-123">Verify hello request</span></span>
<span data-ttu-id="1ae0f-124">En primer lugar, debemos hacer una comprobación rápida en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="1ae0f-125">Puede usar el explorador [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello las solicitudes realizadas.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="1ae0f-126">Compruebe la solicitud de saludo se enviaran a dirección URL del extremo de tooyour, `<endpointname>.azureedge.net`y no su origen.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="1ae0f-127">Compruebe la solicitud de hello contiene un **Accept-Encoding** hello y encabezado el valor de ese encabezado contiene **gzip**, **deflate**, o **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="1ae0f-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="1ae0f-128">Los perfiles de la **red CDN de Azure de Akamai** solo admiten la codificación **gzip**.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Encabezados de solicitud de red CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="1ae0f-130">Comprobar la configuración de compresión (perfil de red CDN estándar)</span><span class="sxs-lookup"><span data-stu-id="1ae0f-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="1ae0f-131">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN estándar de Azure de Verizon** o de **red CDN estándar de Azure de Akamai**.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="1ae0f-132">Navegar por el extremo de tooyour en hello [portal de Azure](https://portal.azure.com) y haga clic en hello **configurar** botón.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="1ae0f-133">Compruebe que la compresión está habilitada.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="1ae0f-134">Compruebe el tipo MIME que Hola Hola contenido toobe comprimido está incluido en lista de Hola de formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Configuración de compresión de red CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="1ae0f-136">Comprobar la configuración de compresión (perfil de red CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="1ae0f-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="1ae0f-137">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN Premium de Azure de Verizon** .</span><span class="sxs-lookup"><span data-stu-id="1ae0f-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="1ae0f-138">Navegar por el extremo de tooyour en hello [portal de Azure](https://portal.azure.com) y haga clic en hello **administrar** botón.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="1ae0f-139">se abrirá el portal complementario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="1ae0f-140">Mantenga el mouse sobre hello **HTTP grandes** ficha y, a continuación, mantenga el mouse sobre hello **configuración de la caché** ventana flotante.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="1ae0f-141">Haga clic en **Compresión**.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-141">Click **Compression**.</span></span> 

* <span data-ttu-id="1ae0f-142">Compruebe que la compresión está habilitada.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="1ae0f-143">Comprobar hello **tipos de archivo** lista contiene una lista separada por comas (sin espacios) de los tipos MIME.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="1ae0f-144">Compruebe el tipo MIME que Hola Hola contenido toobe comprimido está incluido en lista de Hola de formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Configuración de compresión de red CDN Premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="1ae0f-146">Compruebe que se almacena en caché el contenido de Hola</span><span class="sxs-lookup"><span data-stu-id="1ae0f-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="1ae0f-147">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN de Verizon** (Estándar o Premium).</span><span class="sxs-lookup"><span data-stu-id="1ae0f-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="1ae0f-148">Con herramientas de desarrollo de su explorador, compruebe el archivo hello tooensure encabezados de respuesta de Hola se almacena en caché en la región de Hola donde se solicita.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="1ae0f-149">Comprobar hello **Server** encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="1ae0f-150">encabezado de Hello debe tener formato de hello **plataforma (Id. de servidor/POP)**, tal como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="1ae0f-151">Comprobar hello **X caché** encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="1ae0f-152">debe leer el encabezado de Hello **ACIERTOS**.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-152">hello header should read **HIT**.</span></span>  

![Encabezados de respuesta de red CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="1ae0f-154">Compruebe el archivo hello cumple los requisitos de tamaño de Hola</span><span class="sxs-lookup"><span data-stu-id="1ae0f-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="1ae0f-155">Este paso solo se aplica si el perfil de red CDN es un perfil de **red CDN de Verizon** (Estándar o Premium).</span><span class="sxs-lookup"><span data-stu-id="1ae0f-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="1ae0f-156">toobe apta para la compresión, un archivo debe cumplir Hola según los requisitos de tamaño:</span><span class="sxs-lookup"><span data-stu-id="1ae0f-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="1ae0f-157">Mayor que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="1ae0f-158">Menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="1ae0f-159">Compruebe la solicitud de hello en el servidor de origen de hello para un **a través de** encabezado</span><span class="sxs-lookup"><span data-stu-id="1ae0f-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="1ae0f-160">Hola **a través de** encabezado HTTP indica el servidor de web toohello que Hola solicitud se pasa por un servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="1ae0f-161">Servidores web de Microsoft IIS de forma predeterminada no comprimen las respuestas cuando la solicitud de hello contiene un **a través de** encabezado.</span><span class="sxs-lookup"><span data-stu-id="1ae0f-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="1ae0f-162">toooverride este comportamiento, realizar Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1ae0f-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="1ae0f-163">**IIS 6**: [establecer HcNoCompressionForProxies = "FALSE" en Propiedades de la Metabase de IIS de Hola](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="1ae0f-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="1ae0f-164">**IIS 7 y hasta**: [establecer **noCompressionForHttp10** y **noCompressionForProxies** tooFalse en configuración del servidor hello](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="1ae0f-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

