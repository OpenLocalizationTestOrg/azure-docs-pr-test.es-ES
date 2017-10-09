---
title: "diseño de aaaHybrid de subsistemas DRM con servicios multimedia de Azure | Documentos de Microsoft"
description: "En este tema se describe el diseño híbrido de subsistemas DRM con Azure Media Services."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="46200-103">Diseño híbrido de subsistemas DRM</span><span class="sxs-lookup"><span data-stu-id="46200-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="46200-104">En este tema se describe el diseño híbrido de subsistemas DRM con Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="46200-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="46200-105">Información general</span><span class="sxs-lookup"><span data-stu-id="46200-105">Overview</span></span>

<span data-ttu-id="46200-106">Servicios multimedia de Azure proporciona compatibilidad para hello después de tres sistema DRM:</span><span class="sxs-lookup"><span data-stu-id="46200-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="46200-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="46200-107">PlayReady</span></span>
* <span data-ttu-id="46200-108">Widevine (Modular)</span><span class="sxs-lookup"><span data-stu-id="46200-108">Widevine (Modular)</span></span>
* <span data-ttu-id="46200-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="46200-109">FairPlay</span></span>

<span data-ttu-id="46200-110">compatibilidad con DRM de Hello incluye cifrado de DRM (cifrado dinámico) y la entrega de licencia, con el Reproductor de Media de Azure admite todos los 3 DRMs como un Reproductor de explorador SDK.</span><span class="sxs-lookup"><span data-stu-id="46200-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="46200-111">Para obtener un tratamiento detallado de DRM/CENC subsistema diseño e implementación, vea documento Hola titulado [CENC con DRM de múltiples y Control de acceso](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="46200-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="46200-112">Aunque se ofrece compatibilidad total con tres sistemas DRM, en ocasiones, los clientes necesitan toouse distintas partes de sus propia infraestructura/subsistemas suma tooAzure servicios multimedia toobuild un subsistema DRM híbrido.</span><span class="sxs-lookup"><span data-stu-id="46200-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="46200-113">A continuación se incluyen algunas preguntas comunes planteadas por los clientes:</span><span class="sxs-lookup"><span data-stu-id="46200-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="46200-114">"¿Puedo usar mis propio servidores de licencias DRM?"</span><span class="sxs-lookup"><span data-stu-id="46200-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="46200-115">(En este caso, los clientes han invertido en una granja de servidores de licencias DRM con lógica de negocios insertada).</span><span class="sxs-lookup"><span data-stu-id="46200-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="46200-116">"¿Puedo usar únicamente la entrega de licencias DRM en Azure Media Services sin hospedar contenido de AMS?"</span><span class="sxs-lookup"><span data-stu-id="46200-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="46200-117">Modularidad de hello plataforma DRM AMS</span><span class="sxs-lookup"><span data-stu-id="46200-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="46200-118">Como parte de una plataforma integral de vídeo en la nube, DRM de Azure Media Services tiene en mente un diseño flexible modular.</span><span class="sxs-lookup"><span data-stu-id="46200-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="46200-119">Puede usar los servicios multimedia de Azure con cualquiera de hello siguiendo diferentes combinaciones descritas en tabla de hello siguiente (después de obtener una explicación de la notación de Hola que se utiliza en la tabla de Hola).</span><span class="sxs-lookup"><span data-stu-id="46200-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="46200-120">**Hospedaje y origen del contenido**</span><span class="sxs-lookup"><span data-stu-id="46200-120">**Content hosting & origin**</span></span>|<span data-ttu-id="46200-121">**Cifrado de contenido**</span><span class="sxs-lookup"><span data-stu-id="46200-121">**Content encryption**</span></span>|<span data-ttu-id="46200-122">**Entrega de licencia DRM**</span><span class="sxs-lookup"><span data-stu-id="46200-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="46200-123">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-123">AMS</span></span>|<span data-ttu-id="46200-124">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-124">AMS</span></span>|<span data-ttu-id="46200-125">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-125">AMS</span></span>|
|<span data-ttu-id="46200-126">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-126">AMS</span></span>|<span data-ttu-id="46200-127">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-127">AMS</span></span>|<span data-ttu-id="46200-128">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-128">Third-party</span></span>|
|<span data-ttu-id="46200-129">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-129">AMS</span></span>|<span data-ttu-id="46200-130">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-130">Third-party</span></span>|<span data-ttu-id="46200-131">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-131">AMS</span></span>|
|<span data-ttu-id="46200-132">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-132">AMS</span></span>|<span data-ttu-id="46200-133">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-133">Third-party</span></span>|<span data-ttu-id="46200-134">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-134">Third-party</span></span>|
|<span data-ttu-id="46200-135">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-135">Third-party</span></span>|<span data-ttu-id="46200-136">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-136">Third-party</span></span>|<span data-ttu-id="46200-137">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="46200-138">Hospedaje y origen del contenido</span><span class="sxs-lookup"><span data-stu-id="46200-138">Content hosting & origin</span></span>

