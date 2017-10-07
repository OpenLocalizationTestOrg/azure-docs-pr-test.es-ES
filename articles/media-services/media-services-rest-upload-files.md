---
title: archivos de aaaUpload en una cuenta de servicios multimedia con REST | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooget medios de contenido en los servicios multimedia mediante la creación y carga de activos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="f866c-103">Carga de archivos en una cuenta de Servicios multimedia mediante API de REST</span><span class="sxs-lookup"><span data-stu-id="f866c-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f866c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f866c-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="f866c-105">REST</span><span class="sxs-lookup"><span data-stu-id="f866c-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="f866c-106">Portal</span><span class="sxs-lookup"><span data-stu-id="f866c-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="f866c-107">En Servicios multimedia, cargue los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="f866c-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="f866c-108">Hola [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entidad puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.)  Una vez Hola archivos se cargan en el recurso de hello, el contenido está almacenado con seguridad en nube de Hola para su posterior procesamiento y transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="f866c-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="f866c-109">Hola siguientes consideraciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="f866c-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="f866c-110">Servicios multimedia usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="f866c-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="f866c-111">Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="f866c-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="f866c-112">Además, solo puede haber uno '.' para la extensión de nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="f866c-113">longitud de Hello del nombre de hello no debería ser superior a 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f866c-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="f866c-114">Hay un tamaño de archivo máximo de toohello límite admitido para el procesamiento de los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="f866c-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="f866c-115">Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="f866c-116">flujo de trabajo básico de Hola para cargar los activos se divide en hello las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f866c-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="f866c-117">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="f866c-117">Create an Asset</span></span>
* <span data-ttu-id="f866c-118">Cifrado de un recurso (opcional)</span><span class="sxs-lookup"><span data-stu-id="f866c-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="f866c-119">Cargar un almacenamiento de tooblob de archivo</span><span class="sxs-lookup"><span data-stu-id="f866c-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="f866c-120">AMS también permite a activos tooupload de forma masiva.</span><span class="sxs-lookup"><span data-stu-id="f866c-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="f866c-121">Para obtener más información, consulte [esta](media-services-rest-upload-files.md#upload_in_bulk) sección.</span><span class="sxs-lookup"><span data-stu-id="f866c-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="f866c-122">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="f866c-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f866c-123">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f866c-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="f866c-124">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="f866c-124">Connect tooMedia Services</span></span>

<span data-ttu-id="f866c-125">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f866c-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="f866c-126">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="f866c-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f866c-127">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="f866c-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="f866c-128">Carga de activos</span><span class="sxs-lookup"><span data-stu-id="f866c-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="f866c-129">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="f866c-129">Create an asset</span></span>

