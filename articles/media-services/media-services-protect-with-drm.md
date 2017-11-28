---
title: "Uso de cifrado dinámico común de PlayReady o Widevine | Microsoft Docs"
description: "Servicios multimedia de Microsoft Azure le permute entregar secuencias MPEG-DASH, Smooth Streaming y Http-Live-Streaming (HLS) protegidas con DRM de Microsoft PlayReady. AMS también le permite entregar DASH cifrado con DRM de Widevine. En este tema se muestra cómo realizar cifrado dinámico con DRM de PlayReady y Widevine."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 6cfb7b558b8dce511d517e69c022765feae245fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="d8380-105">Uso de cifrado dinámico común de PlayReady o Widevine</span><span class="sxs-lookup"><span data-stu-id="d8380-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8380-106">.NET</span><span class="sxs-lookup"><span data-stu-id="d8380-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="d8380-107">Java</span><span class="sxs-lookup"><span data-stu-id="d8380-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="d8380-108">PHP</span><span class="sxs-lookup"><span data-stu-id="d8380-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="d8380-109">Servicios multimedia de Microsoft Azure le permite entregar secuencias MPEG-DASH, Smooth Streaming y Http-Live-Streaming (HLS) protegidas con [DRM de Microsoft PlayReady](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="d8380-109">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="d8380-110">También permite entregar transmisiones DASH cifradas con licencias DRM de Widevine.</span><span class="sxs-lookup"><span data-stu-id="d8380-110">It also enables you to deliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="d8380-111">Tanto PlayReady como Widewine se cifran según la especificación de cifrado común (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="d8380-111">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="d8380-112">Puede usar el [.NET SDK de AMS](https://www.nuget.org/packages/windowsazure.mediaservices/) (a partir de la versión 3.5.1) o la API de REST para configurar AssetDeliveryConfiguration para usar Widevine.</span><span class="sxs-lookup"><span data-stu-id="d8380-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with the version 3.5.1) or REST API to configure your AssetDeliveryConfiguration to use Widevine.</span></span>

<span data-ttu-id="d8380-113">Servicios multimedia proporciona un servicio para entregar licencias DRM de PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="d8380-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="d8380-114">Servicios multimedia también proporciona unas API que permiten configurar los derechos y las restricciones que desee aplicar en tiempo de ejecución de DRM de PlayReady o Widevine cuando un usuario reproduzca contenido protegido.</span><span class="sxs-lookup"><span data-stu-id="d8380-114">Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span></span> <span data-ttu-id="d8380-115">Cuando un usuario solicita contenido protegido con DRM, la aplicación del reproductor solicitará una licencia del servicio de licencias de AMS.</span><span class="sxs-lookup"><span data-stu-id="d8380-115">When a user requests a DRM protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="d8380-116">El servicio de licencias de AMS emitirá una licencia al reproductor, si está autorizado.</span><span class="sxs-lookup"><span data-stu-id="d8380-116">The AMS license service will issue a license to the player if it is authorized.</span></span> <span data-ttu-id="d8380-117">Una licencia de PlayReady o Widevine contiene la clave de descifrado que puede usar el reproductor cliente para descifrar y transmitir el contenido.</span><span class="sxs-lookup"><span data-stu-id="d8380-117">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="d8380-118">También puede usar los siguientes asociados de AMS para ayudarle a entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/) y [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="d8380-118">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="d8380-119">Para obtener más información, consulte: integración con [Axinom](media-services-axinom-integration.md) y [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="d8380-120">Servicios multimedia admite varias formas de autorizar a los usuarios que realizan solicitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="d8380-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="d8380-121">La directiva de autorización de claves de acceso podría tener una o más restricciones de autorización: abrir o restricción de token.</span><span class="sxs-lookup"><span data-stu-id="d8380-121">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="d8380-122">La directiva con restricción token debe ir acompañada de un token emitido por un Servicio de tokens seguros (STS).</span><span class="sxs-lookup"><span data-stu-id="d8380-122">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="d8380-123">Media Services admite tokens en formato [Token de web simple (SWT)](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) y en formato [JSON Web Token (JWT)](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3).</span><span class="sxs-lookup"><span data-stu-id="d8380-123">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="d8380-124">Para obtener más información, consulte Configuración de la directiva de autorización de la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="d8380-124">For more information, see Configure the content key’s authorization policy.</span></span>

