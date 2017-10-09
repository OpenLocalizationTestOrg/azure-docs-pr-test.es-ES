---
title: "aaaConfigure Hola toosend de codificador en vivo Elemental una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure Hola toosend de codificador en vivo Elemental canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Usar toosend del codificador de Live Elemental de hello una secuencia en directo de velocidad de bits única
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Este tema se muestra cómo hello tooconfigure [Live Elemental](http://www.elementaltechnologies.com/products/elemental-live) codificador toosend una velocidad de bits única transmitir canales tooAMS que están habilitados para la codificación en directo.  Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE). Esta herramienta solo se ejecuta en Windows PC. Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Requisitos previos
* Debe tener conocimientos prácticos de utilizando Live Elemental web interfaz toocreate eventos en directo.
* [Creación de una cuenta de Azure Media Services](media-services-portal-create-account.md)
* Asegúrese de que hay un punto de conexión de streaming en ejecución. Para más información, consulte [Administración de puntos de conexión de streaming en una cuenta de Media Services](media-services-portal-manage-streaming-endpoints.md).
* Instalar la versión más reciente de hello del programa Hola a [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) herramienta.
* Iniciar la herramienta de Hola y conectar con cuenta de tooyour AMS.

## <a name="tips"></a>Sugerencias
* Siempre que sea posible, use una conexión a Internet por cable.
* Una buena regla general al determinar los requisitos de ancho de banda es hello toodouble streaming de velocidades de bits. Aunque esto no es un requisito obligatorio, ayudará a mitigar el impacto de Hola de congestión de la red.
* Cuando se usen codificadores por software, cierre todos los programas innecesarios.

## <a name="elemental-live-with-rtp-ingest"></a>Elemental Live con entrada RTP
Esta sección muestra cómo tooconfigure Hola Elemental codificador en directo que se envía a una velocidad de bits única secuencia en directo a través de RTP.  Para obtener más información, consulte [Transmisión MPEG TS sobre RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Crear un canal

1. En la herramienta AMSE de hello, navegue toohello **Live** ficha y haga clic en el área del canal de Hola. Seleccione **Crear canal...** en el menú de Hola.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Especifique un nombre de canal, el campo de descripción de hello es opcional. En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTP (MPEG-TS)**. Puede dejar todas las demás opciones como están.

    Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.

3. Haga clic en **Crear canal**.

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> canal de Hello puede tardar tanto como toostart de 20 minutos.
>
>

Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo. Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Configurar el codificador de Live Elemental Hola
En este tutorial Hola se utilizan las siguientes opciones de salida. resto de Hola de esta sección describe los pasos de configuración con más detalle.

**Vídeo**:

* Codec (Códec): H.264
* Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])
* Bitrate (Velocidad de bits): 5000 kbps
* Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])
* Frame Rate (Velocidad de fotogramas): 30

**Audio**:

* Codec (Códec): AAC (LC)
* Bitrate (Velocidad de bits): 192 kbps
* Sample Rate (Frecuencia de muestreo): 44,1 kHz

#### <a name="configuration-steps"></a>Pasos de configuración
1. Navegue toohello **Live Elemental** interfaz web y configurar el codificador de Hola para **UDP/TS** transmisión por secuencias.
2. Una vez que se crea un nuevo evento, desplácese hacia abajo de grupos de resultados toohello y agregar hello **UDP/TS** grupo de resultados.
3. Para crear una salida, seleccione **New Stream** (Nueva transmisión) y haga clic en **Add Output** (Agregar salida).  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > Se recomienda ese evento Elemental hello tiene código de hello tiempo establecido demasiado volver a conectar un codificador de hello toohelp "Reloj del sistema" en caso de hello de un error de secuencia.
   >
   >
4. Ahora que hello salida se ha creado, haga clic en **Agregar secuencia**. Ahora se puede configurar la configuración de salida de Hello.
5. Desplácese hacia abajo toohello "Stream 1" que acaba de crear, haga clic en hello **vídeo** ficha Hola izquierda y expanda hello **avanzadas** sección de configuración.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Aunque Live Elemental tiene una amplia gama de personalización disponibles, hello siguiente configuración se recomienda para comenzar a usar tooAMS de transmisión por secuencias.

   * Resolution (Resolución): 1280 x 720
   * Framerate (Velocidad de fotogramas): 30
   * GOP Size (Tamaño de GOP): 60 fotogramas
   * Interlace Mode (Modo de vídeo entrelazado): Progresivo
   * Bit Rate (Velocidad de bits): 5000000 bits/s (se puede ajustar en función de las limitaciones de red)

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Obtener dirección URL de entrada del canal de Hola.

    Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola. Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.

    Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Pegar esta información en hello **destino principal** campo de hello Elemental. Todas las demás opciones pueden permanecer predeterminado Hola.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Para obtener redundancia adicional, repita estos pasos con hello secundaria de dirección URL de entrada mediante la creación de una pestaña independiente de "Salida" para la transmisión por secuencias de UDP/TS.
3. Haga clic en **crear** (si se ha creado un nuevo evento) o **actualización** (si está modificando un evento preexistente) y, a continuación, continuar codificador de hello toostart.

> [!IMPORTANT]
> Antes de hacer clic **iniciar** en interfaz web Live Elemental de hello, **debe** Asegúrese de que el canal de hello está listo.
> Además, asegúrese de que no tooleave Hola canal en un estado listo sin un evento durante más de 15 minutos de >.
>
>

Después de que se ha ejecutado la secuencia de Hola durante 30 segundos, desplácese atrás toohello AMSE herramienta y prueba la reproducción.  

### <a name="test-playback"></a>Prueba de reproducción

Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado. En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.

Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada. Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.   

### <a name="create-a-program"></a>Creación de un programa
1. Una vez confirmada la reproducción de canales, cree un programa. En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Nombre de programa hello y, si es necesario, ajuste hello **duración de la ventana de archivo** (qué horas too4 de los valores predeterminados). También puede especificar una ubicación de almacenamiento o deje el valor predeterminado de Hola.  
3. Comprobar hello **inicio Hola programa ahora** cuadro.
4. Haga clic en **Crear programa**.  

    >[!NOTE]
    > La creación de programas tarda menos que la creación de canales.   
      
5. Una vez que se ejecuta el programa de hello, confirme la reproducción, haga clic en el programa hello y vaya demasiado**programas de reproducción hello** y, a continuación, seleccione **con el Reproductor de Media de Azure**.  
6. Una vez confirmado, haga clic en programa Hola de nuevo y seleccione **copiar tooClipboard de dirección URL de salida de hello** (o recuperar la información desde hello **información y configuración de programas** opción de menú de hello).

secuencia de Hello ahora está listo toobe incrustado en un reproductor o distribuida tooan público para live visualización.  

## <a name="troubleshooting"></a>Solución de problemas
Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
