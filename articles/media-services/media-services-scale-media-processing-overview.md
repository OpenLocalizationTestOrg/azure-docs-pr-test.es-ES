---
title: "información general sobre el procesamiento de medios de aaaScaling | Documentos de Microsoft"
description: "Este tema ofrece una introducción al escalado de procesamiento de medios con on Servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Información general del escalado de procesamiento de medios
Esta página proporciona una visión general de cómo y por qué el procesamiento de medios tooscale. 

## <a name="overview"></a>Información general
Una cuenta de servicios multimedia está asociada a un tipo de unidad reservada, que determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento. Puede elegir entre como consecuencia de hello reservado los tipos de unidad: **S1**, **S2**, o **S3**. Por ejemplo, hello mismo trabajo de codificación se ejecuta con mayor rapidez cuando se usa hello **S2** tipo de unidad reservada comparar toohello **S1** tipo. Para obtener más información, vea hello [tipos de unidad reservada](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Además toospecifying Hola había reservado del tipo de unidad, se puede especificar tooprovision su cuenta con unidades reservadas. número de Hola de unidades reservadas aprovisionadas determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada. Por ejemplo, si su cuenta tiene cinco unidades reservadas, se ejecutarán simultáneamente siempre y tareas de cinco medios como hay toobe de tareas que se procesan. las tareas restantes de Hello esperarán en cola de Hola y se procesarán de manera secuencial cuando finaliza una tarea en ejecución. Si una cuenta no tiene ninguna unidad reservada aprovisionada, las tareas se elegirán de manera secuencial. En este caso, Hola de tiempo entre la finalización de una tarea de espera y hello siguiente que empieza dependerá disponibilidad Hola de recursos de sistema de Hola.

## <a name="choosing-between-different-reserved-unit-types"></a>Selección de los distintos tipos de unidad reservada
Hello en la tabla siguiente le ayuda a tomar la decisión al elegir entre distintas velocidades de codificación. También proporciona algunos casos de prueba comparativa y proporciona las direcciones URL de SAS puede usar vídeos toodownload en el que puede realizar sus propias pruebas:

| Escenarios | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Caso de uso previsto |Codificación con velocidad de bits sencilla. <br/>Archivos con resolución SD o menor, no sujetos a limitación temporal y de bajo costo. |Codificación con velocidad de bits sencilla y múltiple.<br/>Uso normal para codificación SD y HD. |Codificación con velocidad de bits sencilla y múltiple.<br/>Vídeos con resolución Full HD y 4K. Codificación con respuesta más rápida, sujeta a limitación temporal. |
| Prueba comparativa |[Archivo de entrada: 5 minutos de duración, 640 x 360 p a 29,97 fotogramas/segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Codificación de archivos MP4 de velocidad de bits única de tooa, en hello misma resolución tarda aproximadamente 11 minutos. |[Archivo de entrada: 5 minutos de duración, 1280 x 720 p a 29,97 fotogramas/segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>La codificación con el valor predeterminado H264 Single Bitrate 720p tardará aproximadamente 5 minutos.<br/><br/>La codificación con el valor predeterminado H264 Multiple Bitrate 720p tardará aproximadamente 11,5 minutos. |[Archivo de entrada: 5 minutos de duración, 1920 x 1080 p a 29,97 fotogramas/segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>La codificación con el valor predeterminado H264 Single Bitrate 1080p tardará aproximadamente 2,7 minutos.<br/><br/>La codificación con el valor predeterminado "H264 Multiple Bitrate 1080p" tarda aproximadamente 5,7 minutos. |

## <a name="considerations"></a>Consideraciones
> [!IMPORTANT]
> Revise las consideraciones descritas en esta sección.  
> 
> 

* Las unidades reservadas sirven para establecer paralelismos en todo el procesamiento multimedia, incluida la indexación de trabajos mediante Azure Media Indexer.  Sin embargo, a diferencia de la codificación, la indexación de los trabajos no se procesará más rápido con unidades reservadas de mayor rapidez.
* Si usa Hola compartido grupo, es decir, sin ninguna unidades reservadas, a continuación, tiene la tarea de codificación Hola mismo rendimiento al igual que con RUs S1. Sin embargo, no hay ningún tiempo de toohello de límite superior que pueden dedicar sus tareas en estado en cola, y en cualquier momento dado, se ejecutará a lo sumo una tarea.
* Hola después de centros de datos no ofrece hello **S2** reservado del tipo de unidad: sur de Brasil y India occidental.
* Hello siguientes del centro de datos no ofrecen hello **S3** reservado del tipo de unidad: India occidental.

## <a name="billing"></a>Facturación

Se le cobrará en función de los minutos reales de uso de las unidades reservadas de multimedia. Para obtener una explicación detallada, consulte sección Hola preguntas más frecuentes de hello [precios de servicios multimedia](https://azure.microsoft.com/pricing/details/media-services/) página.   

## <a name="quotas-and-limitations"></a>Cuotas y limitaciones
Para obtener información sobre cuotas y límites y cómo tooopen una incidencia de soporte técnico, consulte [cuotas y limitaciones](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Paso siguiente
Lograr Hola ajuste de escala en medio de procesamiento de la tarea con una de estas tecnologías: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

