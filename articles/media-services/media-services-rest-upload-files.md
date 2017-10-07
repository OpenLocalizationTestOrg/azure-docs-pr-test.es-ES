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
# <a name="upload-files-into-a-media-services-account-using-rest"></a>Carga de archivos en una cuenta de Servicios multimedia mediante API de REST
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

En Servicios multimedia, cargue los archivos digitales en un recurso. Hola [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entidad puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.)  Una vez Hola archivos se cargan en el recurso de hello, el contenido está almacenado con seguridad en nube de Hola para su posterior procesamiento y transmisión por secuencias. 

> [!NOTE]
> Hola siguientes consideraciones se aplica:
> 
> * Servicios multimedia usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual. Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Además, solo puede haber uno '.' para la extensión de nombre de archivo de Hola.
> * longitud de Hello del nombre de hello no debería ser superior a 260 caracteres.
> * Hay un tamaño de archivo máximo de toohello límite admitido para el procesamiento de los servicios multimedia. Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.
> 

flujo de trabajo básico de Hola para cargar los activos se divide en hello las secciones siguientes:

* Creación de un recurso
* Cifrado de un recurso (opcional)
* Cargar un almacenamiento de tooblob de archivo

AMS también permite a activos tooupload de forma masiva. Para obtener más información, consulte [esta](media-services-rest-upload-files.md#upload_in_bulk) sección.

> [!NOTE]
> Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP. Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).
> 

## <a name="connect-toomedia-services"></a>Conectar servicios de tooMedia

Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI.

## <a name="upload-assets"></a>Carga de activos

### <a name="create-an-asset"></a>Creación de un recurso

Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos. Hola API de REST, crear un activo requiere el envío de POST solicitar servicios de tooMedia y colocar cualquier información de propiedad sobre el activo en el cuerpo de la solicitud de saludo.

Una de las propiedades de Hola que puede especificar al crear un activo es **opciones**. **Opciones de** es un valor de enumeración que describe las opciones de cifrado de Hola que se puede crear un activo con. Un valor válido es uno de los valores de hello de lista Hola siguiente, no una combinación de valores. 

* **None** = **0**: no se usará cifrado. Se trata de un valor predeterminado de Hola. Tenga en cuenta que al utilizar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.
    Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use esta opción. 
* **StorageEncrypted** = **1**: especifique si desea para su toobe archivos cifrado con cifrado de AES de 256 bits para la carga y almacenamiento.
  
    Si el recurso tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos. Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).
* **CommonEncryptionProtected** = **2**: especifique si va a cargar archivos protegidos con un método de cifrado común (por ejemplo, PlayReady). 
* **EnvelopeEncryptionProtected** = **4**: especifique si va a cargar HLS cifrado con archivos AES. Tenga en cuenta que deben ha codificado y cifrado con Transform Manager archivos Hola.

> [!NOTE]
> Si el recurso usa cifrado, debe crear un **ContentKey** y vincúlela tooyour asset tal y como se describe en el tema siguiente de hello:[cómo toocreate una ContentKey](media-services-rest-create-contentkey.md). Tenga en cuenta que después de cargar archivos de hello en activo de hello, necesario tooupdate propiedades de cifrado de hello en hello **AssetFile** entidad con valores de hello que se obtuvo durante hello **Asset** cifrado. Hacer mediante hello **mezcla** solicitud HTTP. 
> 
> 

Hola siguiente ejemplo se muestra cómo toocreate un activo.

**Solicitud HTTP**

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

**Respuesta HTTP**

Si se realiza correctamente, se devuelve el siguiente hello:

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

