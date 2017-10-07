---
title: "aaaMedia análisis en la plataforma de servicios multimedia de hello | Documentos de Microsoft"
description: "Información general sobre la versión preliminar pública de Análisis multimedia, una colección de servicios de voz y visión informática a escala empresarial, cumplimiento, seguridad y alcance global"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Análisis de multimedia en la plataforma de servicios multimedia de Hola
## <a name="overview"></a>Información general
Las organizaciones más están utilizando vídeo como Hola preferido tootrain intermedio sus empleados, captar sus clientes y las funciones de negocio de documento. Proporciona una manera toostore, la informática en nube transmitir por secuencias y tener acceso a estos archivos multimedia de gran tamaño. Pero a medida que crece la biblioteca de la compañía de contenido de vídeo, necesita un medio igualmente eficaz de extraer información de contenido de Hola. 

tooaddress esta necesidad creciente, servicios multimedia de Azure ofrece análisis de multimedia de Azure. Análisis multimedia es una colección de componentes de voz y visión que resulta más fácil para las organizaciones y empresas información procesable tooderive de sus archivos de vídeo. Creado mediante el uso de componentes de la plataforma de servicios multimedia de hello core, análisis multimedia puede controlar a escala en el primer día de procesamiento de medios.

Con Análisis multimedia, los desarrolladores pueden integrar funcionalidad de vídeo avanzada en las aplicaciones rápidamente. Proporciona entornos empresariales con escala completa hello, cumplimiento, seguridad y alcance global requerido las grandes organizaciones.

Hello siguiente diagrama muestra análisis multimedia y otros componentes principales de la plataforma de servicios multimedia de Hola. 

