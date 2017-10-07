---
title: "aaaConfigure Hola NewTek TriCaster codificador toosend una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure hello Tricaster codificador toosend una velocidad de bits única secuencia tooAMS canales activos que están habilitadas para la codificación en directo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Usar hello NewTek TriCaster codificador toosend una secuencia en directo de velocidad de bits única
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Este tema se muestra cómo hello tooconfigure [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live codificador toosend canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo. Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE). Esta herramienta solo se ejecuta en Windows PC. Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> Al usar Tricaster para el envío de una contribución fuente canales tooAMS que están habilitados para la codificación en directo, pueden producirse problemas de audio/vídeo en el evento en directo si se utilizan ciertas características de Tricaster, como cortar entre las fuentes de distribución rápida, o se modifica de pizarras . Hola AMS equipo está trabajando sobre cómo solucionar estos problemas, hasta entonces, es recomendable no toouse estas características.
>
>

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

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Especifique un nombre de canal, el campo de descripción de hello es opcional. En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTMP**. Puede dejar todas las demás opciones como están.

    Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.

3. Haga clic en **Crear canal**.

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> canal de Hello puede tardar tanto como toostart de 20 minutos.
>
>

Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo. Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Configurar Hola NewTek TriCaster codificador
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
1. Cree un nuevo proyecto de **NewTek TriCaster** según el origen de entrada de vídeo que se use.
2. Una vez dentro de ese proyecto, busque hello **flujo** botón y haga clic en hello engranaje icono siguiente tooit tooaccess hello secuencia menú Configuración.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Una vez que se abre el menú de hello, haga clic en **New** bajo el encabezado de conexión de Hola. Cuando se le solicite para el tipo de conexión de hello, seleccione **Adobe Flash**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. Haga clic en **Aceptar**.
5. Un perfil de FMLE ahora puede importarse, haga clic en hello desplegable flecha situada debajo **perfil Streaming** y navegar demasiado**examinar**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Navegue toowhere Hola configurado FMLE perfil se guardó.
7. Selecciónelo y presione **OK**(Aceptar).

    Cuando se carga el perfil de hello, continuar toohello siguiente paso.
8. Obtener dirección URL de entrada del canal de hello en orden tooassign, toohello Tricaster **RTMP extremo**.

    Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola. Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.

    Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Pegar esta información en hello **ubicación** campo **Flash Server** en proyecto de hello Tricaster. Asignar un nombre de la secuencia en hello **Id. del Streaming** campo.

    Si la información de la secuencia se ha agregado el perfil FMLE toohello, también se puede importar toothis sección haciendo clic en **importar la configuración**, navegar por toohello guarda FMLE perfil y haga clic en **Aceptar**. campos de Flash Server relevantes de Hello deben llenar con información de Hola desde FMLE.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. Cuando termine, haga clic en **Aceptar** final Hola de pantalla de bienvenida. Cuando las entradas de vídeo y audio en hello Tricaster están listos, empezar a transmitir tooAMS haciendo clic en hello **flujo** botón.

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Antes de hacer clic **flujo**, le **debe** Asegúrese de que el canal de hello está listo.
> Además, asegúrese de que no tooleave Hola canal en un estado listo sin una contribución entrada fuente durante más de 15 minutos de >.
>
>

## <a name="test-playback"></a>Prueba de reproducción
Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado. En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.

Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada. Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.  

## <a name="create-a-program"></a>Creación de un programa
1. Una vez confirmada la reproducción de canales, cree un programa. En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
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

## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
