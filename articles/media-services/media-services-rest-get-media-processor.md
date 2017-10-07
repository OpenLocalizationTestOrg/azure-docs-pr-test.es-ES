---
title: "aaa cómo tooget una instancia de procesador multimedia mediante REST | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un tooencode de componente del procesador de multimedia, convertir el formato, cifrar o descifrar contenido multimedia para servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a>¿Cómo tooget una instancia de procesador multimedia
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Información general
En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia. Suele crear un procesador multimedia cuando se crea una tarea tooencode, cifrar o convertir el formato de saludo del contenido multimedia.

## <a name="azure-media-processors"></a>Procesadores de multimedia de Azure 

Hola tema siguiente proporciona listas de procesadores multimedia:

* [Codificación de procesadores de multimedia](scenarios-and-availability.md#encoding-media-processors)
* [Procesadores de multimedia de Analytics](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
>Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP. Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Conectar servicios de tooMedia

Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI.

## <a name="get-a-media-processor"></a>Obtención de un procesador multimedia

Hola después de la llamada de REST, muestra cómo tooget un procesador multimedia instancia por su nombre (en este caso, **Media Encoder estándar**). 

Solicitud:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

Respuesta:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
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


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe cómo tooget una instancia de procesador multimedia, vaya toohello [cómo tooEncode un activo](media-services-rest-get-started.md) tema que le mostrará cómo toouse Hola tooencode Media Encoder estándar a un recurso.