### <a name="create-an-assetfile"></a>Creación de AssetFile
Hola [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidad representa un archivo de vídeo o audio que se almacena en un contenedor de blobs. Un archivo de recursos siempre está asociado a un recurso y un recurso puede contener uno o varios archivos de recursos. se produce un error en la tarea de codificador de servicios multimedia de Hello si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.

Tenga en cuenta que hello **AssetFile** instancia y archivo de hello multimedia real son dos objetos diferentes. instancia de AssetFile Hola contiene metadatos sobre archivo multimedia de hello, mientras que el archivo de medios de hello contiene contenido multimedia real de Hola.

Después de cargar el archivo multimedia digital en un contenedor de blobs, usará hello **mezcla** tooupdate hello AssetFile HTTP solicitud con información sobre el archivo multimedia (como se muestra más adelante en el tema de hello). 

**Solicitud HTTP**

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

**Respuesta HTTP**

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a>Creación de hello AccessPolicy con permiso de escritura.

>[!NOTE]
>Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .

Antes de cargar los archivos en el almacenamiento de blobs, configurar el acceso de hello derechos de directiva para escribir tooan activo. establece toodo que registrar un toohello de solicitud HTTP entidades AccessPolicies. Defina un valor DurationInMinutes durante la creación o recibirá un mensaje de error de servidor interno 500 como respuesta. Para obtener más información sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Hola siguiente ejemplo se muestra cómo toocreate AccessPolicy:

**Solicitud HTTP**

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

**Solicitud HTTP**

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

### <a name="get-hello-upload-url"></a>Obtener Hola cargar dirección URL
tooreceive Hola dirección URL de carga real, cree un localizador SAS. Los localizadores definen la hora de inicio de Hola y el tipo de extremo de conexión para los clientes que desea que los archivos de tooaccess en un recurso. Puede crear varias entidades Locator para un determinada AccessPolicy Asset par toohandle diferentes cliente y las solicitudes y necesidades. Cada uno de los localizadores usa valores de StartTime de Hola y DurationInMinutes de Hola de longitud de hello AccessPolicy toodetermine Hola de tiempo se puede utilizar una dirección URL. Para obtener más información, consulte [Localizador](https://docs.microsoft.com/rest/api/media/operations/locator).

Una dirección URL SAS tiene Hola siguiendo el formato:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Se aplican algunas consideraciones:

* No puede tener más de cinco localizadores únicos asociados a un recurso determinado a la vez. Para obtener más información, consulte Localizador.
* Si necesita los archivos de tooupload de forma inmediata, debe establecer los minutos de toofive de valor de StartTime antes Hola hora actual. Esto se debe a que puede haber un desplazamiento de reloj entre el equipo cliente y Servicios multimedia. Además, debe ser el valor de StartTime Hola siguiendo el formato de fecha y hora: aaaa-MM-ddTHH (por ejemplo, "2014-05-23T17:53:50Z").    
* Puede haber un 30 a 40 segundos retrasar después de crear un localizador toowhen está disponible para su uso. Este problema aplica tooboth URL de SAS y localizadores de origen.

Hola de ejemplo siguiente muestra cómo toocreate un localizador de URL de SAS, tal como se define por Hola propiedad de tipo en el cuerpo de la solicitud de hello ("1" para un localizador SAS) y "2" de un localizador de origen a petición. Hola **ruta de acceso** propiedad devuelta contiene la dirección URL de Hola que se debe usar tooupload en el archivo.

**Solicitud HTTP**

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

**Respuesta HTTP**

Si se realiza correctamente, se devuelve Hola después de respuesta:

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

### <a name="upload-a-file-into-a-blob-storage-container"></a>Carga de un archivo en un contenedor de almacenamiento de blobs
Una vez que tenga hello AccessPolicy y conjunto de localizador, archivo real de hello es el contenedor de almacenamiento de blobs de Azure de tooan cargados con hello las API de REST de almacenamiento de Azure. Debe cargar archivos de hello como blobs en bloques. Azure Media Services no admite los blobs en páginas.  

> [!NOTE]
> Debe agregar el nombre del archivo de hello para el archivo hello desea tooupload toohello localizador **ruta de acceso** valor recibido en la sección anterior de Hola. Por ejemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

Para obtener más información sobre cómo trabajar con blobs de Almacenamiento de Azure, consulte [API de REST del servicio Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Actualizar hello AssetFile
Ahora que ha cargado el archivo, para actualizar información de hello FileAsset tamaño (y otros). Por ejemplo:

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


**Respuesta HTTP**

Si es correcta, siguiente Hola se devuelve: HTTP/1.1 204 Sin contenido

### <a name="delete-hello-locator-and-accesspolicy"></a>Eliminar Hola localizador y AccessPolicy
**Solicitud HTTP**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Respuesta HTTP**

Si se realiza correctamente, se devuelve el siguiente hello:

    HTTP/1.1 204 No Content 
    ...

**Solicitud HTTP**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Respuesta HTTP**

Si se realiza correctamente, se devuelve el siguiente hello:

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>Carga de activos en bloque
### <a name="create-hello-ingestmanifest"></a>Crear hello IngestManifest
Hola IngestManifest es un contenedor para un conjunto de activos, archivos de recursos e información estadística que se puede usar toodetermine progreso de hello de la ingesta en bloque para el conjunto de Hola.

**Solicitud HTTP**

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

### <a name="create-assets"></a>Creación de activos
Antes de crear hello IngestManifestAsset, debe toocreate Hola activo que se llevará a cabo mediante la ingesta en bloque. Un recurso es un contenedor para varios tipos o conjuntos de objetos en Servicios multimedia, como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y archivos de subtítulos. Hola API de REST, crear un activo requiere enviar una tooMicrosoft de solicitud HTTP POST servicios multimedia de Azure y la colocación de cualquier información de propiedad sobre el activo en el cuerpo de la solicitud de Hola. En este ejemplo, hello Asset se crea con hello StorageEncrption(1) opción incluido con el cuerpo de la solicitud de Hola.

**Respuesta HTTP**

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

### <a name="create-hello-ingestmanifestassets"></a>Crear hello IngestManifestAssets
IngestManifestAssets representan los activos dentro de un IngestManifest que se utilizan con la ingesta en bloque. Hola básicamente manifiesto toohello de vínculo Hola activo. Servicios multimedia de Azure supervisa internamente para cargar el archivo hello en función de la colección asociada de IngestManifestFiles toohello IngestManifestAsset. Una vez que estos archivos se cargan, recurso de hello está completo. Puede crear un nuevo IngestManifestAsset con una solicitud HTTP POST. En el cuerpo de la solicitud de hello, incluyen hello identificador de recurso que IngestManifestAsset debe vincular para la ingesta en bloque de Hola y Hola identificador de IngestManifest.

**Respuesta HTTP**

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


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>Crear hello IngestManifestFiles para cada activo
Un IngestManifestFile representa un objeto blob de audio o vídeo real que se cargará como parte de la ingesta en bloque de un activo. Cifrado relacionados con propiedades no son necesarias a menos que Hola recurso use una opción de cifrado. Hello en el ejemplo se utilizan en esta sección se muestra la creación de un IngestManifestFile que usa StorageEncryption para hello que Asset creado previamente.

**Respuesta HTTP**

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

### <a name="upload-hello-files-tooblob-storage"></a>Cargar archivos de hello tooBlob almacenamiento
Puede usar cualquier aplicación de cliente de alta velocidad capaz de cargar el contenedor de almacenamiento de hello asset archivos toohello blob Uri proporcionado por la propiedad BlobStorageUriForUpload de hello IngestManifest Hola. Un servicio de carga de alta velocidad destacado es [Aspera On Demand para la aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=272001).

### <a name="monitor-bulk-ingest-progress"></a>Supervisión del progreso de la ingesta en bloque
Puede supervisar el progreso de Hola de ingesta de operaciones de un IngestManifest sondeando la propiedad de las estadísticas de Hola de hello IngestManifest. Esta propiedad es de tipo complejo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics). hello toopoll propiedad Statistics, enviar una solicitud HTTP GET pasar Hola identificador de IngestManifest.

## <a name="create-contentkeys-used-for-encryption"></a>Creación de ContentKeys para el cifrado
Si el recurso usa cifrado, debe crear hello ContentKey toobe usado para el cifrado antes de crear archivos de recursos de Hola. Para el cifrado de almacenamiento, hello siguientes propiedades se deben incluir en el cuerpo de la solicitud de saludo.

| Propiedad del cuerpo de la solicitud | Description |
| --- | --- |
| Id |Hello identificador de ContentKey que generamos desarrollamos con hello después de dar formato, "NB:<NEW GUID>". |
| ContentKeyType |Este es el tipo de clave contenido de Hola como un número entero para esta clave de contenido. Pasamos el valor de hello 1 para el cifrado de almacenamiento. |
| EncryptedContentKey |Creamos un valor de clave de contenido que es un valor de 256 bits (32 bytes). clave de Hola se cifra mediante el certificado X.509 de cifrado de almacenamiento de Hola que recuperamos de servicios multimedia de Microsoft Azure mediante la ejecución de una solicitud HTTP GET hello GetProtectionKeyId y GetProtectionKey métodos. |
| ProtectionKeyId |Esto es Hola Id. de clave de protección para el certificado X.509 de cifrado de almacenamiento de Hola que estaba tooencrypt usa la clave de contenido. |
| ProtectionKeyType |Se trata de un tipo de cifrado de hello para la clave de protección de Hola que fue utilizado tooencrypt Hola contenido clave. Este valor es StorageEncryption(1) en nuestro ejemplo. |
| Checksum |Hola MD5 suma de comprobación calculada Hola clave de contenido. Se calcula mediante el cifrado de contenido de hello identificador con clave de contenido de Hola. código de ejemplo de Hola muestra cómo toocalculate Hola suma de comprobación. |

**Respuesta HTTP**

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

### <a name="link-hello-contentkey-toohello-asset"></a>Vincular hello ContentKey toohello activo
Hola ContentKey es tooone asociado o más activos mediante el envío de una solicitud HTTP POST. Hello solicitud siguiente es un recurso en el ejemplo se toolink Hola ejemplo ContentKey toohello ejemplo por identificador.

**Respuesta HTTP**

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

**Respuesta HTTP**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>Pasos siguientes

Ahora puede codificar los recursos cargados. Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).

También puede utilizar las funciones de Azure tootrigger un trabajo de codificación basado en un archivo que llegan en el contenedor de hello configurado. Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

