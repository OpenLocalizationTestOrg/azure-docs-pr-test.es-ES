---
title: "aaaOverview y comparación de Azure en exigen codificadores multimedia | Documentos de Microsoft"
description: "En este tema se proporciona información general y una comparación de los codificadores multimedia a petición de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Información general y comparación de codificadores multimedia a petición de Azure
## <a name="encoding-overview"></a>Información general sobre la codificación
Servicios multimedia de Azure proporciona varias opciones para la codificación de Hola de medios en la nube de Hola.

Al iniciar la con los servicios multimedia, es importante toounderstand Hola diferencia entre códecs y formatos de archivo.
Los códecs son software Hola que implementa los algoritmos de compresión y descompresión de hello, mientras que los formatos de archivo son contenedores que alojan el vídeo comprimido de Hola.

Servicios multimedia proporciona empaquetado dinámico que permite toodeliver la velocidad de bits adaptativa MP4 o Smooth Streaming con codificación de contenido de transmisión por secuencias formatos admitidos por los servicios multimedia (MPEG DASH, HLS, Smooth Streaming) sin necesidad de toore-package en estos formatos de transmisión por secuencias.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. aprovechar tootake [empaquetado dinámico](media-services-dynamic-packaging-overview.md), necesita toodo Hola siguiente:
>
>Además, codificar el archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa (más adelante en este tutorial se muestran los pasos de codificación de hello).

Servicios multimedia admite siguientes de hello en los codificadores de petición que se describen en este artículo:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Flujo de trabajo premium de codificación de medios](media-services-encode-asset.md#media-encoder-premium-workflow)

Este artículo ofrece una breve introducción a petición codificadores de medios y proporciona tooarticles de vínculos que proporcionan información más detallada. tema de Hello también proporciona la comparación de codificadores de Hola.

>[!NOTE]
>De forma predeterminada cada cuenta de Servicios multimedia puede tener una tarea de codificación activa a la vez. Puede reservar unidades de codificación que le permiten toohave ejecución simultánea, uno para cada unidad reservada de codificación que se adquieren varias tareas de codificación. Para obtener información, consulte [Escalado de unidades de codificación](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Media Encoder Estándar
### <a name="how-toouse"></a>Cómo toouse
[¿Cómo tooencode con Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Formatos
[Códecs y formatos](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Valores preestablecidos
Media Encoder estándar se configura mediante uno de los valores predefinidos del codificador Hola descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadatos de entrada y salida
Hello codificadores metadatos de entrada se describen [aquí](media-services-input-metadata-schema.md).

Hello metadatos de salida de los codificadores se describen [aquí](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Generación de miniaturas
Para obtener información, consulte [cómo miniaturas de toogenerate utilizando Media Encoder estándar](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Recorte de vídeos
Para obtener información, consulte [cómo vídeos de tootrim con Media Encoder estándar](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Creación de superposiciones
Para obtener información, consulte [cómo toocreate se superpone con Media Encoder estándar](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Otras referencias
[blog de servicios multimedia de Hola](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Flujo de trabajo del Codificador multimedia
### <a name="overview"></a>Información general
[Introducción de la codificación Premium en Servicios multimedia de Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Cómo toouse
El flujo de trabajo del Codificador multimedia Premium se configura mediante flujos de trabajo complejos. Archivos de flujo de trabajo se pudo crear y actualizar con hello [Workflow Designer](media-services-workflow-designer.md) herramienta.

[¿Cómo tooUse Premium de codificación en servicios multimedia de Azure](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Problemas conocidos
Si el vídeo de entrada no contiene subtítulos, Hola salida que activos todavía contendrá un archivo TTML vacío.


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artículos relacionados
* [Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar](media-services-custom-mes-presets-with-dotnet.md)
* [Cuotas y limitaciones](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
