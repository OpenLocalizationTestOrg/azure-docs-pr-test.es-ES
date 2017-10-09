---
title: "directivas de protección de contenido aaaConfiguring mediante Hola portal de Azure | Documentos de Microsoft"
description: "Este artículo demuestra cómo toouse Hola las directivas de protección de contenido de tooconfigure de portal de Azure. Hola artículo también se muestra cómo tooenable cifrado dinámico para los activos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="a34fb-104">Configuración de directivas de protección de contenido mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a34fb-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="a34fb-105">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a34fb-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="a34fb-106">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a34fb-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="a34fb-107">Información general</span><span class="sxs-lookup"><span data-stu-id="a34fb-107">Overview</span></span>
<span data-ttu-id="a34fb-108">Servicios de multimedia de Microsoft Azure (AMS) permite toosecure su media de tiempo de hello sale del equipo a través de almacenamiento, procesamiento y entrega.</span><span class="sxs-lookup"><span data-stu-id="a34fb-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="a34fb-109">Servicios multimedia permite toodeliver el contenido cifrado dinámicamente con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits), cifrado común (CENC) con PlayReady o Widevine DRM y FairPlay de Apple.</span><span class="sxs-lookup"><span data-stu-id="a34fb-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="a34fb-110">AMS proporciona un servicio para entregar licencias de DRM y los clientes de tooauthorized de claves sin cifrado AES.</span><span class="sxs-lookup"><span data-stu-id="a34fb-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="a34fb-111">Hello portal de Azure permite toocreate uno **clave/directiva de autorización de licencia** para todos los tipos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="a34fb-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="a34fb-112">Este artículo demuestra cómo tooconfigure contenido directivas de protección con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a34fb-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="a34fb-113">Hola artículo también se muestra cómo tooyour activos de tooapply cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="a34fb-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="a34fb-114">Si usa directivas de protección de Azure toocreate portal clásico de hello, directivas de hello no pueden aparecer en hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a34fb-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a34fb-115">Sin embargo, todos los Hola antiguo directivas todavía existe.</span><span class="sxs-lookup"><span data-stu-id="a34fb-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="a34fb-116">Puede examinarlas utilizando hello Azure Media Services .NET SDK o hello [Azure-Media-Explorador de servicios](https://github.com/Azure/Azure-Media-Services-Explorer/releases) herramienta (directivas de hello toosee, contextual en activo hello -> Mostrar información (F4) -> haga clic en -> pestaña de claves de contenido Haga clic en clave de hello).</span><span class="sxs-lookup"><span data-stu-id="a34fb-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="a34fb-117">Si desea tooencrypt su activo mediante nuevas directivas, configurarlos con hello portal de Azure, haga clic en Guardar y aplicar el cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="a34fb-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="a34fb-118">Empezar a configurar la protección de contenido</span><span class="sxs-lookup"><span data-stu-id="a34fb-118">Start configuring content protection</span></span>
<span data-ttu-id="a34fb-119">toouse Hola portal toostart configuración de protección del contenido, la cuenta tooyour global AMS, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a34fb-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="a34fb-120">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="a34fb-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a34fb-121">Seleccione **Ajustes** > **Protección de contenido**.</span><span class="sxs-lookup"><span data-stu-id="a34fb-121">Select **Settings** > **Content protection**.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="a34fb-123">directiva de autorización de licencias o claves</span><span class="sxs-lookup"><span data-stu-id="a34fb-123">Key/license authorization policy</span></span>
<span data-ttu-id="a34fb-124">AMS admite varias formas de autenticar a los usuarios que realizan solicitudes de clave o licencia.</span><span class="sxs-lookup"><span data-stu-id="a34fb-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="a34fb-125">Directiva de autorización de clave de contenido de Hello debe configurarse por parte del usuario y cumplir el cliente para hello clave/licencia toobe toohello delived cliente.</span><span class="sxs-lookup"><span data-stu-id="a34fb-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="a34fb-126">Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: **abrir** o **token** restricción.</span><span class="sxs-lookup"><span data-stu-id="a34fb-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="a34fb-127">Hello portal de Azure permite toocreate uno **clave/directiva de autorización de licencia** para todos los tipos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="a34fb-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="a34fb-128">Abrir</span><span class="sxs-lookup"><span data-stu-id="a34fb-128">Open</span></span>
<span data-ttu-id="a34fb-129">Restricción abierta significa que el sistema de hello cumplirán lo hello tooanyone clave que realiza una solicitud de clave.</span><span class="sxs-lookup"><span data-stu-id="a34fb-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="a34fb-130">Esta restricción puede ser útil para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="a34fb-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="a34fb-131">SWT</span><span class="sxs-lookup"><span data-stu-id="a34fb-131">Token</span></span>
<span data-ttu-id="a34fb-132">directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS).</span><span class="sxs-lookup"><span data-stu-id="a34fb-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="a34fb-133">Servicios multimedia admite tokens con formato Simple Web Tokens (SWT) de Hola y el formato de JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="a34fb-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="a34fb-134">Los Servicios multimedia no proporcionan Servicios de tokens seguros.</span><span class="sxs-lookup"><span data-stu-id="a34fb-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="a34fb-135">Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue.</span><span class="sxs-lookup"><span data-stu-id="a34fb-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="a34fb-136">Hola STS debe estar configurado toocreate un token firmado con hello especificado clave y emitir notificaciones que especificó en la configuración de restricción de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="a34fb-137">Servicios de multimedia de Hello servicio de entrega de claves devolverá Hola solicitado Hola y cliente de toohello (o licencias) de la clave si Hola token es válido notificaciones Hola token coinciden con las configuradas para las claves de hello (o licencias).</span><span class="sxs-lookup"><span data-stu-id="a34fb-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="a34fb-138">Al configurar la directiva restringida de tokens de hello, debe especificar la clave de verificación principal hello, emisor y parámetros de audiencia.</span><span class="sxs-lookup"><span data-stu-id="a34fb-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="a34fb-139">clave de verificación principal Hello contiene Hola clave que Hola token se firmó con, el emisor es Hola servicio de token seguro que emite el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="a34fb-140">audiencia de Hello (a veces denominado ámbito) describe intención de hello del token de Hola u Hola recursos Hola token autoriza acceso.</span><span class="sxs-lookup"><span data-stu-id="a34fb-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="a34fb-141">Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="a34fb-143">Plantilla de derechos de PlayReady</span><span class="sxs-lookup"><span data-stu-id="a34fb-143">PlayReady rights template</span></span>
<span data-ttu-id="a34fb-144">Para obtener información detallada acerca de la plantilla de derechos de hello PlayReady, vea [Media Services PlayReady licencia plantilla Overview](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a34fb-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="a34fb-145">No persistente</span><span class="sxs-lookup"><span data-stu-id="a34fb-145">Non persistent</span></span>
<span data-ttu-id="a34fb-146">Si configura licencia como no persistentes, solo se mantiene en memoria mientras Reproductor Hola está usando la licencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="a34fb-148">Persistente</span><span class="sxs-lookup"><span data-stu-id="a34fb-148">Persistent</span></span>
<span data-ttu-id="a34fb-149">Si configura licencia hello como persistente, se guarda en el almacenamiento persistente en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="a34fb-151">Plantilla de derechos de Widevine</span><span class="sxs-lookup"><span data-stu-id="a34fb-151">Widevine rights template</span></span>
<span data-ttu-id="a34fb-152">Para obtener información detallada acerca de la plantilla de hello Widevine permisos, consulte [información general de plantilla de licencias de Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a34fb-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="a34fb-153">Básica</span><span class="sxs-lookup"><span data-stu-id="a34fb-153">Basic</span></span>
<span data-ttu-id="a34fb-154">Cuando se selecciona **básica**, se creará la plantilla de Hola a todos los valores de los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="a34fb-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="a34fb-155">Avanzado</span><span class="sxs-lookup"><span data-stu-id="a34fb-155">Advanced</span></span>
<span data-ttu-id="a34fb-156">Para una explicación detallada acerca de la opción avanzada de configuraciones de Widevine, consulte [este tema](media-services-widevine-license-template-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="a34fb-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="a34fb-158">Configuración de FairPlay</span><span class="sxs-lookup"><span data-stu-id="a34fb-158">FairPlay configuration</span></span>
<span data-ttu-id="a34fb-159">tooenable FairPlay cifrado, necesita tooprovide Hola certificado de la aplicación y clave de secreto de aplicación (consulte) a través de la opción de configuración FairPlay Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="a34fb-160">Para más información sobre la configuración y los requisitos de FairPlay, consulte [este artículo](media-services-protect-hls-with-fairplay.md) .</span><span class="sxs-lookup"><span data-stu-id="a34fb-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="a34fb-162">Aplicar activos tooyour de cifrado dinámico</span><span class="sxs-lookup"><span data-stu-id="a34fb-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="a34fb-163">tootake ventaja del cifrado dinámico, debe tooencode el archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="a34fb-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="a34fb-164">Seleccione un recurso que desea tooencrypt</span><span class="sxs-lookup"><span data-stu-id="a34fb-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="a34fb-165">toosee todos sus activos, seleccione **configuración** > **activos**.</span><span class="sxs-lookup"><span data-stu-id="a34fb-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="a34fb-167">Cifrado con AES o DRM</span><span class="sxs-lookup"><span data-stu-id="a34fb-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="a34fb-168">Cuando presiona **Cifrar** en un recurso, se le presentan dos opciones: **AES** o **DRM**.</span><span class="sxs-lookup"><span data-stu-id="a34fb-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="a34fb-169">AES</span><span class="sxs-lookup"><span data-stu-id="a34fb-169">AES</span></span>
<span data-ttu-id="a34fb-170">El cifrado de claves sin cifrado AES se habilitará en todos los protocolos de streaming: Smooth Streaming, HLS y MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="a34fb-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="a34fb-172">DRM</span><span class="sxs-lookup"><span data-stu-id="a34fb-172">DRM</span></span>
<span data-ttu-id="a34fb-173">Cuando se selecciona la pestaña DRM de hello, se presentan con las diferentes opciones de directivas de protección de contenido (que debe haber configurado hasta ahora) + un conjunto de protocolos de transmisión de datos.</span><span class="sxs-lookup"><span data-stu-id="a34fb-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="a34fb-174">**PlayReady y Widevine con MPEG-DASH** : cifrará dinámicamente su transmisión MPEG-DASH con DRM de PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="a34fb-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="a34fb-175">**PlayReady y Widevine con MPEG-DASH más FairPlay con HLS** : cifrará dinámicamente su transmisión MPEG-DASH con DRM de PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="a34fb-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="a34fb-176">También se cifrarán las transmisiones HLS con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="a34fb-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="a34fb-177">**PlayReady solo con Smooth Streaming, HLS y MPEG-DASH** : cifrará dinámicamente Smooth Streaming, HLS, transmisiones MPEG DASH con DRM de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="a34fb-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="a34fb-178">**Widevine solo con MPEG-DASH** : cifrará dinámicamente MPEG-DASH con DRM de Widevine.</span><span class="sxs-lookup"><span data-stu-id="a34fb-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="a34fb-179">**FairPlay solo con HLS** : cifrará dinámicamente su transmisión HLS con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="a34fb-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="a34fb-180">tooenable FairPlay cifrado, necesita tooprovide Hola certificado de la aplicación y clave de secreto de aplicación (consulte) a través de la opción de configuración de FairPlay de hoja de configuración de protección de contenido de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a34fb-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="a34fb-182">Una vez realizada la selección de cifrado de hello, presione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="a34fb-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="a34fb-183">Si tiene previsto tooplay un AES cifrado HLS en Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="a34fb-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a34fb-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a34fb-184">Next steps</span></span>
<span data-ttu-id="a34fb-185">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a34fb-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a34fb-186">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a34fb-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

