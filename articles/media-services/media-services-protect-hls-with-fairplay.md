---
title: "Protección del contenido HLS con Microsoft PlayReady o Apple FairPlay | Microsoft Docs"
description: "Este tema ofrece información general y muestra cómo usar Servicios multimedia de Azure para cifrar dinámicamente el contenido HTTP Live Streaming (HLS) con Apple FairPlay. También muestra cómo utilizar el servicio de entrega de licencias de Servicios multimedia para entregar licencias de FairPlay a los clientes."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="8a96a-104">Protección del contenido HLS con Apple FairPlay o Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="8a96a-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="8a96a-105">Azure Media Services permite cifrar dinámicamente el contenido HTTP Live Streaming (HLS) usando los siguientes formatos:</span><span class="sxs-lookup"><span data-stu-id="8a96a-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="8a96a-106">**Clave sin cifrado de sobre AES-128**</span><span class="sxs-lookup"><span data-stu-id="8a96a-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="8a96a-107">El fragmento completo se cifra con el modo **AES-128 CBC**.</span><span class="sxs-lookup"><span data-stu-id="8a96a-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="8a96a-108">El reproductor de OS X e iOS admite el descifrado de la transmisión de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="8a96a-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="8a96a-109">Para más información, consulte [Uso del cifrado dinámico AES-128 y del servicio de entrega de claves](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="8a96a-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="8a96a-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="8a96a-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="8a96a-111">Las muestras de audio y vídeo individuales se cifran con el modo **AES-128 CBC**.</span><span class="sxs-lookup"><span data-stu-id="8a96a-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="8a96a-112">**FairPlay Streaming** (FPS) se integra en los sistemas operativos de dispositivos, con compatibilidad nativa en iOS y TV de Apple.</span><span class="sxs-lookup"><span data-stu-id="8a96a-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="8a96a-113">Safari en OS X habilita FPS utilizando la compatibilidad con la interfaz Encrypted Media Extensions (EME).</span><span class="sxs-lookup"><span data-stu-id="8a96a-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="8a96a-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="8a96a-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="8a96a-115">La siguiente imagen muestra el flujo de trabajo del **cifrado dinámico de HLS más FairPlay o PlayReady**.</span><span class="sxs-lookup"><span data-stu-id="8a96a-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagrama de flujo de trabajo de cifrado dinámico](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="8a96a-117">Este tema muestra cómo usar Media Services para cifrar dinámicamente el contenido HLS con FairPlay de Apple.</span><span class="sxs-lookup"><span data-stu-id="8a96a-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="8a96a-118">También muestra cómo utilizar el servicio de entrega de licencias de Servicios multimedia para entregar licencias de FairPlay a los clientes.</span><span class="sxs-lookup"><span data-stu-id="8a96a-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="8a96a-119">Si también quiere cifrar el contenido HLS con PlayReady, debe crear una clave de contenido común y asociarla con el recurso.</span><span class="sxs-lookup"><span data-stu-id="8a96a-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="8a96a-120">También tiene que configurar la directiva de autorización de la clave de contenido, como se describe en el tema [Uso de cifrado dinámico común de PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="8a96a-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="8a96a-121">Requisitos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="8a96a-121">Requirements and considerations</span></span>

<span data-ttu-id="8a96a-122">Cuando se usa Media Services para proporcionar HLS cifrado con FairPlay y entregar licencias de FairPlay se necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8a96a-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="8a96a-123">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8a96a-123">An Azure account.</span></span> <span data-ttu-id="8a96a-124">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8a96a-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="8a96a-125">Una cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="8a96a-125">A Media Services account.</span></span> <span data-ttu-id="8a96a-126">Para crear una, consulte [Creación de una cuenta de Azure Media Services mediante Azure Portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8a96a-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="8a96a-127">Suscríbase al [programa de desarrollo de Apple](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="8a96a-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="8a96a-128">En Apple es obligatorio que el propietario del contenido obtenga el [paquete de implementación](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="8a96a-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="8a96a-129">Indique que ya ha implementado el módulo principal de seguridad (KSM) con Media Services y que está solicitando el paquete FPS final.</span><span class="sxs-lookup"><span data-stu-id="8a96a-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="8a96a-130">Hay instrucciones que aparecen en el paquete FPS final para generar certificados y obtener la clave secreta de la aplicación (ASK).</span><span class="sxs-lookup"><span data-stu-id="8a96a-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="8a96a-131">Utilice la ASK para configurar FairPlay.</span><span class="sxs-lookup"><span data-stu-id="8a96a-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="8a96a-132">Versión **3.6.0** del SDK .NET de Servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="8a96a-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="8a96a-133">En la entrega de claves de Media Services se debe establecer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8a96a-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="8a96a-134">**Certificado de la aplicación (CA)**: se trata de un archivo .pfx que contiene la clave privada.</span><span class="sxs-lookup"><span data-stu-id="8a96a-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="8a96a-135">Puede crear este archivo y cifrarlo con una contraseña.</span><span class="sxs-lookup"><span data-stu-id="8a96a-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="8a96a-136">Cuando configure la directiva de entrega de claves, tiene que proporcionar esa contraseña y el archivo .pfx en formato Base64.</span><span class="sxs-lookup"><span data-stu-id="8a96a-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="8a96a-137">En los pasos siguientes se describe cómo generar un certificado pfx para FairPlay:</span><span class="sxs-lookup"><span data-stu-id="8a96a-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="8a96a-138">Instalación de OpenSSL desde https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="8a96a-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="8a96a-139">Vaya a la carpeta donde están los certificados FairPlay y otros archivos cuyo emisor sea Apple.</span><span class="sxs-lookup"><span data-stu-id="8a96a-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="8a96a-140">Ejecute el siguiente comando desde la línea de comando.</span><span class="sxs-lookup"><span data-stu-id="8a96a-140">Run the following command from the command line.</span></span> <span data-ttu-id="8a96a-141">Esto convierte el archivo .cer en un archivo .pem.</span><span class="sxs-lookup"><span data-stu-id="8a96a-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="8a96a-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="8a96a-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="8a96a-143">Ejecute el siguiente comando desde la línea de comando.</span><span class="sxs-lookup"><span data-stu-id="8a96a-143">Run the following command from the command line.</span></span> <span data-ttu-id="8a96a-144">Esto convierte el archivo .pem a un archivo .pfx con la clave privada.</span><span class="sxs-lookup"><span data-stu-id="8a96a-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="8a96a-145">A continuación, OpenSSL pide la contraseña para el archivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="8a96a-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="8a96a-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="8a96a-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="8a96a-147">**Contraseña de certificado de la aplicación**: la contraseña para crear el archivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="8a96a-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="8a96a-148">**Identificador de la contraseña de certificado de la aplicación**: tiene que cargar la contraseña de forma similar a como cargan otras claves de Media Services.</span><span class="sxs-lookup"><span data-stu-id="8a96a-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="8a96a-149">Use el valor de enumeración **ContentKeyType.FairPlayPfxPassword** para obtener el identificador de Media Services.</span><span class="sxs-lookup"><span data-stu-id="8a96a-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="8a96a-150">Esto es lo que se necesita usar dentro de la opción de directiva de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="8a96a-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="8a96a-151">**iv**: se trata de un valor aleatorio de 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="8a96a-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="8a96a-152">Tiene que coincidir con el iv de la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="8a96a-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="8a96a-153">El cliente genera el iv y lo pone en ambos lugares: en la directiva de entrega de recursos y en la opción de directiva de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="8a96a-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="8a96a-154">**ASK**: esta clave se recibe cuando se genera la certificación mediante el portal para desarrolladores de Apple (Apple Developer).</span><span class="sxs-lookup"><span data-stu-id="8a96a-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="8a96a-155">Cada equipo de desarrollo recibirá una única ASK.</span><span class="sxs-lookup"><span data-stu-id="8a96a-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="8a96a-156">Guarde una copia de la ASK y almacénela en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="8a96a-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="8a96a-157">Tendrá que configurar la ASK como FairPlayAsk en Media Services más adelante.</span><span class="sxs-lookup"><span data-stu-id="8a96a-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="8a96a-158">**Identificador de ASK**: este identificador se obtiene cuando se carga la ASK en Media Services.</span><span class="sxs-lookup"><span data-stu-id="8a96a-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="8a96a-159">Tiene que cargar la ASK mediante el valor de enumeración **ContentKeyType.FairPlayAsk**.</span><span class="sxs-lookup"><span data-stu-id="8a96a-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="8a96a-160">Como resultado, se obtiene el identificador de Media Services, que debe utilizarse al establecer la opción de directiva de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="8a96a-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="8a96a-161">En el lado cliente FPS se debe establecer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8a96a-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="8a96a-162">**Certificado de aplicación (CA)**: se trata de un archivo .cer/.der que contiene la clave pública que el sistema operativo usa para cifrar alguna carga útil.</span><span class="sxs-lookup"><span data-stu-id="8a96a-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="8a96a-163">Media Services necesita tener información sobre él porque lo necesita el reproductor.</span><span class="sxs-lookup"><span data-stu-id="8a96a-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="8a96a-164">El servicio de entrega de claves lo descifra utilizando la clave privada correspondiente.</span><span class="sxs-lookup"><span data-stu-id="8a96a-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="8a96a-165">Para reproducir una transmisión cifrada FairPlay, obtenga primero la ASK real y luego genere un certificado real.</span><span class="sxs-lookup"><span data-stu-id="8a96a-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="8a96a-166">Este proceso crea todas las tres partes:</span><span class="sxs-lookup"><span data-stu-id="8a96a-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="8a96a-167">archivo .der</span><span class="sxs-lookup"><span data-stu-id="8a96a-167">.der file</span></span>
  * <span data-ttu-id="8a96a-168">archivo .pfx</span><span class="sxs-lookup"><span data-stu-id="8a96a-168">.pfx file</span></span>
  * <span data-ttu-id="8a96a-169">la contraseña para el archivo .pfx</span><span class="sxs-lookup"><span data-stu-id="8a96a-169">password for the .pfx</span></span>

<span data-ttu-id="8a96a-170">Los siguientes clientes son compatibles con HLS con cifrado **AES-128 CBC**: Safari en OS X, TV Apple e iOS.</span><span class="sxs-lookup"><span data-stu-id="8a96a-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="8a96a-171">Configuración del cifrado dinámico y los servicios de entrega de licencias de FairPlay</span><span class="sxs-lookup"><span data-stu-id="8a96a-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="8a96a-172">Estos son los pasos generales para proteger los recursos con FairPlay, mediante el servicio de entrega de licencias de Media Services y también mediante cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="8a96a-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="8a96a-173">Creación de un recurso y carga de los archivos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="8a96a-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="8a96a-174">Codificación del recurso que contiene el archivo para el conjunto de MP4 de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="8a96a-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="8a96a-175">Creación de una clave de contenido y su asociación con el recurso codificado.</span><span class="sxs-lookup"><span data-stu-id="8a96a-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="8a96a-176">Configuración de la directiva de autorización de la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="8a96a-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="8a96a-177">Especifique lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8a96a-177">Specify the following:</span></span>

   * <span data-ttu-id="8a96a-178">Método de entrega (en este caso, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="8a96a-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="8a96a-179">Configuración de opciones de directiva de FairPlay.</span><span class="sxs-lookup"><span data-stu-id="8a96a-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="8a96a-180">Para más detalles sobre cómo configurar FairPlay, consulte el método **ConfigureFairPlayPolicyOptions()** en el ejemplo más adelante.</span><span class="sxs-lookup"><span data-stu-id="8a96a-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8a96a-181">En general, lo más seguro es que configure las opciones de directiva de FairPlay solo una vez, ya que solo tendrá un conjunto de certificados y una ASK.</span><span class="sxs-lookup"><span data-stu-id="8a96a-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="8a96a-182">Restricciones (abiertas o token).</span><span class="sxs-lookup"><span data-stu-id="8a96a-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="8a96a-183">La información específica del tipo de entrega de claves que define cómo se entrega la clave al cliente.</span><span class="sxs-lookup"><span data-stu-id="8a96a-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="8a96a-184">Configuración de directivas de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="8a96a-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="8a96a-185">La configuración de directiva de entrega incluye:</span><span class="sxs-lookup"><span data-stu-id="8a96a-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="8a96a-186">Protocolo de entrega (HLS).</span><span class="sxs-lookup"><span data-stu-id="8a96a-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="8a96a-187">El tipo de cifrado dinámico (cifrado CBC común).</span><span class="sxs-lookup"><span data-stu-id="8a96a-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="8a96a-188">La dirección URL de adquisición de licencias.</span><span class="sxs-lookup"><span data-stu-id="8a96a-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8a96a-189">Si desea entregar una transmisión que se cifra con FairPlay + otro sistema de administración de derechos digitales (DRM), tiene que configurar directivas de entrega independientes:</span><span class="sxs-lookup"><span data-stu-id="8a96a-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="8a96a-190">Una IAssetDeliveryPolicy para configurar Dynamic Adaptive Streaming sobre HTTP (DASH) con Common Encryption (CENC) (PlayReady + Widevine), y Smooth con PlayReady</span><span class="sxs-lookup"><span data-stu-id="8a96a-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="8a96a-191">Otra IAssetDeliveryPolicy para configurar FairPlay para HLS</span><span class="sxs-lookup"><span data-stu-id="8a96a-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="8a96a-192">Creación de un localizador a petición para obtener una URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="8a96a-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="8a96a-193">Uso de la entrega de la clave FairPlay por aplicaciones reproductor</span><span class="sxs-lookup"><span data-stu-id="8a96a-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="8a96a-194">Puede desarrollar aplicaciones de reproductor usando el SDK de iOS.</span><span class="sxs-lookup"><span data-stu-id="8a96a-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="8a96a-195">Para poder reproducir el contenido de FairPlay, tiene que implementar el protocolo de intercambio de licencias.</span><span class="sxs-lookup"><span data-stu-id="8a96a-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="8a96a-196">Apple no especifica este protocolo.</span><span class="sxs-lookup"><span data-stu-id="8a96a-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="8a96a-197">Depende de cada aplicación decidir cómo enviar las solicitudes de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="8a96a-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="8a96a-198">El servicio de entrega de claves de FairPlay de Media Services espera que SPC funcione como mensaje de publicación codificado www-form-url con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8a96a-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="8a96a-199">Reproductor multimedia de Azure no admite la reproducción de FairPlay de fábrica.</span><span class="sxs-lookup"><span data-stu-id="8a96a-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="8a96a-200">Para tener la reproducción de FairPlay en MAC OS X, obtenga el reproductor de ejemplo de la cuenta de desarrollador de Apple.</span><span class="sxs-lookup"><span data-stu-id="8a96a-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="8a96a-201">Direcciones URL de streaming</span><span class="sxs-lookup"><span data-stu-id="8a96a-201">Streaming URLs</span></span>
<span data-ttu-id="8a96a-202">Si el recurso se cifró con más de un DRM, debe usar una etiqueta de cifrado en la dirección URL de streaming: (formato = 'm3u8-aapl', cifrado = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="8a96a-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="8a96a-203">Se aplican las siguientes consideraciones:</span><span class="sxs-lookup"><span data-stu-id="8a96a-203">The following considerations apply:</span></span>

* <span data-ttu-id="8a96a-204">Se puede especificar solo un tipo de cifrado o ninguno.</span><span class="sxs-lookup"><span data-stu-id="8a96a-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="8a96a-205">El tipo de cifrado no tiene que especificarse en la dirección URL si solo se aplicó un cifrado al recurso.</span><span class="sxs-lookup"><span data-stu-id="8a96a-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="8a96a-206">El tipo de cifrado distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8a96a-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="8a96a-207">Se pueden especificar los siguientes tipos de cifrado:</span><span class="sxs-lookup"><span data-stu-id="8a96a-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="8a96a-208">**cenc**: cifrado común (PlayReady o Widevine)</span><span class="sxs-lookup"><span data-stu-id="8a96a-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="8a96a-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="8a96a-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="8a96a-210">**cbc**: cifrado de sobre AES</span><span class="sxs-lookup"><span data-stu-id="8a96a-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8a96a-211">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a96a-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="8a96a-212">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8a96a-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="8a96a-213">Agregue los siguientes elementos al elemento **appSettings** definido en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="8a96a-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="8a96a-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a96a-214">Example</span></span>

<span data-ttu-id="8a96a-215">El ejemplo siguiente muestra la capacidad para usar Media Services para entregar el contenido cifrado con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="8a96a-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="8a96a-216">Esta funcionalidad se introdujo en el SDK de Azure Media Services para .NET versión 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="8a96a-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="8a96a-217">Sobrescriba el código del archivo Program.cs con el código mostrado en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8a96a-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="8a96a-218">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="8a96a-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8a96a-219">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="8a96a-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8a96a-220">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="8a96a-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="8a96a-221">Asegúrese de actualizar las variables para que apunten a las carpetas donde se encuentran los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="8a96a-221">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="8a96a-222">Siguientes pasos: Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="8a96a-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8a96a-223">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="8a96a-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
