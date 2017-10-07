---
title: "aaaHow tooencode un recurso de Azure mediante el uso de medios codificador estándar | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Media Encoder estándar tooencode medios de contenido en servicios multimedia de Azure. Los ejemplos de código usan la API de REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>¿Cómo tooencode un activo mediante el uso de medios codificador estándar
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Información general
toodeliver vídeo digital a través de Internet de hello, debe comprimir medios Hola. Archivos de vídeo digital son grandes y pueden ser demasiado grande toodeliver a través de Internet de hello, o para toodisplay de dispositivos de los clientes correctamente. La codificación es el proceso de Hola de compresión de vídeo y audio para que los clientes puedan ver los medios.

Trabajos de codificación son una de las operaciones de procesamiento más habituales de hello en los servicios de multimedia de Azure. Crear archivos multimedia de codificación trabajos tooconvert desde una tooanother de codificación. Al codificar, puede usar (estándar de codificador multimedia) de codificador integrado de servicios multimedia de Hola. También puede usar un codificador proporcionado por un partner de Media Services. Codificadores de terceros están disponibles a través de hello Azure Marketplace. Puede especificar detalles de Hola de tareas de codificación mediante cadenas de valores preestablecidos definidas para el codificador o mediante el uso de archivos de configuración de valores predefinidos. toosee Hola tipos de valores predefinidos que están disponibles, consulte [valores preestablecidos de tarea para Media Encoder estándar](http://msdn.microsoft.com/library/mt269960).

Cada trabajo puede tener uno o más tareas según el tipo de saludo de procesamiento que desea tooaccomplish. A través de la API de REST de hello, puede crear trabajos y sus tareas relacionadas en una de dos maneras:

* Las tareas pueden definir en línea a través de la propiedad de navegación de las tareas de hello en entidades de trabajos.
* Uso del procesamiento por lotes de OData.

Se recomienda codificar siempre los archivos de origen en un conjunto de MP4 de velocidad de bits adaptativa y, a continuación, convertir el formato deseado de hello conjunto toohello mediante [empaquetado dinámico](media-services-dynamic-packaging-overview.md).

Si su recurso de salida es el almacenamiento de cifrado, debe configurar la directiva de entrega del activo de Hola. Para obtener más información, consulte [Configuración de directivas de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Consideraciones

Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP. Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).

Antes de iniciar que hacen referencia a procesadores multimedia, compruebe que haya Hola Id. de procesador de medios correctos. Para obtener más información, consulte [Obtención de procesadores multimedia](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Conectar servicios de tooMedia

Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Creación de un trabajo con una sola tarea de codificación
> [!NOTE]
> Cuando se trabaja con API de REST de servicios multimedia de hello, hello siguientes consideraciones:
>
> Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP. Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Media Services](media-services-rest-how-to-use.md).
>
> Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI. Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).
>
> Cuando usa JSON y especifica toouse hello **__metadata** palabra clave en la solicitud de hello (por ejemplo, tooreferences un objeto vinculado), debe establecer hello **Accept** encabezado demasiado[formato JSON detallado ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Aceptar: application/json; odata = detallado.
>
>

Hola de ejemplo siguiente muestra cómo toocreate y post un trabajo con una tarea establece tooencode un vídeo en una resolución y calidad específicas. Al codificar con Media Encoder Standard, puede usar los valores preestablecidos de configuración de tareas especificados [aquí](http://msdn.microsoft.com/library/mt269960).

Solicitud:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Respuesta:

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Establece el nombre del recurso de salida de hello
Hola de ejemplo siguiente muestra cómo tooset Hola atributo assetName:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Consideraciones
* Propiedades TaskBody deben usar el número de hello literal de toodefine XML de entrada o recursos de salida que se usan por tarea hello. tema de la tarea Hello contiene Hola definición de esquemas XML para hello XML.
* Hola definición TaskBody, cada interna valor <inputAsset> y <outputAsset> debe establecerse como JobInputAsset(value) o JobOutputAsset(value).
* Una tarea puede tener varios recursos de salida. Un elemento JobOutputAsset(x) solo se puede usar una vez como salida de una tarea en un trabajo.
* Puede especificar JobInputAsset o JobOutputAsset como un recurso de entrada de una tarea.
* Las tareas no pueden formar un ciclo.
* valor del parámetro Hello que pasar tooJobInputAsset o JobOutputAsset representa el valor de índice de Hola para un activo. recursos reales de Hola se definen en hello InputMediaAssets y OutputMediaAssets propiedades de navegación en la definición de la entidad de hello trabajo.
* Dado que los servicios multimedia se fundamentan en OData v3, Hola activos individuales en hello InputMediaAssets y OutputMediaAssets colecciones de propiedades de navegación se hace referencia a través de un "__metadata: uri" par nombre / valor.
* InputMediaAssets asigna tooone o más activos que creó en los servicios multimedia. Sistema de hello crea los OutputMediaAssets. Estos no hacen referencia a ningún recurso existente.
* Los OutputMediaAssets puede llamarse mediante hello assetName atributo. Si este atributo no está presente, el nombre de Hola de hello OutputMediaAsset es cualquier valor de texto interno de Hola de hello <outputAsset> elemento es con un sufijo de valor de nombre del trabajo de Hola o valor de Id. de trabajo de hello (en caso de hello donde no se ha definido la propiedad de nombre de hello). Por ejemplo, si establece un valor para assetName demasiado "Sample" y, a continuación, Hola nombre OutputMediaAsset se establece la propiedad demasiado "Sample." Sin embargo, si no ha configurado un valor para assetName, pero ha especificado el nombre del trabajo Hola demasiado "como NewJob" y, a continuación, Hola nombre OutputMediaAsset sería "JobOutputAsset (valor) _NewJob".

## <a name="create-a-job-with-chained-tasks"></a>Creación de un trabajo con tareas encadenadas
En muchos escenarios de aplicación, los desarrolladores desean toocreate una serie de tareas de procesamiento. En Servicios multimedia, puede crear una serie de tareas encadenadas. Cada tarea realiza distintos pasos de procesamiento diferentes y puede usar diferentes procesadores multimedia. tareas de Hello encadenada pueden entregar un activo de una tarea tooanother, realizar una secuencia lineal de tareas en activos de Hola. Sin embargo, las tareas de hello realizadas en un trabajo no son toobe necesario en una secuencia. Cuando se crea una tarea encadenada, Hola encadenadas **ITask** objetos se crean en un único **IJob** objeto.

> [!NOTE]
> Actualmente hay un límite de 30 tareas por trabajo. Si necesita más de 30 tareas toochain, cree más de un trabajo de tareas de Hola de toocontain.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Consideraciones
tooenable encadenamiento de tareas:

* Un trabajo debe tener al menos dos tareas.
* Debe haber al menos una tarea cuya entrada sea salida de hello de otra tarea en el trabajo de Hola.

## <a name="use-odata-batch-processing"></a>Uso del procesamiento por lotes de OData
Hola de ejemplo siguiente muestra cómo toouse OData por lotes las toocreate de procesamiento de un trabajo y tareas. Para obtener información sobre el procesamiento por lotes, consulte [Procesamiento por lotes del protocolo Open Data (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Creación de un trabajo mediante una plantilla JobTemplate
Cuando se procesan varios recursos mediante el uso de un conjunto común de tareas, utilice que una tarea de forma predeterminada de JobTemplate toospecify Hola presintonías u orden de hello tooset de tareas.

Hola siguiente ejemplo muestra cómo toocreate una JobTemplate con una TaskTemplate que está había definido en línea. Hola TaskTemplate usa Hola Media Encoder estándar como archivo de recursos de hello MediaProcessor tooencode Hola. Sin embargo, también se pueden usar otros elementos MediaProcessor.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> A diferencia de otras entidades de servicios multimedia, debe definir un nuevo identificador GUID para cada TaskTemplate y colocarlo en taskTemplateId de Hola y la propiedad Id en el cuerpo de la solicitud. esquema de identificación de contenido de Hello debe seguir el esquema de hello descrito en identificar las entidades de servicios de multimedia de Azure. Además, las plantillas de trabajo no se pueden actualizar. Por el contrario, debe crear una nueva con los cambios actualizados.
>
>

Si se realiza correctamente, se devuelve Hola después de respuesta:

    HTTP/1.1 201 Created

    . . .


Hola siguiente ejemplo se muestra cómo toocreate un trabajo que hace referencia a un identificador de JobTemplate:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


Si se realiza correctamente, se devuelve Hola después de respuesta:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe cómo toocreate una tooencode trabajo un activo, consulte [cómo toocheck trabajo progreso con servicios multimedia](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Otras referencias
[Obtención de una instancia de procesador multimedia](media-services-rest-get-media-processor.md)
