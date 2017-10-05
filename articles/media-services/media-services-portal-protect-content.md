---
title: "Configuración de directivas de protección de contenido mediante Azure Portal | Microsoft Docs"
description: "En este artículo se muestra cómo usar Azure Portal para configurar las directivas de protección de contenido. El artículo también muestra cómo habilitar el cifrado dinámico para los recursos."
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
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="3bf01-104">Configuración de directivas de protección de contenido mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3bf01-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="3bf01-105">Para completar este tutorial, deberá tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf01-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3bf01-106">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bf01-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="3bf01-107">Información general</span><span class="sxs-lookup"><span data-stu-id="3bf01-107">Overview</span></span>
<span data-ttu-id="3bf01-108">Microsoft Azure Media Services (AMS) le permite proteger su contenido multimedia desde el momento en que deja el equipo a través de almacenamiento, procesamiento y entrega.</span><span class="sxs-lookup"><span data-stu-id="3bf01-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="3bf01-109">Media Services permite entregar el contenido cifrado de forma dinámica con Estándar de cifrado avanzado (AES) (mediante claves de cifrado de 128 bits) y cifrado común (CENC) mediante PlayReady o Widevine DRM, and Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3bf01-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="3bf01-110">AMS proporciona un servicio para proporcionar licencias de DRM y claves sin cifrado de AES a clientes autorizados.</span><span class="sxs-lookup"><span data-stu-id="3bf01-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="3bf01-111">Azure Portal le permite crear una **directiva de autorización de licencias o claves** para todos los tipos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="3bf01-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="3bf01-112">En este artículo se muestra cómo configurar las directivas de protección de contenido con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3bf01-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="3bf01-113">El artículo también muestra cómo aplicar el cifrado dinámico a los recursos.</span><span class="sxs-lookup"><span data-stu-id="3bf01-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="3bf01-114">Si utiliza el Portal de Azure clásico para crear directivas de protección, es posible que las directivas no aparezcan en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3bf01-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3bf01-115">Sin embargo, siguen existiendo todavía las directivas antiguas.</span><span class="sxs-lookup"><span data-stu-id="3bf01-115">However, all the old polices still exist.</span></span> <span data-ttu-id="3bf01-116">Puede examinarlas mediante el SDK de .NET de Azure Media Services o la herramienta [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) (para ver las directivas, haga clic con el botón derecho en el recurso -> Mostrar información (F4) -> haga clic en la pestaña de claves de contenido -> haga clic en la clave).</span><span class="sxs-lookup"><span data-stu-id="3bf01-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="3bf01-117">Si quiere cifrar el recurso con nuevas directivas, configúrelas con Azure Portal, haga clic en Guardar y vuelva a aplicar el cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="3bf01-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="3bf01-118">Empezar a configurar la protección de contenido</span><span class="sxs-lookup"><span data-stu-id="3bf01-118">Start configuring content protection</span></span>
<span data-ttu-id="3bf01-119">Para usar el portal para empezar a configurar la protección de contenido, para su cuenta de AMS, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3bf01-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="3bf01-120">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="3bf01-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3bf01-121">Seleccione **Ajustes** > **Protección de contenido**.</span><span class="sxs-lookup"><span data-stu-id="3bf01-121">Select **Settings** > **Content protection**.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="3bf01-123">directiva de autorización de licencias o claves</span><span class="sxs-lookup"><span data-stu-id="3bf01-123">Key/license authorization policy</span></span>
<span data-ttu-id="3bf01-124">AMS admite varias formas de autenticar a los usuarios que realizan solicitudes de clave o licencia.</span><span class="sxs-lookup"><span data-stu-id="3bf01-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="3bf01-125">El usuario debe configurar la directiva de autorización de claves y el cliente debe conocerla para que se le proporcione la clave o licencia.</span><span class="sxs-lookup"><span data-stu-id="3bf01-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="3bf01-126">La directiva de autorización de claves de acceso podría tener una o más restricciones de autorización: **abrir** o restricción de **token**.</span><span class="sxs-lookup"><span data-stu-id="3bf01-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="3bf01-127">Azure Portal le permite crear una **directiva de autorización de licencias o claves** para todos los tipos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="3bf01-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="3bf01-128">Abrir</span><span class="sxs-lookup"><span data-stu-id="3bf01-128">Open</span></span>
<span data-ttu-id="3bf01-129">La restricción open significa que el sistema entregará la clave a cualquier persona que realice una solicitud de clave.</span><span class="sxs-lookup"><span data-stu-id="3bf01-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="3bf01-130">Esta restricción puede ser útil para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="3bf01-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="3bf01-131">token</span><span class="sxs-lookup"><span data-stu-id="3bf01-131">Token</span></span>
<span data-ttu-id="3bf01-132">La directiva con restricción token debe ir acompañada de un token emitido por un Servicio de tokens seguros (STS).</span><span class="sxs-lookup"><span data-stu-id="3bf01-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="3bf01-133">Servicios multimedia admite tokens en formato Token de web simple (SWT) y en formato Token de web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="3bf01-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="3bf01-134">Los Servicios multimedia no proporcionan Servicios de tokens seguros.</span><span class="sxs-lookup"><span data-stu-id="3bf01-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="3bf01-135">Puede crear un STS personalizado o aprovechar el Servicio de control de acceso (ACS) de Microsoft Azure para emitir tokens.</span><span class="sxs-lookup"><span data-stu-id="3bf01-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="3bf01-136">Se debe configurar el STS para crear un token firmado con las notificaciones de clave y emisión que especificó en la configuración de restricción de tokens.</span><span class="sxs-lookup"><span data-stu-id="3bf01-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="3bf01-137">El servicio de entrega de claves de Servicios multimedia devolverá la clave solicitada (o licencia) al cliente si el token es válido y las reclamaciones del token coinciden con las configuradas para la clave (o licencia).</span><span class="sxs-lookup"><span data-stu-id="3bf01-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="3bf01-138">Al configurar la directiva de restricción de token, debe especificar los parámetros de clave de comprobación principal, emisor y público.</span><span class="sxs-lookup"><span data-stu-id="3bf01-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="3bf01-139">La clave de comprobación principal contiene la clave con la que se firmó el token y el emisor es el servicio de tokens seguros que emite el token.</span><span class="sxs-lookup"><span data-stu-id="3bf01-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="3bf01-140">El público (a veces denominado ámbito) describe la intención del token o del recurso cuyo acceso está autorizado por el token.</span><span class="sxs-lookup"><span data-stu-id="3bf01-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="3bf01-141">El servicio de entrega de claves de los Servicios multimedia valida que estos valores del token coincidan con los valores de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="3bf01-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="3bf01-143">Plantilla de derechos de PlayReady</span><span class="sxs-lookup"><span data-stu-id="3bf01-143">PlayReady rights template</span></span>
<span data-ttu-id="3bf01-144">Para más información sobre la plantilla de derechos de PlayReady, consulte [Información general de plantillas de licencias de PlayReady de Media Services](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bf01-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="3bf01-145">No persistente</span><span class="sxs-lookup"><span data-stu-id="3bf01-145">Non persistent</span></span>
<span data-ttu-id="3bf01-146">Si configura la licencia como no persistente, solo se mantiene en memoria mientras el reproductor está usando la licencia.</span><span class="sxs-lookup"><span data-stu-id="3bf01-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="3bf01-148">Persistente</span><span class="sxs-lookup"><span data-stu-id="3bf01-148">Persistent</span></span>
<span data-ttu-id="3bf01-149">Si configura la licencia como persistente, se guarda en el almacenamiento persistente en el cliente.</span><span class="sxs-lookup"><span data-stu-id="3bf01-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="3bf01-151">Plantilla de derechos de Widevine</span><span class="sxs-lookup"><span data-stu-id="3bf01-151">Widevine rights template</span></span>
<span data-ttu-id="3bf01-152">Para más información sobre la plantilla de derechos de Widevine, consulte [Información general sobre las plantillas de licencias de Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bf01-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="3bf01-153">Básica</span><span class="sxs-lookup"><span data-stu-id="3bf01-153">Basic</span></span>
<span data-ttu-id="3bf01-154">Al seleccionar **Básico**, la plantilla se creará con todos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3bf01-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="3bf01-155">Avanzado</span><span class="sxs-lookup"><span data-stu-id="3bf01-155">Advanced</span></span>
<span data-ttu-id="3bf01-156">Para una explicación detallada acerca de la opción avanzada de configuraciones de Widevine, consulte [este tema](media-services-widevine-license-template-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="3bf01-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="3bf01-158">Configuración de FairPlay</span><span class="sxs-lookup"><span data-stu-id="3bf01-158">FairPlay configuration</span></span>
<span data-ttu-id="3bf01-159">Para habilitar el cifrado de FairPlay, debe proporcionar el certificado de la aplicación y la clave de secreto de aplicación (ASK) mediante la opción de configuración de FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3bf01-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="3bf01-160">Para más información sobre la configuración y los requisitos de FairPlay, consulte [este artículo](media-services-protect-hls-with-fairplay.md) .</span><span class="sxs-lookup"><span data-stu-id="3bf01-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="3bf01-162">Aplicación del cifrado dinámico al recurso</span><span class="sxs-lookup"><span data-stu-id="3bf01-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="3bf01-163">Para aprovechar las ventajas del cifrado dinámico, debe codificar el archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="3bf01-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="3bf01-164">Seleccione el recurso que desea cifrar.</span><span class="sxs-lookup"><span data-stu-id="3bf01-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="3bf01-165">Para ver todos sus recursos, seleccione **Configuración** > **Recursos**.</span><span class="sxs-lookup"><span data-stu-id="3bf01-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="3bf01-167">Cifrado con AES o DRM</span><span class="sxs-lookup"><span data-stu-id="3bf01-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="3bf01-168">Cuando presiona **Cifrar** en un recurso, se le presentan dos opciones: **AES** o **DRM**.</span><span class="sxs-lookup"><span data-stu-id="3bf01-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="3bf01-169">AES</span><span class="sxs-lookup"><span data-stu-id="3bf01-169">AES</span></span>
<span data-ttu-id="3bf01-170">El cifrado de claves sin cifrado AES se habilitará en todos los protocolos de streaming: Smooth Streaming, HLS y MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="3bf01-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="3bf01-172">DRM</span><span class="sxs-lookup"><span data-stu-id="3bf01-172">DRM</span></span>
<span data-ttu-id="3bf01-173">Cuando se selecciona la pestaña DRM, se le presentan distintas opciones de directivas de protección de contenido (que debe haber configurado ya) más un conjunto de protocolos de streaming.</span><span class="sxs-lookup"><span data-stu-id="3bf01-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="3bf01-174">**PlayReady y Widevine con MPEG-DASH** : cifrará dinámicamente su transmisión MPEG-DASH con DRM de PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="3bf01-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="3bf01-175">**PlayReady y Widevine con MPEG-DASH más FairPlay con HLS** : cifrará dinámicamente su transmisión MPEG-DASH con DRM de PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="3bf01-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="3bf01-176">También se cifrarán las transmisiones HLS con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3bf01-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="3bf01-177">**PlayReady solo con Smooth Streaming, HLS y MPEG-DASH** : cifrará dinámicamente Smooth Streaming, HLS, transmisiones MPEG DASH con DRM de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="3bf01-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="3bf01-178">**Widevine solo con MPEG-DASH** : cifrará dinámicamente MPEG-DASH con DRM de Widevine.</span><span class="sxs-lookup"><span data-stu-id="3bf01-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="3bf01-179">**FairPlay solo con HLS** : cifrará dinámicamente su transmisión HLS con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3bf01-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="3bf01-180">Para habilitar el cifrado de FairPlay, debe proporcionar el certificado de la aplicación y la clave de secreto de aplicación (ASK) mediante la opción de configuración de FairPlay de la hoja de configuración de Content Protection.</span><span class="sxs-lookup"><span data-stu-id="3bf01-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="3bf01-182">Una vez realizada la selección de cifrado, pulse **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="3bf01-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="3bf01-183">Si va a planear la reproducción de una instancia de HLS cifrada mediante AES en Safari, vea [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="3bf01-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bf01-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bf01-184">Next steps</span></span>
<span data-ttu-id="3bf01-185">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="3bf01-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3bf01-186">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="3bf01-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

