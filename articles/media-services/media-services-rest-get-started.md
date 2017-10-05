---
title: "Introducción a la entrega de contenido a petición mediante REST | Microsoft Docs"
description: "Este tutorial le guiará por los pasos necesarios para implementar una aplicación de entrega de contenido a petición con Servicios multimedia de Azure mediante la API de REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="917da-103">Introducción a la entrega de contenido a petición mediante REST</span><span class="sxs-lookup"><span data-stu-id="917da-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="917da-104">Esta guía de inicio rápido le guiará por los pasos necesarios para implementar una aplicación de entrega de contenido de vídeo bajo demanda (VoD) mediante API de REST de Servicios multimedia de Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="917da-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="917da-105">Presenta el flujo de trabajo básico de Servicios multimedia y la mayoría de los objetos y tareas de programación más comunes necesarios para el desarrollo de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="917da-106">Al término del tutorial, podrá transmitir o cargar progresivamente un archivo multimedia de ejemplo que cargó, codificó y descargó.</span><span class="sxs-lookup"><span data-stu-id="917da-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="917da-107">En la ilustración siguiente se muestran algunos de los objetos que se utilizan con más frecuencia al desarrollar aplicaciones de VoD con el modelo OData de Media Services.</span><span class="sxs-lookup"><span data-stu-id="917da-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="917da-108">Haga clic en la imagen para verla a tamaño completo.</span><span class="sxs-lookup"><span data-stu-id="917da-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="917da-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="917da-109">Prerequisites</span></span>
<span data-ttu-id="917da-110">Los siguientes requisitos previos son necesarios para empezar a desarrollar con las API de REST de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="917da-111">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="917da-111">An Azure account.</span></span> <span data-ttu-id="917da-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="917da-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="917da-113">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="917da-113">A Media Services account.</span></span> <span data-ttu-id="917da-114">Para crear una cuenta de Media Services, consulte el tema [Creación de una cuenta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="917da-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="917da-115">Información sobre cómo desarrollar con las API de REST de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="917da-116">Para más información, consulte [Información general sobre la API de REST de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="917da-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="917da-117">Una aplicación de su elección que puede enviar solicitudes y respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="917da-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="917da-118">En este tutorial se usa [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="917da-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="917da-119">En este tutorial rápido se muestran las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="917da-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="917da-120">Inicio de punto de conexión de streaming (mediante Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="917da-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="917da-121">Conexión a la cuenta de Servicios multimedia con API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="917da-122">Creación de un nuevo recurso y carga de un archivo de vídeo con la API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="917da-123">Codificación del archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptable con API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="917da-124">Publicación del recurso y obtención de direcciones URL de streaming y de descarga progresiva con API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="917da-125">Reproduzca el contenido.</span><span class="sxs-lookup"><span data-stu-id="917da-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="917da-126">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="917da-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="917da-127">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="917da-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="917da-128">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="917da-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="917da-129">Para más información acerca de las entidades de AMS REST utilizadas en este tema, consulte [Referencia de la API de REST de Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="917da-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="917da-130">Consulte también [Conceptos de Azure Media Services](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="917da-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="917da-131">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="917da-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="917da-132">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="917da-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="917da-133">Inicio de los puntos de conexión de streaming con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="917da-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="917da-134">Cuando se trabaja con Azure Media Services, uno de los escenarios más comunes es entregar contenido de vídeo a los clientes mediante streaming con velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="917da-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="917da-135">Media Services proporciona empaquetado dinámico que permite entregar contenido codificado MP4 con velocidad de bits adaptable en formatos de streaming admitidos por Media Services (MPEG DASH, HLS, Smooth Streaming) justo a tiempo, sin tener que almacenar versiones previamente empaquetadas de cada uno de estos formatos.</span><span class="sxs-lookup"><span data-stu-id="917da-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="917da-136">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="917da-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="917da-137">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="917da-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="917da-138">Para iniciar el punto de conexión de streaming, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="917da-139">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="917da-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="917da-140">En la ventana Settings (Configuración), haga clic en Streaming endpoints (Puntos de conexión de streaming).</span><span class="sxs-lookup"><span data-stu-id="917da-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="917da-141">Haga clic en el punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="917da-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="917da-142">Aparecerá la ventana de detalles del punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="917da-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="917da-143">Haga clic en el icono de inicio.</span><span class="sxs-lookup"><span data-stu-id="917da-143">Click the Start icon.</span></span>
5. <span data-ttu-id="917da-144">Haga clic en el botón Save (Guardar) para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="917da-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="917da-145"><a id="connect"></a>Conexión a la cuenta de Servicios multimedia con API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="917da-146">Para obtener más información sobre cómo conectarse a la API de Azure Media Services, consulte [Acceso a la API de Azure Media Services con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="917da-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="917da-147">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="917da-148">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="917da-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="917da-149">Por ejemplo, si después de intentar conectarse, obtiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="917da-150">Debe registrar las llamadas posteriores de API en https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="917da-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="917da-151"><a id="upload"></a>Creación de un nuevo recurso y carga de un archivo de vídeo con la API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="917da-152">En Servicios multimedia, cargue los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="917da-153">La entidad **Asset** puede contener archivos de vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y subtítulos (y los metadatos sobre estos archivos).  Una vez cargados los archivos en el recurso, el contenido se almacena de forma segura en la nube para un posterior procesamiento y streaming.</span><span class="sxs-lookup"><span data-stu-id="917da-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="917da-154">Uno de los valores que se deben proporcionar al crear un recurso son las opciones de creación de activos.</span><span class="sxs-lookup"><span data-stu-id="917da-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="917da-155">La propiedad **Options** es un valor de enumeración que describe las opciones de cifrado con las que se puede crear un recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="917da-156">Un valor válido es uno de los valores de la lista siguiente, no una combinación de valores de esta lista:</span><span class="sxs-lookup"><span data-stu-id="917da-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="917da-157">**None** = **0**: no se utiliza cifrado.</span><span class="sxs-lookup"><span data-stu-id="917da-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="917da-158">Cuando se utiliza esta opción, el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="917da-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="917da-159">Si tiene previsto entregar un MP4 mediante una descarga progresiva, utilice esta opción.</span><span class="sxs-lookup"><span data-stu-id="917da-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="917da-160">**StorageEncrypted** = **1**: cifra el contenido no cifrado localmente mediante el cifrado AES de 256 bits y, a continuación, lo carga en Azure Storage, donde se almacena cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="917da-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="917da-161">Los recursos protegidos con el cifrado de almacenamiento se descifran automáticamente y se colocan en un sistema de archivos cifrados antes de la codificación y, opcionalmente, se vuelven a cifrar antes de volver a cargarlos como un nuevo recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="917da-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="917da-162">El caso de uso principal para el cifrado de almacenamiento es cuando desea proteger los archivos multimedia de entrada de alta calidad con un sólido cifrado en reposo en disco.</span><span class="sxs-lookup"><span data-stu-id="917da-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="917da-163">**CommonEncryptionProtected** = **2**: use esta opción si va a cargar contenido que ya se cifró y protegió con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).</span><span class="sxs-lookup"><span data-stu-id="917da-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="917da-164">**EnvelopeEncryptionProtected** = **4**: use esta opción si va a cargar HLS cifrado con AES.</span><span class="sxs-lookup"><span data-stu-id="917da-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="917da-165">Los archivos deben haberse codificado y cifrado con Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="917da-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="917da-166">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="917da-166">Create an asset</span></span>
<span data-ttu-id="917da-167">Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="917da-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="917da-168">En la API de REST, crear un recurso requiere el envío de una solicitud POST a Servicios multimedia y colocar la información sobre cualquier propiedad del recurso en el cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="917da-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="917da-169">En el ejemplo siguiente se muestra cómo crear un recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="917da-170">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="917da-171">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-171">**HTTP Response**</span></span>

<span data-ttu-id="917da-172">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-172">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="917da-173">Creación de AssetFile</span><span class="sxs-lookup"><span data-stu-id="917da-173">Create an AssetFile</span></span>
<span data-ttu-id="917da-174">La entidad [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa un archivo de audio o vídeo que se almacena en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="917da-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="917da-175">Un archivo de recursos siempre está asociado a un recurso y un recurso puede contener uno o varios archivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="917da-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="917da-176">La tarea de Servicios multimedia produce un error si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="917da-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="917da-177">Después de cargar el archivo multimedia digital en un contenedor de blobs, usará la solicitud HTTP **MERGE** para actualizar la entidad AssetFile con información sobre el archivo multimedia (tal como se muestra más adelante en este tema).</span><span class="sxs-lookup"><span data-stu-id="917da-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="917da-178">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="917da-179">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="917da-180">Creación de AccessPolicy con permiso de escritura</span><span class="sxs-lookup"><span data-stu-id="917da-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="917da-181">Antes de cargar los archivos en el almacenamiento de blobs, establezca los derechos de la directiva de acceso para escribir en un recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="917da-182">Para ello, envíe una solicitud HTTP al conjunto de entidades AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="917da-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="917da-183">Defina un valor DurationInMinutes tras la creación o recibirá un mensaje de error de servidor interno 500 como respuesta.</span><span class="sxs-lookup"><span data-stu-id="917da-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="917da-184">Para obtener más información sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="917da-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="917da-185">En el ejemplo siguiente se muestra cómo crear una entidad AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="917da-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="917da-186">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="917da-187">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-187">**HTTP Response**</span></span>

<span data-ttu-id="917da-188">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-188">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="917da-189">Obtención de la dirección URL de carga</span><span class="sxs-lookup"><span data-stu-id="917da-189">Get the Upload URL</span></span>

<span data-ttu-id="917da-190">Para recibir la dirección URL de carga real, cree un localizador de SAS.</span><span class="sxs-lookup"><span data-stu-id="917da-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="917da-191">Los localizadores definen la hora de inicio y el tipo de extremo de conexión para los clientes que desean tener acceso a archivos de un recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="917da-192">Puede crear varias entidades Locator para un par AccessPolicy y Asset determinado a fin de controlar las distintas solicitudes y necesidades del cliente.</span><span class="sxs-lookup"><span data-stu-id="917da-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="917da-193">Cada uno de estos localizadores usa el valor StartTime más el valor DurationInMinutes de AccessPolicy para determinar la cantidad de tiempo que se puede usar una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="917da-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="917da-194">Para obtener más información, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="917da-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="917da-195">Una dirección URL de SAS tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="917da-196">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="917da-196">Some considerations apply:</span></span>

* <span data-ttu-id="917da-197">No puede tener más de cinco localizadores únicos asociados a un recurso determinado a la vez.</span><span class="sxs-lookup"><span data-stu-id="917da-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="917da-198">Para obtener más información, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="917da-198">For more information, see Locator.</span></span>
* <span data-ttu-id="917da-199">Si necesita cargar los archivos inmediatamente, debe establecer el valor StartTime cinco minutos antes de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="917da-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="917da-200">Esto se debe a que puede haber un desplazamiento de reloj entre el equipo cliente y Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="917da-201">Además, el valor de StartTime debe tener el siguiente formato: YYYY-MM-DDTHH:mm:ssZ (por ejemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="917da-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="917da-202">Puede haber un retraso de 30 a 40 segundos desde el momento en que se crea un localizador hasta que este está disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="917da-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="917da-203">Este problema afecta a la dirección URL de SAS y a localizadores de origen.</span><span class="sxs-lookup"><span data-stu-id="917da-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="917da-204">Para más información sobre localizadores de SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="917da-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="917da-205">En el ejemplo siguiente se muestra cómo crear un localizador de dirección URL de SAS, tal como se define en la propiedad Type del cuerpo de solicitud ("1" para un localizador de SAS y "2" para un localizador de origen bajo demanda).</span><span class="sxs-lookup"><span data-stu-id="917da-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="917da-206">La propiedad **Path** devuelta contiene la dirección URL que debe usar para cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="917da-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="917da-207">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="917da-208">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-208">**HTTP Response**</span></span>

<span data-ttu-id="917da-209">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-209">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="917da-210">Carga de un archivo en un contenedor de almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="917da-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="917da-211">Una vez establecidas las propiedades AccessPolicy y Locator, el archivo real se carga en un contenedor de Azure Blob Storage mediante las API de REST de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="917da-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="917da-212">Debe cargar los archivos como blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="917da-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="917da-213">Azure Media Services no admite los blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="917da-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="917da-214">Debe agregar el nombre de archivo para el archivo que desea cargar en el valor **Path** del localizador recibido en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="917da-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="917da-215">Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="917da-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="917da-216">.</span><span class="sxs-lookup"><span data-stu-id="917da-216">.</span></span> <span data-ttu-id="917da-217">.</span><span class="sxs-lookup"><span data-stu-id="917da-217">.</span></span> <span data-ttu-id="917da-218">.</span><span class="sxs-lookup"><span data-stu-id="917da-218">.</span></span>
>
>

<span data-ttu-id="917da-219">Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="917da-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="917da-220">Actualización de AssetFile</span><span class="sxs-lookup"><span data-stu-id="917da-220">Update the AssetFile</span></span>
<span data-ttu-id="917da-221">Ahora que ha cargado el archivo, actualice la información de tamaño de FileAsset (y otro tipo de información).</span><span class="sxs-lookup"><span data-stu-id="917da-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="917da-222">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="917da-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="917da-223">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-223">**HTTP Response**</span></span>

<span data-ttu-id="917da-224">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="917da-225">Eliminación de Locator y AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="917da-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="917da-226">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="917da-227">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-227">**HTTP Response**</span></span>

<span data-ttu-id="917da-228">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="917da-229">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="917da-230">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-230">**HTTP Response**</span></span>

<span data-ttu-id="917da-231">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="917da-232"><a id="encode"></a>Codificación del archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa</span><span class="sxs-lookup"><span data-stu-id="917da-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="917da-233">Después de introducir los recursos en Servicios multimedia, los elementos multimedia se pueden codificar, transmultiplexar, agregar una marca de agua, entre otras opciones, antes de entregarse a los clientes.</span><span class="sxs-lookup"><span data-stu-id="917da-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="917da-234">Estas actividades se programan y se ejecutan en varias instancias de rol en segundo plano para garantizar la disponibilidad y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="917da-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="917da-235">Estas actividades se denominan trabajos y cada trabajo está compuesto de tareas atómicas que realizan el trabajo real en el archivo del recurso (para más información, consulte las descripciones de [trabajo](/rest/api/media/services/job) y [tarea](/rest/api/media/services/task)).</span><span class="sxs-lookup"><span data-stu-id="917da-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="917da-236">Como se ha indicado antes, cuando se trabaja con Servicios multimedia de Azure, uno de los escenarios más comunes es ofrecer streaming de velocidad de bits adaptable a los clientes.</span><span class="sxs-lookup"><span data-stu-id="917da-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="917da-237">Media Services puede empaquetar de manera dinámica un conjunto de archivos MP4 de velocidad de bits adaptable en uno de los siguientes formatos: HTTP Live Streaming (HLS), Smooth Streaming y MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="917da-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="917da-238">En la sección siguiente se muestra cómo crear un trabajo que contiene una tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="917da-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="917da-239">La tarea especifica la transcodificación del archivo intermedio en un conjunto de archivos MP4 de velocidad de bits adaptable con **Codificador multimedia estándar**.</span><span class="sxs-lookup"><span data-stu-id="917da-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="917da-240">La sección también muestra cómo supervisar el progreso del procesamiento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="917da-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="917da-241">Una vez finalizado el trabajo, podría crear los localizadores necesarios para acceder a los recursos.</span><span class="sxs-lookup"><span data-stu-id="917da-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="917da-242">Obtención de un procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="917da-242">Get a media processor</span></span>
<span data-ttu-id="917da-243">En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="917da-244">Para la tarea de codificación que se muestra en este tutorial, usaremos el Codificador multimedia estándar.</span><span class="sxs-lookup"><span data-stu-id="917da-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="917da-245">El código siguiente solicita el identificador del codificador.</span><span class="sxs-lookup"><span data-stu-id="917da-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="917da-246">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="917da-247">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="917da-248">Creación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="917da-248">Create a job</span></span>
<span data-ttu-id="917da-249">Cada trabajo puede tener una o más tareas según el tipo de procesamiento que desee llevar a cabo.</span><span class="sxs-lookup"><span data-stu-id="917da-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="917da-250">A través de la API de REST, puede crear trabajos y sus tareas relacionadas en una de las dos maneras siguientes: las tareas se pueden definir en línea a través de la propiedad de navegación Tasks en entidades Job o de procesamiento por lotes de OData.</span><span class="sxs-lookup"><span data-stu-id="917da-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="917da-251">El SDK de Media Services usa el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="917da-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="917da-252">Sin embargo, para que sea fácil entender los ejemplos de código de este tema, las tareas se definen en línea.</span><span class="sxs-lookup"><span data-stu-id="917da-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="917da-253">Para obtener información sobre el procesamiento por lotes, consulte [Procesamiento por lotes del protocolo Open Data (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="917da-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="917da-254">En el ejemplo siguiente se muestra cómo crear y publicar un trabajo con un conjunto de tareas para codificar un vídeo con una resolución y calidad específicas.</span><span class="sxs-lookup"><span data-stu-id="917da-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="917da-255">La siguiente sección de la documentación contiene la lista de todos los [valores preestablecidos de tareas](http://msdn.microsoft.com/library/mt269960) admitidos por el procesador de Codificador multimedia estándar.</span><span class="sxs-lookup"><span data-stu-id="917da-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="917da-256">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="917da-257">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-257">**HTTP Response**</span></span>

<span data-ttu-id="917da-258">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-258">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="917da-259">Hay algunas cuestiones importantes a tener en cuenta en cualquier solicitud de trabajo:</span><span class="sxs-lookup"><span data-stu-id="917da-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="917da-260">Las propiedades TaskBody deben usar archivos XML literales para definir el número de recursos de entrada o salida que se usarán en la tarea.</span><span class="sxs-lookup"><span data-stu-id="917da-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="917da-261">El tema Tarea incluye la definición de esquema XML para el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="917da-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="917da-262">En la definición de TaskBody, cada valor interno para <inputAsset> y <outputAsset> se debe establecer como JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="917da-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="917da-263">Una tarea puede tener varios recursos de salida.</span><span class="sxs-lookup"><span data-stu-id="917da-263">A task can have multiple output assets.</span></span> <span data-ttu-id="917da-264">Un elemento JobOutputAsset(x) solo se puede usar una vez como salida de una tarea en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="917da-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="917da-265">Puede especificar JobInputAsset o JobOutputAsset como un recurso de entrada de una tarea.</span><span class="sxs-lookup"><span data-stu-id="917da-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="917da-266">Las tareas no pueden formar un ciclo.</span><span class="sxs-lookup"><span data-stu-id="917da-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="917da-267">El parámetro de valor que se pasa a JobInputAsset o JobOutputAsset representa el valor de índice para un recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="917da-268">Los recursos reales se definen en las propiedades de navegación InputMediaAssets y OutputMediaAssets en la definición de la entidad Job.</span><span class="sxs-lookup"><span data-stu-id="917da-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="917da-269">Dado que Servicios multimedia se basa en OData v3, se hace referencia a los recursos individuales de las colecciones de propiedades de navegación InputMediaAssets y OutputMediaAssets a través de un par nombre-valor "__metadata: uri".</span><span class="sxs-lookup"><span data-stu-id="917da-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="917da-270">InputMediaAssets se asigna a uno o más recursos que ha creado en Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="917da-271">El sistema crea OutputMediaAssets.</span><span class="sxs-lookup"><span data-stu-id="917da-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="917da-272">Estos no hacen referencia a ningún recurso existente.</span><span class="sxs-lookup"><span data-stu-id="917da-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="917da-273">Se puede asignar un nombre a OutputMediaAssets con el atributo assetName.</span><span class="sxs-lookup"><span data-stu-id="917da-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="917da-274">Si este atributo no está presente, el nombre de OutputMediaAsset será el valor del texto interno del elemento <outputAsset> con un sufijo del valor Job Name o del valor Job Id (en el caso de que no se haya definido la propiedad Name).</span><span class="sxs-lookup"><span data-stu-id="917da-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="917da-275">Por ejemplo, si establece un valor para assetName como "Sample", se establecería la propiedad de OutputMediaAsset Name en "Sample".</span><span class="sxs-lookup"><span data-stu-id="917da-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="917da-276">Sin embargo, si no se ha definido un valor para assetName, pero se ha especificado el nombre del trabajo como "NewJob", OutputMediaAsset Name será "JobOutputAsset (value) _NewJob".</span><span class="sxs-lookup"><span data-stu-id="917da-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="917da-277">En el ejemplo siguiente se muestra cómo establecer el atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="917da-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="917da-278">Para habilitar el encadenamiento de tareas:</span><span class="sxs-lookup"><span data-stu-id="917da-278">To enable task chaining:</span></span>

  * <span data-ttu-id="917da-279">Un trabajo debe tener al menos dos tareas.</span><span class="sxs-lookup"><span data-stu-id="917da-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="917da-280">Debe haber al menos una tarea cuya entrada sea salida de otra tarea del trabajo.</span><span class="sxs-lookup"><span data-stu-id="917da-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="917da-281">Para obtener más información, consulte [Creación de un trabajo de codificación con la API de REST de Servicios multimedia](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="917da-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="917da-282">Supervisión del progreso del procesamiento</span><span class="sxs-lookup"><span data-stu-id="917da-282">Monitor Processing Progress</span></span>
<span data-ttu-id="917da-283">Puede recuperar el estado del trabajo mediante la propiedad State, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="917da-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="917da-284">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="917da-285">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-285">**HTTP Response**</span></span>

<span data-ttu-id="917da-286">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-286">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="917da-287">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="917da-287">Cancel a job</span></span>
<span data-ttu-id="917da-288">Servicios multimedia le permite cancelar trabajos en ejecución a través de la función CancelJob.</span><span class="sxs-lookup"><span data-stu-id="917da-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="917da-289">Esta llamada devolverá un código de error 400 si intenta cancelar un trabajo cuando su estado sea cancelado, cancelando, error o finalizado.</span><span class="sxs-lookup"><span data-stu-id="917da-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="917da-290">En el ejemplo siguiente se muestra cómo llamar a CancelJob.</span><span class="sxs-lookup"><span data-stu-id="917da-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="917da-291">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="917da-292">Si se realiza correctamente, se devuelve un código de respuesta 204 sin cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="917da-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="917da-293">Debe codificar con URL el identificador del trabajo (normalmente, nb:jid:UUID: somevalue) al pasarlo como parámetro a CancelJob.</span><span class="sxs-lookup"><span data-stu-id="917da-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="917da-294">Obtención del resultado de salida</span><span class="sxs-lookup"><span data-stu-id="917da-294">Get the output asset</span></span>
<span data-ttu-id="917da-295">En el código siguiente se muestra cómo solicitar el identificador del recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="917da-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="917da-296">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="917da-297">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="917da-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="917da-298"><a id="publish_get_urls"></a>Publicación del recurso y obtención de direcciones URL de streaming y de descarga progresiva con API de REST</span><span class="sxs-lookup"><span data-stu-id="917da-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="917da-299">Para transmitir o descargar un recurso, necesita "publicarlo" mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="917da-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="917da-300">Los localizadores proporcionan acceso a los archivos contenidos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="917da-301">Servicios multimedia admite dos tipos de localizadores: OnDemandOrigin locators, utilizados para transmitir contenido (por ejemplo, MPEG DASH, HLS o Smooth Streaming) y localizadores de firma de acceso (SAS), que se usan para descargar archivos multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="917da-302">Para más información sobre localizadores de SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="917da-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="917da-303">Una vez que se crean los localizadores, puede generar las direcciones URL que se utilizan para transmitir o descargar los archivos.</span><span class="sxs-lookup"><span data-stu-id="917da-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="917da-304">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="917da-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="917da-305">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="917da-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="917da-306">Una dirección URL de streaming de Smooth Streaming tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="917da-307">Una dirección URL de streaming de HLS tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="917da-308">Una dirección URL de streaming de MPEG DASH tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="917da-309">Una dirección URL de SAS utilizada para descargar archivos tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="917da-310">En estas secciones se muestra cómo realizar las siguientes tareas necesarias para "publicar" los recursos.</span><span class="sxs-lookup"><span data-stu-id="917da-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="917da-311">Creación de AccessPolicy con permiso de lectura</span><span class="sxs-lookup"><span data-stu-id="917da-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="917da-312">Creación de una URL de SAS para descargar contenido</span><span class="sxs-lookup"><span data-stu-id="917da-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="917da-313">Creación de una URL de origen para transmitir contenido</span><span class="sxs-lookup"><span data-stu-id="917da-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="917da-314">Creación de AccessPolicy con permiso de lectura</span><span class="sxs-lookup"><span data-stu-id="917da-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="917da-315">Antes de descargar o transmitir contenido multimedia, primero defina una AccessPolicy con permisos de lectura y cree la entidad Locator adecuada que especifique el tipo de mecanismo de entrega que desea habilitar para los clientes.</span><span class="sxs-lookup"><span data-stu-id="917da-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="917da-316">Para obtener más información sobre las propiedades disponibles, consulte [Propiedades de la entidad AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="917da-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="917da-317">En el ejemplo siguiente se muestra cómo especificar AccessPolicy para los permisos de lectura de un recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="917da-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="917da-318">Si se realiza correctamente, se devuelve un código de correcto 201 que describe la entidad AccessPolicy que ha creado.</span><span class="sxs-lookup"><span data-stu-id="917da-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="917da-319">A continuación, usará AccessPolicy Id junto con Asset Id del recurso que contiene el archivo que desea entregar (por ejemplo, un recurso de salida) para crear la entidad Locator.</span><span class="sxs-lookup"><span data-stu-id="917da-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="917da-320">Este flujo de trabajo básico es el mismo que la carga de un archivo al ingerir un recurso (como se explicó anteriormente en este tema).</span><span class="sxs-lookup"><span data-stu-id="917da-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="917da-321">Además, como en la carga de archivos, si usted (o sus clientes) necesitan tener acceso a los archivos inmediatamente, establezca el valor StartTime en cinco minutos antes de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="917da-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="917da-322">Esta acción es necesaria porque puede haber un desplazamiento de reloj entre el cliente y Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="917da-323">El valor de StartTime debe tener el siguiente formato: YYYY-MM-DDTHH:mm:ssZ (por ejemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="917da-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="917da-324">Creación de una URL de SAS para descargar contenido</span><span class="sxs-lookup"><span data-stu-id="917da-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="917da-325">El código siguiente muestra cómo obtener una dirección URL que se puede usar para descargar un archivo multimedia creado y cargado previamente.</span><span class="sxs-lookup"><span data-stu-id="917da-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="917da-326">AccessPolicy tiene permisos de lectura establecidos y a ruta de acceso de Locator hace referencia a una dirección URL de descarga de SAS.</span><span class="sxs-lookup"><span data-stu-id="917da-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="917da-327">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-327">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="917da-328">La propiedad **Path** devuelta contiene la dirección URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="917da-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="917da-329">Si descarga contenido cifrado del almacenamiento, debe descifrarlo manualmente antes de presentarlo o usar el procesador multimedia de descifrado de almacenamiento en una tarea de procesamiento para extraer archivos procesados sin cifrar en un recurso de salida y, a continuación, descargar desde ese recurso.</span><span class="sxs-lookup"><span data-stu-id="917da-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="917da-330">Para obtener más información sobre el procesamiento, consulte Creación de un trabajo de codificación con la API de REST de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="917da-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="917da-331">Además, los localizadores de dirección URL de SAS no se pueden actualizar una vez creados.</span><span class="sxs-lookup"><span data-stu-id="917da-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="917da-332">Por ejemplo, no se puede reutilizar el mismo localizador con un valor StartTime actualizado.</span><span class="sxs-lookup"><span data-stu-id="917da-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="917da-333">Esto se debe a la manera en que se crean las direcciones URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="917da-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="917da-334">Si desea obtener acceso a un recurso para descargarlo después de que expire un localizador, debe crear uno nuevo con un valor StartTime.</span><span class="sxs-lookup"><span data-stu-id="917da-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="917da-335">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="917da-335">Download files</span></span>
<span data-ttu-id="917da-336">Una vez establecidos AccessPolicy y Locator, puede descargar archivos mediante las API de REST de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="917da-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="917da-337">Debe agregar el nombre de archivo para el archivo que desea descargar en el valor **Path** del localizador recibido en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="917da-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="917da-338">Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="917da-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="917da-339">.</span><span class="sxs-lookup"><span data-stu-id="917da-339">.</span></span> <span data-ttu-id="917da-340">.</span><span class="sxs-lookup"><span data-stu-id="917da-340">.</span></span> <span data-ttu-id="917da-341">.</span><span class="sxs-lookup"><span data-stu-id="917da-341">.</span></span>
>
>

<span data-ttu-id="917da-342">Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="917da-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="917da-343">Como resultado del trabajo de codificación que realizó anteriormente (codificación en un conjunto de archivos MP4 adaptables), hay varios archivos MP4 que se pueden descargar progresivamente.</span><span class="sxs-lookup"><span data-stu-id="917da-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="917da-344">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="917da-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="917da-345">Creación de una URL de streaming para transmitir contenido</span><span class="sxs-lookup"><span data-stu-id="917da-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="917da-346">El siguiente código muestra cómo crear un localizador de direcciones URL de streaming:</span><span class="sxs-lookup"><span data-stu-id="917da-346">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="917da-347">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="917da-347">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="917da-348">Para transmitir una URL de origen de Smooth Streaming en un reproductor multimedia de streaming, debe anexar la propiedad Path con el nombre del archivo de manifiesto de Smooth Streaming seguido de "/manifest".</span><span class="sxs-lookup"><span data-stu-id="917da-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="917da-349">Para transmitir HLS, anexe(format=m3u8-aapl) después de "/manifest".</span><span class="sxs-lookup"><span data-stu-id="917da-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="917da-350">Para transmitir MPEG DASH, anexe(format=mpd-time-csf) después de "/manifest".</span><span class="sxs-lookup"><span data-stu-id="917da-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="917da-351"><a id="play"></a>Reproducción del contenido</span><span class="sxs-lookup"><span data-stu-id="917da-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="917da-352">Para transmitir vídeo, use [Reproductor de Servicios multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="917da-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="917da-353">Para probar la descarga progresiva, pegue una dirección URL en un explorador (por ejemplo, Internet Explorer, Chrome o Safari).</span><span class="sxs-lookup"><span data-stu-id="917da-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="917da-354">Siguientes pasos: Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="917da-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="917da-355">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="917da-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
