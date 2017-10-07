---
title: "aaaGet se inició con la entrega de VoD mediante Hola portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de saludo de la implementación de un servicio de entrega de contenido de vídeo bajo demanda (VoD) básico con aplicación de servicios de multimedia de Azure (AMS) mediante Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Introducción a la entrega de contenido a petición con hello portal de Azure
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Este tutorial le guiará por los pasos de saludo de la implementación de un servicio de entrega de contenido de vídeo bajo demanda (VoD) básico con aplicación de servicios de multimedia de Azure (AMS) mediante Hola portal de Azure.

## <a name="prerequisites"></a>Requisitos previos
tutorial de hello toocomplete necesarios son las siguientes de Hello:

* Una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Una cuenta de Media Services. toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).

Este tutorial incluye Hola siguientes tareas:

1. Inicie el punto de conexión de streaming.
2. Carga de un archivo de vídeo.
3. Codificar el archivo de código fuente de hello en un conjunto de archivos MP4 de velocidad de bits adaptativa.
4. Publicar los activos de Hola y get de transmisión por secuencias y direcciones URL de descarga progresiva.  
5. Reproduzca el contenido.

## <a name="start-streaming-endpoints"></a>Inicio de los puntos de conexión de streaming 

Cuando se trabaja con uno de los escenarios más comunes de hello es entregar vídeo a través de la velocidad de bits de transmisión por secuencias adaptativa de servicios de multimedia de Azure. Servicios multimedia proporciona empaquetado dinámico, lo que permite toodeliver la velocidad de bits adaptativa MP4 codificados contenido de transmisión por secuencias formatos admitidos por servicios multimedia (MPEG DASH, HLS, Smooth Streaming) just-in-time, sin necesidad de toostore preempaquetado versiones de cada uno de estos formatos de transmisión por secuencias.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

toostart Hola extremo de streaming, Hola siguientes:

1. Inicie sesión en hello [portal de Azure](https://portal.azure.com/).
2. En la ventana de configuración de hello, haga clic en los puntos de conexión de la transmisión por secuencias. 
3. Haga clic en predeterminada Hola extremo de streaming. 

    Aparecerá la ventana de detalles predeterminada del extremo de transmisión por secuencias de Hola.

4. Haga clic en el icono de inicio de Hola.
5. Haga clic en botón toosave de hello guardar los cambios.

## <a name="upload-files"></a>Carga de archivos
toostream vídeos con servicios multimedia de Azure, necesita vídeos de origen de tooupload hello, codificarlos en varias velocidades de bits y publicar resultados de Hola. primer paso de Hola se trata en esta sección. 

1. Hola **configuración** ventana, haga clic en **activos**.
   
    ![Carga de archivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Haga clic en hello **cargar** botón.
   
    Hola **cargar un recurso de vídeo** aparecerá la ventana.
   
   > [!NOTE]
   > No hay ninguna limitación de tamaño de archivo.
   > 
   > 
3. Examinar vídeo toohello deseado en el equipo, selecciónelo y haga clic en Aceptar.  
   
    inicia la carga de Hola y puede ver progreso de hello en nombre de archivo de Hola.  

Una vez completada la carga de hello, vea activo nuevo Hola enumerado en hello **activos** ventana. 

## <a name="encode-assets"></a>Codificación de recursos

Cuando se trabaja con servicios de multimedia de Azure, uno de los escenarios más comunes de hello entrega a clientes tooyour streaming de velocidad de bits adaptativa. Servicios multimedia admite Hola siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare los vídeos de streaming de velocidad de bits adaptativa, necesita tooencode el origen de vídeo en archivos de varias velocidades de bits. Debe usar hello **Media Encoder estándar** codificador tooencode sus vídeos.  

Servicios multimedia también proporciona el empaquetado dinámico, lo que permite toodeliver su MP4s velocidades de bits en los siguientes formatos de streaming de Hola: MPEG DASH, HLS, Smooth Streaming, sin necesidad de toorepackage en estos formatos de transmisión por secuencias. Con el empaquetado dinámico, solo tendrá toostore y pago para archivos de hello en formato de almacenamiento único y servicios multimedia genera y actúa según las solicitudes de un cliente de respuesta adecuada Hola.

tootake ventaja del empaquetado dinámico, debe tooencode el archivo de origen en un conjunto de archivos MP4 de velocidad de bits múltiple (pasos de codificación de Hola se muestran más adelante en esta sección).

### <a name="toouse-hello-portal-tooencode"></a>toouse Hola portal tooencode
Esta sección describen los pasos de Hola que puede seguir tooencode el contenido con Media Encoder estándar.

1. Hola **configuración** ventana, seleccione **activos**.  
2. Hola **activos** (ventana), activo Hola select que desearía tooencode.
3. Hola presione **Encode** botón.
4. Hola **codificar un activo** ventana, procesador "Media Encoder" estándar"hello select y un valor preestablecido. Para más información acerca de los valores preestablecidos, consulte [Generación automática de una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) y [Valores preestablecidos de tarea para MES](media-services-mes-presets-overview.md). Si tiene previsto toocontrol se utiliza el valor predeterminado de codificación, Téngalo en cuenta: es importante tooselect Hola preestablecido que sea más adecuado para el vídeo de entrada. Por ejemplo, si sabe que el vídeo de entrada tiene una resolución de 1920 x 1080 píxeles, a continuación, podría utilizar Hola "H264 1080p de velocidad de bits múltiple" preestablecido. Si tiene un vídeo de baja resolución (640 x 360), no debería utilizar el valor preestablecido "H264 Multiple Bitrate 1080p".
   
   Para facilitar la administración, tendrá una opción de edición nombre Hola de recurso de salida de hello y nombre de Hola de trabajo de Hola.
   
   ![Codificación de recursos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Pulse **Crear**.

### <a name="monitor-encoding-job-progress"></a>Supervisión del progreso del trabajo de codificación
progreso de hello toomonitor de hello codificación de trabajo, haga clic en **configuración** (al principio de Hola de página de hello) y, a continuación, seleccione **trabajos**.

![Trabajos](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Publicación de contenido
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

> [!NOTE]
> Si utiliza los localizadores de hello toocreate portal antes de marzo de 2015, se crearon localizadores con una fecha de expiración de dos años.  
> 
> 

tooupdate una fecha de caducidad en un localizador, utilice [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Cuando se actualiza la fecha de expiración de Hola de un localizador SAS, cambia la dirección URL de Hola.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse Hola portal toopublish un activo
toouse Hola portal toopublish un activo, Hola siguientes:

1. Seleccione **Configuración** > **Activos**.
2. Seleccione activo de Hola que desea toopublish.
3. Haga clic en hello **publicar** botón.
4. Seleccione el tipo de localizador de Hola.
5. Presione **Agregar**.
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

dirección URL de Hola se agrega la lista de toohello de **publicado direcciones URL**.

## <a name="play-content-from-hello-portal"></a>Reproducir contenido del portal de Hola
Hello portal de Azure proporciona un Reproductor de contenido que se puede usar tootest el vídeo.

Haga clic en vídeo de hello deseado y, a continuación, haga clic en hello **reproducir** botón.

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

Se aplican algunas consideraciones:

* toobegin transmisión por secuencias, iniciar la ejecución hello **predeterminado** extremo de streaming.
* Asegúrese de que se ha publicado Hola vídeo.
* Esto **Reproductor** reproduce desde predeterminado Hola extremo de streaming. Si desea que tooplay de un valor no predeterminado del origen, haga clic en la dirección URL de hello toocopy y utilice otro reproductor. Por ejemplo, [Reproductor de Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

