---
title: aaaGet Started with Azure Mobile Engagement para Cordova/Phonegap
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para las aplicaciones de Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Introducción a Azure Mobile Engagement para Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand desarrollado su aplicación uso y envío inserción notificaciones toosegmented a los usuarios para una aplicación móvil con Cordova.

En este tutorial, se creará una aplicación de Cordova vacía usando Mac y, después, se integrará el SDK de Mobile Engagement. Recopila datos de análisis básicos y recibe notificaciones push usando Apple Push Notification System (APNS) para iOS y Google Cloud Messaging (GCM) para Android. Se implementará esta tooan dispositivo iOS o Android para las pruebas. 

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Este tutorial requiere siguiente de hello:

* XCode, que se puede instalar desde la tienda de aplicaciones de Mac (para la implementación de tooiOS)
* [Android SDK & emulador](http://developer.android.com/sdk/installing/index.html) (para la implementación de tooAndroid)
* Certificado de notificaciones push (.p12), que puede obtener en el centro de desarrolladores de Apple para APNS.
* Número de proyecto de GCM, que puede obtener en la consola de Google para desarrolladores para GCM.
* [Complemento Cordova para Mobile Engagement](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> Puede buscar código fuente de Hola y Hola Léame para el complemento de Cordova hello en [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Cordova
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "integración básica de" hello mínimo establecido toocollect requiere datos y enviar una notificación de inserción. 

Se creará una aplicación básica con la integración de hello toodemonstrate Cordova:

### <a name="create-a-new-cordova-project"></a>Creación de un nuevo proyecto de Cordova
1. Iniciar *Terminal* ventana en su Hola de máquina y el tipo de Mac después de que creará un nuevo proyecto de Cordova de plantilla predeterminada de Hola. Asegúrese de que la publicación Hola perfil que finalmente toodeploy de uso la aplicación de iOS usa 'com.mycompany.myapp' como Hola identificador de aplicación. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Ejecutar Hola después tooconfigure el proyecto para **iOS** y lo ejecuta en el simulador de iOS de hello:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Ejecutar Hola después tooconfigure el proyecto para **Android** y lo ejecuta en el emulador de Android Hola. Asegúrese de que la configuración del emulador de Android SDK tiene su destino como Google APIs (Google Inc.) con hello CPU / ABI como Google APIs ARM.  
   
        $ cordova platform add android
        $ cordova run android
4. Agregar Hola complemento Cordova Console. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar el backend de interacción de tooMobile de aplicación
1. Instale el complemento de Azure Mobile Engagement Cordova de hello proporcionando Hola valores de las variables tooconfigure Hola complemento:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Icono de llegar a Android* : debe ser Hola nombre de recurso de hello sin ninguna extensión, ni puede dibujar prefijo (p. ej: mynotificationicon), y se debe copiar el archivo de icono de hello en el proyecto de android (plataformas android/res/activa)

*iOS alcanzar icono* : debe ser Hola nombre de recurso de hello con su extensión (p. ej: mynotificationicon.png), y archivo de icono de hello debe agregarse al proyecto de iOS con XCode (mediante Hola menú de archivos de complemento)

## <a id="monitor"></a>Habilitar supervisión en tiempo real
1. En el proyecto de Cordova Hola - editar **www/js/index.js** tooadd llamada de hello tooMobile interacción toodeclare una nueva actividad una vez Hola *deviceReady* recibe el evento.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Ejecute la aplicación hello:
   
   * **Para iOS**
     
       En `Terminal` ventana inicie la aplicación en una nueva instancia de simulador ejecutando Hola siguientes:
     
           cordova run ios
   * **Para Android**
     
       En `Terminal` ventana inicie la aplicación en una nueva instancia de emulador ejecutando Hola siguientes:
     
           cordova run android
3. Puede ver la siguiente de hello en registros de la consola de hello:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de las notificaciones de inserción y mensajería en la aplicación
Mobile Engagement le permite toointeract con los usuarios mediante las notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hello las secciones siguientes se configurará la aplicación tooreceive ellos.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Configuración de las credenciales Push para Mobile Engagement
tooallow Mobile Engagement toosend notificaciones de inserción en su nombre, debe toogrant obtener acceso a tooyour el certificado de iOS de Apple o la clave de API de servidor de GCM. 

1. Navegue tooyour portal de interacción móvil. Asegúrese de que está en aplicación de hello se usa para este proyecto y, a continuación, haga clic en hello **implique** situado en la parte inferior de hello:
   
    ![][1]
2. Se colocará en la página de configuración de hello en el Portal de interacción. Desde allí, haga clic en hello **inserción nativa** sección:
   
    ![][2]
3. Configuración del certificado de iOS o la clave de API del servidor de GCM
   
    **[iOS]**
   
    a. Elija el certificado .p12, cárguelo y escriba la contraseña:
   
    ![][3]
   
    **[Android]**
   
    a. Haga clic en el icono de edición de hello delante del **clave de API** en la sección de configuración de GCM hello en ventana emergente de Hola que se muestra, pegue Hola GCM clave del servidor y haga clic en **Aceptar**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Habilitar las notificaciones de inserción en la aplicación de Cordova hello
Editar **www/js/index.js** tooadd Hola llamada tooMobile interacción toorequest notificaciones de inserción y declare un controlador:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Ejecutar aplicación hello
**[iOS]**

1. Se utilizará XCode toobuild e implementar aplicación hello en notificaciones de inserción de hello dispositivo tootest puesto que iOS permite solo dispositivo real de tooan de notificaciones de inserción. Vaya a ubicación toohello donde se crea el proyecto de Cordova y navegue demasiado**...\platforms\ios** ubicación. Abra el archivo .xcodeproj nativo de hello en XCode. 
2. Compilar e implementar hello Cordova aplicación toohello el dispositivo iOS con cuenta de hello que tiene el perfil que contiene el certificado de Hola que acaba de cargar hello Id. de aplicación que coincide con hello uno que proporcionó durante la creación y el portal de interacción móvil toohello de aprovisionamiento de Hola aplicación de Cordova Hello. Es posible desproteger hello *identificador de paquete* en su **recursos\*-info.plist** archivo en XCode toomatch seguridad. 
3. Verá el elemento emergente de iOS estándar de hello en el dispositivo que indica que la aplicación hello solicita las notificaciones de toosend de permiso. Conceda el permiso de Hola. 

**[Android]**

Puede usar simplemente aplicación Android de hello emulador toorun Hola tal y como se admiten las notificaciones de GCM en el emulador de Android Hola. 

    cordova run android

## <a id="send"></a>Enviar una aplicación de tooyour de notificación
Se creará una campaña de notificación de inserción simple que se va a enviar una aplicación de tooyour de inserción ejecuta en el dispositivo de hello:

1. Navegue toohello **alcanzar** ficha en el portal de interacción móvil
2. Haga clic en **nuevo anuncio** toocreate la campaña de inserción
   
    ![][6]
3. Proporcionar entradas toocreate la campaña **[Android]**
   
   * Proporcione un **Nombre** para la campaña. 
   * Seleccione hello **tipo de entrega** como *notificación del sistema* *Simple*
   * Seleccione hello **hora de entrega** como *"Cualquier hora"*
   * Proporcionar un **título** para la notificación que será la primera línea de Hola de inserción de Hola.
   * Proporcionar un **mensaje** para la notificación que servirá como cuerpo del mensaje Hola. 
     
     ![][11]
4. Proporcionar entradas toocreate la campaña **[iOS]**
   
   * Proporcione un **Nombre** para la campaña. 
   * Seleccione hello **hora de entrega** como *"fuera de la aplicación solo"*
   * Proporcionar un **título** para la notificación que será la primera línea de Hola de inserción de Hola.
   * Proporcionar un **mensaje** para la notificación que servirá como cuerpo del mensaje Hola. 
     
     ![][12]
5. Desplácese hacia abajo y, en hello seleccione sección contenido **solo notificación**
   
    ![][8]
6. [Opcional] También puede proporcionar la dirección URL de una acción. Asegúrese de que utiliza un esquema de dirección URL proporcionado durante la configuración del complemento de hello **AZME\_REDIRIGIR\_URL** variable p. ej. *myapp://test*.  
7. Ha terminado la posible de campaña más básica de configuración Hola. Ahora, desplácese hacia abajo en nuevo y haga clic en hello **crear** botón toosave la campaña.
8. Por último, **active** la campaña.
   
    ![][10]
9. Ahora verá una notificación push en el dispositivo o en el emulador como parte de esta campaña. 

## <a id="next-steps"></a>Pasos siguientes
[Información general de todos los métodos disponibles con el SDK de Mobile Engagement para Cordova](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

