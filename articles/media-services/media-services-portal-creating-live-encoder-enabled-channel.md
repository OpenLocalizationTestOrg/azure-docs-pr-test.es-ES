---
title: aaaHow tooperform streaming en vivo con secuencias de velocidades de bits de servicios multimedia de Azure toocreate Hola portal de Azure | Documentos de Microsoft
description: "Este tutorial le guía a través de los pasos de Hola de creación de un canal que recibe una secuencia en directo de velocidad de bits única y lo codifica en la secuencia de velocidad de bits toomulti utilizando Hola portal de Azure."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>¿Cómo tooperform streaming en vivo con servicios multimedia de Azure toocreate velocidades de bits se transmita por secuencias con hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [API DE REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Este tutorial le guiará por los pasos de Hola de creación de un **canal** que recibe una secuencia en directo de velocidad de bits única y lo codifica en la secuencia de velocidad de bits toomulti.

> [!NOTE]
> Para obtener más información consulte tooChannels relacionados que están habilitados para la codificación en directo, [streaming en vivo al utilizar secuencias de velocidades de bits de servicios multimedia de Azure toocreate](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Escenario común de streaming en vivo
Hola siguientes pasos son generales implicadas en la creación de aplicaciones de transmisión por secuencias en directo común.

> [!NOTE]
> Actualmente, Hola máximo recomendado de duración de un evento en directo es 8 horas. Póngase en contacto con amslived Microsoft.com si necesitas toorun un canal para períodos más largos de tiempo.
> 
> 

1. Conectar un equipo de tooa de cámara de vídeo. Iniciar y configurar un codificador en directo local que pueda dar como resultado una secuencia de velocidad de bits única en uno de hello siguientes protocolos: RTP (MPEG-TS), Smooth Streaming o RTMP. Para obtener más información, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Este paso también puede realizarse después de crear el canal.
2. Cree e inicie un canal. 
3. URL de introducción de hello recuperar canales. 
   
    URL de introducción de Hola Hola codificador en directo toosend hello secuencia toohello canal utiliza.
4. Recuperar la dirección URL de vista previa de canal de Hola. 
   
    Utilice este tooverify de dirección URL que el canal está recibiendo correctamente la secuencia en directo de Hola.
5. Cree un evento o programa (que también creará un recurso). 
6. Publicar eventos hello (que se va a crear un localizador a petición para el recurso asociado hello).    
7. Evento de hello cuando esté listo toostart streaming y archivado de inicio.
8. Si lo desea, codificador en directo de hello puede ser señalado toostart un anuncio. anuncio de Hola se inserta en el flujo de salida de hello.
9. Detener el evento de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.
10. Eliminar un evento de hello (y opcionalmente eliminar recurso de hello).   

## <a name="in-this-tutorial"></a>Apartados de este tutorial
En este tutorial, Hola portal de Azure es hello tooaccomplish usado siguiente las tareas: 

1. Crear un canal que es habilitado tooperform codificación en directo.
2. Get Hola URL de introducción en orden toosupply se toolive codificador. codificador en directo de Hello utilizará esta secuencia de dirección URL tooingest hello en hello canal.
3. Cree un evento o programa (y un recurso).
4. Publicar el recurso de Hola y obtenga direcciones URL de streaming.  
5. Reproduzca el contenido.
6. Realice la limpieza.

## <a name="prerequisites"></a>Requisitos previos
los siguientes Hola son tutorial de hello toocomplete necesarios.

* toocomplete este tutorial, necesita una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. 
  Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* Una cuenta de Media Services. toocreate una cuenta de servicios multimedia, consulte [crear cuenta](media-services-portal-create-account.md).
* Una cámara web y un codificador que pueda enviar una secuencia en vivo de una sola velocidad de bits.

## <a name="create-a-channel"></a>Crear un canal
1. Hola [portal de Azure](https://portal.azure.com/), seleccione los servicios multimedia y, a continuación, haga clic en el nombre de la cuenta de servicios multimedia.
2. Seleccione **Streaming en vivo**.
3. Seleccione **Creación personalizada**. Esta opción le permite crear un canal habilitado para la codificación en directo.
   
    ![Creación de un canal](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Haga clic en **Configuración**.
   
   1. Elija hello **codificación en directo** tipo de canal. Este tipo se especifica que desea toocreate un canal que está habilitado para la codificación en directo. Que significa Hola entrante velocidad de bits única secuencia se envía toohello canal y se codifica como una secuencia de bits múltiple con la configuración de codificador en directo especificado. Para obtener más información, consulte [streaming en vivo al utilizar secuencias de velocidades de bits de servicios multimedia de Azure toocreate](media-services-manage-live-encoder-enabled-channels.md). Haga clic en Aceptar.
   2. Especifique el nombre de un canal.
   3. Haga clic en Aceptar en la parte inferior de Hola de pantalla de bienvenida.
5. Seleccione hello **Introducción** ficha.
   
   1. En esta página, puede seleccionar un protocolo de streaming. Para hello **codificación en directo** son de tipo de canal, opciones de protocolo válido:
      
      * MP4 fragmentado de una sola velocidad de bits (Smooth Streaming)
      * RTMP de velocidad de bits única
      * RTP (MPEG-TS): secuencia de transporte MPEG-2 a través de RTP.
        
        Para ver una explicación detallada acerca de cada protocolo, vea [streaming en vivo al utilizar secuencias de velocidades de bits de servicios multimedia de Azure toocreate](media-services-manage-live-encoder-enabled-channels.md).
        
        No se puede cambiar la opción de protocolo de hello mientras Hola canal o se ejecutan sus programas y eventos asociados. Si necesitan diferentes protocolos, debe crear canales independientes para cada protocolo de streaming.  
   2. Puede aplicar restricciones de IP en Hola de introducción. 
      
       Puede definir Hola IP permiten direcciones que están tooingest un canal de vídeo toothis. Dichas direcciones se pueden especificar como dirección IP individual (por ejemplo, ‘10.0.0.1’), un intervalo de direcciones IP mediante una dirección IP y una máscara de subred CIDR (por ejemplo, ‘10.0.0.1/22’) o un intervalo de direcciones IP mediante una dirección IP y una máscara de subred decimal con puntos (por ejemplo, '10.0.0.1(255.255.252.0)').
      
       Si no se especifican direcciones IP y no hay ninguna definición de regla, no se permitirá ninguna dirección IP. tooallow todas las direcciones IP, cree una regla y establezca 0.0.0.0/0.
6. En hello **vista previa** pestaña, se aplican restricciones de IP en vista previa de Hola.
7. En hello **codificación** ficha, especifique el valor predeterminado de codificación de Hola. 
   
    Actualmente, Hola solo sistema preestablecida puede seleccionar es **predeterminado 720p**. toospecify personalizado preestablecido, abra una incidencia de soporte técnico de Microsoft. A continuación, escriba el nombre de Hola de hello creado para la programación. 

> [!NOTE]
> Actualmente, el inicio de canal de hello puede tardar hasta too30 minutos. Restablecimiento de un canal puede tardar minutos too5.
> 
> 

Una vez creado el canal de hello, puede hacer clic en el canal de Hola y seleccione **configuración** donde puede ver las configuraciones de canales. 

Para obtener más información, consulte [streaming en vivo al utilizar secuencias de velocidades de bits de servicios multimedia de Azure toocreate](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Obtención de direcciones URL de introducción
Una vez creado el canal de hello, puede obtener direcciones URL que proporcionará toohello de codificador en directo de entrada. Codificador de Hello usa estos tooinput de direcciones URL de una secuencia en directo.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Creación y administración de eventos
### <a name="overview"></a>Información general
Un canal está asociado con programas y eventos que permiten la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo. Los canales administran los eventos y programas. Hello relación de canales y los programas es un medio muy similar tootraditional donde un canal tiene un flujo constante de contenido y un programa es toosome ámbito ha superado el tiempo de evento en ese canal.

Puede especificar número de Hola de horas que desee tooretain Hola registran contenido para el evento de Hola Hola establecer **ventana de archivo** longitud. Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas. Duración de la ventana de archivo también establece la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola. Se pueden ejecutar eventos sobre la cantidad de tiempo especificada de hello, pero continuamente se descarta el contenido que se encuentra detrás de la longitud de la ventana de Hola. El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.

Cada evento está asociado a un recurso. evento de hello toopublish debe crear un localizador OnDemand para hello asociado activo. Este localizador permitirá toobuild una URL de streaming puede proporcionar a los clientes de tooyour.

Un canal admite hasta toothree eventos en ejecución simultánea por lo que puede crear varios archivos de hello mismo flujo entrante. Esto le permite toopublish y archivar diferentes partes de un evento según sea necesario. Por ejemplo, sus necesidades de negocio es tooarchive 6 horas de un evento, pero toobroadcast solo últimos 10 minutos. tooaccomplish esto, se necesitan toocreate dos en ejecución simultánea eventos. Un evento se establece tooarchive 6 horas de evento de hello pero no se publica el programa Hola. Hello otro evento es conjunto tooarchive durante 10 minutos y se publica este programa.

No debe volver a usar programas existentes para eventos nuevos. En su lugar, cree e inicie un programa nuevo para cada evento.

Iniciar un programa o el evento cuando esté listo toostart streaming y archivado. Detener el evento de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola. 

contenido toodelete archivado, detener y eliminar eventos de Hola y, a continuación, eliminar recurso asociado Hola. No se puede eliminar un recurso si se usa por evento de hello; evento de Hello debe eliminarse en primer lugar. 

Incluso después de detener y eliminar un evento de hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola.

Si desea hello tooretain archivado de contenido, pero no la tiene disponible para la transmisión por secuencias, eliminar Hola localizador de streaming.

### <a name="createstartstop-events"></a>Creación/inicio/detención de eventos
Una vez que tenga el flujo de hello fluyendo en canal de hello puede empezar Hola transmisión por secuencias de eventos mediante la creación de un recurso, el programa y el localizador de Streaming. Esto archivar hello secuencia y hacerla tooviewers disponible a través de hello extremo de transmisión por secuencias. 

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

Hay eventos de toostart de dos maneras: 

1. De hello **canal** página, presione **Live eventos** tooadd un nuevo evento.
   
    Especifique lo siguiente: nombre de evento, nombre de recurso, ventana de archivo y opción de cifrado.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Si ha dejado **publicar ahora este evento en vivo** activa, se creará Hola Hola de evento direcciones URL de publicación.
   
    Puede presionar **iniciar**, siempre que son eventos de hello toostream listo.
   
    Una vez que comience el evento de hello, puede presionar **inspección** toostart reproducir contenido de Hola.
2. Como alternativa, puede usar un método abreviado y presione **Go Live** botón en hello **canal** página. Se creará un recurso, un programa y el localizador de streaming predeterminados.
   
    evento de Hola se denomina **predeterminada** y se establece la ventana de archivo de hello too8 horas.

Puede observar los eventos publicados de Hola de hello **evento en directo** página. 

Si hace clic en **Off air**(Cancelar emisión), se detienen todos los eventos en directo. 

## <a name="watch-hello-event"></a>Evento de Hola de inspección
evento de hello toowatch, haga clic en **inspección** en hello Azure Hola portal o copiar dirección URL de streaming y utilizar un Reproductor de su elección. 

![Creado](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Evento en directo convierte automáticamente el contenido a petición tooon eventos cuando se detuvo.

## <a name="clean-up"></a>Limpieza
Si se realiza la transmisión por secuencias de eventos y desea tooclean recursos Hola aprovisionado anteriormente, siga Hola siguiendo el procedimiento.

* Detenga la inserción de secuencia de Hola de codificador de Hola.
* Detener el canal de Hola. Una vez que se detiene el canal de hello, no implicará cualquier cargo. Cuando necesite toostart nuevo, lo tendrá hello misma URL de introducción por lo que no necesita tooreconfigure su codificador.
* Puede detener el punto de conexión de la transmisión por secuencias, a menos que desee archivar de hello toocontinue tooprovide de evento en vivo como una secuencia a petición. Si el canal de hello está en estado detenido, no implicará cualquier cargo.

## <a name="view-archived-content"></a>Visualización del contenido archivado
Incluso después de detener y eliminar un evento de hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola. No se puede eliminar un recurso si se utiliza un evento; evento de Hello debe eliminarse en primer lugar. 

Seleccionar de los activos de toomanage **configuración** y haga clic en **activos**.

![Recursos](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Consideraciones
* Actualmente, Hola máximo recomendado de duración de un evento en directo es 8 horas. Póngase en contacto con amslived Microsoft.com si necesitas toorun un canal para períodos más largos de tiempo.
* Asegúrese de que esté Hola streaming el contenido de punto de conexión desde el que desea toostream Hola **ejecutando** estado.

## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

