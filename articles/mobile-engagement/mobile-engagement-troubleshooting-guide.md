---
title: "aaaAzure guías de solución de problemas de interacción móvil"
description: "Guía de solución de problemas de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement: guía de solución de problemas
## <a name="introduction"></a>Introducción
Hola, siga a la Guía de solución de problemas le ayudará a comprender las causas raíz de algunos problemas habituales y se le permiten tootroubleshoot por su cuenta. 

## <a name="general"></a>General
En general, siempre debe asegurarse siguiente hello:

1. Asegúrese de que ha realizado todos los pasos de hello requeridas para la integración, como se describe en nuestro [tutoriales de introducción](mobile-engagement-windows-store-dotnet-get-started.md)
2. Está utilizando la versión más reciente de Hola de SDK de plataforma de Hola. 
3. Pruebe en un dispositivo real y un emulador porque algunos problemas son solo tooemulator específico. 
4. No supera los límites de Mobile Engagement que se indican [aquí](../azure-subscription-service-limits.md)
5. Si no se pueden tooconnect toohello Mobile Engagement servicio back-end o ver datos que no se cargan de forma continua, a continuación, asegúrese de que no hay ningún incidentes de servicio en curso activando [aquí](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>Problemas de 'Supervisar'
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>No veo mi dispositivo aparecen en la pestaña Monitor Hola
Ficha Monitor muestra la plataforma de Mobile Engagement de hello dispositivos conectados tooyour en tiempo real. Si depura en un emulador y un dispositivo, debe ver aquí al menos una sesión. Si se distribuye la aplicación hello, verá Hola sesiones activas medidor reflejar dispositivos Hola que son de la plataforma toohello conectado en tiempo real. 

Si no ve el dispositivo en la pestaña Monitor de hello, a continuación, probablemente es un problema de integración del SDK. Algunos tootroubleshoot tootake de pasos comunes son los siguientes:

1. Asegúrese de que utilizas cadena de conexión correcta de hello en aplicaciones móviles de Hola y está en la sección de claves SDK de Hola y sección Hola API claves no. cadena de conexión de Hola conecta a la instancia de toohello de aplicación móvil de la aplicación de interacción móvil de hello en el que podrá ver su dispositivo en la pestaña Monitor de Hola. 
2. Para la plataforma Windows - si la página invalida hello `OnNavigatedTo` /método siguiente, asegúrese de que toocall `base.OnNavigatedTo(e)`.
3. Si va a integrar Mobile Engagement en una aplicación móvil existente, también puede asegurarse de que no faltan todos los pasos examinando Hola avanzada pasos de integración [aquí](mobile-engagement-windows-store-integrate-engagement.md)
4. Asegúrese de que está enviando al menos una pantalla/actividad mediante la invalidación de la página de hello con EngagementActivity según la plataforma Hola trabaja tal y como se describe en hello [tutoriales de introducción a](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>Obtengo ficha del Monitor de Hola que muestra una sesión incluso cuando he desconectado o cerrado mi aplicación / emulador.
Si es una plataforma de toohello conectado hello en este momento y que usa una aplicación de hello emulador tooopen esto es probable debido tooemulator interpretación. En general, debe tooensure que se vuelven a estar toohello portada en el emulador de Hola para toodisconnect de sesión de aplicación Hola correctamente. Además, en la plataforma Windows, durante la depuración con Visual Studio, puede que necesite tooensure que en Visual Studio, vaya toohello **eventos de ciclo de vida de** barra de menús y haga clic en **Suspend** tooreally cerrar sesión de Hola. Consulte el [tutorial de Windows](mobile-engagement-windows-store-dotnet-get-started.md) para obtener más información. 

## <a name="analytics-issues"></a>Problemas de 'Análisis'
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>No veo ningún dato o datos actualizados en la pestaña Análisis
Los datos de análisis se recalculan periódicamente, pero la actualización puede tardar hasta 24 horas. No son datos en tiempo real y aparecerán actualizados en este margen de 24 horas.
Asegúrese de no obstante que va a enviar al menos una pantalla o actividad toohello plataforma back-end cualquier reemplazo al menos una página con `EngagementActivity` o llamando a `SendActivity` forma explícita. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Veo fecha/hora capturada de manera incorrecta para un dispositivo en la pestaña de análisis de Hola
Hello período de tiempo para el análisis se basa fecha hello de la configuración de dispositivo de los usuarios de Hola. Por tanto, asegúrese de que Hola dispositivo tiene fecha Hola ha configurado correctamente. 

## <a name="segment-issues"></a>Problemas de 'Segmento'
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>Creé un segmento y se muestra atenuado o no muestra ningún dato
Creación de segmento no es en tiempo real en el momento de Hola. Se calcula en hello que mismo tiempo que se agregan los datos de análisis de Hola y por lo que podría tardar hasta 24 horas. Debe comprobar volver más tarde, pero mientras tanto también debe asegurarse de que las aplicaciones móviles realmente envían datos Hola según Hola de los cuales son que forman los segmentos de Hola. Por ejemplo, Si un evento diga "foo" no está enviando a cualquier dispositivo móvil, a continuación, no tendría que haber ningún dato de segmento para un segmento creado con EventName = foo como criterio de Hola. También debe comprobar su tooensure de integración del SDK su aplicación móvil está enviando datos Hola correctamente. 

## <a name="reach-or-push-notifications-issues"></a>Problemas de 'Alcance' o de notificaciones push
### <a name="my-push-messages-are-not-being-delivered"></a>Los mensajes de inserción no se entregan
1. Vuelva a enviar las notificaciones tooa prueba dispositivo primera tooensure que todos los componentes de hello - aplicación móvil, servicio de SDK y Hola están conectados correctamente y pueda toodeliver notificaciones de inserción. 
2. Siempre enviar más sencillo Hola 'notificación de fuera de la aplicación' primero a través de una campaña que no está programada y ni tiene ningún criterio de audiencia especificado. Esto vuelve a tooprove que funciona correctamente la conectividad de notificación. 
3. Si experimenta problemas en la entrega de notificaciones de la aplicación también es un buen primer paso tootry enviar una notificación de fuera de la aplicación en primer lugar. 
4. Asegúrese de que hello 'Push' Native' está configurado correctamente para su aplicación móvil. Dependiendo de la plataforma de Hola o implicará claves (Android, Windows) o certificados (iOS). Consulte [Interfaz de usuario: configuración](mobile-engagement-user-interface-settings.md)
5. Fuera de la aplicación las notificaciones también pudieron estar bloqueadas por hello usuario a través de hello que SO móvil garantizar por lo que esto no sucede Hola. 
6. Asegúrese de que no va a establecer hello *omitir audiencia, dejarán de enviarse toousers a través de la API de hello* opción Hola **campaña** sección de un alcance de campaña porque así asegurará de que inserción notificaciones solo se envían a través de las API. 
7. Asegúrese de que se está probando la campaña de inserción con ambos un dispositivo conectado a través de Wi-Fi y phone operador tooeliminate Hola red conexión de red como un posible origen de problemas.
8. Asegurarse de que Hola sistema fecha y hora en el emulador de dispositivos es correcta porque cualquier dispositivo no está sincronizado también va a interferir con las notificaciones de hello servicio de notificaciones Push capacidad toodeliver. 

A continuación se incluyen instrucciones adicionales de solución de problemas específicas de plataforma:

1. **iOS** 
   
   * Asegúrese de que los certificados de hello son válidas y vigentes para iOS notificaciones de inserción. 
   * Asegúrese de que configura correctamente un certificado de *Producción* en la aplicación Mobile Engagement. 
   * Asegúrese de que se está probando en un *dispositivo físico real*. simulador de iOS de Hello no puede procesar mensajes de inserción.
   * Asegúrese de que Hola que identificador de paquete está configurado correctamente en la aplicación móvil de Hola. Consulte las instrucciones de hello [aquí](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Al probar, use la distribución "Ad Hoc" en el perfil de aprovisionamiento móvil. No será capaz de tooreceive notificación si la aplicación se compila utilizando "Debug"
2. **Android**
   
   * Asegúrese de que ha especificado el número correcto de proyecto de hello en el archivo AndroidManifest.xml la aplicación móvil que va seguido de caracteres \n. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Asegúrese de que no faltan o mal configurado ningún permiso en el archivo de manifiesto de Android hello 
   * Asegúrese de que número de proyecto de hello va a agregar la aplicación de cliente de tooyour es de hello misma cuenta donde obtuvo Hola GCM clave del servidor. Si hay alguna incoherencia entre Hola dos impedirá que su inserciones saliendo. 
   * Si recibe sistema notificaciones, pero no en la aplicación, a continuación, revise hello [especifica un icono para la sección notificaciones](mobile-engagement-android-get-started.md) como probablemente no está especificando el icono correcto de hello en el archivo de manifiesto de Android de Hola. 
   * Si va a enviar una notificación de BigPicture, garantizar que, si tiene servidores de imagen externos, a continuación, deben toobe capaz de toosupport HTTP "GET" y "HEAD".
3. **Windows**
   
   * Asegúrese de que se ha asociado la aplicación hello con una aplicación de tienda de Windows válida. En Visual Studio - tendrá tooright haga clic en proyecto de Hola y seleccione opción "Asociar aplicación con Store" y aplicación de hello select que creó en la tienda Windows hello. Esta aplicación de la tienda de Windows debe ser Hola uno mismo desde donde obtuvo tooconfigure de credenciales de inserción nativa de hello en el portal de interacción móvil Hola.
   * Si recibe notificaciones push fuera de aplicación pero no de aplicación con integración `EngagementOverlay` , asegúrese de que la página incluye un elemento de cuadrícula raíz en la página. EngagementOverlay utiliza el primer elemento de "Cuadrícula" Hola que busca en las vistas de web dos de tooadd de archivo de xaml en la página. Si desea toolocate donde se establecerá vistas web, puede definir una cuadrícula denominada "EngagementGrid" similar al siguiente, sin embargo, tendrá tooensure hay suficiente alto y ancho para hello dos posteriores web vistas que se muestran la notificación de Hola y Hola después anuncio como notificación en la aplicación:
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>He creado un notificación de inserción/anuncio/campaña e incluso después de que me envíe notificaciones de hello, se muestra como 'Active'. ¿Qué significa?
Hola **campaña** que creó en Mobile Engagement se denomina modo porque es un ejecución prolongada significado de notificación de inserción como plataforma de interacción móvil tooyour conectarán los dispositivos nuevos, se enviará automáticamente notificaciones de Hola en este caso, configure siempre y cuando se cumplen criterio Hola que se establecen en la campaña de Hola. No se trata de una configuración de notificación de un solo uso. Tendrá que toomanually haga clic en hello **finalizar** botón campaña de hello tooterminate para que no enviar más notificaciones. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>¿He creado una campaña de inserción y estoy recibiendo notificaciones correctamente sin embargo cada vez que se abre la aplicación hello, obtengo Hola misma notificación incluso cuando tuve ejecutados con anterioridad?
Es probable que toohappen durante las pruebas y si usas emuladores o algún marco de trabajo de prueba como TestFlight. ¿Qué sucede aquí es que en todas las aplicaciones de instancia de ejecución, es adquirir un nuevo Id. de dispositivo y enviarlo tooour back-end, que está causando tootreat de plataforma de Mobile Engagement Hola como un nuevo dispositivo y enviar notificaciones de Hola. 

## <a name="getting-support"></a>Obtención de soporte técnico
Si son problema de hello tooresolve no se puede, a continuación, hacer lo siguiente:

1. Busque su problema en los subprocesos existentes en el foro de StackOverflow hello y [foro de MSDN](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) y si no, a continuación, hacer una pregunta no existe. 
2. Si encuentra una característica que faltan, a continuación, agregar y vote por solicitud hello en nuestro [foro de UserVoice](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Si tiene Microsoft admite abierto un incidente de soporte técnico proporcionando Hola detalles siguientes: 
   * Identificador de suscripción de Azure
   * Plataforma (por ejemplo, iOS, Android, etc.)
   * Id. de aplicación
   * Identificador de campaña (para problemas con notificaciones push)
   * Id. de dispositivo
   * Versión de SDK de Mobile Engagement (por ejemplo, Android SDK v2.1.0)
   * Detalles del error con el mensaje de error exacto y el escenario

