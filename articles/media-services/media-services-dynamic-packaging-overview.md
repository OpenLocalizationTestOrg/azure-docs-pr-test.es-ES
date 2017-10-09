---
title: "información general sobre el empaquetado dinámico de servicios multimedia aaaAzure | Documentos de Microsoft"
description: "Hola tema proporciona y visión general de los paquetes dinámicos."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>Empaquetado dinámico
## <a name="overview"></a>Información general
Servicios de multimedia de Microsoft Azure puede ser usado toodeliver origen multimedia muchos formatos de archivo, formatos de transmisión por secuencias de multimedia y formatos de protección de contenido tooa gran variedad de tecnologías de cliente (por ejemplo, iOS, XBOX, Silverlight, Windows 8). Estos clientes entienden distintos protocolos. Por ejemplo, iOS requiere un formato HTTP Live Streaming (HLS) V4, y Silverlight y Xbox requieren Smooth Streaming. Si tiene un conjunto de velocidad de bits adaptativa (velocidades de bits) MP4 archivos (ISO Base Media 14496-12) o un conjunto de archivos de Smooth Streaming de velocidad de bits adaptativa que desea tooclients tooserve que entienden MPEG DASH, HLS o Smooth Streaming, le conviene aprovechar de medios Servicios de empaquetado dinámico.

Con el empaquetado dinámico todo lo que necesita es toocreate un activo que contiene un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa. A continuación, según Hola formato especificado en el manifiesto de Hola o fragmentar la solicitud, Hola servidor se asegurará de que recibe Hola transmisión por secuencias de protocolo de Hola que ha elegido el Streaming a petición. Como resultado, solo tendrá toostore y pago para los archivos de hello en formato de almacenamiento único y el servicio de servicios multimedia creará y proporcionará la respuesta adecuada Hola según las solicitudes de un cliente.

Hello siguiente diagrama muestra la codificación tradicional de Hola y flujo de trabajo de empaquetado estático.

![Codificación estática](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Hello siguiente diagrama muestra el flujo de trabajo de hello empaquetado dinámico.

![Codificación dinámica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Escenario común
1. Cargar un archivo de entrada (llamado archivo intermedio). Por ejemplo, H.264, MP4 o WMV (consulte lista de Hola de formatos admitidos [formatos compatibles con hello Media Encoder estándar](media-services-media-encoder-standard-formats.md).
2. Codificar los conjuntos de velocidad de bits adaptativa mezzanine tooH.264 MP4 de archivo.
3. Publicar el recurso de Hola que contiene Hola velocidad de bits adaptativa MP4 establecido mediante la creación de hello localizador a petición.
4. Compile hello tooaccess de direcciones URL de streaming y transmitir el contenido.

## <a name="preparing-assets-for-dynamic-streaming"></a>Preparación de recursos para el streaming dinámico
tooprepare su activo para dinámicas de transmisión por secuencias se tiene dos opciones:

1. [Cargar un archivo maestro](media-services-dotnet-upload-files.md).
2. [Usar conjuntos de velocidad de bits adaptativa de codificador Media Encoder estándar de hello tooproduce MP4 H.264](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Transmita el contenido](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Formatos no compatibles con el empaquetado dinámico
Hello siguientes formatos de archivo de origen no se admiten con el empaquetado dinámico.

* Archivos MP4 Dolby Digital.
* Archivos MP4 Dolby Digital Smooth.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

