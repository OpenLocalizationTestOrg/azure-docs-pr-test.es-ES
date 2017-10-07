---
title: secuencia de aaaLive con codificadores locales mediante Hola portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de creación de un canal que está configurado para la entrega de una acceso directo."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>¿Cómo tooperform streaming en vivo con local codificadores mediante Hola portal de Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Este tutorial le guiará por los pasos de hello del uso de hello Azure toocreate portal un **canal** que está configurado para la entrega de una acceso directo. 

## <a name="prerequisites"></a>Requisitos previos
tutorial de hello toocomplete necesarios son las siguientes de Hello:

* Una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Una cuenta de Media Services. toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).
* Una cámara web. Por ejemplo, el [codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).

Se recomienda encarecidamente hello tooreview siguientes artículos:

* [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo.](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Información general de streaming en vivo con Servicios multimedia de Azure](media-services-manage-channels-overview.md)
* [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Escenario común de streaming en vivo
Hello pasos siguientes describen las tareas implicadas en la creación de aplicaciones transmisión por secuencias en directo comunes que usan los canales que se configuran para la entrega de paso a través. Este tutorial se muestra cómo toocreate y administrar un canal de acceso directo y eventos en directo.

>[!NOTE]
>Asegúrese de que esté Hola origen desde el que desea que el contenido de toostream Hola **ejecutando** estado. 
    
1. Conectar un equipo de tooa de cámara de vídeo. Inicie y configure un codificador en directo local que genere una transmisión de RTMP o MP4 fragmentado con velocidad de bits múltiple. Para obtener más información, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Este paso también puede realizarse después de crear el canal.
2. Cree e inicie un canal de paso a través.
3. URL de introducción de hello recuperar canales. 
   
    URL de introducción de Hola Hola codificador en directo toosend hello secuencia toohello canal utiliza.
4. Recuperar la dirección URL de vista previa de canal de Hola. 
   
    Utilice este tooverify de dirección URL que el canal está recibiendo correctamente la secuencia en directo de Hola.
5. Cree un evento o programa en directo. 
   
    Al usar hello portal de Azure, también crea un evento en directo crea un activo. 

6. Inicie Hola eventos/programa cuando esté listo toostart streaming y archivado.
7. Si lo desea, codificador en directo de hello puede ser señalado toostart un anuncio. anuncio de Hola se inserta en el flujo de salida de hello.
8. Detener Hola eventos/programa siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.
9. Eliminar eventos de Hola y programa (y opcionalmente eliminar recurso de hello).     

> [!IMPORTANT]
> Revise [de transmisión por secuencias en directo con codificadores locales que crean secuencias de velocidades de bits](media-services-live-streaming-with-onprem-encoders.md) toolearn sobre los conceptos y consideraciones relacionadas con streaming toolive con codificadores locales y los canales de acceso directo.
> 
> 

## <a name="tooview-notifications-and-errors"></a>errores y las notificaciones de tooview
Si desea que las notificaciones de tooview y los errores generados por hello portal de Azure, haga clic en el icono de notificación de Hola.

![Notificaciones](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Creación e inicio de canales de paso a través y eventos
Un canal está asociado con programas y eventos que permiten la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo. Los canales administran los eventos. 

Puede especificar Hola número de horas que quiere tooretain Hola registran contenido de programa Hola, establecer hello **ventana de archivo** longitud. Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas. Duración de la ventana de archivo también establece la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola. Se pueden ejecutar eventos sobre la cantidad de tiempo especificada de hello, pero continuamente se descarta el contenido que se encuentra detrás de la longitud de la ventana de Hola. El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.

Cada evento está asociado a un recurso. evento de hello toopublish, debe crear un localizador OnDemand para activo Hola asociado. Este localizador permite toobuild una URL de streaming puede proporcionar a los clientes de tooyour.

Un canal admite hasta toothree eventos en ejecución simultánea por lo que puede crear varios archivos de hello mismo flujo entrante. Esto le permite toopublish y archivar diferentes partes de un evento según sea necesario. Por ejemplo, sus necesidades de negocio es tooarchive 6 horas de un programa, pero toobroadcast solo últimos 10 minutos. tooaccomplish, necesita toocreate dos programas en ejecución simultáneos. Un programa se establece tooarchive 6 horas de evento de hello pero no se publica el programa Hola. Hello otro programa es conjunto tooarchive durante 10 minutos y se publica este programa.

No debería reutilizar eventos en directo ya existentes. En su lugar, cree e inicie un evento nuevo para cada evento.

Evento de hello cuando esté listo toostart streaming y archivado de inicio. Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola. 

contenido toodelete archivado, detener y eliminar eventos de Hola y, a continuación, eliminar recurso asociado Hola. No se puede eliminar un recurso si se utiliza un evento; evento de Hello debe eliminarse en primer lugar. 

Incluso después de detener y eliminar un evento de hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola.

Si desea hello tooretain archivado de contenido, pero no la tiene disponible para la transmisión por secuencias, eliminar Hola localizador de streaming.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse Hola portal toocreate un canal
Esta sección se muestra cómo hello toouse **creación rápida** opción toocreate un canal de acceso directo.

Para más información sobre este tipo de canales, consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Hola **configuración** ventana, haga clic en **streaming en vivo**. 
   
    ![Introducción](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Hola **streaming en vivo** aparecerá la ventana.
3. Haga clic en **creación rápida** protocolo de introducción de toocreate un canal de acceso directo con hello RTMP.
   
    Hola **crear un nuevo canal** aparecerá la ventana.
4. Asigne un nombre de canal nuevo de Hola y haga clic en **crear**. 
   
    Esto crea un canal de acceso directo con hello protocolo de introducción RTMP.

## <a name="create-events"></a>Creación de eventos
1. Seleccione un toowhich de canal que desee tooadd un evento.
2. Pulse el botón **Evento en directo** .

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Obtención de direcciones URL de introducción
Una vez creado el canal de hello, puede obtener direcciones URL que proporcionará toohello de codificador en directo de entrada. Codificador de Hello usa estos tooinput de direcciones URL de una secuencia en directo.

![Creado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Evento de Hola de inspección
evento de hello toowatch, haga clic en **inspección** en hello Azure Hola portal o copiar dirección URL de streaming y utilizar un Reproductor de su elección. 

![Creado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Evento en directo obtienen automáticamente contenido de tooon convertido a petición cuando se detuvo.

## <a name="clean-up"></a>Limpieza
Para más información sobre este tipo de canales, consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).

* Un canal se puede detener cuando se hayan detenido todos los programas y eventos en el canal de Hola.  Una vez que se detiene el canal de hello, no incurrirás en gastos. Cuando necesite toostart nuevo, lo tendrá hello misma URL de introducción por lo que no necesita tooreconfigure su codificador.
* Un canal puede eliminarse solo si se han eliminado todos los eventos en directo en el canal de Hola.

## <a name="view-archived-content"></a>Visualización del contenido archivado
Incluso después de detener y eliminar un evento de hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola. No se puede eliminar un recurso si se utiliza un evento; evento de Hello debe eliminarse en primer lugar. 

Seleccionar de los activos de toomanage **configuración** y haga clic en **activos**.

![Recursos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

