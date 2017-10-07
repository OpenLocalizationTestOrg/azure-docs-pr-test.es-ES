---
title: "aaaGet se inició con la entrega de contenido a petición con REST | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de Hola de implementar una aplicación de entrega de contenido de petición de servicios multimedia de Azure mediante API de REST."
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
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="be2f7-103">Introducción a la entrega de contenido a petición mediante REST</span><span class="sxs-lookup"><span data-stu-id="be2f7-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="be2f7-104">Este inicio rápido le guiará por los pasos de saludo de la implementación de una aplicación de entrega de contenido de vídeo bajo demanda (VoD) mediante las API de REST de servicios de multimedia de Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="be2f7-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="be2f7-105">tutorial de Hello presenta el flujo de trabajo de hello básico de servicios multimedia y objetos de programación más habituales de Hola y las tareas necesarias para el desarrollo de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="be2f7-106">Complete Hola tutorial Hola, se le pueda toostream o descargar progresivamente un archivo multimedia de ejemplo que cargar, codificado y descarga.</span><span class="sxs-lookup"><span data-stu-id="be2f7-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="be2f7-107">Hello siguiente imagen muestra algunos de los objetos de hello suelen usada al desarrollar aplicaciones de VoD en modelo de OData de servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="be2f7-108">Haga clic en tooview de imagen de hello tamaño completo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="be2f7-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="be2f7-109">Prerequisites</span></span>
<span data-ttu-id="be2f7-110">Hello siguientes requisitos previos son necesario toostart desarrollo con servicios multimedia con las API de REST.</span><span class="sxs-lookup"><span data-stu-id="be2f7-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="be2f7-111">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="be2f7-111">An Azure account.</span></span> <span data-ttu-id="be2f7-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be2f7-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="be2f7-113">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="be2f7-113">A Media Services account.</span></span> <span data-ttu-id="be2f7-114">toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="be2f7-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="be2f7-115">Descripción de cómo toodevelop con API de REST de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="be2f7-116">Para más información, consulte [Información general sobre la API de REST de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="be2f7-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="be2f7-117">Una aplicación de su elección que puede enviar solicitudes y respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="be2f7-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="be2f7-118">En este tutorial se usa [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="be2f7-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="be2f7-119">Hola siguiente las tareas se muestra en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="be2f7-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="be2f7-120">Iniciar el origen (con hello portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="be2f7-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="be2f7-121">Conectar la cuenta de servicios multimedia de toohello con API de REST.</span><span class="sxs-lookup"><span data-stu-id="be2f7-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="be2f7-122">Creación de un nuevo recurso y carga de un archivo de vídeo con la API de REST</span><span class="sxs-lookup"><span data-stu-id="be2f7-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="be2f7-123">Codificar el archivo de código fuente de hello en un conjunto de archivos MP4 de velocidad de bits adaptativa con API de REST.</span><span class="sxs-lookup"><span data-stu-id="be2f7-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="be2f7-124">Publicar los activos de Hola y get de transmisión por secuencias y direcciones URL de descarga progresiva con API de REST.</span><span class="sxs-lookup"><span data-stu-id="be2f7-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="be2f7-125">Reproduzca el contenido.</span><span class="sxs-lookup"><span data-stu-id="be2f7-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="be2f7-126">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="be2f7-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="be2f7-127">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="be2f7-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="be2f7-128">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="be2f7-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="be2f7-129">Para más información acerca de las entidades de AMS REST utilizadas en este tema, consulte [Referencia de la API de REST de Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="be2f7-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="be2f7-130">Consulte también [Conceptos de Azure Media Services](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="be2f7-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="be2f7-131">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="be2f7-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="be2f7-132">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="be2f7-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="be2f7-133">Iniciar la transmisión de los extremos que usan Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="be2f7-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="be2f7-134">Cuando se trabaja con uno de los escenarios más comunes de hello es entregar vídeo a través de la velocidad de bits de transmisión por secuencias adaptativa de servicios de multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="be2f7-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="be2f7-135">Servicios multimedia proporciona empaquetado dinámico, lo que permite toodeliver la velocidad de bits adaptativa MP4 codificados contenido de transmisión por secuencias formatos admitidos por servicios multimedia (MPEG DASH, HLS, Smooth Streaming) just-in-time, sin necesidad de toostore preempaquetado versiones de cada uno de estos formatos de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="be2f7-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="be2f7-136">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="be2f7-137">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="be2f7-138">toostart Hola extremo de streaming, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="be2f7-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="be2f7-139">Inicie sesión en hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="be2f7-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="be2f7-140">En la ventana de configuración de hello, haga clic en los puntos de conexión de la transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="be2f7-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="be2f7-141">Haga clic en predeterminada Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="be2f7-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="be2f7-142">Aparecerá la ventana de detalles predeterminada del extremo de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="be2f7-143">Haga clic en el icono de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="be2f7-144">Haga clic en botón toosave de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="be2f7-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="be2f7-145"><a id="connect"></a>Conectar la cuenta de servicios multimedia de toohello con API de REST</span><span class="sxs-lookup"><span data-stu-id="be2f7-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="be2f7-146">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="be2f7-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="be2f7-147">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="be2f7-148">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="be2f7-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="be2f7-149">Por ejemplo, si después de intentar tooconnect, obtuvo siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="be2f7-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="be2f7-150">Debe publicar los siguientes API llamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="be2f7-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="be2f7-151"><a id="upload"></a>Creación de un nuevo recurso y carga de un archivo de vídeo con la API de REST</span><span class="sxs-lookup"><span data-stu-id="be2f7-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="be2f7-152">En Servicios multimedia, cargue los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="be2f7-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="be2f7-153">Hola **Asset** entidad puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.)  Una vez Hola archivos se cargan en el recurso de hello, el contenido está almacenado con seguridad en nube de Hola para su posterior procesamiento y transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="be2f7-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="be2f7-154">Uno de los valores de hello tiene tooprovide al crear un activo es opciones de creación de activos.</span><span class="sxs-lookup"><span data-stu-id="be2f7-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="be2f7-155">Hola **opciones** propiedad es un valor de enumeración que describe las opciones de cifrado de Hola que se puede crear un activo con.</span><span class="sxs-lookup"><span data-stu-id="be2f7-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="be2f7-156">Un valor válido es uno de los valores de hello en lista de hello siguiente, no una combinación de valores de esta lista:</span><span class="sxs-lookup"><span data-stu-id="be2f7-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="be2f7-157">**None** = **0**: no se utiliza cifrado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="be2f7-158">Cuando se utiliza esta opción, el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="be2f7-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="be2f7-159">Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use esta opción.</span><span class="sxs-lookup"><span data-stu-id="be2f7-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="be2f7-160">**StorageEncrypted** = **1** : cifra el contenido no localmente mediante cifrado AES de 256 bits y, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="be2f7-161">Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="be2f7-162">caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure los archivos multimedia de entrada de alta calidad con cifrado de alta seguridad en reposo en el disco.</span><span class="sxs-lookup"><span data-stu-id="be2f7-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="be2f7-163">**CommonEncryptionProtected** = **2**: use esta opción si va a cargar contenido que ya se cifró y protegió con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).</span><span class="sxs-lookup"><span data-stu-id="be2f7-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="be2f7-164">**EnvelopeEncryptionProtected** = **4**: use esta opción si va a cargar HLS cifrado con AES.</span><span class="sxs-lookup"><span data-stu-id="be2f7-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="be2f7-165">deben tener archivos Hola se ha codificado y cifrado con Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="be2f7-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="be2f7-166">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="be2f7-166">Create an asset</span></span>
<span data-ttu-id="be2f7-167">Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="be2f7-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="be2f7-168">Hola API de REST, crear un activo requiere el envío de POST solicitar servicios de tooMedia y colocar cualquier información de propiedad sobre el activo en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="be2f7-169">Hola siguiente ejemplo se muestra cómo toocreate un activo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="be2f7-170">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-170">**HTTP Request**</span></span>

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


