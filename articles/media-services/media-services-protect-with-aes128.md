---
title: "Uso del cifrado dinámico AES-128 y del servicio de entrega de claves | Microsoft Docs"
description: "Servicios multimedia de Microsoft Azure le permite entregar el contenido cifrado con claves de cifrado AES de 128 bits. Servicios multimedia también proporciona el servicio de entrega de claves que distribuye claves de cifrado a los usuarios autorizados. En este tema se muestra cómo cifrar dinámicamente con AES-128 y usar el servicio de entrega de claves."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="9ee5c-105">Uso del cifrado dinámico AES-128 y del servicio de entrega de claves</span><span class="sxs-lookup"><span data-stu-id="9ee5c-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ee5c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9ee5c-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="9ee5c-107">Java</span><span class="sxs-lookup"><span data-stu-id="9ee5c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="9ee5c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="9ee5c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="9ee5c-109">Información general</span><span class="sxs-lookup"><span data-stu-id="9ee5c-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="9ee5c-110">Vea [este](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) vídeo para obtener información general sobre cómo proteger su contenido multimedia con el cifrado AES.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="9ee5c-111">Servicios multimedia de Microsoft Azure le permite entregar secuencias Http-Live-Streaming (HLS) y Smooth Streaming cifradas con el Estándar de cifrado avanzado (AES) (mediante claves de cifrado de 128 bits).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="9ee5c-112">Servicios multimedia también proporciona el servicio de entrega de claves que distribuye claves de cifrado a los usuarios autorizados.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="9ee5c-113">Si desea que Servicios multimedia cifre un recurso, debe asociar una clave de cifrado con el recurso y, además, configurar directivas de autorización para la clave.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="9ee5c-114">Cuando un reproductor solicita una secuencia, Servicios multimedia usa la clave especificada para cifrar de forma dinámica el contenido mediante AES.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="9ee5c-115">Para descifrar la secuencia, el reproductor solicitará la clave del servicio de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="9ee5c-116">Para decidir si el usuario está o no autorizado para obtener la clave, el servicio evalúa las directivas de autorización que especificó para la clave.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="9ee5c-117">Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="9ee5c-118">La directiva de autorización de claves de acceso podría tener una o más restricciones de autorización: abrir o restricción de token.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="9ee5c-119">La directiva con restricción token debe ir acompañada de un token emitido por un Servicio de tokens seguros (STS).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="9ee5c-120">Media Services admite tokens en formato [Token de web simple (SWT)](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) y en formato [JSON Web Token (JWT)](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="9ee5c-121">Para obtener más información, consulte [Configuración de la directiva de autorización de la clave de contenido](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="9ee5c-122">Para aprovechar las ventajas del cifrado dinámico, debe disponer de un recurso que contenga un conjunto de archivos MP4 o archivos de origen Smooth Streaming, de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="9ee5c-123">También debe configurar la directiva de entrega para el recurso (se describe más adelante en este tema).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="9ee5c-124">Luego, según el formato especificado en la URL de streaming, el servidor de streaming a petición se asegurará de que se reciba la secuencia en el protocolo elegido.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="9ee5c-125">Como resultado, solo tendrá que almacenar y pagar los archivos en formato de almacenamiento único y Servicios multimedia creará y proporcionará la respuesta adecuada en función de las solicitudes de un cliente.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="9ee5c-126">Este tema será útil para los desarrolladores que trabajan en aplicaciones que proporcionan contenido multimedia protegido.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="9ee5c-127">Se describe cómo configurar el servicio de entrega de claves con directivas de autorización para que solo los clientes autorizados puedan recibir las claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="9ee5c-128">También se describe cómo usar el cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="9ee5c-129">Flujo de trabajo de cifrado dinámico AES-128 y del servicio de entrega de claves</span><span class="sxs-lookup"><span data-stu-id="9ee5c-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="9ee5c-130">Éstos son los pasos generales que deberá realizar al cifrar los recursos con AES, mediante el servicio de entrega claves de Servicios multimedia y también mediante cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="9ee5c-131">[Creación de un recurso y carga de los archivos en el recurso](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="9ee5c-132">[Codificación del recurso que contiene el archivo con Adaptive Bitrate MP4 Set](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="9ee5c-133">[Creación de una clave de contenido y su asociación con el recurso codificado](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="9ee5c-134">En Servicios multimedia, la clave de contenido contiene la clave de cifrado del recurso.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="9ee5c-135">[Configuración de la directiva de autorización de la clave de contenido](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="9ee5c-136">El usuario debe configurar la directiva de autorización de claves y el cliente (reproductor) debe conocerla para que se le entregue la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="9ee5c-137">[Configuración de la directiva de entrega para un recurso](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="9ee5c-138">La configuración de la directiva de entrega incluye: la URL de adquisición de claves y vector de inicialización (IV) (AES 128 requiere que se suministre el mismo IV en el cifrado y descifrado), el protocolo de entrega (por ejemplo, MPEG DASH, HLS y Smooth Streaming o todos) y el tipo de cifrado dinámico (por ejemplo Envelope o sin cifrado dinámico).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="9ee5c-139">Puede aplicar diferentes directivas a cada protocolo en el mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="9ee5c-140">Por ejemplo, puede aplicar cifrado PlayReady a Smooth/DASH y AES Envelope a HLS.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="9ee5c-141">Se bloqueará la transmisión para todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, si agrega una sola directiva que solo especifica HLS como el protocolo).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="9ee5c-142">La excepción a esta regla se produce en el caso de que no haya definido ninguna directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="9ee5c-143">En tal caso, todos los protocolos estarán habilitados sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="9ee5c-144">[Creación de un localizador a petición](media-services-protect-with-aes128.md#create_locator) para obtener una URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="9ee5c-145">El tema también muestra [cómo una aplicación cliente puede solicitar una clave al servicio de entrega de claves](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="9ee5c-146">Encontrará un [ejemplo](media-services-protect-with-aes128.md#example) completo para .NET al final del tema.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="9ee5c-147">La siguiente imagen muestra el flujo de trabajo que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="9ee5c-148">Aquí el token se usa para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-148">Here the token is used for authentication.</span></span>

![Protección con AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="9ee5c-150">El resto de este tema proporciona explicaciones detalladas, ejemplos de código y vínculos a temas que le muestran cómo lograr las tareas descritas arriba.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="9ee5c-151">Limitaciones actuales</span><span class="sxs-lookup"><span data-stu-id="9ee5c-151">Current limitations</span></span>
<span data-ttu-id="9ee5c-152">Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="9ee5c-153"><a id="create_asset"></a>Creación de un recurso y carga de los archivos en el recurso</span><span class="sxs-lookup"><span data-stu-id="9ee5c-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="9ee5c-154">Para administrar, codificar y transmitir por secuencias sus vídeos, primero debe cargar el contenido en Servicios multimedia de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="9ee5c-155">Una vez cargado, el contenido se almacena de forma segura en la nube para su posterior procesamiento y transmisión.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="9ee5c-156">Para obtener información detallada, consulte [Carga de archivos en una cuenta de Servicios multimedia](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="9ee5c-157"><a id="encode_asset"></a>Codificación del activo que contiene el archivo con Adaptive Bitrate MP4 Set.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="9ee5c-158">Con el cifrado dinámico, todo lo que tiene que hacer es crear un recurso que contenga un conjunto de archivos MP4 o archivos Smooth Streaming, de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="9ee5c-159">Luego, según el formato especificado en la solicitud de manifiesto o fragmento, el servidor de streaming a petición se asegurará de que reciba la secuencia en el protocolo elegido.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="9ee5c-160">Como resultado, solo tendrá que almacenar y pagar los archivos en formato de almacenamiento único y Servicios multimedia creará y proporcionará la respuesta adecuada en función de las solicitudes de un cliente.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="9ee5c-161">Para más información, consulte el tema [Información general sobre el empaquetado dinámico](media-services-dynamic-packaging-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="9ee5c-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="9ee5c-162">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="9ee5c-163">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="9ee5c-164">Además, para poder usar el empaquetado dinámico y el cifrado dinámico, el recurso debe contener un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="9ee5c-165">Para obtener instrucciones sobre cómo codificar, consulte [Codificación de un recurso mediante Codificador multimedia estándar](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="9ee5c-166"><a id="create_contentkey"></a>Creación de una clave de contenido y su asociación con el activo codificado</span><span class="sxs-lookup"><span data-stu-id="9ee5c-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="9ee5c-167">En Servicios multimedia, la clave de contenido contiene la clave con la que desea cifrar un recurso.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="9ee5c-168">Para obtener más información, consulte [Creación de la clave de contenido](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="9ee5c-169"><a id="configure_key_auth_policy"></a>Configuración de la directiva de autorización de claves de contenido</span><span class="sxs-lookup"><span data-stu-id="9ee5c-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="9ee5c-170">Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="9ee5c-171">El usuario debe configurar la directiva de autorización de claves y el cliente (reproductor) debe conocerla para que se le entregue la clave.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="9ee5c-172">La directiva de autorización de clave de acceso podría tener una o más restricciones de autorización: abrir, restricción de token o restricción de IP.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="9ee5c-173">Para obtener información detallada, consulte [Configuración de la directiva de autorización de claves de contenido](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="9ee5c-174"><a id="configure_asset_delivery_policy"></a>Configuración de directivas de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="9ee5c-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="9ee5c-175">Configure la directiva de entrega de sus recursos.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="9ee5c-176">Algunos de los elementos que incluye la configuración de la directiva de entrega de recursos son:</span><span class="sxs-lookup"><span data-stu-id="9ee5c-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="9ee5c-177">La URL de adquisición de clave.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="9ee5c-178">El vector de inicialización (IV) que se usará para el cifrado Envelope.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="9ee5c-179">AES 128 requiere que se suministre el mismo IV en el cifrado y descifrado.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="9ee5c-180">El protocolo de entrega de recursos (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="9ee5c-181">El tipo de cifrado dinámico (por ejemplo, AES Envelope) o sin cifrado dinámico.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="9ee5c-182">Para obtener más información, consulte [Configuración de la directiva de entrega de recursos ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="9ee5c-183"><a id="create_locator"></a>Creación de un localizador de streaming a petición para obtener una URL de streaming</span><span class="sxs-lookup"><span data-stu-id="9ee5c-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="9ee5c-184">Deberá suministrar al usuario la URL de streaming para Smooth, DASH o HLS.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="9ee5c-185">Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="9ee5c-186">Para obtener instrucciones sobre cómo publicar un recurso y generar una dirección URL de streaming, vea [Creación de una dirección URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="9ee5c-187">Obtención de un token de prueba</span><span class="sxs-lookup"><span data-stu-id="9ee5c-187">Get a test token</span></span>
<span data-ttu-id="9ee5c-188">Obtenga un token de prueba basado en la restricción de token que se usó para la directiva de autorización de claves.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="9ee5c-189">Puede usar [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) para probar la secuencia.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="9ee5c-190"><a id="client_request"></a>Cómo el cliente puede solicitar una clave al servicio de entrega de claves</span><span class="sxs-lookup"><span data-stu-id="9ee5c-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="9ee5c-191">En el paso anterior, creó la URL que apunta a un archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="9ee5c-192">El cliente debe extraer la información necesaria de los archivos de manifiesto de streaming para realizar una solicitud al servicio de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="9ee5c-193">Archivos de manifiesto</span><span class="sxs-lookup"><span data-stu-id="9ee5c-193">Manifest files</span></span>
<span data-ttu-id="9ee5c-194">El cliente debe extraer el valor de la URL (que también contiene el identificador de la clave de contenido) del archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="9ee5c-195">El cliente intentará entonces obtener la clave de cifrado del servicio de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="9ee5c-196">El cliente también debe extraer el valor de IV y usarlo para descifrar la transmisión. El siguiente fragmento de código muestra el elemento <Protection> del manifiesto de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="9ee5c-197">En el caso de HLS, el manifiesto raíz se divide en archivos de segmento.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="9ee5c-198">Por ejemplo, el manifiesto raíz es http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) y contiene una lista de nombres de archivo de segmento.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="9ee5c-199">Si abre uno de los archivos de segmento en el editor de texto (por ejemplo, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), debe incluir #EXT-X-CLAVE, que indica que el archivo está cifrado.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="9ee5c-200">Si va a planear la reproducción de una instancia de HLS cifrada mediante AES en Safari, vea [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="9ee5c-201">Solicitud de la clave al servicio de entrega de claves</span><span class="sxs-lookup"><span data-stu-id="9ee5c-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="9ee5c-202">El código siguiente muestra cómo enviar una solicitud al servicio de entrega de claves de Media Services mediante un URI de entrega de claves (que se ha extrajo del manifiesto) y un token (en este tema no se habla de cómo obtener tokens web simples de un servicio de token seguro).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="9ee5c-203">Protección del contenido con AES-128 mediante .NET</span><span class="sxs-lookup"><span data-stu-id="9ee5c-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9ee5c-204">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9ee5c-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="9ee5c-205">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="9ee5c-206">Agregue los siguientes elementos al elemento **appSettings** definido en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="9ee5c-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="9ee5c-207"><a id="example"></a>Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9ee5c-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="9ee5c-208">Sobrescriba el código del archivo Program.cs con el código mostrado en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="9ee5c-209">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="9ee5c-210">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="9ee5c-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="9ee5c-211">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="9ee5c-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="9ee5c-212">Asegúrese de actualizar las variables para que apunten a las carpetas donde se encuentran los archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="9ee5c-212">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="9ee5c-213">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9ee5c-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9ee5c-214">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9ee5c-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

