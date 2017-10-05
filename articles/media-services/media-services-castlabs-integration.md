---
title: Uso de castLabs para proporcionar licencias de Widevine a Azure Media Services | Microsoft Docs
description: "En este artículo se describe cómo puede usar Servicios multimedia de Azure (AMS) para entregar una secuencia que se cifra dinámicamente por AMS con DRM tanto de PlayReady como Widevine. La licencia de PlayReady procede del servidor de licencias PlayReady de Servicios multimedia y la licencia de Widevine se entrega al servidor de licencias de castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="09a6b-104">Uso de castLabs para entregar licencias de Widevine a Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="09a6b-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09a6b-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="09a6b-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="09a6b-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="09a6b-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="09a6b-107">Información general</span><span class="sxs-lookup"><span data-stu-id="09a6b-107">Overview</span></span>
<span data-ttu-id="09a6b-108">En este artículo se describe cómo puede usar Servicios multimedia de Azure (AMS) para entregar una secuencia que se cifra dinámicamente por AMS con DRM tanto de PlayReady como Widevine.</span><span class="sxs-lookup"><span data-stu-id="09a6b-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="09a6b-109">La licencia de PlayReady procede del servidor de licencias de PlayReady de Servicios multimedia y la licencia de Widevine se entrega por el servidor de licencias **castLabs** .</span><span class="sxs-lookup"><span data-stu-id="09a6b-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="09a6b-110">Para la reproducción de contenido en streaming protegido por CENC (PlayReady o Widevine), puede usar [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="09a6b-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="09a6b-111">Consulte el [documento AMP](http://amp.azure.net/libs/amp/latest/docs/) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="09a6b-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="09a6b-112">En el siguiente diagrama se muestra una arquitectura de integración de castLabs y Servicios multimedia de Azure de alto nivel.</span><span class="sxs-lookup"><span data-stu-id="09a6b-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integración](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="09a6b-114">Configuración de sistema típico</span><span class="sxs-lookup"><span data-stu-id="09a6b-114">Typical system set up</span></span>
* <span data-ttu-id="09a6b-115">El contenido multimedia se almacena en AMS.</span><span class="sxs-lookup"><span data-stu-id="09a6b-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="09a6b-116">Los id. de clave de claves de contenido se almacenan en castLabs y AMS.</span><span class="sxs-lookup"><span data-stu-id="09a6b-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="09a6b-117">Tanto castLabs como AMS tienen la autenticación de tokens integrada.</span><span class="sxs-lookup"><span data-stu-id="09a6b-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="09a6b-118">En las secciones siguientes se analizan los tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="09a6b-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="09a6b-119">Cuando un cliente solicita transmitir el vídeo, el contenido se cifra dinámicamente con **cifrado común** (CENC) y se empaqueta dinámicamente por AMS a Smooth Streaming y DASH.</span><span class="sxs-lookup"><span data-stu-id="09a6b-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="09a6b-120">También ofrecemos cifrado de streaming elemental de PlayReady M2TS para el protocolo de streaming HLS.</span><span class="sxs-lookup"><span data-stu-id="09a6b-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="09a6b-121">La licencia de PlayReady se recupera del servidor de licencias de AMS y la licencia de Widevine se recupera del servidor de licencias de castLabs.</span><span class="sxs-lookup"><span data-stu-id="09a6b-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="09a6b-122">El reproductor multimedia decide automáticamente qué licencia capturar basándose en la capacidad de la plataforma del cliente.</span><span class="sxs-lookup"><span data-stu-id="09a6b-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="09a6b-123">Generación de tokens de autenticación para obtener una licencia</span><span class="sxs-lookup"><span data-stu-id="09a6b-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="09a6b-124">Tanto castLabs como AMS admiten el formato de token JWT (token web JSON) usado para autorizar una licencia.</span><span class="sxs-lookup"><span data-stu-id="09a6b-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="09a6b-125">Token JWT en AMS</span><span class="sxs-lookup"><span data-stu-id="09a6b-125">JWT token in AMS</span></span>
<span data-ttu-id="09a6b-126">En la tabla siguiente se describen los tokens JWT en AMS.</span><span class="sxs-lookup"><span data-stu-id="09a6b-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="09a6b-127">Emisor</span><span class="sxs-lookup"><span data-stu-id="09a6b-127">Issuer</span></span> | <span data-ttu-id="09a6b-128">Cadena de emisor desde el servicio de tokens seguro (STS) elegido</span><span class="sxs-lookup"><span data-stu-id="09a6b-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="09a6b-129">Público</span><span class="sxs-lookup"><span data-stu-id="09a6b-129">Audience</span></span> |<span data-ttu-id="09a6b-130">Cadena de audiencia del STS usado</span><span class="sxs-lookup"><span data-stu-id="09a6b-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="09a6b-131">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="09a6b-131">Claims</span></span> |<span data-ttu-id="09a6b-132">Un conjunto de notificaciones</span><span class="sxs-lookup"><span data-stu-id="09a6b-132">A set of claims</span></span> |
| <span data-ttu-id="09a6b-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="09a6b-133">NotBefore</span></span> |<span data-ttu-id="09a6b-134">Iniciar la validez del token</span><span class="sxs-lookup"><span data-stu-id="09a6b-134">Start validity of the token</span></span> |
| <span data-ttu-id="09a6b-135">Expira</span><span class="sxs-lookup"><span data-stu-id="09a6b-135">Expires</span></span> |<span data-ttu-id="09a6b-136">Finalizar la validez del token</span><span class="sxs-lookup"><span data-stu-id="09a6b-136">End validity of the token</span></span> |
| <span data-ttu-id="09a6b-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="09a6b-137">SigningCredentials</span></span> |<span data-ttu-id="09a6b-138">La clave que se comparte entre el servidor de licencias de PlayReady, el servidor de licencias de castLabs y STS; podría ser una clave simétrica o asimétrica.</span><span class="sxs-lookup"><span data-stu-id="09a6b-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="09a6b-139">Token JWT en castLabs</span><span class="sxs-lookup"><span data-stu-id="09a6b-139">JWT token in castLabs</span></span>
<span data-ttu-id="09a6b-140">En la tabla siguiente se describen los tokens JWT en castLabs.</span><span class="sxs-lookup"><span data-stu-id="09a6b-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="09a6b-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="09a6b-141">Name</span></span> | <span data-ttu-id="09a6b-142">Description</span><span class="sxs-lookup"><span data-stu-id="09a6b-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09a6b-143">optData</span><span class="sxs-lookup"><span data-stu-id="09a6b-143">optData</span></span> |<span data-ttu-id="09a6b-144">Cadena JSON que contiene información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="09a6b-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="09a6b-145">crt</span><span class="sxs-lookup"><span data-stu-id="09a6b-145">crt</span></span> |<span data-ttu-id="09a6b-146">Cadena JSON que contiene información sobre el activo, su información de licencia y derechos de reproducción.</span><span class="sxs-lookup"><span data-stu-id="09a6b-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="09a6b-147">iat</span><span class="sxs-lookup"><span data-stu-id="09a6b-147">iat</span></span> |<span data-ttu-id="09a6b-148">La fecha y hora actual en la época.</span><span class="sxs-lookup"><span data-stu-id="09a6b-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="09a6b-149">jti</span><span class="sxs-lookup"><span data-stu-id="09a6b-149">jti</span></span> |<span data-ttu-id="09a6b-150">Identificador único sobre este token (cada token solo puede usarse una vez en el sistema castLabs).</span><span class="sxs-lookup"><span data-stu-id="09a6b-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="09a6b-151">Configuración de soluciones de ejemplo</span><span class="sxs-lookup"><span data-stu-id="09a6b-151">Sample solution set up</span></span>
<span data-ttu-id="09a6b-152">La [solución de ejemplo](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consta de dos proyectos:</span><span class="sxs-lookup"><span data-stu-id="09a6b-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="09a6b-153">Una aplicación de consola que puede usarse para establecer restricciones de DRM en un activo ya introducido, tanto para PlayReady como para Widevine.</span><span class="sxs-lookup"><span data-stu-id="09a6b-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="09a6b-154">Una aplicación web que distribuye tokens, que podrían considerarse como una versión MUY SIMPLIFICADA de un STS.</span><span class="sxs-lookup"><span data-stu-id="09a6b-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="09a6b-155">Para usar la aplicación de consola:</span><span class="sxs-lookup"><span data-stu-id="09a6b-155">To use the console application:</span></span>

1. <span data-ttu-id="09a6b-156">Cambie el archivo app.config para configurar las credenciales de AMS, las credenciales de castLabs, la configuración de STS y la clave compartida.</span><span class="sxs-lookup"><span data-stu-id="09a6b-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="09a6b-157">Cargue un activo en AMS.</span><span class="sxs-lookup"><span data-stu-id="09a6b-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="09a6b-158">Obtenga el UUID del recurso cargado y cambie la línea 32 del archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="09a6b-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="09a6b-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="09a6b-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="09a6b-160">Use un AssetId para asignar un nombre al activo del sistema castLabs (línea 44 del archivo Program.cs).</span><span class="sxs-lookup"><span data-stu-id="09a6b-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="09a6b-161">Debe establecer AssetId para **castLabs**; debe ser una cadena alfanumérica única.</span><span class="sxs-lookup"><span data-stu-id="09a6b-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="09a6b-162">Ejecute el programa.</span><span class="sxs-lookup"><span data-stu-id="09a6b-162">Run the program.</span></span>

<span data-ttu-id="09a6b-163">Para usar la aplicación web (STS):</span><span class="sxs-lookup"><span data-stu-id="09a6b-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="09a6b-164">Cambie el archivo web.config para configurar el id. de comerciante de castlabs, la configuración de STS y la clave compartida.</span><span class="sxs-lookup"><span data-stu-id="09a6b-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="09a6b-165">Implemente en Sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="09a6b-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="09a6b-166">Vaya al sitio web.</span><span class="sxs-lookup"><span data-stu-id="09a6b-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="09a6b-167">Reproducir un vídeo</span><span class="sxs-lookup"><span data-stu-id="09a6b-167">Playing back a video</span></span>
<span data-ttu-id="09a6b-168">Para reproducir un vídeo cifrado con cifrado común (PlayReady o Widevine), puede usar [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="09a6b-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="09a6b-169">Cuando se ejecuta la aplicación de consola, se reflejan el id. de clave de contenido y la dirección URL del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="09a6b-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="09a6b-170">Abra una nueva pestaña e inicie STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="09a6b-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="09a6b-171">Vaya al [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="09a6b-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="09a6b-172">Pegue la dirección URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="09a6b-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="09a6b-173">Haga clic en la casilla **Opciones avanzadas** .</span><span class="sxs-lookup"><span data-stu-id="09a6b-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="09a6b-174">En el menú desplegable **Protección** , seleccione PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="09a6b-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="09a6b-175">Pegue el token que obtuvo de su STS en el cuadro de texto Token.</span><span class="sxs-lookup"><span data-stu-id="09a6b-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="09a6b-176">El servidor de licencias de castLab no necesita el prefijo “Bearer=” delante del token.</span><span class="sxs-lookup"><span data-stu-id="09a6b-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="09a6b-177">Por tanto, quítelo antes de enviar el token.</span><span class="sxs-lookup"><span data-stu-id="09a6b-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="09a6b-178">Actualice el reproductor.</span><span class="sxs-lookup"><span data-stu-id="09a6b-178">Update the player.</span></span>
8. <span data-ttu-id="09a6b-179">El vídeo se debe estar reproduciendo.</span><span class="sxs-lookup"><span data-stu-id="09a6b-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="09a6b-180">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="09a6b-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09a6b-181">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="09a6b-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