![Flujo de trabajo de VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

Los procesadores multimedia de Análisis multimedia generan archivos MP4 o JSON. Si un procesador multimedia genera un archivo MP4, puede descargar progresivamente archivo hello. Si un procesador multimedia genera un archivo JSON, puede descargar el archivo hello desde el almacenamiento de blobs de Azure. 

## <a name="media-analytics-services"></a>Servicios de Análisis multimedia

### <a name="indexer"></a>Indexer
Con Azure Media Indexer puede realizar búsquedas en el contenido, así como generar pistas de subtítulos. La versión anterior de toohello comparados, vista previa de Azure Media Indexer 2 es indización rápida y más amplia de lenguaje compatible con. Los idiomas compatibles son alemán, árabe, chino, español, francés, inglés, italiano y portugués. Para obtener información detallada y ejemplos, vea [Process videos with Azure Media Indexer 2 (Procesar vídeos con Azure Media Indexer 2)](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse combina estabilización del vídeo y capacidad lapso de tiempo toocreate rápido, puede usar vídeos desde el contenido de formato largo. Además de la creación de vídeo de lapso de tiempo, puede usar Hyperlapse toocreate estables vídeos de vídeos cambiante de captura a través de teléfonos y cámaras de vídeo. Para obtener información detallada y ejemplos, vea [Archivos multimedia de Hyperlapse con Azure Media Hyperlapse](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Detector de movimientos
Puede usar el movimiento de toodetect Detector de movimiento en un vídeo con fondos estacionarios. Esto hace posible toocheck de falsos positivos en eventos de movimiento detectados por las cámaras de vigilancia. Para obtener información detallada y ejemplos, vea [Motion Detection for Azure Media Analytics (Detección de movimiento para Análisis multimedia de Azure)](media-services-motion-detection.md).
### <a name="face-detector"></a>Detector de caras
Con Face Detector puede detectar las caras y las emociones de las personas, lo que incluye felicidad, tristeza y sorpresa. Esto tiene varias aplicaciones útiles para el sector, que se describen más adelante, como la adición y el análisis de reacciones de personas que asisten a un evento. Para obtener información detallada y ejemplos, vea [Face and Emotion Detection for Azure Media Analytics (Detección de caras y emociones para Análisis multimedia de Azure)](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Resumen de vídeo
Resumen de vídeo puede ayudar a crear resúmenes de los vídeos largos seleccionando automáticamente interesantes fragmentos de vídeo de origen de Hola. Esta capacidad es útil cuando se desea una introducción rápida de qué tooexpect en un vídeo largo tooprovide. Para obtener información detallada y ejemplos, vea [resumen vídeo de miniaturas de vídeo de multimedia de Azure de uso toocreate](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Reconocimiento óptico de caracteres
Con Azure Media OCR (reconocimiento óptico de caracteres), puede convertir el contenido de texto de archivos de vídeo en texto digital modificable y utilizable en búsquedas. A continuación, puede automatizar extracción Hola de metadatos significativo de señal de vídeo de Hola de los medios.
### <a name="scalable-face-redaction"></a>Censura de rostros escalable
Redactor de multimedia de Azure es un procesador de multimedia de análisis multimedia que ofrece la redacción de cara escalable en la nube de Hola. Mediante el uso de redacción de cara, puede modificar sus caras tooblur vídeo de los usuarios seleccionados. Puede ser conveniente servicio de redacción de cara de toouse hello en los medios de noticias o cuando está implicada seguridad pública. Unos pocos minutos después de material de archivo que contiene varios tipos pueden tardar horas tooredact manualmente, pero con este servicio, redacción de cara tarda unos pocos pasos sencillos. Para obtener más información, vea hello [censurar caras con análisis de multimedia de Azure](media-services-face-redaction.md) artículo.

## <a name="common-scenarios"></a>Escenarios comunes
Análisis multimedia puede ayudar a las organizaciones y empresas a recopilar nuevos datos relevantes a partir del vídeo y a administrar más eficazmente grandes volúmenes de contenido de vídeo. Estos son algunos escenarios:

* **Centros de atención al cliente**. Incluso con la llegada de Hola de redes sociales, centros de llamadas de cliente todavía facilitan un porcentaje elevado de transacciones de servicio al cliente. Codificados en estos datos de audio es una gran cantidad de información del cliente que se pueden analiza tooachieve mayor satisfacción del cliente. Con Media Indexer, las organizaciones pueden extraer texto y crear índices y paneles de búsqueda. Luego pueden extraer inteligencia de las quejas habituales, los orígenes de las quejas y otros datos relevantes.
* **Moderación de contenido generado por el usuario**. De departamentos de toopolice de distribuidores de medios de noticias, muchas organizaciones tienen portales de acceso público que aceptan multimedia generado por el usuario, como imágenes y vídeos. volumen de Hola de contenido puede tener picos debido toounexpected eventos. En estos casos, resulta difícil tooconduct las revisiones del manual efectiva del contenido de idoneidad. Los clientes pueden basarse en hello toofocus de servicio de moderación de contenido en el contenido que es adecuado.
* **Vigilancia**. Hola crecimiento del uso de cámaras IP conlleva un inventario creciente de vídeo de vigilancia. Revisar manualmente vídeo vigilancia es toohuman intensivo y propensa a errores en tiempo de. Análisis multimedia proporciona servicios como la detección de movimiento y detección de cara, proceso de Hyperlapse toomake Hola de revisar, administrar y crear los derivados más fácil.

## <a name="media-analytics-media-processors"></a>Procesadores de multimedia de Análisis multimedia
Esta sección procesadores de multimedia de listas Hola análisis multimedia y muestra cómo toouse .NET o REST tooget un objeto de procesador (MP) de medios.

### <a name="mp-names"></a>Nombres de MP
* Azure Media Indexer 2 Preview
* Azure Media Indexer
* Azure Media Hyperlapse
* Azure Media Face Detector
* Azure Media Motion Detector
* Azure Media Video Thumbnails
* Azure Media OCR

### <a name="net"></a>.NET
Hola después de la función toma uno del programa Hola a especifica nombres de módulo de administración y devuelve un objeto de módulo de administración.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
Solicitud:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Respuesta:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Demostraciones
Vea [Demostraciones de Análisis multimedia de Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artículos relacionados
Vea [Media Services Analytics announcement (Anuncio de análisis de Media Services)](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