<span data-ttu-id="d8380-125">Para aprovechar las ventajas del cifrado dinámico, debe disponer de un recurso que contenga un conjunto de archivos MP4 o archivos de origen Smooth Streaming, de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="d8380-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="d8380-126">También es preciso configurar las directivas de entrega del recurso (se describe más adelante en este tema).</span><span class="sxs-lookup"><span data-stu-id="d8380-126">You also need to configure the delivery policies for the asset (described later in this topic).</span></span> <span data-ttu-id="d8380-127">Luego, según el formato especificado en la URL de streaming, el servidor de streaming a petición se asegurará de que se reciba la secuencia en el protocolo elegido.</span><span class="sxs-lookup"><span data-stu-id="d8380-127">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="d8380-128">Como resultado, solo tendrá que almacenar y pagar los archivos en un solo formato de almacenamiento y Servicios multimedia compilará y proporcionará la respuesta adecuada en función de cada solicitud de un cliente.</span><span class="sxs-lookup"><span data-stu-id="d8380-128">As a result, you only need to store and pay for the files in a single storage format and Media Services will build and serve the appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="d8380-129">Este tema será útil para los desarrolladores que trabajan en aplicaciones que entregan medios protegidos con varios DRM, por ejemplo, PlayReady y Widevine.</span><span class="sxs-lookup"><span data-stu-id="d8380-129">This topic would be useful to developers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="d8380-130">En este tema se muestra cómo configurar el servicio de entrega de licencias de PlayReady con directivas de autorización para que solo los clientes autorizados puedan recibir licencias de PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="d8380-130">The topic shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="d8380-131">También muestra cómo usar el cifrado dinámico con DRM de PlayReady o Widevine a través de DASH.</span><span class="sxs-lookup"><span data-stu-id="d8380-131">It also shows how to use dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="d8380-132">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="d8380-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d8380-133">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="d8380-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="d8380-134">Descarga de un ejemplo</span><span class="sxs-lookup"><span data-stu-id="d8380-134">Download sample</span></span>
<span data-ttu-id="d8380-135">Puede descargar el ejemplo descrito en este artículo [aquí](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="d8380-135">You can download the sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="d8380-136">Configuración del cifrado dinámico común y el servicio de entrega de licencias DRM</span><span class="sxs-lookup"><span data-stu-id="d8380-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="d8380-137">Éstos son los pasos generales que deberá realizar al proteger sus recursos con PlayReady, mediante el servicio de entrega de licencias de Servicios multimedia y también mediante cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="d8380-137">The following are general steps that you would need to perform when protecting your assets with PlayReady, using the Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="d8380-138">Creación de un recurso y carga de los archivos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="d8380-138">Create an asset and upload files into the asset.</span></span>
2. <span data-ttu-id="d8380-139">Codificación del recurso que contiene el archivo con Adaptive Bitrate MP4 Set.</span><span class="sxs-lookup"><span data-stu-id="d8380-139">Encode the asset containing the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="d8380-140">Creación de una clave de contenido y su asociación con el recurso codificado.</span><span class="sxs-lookup"><span data-stu-id="d8380-140">Create a content key and associate it with the encoded asset.</span></span> <span data-ttu-id="d8380-141">En Servicios multimedia, la clave de contenido contiene la clave de cifrado del recurso.</span><span class="sxs-lookup"><span data-stu-id="d8380-141">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="d8380-142">Configuración de la directiva de autorización de la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="d8380-142">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="d8380-143">El usuario debe configurar la directiva de autorización de claves y el cliente (reproductor) debe conocerla para que se le entregue la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="d8380-143">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>

    <span data-ttu-id="d8380-144">Al crear la directiva de autorización de claves de contenido, debe especificar lo siguiente: método de entrega (PlayReady o Widevine), restricciones (abiertas o tokens) e información específica del tipo de entrega de claves que define cómo se entrega la clave al cliente (plantilla de licencia [PlayReady](media-services-playready-license-template-overview.md) o [Widevine](media-services-widevine-license-template-overview.md)).</span><span class="sxs-lookup"><span data-stu-id="d8380-144">When creating the content key authorization policy, you need to specify the following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="d8380-145">Configuración de la directiva de entrega para un recurso.</span><span class="sxs-lookup"><span data-stu-id="d8380-145">Configure the delivery policy for an asset.</span></span> <span data-ttu-id="d8380-146">La configuración de directivas de entrega incluye: el protocolo de entrega (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), el tipo de cifrado dinámico (por ejemplo, cifrado común) y la URL de adquisición de licencias de PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="d8380-146">The delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="d8380-147">Puede aplicar diferentes directivas a cada protocolo en el mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="d8380-147">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="d8380-148">Por ejemplo, puede aplicar cifrado PlayReady a Smooth/DASH y AES Envelope a HLS.</span><span class="sxs-lookup"><span data-stu-id="d8380-148">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="d8380-149">Se bloqueará la transmisión para todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, si agrega una sola directiva que solo especifica HLS como el protocolo).</span><span class="sxs-lookup"><span data-stu-id="d8380-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d8380-150">La excepción a esta regla se produce en el caso de que no haya definido ninguna directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8380-150">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d8380-151">En tal caso, todos los protocolos estarán habilitados sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="d8380-151">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="d8380-152">Creación de un localizador a petición para obtener una URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="d8380-152">Create an OnDemand locator in order to get a streaming URL.</span></span>

