---
title: aaaAnalyze los medios que utilizan Hola portal de Azure | Documentos de Microsoft
description: "Este tema se describe cómo tooprocess multimedia con procesadores de multimedia de análisis multimedia (MP) mediante Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analizar el contenido multimedia mediante Hola portal de Azure
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Información general
Análisis de servicios multimedia de Azure es una colección de componentes de voz y visión (en escala empresarial, cumplimiento de normas, seguridad y alcance global) que resulte más fácil para las organizaciones y empresas información procesable tooderive de sus archivos de vídeo. Para obtener información más detallada de Análisis de Azure Media Services, consulte [este](media-services-analytics-overview.md) tema. 

Este tema se describe cómo tooprocess multimedia con procesadores de multimedia de análisis multimedia (MP) mediante Hola portal de Azure. Los procesadores de multimedia de Análisis multimedia generan archivos MP4 o JSON. Si un procesador multimedia genera un archivo MP4, puede descargar progresivamente archivo hello. Si un procesador multimedia genera un archivo JSON, puede descargar el archivo hello de hello almacenamiento de blobs de Azure. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Elija un recurso que desea tooanalyze
1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Hola **configuración** ventana, seleccione **activos**.  
   .
    ![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Activos de hello SELECT que le gustaría hello tooanalyze y presione **analizar** botón.
   
    ![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. Hola **activo multimedia de proceso con análisis multimedia** (ventana), el procesador de hello seleccione. 
   
    resto de Hello del artículo de hello explica por qué y cómo toouse cada procesador. 
5. Presione **crear** toohello iniciar un trabajo.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Hola **Azure Media Indexer** procesador multimedia permite toomake los archivos multimedia y contenido para la búsqueda, así como generar pistas de subtítulos. En esta sección se proporcionan algunos detalles sobre las opciones que puede especificar para este MP.

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>language
Hola toobe de lenguaje natural que se reconocen en el archivo multimedia de hello. Por ejemplo, inglés o español. 

### <a name="captions"></a>Subtítulos
Puede elegir un formato de subtitulado que se generará a partir del contenido. Un trabajo de indización puede generar archivos de subtítulos de hello siguientes formatos:  

* **SAMI**
* **TTML**
* **WebVTT**

Archivos cerrados de subtítulos (CC) en estos formatos pueden ser usado toomake audio y archivos de vídeo toopeople accesible con discapacidades auditivas.

### <a name="aib-file"></a>Archivo AIB
Seleccione esta opción si se como archivo de Blob de índice de Audio de hello toogenerate para su uso con el Hola IFilter personalizada de servidor de SQL. Para más información, consulte [este blog](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) .

### <a name="keywords"></a>Palabras clave
Seleccione esta opción si desea que toogenerate un archivo XML de palabras clave. Este archivo contiene palabras clave extraídas de contenidos de hello orales, con frecuencia y la información de desplazamiento.

### <a name="job-name"></a>Nombre del trabajo
Un nombre descriptivo que le permite identificar el trabajo de Hola. [Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo. 

### <a name="output-file"></a>Archivo de salida
Un nombre descriptivo que le permite identificar el contenido de la salida de hello. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse es un MP que crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción.  Para obtener más información, consulte [este tema](media-services-hyperlapse-content.md) . En esta sección se proporcionan algunos detalles sobre las opciones que puede especificar para este MP.

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Velocidad
Especifica la velocidad de hello con qué toospeed el vídeo de entrada de Hola. salida de Hello es una copia estabilizar y vencido de tiempo del vídeo de entrada de Hola.

### <a name="job-name"></a>Nombre del trabajo
Un nombre descriptivo que le permite identificar el trabajo de Hola. [Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo. 

### <a name="output-file"></a>Archivo de salida
Un nombre descriptivo que le permite identificar el contenido de la salida de hello. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
Hola **Detector de caras de multimedia de Azure** procesador multimedia (MP) le permite toocount, movimientos de seguimiento y participación de la audiencia de medidor incluso y reacción a través de expresiones faciales. Este servicio contiene dos características: 

* **Detección de caras**
  
    La detección de caras busca y realiza el seguimiento de caras humanas dentro de un vídeo. Varias caras pueden detectarse y posteriormente se realiza el seguimiento de medida que se mueven, con metadatos de tiempo y la ubicación de hello devueltos en un archivo JSON. Durante el seguimiento, tratará de toogive un toohello identificador coherente mismo enfrentan mientras está moviendo persona Hola en pantalla, incluso si se puede ver obstruidos o brevemente deje marco Hola.
  
  > [!NOTE]
  > Este servicio no lleva a cabo el reconocimiento facial. Una persona que sale del marco de Hola o deja de estar obstruida para demasiado larga se le asignará un nuevo identificador cuando devuelven.
  > 
  > 
* **Detección de emociones**
  
    Detección de emoción es un componente opcional de hello procesador de multimedia de detección de cara que devuelve el análisis en varios atributos emoción de caras de hello detectados, incluida la satisfacción, tristeza, temor, ira y mucho más. 

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Modo de detección
Uno de los siguientes modos de hello puede usarse por procesador hello:

* Detección de caras
* Detección de emociones por cara
* Detección de emociones agregadas

### <a name="job-name"></a>Nombre del trabajo
Un nombre descriptivo que le permite identificar el trabajo de Hola. [Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo. 

### <a name="output-file"></a>Archivo de salida
Un nombre descriptivo que le permite identificar el contenido de la salida de hello. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
Hola **Detector de movimiento de multimedia de Azure** habilita el procesador (MP) media tooefficiently se identifican las secciones de interés dentro de un vídeo largo y sin incidentes en caso contrario. Detección de movimiento puede usarse en secciones de tooidentify grabaciones de cámaras estáticas de vídeo de Hola donde se produce un movimiento. Genera un archivo JSON que contiene un metadatos con hello límite región donde se produjo el evento de Hola y marcas de tiempo.

Destinado fuentes de vídeo de seguridad, esta tecnología es capaz de toocategorize movimiento en los eventos relevantes y falsos positivos, como los cambios de iluminación y sombras. Esto permite toogenerate alertas de seguridad de las fuentes de cámara sin que se va a spam con eventos irrelevantes infinitos, al que se va a momentos tooextract capaz de interés de vídeos de vigilancia muy largos.

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Este procesador puede ayudarle a crear resúmenes de los vídeos largos seleccionando automáticamente interesantes fragmentos de vídeo de origen de Hola. Esto es útil cuando se desea una introducción rápida de qué tooexpect en un vídeo largo tooprovide. Para obtener información detallada y ejemplos, vea [tooCreate de miniaturas de vídeo de multimedia de Azure Use un resumen de vídeo](media-services-video-summarization.md)

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Nombre del trabajo
Un nombre descriptivo que le permite identificar el trabajo de Hola. [Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo. 

### <a name="output-file"></a>Archivo de salida
Un nombre descriptivo que le permite identificar el contenido de la salida de hello. 

## <a name="next-steps"></a>Pasos siguientes
Ver las rutas de aprendizaje de Media Services

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

