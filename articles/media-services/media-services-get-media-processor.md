---
title: tooCreate aaaHow un procesador de medios mediante Hola SDK de servicios multimedia de Azure para .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un tooencode de componente del procesador de multimedia, convertir el formato, cifrar o descifrar contenido multimedia para servicios multimedia de Azure. Ejemplos de código están escritos en C# y usar hello SDK de servicios multimedia para. NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>Obtención de una instancia de procesador multimedia
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

## <a name="get-media-processor"></a>Obtención de un procesador multimedia

Hola siguiendo el método muestra cómo tooget una instancia de procesador de multimedia. ejemplo de código de Hello supone el uso de Hola de una variable de nivel de módulo con el nombre **_contexto** tooreference contexto de servidor hello tal y como se describe en la sección de hello [Cómo: conectar servicios mediante programación tooMedia](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe cómo tooget una instancia de procesador multimedia, vaya toohello [cómo tooEncode un activo](media-services-dotnet-encode-with-media-encoder-standard.md) tema que le mostrará cómo toouse Hola tooencode Media Encoder estándar a un recurso.