* <span data-ttu-id="46200-139">AMS: el recurso de vídeo se hospeda en AMS y el streaming se realiza a través de puntos de conexión de streaming de AMS (pero no necesariamente de empaquetado dinámico).</span><span class="sxs-lookup"><span data-stu-id="46200-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="46200-140">Aplicaciones de terceros: el vídeo se hospeda y se entrega en una plataforma de streaming de terceros fuera AMS.</span><span class="sxs-lookup"><span data-stu-id="46200-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="46200-141">Cifrado de contenido</span><span class="sxs-lookup"><span data-stu-id="46200-141">Content encryption</span></span>

* <span data-ttu-id="46200-142">AMS: el cifrado de contenido se realiza de forma dinámica o a petición mediante cifrado dinámico de AMS.</span><span class="sxs-lookup"><span data-stu-id="46200-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="46200-143">Aplicaciones de terceros: el cifrado de contenido se realiza fuera de AMS mediante un flujo de trabajo previo al procesamiento.</span><span class="sxs-lookup"><span data-stu-id="46200-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="46200-144">Entrega de licencias DRM</span><span class="sxs-lookup"><span data-stu-id="46200-144">DRM license delivery</span></span>

* <span data-ttu-id="46200-145">AMS: el servicio de entrega de licencias de AMS entrega la licencia DRM.</span><span class="sxs-lookup"><span data-stu-id="46200-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="46200-146">Aplicaciones de terceros: la licencia DRM se entrega mediante un servidor de licencias DRM de terceros fuera de AMS.</span><span class="sxs-lookup"><span data-stu-id="46200-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="46200-147">Configuración en función del escenario híbrido</span><span class="sxs-lookup"><span data-stu-id="46200-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="46200-148">Clave de contenido</span><span class="sxs-lookup"><span data-stu-id="46200-148">Content key</span></span>

<span data-ttu-id="46200-149">Configuración de una clave de contenido, puede controlar Hola siguientes atributos de cifrado dinámico AMS y servicio de entrega de licencia de AMS:</span><span class="sxs-lookup"><span data-stu-id="46200-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="46200-150">clave de contenido Hola usado para el cifrado dinámico de DRM.</span><span class="sxs-lookup"><span data-stu-id="46200-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="46200-151">Toobe contenido de licencias DRM entregado por servicios de entrega de licencia: derechos, clave de contenido y las restricciones.</span><span class="sxs-lookup"><span data-stu-id="46200-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="46200-152">Tipo de **restricción de la directiva de autorización de claves de contenido**: abierta, IP o restricción de token.</span><span class="sxs-lookup"><span data-stu-id="46200-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="46200-153">Si **token** tipo de **se utiliza la restricción de la directiva de autorización de clave de contenido**, hello **restricción de la directiva de autorización de claves de contenido** deben cumplirse antes de que se emite una licencia.</span><span class="sxs-lookup"><span data-stu-id="46200-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="46200-154">Directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="46200-154">Asset delivery policy</span></span>

