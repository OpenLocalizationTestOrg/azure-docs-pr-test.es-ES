---
title: aaaProtect de contenido HLS con Microsoft PlayReady o Apple FairPlay - Azure | Documentos de Microsoft
description: "Este tema proporciona información general y muestra cómo toouse servicios multimedia de Azure toodynamically cifrar el contenido HTTP Live Streaming (HLS) con FairPlay de Apple. También muestra cómo toouse Hola servicios multimedia de licencia toodeliver de servicio de entrega tooclients de licencias FairPlay."
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
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="4e0bb-104">Protección del contenido HLS con Apple FairPlay o Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="4e0bb-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="4e0bb-105">Azure Media Services permite toodynamically cifrar el contenido de HTTP Live Streaming (HLS) mediante el uso de hello siguientes formatos:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="4e0bb-106">**Clave sin cifrado de sobre AES-128**</span><span class="sxs-lookup"><span data-stu-id="4e0bb-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="4e0bb-107">Hello fragmento completo se cifra con hello **AES-128 CBC** modo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="4e0bb-108">descifrado de Hola de secuencia de hello es compatible con iOS y el Reproductor de OS X de la forma nativa.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="4e0bb-109">Para más información, consulte [Uso del cifrado dinámico AES-128 y del servicio de entrega de claves](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="4e0bb-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="4e0bb-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="4e0bb-111">Hola individual vídeo y muestras de audio se cifran mediante el uso de hello **AES-128 CBC** modo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="4e0bb-112">**Transmisión por secuencias de FairPlay** (FPS) se integra en hello sistemas operativos de dispositivos, con compatibilidad nativa en iOS y Apple TV.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="4e0bb-113">Safari en OS X permite FPS utilizando el soporte de interfaz de hello las extensiones de medios de cifrado (EME).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="4e0bb-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="4e0bb-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="4e0bb-115">Hello siguiente imagen muestra hello **HLS + FairPlay o PlayReady cifrado dinámico** flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagrama de flujo de trabajo de cifrado dinámico](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="4e0bb-117">Este tema muestra cómo toouse servicios multimedia toodynamically cifrar el contenido HLS con FairPlay de Apple.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="4e0bb-118">También muestra cómo toouse Hola servicios multimedia de licencia toodeliver de servicio de entrega tooclients de licencias FairPlay.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0bb-119">Si también desea tooencrypt su HLS contenido con PlayReady, es necesario toocreate una clave de contenido común y asociarlo con el recurso.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="4e0bb-120">También deberá directiva de autorización de tooconfigure Hola la clave de contenido, tal y como se describe en [cifrado dinámico comunes de usar PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="4e0bb-121">Requisitos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="4e0bb-121">Requirements and considerations</span></span>

<span data-ttu-id="4e0bb-122">Hola se necesita siguiente al usar toodeliver de servicios multimedia que HLS cifrado con FairPlay y toodeliver FairPlay licencias:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="4e0bb-123">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-123">An Azure account.</span></span> <span data-ttu-id="4e0bb-124">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="4e0bb-125">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-125">A Media Services account.</span></span> <span data-ttu-id="4e0bb-126">toocreate uno, vea [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="4e0bb-127">Suscríbase al [programa de desarrollo de Apple](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="4e0bb-128">Apple requiere Hola de hello propietario del contenido tooobtain [paquete de implementación](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="4e0bb-129">Estado que ya se ha implementado módulo de seguridad de clave (KSM) con servicios multimedia, por lo que está solicitando paquete FPS final de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="4e0bb-130">Hay instrucciones de hello FPS final toogenerate certificación del paquete y obtener Hola clave de secreto de aplicación (consulte).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="4e0bb-131">Utilice ASK tooconfigure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="4e0bb-132">Versión **3.6.0** del SDK .NET de Servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="4e0bb-133">Hola después cosas debe establecerse en el lado de la entrega de claves de servicios multimedia:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="4e0bb-134">**Aplicación de certificados (CA)**: se trata de un archivo .pfx que contiene la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="4e0bb-135">Puede crear este archivo y cifrarlo con una contraseña.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="4e0bb-136">Cuando se configura una directiva de entrega de claves, debe proporcionar ese archivo .pfx hello y la contraseña en formato Base64.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="4e0bb-137">Hola pasos describe cómo archivo toogenerate un certificado .pfx para FairPlay:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="4e0bb-138">Instalación de OpenSSL desde https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="4e0bb-139">Vaya a carpeta de toohello donde se certificado FairPlay de Hola y otros archivos entregados por Apple.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="4e0bb-140">Ejecute hello siguiente comando desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="4e0bb-141">Esto convierte el archivo PEM tooa de hello .cer archivo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="4e0bb-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="4e0bb-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="4e0bb-143">Ejecute hello siguiente comando desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="4e0bb-144">Esto convierte el archivo .pfx tooa de hello PEM archivo con clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="4e0bb-145">contraseña de Hola para archivo hello, a continuación, se pide al OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="4e0bb-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="4e0bb-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="4e0bb-147">**Contraseña del certificado de la aplicación**: contraseña de Hola para crear el archivo .pfx de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="4e0bb-148">**Id. de la contraseña de certificado de la aplicación**: debe cargar contraseña hello, toohow similar cargan otras claves de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="4e0bb-149">Hola de uso **ContentKeyType.FairPlayPfxPassword** Hola de tooget valor enum identificador de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="4e0bb-150">Esto es lo necesitan toouse dentro de la opción de directiva de entrega de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="4e0bb-151">**iv**: se trata de un valor aleatorio de 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="4e0bb-152">Debe coincidir con Hola iv en directiva de entrega de hello activo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="4e0bb-153">Generar Hola iv y colóquelo en ambos lugares: directiva de entrega del activo de Hola y la opción de directiva de entrega de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="4e0bb-154">**PIDA**: esta clave se recibe cuando genere certificación hello mediante portal para desarrolladores de Apple Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="4e0bb-155">Cada equipo de desarrollo recibirá una única ASK.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="4e0bb-156">Guardar una copia del programa Hola a FORMULAR y almacenarlo en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="4e0bb-157">Más adelante necesitará tooconfigure ASK como FairPlayAsk tooMedia servicios.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="4e0bb-158">**Identificador de ASK**: este identificador se obtiene cuando se carga la ASK en Media Services.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="4e0bb-159">Debe cargar ASK mediante hello **ContentKeyType.FairPlayAsk** valor enum.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="4e0bb-160">Como resultado de hello, se devuelve el Id. de servicios multimedia de Hola y esto es lo que se debe usar al establecer la opción de directiva de entrega de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="4e0bb-161">Hello lo siguiente debe establecerse por hello cliente FPS:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="4e0bb-162">**Aplicación de certificados (CA)**: se trata de un archivo.cer/.der que contiene la clave pública de hello, sistema operativo hello usa tooencrypt algunos carga.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="4e0bb-163">Servicios multimedia debe tooknow sobre él porque es necesaria para el Reproductor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="4e0bb-164">servicio de entrega de claves de Hello descifra mediante la clave privada correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="4e0bb-165">tooplay hacer copia de una secuencia cifrada FairPlay, obtener primero un ASK real y, a continuación, generar un certificado real.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="4e0bb-166">Este proceso crea todas las tres partes:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="4e0bb-167">archivo .der</span><span class="sxs-lookup"><span data-stu-id="4e0bb-167">.der file</span></span>
  * <span data-ttu-id="4e0bb-168">archivo .pfx</span><span class="sxs-lookup"><span data-stu-id="4e0bb-168">.pfx file</span></span>
  * <span data-ttu-id="4e0bb-169">contraseña de hello .pfx</span><span class="sxs-lookup"><span data-stu-id="4e0bb-169">password for hello .pfx</span></span>

<span data-ttu-id="4e0bb-170">Hello siguientes clientes admiten HLS con **AES-128 CBC** cifrado: Safari en OS X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="4e0bb-171">Configuración del cifrado dinámico y los servicios de entrega de licencias de FairPlay</span><span class="sxs-lookup"><span data-stu-id="4e0bb-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="4e0bb-172">Hola siguientes pasos son generales para proteger sus activos con FairPlay mediante servicio de entrega de licencias de servicios multimedia de hello y también mediante el uso de cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="4e0bb-173">Crear un activo y cargar archivos en el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="4e0bb-174">Codificar el activo de Hola que contenga Hola archivo toohello velocidad de bits adaptativa que MP4 establecido.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="4e0bb-175">Crear una clave de contenido y asociarla a activos de hello codificado.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="4e0bb-176">Configurar la directiva de autorización de la clave de hello contenido.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="4e0bb-177">Especifique Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-177">Specify hello following:</span></span>

   * <span data-ttu-id="4e0bb-178">método de entrega de Hello (en este caso, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="4e0bb-179">Configuración de opciones de directiva de FairPlay.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="4e0bb-180">Para obtener más información acerca de cómo tooconfigure FairPlay, vea hello **ConfigureFairPlayPolicyOptions()** método en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4e0bb-181">Por lo general, sería aconsejable tooconfigure FairPlay directiva opciones sólo una vez, ya que sólo tendrá un conjunto de una entidad y un ASK.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="4e0bb-182">Restricciones (abiertas o token).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="4e0bb-183">Tipo de la entrega de claves de toohello específico información que define cómo clave Hola se entrega a toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="4e0bb-184">Configurar directiva de entrega de hello activo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="4e0bb-185">configuración de directiva de entrega de Hello incluye:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="4e0bb-186">Protocolo de entrega de Hello (HLS).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="4e0bb-187">tipo de Hola de cifrado dinámico (cifrado CBC común).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="4e0bb-188">dirección URL de adquisición de licencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4e0bb-189">Si desea toodeliver una secuencia que se cifra con FairPlay y otro sistema de administración de derechos digitales (DRM), tienen directivas de entrega diferente de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="4e0bb-190">Una tooconfigure IAssetDeliveryPolicy dinámica transmisión por secuencias adaptativa sobre HTTP (guión) con CENC (Common Encryption) (PlayReady + Widevine) y suave con PlayReady</span><span class="sxs-lookup"><span data-stu-id="4e0bb-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="4e0bb-191">Otro IAssetDeliveryPolicy tooconfigure FairPlay para HLS</span><span class="sxs-lookup"><span data-stu-id="4e0bb-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="4e0bb-192">Crear un tooget de localizador OnDemand una URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="4e0bb-193">Uso de la entrega de la clave FairPlay por aplicaciones reproductor</span><span class="sxs-lookup"><span data-stu-id="4e0bb-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="4e0bb-194">Puede desarrollar aplicaciones de Reproductor mediante el uso de SDK de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="4e0bb-195">tooplay toobe capaz de FairPlay contenido, tendrá protocolo de intercambio de licencias de tooimplement Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="4e0bb-196">Apple no especifica este protocolo.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="4e0bb-197">Es la aplicación de tooeach cómo solicita toosend entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="4e0bb-198">Hola servicio de entrega de clave de Media Services FairPlay espera Hola SPC toocome como un mensaje de post codificados www-form-url, Hola siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="4e0bb-199">El Reproductor multimedia de Azure no admita la reproducción de FairPlay fuera del cuadro de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="4e0bb-200">reproducción de FairPlay tooget en MAC OS X para obtenerlo Reproductor de ejemplo de Hola Hola cuenta de desarrollador de Apple.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="4e0bb-201">Direcciones URL de streaming</span><span class="sxs-lookup"><span data-stu-id="4e0bb-201">Streaming URLs</span></span>
<span data-ttu-id="4e0bb-202">Si el recurso se cifró con DRM de más de una, debe usar una etiqueta de cifrado en hello transmisión por secuencias de dirección URL: (formato = 'm3u8-aapl' cifrado = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="4e0bb-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="4e0bb-203">Hola siguientes consideraciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-203">hello following considerations apply:</span></span>

* <span data-ttu-id="4e0bb-204">Se puede especificar solo un tipo de cifrado o ninguno.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="4e0bb-205">tipo de cifrado de Hello no tiene toobe especificado en dirección URL de hello si solo un cifrado estaba activo toohello aplicada.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="4e0bb-206">tipo de cifrado de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="4e0bb-207">Hola siguientes tipos de cifrado se puede especificar:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="4e0bb-208">**cenc**: cifrado común (PlayReady o Widevine)</span><span class="sxs-lookup"><span data-stu-id="4e0bb-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="4e0bb-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="4e0bb-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="4e0bb-210">**cbc**: cifrado de sobre AES</span><span class="sxs-lookup"><span data-stu-id="4e0bb-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4e0bb-211">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e0bb-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="4e0bb-212">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="4e0bb-213">Agregar Hola después elementos demasiado**appSettings** definido en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="4e0bb-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4e0bb-214">Example</span></span>

<span data-ttu-id="4e0bb-215">Hola siguiente ejemplo muestra hello capacidad toouse toodeliver de servicios multimedia el contenido cifrado con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="4e0bb-216">Esta funcionalidad se introdujo en hello SDK de servicios multimedia de Azure para .NET versión 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="4e0bb-217">Sobrescribir el código de hello en el archivo Program.cs con el código de hello que se muestra en esta sección.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="4e0bb-218">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="4e0bb-219">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="4e0bb-220">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="4e0bb-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="4e0bb-221">Seguro tooupdate que las variables sean toopoint toofolders donde se encuentran los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
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

            // Associate hello key with hello asset.
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

            // Associate hello content key authorization policy with hello content key.
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

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="4e0bb-222">Siguientes pasos: Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="4e0bb-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4e0bb-223">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="4e0bb-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
