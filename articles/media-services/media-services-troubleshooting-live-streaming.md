---
title: "Guía de aaaTroubleshooting de transmisión por secuencias en directo | Documentos de Microsoft"
description: "Este tema ofrece sugerencias sobre cómo tootroubleshoot live problemas de transmisión por secuencias."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Guía de solución de problemas para el streaming en vivo
Este tema ofrece sugerencias acerca de cómo tootroubleshoot algunas live streaming problemas.

## <a name="issues-related-tooon-premises-encoders"></a>Problemas relacionados con codificadores tooon locales
Esta sección proporciona sugerencias sobre cómo codificadores locales tooon relacionados de tootroubleshoot problemas que están configuración toosend canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo.

### <a name="problem-would-like-toosee-logs"></a>Problema: Desearía toosee registros
* **Posible problema**: no puede encontrar los registros del codificador que podrían ayudar en los problemas de depuración.
  
  * **Telestream Wirecast**: normalmente encontrará los registros en C:\Users\{username}\AppData\Roaming\Wirecast\ 
  * **Live elemental**: puede encontrar tiene toologs de vínculos en el portal de administración de Hola. Haga clic en **Estadísticas** y luego en **Registros**. En hello **archivos de registro** página, verá una lista de registros para todos los Hola AcontecimientoEnDirecto elementos; seleccione Hola una coincidencia de la sesión actual. 
  * **Flash el Codificador multimedia de Live**: puede encontrar Hola **directorio de registro...**  desplazándose toohello **registro codificación** ficha.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Problema: no hay ninguna opción para generar una secuencia progresiva
* **Problema potencial**: automáticamente no deshacer el entrelazado de codificador de Hola que se va a usar. 
  
    **Pasos para solucionar problemas**: buscar una opción entrelazada dentro de la interfaz del codificador Hola. Cuando se habilite la opción de eliminación de entrelazado, compruebe de nuevo la configuración de la salida progresiva. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Problema: Se intentó varias configuraciones de salida de codificador y tooconnect todavía no se puede.
* **Posible problema**: el canal de codificación Azure no se restableció correctamente. 
  
    **Pasos para solucionar problemas**: asegúrese de codificador de hello seguro ya no inserta tooAMS, detener y restablecer el canal de Hola. Una vez que se ejecuta de nuevo, intente conectarse su codificador con una nueva configuración de Hola. Si todavía no se soluciona el problema de hello, intente crear un nuevo canal completamente, en ocasiones, pueden dañarse los canales tras varios intentos fallidos.  
* **Problema potencial**: Hola GOP configuración de tamaño o fotograma clave no es óptimas. 
  
    **Pasos para solucionar problemas**: el intervalo de fotogramas clave o el tamaño de GOP recomendado es de 2 segundos. Algunos codificadores calculan esta configuración en el número de fotogramas, mientras que otros usan segundos. Por ejemplo: cuando se realizan envíos a 30fps, Hola tamaño GOP sería 60 marcos, que es equivalente too2 segundos.  
* **Problema potencial**: puertos estén cerrados están bloqueando el flujo de Hola. 
  
    **Pasos para solucionar problemas**: transmisión por secuencias a través de RTMP, compruebe el firewall o tooconfirm de configuración de proxy que estén abiertos los puertos de salida 1935 y 1936. Cuando se use el streaming de RTP, confirme que el puerto saliente 2010 está abierto. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Problema: Al configurar Hola codificador toostream con hello protocolo RTP, hay ningún lugar tooenter un nombre de host.
* **Problema potencial**: codificadores RTP muchas no permiten nombres de host y una dirección IP deberá toobe adquirido.  
  
    **Pasos para solucionar problemas**: toofind Hola dirección IP, abra un símbolo del sistema en cualquier equipo. toodo esto en Windows, abra Hola selector de ejecución (WIN + R) y escriba "cmd" tooopen.  
  
    Una vez abierto Hola símbolo del sistema, escriba "Ping [nombre de Host de AMS]". 
  
    nombre de host de Hello puede obtenerse mediante la omisión de número de puerto de Hola de hello URL de introducción de Azure, como se resalta en el siguiente ejemplo de Hola: 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Si, después de seguir los pasos de solución de problemas de Hola que todavía no se puede transmitir correctamente, envíe una incidencia de soporte técnico mediante Hola portal de Azure.
> 
> 

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

