---
title: "aaaAzure servicios multimedia de preguntas más frecuentes | Documentos de Microsoft"
description: "Preguntas más frecuentes (P+F)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Preguntas más frecuentes

Este artículo tratan las preguntas más frecuentes generadas por la Comunidad de usuarios de servicios de multimedia de Azure (AMS) Hola.

## <a name="general-ams-faqs"></a>Preguntas más frecuentes generales sobre AMS
P: ¿Cómo se escala la indización?

R: unidades de hello reservado se Hola mismo para la codificación y tareas de indización. Siga las instrucciones de [cómo unidades reservadas de codificación tooScale](media-services-scale-media-processing-overview.md). **Tenga en cuenta** que el rendimiento del indexador no se ve afectado por el tipo de unidad reservada.

P: He cargado, codificado y publicado un vídeo. ¿Lo que sería un vídeo de Hola de hello motivo no se reproduce cuando intento toostream él?

R: uno de hello más comunes motivos por los que es no tener Hola origen desde el que está tratando de tooplayback Hola **ejecutando** estado.  

P: ¿Puedo realizar una composición en una secuencia en directo?

R: la composición en secuencias en directo no proporciona actualmente en los servicios de multimedia de Azure, lo que deberá toopre-crear en el equipo.

P: ¿Puedo usar CDN de Azure con secuencia en directo?

R: servicios multimedia de admite la integración con la red CDN de Azure (para obtener más información, consulte [cómo tooManage los extremos de Streaming en una cuenta de servicios multimedia](media-services-portal-manage-streaming-endpoints.md)).  Puede usar el streaming en vivo con CDN. Servicios multimedia de Azure proporciona salidas de Smooth Streaming, HLS y MPEG-DASH. Todos estos formatos usan HTTP para transferir datos y obtener beneficios del almacenamiento en caché de HTTP. En directo de datos reales de audio/vídeo de transmisión por secuencias es toofragments dividido y se almacene en caché este fragmentos individuales en la red CDN. Solo los toobe de necesidades datos actualizados es datos de manifiesto de saludo. CDN actualiza periódicamente los datos de manifiesto.

P: ¿Los servicios multimedia de Azure admiten el almacenamiento de imágenes?

R: si solo desea toostore JPEG o imágenes PNG, debe mantenerlos de almacenamiento de blobs de Azure. No hay ningún tooputting de beneficio en los servicios multimedia de la cuenta a menos que desee tookeep que ellos asociados con el vídeo o Audio activos. O bien, si es posible que tenga una necesidad toouse hello las imágenes como superposiciones de codificador de vídeo de Hola. Media Encoder estándar es compatible con imágenes de capas en la parte superior vídeos, y que es lo que muestra JPEG y PNG como admiten formatos de entrada. Para obtener más información, consulte [Creación de superposiciones](media-services-advanced-encoding-with-mes.md#overlay).

P: ¿Cómo puedo copiar activos de una tooanother de cuenta de servicios multimedia.

R: toocopy activos de una tooanother de cuenta de servicios multimedia con. NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) método de extensión disponible en hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repositorio. Para obtener más información, consulte [esta](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) conversación del foro.

P: ¿Cuáles son Hola admite caracteres para asignar nombres a archivos cuando se trabaja con AMS?

R: servicios multimedia de usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual. Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Además, solo puede haber un "." para la extensión de nombre de archivo de Hola.

P: ¿cómo uso tooconnect REST?

R: para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI. 

P: ¿¿Cómo puedo girar un vídeo durante el proceso de codificación de Hola.

R: Hola [Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md) admite la rotación de ángulos de 90, 180 y 270. comportamiento predeterminado de Hello es "Auto", donde intenta toodetect Hola rotación metadatos en el archivo MP4/.mov entrante de Hola y compensar para él. Hola siguientes **orígenes** tooone de elemento de valores preestablecidos de json de hello definido [aquí](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
