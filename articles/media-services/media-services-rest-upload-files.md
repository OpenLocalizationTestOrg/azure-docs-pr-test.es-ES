---
title: Carga de archivos en una cuenta de Media Services mediante REST | Microsoft Docs
description: "Aprenda a obtener contenido multimedia en Servicios multimedia mediante la creación y carga de recursos."
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="76575-103">Carga de archivos en una cuenta de Servicios multimedia mediante API de REST</span><span class="sxs-lookup"><span data-stu-id="76575-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76575-104">.NET</span><span class="sxs-lookup"><span data-stu-id="76575-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="76575-105">REST</span><span class="sxs-lookup"><span data-stu-id="76575-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="76575-106">Portal</span><span class="sxs-lookup"><span data-stu-id="76575-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="76575-107">En Servicios multimedia, cargue los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="76575-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="76575-108">La entidad [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) puede contener archivos de vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y subtítulos (y los metadatos sobre estos archivos).  Una vez cargados los archivos en el recurso, el contenido se almacena de forma segura en la nube para un posterior procesamiento y streaming.</span><span class="sxs-lookup"><span data-stu-id="76575-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="76575-109">Se aplican las siguientes consideraciones:</span><span class="sxs-lookup"><span data-stu-id="76575-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="76575-110">Los Servicios multimedia usan el valor de la propiedad IAssetFile.Name al generar direcciones URL para el contenido de streaming (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="76575-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="76575-111">El valor de la propiedad **Name**no puede tener ninguno de los siguientes [caracteres reservados para la codificación porcentual](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):!*'();:@&=+$,/?%#[]" </span><span class="sxs-lookup"><span data-stu-id="76575-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="76575-112">Además, solo puede haber un '.' para la extensión del nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="76575-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="76575-113">La longitud del nombre no debe ser superior a 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="76575-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="76575-114">Existe un límite máximo de tamaño de archivo admitido para el procesamiento en Media Services.</span><span class="sxs-lookup"><span data-stu-id="76575-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="76575-115">Consulte [este](media-services-quotas-and-limitations.md) tema para obtener información más detallada acerca de la limitación de tamaño de archivo.</span><span class="sxs-lookup"><span data-stu-id="76575-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="76575-116">El flujo de trabajo básico para la carga de activos se divide en las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="76575-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="76575-117">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="76575-117">Create an Asset</span></span>
* <span data-ttu-id="76575-118">Cifrado de un recurso (opcional)</span><span class="sxs-lookup"><span data-stu-id="76575-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="76575-119">Carga de un archivo al almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="76575-119">Upload a file to blob storage</span></span>

<span data-ttu-id="76575-120">AMS también permite cargar activos en bloque.</span><span class="sxs-lookup"><span data-stu-id="76575-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="76575-121">Para obtener más información, consulte [esta](media-services-rest-upload-files.md#upload_in_bulk) sección.</span><span class="sxs-lookup"><span data-stu-id="76575-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="76575-122">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="76575-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="76575-123">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="76575-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="76575-124">Conexión con Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="76575-124">Connect to Media Services</span></span>

<span data-ttu-id="76575-125">Para obtener más información sobre cómo conectarse a la API de Azure Media Services, consulte [Acceso a la API de Azure Media Services con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="76575-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="76575-126">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="76575-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="76575-127">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="76575-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="76575-128">Carga de activos</span><span class="sxs-lookup"><span data-stu-id="76575-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="76575-129">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="76575-129">Create an asset</span></span>

<span data-ttu-id="76575-130">Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="76575-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="76575-131">En la API de REST, crear un recurso requiere el envío de una solicitud POST a Servicios multimedia y colocar la información sobre cualquier propiedad del recurso en el cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="76575-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="76575-132">Una de las propiedades que se pueden especificar al crear un recurso es **Options**.</span><span class="sxs-lookup"><span data-stu-id="76575-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="76575-133">**Options** es un valor de enumeración que describe las opciones de cifrado con las que se puede crear un recurso.</span><span class="sxs-lookup"><span data-stu-id="76575-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="76575-134">Un valor válido es uno de los valores de la lista siguiente, no una combinación de valores.</span><span class="sxs-lookup"><span data-stu-id="76575-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="76575-135">**None** = **0**: no se usará cifrado.</span><span class="sxs-lookup"><span data-stu-id="76575-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="76575-136">Este es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="76575-136">This is the default value.</span></span> <span data-ttu-id="76575-137">Tenga en cuenta que al utilizar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="76575-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="76575-138">Si tiene previsto entregar un MP4 mediante una descarga progresiva, utilice esta opción.</span><span class="sxs-lookup"><span data-stu-id="76575-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="76575-139">**StorageEncrypted** = **1**: especifique si desea que los archivos se cifren con cifrado AES de 256 bits para la carga y el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="76575-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="76575-140">Si el recurso tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="76575-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="76575-141">Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="76575-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="76575-142">**CommonEncryptionProtected** = **2**: especifique si va a cargar archivos protegidos con un método de cifrado común (por ejemplo, PlayReady).</span><span class="sxs-lookup"><span data-stu-id="76575-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="76575-143">**EnvelopeEncryptionProtected** = **4**: especifique si va a cargar HLS cifrado con archivos AES.</span><span class="sxs-lookup"><span data-stu-id="76575-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="76575-144">Tenga en cuenta que los archivos deben haberse codificado y cifrado con Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="76575-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="76575-145">Si el recurso usa cifrado, debe crear una **ContentKey** y vincularla al recurso, tal como se describe en el siguiente tema:[Creación de ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="76575-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="76575-146">Tenga en cuenta que después de cargar los archivos en el recurso, debe actualizar las propiedades de cifrado en la entidad **AssetFile** con los valores que obtuvo durante el cifrado del **recurso**.</span><span class="sxs-lookup"><span data-stu-id="76575-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="76575-147">Para ello, use la solicitud HTTP **MERGE** .</span><span class="sxs-lookup"><span data-stu-id="76575-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="76575-148">En el ejemplo siguiente se muestra cómo crear un recurso.</span><span class="sxs-lookup"><span data-stu-id="76575-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="76575-149">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-149">**HTTP Request**</span></span>

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

<span data-ttu-id="76575-150">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-150">**HTTP Response**</span></span>

<span data-ttu-id="76575-151">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="76575-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="76575-152">Creación de AssetFile</span><span class="sxs-lookup"><span data-stu-id="76575-152">Create an AssetFile</span></span>
<span data-ttu-id="76575-153">La entidad [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa un archivo de audio o vídeo que se almacena en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="76575-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="76575-154">Un archivo de recursos siempre está asociado a un recurso y un recurso puede contener uno o varios archivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="76575-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="76575-155">La tarea de Servicios multimedia produce un error si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="76575-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="76575-156">Tenga en cuenta que la instancia de **AssetFile** y el archivo multimedia real son dos objetos distintos.</span><span class="sxs-lookup"><span data-stu-id="76575-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="76575-157">La instancia de AssetFile contiene metadatos sobre el archivo multimedia, mientras que el archivo multimedia contiene el contenido multimedia real.</span><span class="sxs-lookup"><span data-stu-id="76575-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="76575-158">Después de cargar el archivo multimedia digital en un contenedor de blobs, usará la solicitud HTTP **MERGE** para actualizar la entidad AssetFile con información sobre el archivo multimedia (tal como se muestra más adelante en este tema).</span><span class="sxs-lookup"><span data-stu-id="76575-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="76575-159">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-159">**HTTP Request**</span></span>

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

<span data-ttu-id="76575-160">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="76575-161">Creación de AccessPolicy con permiso de escritura.</span><span class="sxs-lookup"><span data-stu-id="76575-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="76575-162">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="76575-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="76575-163">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="76575-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="76575-164">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="76575-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="76575-165">Antes de cargar los archivos en el almacenamiento de blobs, establezca los derechos de la directiva de acceso para escribir en un recurso.</span><span class="sxs-lookup"><span data-stu-id="76575-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="76575-166">Para ello, envíe una solicitud HTTP al conjunto de entidades AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="76575-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="76575-167">Defina un valor DurationInMinutes durante la creación o recibirá un mensaje de error de servidor interno 500 como respuesta.</span><span class="sxs-lookup"><span data-stu-id="76575-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="76575-168">Para obtener más información sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="76575-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="76575-169">En el ejemplo siguiente se muestra cómo crear una entidad AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="76575-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="76575-170">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-170">**HTTP Request**</span></span>

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

<span data-ttu-id="76575-171">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="76575-172">Obtención de la dirección URL de carga</span><span class="sxs-lookup"><span data-stu-id="76575-172">Get the Upload URL</span></span>
<span data-ttu-id="76575-173">Para recibir la dirección URL de carga real, cree un localizador de SAS.</span><span class="sxs-lookup"><span data-stu-id="76575-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="76575-174">Los localizadores definen la hora de inicio y el tipo de extremo de conexión para los clientes que desean tener acceso a archivos de un recurso.</span><span class="sxs-lookup"><span data-stu-id="76575-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="76575-175">Puede crear varias entidades Locator para un par AccessPolicy y Asset determinado a fin de controlar las distintas solicitudes y necesidades del cliente.</span><span class="sxs-lookup"><span data-stu-id="76575-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="76575-176">Cada uno de estos localizadores usa el valor StartTime más el valor DurationInMinutes de AccessPolicy para determinar la cantidad de tiempo que se puede usar una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="76575-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="76575-177">Para obtener más información, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="76575-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="76575-178">Una dirección URL de SAS tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="76575-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="76575-179">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="76575-179">Some considerations apply:</span></span>

* <span data-ttu-id="76575-180">No puede tener más de cinco localizadores únicos asociados a un recurso determinado a la vez.</span><span class="sxs-lookup"><span data-stu-id="76575-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="76575-181">Para obtener más información, consulte Localizador.</span><span class="sxs-lookup"><span data-stu-id="76575-181">For more information, see Locator.</span></span>
* <span data-ttu-id="76575-182">Si necesita cargar los archivos inmediatamente, debe establecer el valor StartTime cinco minutos antes de la hora actual.</span><span class="sxs-lookup"><span data-stu-id="76575-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="76575-183">Esto se debe a que puede haber un desplazamiento de reloj entre el equipo cliente y Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="76575-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="76575-184">Además, el valor de StartTime debe tener el siguiente formato: YYYY-MM-DDTHH:mm:ssZ (por ejemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="76575-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="76575-185">Puede haber un retraso de 30 a 40 segundos desde el momento en que se crea un localizador hasta que este está disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="76575-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="76575-186">Este problema afecta a la dirección URL de SAS y a localizadores de origen.</span><span class="sxs-lookup"><span data-stu-id="76575-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="76575-187">En el ejemplo siguiente se muestra cómo crear un localizador de dirección URL de SAS, tal como se define en la propiedad Type del cuerpo de solicitud ("1" para un localizador de SAS y "2" para un localizador de origen bajo demanda).</span><span class="sxs-lookup"><span data-stu-id="76575-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="76575-188">La propiedad **Path** devuelta contiene la dirección URL que debe usar para cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="76575-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="76575-189">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-189">**HTTP Request**</span></span>

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

<span data-ttu-id="76575-190">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-190">**HTTP Response**</span></span>

<span data-ttu-id="76575-191">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="76575-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="76575-192">Carga de un archivo en un contenedor de almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="76575-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="76575-193">Una vez establecidas AccessPolicy y Locator, el archivo real se carga en un contenedor de almacenamiento de blobs de Azure mediante las API de REST de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="76575-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="76575-194">Debe cargar los archivos como blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="76575-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="76575-195">Azure Media Services no admite los blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="76575-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="76575-196">Debe agregar el nombre de archivo para el archivo que desea cargar en el valor **Path** del localizador recibido en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="76575-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="76575-197">Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="76575-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="76575-198">.</span><span class="sxs-lookup"><span data-stu-id="76575-198">.</span></span> <span data-ttu-id="76575-199">.</span><span class="sxs-lookup"><span data-stu-id="76575-199">.</span></span> <span data-ttu-id="76575-200">.</span><span class="sxs-lookup"><span data-stu-id="76575-200">.</span></span> 
> 
> 

<span data-ttu-id="76575-201">Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="76575-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="76575-202">Actualización de AssetFile</span><span class="sxs-lookup"><span data-stu-id="76575-202">Update the AssetFile</span></span>
<span data-ttu-id="76575-203">Ahora que ha cargado el archivo, actualice la información de tamaño de FileAsset (y otro tipo de información).</span><span class="sxs-lookup"><span data-stu-id="76575-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="76575-204">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="76575-204">For example:</span></span>

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


<span data-ttu-id="76575-205">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-205">**HTTP Response**</span></span>

<span data-ttu-id="76575-206">Si se realiza correctamente, se devuelve lo siguiente: HTTP/1.1 204 No Content</span><span class="sxs-lookup"><span data-stu-id="76575-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="76575-207">Eliminación de Locator y AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="76575-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="76575-208">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="76575-209">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-209">**HTTP Response**</span></span>

<span data-ttu-id="76575-210">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="76575-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="76575-211">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="76575-212">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-212">**HTTP Response**</span></span>

<span data-ttu-id="76575-213">Si se realiza correctamente, se devuelve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="76575-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="76575-214"><a id="upload_in_bulk"></a>Carga de activos en bloque</span><span class="sxs-lookup"><span data-stu-id="76575-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="76575-215">Creación de IngestManifest</span><span class="sxs-lookup"><span data-stu-id="76575-215">Create the IngestManifest</span></span>
<span data-ttu-id="76575-216">IngestManifest es un contenedor para un conjunto de activos, archivos de activos e información estadística que puede utilizarse para determinar el progreso de la ingesta en bloque para el conjunto.</span><span class="sxs-lookup"><span data-stu-id="76575-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="76575-217">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="76575-218">Creación de activos</span><span class="sxs-lookup"><span data-stu-id="76575-218">Create assets</span></span>
<span data-ttu-id="76575-219">Antes de crear IngestManifestAsset, deberá crear el activo que se completará con la ingesta en bloque.</span><span class="sxs-lookup"><span data-stu-id="76575-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="76575-220">Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="76575-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="76575-221">En la API de REST, para crear un activo hay que enviar una solicitud HTTP POST a los Servicios multimedia de Microsoft Azure y colocar cualquier información sobre las propiedades del activo en el cuerpo de solicitud. En este ejemplo, el activo se crea mediante la opción StorageEncrption(1) incluida en el cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="76575-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="76575-222">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="76575-223">Creación de IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="76575-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="76575-224">IngestManifestAssets representan los activos dentro de un IngestManifest que se utilizan con la ingesta en bloque.</span><span class="sxs-lookup"><span data-stu-id="76575-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="76575-225">Básicamente, lo que hacen es vincular el activo al manifiesto.</span><span class="sxs-lookup"><span data-stu-id="76575-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="76575-226">Los Servicios multimedia de Azure buscan internamente el archivo cargado en función de la colección de IngestManifestFiles asociada a IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="76575-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="76575-227">Una vez que se hayan cargado los archivos, el activo estará completo.</span><span class="sxs-lookup"><span data-stu-id="76575-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="76575-228">Puede crear un nuevo IngestManifestAsset con una solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="76575-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="76575-229">En el cuerpo de solicitud, incluya el identificador de IngestManifest y el identificador del activo que IngestManifestAsset debe vincular para la ingesta en bloque.</span><span class="sxs-lookup"><span data-stu-id="76575-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="76575-230">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="76575-231">Creación de IngestManifestFiles para cada activo</span><span class="sxs-lookup"><span data-stu-id="76575-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="76575-232">Un IngestManifestFile representa un objeto blob de audio o vídeo real que se cargará como parte de la ingesta en bloque de un activo.</span><span class="sxs-lookup"><span data-stu-id="76575-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="76575-233">Propiedades de cifrado relacionadas que no son necesarias, a menos que el recurso esté usando una opción de cifrado.</span><span class="sxs-lookup"><span data-stu-id="76575-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="76575-234">El ejemplo utilizado en esta sección muestra la creación de un IngestManifestFile que usa StorageEncryption para el activo creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="76575-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="76575-235">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="76575-236">Carga de archivos en el almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="76575-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="76575-237">Puede usar cualquier aplicación cliente de alta velocidad capaz de cargar los archivos de activos en el URI del contenedor de almacenamiento de blobs proporcionado por la propiedad BlobStorageUriForUpload de IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="76575-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="76575-238">Un servicio de carga de alta velocidad destacado es [Aspera On Demand para la aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="76575-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="76575-239">Supervisión del progreso de la ingesta en bloque</span><span class="sxs-lookup"><span data-stu-id="76575-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="76575-240">Puede supervisar el progreso de las operaciones de ingesta en bloque para un IngestManifest mediante el sondeo de la propiedad Statistics de IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="76575-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="76575-241">Esta propiedad es de tipo complejo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="76575-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="76575-242">Para sondear la propiedad Statistics, envíe una solicitud HTTP GET pasando el identificador de IngestManifest</span><span class="sxs-lookup"><span data-stu-id="76575-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="76575-243">Creación de ContentKeys para el cifrado</span><span class="sxs-lookup"><span data-stu-id="76575-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="76575-244">Si el activo va a usar cifrado, debe crear la ContentKey que se utilizará para el cifrado antes de crear los archivos de recurso.</span><span class="sxs-lookup"><span data-stu-id="76575-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="76575-245">Para el cifrado de almacenamiento, se deben incluir las siguientes propiedades en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76575-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="76575-246">Propiedad del cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="76575-246">Request body property</span></span> | <span data-ttu-id="76575-247">Description</span><span class="sxs-lookup"><span data-stu-id="76575-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76575-248">Id</span><span class="sxs-lookup"><span data-stu-id="76575-248">Id</span></span> |<span data-ttu-id="76575-249">El identificador de ContentKey que generamos nosotros mismos utilizando el siguiente formato “nb:kid:UUID:<NEW GUID>”.</span><span class="sxs-lookup"><span data-stu-id="76575-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="76575-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="76575-250">ContentKeyType</span></span> |<span data-ttu-id="76575-251">Este es el tipo de clave de contenido en forma de entero para esta clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="76575-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="76575-252">Pasamos el valor 1 para el cifrado del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="76575-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="76575-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="76575-253">EncryptedContentKey</span></span> |<span data-ttu-id="76575-254">Creamos un valor de clave de contenido que es un valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="76575-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="76575-255">La clave se cifra con el certificado X.509 de cifrado de almacenamiento que recuperamos de Servicios multimedia de Microsoft Azure mediante la ejecución de una solicitud HTTP GET para los métodos de GetProtectionKeyId y GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="76575-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="76575-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="76575-256">ProtectionKeyId</span></span> |<span data-ttu-id="76575-257">Es el identificador de la clave de protección para el certificado X.509 de cifrado de almacenamiento que se usó para cifrar la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="76575-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="76575-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="76575-258">ProtectionKeyType</span></span> |<span data-ttu-id="76575-259">Es el tipo de cifrado para la clave de protección que se usó para cifrar la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="76575-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="76575-260">Este valor es StorageEncryption(1) en nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="76575-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="76575-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="76575-261">Checksum</span></span> |<span data-ttu-id="76575-262">Suma de comprobación calculada de MD5 para la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="76575-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="76575-263">Se calcula mediante el cifrado del identificador de contenido con la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="76575-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="76575-264">El código de ejemplo muestra cómo calcular la suma de comprobación.</span><span class="sxs-lookup"><span data-stu-id="76575-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="76575-265">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="76575-266">Vinculación de ContentKey al activo</span><span class="sxs-lookup"><span data-stu-id="76575-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="76575-267">ContentKey se asocia a uno o varios activos al enviar una solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="76575-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="76575-268">La solicitud siguiente es un ejemplo para vincular la ContentKey de ejemplo con el conjunto de activos de ejemplo en función del identificador.</span><span class="sxs-lookup"><span data-stu-id="76575-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="76575-269">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-269">**HTTP Response**</span></span>

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

<span data-ttu-id="76575-270">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="76575-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="76575-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76575-271">Next steps</span></span>

<span data-ttu-id="76575-272">Ahora puede codificar los recursos cargados.</span><span class="sxs-lookup"><span data-stu-id="76575-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="76575-273">Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="76575-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="76575-274">También puede usar Azure Functions para desencadenar un trabajo de codificación basado en un archivo que llega al contenedor configurado.</span><span class="sxs-lookup"><span data-stu-id="76575-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="76575-275">Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="76575-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="76575-276">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="76575-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="76575-277">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="76575-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