<span data-ttu-id="be2f7-171">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-171">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-172">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="be2f7-172">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="be2f7-173">Creación de AssetFile</span><span class="sxs-lookup"><span data-stu-id="be2f7-173">Create an AssetFile</span></span>
<span data-ttu-id="be2f7-174">Hola [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidad representa un archivo de vídeo o audio que se almacena en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="be2f7-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="be2f7-175">Un archivo de recursos siempre está asociado a un recurso y un recurso puede contener uno o varios archivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="be2f7-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="be2f7-176">se produce un error en la tarea de codificador de servicios multimedia de Hello si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="be2f7-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="be2f7-177">Después de cargar el archivo multimedia digital en un contenedor de blobs, use hello **mezcla** tooupdate hello AssetFile HTTP solicitud con información sobre el archivo multimedia (como se muestra más adelante en el tema de hello).</span><span class="sxs-lookup"><span data-stu-id="be2f7-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="be2f7-178">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-178">**HTTP Request**</span></span>

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


<span data-ttu-id="be2f7-179">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="be2f7-180">Creación de hello AccessPolicy con permiso de escritura</span><span class="sxs-lookup"><span data-stu-id="be2f7-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="be2f7-181">Antes de cargar los archivos en el almacenamiento de blobs, configurar el acceso de hello derechos de directiva para escribir tooan activo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="be2f7-182">establece toodo que registrar un toohello de solicitud HTTP entidades AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="be2f7-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="be2f7-183">Defina un valor DurationInMinutes tras la creación o recibirá un mensaje de error de servidor interno 500 como respuesta.</span><span class="sxs-lookup"><span data-stu-id="be2f7-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="be2f7-184">Para obtener más información sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="be2f7-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="be2f7-185">Hola siguiente ejemplo se muestra cómo toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="be2f7-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="be2f7-186">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-186">**HTTP Request**</span></span>

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

<span data-ttu-id="be2f7-187">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-187">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-188">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="be2f7-188">If successful, hello following response is returned:</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="be2f7-189">Obtener Hola cargar dirección URL</span><span class="sxs-lookup"><span data-stu-id="be2f7-189">Get hello Upload URL</span></span>

<span data-ttu-id="be2f7-190">tooreceive Hola dirección URL de carga real, cree un localizador SAS.</span><span class="sxs-lookup"><span data-stu-id="be2f7-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="be2f7-191">Los localizadores definen la hora de inicio de Hola y el tipo de extremo de conexión para los clientes que desea que los archivos de tooaccess en un recurso.</span><span class="sxs-lookup"><span data-stu-id="be2f7-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="be2f7-192">Puede crear varias entidades Locator para un determinada AccessPolicy Asset par toohandle diferentes cliente y las solicitudes y necesidades.</span><span class="sxs-lookup"><span data-stu-id="be2f7-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="be2f7-193">Cada uno de los localizadores usa valores de StartTime de Hola y DurationInMinutes de Hola de longitud de hello AccessPolicy toodetermine Hola de tiempo que se puede utilizar una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="be2f7-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="be2f7-194">Para obtener más información, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="be2f7-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="be2f7-195">Una dirección URL SAS tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="be2f7-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="be2f7-196">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="be2f7-196">Some considerations apply:</span></span>

* <span data-ttu-id="be2f7-197">No puede tener más de cinco localizadores únicos asociados a un recurso determinado a la vez.</span><span class="sxs-lookup"><span data-stu-id="be2f7-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="be2f7-198">Para obtener más información, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="be2f7-198">For more information, see Locator.</span></span>
* <span data-ttu-id="be2f7-199">Si necesita los archivos de tooupload de forma inmediata, debe establecer los minutos de toofive de valor de StartTime antes Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="be2f7-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="be2f7-200">Esto se debe a que puede haber un desplazamiento de reloj entre el equipo cliente y Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="be2f7-201">Además, debe ser el valor de StartTime Hola siguiendo el formato de fecha y hora: aaaa-MM-ddTHH (por ejemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="be2f7-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="be2f7-202">Puede haber un 30 a 40 segundos retrasar después de crear un localizador toowhen está disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="be2f7-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="be2f7-203">Este problema aplica tooboth URL de SAS y localizadores de origen.</span><span class="sxs-lookup"><span data-stu-id="be2f7-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="be2f7-204">Para más información sobre localizadores de SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="be2f7-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="be2f7-205">Hola de ejemplo siguiente muestra cómo toocreate un localizador de URL de SAS, tal como se define por Hola propiedad de tipo en el cuerpo de la solicitud de hello ("1" para un localizador SAS) y "2" de un localizador de origen a petición.</span><span class="sxs-lookup"><span data-stu-id="be2f7-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="be2f7-206">Hola **ruta de acceso** propiedad devuelta contiene la dirección URL de Hola que se debe usar tooupload en el archivo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="be2f7-207">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-207">**HTTP Request**</span></span>

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


<span data-ttu-id="be2f7-208">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-208">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-209">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="be2f7-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="be2f7-210">Carga de un archivo en un contenedor de almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="be2f7-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="be2f7-211">Una vez que tenga hello AccessPolicy y conjunto de localizador, archivo real de hello es el contenedor de almacenamiento de blobs de Azure de tooan cargados con hello las API de REST de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="be2f7-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="be2f7-212">Debe cargar archivos de hello como blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="be2f7-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="be2f7-213">Azure Media Services no admite los blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="be2f7-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="be2f7-214">Debe agregar el nombre del archivo de hello para el archivo hello desea tooupload toohello localizador **ruta de acceso** valor recibido en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="be2f7-215">Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="be2f7-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="be2f7-216">.</span><span class="sxs-lookup"><span data-stu-id="be2f7-216">.</span></span> <span data-ttu-id="be2f7-217">.</span><span class="sxs-lookup"><span data-stu-id="be2f7-217">.</span></span> <span data-ttu-id="be2f7-218">.</span><span class="sxs-lookup"><span data-stu-id="be2f7-218">.</span></span>
>
>

<span data-ttu-id="be2f7-219">Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="be2f7-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="be2f7-220">Actualizar hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="be2f7-220">Update hello AssetFile</span></span>
<span data-ttu-id="be2f7-221">Ahora que ha cargado el archivo, para actualizar información de hello FileAsset tamaño (y otros).</span><span class="sxs-lookup"><span data-stu-id="be2f7-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="be2f7-222">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="be2f7-222">For example:</span></span>

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


<span data-ttu-id="be2f7-223">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-223">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-224">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="be2f7-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="be2f7-225">Eliminar Hola localizador y AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="be2f7-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="be2f7-226">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="be2f7-227">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-227">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-228">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="be2f7-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="be2f7-229">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="be2f7-230">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-230">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-231">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="be2f7-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="be2f7-232"><a id="encode"></a>Codificar el archivo de código fuente de hello en un conjunto de archivos MP4 de velocidad de bits adaptativa</span><span class="sxs-lookup"><span data-stu-id="be2f7-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="be2f7-233">Después de introducir que activos en los servicios multimedia, multimedia pueden codificarse, transmultiplexar, marca de agua y así sucesivamente, antes de que se envía tooclients.</span><span class="sxs-lookup"><span data-stu-id="be2f7-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="be2f7-234">Estas actividades se programen y se ejecutarán varias fondo rol instancias tooensure alto rendimiento y disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="be2f7-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="be2f7-235">Estas actividades se denominan trabajos y cada trabajo está compuesto de tareas atómicas que Hola trabajo real en el archivo de recursos de hello (para obtener más información, consulte [trabajo](/rest/api/media/services/job), [tarea](/rest/api/media/services/task) descripciones).</span><span class="sxs-lookup"><span data-stu-id="be2f7-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="be2f7-236">Tal y como se mencionó anteriormente, al trabajar con servicios de multimedia de Azure uno de los escenarios más comunes de hello está proporcionando los clientes tooyour de transmisión por secuencias de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="be2f7-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="be2f7-237">Servicios multimedia dinámicamente puede empaquetar un conjunto de archivos MP4 de velocidad de bits adaptativa en uno de hello siguientes formatos: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="be2f7-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="be2f7-238">Hola siguiente sección muestra cómo toocreate un trabajo que contiene una codificación de tareas.</span><span class="sxs-lookup"><span data-stu-id="be2f7-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="be2f7-239">Hello tarea Especifica archivo mezzanine de tootranscode hello en un conjunto de velocidad de bits adaptativa MP4s utilizando **Media Encoder estándar**.</span><span class="sxs-lookup"><span data-stu-id="be2f7-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="be2f7-240">sección de Hello también muestra cómo toomonitor Hola progreso de procesamiento del trabajo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="be2f7-241">Cuando se complete el trabajo de hello, sería capaz de toocreate localizadores que son necesarios tooget acceso tooyour activos.</span><span class="sxs-lookup"><span data-stu-id="be2f7-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="be2f7-242">Obtención de un procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="be2f7-242">Get a media processor</span></span>
<span data-ttu-id="be2f7-243">En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="be2f7-244">Para hello codificación de tarea que se muestra en este tutorial, vamos hello toouse Media Encoder estándar.</span><span class="sxs-lookup"><span data-stu-id="be2f7-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="be2f7-245">Hola Id. del siguiente código solicitudes Hola del codificador.</span><span class="sxs-lookup"><span data-stu-id="be2f7-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="be2f7-246">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="be2f7-247">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="be2f7-248">Creación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="be2f7-248">Create a job</span></span>
<span data-ttu-id="be2f7-249">Cada trabajo puede tener uno o más tareas según el tipo de saludo de procesamiento que desea tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="be2f7-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="be2f7-250">A través de la API de REST de hello, puede crear trabajos y sus tareas relacionadas en una de dos maneras: tareas pueden definir en línea a través de la propiedad de navegación de las tareas de hello en entidades de trabajos o a través de procesamiento por lotes de OData.</span><span class="sxs-lookup"><span data-stu-id="be2f7-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="be2f7-251">Hola SDK de servicios multimedia usa el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="be2f7-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="be2f7-252">Sin embargo, para mejorar la legibilidad Hola Hola ejemplos de código de este tema, las tareas son definida insertada.</span><span class="sxs-lookup"><span data-stu-id="be2f7-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="be2f7-253">Para obtener información sobre el procesamiento por lotes, consulte [Procesamiento por lotes del protocolo Open Data (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="be2f7-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="be2f7-254">Hola de ejemplo siguiente muestra cómo toocreate y post un trabajo con una tarea establece tooencode un vídeo en una resolución y calidad específicas.</span><span class="sxs-lookup"><span data-stu-id="be2f7-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="be2f7-255">Hola pasos de la sección de documentación contiene la lista de hello del programa Hola a todos los [valores preestablecidos de tareas](http://msdn.microsoft.com/library/mt269960) compatible con procesador multimedia codificador estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="be2f7-256">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-256">**HTTP Request**</span></span>

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

<span data-ttu-id="be2f7-257">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-257">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-258">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="be2f7-258">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="be2f7-259">Hay unos toonote cosas importantes en cualquier solicitud de trabajo:</span><span class="sxs-lookup"><span data-stu-id="be2f7-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="be2f7-260">Propiedades TaskBody deben usar el número de hello literal de toodefine XML de entrada o recursos de salida que usan Hola tarea.</span><span class="sxs-lookup"><span data-stu-id="be2f7-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="be2f7-261">tema de la tarea Hello contiene Hola definición de esquemas XML para hello XML.</span><span class="sxs-lookup"><span data-stu-id="be2f7-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="be2f7-262">Hola definición TaskBody, cada interna valor <inputAsset> y <outputAsset> debe establecerse como JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="be2f7-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="be2f7-263">Una tarea puede tener varios recursos de salida.</span><span class="sxs-lookup"><span data-stu-id="be2f7-263">A task can have multiple output assets.</span></span> <span data-ttu-id="be2f7-264">Un elemento JobOutputAsset(x) solo se puede usar una vez como salida de una tarea en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="be2f7-265">Puede especificar JobInputAsset o JobOutputAsset como un recurso de entrada de una tarea.</span><span class="sxs-lookup"><span data-stu-id="be2f7-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="be2f7-266">Las tareas no pueden formar un ciclo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="be2f7-267">valor del parámetro Hello que pasar tooJobInputAsset o JobOutputAsset representa el valor de índice de Hola para un activo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="be2f7-268">Hello recursos reales se definen en las propiedades de navegación de hello InputMediaAssets y OutputMediaAssets en hello definición de la entidad de trabajo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="be2f7-269">Dado que los servicios multimedia se fundamentan en OData v3, Hola activos individuales en InputMediaAssets y OutputMediaAssets colecciones de propiedades de navegación se hace referencia a través de un "__metadata: uri" par nombre / valor.</span><span class="sxs-lookup"><span data-stu-id="be2f7-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="be2f7-270">InputMediaAssets asigna tooone o más recursos que ha creado en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="be2f7-271">Sistema de hello crea los OutputMediaAssets.</span><span class="sxs-lookup"><span data-stu-id="be2f7-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="be2f7-272">Estos no hacen referencia a ningún recurso existente.</span><span class="sxs-lookup"><span data-stu-id="be2f7-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="be2f7-273">Los OutputMediaAssets se pueden nombrar con el atributo assetName de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="be2f7-274">Si este atributo no está presente, el nombre de Hola de hello OutputMediaAsset es cualquier valor de texto interno de Hola de hello <outputAsset> elemento es con un sufijo de valor de nombre del trabajo de Hola o valor de Id. de trabajo de hello (en caso de hello donde no se ha definido la propiedad de nombre de hello).</span><span class="sxs-lookup"><span data-stu-id="be2f7-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="be2f7-275">Por ejemplo, si establece un valor para assetName demasiado "Sample" y, a continuación, Hola nombre OutputMediaAsset se establecería la propiedad demasiado "Sample".</span><span class="sxs-lookup"><span data-stu-id="be2f7-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="be2f7-276">Sin embargo, si no se ha definido un valor para assetName, pero ha especificado el nombre del trabajo Hola demasiado como "NewJob" y, a continuación, Hola nombre OutputMediaAsset sería "JobOutputAsset (valor) _NewJob".</span><span class="sxs-lookup"><span data-stu-id="be2f7-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="be2f7-277">Hola de ejemplo siguiente muestra cómo tooset Hola atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="be2f7-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="be2f7-278">tooenable encadenamiento de tareas:</span><span class="sxs-lookup"><span data-stu-id="be2f7-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="be2f7-279">Un trabajo debe tener al menos dos tareas.</span><span class="sxs-lookup"><span data-stu-id="be2f7-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="be2f7-280">Debe haber al menos una tarea cuya entrada sea salida de otra tarea en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="be2f7-281">Para obtener más información, vea [crear un trabajo de codificación con API de REST de servicios multimedia de hello](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="be2f7-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="be2f7-282">Supervisión del progreso del procesamiento</span><span class="sxs-lookup"><span data-stu-id="be2f7-282">Monitor Processing Progress</span></span>
<span data-ttu-id="be2f7-283">Puede recuperar el estado del trabajo de hello mediante el uso de la propiedad de estado de hello, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="be2f7-284">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="be2f7-285">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-285">**HTTP Response**</span></span>

<span data-ttu-id="be2f7-286">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="be2f7-286">If successful, hello following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="be2f7-287">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="be2f7-287">Cancel a job</span></span>
<span data-ttu-id="be2f7-288">Servicios multimedia permite toocancel trabajos en ejecución a través de la función CancelJob Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="be2f7-289">Esta llamada devuelve un código de 400 error si intenta toocancel un trabajo cuando su estado sea cancelado, cancelando, error o finalizado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="be2f7-290">Hola siguiente ejemplo se muestra cómo toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="be2f7-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="be2f7-291">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="be2f7-292">Si se realiza correctamente, se devuelve un código de respuesta 204 sin cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="be2f7-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="be2f7-293">Debe codificar con URL Id. de trabajo de hello (normalmente jid: somevalue) al pasarla como un parámetro tooCancelJob.</span><span class="sxs-lookup"><span data-stu-id="be2f7-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="be2f7-294">Obtener el recurso de salida de hello</span><span class="sxs-lookup"><span data-stu-id="be2f7-294">Get hello output asset</span></span>
<span data-ttu-id="be2f7-295">Hello código siguiente muestra cómo toorequest Hola salida ID de activo.</span><span class="sxs-lookup"><span data-stu-id="be2f7-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="be2f7-296">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="be2f7-297">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="be2f7-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="be2f7-298"><a id="publish_get_urls"></a>Publicar activos de Hola y get de transmisión por secuencias y las direcciones URL de descarga progresiva con API de REST</span><span class="sxs-lookup"><span data-stu-id="be2f7-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="be2f7-299">toostream o descarga un recurso, primero necesita demasiado "publicar", mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="be2f7-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="be2f7-300">Los localizadores proporcionan toofiles de acceso que contiene el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="be2f7-301">Servicios multimedia admite dos tipos de localizadores: OnDemandOrigin localizadores, toostream usa medios (por ejemplo, MPEG DASH, HLS o Smooth Streaming) y localizadores de Access Signature (SAS), los archivos de medios de toodownload utilizan.</span><span class="sxs-lookup"><span data-stu-id="be2f7-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="be2f7-302">Para más información sobre localizadores de SAS, consulte [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="be2f7-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="be2f7-303">Una vez que cree los localizadores de hello, puede crear direcciones URL de hello toostream usado o descargar los archivos.</span><span class="sxs-lookup"><span data-stu-id="be2f7-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="be2f7-304">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="be2f7-305">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="be2f7-306">Una dirección URL de streaming para Smooth Streaming tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="be2f7-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="be2f7-307">Una dirección URL de streaming para HLS tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="be2f7-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="be2f7-308">Una dirección URL de streaming de MPEG DASH tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="be2f7-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="be2f7-309">Archivos de toodownload de una dirección URL de SAS utilizada tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="be2f7-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="be2f7-310">Esta sección muestra cómo tooperform Hola siguientes tareas necesarias demasiado "publicar" sus activos.</span><span class="sxs-lookup"><span data-stu-id="be2f7-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="be2f7-311">Creación de hello AccessPolicy con permiso de lectura</span><span class="sxs-lookup"><span data-stu-id="be2f7-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="be2f7-312">Creación de una URL de SAS para descargar contenido</span><span class="sxs-lookup"><span data-stu-id="be2f7-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="be2f7-313">Creación de una URL de origen para transmitir contenido</span><span class="sxs-lookup"><span data-stu-id="be2f7-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="be2f7-314">Creación de hello AccessPolicy con permiso de lectura</span><span class="sxs-lookup"><span data-stu-id="be2f7-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="be2f7-315">Antes de descargar o cualquier contenido multimedia de transmisión por secuencias, primero se definen una AccessPolicy con permisos de lectura y crear entidad Locator adecuada Hola que especifica el tipo de saludo del mecanismo de entrega que desee tooenable para los clientes.</span><span class="sxs-lookup"><span data-stu-id="be2f7-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="be2f7-316">Para obtener más información sobre las propiedades de hello disponibles, consulte [propiedades de la entidad AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="be2f7-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="be2f7-317">Hola de ejemplo siguiente muestra cómo toospecify Hola AccessPolicy para permisos de lectura de un recurso.</span><span class="sxs-lookup"><span data-stu-id="be2f7-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="be2f7-318">Si se realiza correctamente, se devuelve un código 201 que describe la entidad AccessPolicy de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="be2f7-319">A continuación, usar Hola identificador de AccessPolicy junto con hello identificador de recurso del recurso de Hola que contiene el archivo hello desea toodeliver (por ejemplo, un recurso de salida) toocreate Hola localizador entidad.</span><span class="sxs-lookup"><span data-stu-id="be2f7-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="be2f7-320">Este flujo de trabajo básico es Hola igual que cargar un archivo cuando ingesta de un recurso (tal y como se explicó anteriormente en este tema).</span><span class="sxs-lookup"><span data-stu-id="be2f7-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="be2f7-321">Además, como la carga de archivos, si usted (o los clientes) necesitan tooaccess los archivos inmediatamente, Establece los minutos de toofive de valor de StartTime antes Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="be2f7-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="be2f7-322">Esta acción es necesaria porque puede haber un reloj desfase entre el cliente de Hola y servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="be2f7-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="be2f7-323">Hola valor de StartTime debe estar en hello siguiendo el formato de fecha y hora: aaaa-MM-ddTHH (por ejemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="be2f7-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="be2f7-324">Creación de una URL de SAS para descargar contenido</span><span class="sxs-lookup"><span data-stu-id="be2f7-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="be2f7-325">Hola siguiente código muestra cómo la tooget una dirección URL que puede ser toodownload usa un archivo multimedia creado y cargado previamente.</span><span class="sxs-lookup"><span data-stu-id="be2f7-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="be2f7-326">Hola AccessPolicy tiene el conjunto de permisos de lectura y ruta del localizador Hola hace referencia la dirección URL de descarga SAS tooa.</span><span class="sxs-lookup"><span data-stu-id="be2f7-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

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

<span data-ttu-id="be2f7-327">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="be2f7-327">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="be2f7-328">Hola devuelve **ruta de acceso** propiedad contiene Hola URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="be2f7-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="be2f7-329">Si descarga contenido cifrado del almacenamiento, debe hacer manualmente descifrar antes de procesarlo o usar hello MediaProcessor de descifrado del almacenamiento en un toooutput de la tarea de procesamiento procesan archivos en hello desactive tooan OutputAsset y, a continuación, descargarlos del Asset.</span><span class="sxs-lookup"><span data-stu-id="be2f7-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="be2f7-330">Para obtener más información sobre el procesamiento, vea Crear un trabajo de codificación con API de REST de servicios multimedia de hello.</span><span class="sxs-lookup"><span data-stu-id="be2f7-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="be2f7-331">Además, los localizadores de dirección URL de SAS no se pueden actualizar una vez creados.</span><span class="sxs-lookup"><span data-stu-id="be2f7-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="be2f7-332">Por ejemplo, no puede reutilizar Hola mismo localizador con un valor StartTime actualizado.</span><span class="sxs-lookup"><span data-stu-id="be2f7-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="be2f7-333">Esto es debido a la manera de Hola que se crean direcciones URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="be2f7-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="be2f7-334">Si desea tooaccess un activo para su descarga después de que expire un localizador, debe crear uno nuevo con un valor de StartTime.</span><span class="sxs-lookup"><span data-stu-id="be2f7-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="be2f7-335">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="be2f7-335">Download files</span></span>
<span data-ttu-id="be2f7-336">Una vez que tenga hello AccessPolicy y conjunto de localizador, puede descargar archivos mediante hello las API de REST de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="be2f7-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="be2f7-337">Debe agregar el nombre del archivo de hello para el archivo hello desea toodownload toohello localizador **ruta de acceso** valor recibido en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="be2f7-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="be2f7-338">Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="be2f7-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="be2f7-339">.</span><span class="sxs-lookup"><span data-stu-id="be2f7-339">.</span></span> <span data-ttu-id="be2f7-340">.</span><span class="sxs-lookup"><span data-stu-id="be2f7-340">.</span></span> <span data-ttu-id="be2f7-341">.</span><span class="sxs-lookup"><span data-stu-id="be2f7-341">.</span></span>
>
>

<span data-ttu-id="be2f7-342">Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="be2f7-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="be2f7-343">Como resultado de hello codificación trabajo que realizó anteriormente (codificación en conjunto MP4 adaptable), tienen varios archivos MP4 que se pueden descargar progresivamente.</span><span class="sxs-lookup"><span data-stu-id="be2f7-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="be2f7-344">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="be2f7-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="be2f7-345">Creación de una URL de streaming para transmitir contenido</span><span class="sxs-lookup"><span data-stu-id="be2f7-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="be2f7-346">Hola el siguiente código muestra cómo toocreate un localizador de URL de streaming:</span><span class="sxs-lookup"><span data-stu-id="be2f7-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

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

<span data-ttu-id="be2f7-347">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="be2f7-347">If successful, hello following response is returned:</span></span>

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

<span data-ttu-id="be2f7-348">toostream una dirección URL de origen de transmisión por secuencias suave en un reproductor multimedia de transmisión por secuencias, debe agregar la propiedad de ruta de acceso de hello con el nombre de Hola de hello Smooth Streaming manifiestos de archivo, seguido de "/ manifiesto".</span><span class="sxs-lookup"><span data-stu-id="be2f7-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="be2f7-349">toostream HLS, anexar (formato = m3u8-aapl) después de hello "/ manifiesto".</span><span class="sxs-lookup"><span data-stu-id="be2f7-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="be2f7-350">toostream MPEG DASH, anexar (formato = mpd: tiempo-csf) después de hello "/ manifiesto".</span><span class="sxs-lookup"><span data-stu-id="be2f7-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="be2f7-351"><a id="play"></a>Reproducción del contenido</span><span class="sxs-lookup"><span data-stu-id="be2f7-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="be2f7-352">toostream vídeo, usas [Reproductor de servicios multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="be2f7-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="be2f7-353">tootest progresiva descargar, pegue una dirección URL en un explorador (por ejemplo, Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="be2f7-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="be2f7-354">Siguientes pasos: Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="be2f7-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="be2f7-355">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="be2f7-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