<span data-ttu-id="46200-155">A través de la configuración de una directiva de entrega del activo, puede controlar Hola siguiendo los atributos utilizados por la funcionalidad de paquetes dinámico AMS y cifrado dinámico de un extremo de streaming de AMS:</span><span class="sxs-lookup"><span data-stu-id="46200-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="46200-156">Combinación de protocolo de streaming y cifrado de DRM, como DASH en CENC (PlayReady y Widevine), Smooth Streaming en PlayReady, HLS en Widevine o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="46200-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="46200-157">Hola predeterminado/incrustado licencia entrega las direcciones URL para cada uno de hello implicados DRMs.</span><span class="sxs-lookup"><span data-stu-id="46200-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="46200-158">Si las direcciones URL de adquisición de licencia (LA_URL) en DASH MPD o la lista de reproducción de HLS contienen la cadena de consulta del identificador de clave (KID) para Widevine y FairPlay, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="46200-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="46200-159">Escenarios y ejemplos</span><span class="sxs-lookup"><span data-stu-id="46200-159">Scenarios and samples</span></span>

<span data-ttu-id="46200-160">Según explicaciones de hello en la sección anterior de hello, use respectivos Hola siguiendo cinco escenarios híbridos **clave de contenido**-**directiva de entrega activo** combinaciones de configuración (Hola ejemplos mencionados en la última columna de hello siguen tabla hello):</span><span class="sxs-lookup"><span data-stu-id="46200-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="46200-161">**Hospedaje y origen del contenido**</span><span class="sxs-lookup"><span data-stu-id="46200-161">**Content hosting & origin**</span></span>|<span data-ttu-id="46200-162">**Cifrado de DRM**</span><span class="sxs-lookup"><span data-stu-id="46200-162">**DRM encryption**</span></span>|<span data-ttu-id="46200-163">**Entrega de licencia DRM**</span><span class="sxs-lookup"><span data-stu-id="46200-163">**DRM license delivery**</span></span>|<span data-ttu-id="46200-164">**Configurar la clave de contenido**</span><span class="sxs-lookup"><span data-stu-id="46200-164">**Configure content key**</span></span>|<span data-ttu-id="46200-165">**Configuración de directivas de entrega de activos**</span><span class="sxs-lookup"><span data-stu-id="46200-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="46200-166">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="46200-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="46200-167">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-167">AMS</span></span>|<span data-ttu-id="46200-168">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-168">AMS</span></span>|<span data-ttu-id="46200-169">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-169">AMS</span></span>|<span data-ttu-id="46200-170">Sí</span><span class="sxs-lookup"><span data-stu-id="46200-170">Yes</span></span>|<span data-ttu-id="46200-171">Sí</span><span class="sxs-lookup"><span data-stu-id="46200-171">Yes</span></span>|<span data-ttu-id="46200-172">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="46200-172">Sample 1</span></span>|
|<span data-ttu-id="46200-173">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-173">AMS</span></span>|<span data-ttu-id="46200-174">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-174">AMS</span></span>|<span data-ttu-id="46200-175">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-175">Third-party</span></span>|<span data-ttu-id="46200-176">Sí</span><span class="sxs-lookup"><span data-stu-id="46200-176">Yes</span></span>|<span data-ttu-id="46200-177">Sí</span><span class="sxs-lookup"><span data-stu-id="46200-177">Yes</span></span>|<span data-ttu-id="46200-178">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="46200-178">Sample 2</span></span>|
|<span data-ttu-id="46200-179">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-179">AMS</span></span>|<span data-ttu-id="46200-180">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-180">Third-party</span></span>|<span data-ttu-id="46200-181">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-181">AMS</span></span>|<span data-ttu-id="46200-182">Sí</span><span class="sxs-lookup"><span data-stu-id="46200-182">Yes</span></span>|<span data-ttu-id="46200-183">No</span><span class="sxs-lookup"><span data-stu-id="46200-183">No</span></span>|<span data-ttu-id="46200-184">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="46200-184">Sample 3</span></span>|
|<span data-ttu-id="46200-185">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-185">AMS</span></span>|<span data-ttu-id="46200-186">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-186">Third-party</span></span>|<span data-ttu-id="46200-187">Externo</span><span class="sxs-lookup"><span data-stu-id="46200-187">Outside</span></span>|<span data-ttu-id="46200-188">No</span><span class="sxs-lookup"><span data-stu-id="46200-188">No</span></span>|<span data-ttu-id="46200-189">No</span><span class="sxs-lookup"><span data-stu-id="46200-189">No</span></span>|<span data-ttu-id="46200-190">Ejemplo 4</span><span class="sxs-lookup"><span data-stu-id="46200-190">Sample 4</span></span>|
|<span data-ttu-id="46200-191">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-191">Third-party</span></span>|<span data-ttu-id="46200-192">Aplicaciones de terceros</span><span class="sxs-lookup"><span data-stu-id="46200-192">Third-party</span></span>|<span data-ttu-id="46200-193">AMS</span><span class="sxs-lookup"><span data-stu-id="46200-193">AMS</span></span>|<span data-ttu-id="46200-194">Sí</span><span class="sxs-lookup"><span data-stu-id="46200-194">Yes</span></span>|<span data-ttu-id="46200-195">No</span><span class="sxs-lookup"><span data-stu-id="46200-195">No</span></span>|    