<span data-ttu-id="d8380-153">Al final del tema encontrará un ejemplo de .NET completo.</span><span class="sxs-lookup"><span data-stu-id="d8380-153">You will find a complete .NET example at the end of the topic.</span></span>

<span data-ttu-id="d8380-154">La siguiente imagen muestra el flujo de trabajo que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d8380-154">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="d8380-155">Aquí el token se usa para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d8380-155">Here the token is used for authentication.</span></span>

![Protección con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="d8380-157">El resto de este tema proporciona explicaciones detalladas, ejemplos de código y vínculos a temas que le muestran cómo lograr las tareas descritas arriba.</span><span class="sxs-lookup"><span data-stu-id="d8380-157">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="d8380-158">Limitaciones actuales</span><span class="sxs-lookup"><span data-stu-id="d8380-158">Current limitations</span></span>
<span data-ttu-id="d8380-159">Si agrega o actualiza la directiva de entrega de recursos, debe eliminar el localizador asociado (si hay) y crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d8380-159">If you add or update an asset delivery policy, you must delete the associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="d8380-160">Limitación cuando se cifra con Widevine con Servicios multimedia de Azure: actualmente, no se admiten varias claves de contenido.</span><span class="sxs-lookup"><span data-stu-id="d8380-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-the-asset"></a><span data-ttu-id="d8380-161">Creación de un recurso y carga de los archivos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="d8380-161">Create an asset and upload files into the asset</span></span>
<span data-ttu-id="d8380-162">Para administrar, codificar y transmitir por secuencias sus vídeos, primero debe cargar el contenido en Servicios multimedia de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d8380-162">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="d8380-163">Una vez cargado, el contenido se almacena de forma segura en la nube para su posterior procesamiento y transmisión.</span><span class="sxs-lookup"><span data-stu-id="d8380-163">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="d8380-164">Para obtener información detallada, consulte [Carga de archivos en una cuenta de Servicios multimedia](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-the-asset-containing-the-file-to-the-adaptive-bitrate-mp4-set"></a><span data-ttu-id="d8380-165">Codificación del recurso que contiene el archivo con Adaptive Bitrate MP4 Set.</span><span class="sxs-lookup"><span data-stu-id="d8380-165">Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="d8380-166">Con el cifrado dinámico, todo lo que tiene que hacer es crear un recurso que contenga un conjunto de archivos MP4 o archivos Smooth Streaming, de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="d8380-166">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="d8380-167">Luego, según el formato especificado en la solicitud de manifiesto o de fragmento, el servidor de streaming a petición se asegurará de que reciba la transmisión en el protocolo elegido.</span><span class="sxs-lookup"><span data-stu-id="d8380-167">Then, based on the specified format in the manifest and fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="d8380-168">Como resultado, solo tendrá que almacenar y pagar los archivos en formato de almacenamiento único y Servicios multimedia creará y proporcionará la respuesta adecuada en función de las solicitudes de un cliente.</span><span class="sxs-lookup"><span data-stu-id="d8380-168">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="d8380-169">Para más información, consulte el tema [Información general sobre el empaquetado dinámico](media-services-dynamic-packaging-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="d8380-169">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="d8380-170">Para obtener instrucciones sobre cómo codificar, consulte [Codificación de un recurso mediante Codificador multimedia estándar](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-170">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="d8380-171"><a id="create_contentkey"></a>Creación de una clave de contenido y su asociación con el activo codificado</span><span class="sxs-lookup"><span data-stu-id="d8380-171"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="d8380-172">En Servicios multimedia, la clave de contenido contiene la clave con la que desea cifrar un recurso.</span><span class="sxs-lookup"><span data-stu-id="d8380-172">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="d8380-173">Para obtener más información, consulte [Creación de la clave de contenido](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="d8380-174"><a id="configure_key_auth_policy"></a>Configuración de la directiva de autorización de claves de contenido</span><span class="sxs-lookup"><span data-stu-id="d8380-174"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="d8380-175">Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="d8380-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="d8380-176">El usuario debe configurar la directiva de autorización de claves y el cliente (reproductor) debe conocerla para que se le entregue la clave.</span><span class="sxs-lookup"><span data-stu-id="d8380-176">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="d8380-177">La directiva de autorización de claves de acceso podría tener una o más restricciones de autorización: abrir o restricción de token.</span><span class="sxs-lookup"><span data-stu-id="d8380-177">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="d8380-178">Para obtener información detallada, consulte [Configuración de la directiva de autorización de claves de contenido](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="d8380-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="d8380-179"><a id="configure_asset_delivery_policy"></a>Configuración de directivas de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="d8380-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="d8380-180">Configure la directiva de entrega de sus recursos.</span><span class="sxs-lookup"><span data-stu-id="d8380-180">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="d8380-181">Algunos de los elementos que incluye la configuración de la directiva de entrega de recursos son:</span><span class="sxs-lookup"><span data-stu-id="d8380-181">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="d8380-182">La dirección URL de adquisición de licencias de DRM.</span><span class="sxs-lookup"><span data-stu-id="d8380-182">The DRM license acquisition URL.</span></span>
* <span data-ttu-id="d8380-183">El protocolo de entrega de recursos (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos).</span><span class="sxs-lookup"><span data-stu-id="d8380-183">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="d8380-184">El tipo de cifrado dinámico (en este caso, cifrado común).</span><span class="sxs-lookup"><span data-stu-id="d8380-184">The type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="d8380-185">Para obtener más información, consulte [Configuración de directivas de entrega de recursos ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="d8380-186"><a id="create_locator"></a>Creación de un localizador de streaming a petición para obtener una URL de streaming</span><span class="sxs-lookup"><span data-stu-id="d8380-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="d8380-187">Deberá suministrar al usuario la URL de streaming para Smooth, DASH o HLS.</span><span class="sxs-lookup"><span data-stu-id="d8380-187">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="d8380-188">Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d8380-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="d8380-189">Para obtener instrucciones sobre cómo publicar un recurso y generar una dirección URL de streaming, vea [Creación de una dirección URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-189">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="d8380-190">Obtención de un token de prueba</span><span class="sxs-lookup"><span data-stu-id="d8380-190">Get a test token</span></span>
<span data-ttu-id="d8380-191">Obtenga un token de prueba basado en la restricción de token que se usó para la directiva de autorización de claves.</span><span class="sxs-lookup"><span data-stu-id="d8380-191">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="d8380-192">Puede usar [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) para probar la secuencia.</span><span class="sxs-lookup"><span data-stu-id="d8380-192">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d8380-193">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8380-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d8380-194">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d8380-194">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d8380-195">Agregue los siguientes elementos al elemento **appSettings** definido en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="d8380-195">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="d8380-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d8380-196">Example</span></span>

<span data-ttu-id="d8380-197">En el ejemplo siguiente muestra la funcionalidad que se introdujo en el SDK de Servicios multimedia para .NET de Azure versión 3.5.2 (en concreto, la capacidad de definir una plantilla de licencia de Widevine y solicitar una licencia de Widevine de Servicios multimedia de Azure).</span><span class="sxs-lookup"><span data-stu-id="d8380-197">The following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, the ability to define a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="d8380-198">Sobrescriba el código del archivo Program.cs con el código mostrado en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d8380-198">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="d8380-199">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d8380-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d8380-200">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="d8380-200">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d8380-201">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="d8380-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d8380-202">Asegúrese de actualizar las variables para que apunten a las carpetas donde se encuentran los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="d8380-202">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
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

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
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

            // You can use the http://amsplayer.azurewebsites.net/azuremediaplayer.html player to test streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} to {1}",
                        inputAsset.Name,
                        encodingPreset));

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


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

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

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
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

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
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

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // The following code configures PlayReady License Template using .NET classes
            // and returns the XML string.

            //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user.
            //It contains a field for a custom data string between the license server and the application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // to be returned to the end users.
            //It contains the data on the content key in the license and any rights or restrictions to be
            //enforced by the PlayReady DRM runtime when using the content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether the license is persistent (saved in persistent storage on the client)
            //or non-persistent (only held in memory while the player is using the license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use the license or not.  
            // If true, the MinimumSecurityLevel property of the license
            // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class.
            // It grants the user the ability to playback the content subject to the zero or more restrictions
            // configured in the license and on the PlayRight itself (for playback specific policy).
            // Much of the policy on the PlayRight has to do with output restrictions
            // which control the types of outputs that the content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if the DigitalVideoOnlyContentRestriction is enabled,
            //then the DRM runtime will only allow the video to be displayed over digital outputs
            //(analog video outputs won’t be allowed to pass the content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience.
            // If the output protections are configured too restrictive,
            // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get the PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // to append /? KID =< keyId > to the end of the url when creating the manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in the delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
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


## <a name="next-step"></a><span data-ttu-id="d8380-203">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="d8380-203">Next step</span></span>
<span data-ttu-id="d8380-204">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d8380-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8380-205">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d8380-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d8380-206">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d8380-206">See also</span></span>
[<span data-ttu-id="d8380-207">CENC with Multi-DRM and Access Control (CENC con DRM múltiple y Control de acceso)</span><span class="sxs-lookup"><span data-stu-id="d8380-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="d8380-208">Configuración del empaquetado Widevine con AMS</span><span class="sxs-lookup"><span data-stu-id="d8380-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="d8380-209">Anuncio de los servicios de entrega de licencias de Google Widevine en Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="d8380-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
