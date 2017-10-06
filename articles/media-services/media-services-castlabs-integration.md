---
title: aaaUsing castLabs toodeliver Widevine licencias de servicios de multimedia de tooAzure | Documentos de Microsoft
description: "Este artículo describe cómo puede usar servicios de multimedia de Azure (AMS) toodeliver una secuencia que se cifra dinámicamente por AMS con PlayReady y Widevine DRMs. licencia de PlayReady Hola procede del servidor de licencias de PlayReady de servicios multimedia y licencias de Widevine enviada por el servidor de licencias de castLabs."
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
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="d631d-104">Uso de tooAzure de licencias de Widevine castLabs toodeliver servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="d631d-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d631d-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="d631d-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="d631d-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="d631d-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d631d-107">Información general</span><span class="sxs-lookup"><span data-stu-id="d631d-107">Overview</span></span>
<span data-ttu-id="d631d-108">Este artículo describe cómo puede usar servicios de multimedia de Azure (AMS) toodeliver una secuencia que se cifra dinámicamente por AMS con PlayReady y Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="d631d-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="d631d-109">licencia de PlayReady Hola procede del servidor de licencias de PlayReady de servicios multimedia y licencias de Widevine enviada por **castLabs** servidor de licencias.</span><span class="sxs-lookup"><span data-stu-id="d631d-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="d631d-110">tooplayback transmisión por secuencias el contenido protegido por CENC (PlayReady o Widevine), puede usar [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d631d-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="d631d-111">Consulte el [documento AMP](http://amp.azure.net/libs/amp/latest/docs/) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="d631d-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="d631d-112">Hola siguiente diagrama muestra una arquitectura de integración de servicios multimedia de Azure y castLabs alto nivel.</span><span class="sxs-lookup"><span data-stu-id="d631d-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integración](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="d631d-114">Configuración de sistema típico</span><span class="sxs-lookup"><span data-stu-id="d631d-114">Typical system set up</span></span>
* <span data-ttu-id="d631d-115">El contenido multimedia se almacena en AMS.</span><span class="sxs-lookup"><span data-stu-id="d631d-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="d631d-116">Los id. de clave de claves de contenido se almacenan en castLabs y AMS.</span><span class="sxs-lookup"><span data-stu-id="d631d-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="d631d-117">Tanto castLabs como AMS tienen la autenticación de tokens integrada.</span><span class="sxs-lookup"><span data-stu-id="d631d-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="d631d-118">Hola siguientes secciones describe los tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="d631d-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="d631d-119">Cuando un cliente solicita el vídeo de hello toostream, contenido de hello dinámicamente se cifran con **cifrado común** (CENC) y empaquetar AMS tooSmooth dinámicamente la transmisión por secuencias y el guión.</span><span class="sxs-lookup"><span data-stu-id="d631d-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="d631d-120">También ofrecemos cifrado de streaming elemental de PlayReady M2TS para el protocolo de streaming HLS.</span><span class="sxs-lookup"><span data-stu-id="d631d-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="d631d-121">La licencia de PlayReady se recupera del servidor de licencias de AMS y la licencia de Widevine se recupera del servidor de licencias de castLabs.</span><span class="sxs-lookup"><span data-stu-id="d631d-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="d631d-122">El Reproductor de Media automáticamente decide qué toofetch de licencia en función de la capacidad de la plataforma cliente Hola.</span><span class="sxs-lookup"><span data-stu-id="d631d-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="d631d-123">Generación de tokens de autenticación para obtener una licencia</span><span class="sxs-lookup"><span data-stu-id="d631d-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="d631d-124">CastLabs y AMS admite JWT (JSON Web Token) tooauthorize de formato de token usa una licencia.</span><span class="sxs-lookup"><span data-stu-id="d631d-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="d631d-125">Token JWT en AMS</span><span class="sxs-lookup"><span data-stu-id="d631d-125">JWT token in AMS</span></span>
<span data-ttu-id="d631d-126">Hello en la tabla siguiente describe los tokens JWT en AMS.</span><span class="sxs-lookup"><span data-stu-id="d631d-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="d631d-127">Emisor</span><span class="sxs-lookup"><span data-stu-id="d631d-127">Issuer</span></span> | <span data-ttu-id="d631d-128">Cadena de emisor de hello elegido el servicio de Token seguro (STS)</span><span class="sxs-lookup"><span data-stu-id="d631d-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="d631d-129">Público</span><span class="sxs-lookup"><span data-stu-id="d631d-129">Audience</span></span> |<span data-ttu-id="d631d-130">Cadena de audiencia de hello usa STS</span><span class="sxs-lookup"><span data-stu-id="d631d-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="d631d-131">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="d631d-131">Claims</span></span> |<span data-ttu-id="d631d-132">Un conjunto de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d631d-132">A set of claims</span></span> |
| <span data-ttu-id="d631d-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="d631d-133">NotBefore</span></span> |<span data-ttu-id="d631d-134">Iniciar la validez del token de Hola</span><span class="sxs-lookup"><span data-stu-id="d631d-134">Start validity of hello token</span></span> |
| <span data-ttu-id="d631d-135">Expira</span><span class="sxs-lookup"><span data-stu-id="d631d-135">Expires</span></span> |<span data-ttu-id="d631d-136">Final de validez del token de Hola</span><span class="sxs-lookup"><span data-stu-id="d631d-136">End validity of hello token</span></span> |
| <span data-ttu-id="d631d-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="d631d-137">SigningCredentials</span></span> |<span data-ttu-id="d631d-138">clave de Hola que se comparte entre el servidor de licencias de PlayReady, castLabs servidor de licencias y STS, podría ser clave simétrica o asimétrica.</span><span class="sxs-lookup"><span data-stu-id="d631d-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="d631d-139">Token JWT en castLabs</span><span class="sxs-lookup"><span data-stu-id="d631d-139">JWT token in castLabs</span></span>
<span data-ttu-id="d631d-140">Hello en la tabla siguiente describe el token JWT en castLabs.</span><span class="sxs-lookup"><span data-stu-id="d631d-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="d631d-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="d631d-141">Name</span></span> | <span data-ttu-id="d631d-142">Description</span><span class="sxs-lookup"><span data-stu-id="d631d-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d631d-143">optData</span><span class="sxs-lookup"><span data-stu-id="d631d-143">optData</span></span> |<span data-ttu-id="d631d-144">Cadena JSON que contiene información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="d631d-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="d631d-145">crt</span><span class="sxs-lookup"><span data-stu-id="d631d-145">crt</span></span> |<span data-ttu-id="d631d-146">Un JSON cadena que contiene información sobre activos hello, sus derechos de reproducción y la información de licencia.</span><span class="sxs-lookup"><span data-stu-id="d631d-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="d631d-147">iat</span><span class="sxs-lookup"><span data-stu-id="d631d-147">iat</span></span> |<span data-ttu-id="d631d-148">Hola datetime actual en tiempo.</span><span class="sxs-lookup"><span data-stu-id="d631d-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="d631d-149">jti</span><span class="sxs-lookup"><span data-stu-id="d631d-149">jti</span></span> |<span data-ttu-id="d631d-150">Un identificador único sobre este token (cada token sólo puede utilizarse una vez en el sistema de hello castLabs).</span><span class="sxs-lookup"><span data-stu-id="d631d-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="d631d-151">Configuración de soluciones de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d631d-151">Sample solution set up</span></span>
<span data-ttu-id="d631d-152">Hola [solución de ejemplo](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consta de dos proyectos:</span><span class="sxs-lookup"><span data-stu-id="d631d-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="d631d-153">Una aplicación de consola que puede ser utilizados tooset DRM restricciones en un activo ya integrado, para PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="d631d-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="d631d-154">Una aplicación web que distribuye tokens, que podrían considerarse como una versión MUY SIMPLIFICADA de un STS.</span><span class="sxs-lookup"><span data-stu-id="d631d-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="d631d-155">aplicación de consola de Hola toouse:</span><span class="sxs-lookup"><span data-stu-id="d631d-155">toouse hello console application:</span></span>

1. <span data-ttu-id="d631d-156">Cambiar las credenciales de hello app.config toosetup AMS, castLabs credenciales, configuración de STS y una clave compartida.</span><span class="sxs-lookup"><span data-stu-id="d631d-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="d631d-157">Cargue un activo en AMS.</span><span class="sxs-lookup"><span data-stu-id="d631d-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="d631d-158">Get hello UUID de hello cargado activo y cambia 32 de línea en el archivo Program.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="d631d-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="d631d-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="d631d-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="d631d-160">Aplique un AssetId de activos de hello en sistema de hello castLabs (44 de línea en el archivo Program.cs de hello).</span><span class="sxs-lookup"><span data-stu-id="d631d-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="d631d-161">Debe establecer AssetId para **castLabs**; debe toobe una cadena alfanumérica única.</span><span class="sxs-lookup"><span data-stu-id="d631d-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="d631d-162">Ejecutar programa Hola.</span><span class="sxs-lookup"><span data-stu-id="d631d-162">Run hello program.</span></span>

<span data-ttu-id="d631d-163">Hola toouse aplicación Web (STS):</span><span class="sxs-lookup"><span data-stu-id="d631d-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="d631d-164">Toosetup castlabs comerciante de cambio Hola web.config Id., configuración de STS de Hola y Hola una clave compartida.</span><span class="sxs-lookup"><span data-stu-id="d631d-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="d631d-165">Implementar tooAzure sitios Web.</span><span class="sxs-lookup"><span data-stu-id="d631d-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="d631d-166">Explorar el sitio Web de toohello.</span><span class="sxs-lookup"><span data-stu-id="d631d-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="d631d-167">Reproducir un vídeo</span><span class="sxs-lookup"><span data-stu-id="d631d-167">Playing back a video</span></span>
<span data-ttu-id="d631d-168">tooplayback un vídeo cifrada con cifrado común (PlayReady o Widevine), puede usar hello [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d631d-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="d631d-169">Cuando se ejecuta la aplicación de consola de hello, se reflejan el identificador de clave de contenido de Hola y Hola dirección URL del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="d631d-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="d631d-170">Abra una nueva pestaña e inicie STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="d631d-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="d631d-171">Vaya demasiado[Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d631d-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="d631d-172">Pegue en hello transmisión por secuencias de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d631d-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="d631d-173">Haga clic en hello **opciones avanzadas** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="d631d-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="d631d-174">Hola **protección** lista desplegable, seleccione PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="d631d-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="d631d-175">Pegue el token de Hola que obtuvo en los STS en el cuadro de texto de hello símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="d631d-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="d631d-176">no es necesario el servidor de licencias de castLab de Hola Hola "portador =" prefijo delante del símbolo (token) de Hola.</span><span class="sxs-lookup"><span data-stu-id="d631d-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="d631d-177">Así que quite antes de enviar el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="d631d-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="d631d-178">Actualizar el Reproductor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d631d-178">Update hello player.</span></span>
8. <span data-ttu-id="d631d-179">Hola vídeo debe ser reproducción en curso.</span><span class="sxs-lookup"><span data-stu-id="d631d-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d631d-180">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="d631d-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d631d-181">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d631d-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

