---
title: "aaaEncode un activo con Media Encoder estándar Hola portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de Hola de codificación de un activo con Media Encoder estándar Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Codificar un activo con Media Encoder estándar con hello portal de Azure
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Cuando se trabaja con servicios de multimedia de Azure, uno de los escenarios más comunes de hello entrega a clientes tooyour streaming de velocidad de bits adaptativa. Servicios multimedia admite Hola siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare los vídeos de streaming de velocidad de bits adaptativa, necesita tooencode el origen de vídeo en archivos de varias velocidades de bits. Debe usar hello **Media Encoder estándar** codificador tooencode sus vídeos.  

Servicios multimedia también proporciona el empaquetado dinámico que permite toodeliver su MP4s velocidades de bits en los siguientes formatos de streaming de Hola: MPEG DASH, HLS, Smooth Streaming, sin necesidad de toore-package en estos formatos de transmisión por secuencias. Con el empaquetado dinámico solo tendrá toostore y pago para archivos de hello en formato de almacenamiento único y servicios multimedia creará y proporcionará Hola respuesta adecuada según las solicitudes de un cliente.

tootake ventaja del empaquetado dinámico, debe tooencode el archivo de origen en un conjunto de archivos MP4 de velocidad de bits múltiple (pasos de codificación de Hola se muestran más adelante en esta sección).

media de tooscale de procesamiento, consulte [esto](media-services-portal-scale-media-processing.md) tema.

## <a name="encode-with-hello-azure-portal"></a>Codificar con hello portal de Azure
Esta sección describen los pasos de Hola que puede seguir tooencode el contenido con Media Encoder estándar.

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Hola **configuración** ventana, seleccione **activos**.  
3. Hola **activos** (ventana), activo Hola select que desearía tooencode.
4. Hola presione **Encode** botón.
5. Hola **codificar un activo** ventana, procesador "Media Encoder" estándar"hello select y un valor preestablecido. Para más información acerca de los valores preestablecidos, consulte [Generación automática de una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) y [Valores preestablecidos de tarea para MES](media-services-mes-presets-overview.md). Si tiene previsto toocontrol se utiliza el valor predeterminado de codificación, Téngalo en cuenta: es importante tooselect Hola preestablecido que sea más adecuado para el vídeo de entrada. Por ejemplo, si sabe que el vídeo de entrada tiene una resolución de 1920 x 1080 píxeles, a continuación, podría utilizar Hola "H264 1080p de velocidad de bits múltiple" preestablecido. Si tiene un vídeo de baja resolución (640 x 360), no debería utilizar el valor preestablecido "H264 Multiple Bitrate 1080p".
   
   Para facilitar la administración, tendrá una opción de edición nombre Hola de recurso de salida de hello y nombre de Hola de trabajo de Hola.
   
   ![Codificación de recursos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Pulse **Crear**.

## <a name="next-step"></a>Paso siguiente
Puede supervisar el progreso de trabajo de codificación con hello portal de Azure, como se describe en [esto](media-services-portal-check-job-progress.md) artículo.  

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