<span data-ttu-id="f866c-130">Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="f866c-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="f866c-131">Hola API de REST, crear un activo requiere el envío de POST solicitar servicios de tooMedia y colocar cualquier información de propiedad sobre el activo en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f866c-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="f866c-132">Una de las propiedades de Hola que puede especificar al crear un activo es **opciones**.</span><span class="sxs-lookup"><span data-stu-id="f866c-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="f866c-133">**Opciones de** es un valor de enumeración que describe las opciones de cifrado de Hola que se puede crear un activo con.</span><span class="sxs-lookup"><span data-stu-id="f866c-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="f866c-134">Un valor válido es uno de los valores de hello de lista Hola siguiente, no una combinación de valores.</span><span class="sxs-lookup"><span data-stu-id="f866c-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="f866c-135">**None** = **0**: no se usará cifrado.</span><span class="sxs-lookup"><span data-stu-id="f866c-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="f866c-136">Se trata de un valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-136">This is hello default value.</span></span> <span data-ttu-id="f866c-137">Tenga en cuenta que al utilizar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f866c-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="f866c-138">Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use esta opción.</span><span class="sxs-lookup"><span data-stu-id="f866c-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="f866c-139">**StorageEncrypted** = **1**: especifique si desea para su toobe archivos cifrado con cifrado de AES de 256 bits para la carga y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f866c-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="f866c-140">Si el recurso tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="f866c-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="f866c-141">Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f866c-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="f866c-142">**CommonEncryptionProtected** = **2**: especifique si va a cargar archivos protegidos con un método de cifrado común (por ejemplo, PlayReady).</span><span class="sxs-lookup"><span data-stu-id="f866c-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="f866c-143">**EnvelopeEncryptionProtected** = **4**: especifique si va a cargar HLS cifrado con archivos AES.</span><span class="sxs-lookup"><span data-stu-id="f866c-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="f866c-144">Tenga en cuenta que deben ha codificado y cifrado con Transform Manager archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="f866c-145">Si el recurso usa cifrado, debe crear un **ContentKey** y vincúlela tooyour asset tal y como se describe en el tema siguiente de hello:[cómo toocreate una ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="f866c-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="f866c-146">Tenga en cuenta que después de cargar archivos de hello en activo de hello, necesario tooupdate propiedades de cifrado de hello en hello **AssetFile** entidad con valores de hello que se obtuvo durante hello **Asset** cifrado.</span><span class="sxs-lookup"><span data-stu-id="f866c-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="f866c-147">Hacer mediante hello **mezcla** solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f866c-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="f866c-148">Hola siguiente ejemplo se muestra cómo toocreate un activo.</span><span class="sxs-lookup"><span data-stu-id="f866c-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="f866c-149">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="f866c-150">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-150">**HTTP Response**</span></span>

<span data-ttu-id="f866c-151">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f866c-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="f866c-152">Creación de AssetFile</span><span class="sxs-lookup"><span data-stu-id="f866c-152">Create an AssetFile</span></span>
<span data-ttu-id="f866c-153">Hola [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidad representa un archivo de vídeo o audio que se almacena en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="f866c-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="f866c-154">Un archivo de recursos siempre está asociado a un recurso y un recurso puede contener uno o varios archivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="f866c-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="f866c-155">se produce un error en la tarea de codificador de servicios multimedia de Hello si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="f866c-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="f866c-156">Tenga en cuenta que hello **AssetFile** instancia y archivo de hello multimedia real son dos objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="f866c-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="f866c-157">instancia de AssetFile Hola contiene metadatos sobre archivo multimedia de hello, mientras que el archivo de medios de hello contiene contenido multimedia real de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="f866c-158">Después de cargar el archivo multimedia digital en un contenedor de blobs, usará hello **mezcla** tooupdate hello AssetFile HTTP solicitud con información sobre el archivo multimedia (como se muestra más adelante en el tema de hello).</span><span class="sxs-lookup"><span data-stu-id="f866c-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="f866c-159">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="f866c-160">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="f866c-161">Creación de hello AccessPolicy con permiso de escritura.</span><span class="sxs-lookup"><span data-stu-id="f866c-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="f866c-162">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f866c-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f866c-163">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="f866c-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f866c-164">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="f866c-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="f866c-165">Antes de cargar los archivos en el almacenamiento de blobs, configurar el acceso de hello derechos de directiva para escribir tooan activo.</span><span class="sxs-lookup"><span data-stu-id="f866c-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="f866c-166">establece toodo que registrar un toohello de solicitud HTTP entidades AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="f866c-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="f866c-167">Defina un valor DurationInMinutes durante la creación o recibirá un mensaje de error de servidor interno 500 como respuesta.</span><span class="sxs-lookup"><span data-stu-id="f866c-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="f866c-168">Para obtener más información sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="f866c-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="f866c-169">Hola siguiente ejemplo se muestra cómo toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="f866c-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="f866c-170">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="f866c-171">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="f866c-172">Obtener Hola cargar dirección URL</span><span class="sxs-lookup"><span data-stu-id="f866c-172">Get hello Upload URL</span></span>
<span data-ttu-id="f866c-173">tooreceive Hola dirección URL de carga real, cree un localizador SAS.</span><span class="sxs-lookup"><span data-stu-id="f866c-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="f866c-174">Los localizadores definen la hora de inicio de Hola y el tipo de extremo de conexión para los clientes que desea que los archivos de tooaccess en un recurso.</span><span class="sxs-lookup"><span data-stu-id="f866c-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="f866c-175">Puede crear varias entidades Locator para un determinada AccessPolicy Asset par toohandle diferentes cliente y las solicitudes y necesidades.</span><span class="sxs-lookup"><span data-stu-id="f866c-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="f866c-176">Cada uno de los localizadores usa valores de StartTime de Hola y DurationInMinutes de Hola de longitud de hello AccessPolicy toodetermine Hola de tiempo se puede utilizar una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f866c-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="f866c-177">Para obtener más información, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="f866c-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="f866c-178">Una dirección URL SAS tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="f866c-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="f866c-179">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="f866c-179">Some considerations apply:</span></span>

* <span data-ttu-id="f866c-180">No puede tener más de cinco localizadores únicos asociados a un recurso determinado a la vez.</span><span class="sxs-lookup"><span data-stu-id="f866c-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="f866c-181">Para obtener más información, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="f866c-181">For more information, see Locator.</span></span>
* <span data-ttu-id="f866c-182">Si necesita los archivos de tooupload de forma inmediata, debe establecer los minutos de toofive de valor de StartTime antes Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="f866c-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="f866c-183">Esto se debe a que puede haber un desplazamiento de reloj entre el equipo cliente y Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="f866c-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="f866c-184">Además, debe ser el valor de StartTime Hola siguiendo el formato de fecha y hora: aaaa-MM-ddTHH (por ejemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="f866c-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="f866c-185">Puede haber un 30 a 40 segundos retrasar después de crear un localizador toowhen está disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="f866c-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="f866c-186">Este problema aplica tooboth URL de SAS y localizadores de origen.</span><span class="sxs-lookup"><span data-stu-id="f866c-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="f866c-187">Hola de ejemplo siguiente muestra cómo toocreate un localizador de URL de SAS, tal como se define por Hola propiedad de tipo en el cuerpo de la solicitud de hello ("1" para un localizador SAS) y "2" de un localizador de origen a petición.</span><span class="sxs-lookup"><span data-stu-id="f866c-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="f866c-188">Hola **ruta de acceso** propiedad devuelta contiene la dirección URL de Hola que se debe usar tooupload en el archivo.</span><span class="sxs-lookup"><span data-stu-id="f866c-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="f866c-189">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="f866c-190">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-190">**HTTP Response**</span></span>

<span data-ttu-id="f866c-191">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="f866c-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="f866c-192">Carga de un archivo en un contenedor de almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="f866c-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="f866c-193">Una vez que tenga hello AccessPolicy y conjunto de localizador, archivo real de hello es el contenedor de almacenamiento de blobs de Azure de tooan cargados con hello las API de REST de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f866c-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="f866c-194">Debe cargar archivos de hello como blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="f866c-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="f866c-195">Azure Media Services no admite los blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="f866c-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="f866c-196">Debe agregar el nombre del archivo de hello para el archivo hello desea tooupload toohello localizador **ruta de acceso** valor recibido en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="f866c-197">Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="f866c-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="f866c-198">.</span><span class="sxs-lookup"><span data-stu-id="f866c-198">.</span></span> <span data-ttu-id="f866c-199">.</span><span class="sxs-lookup"><span data-stu-id="f866c-199">.</span></span> <span data-ttu-id="f866c-200">.</span><span class="sxs-lookup"><span data-stu-id="f866c-200">.</span></span> 
> 
> 

<span data-ttu-id="f866c-201">Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="f866c-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="f866c-202">Actualizar hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="f866c-202">Update hello AssetFile</span></span>
<span data-ttu-id="f866c-203">Ahora que ha cargado el archivo, para actualizar información de hello FileAsset tamaño (y otros).</span><span class="sxs-lookup"><span data-stu-id="f866c-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="f866c-204">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f866c-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="f866c-205">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-205">**HTTP Response**</span></span>

<span data-ttu-id="f866c-206">Si es correcta, siguiente Hola se devuelve: HTTP/1.1 204 Sin contenido</span><span class="sxs-lookup"><span data-stu-id="f866c-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="f866c-207">Eliminar Hola localizador y AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="f866c-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="f866c-208">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="f866c-209">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-209">**HTTP Response**</span></span>

<span data-ttu-id="f866c-210">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f866c-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="f866c-211">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="f866c-212">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-212">**HTTP Response**</span></span>

<span data-ttu-id="f866c-213">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f866c-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="f866c-214"><a id="upload_in_bulk"></a>Carga de activos en bloque</span><span class="sxs-lookup"><span data-stu-id="f866c-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="f866c-215">Crear hello IngestManifest</span><span class="sxs-lookup"><span data-stu-id="f866c-215">Create hello IngestManifest</span></span>
<span data-ttu-id="f866c-216">Hola IngestManifest es un contenedor para un conjunto de activos, archivos de recursos e información estadística que se puede usar toodetermine progreso de hello de la ingesta en bloque para el conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="f866c-217">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="f866c-218">Creación de activos</span><span class="sxs-lookup"><span data-stu-id="f866c-218">Create assets</span></span>
<span data-ttu-id="f866c-219">Antes de crear hello IngestManifestAsset, debe toocreate Hola activo que se llevará a cabo mediante la ingesta en bloque.</span><span class="sxs-lookup"><span data-stu-id="f866c-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="f866c-220">Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="f866c-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="f866c-221">Hola API de REST, crear un activo requiere enviar una tooMicrosoft de solicitud HTTP POST servicios multimedia de Azure y la colocación de cualquier información de propiedad sobre el activo en el cuerpo de la solicitud de Hola. En este ejemplo, hello Asset se crea con hello StorageEncrption(1) opción incluido con el cuerpo de la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="f866c-222">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="f866c-223">Crear hello IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="f866c-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="f866c-224">IngestManifestAssets representan los activos dentro de un IngestManifest que se utilizan con la ingesta en bloque.</span><span class="sxs-lookup"><span data-stu-id="f866c-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="f866c-225">Hola básicamente manifiesto toohello de vínculo Hola activo.</span><span class="sxs-lookup"><span data-stu-id="f866c-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="f866c-226">Servicios multimedia de Azure supervisa internamente para cargar el archivo hello en función de la colección asociada de IngestManifestFiles toohello IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="f866c-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="f866c-227">Una vez que estos archivos se cargan, recurso de hello está completo.</span><span class="sxs-lookup"><span data-stu-id="f866c-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="f866c-228">Puede crear un nuevo IngestManifestAsset con una solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="f866c-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="f866c-229">En el cuerpo de la solicitud de hello, incluyen hello identificador de recurso que IngestManifestAsset debe vincular para la ingesta en bloque de Hola y Hola identificador de IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="f866c-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="f866c-230">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="f866c-231">Crear hello IngestManifestFiles para cada activo</span><span class="sxs-lookup"><span data-stu-id="f866c-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="f866c-232">Un IngestManifestFile representa un objeto blob de audio o vídeo real que se cargará como parte de la ingesta en bloque de un activo.</span><span class="sxs-lookup"><span data-stu-id="f866c-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="f866c-233">Cifrado relacionados con propiedades no son necesarias a menos que Hola recurso use una opción de cifrado.</span><span class="sxs-lookup"><span data-stu-id="f866c-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="f866c-234">Hello en el ejemplo se utilizan en esta sección se muestra la creación de un IngestManifestFile que usa StorageEncryption para hello que Asset creado previamente.</span><span class="sxs-lookup"><span data-stu-id="f866c-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="f866c-235">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="f866c-236">Cargar archivos de hello tooBlob almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f866c-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="f866c-237">Puede usar cualquier aplicación de cliente de alta velocidad capaz de cargar el contenedor de almacenamiento de hello asset archivos toohello blob Uri proporcionado por la propiedad BlobStorageUriForUpload de hello IngestManifest Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="f866c-238">Un servicio de carga de alta velocidad destacado es [Aspera On Demand para la aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="f866c-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="f866c-239">Supervisión del progreso de la ingesta en bloque</span><span class="sxs-lookup"><span data-stu-id="f866c-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="f866c-240">Puede supervisar el progreso de Hola de ingesta de operaciones de un IngestManifest sondeando la propiedad de las estadísticas de Hola de hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="f866c-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="f866c-241">Esta propiedad es de tipo complejo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="f866c-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="f866c-242">hello toopoll propiedad Statistics, enviar una solicitud HTTP GET pasar Hola identificador de IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="f866c-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="f866c-243">Creación de ContentKeys para el cifrado</span><span class="sxs-lookup"><span data-stu-id="f866c-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="f866c-244">Si el recurso usa cifrado, debe crear hello ContentKey toobe usado para el cifrado antes de crear archivos de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="f866c-245">Para el cifrado de almacenamiento, hello siguientes propiedades se deben incluir en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f866c-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="f866c-246">Propiedad del cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="f866c-246">Request body property</span></span> | <span data-ttu-id="f866c-247">Description</span><span class="sxs-lookup"><span data-stu-id="f866c-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f866c-248">Id</span><span class="sxs-lookup"><span data-stu-id="f866c-248">Id</span></span> |<span data-ttu-id="f866c-249">Hello identificador de ContentKey que generamos desarrollamos con hello después de dar formato, "NB:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="f866c-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="f866c-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="f866c-250">ContentKeyType</span></span> |<span data-ttu-id="f866c-251">Este es el tipo de clave contenido de Hola como un número entero para esta clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="f866c-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="f866c-252">Pasamos el valor de hello 1 para el cifrado de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f866c-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="f866c-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="f866c-253">EncryptedContentKey</span></span> |<span data-ttu-id="f866c-254">Creamos un valor de clave de contenido que es un valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="f866c-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="f866c-255">clave de Hola se cifra mediante el certificado X.509 de cifrado de almacenamiento de Hola que recuperamos de servicios multimedia de Microsoft Azure mediante la ejecución de una solicitud HTTP GET hello GetProtectionKeyId y GetProtectionKey métodos.</span><span class="sxs-lookup"><span data-stu-id="f866c-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="f866c-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="f866c-256">ProtectionKeyId</span></span> |<span data-ttu-id="f866c-257">Esto es Hola Id. de clave de protección para el certificado X.509 de cifrado de almacenamiento de Hola que estaba tooencrypt usa la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="f866c-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="f866c-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="f866c-258">ProtectionKeyType</span></span> |<span data-ttu-id="f866c-259">Se trata de un tipo de cifrado de hello para la clave de protección de Hola que fue utilizado tooencrypt Hola contenido clave.</span><span class="sxs-lookup"><span data-stu-id="f866c-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="f866c-260">Este valor es StorageEncryption(1) en nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f866c-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="f866c-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="f866c-261">Checksum</span></span> |<span data-ttu-id="f866c-262">Hola MD5 suma de comprobación calculada Hola clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="f866c-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="f866c-263">Se calcula mediante el cifrado de contenido de hello identificador con clave de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="f866c-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="f866c-264">código de ejemplo de Hola muestra cómo toocalculate Hola suma de comprobación.</span><span class="sxs-lookup"><span data-stu-id="f866c-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="f866c-265">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="f866c-266">Vincular hello ContentKey toohello activo</span><span class="sxs-lookup"><span data-stu-id="f866c-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="f866c-267">Hola ContentKey es tooone asociado o más activos mediante el envío de una solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="f866c-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="f866c-268">Hello solicitud siguiente es un recurso en el ejemplo se toolink Hola ejemplo ContentKey toohello ejemplo por identificador.</span><span class="sxs-lookup"><span data-stu-id="f866c-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="f866c-269">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="f866c-270">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f866c-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="f866c-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f866c-271">Next steps</span></span>

<span data-ttu-id="f866c-272">Ahora puede codificar los recursos cargados.</span><span class="sxs-lookup"><span data-stu-id="f866c-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="f866c-273">Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="f866c-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="f866c-274">También puede utilizar las funciones de Azure tootrigger un trabajo de codificación basado en un archivo que llegan en el contenedor de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="f866c-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="f866c-275">Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="f866c-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f866c-276">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="f866c-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f866c-277">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f866c-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