<span data-ttu-id="46200-196">En los ejemplos de hello, funciona la protección de PlayReady para DASH y smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="46200-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="46200-197">Hola vídeo las direcciones URL siguientes son smooth streaming las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="46200-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="46200-198">tooget Hola correspondientes direcciones URL de guión, simplemente anexar "(formato = mpd: tiempo-csf)".</span><span class="sxs-lookup"><span data-stu-id="46200-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="46200-199">Puede usar hello [multimedia de azure probar Reproductor](http://aka.ms/amtest) tootest en un explorador.</span><span class="sxs-lookup"><span data-stu-id="46200-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="46200-200">Le permite tooconfigure que toouse de protocolo, en qué tecnología de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="46200-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="46200-201">IE11 y MS Edge en Windows 10 admiten PlayReady a través de EME.</span><span class="sxs-lookup"><span data-stu-id="46200-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="46200-202">Para obtener más información, consulte [detalles sobre Hola probar herramienta](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="46200-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="46200-203">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="46200-203">Sample 1</span></span>

* <span data-ttu-id="46200-204">Dirección URL (base) de origen: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="46200-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="46200-205">LA_URL de PlayReady (DASH y Smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="46200-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="46200-206">LA_URL de Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="46200-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="46200-207">LA_URL de FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="46200-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="46200-208">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="46200-208">Sample 2</span></span>

* <span data-ttu-id="46200-209">Dirección URL (base) de origen: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="46200-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="46200-210">LA_URL de PlayReady (DASH y Smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="46200-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="46200-211">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="46200-211">Sample 3</span></span>

* <span data-ttu-id="46200-212">Dirección URL de origen: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="46200-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="46200-213">LA_URL de PlayReady (DASH y Smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="46200-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="46200-214">Ejemplo 4</span><span class="sxs-lookup"><span data-stu-id="46200-214">Sample 4</span></span>

* <span data-ttu-id="46200-215">Dirección URL de origen: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="46200-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="46200-216">LA_URL de PlayReady (DASH y smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="46200-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="46200-217">Resumen</span><span class="sxs-lookup"><span data-stu-id="46200-217">Summary</span></span>

<span data-ttu-id="46200-218">En resumen, los componentes DRM de Azure Media Services son flexibles y se pueden usar en un escenario híbrido mediante la configuración correcta de la clave de contenido y la directiva de entrega de activos, como se describe en este tema.</span><span class="sxs-lookup"><span data-stu-id="46200-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46200-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46200-219">Next steps</span></span>
<span data-ttu-id="46200-220">Ver las rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="46200-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="46200-221">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="46200-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

