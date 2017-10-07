---
title: aaa"publicar contenido con hello portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de saludo de la publicación del contenido con hello portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Publicar contenido con hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Información general
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

tooprovide el usuario con una dirección URL que puede ser toostream usado o descargar el contenido, primero necesita demasiado "publicar" su activo mediante la creación de un localizador. Los localizadores proporcionan toofiles de acceso que contiene el recurso de Hola. Media Services admite dos tipos de localizadores: 

* Transmisión por secuencias localizadores (OnDemandOrigin), que se usan para streaming adaptable (por ejemplo, toostream MPEG DASH, HLS o Smooth Streaming). toocreate un localizador de streaming el activo debe contener un archivo .ism. 
* Localizadores (SAS) progresivos, utilizados para la entrega de vídeo mediante descarga progresiva.

Una dirección URL de streaming tiene Hola siguiendo el formato y se pueden usar recursos de Smooth Streaming tooplay.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Anexar toobuild una transmisión por secuencias de dirección URL, de HLS (formato = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Anexar toobuild una dirección URL de streaming de MPEG DASH (formato = mpd: tiempo-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

Una dirección URL SAS tiene Hola siguiendo el formato.

    {blob container name}/{asset name}/{file name}/{SAS signature}

Para obtener más información, consulte la [introducción a la entrega de contenidos](media-services-deliver-content-overview.md).

> [!NOTE]
> Si utiliza los localizadores de hello toocreate portal antes de marzo de 2015, se crearon localizadores con una fecha de expiración de dos años.  
> 
> 

tooupdate una fecha de caducidad en un localizador, utilice [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Tenga en cuenta que cuando se actualiza la fecha de expiración de Hola de un localizador SAS, dirección URL de hello cambia.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse Hola portal toopublish un activo
toouse Hola portal toopublish un activo, Hola siguientes:

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Seleccione **Configuración** > **Activos**.
3. Seleccione activo de Hola que desea toopublish.
4. Haga clic en hello **publicar** botón.
5. Seleccione el tipo de localizador de Hola.
6. Presione **Agregar**.
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

dirección URL de Hola se agregarán toohello lista de **publicado direcciones URL**.

## <a name="play-content-from-hello-portal"></a>Reproducir contenido del portal de Hola
Hello portal de Azure proporciona un Reproductor de contenido que se puede usar tootest el vídeo.

Haga clic en vídeo de hello deseado y, a continuación, haga clic en hello **reproducir** botón.

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

Se aplican algunas consideraciones:

* Asegúrese de que se ha publicado Hola vídeo.
* Esto **Reproductor** reproduce desde predeterminado Hola extremo de streaming. Si desea que tooplay de un valor no predeterminado del origen, haga clic en la dirección URL de hello toocopy y utilice otro reproductor. Por ejemplo, [Reproductor de Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Hola origen desde el que está transmitiendo por secuencias debe estar ejecutándose.  

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

