---
title: "aaaConfigure Hola FMLE codificador toosend una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure Hola toosend de codificador de codificador de Live de medios de Flash (FMLE) a una velocidad de bits única secuencia tooAMS los canales que están habilitadas para la codificación en directo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Usar hello FMLE codificador toosend una secuencia en directo de velocidad de bits única
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

Este tema se muestra cómo hello tooconfigure [Flash Live el Codificador multimedia de](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) codificador toosend una velocidad de bits única transmitir canales tooAMS que están habilitados para la codificación en directo. Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE). Esta herramienta solo se ejecuta en Windows PC. Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

Tenga en cuenta que en este tutorial se describe el uso de AAC. Sin embargo, FMLE no es compatible con AAC de forma predeterminada. Deberá toopurchase un complemento para la codificación AAC como MainConcept: [AAC complemento](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

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

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Especifique un nombre de canal, el campo de descripción de hello es opcional. En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTMP**. Puede dejar todas las demás opciones como están.

    Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.

3. Haga clic en **Crear canal**.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> canal de Hello puede tardar tanto como toostart de 20 minutos.
>
>

Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo. Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Configurar el codificador de hello FMLE
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
1. Navegue toohello que Flash Live Codificador multimedia (FMLE) de la interfaz en la máquina de Hola que se utiliza.

    interfaz de Hello es una página principal de configuración. Tome nota de los siguientes Hola recomendadas configuración tooget a trabajar con la transmisión mediante FMLE.

   * Format (Formato): H.264, Frame Rate (Velocidad de fotogramas): 30.00
   * Input Size (Tamaño de entrada): 1280 x 720
   * Bit Rate (Velocidad de bits): 5000 kbps (se puede ajustar en función de las limitaciones de red)  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     Al usar entrelazado orígenes, por favor, marca de verificación Hola "Desentrelazar" opción
2. Seleccione Hola llave inglesa icono siguiente tooFormat, deben tener estos valores adicionales:

   * Profile (Perfil): Main (Principal)
   * Level (Nivel): 4.0
   * Keyframe Frequency (Frecuencia de fotogramas clave): 2 seconds (2 segundos)

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Establecer Hola después de la configuración de audio importante:

   * Format (Formato): AAC
   * Sample Rate (Frecuencia de muestreo): 44100 kHz
   * Bitrate (Velocidad de bits): 192 kbps

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Obtener dirección URL de entrada del canal de hello en orden tooassign, toohello FMLE **RTMP extremo**.

    Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola. Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.

    Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Pegar esta información en hello **FMS URL** campo de la sección de la salida de hello y asigne un nombre de la secuencia.

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    Para obtener redundancia adicional, repita estos pasos con hello secundaria de dirección URL de entrada.
6. Seleccione **Conectar**.

> [!IMPORTANT]
> Antes de hacer clic **conectar**, le **debe** Asegúrese de que el canal de hello está listo.
> Además, asegúrese de que no tooleave Hola canal en un estado listo sin una contribución entrada fuente durante más de 15 minutos de >.
>
>

## <a name="test-playback"></a>Prueba de reproducción

Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado. En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.

Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada. Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.  

## <a name="create-a-program"></a>Creación de un programa
1. Una vez confirmada la reproducción de canales, cree un programa. En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
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
