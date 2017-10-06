---
title: "códigos de error de codificación de servicios multimedia aaaAzure | Documentos de Microsoft"
description: "Este tema enumeran los códigos de error que se pueden devolver en caso de que se detectó un error durante la ejecución de la tarea de codificación de Hola..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a>Códigos de error de Encoding

Hello tabla siguiente enumeran los códigos de error que se pueden devolver en caso de que se detectó un error durante la ejecución de la tarea de codificación de Hola.  tooget detalles del error en el código. NET, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) clase. tooget detalles del error en el código REST, usar hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API de REST.

| ErrorDetail.Code | Posibles causas de error |
| --- | --- |
| Desconocido |Error desconocido al ejecutar la tarea hello |
| ErrorDownloadingInputAssetMalformedContent |Categoría de errores en la que se incluyen errores en la descarga de recursos de entrada, como nombres de archivo no válidos, archivos de longitud cero, formatos incorrectos, etc. |
| ErrorDownloadingInputAssetServiceFailure |Categoría de errores que se trata problemas en lado de servicio de hello - errores de red o almacenamiento de ejemplo mientras se descargaba. |
| ErrorParsingConfiguration |Categoría de errores donde tarea <see cref="MediaTask.PrivateData"/> (configuración) no es válida, por ejemplo Hola configuración no es un sistema válido preestablecido o contiene un XML no válido. |
| ErrorExecutingTaskMalformedContent |Categoría de errores durante la ejecución de Hola de tarea hello donde problemas dentro de hello entrada archivos multimedia provocan un error. |
| ErrorExecutingTaskUnsupportedFormat |Categoría de errores donde procesador de multimedia de hello no puede procesar archivos Hola proporcionados: media de formato no compatible o no coincide con la configuración de Hola. Por ejemplo, al tratar de tooproduce una salida de solo audio desde un recurso que tiene solo vídeo |
| ErrorProcessingTask |Categoría de otros errores que Hola procesador multimedia se encuentra durante el procesamiento de Hola de tarea de Hola que están relacionados con toocontent. |
| ErrorUploadingOutputAsset |Categoría de errores al cargar el recurso de salida de hello |
| ErrorCancelingTask |Categoría de errores de toocover de errores al intentar toocancel Hola tarea |
| TransientError |Categoría de errores toocover problemas transitorios (p. ej. ej., problemas de red temporales con Almacenamiento de Azure). |

Ayuda de tooget de hello **servicios multimedia** equipo, abra un [incidencia de soporte técnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artículos relacionados
* [Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar](media-services-custom-mes-presets-with-dotnet.md)
* [Cuotas y limitaciones](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
