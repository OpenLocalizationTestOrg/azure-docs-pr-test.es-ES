---
title: "aaaConfigure Hola toosend de codificador Telestream Wirecast una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure hello Wirecast codificador toosend una velocidad de bits única secuencia tooAMS canales activos que están habilitadas para la codificación en directo. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Usar hello Wirecast codificador toosend una secuencia en directo de velocidad de bits única
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Este tema se muestra cómo hello tooconfigure [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live codificador toosend canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo.  Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE). Esta herramienta solo se ejecuta en Windows PC. Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Requisitos previos
* [Creación de una cuenta de Azure Media Services](media-services-portal-create-account.md)
* Asegúrese de que hay un punto de conexión de streaming en ejecución. Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)
* Instalar la versión más reciente de hello del programa Hola a [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) herramienta.
* Iniciar la herramienta de Hola y conectar con cuenta de tooyour AMS.

## <a name="tips"></a>Sugerencias
* Siempre que sea posible, use una conexión a Internet por cable.
* Una buena regla general al determinar los requisitos de ancho de banda es hello toodouble streaming de velocidades de bits. Aunque esto no es un requisito obligatorio, ayudará a mitigar el impacto de Hola de congestión de la red.
* Cuando se usen codificadores por software, cierre todos los programas innecesarios.

## <a name="create-a-channel"></a>Crear un canal
1. En la herramienta AMSE de hello, navegue toohello **Live** ficha y haga clic en el área del canal de Hola. Seleccione **Crear canal...** en el menú de Hola.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Especifique un nombre de canal, el campo de descripción de hello es opcional. En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTMP**. Puede dejar todas las demás opciones como están.

    Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.

3. Haga clic en **Crear canal**.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> canal de Hello puede tardar tanto como toostart de 20 minutos.
>
>

Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo. Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Configurar Hola codificador Telestream Wirecast
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

### <a name="configuration-steps"></a>Pasos de configuración
1. Abra la aplicación de Telestream Wirecast de hello en hello máquina que se va a usar y configurar para la transmisión por secuencias RTMP.
2. Configurar la salida de hello desplazándose toohello **salida** ficha y seleccionando **configuración de salida...** .

    Asegúrese de hello seguro **destino de salida** se establece demasiado**servidor RTMP**.
3. Haga clic en **Aceptar**.
4. En la página de configuración de hello, Establece hello **destino** campo toobe **servicios multimedia de Azure**.

    Hola perfil de codificación está preseleccionada demasiado**Azure H.264 720 p 16:9 (1280 x 720)**. toocustomize estas opciones, seleccione Hola engranaje icono toohello derecha del saludo de lista desplegable y, a continuación, elija **nuevo valor predeterminado**.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Configure los valores preestablecidos del codificador.

    Hola nombre preestablecido y busque siguiente Hola configuración recomendada:

    **Vídeo**

   * Encoder (Codificador): MainConcept H.264
   * Frames per Second (Fotogramas por segundo): 30
   * Bit Rate (Velocidad de bits): 5000 kbps/sec (seg.) (se puede ajustar en función de las limitaciones de red)
   * Profile (Perfil): Main (Principal)
   * Key frame every (Fotograma clave cada): 60 frames (fotogramas)

    **Audio**

   * Target bit rate (Velocidad de bits de destino): 192 kbits/sec (seg)
   * Sample Rate (Frecuencia de muestreo): 44,100 kHz

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Presione **Save**(Guardar).

    campo de codificación de Hello tiene ahora disponibles para la selección de perfil de hello recién creado.

    Asegúrese de que está seleccionado el nuevo perfil de Hola.
7. Obtener dirección URL de entrada del canal de hello en orden tooassign, toohello Wirecast **RTMP extremo**.

    Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola. Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.

    Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. Hola Wirecast **configuración de salida** ventana, pegar esta información en hello **dirección** campo de la sección de la salida de hello y asigne un nombre de la secuencia.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Seleccione **Aceptar**.
2. En hello principal **Wirecast** , confirme los orígenes de entrada de vídeo y audio están listos y, a continuación, presione **flujo** en la esquina superior izquierda de Hola.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Antes de hacer clic **flujo**, le **debe** Asegúrese de que el canal de hello está listo.
> Además, asegúrese de que no tooleave Hola canal en un estado listo sin una contribución entrada fuente durante más de 15 minutos de >.
>
>

## <a name="test-playback"></a>Prueba de reproducción

Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado. En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.

Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada. Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.  

## <a name="create-a-program"></a>Creación de un programa
1. Una vez confirmada la reproducción de canales, cree un programa. En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. Nombre de programa hello y, si es necesario, ajuste hello **duración de la ventana de archivo** (qué horas too4 de los valores predeterminados). También puede especificar una ubicación de almacenamiento o deje el valor predeterminado de Hola.  
3. Comprobar hello **inicio Hola programa ahora** cuadro.
4. Haga clic en **Crear programa**.  

   >[!NOTE]
   >La creación de programas tarda menos que la creación de canales.
       
5. Una vez que se ejecuta el programa de hello, confirme la reproducción, haga clic en el programa hello y vaya demasiado**programas de reproducción hello** y, a continuación, seleccione **con el Reproductor de Media de Azure**.  
6. Una vez confirmado, haga clic en programa Hola de nuevo y seleccione **copiar tooClipboard de dirección URL de salida de hello** (o recuperar la información desde hello **información y configuración de programas** opción de menú de hello).

secuencia de Hello ahora está listo toobe incrustado en un reproductor o distribuida tooan público para live visualización.  

## <a name="troubleshooting"></a>Solución de problemas
Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
