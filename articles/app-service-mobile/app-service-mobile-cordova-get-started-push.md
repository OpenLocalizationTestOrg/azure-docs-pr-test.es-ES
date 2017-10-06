---
title: "Notificaciones de inserción de aaaAdd tooApache Cordova App con aplicaciones móviles de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo aplicaciones de Apache Cordova de tooyour de notificaciones de inserción de toouse toosend de aplicaciones móviles de Azure."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Agregar aplicación de Apache Cordova de tooyour de notificaciones de inserción
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregue un proyecto de toohello [inicio rápido de Apache Cordova] de notificaciones de inserción para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, necesita Hola paquete de extensión de notificación de inserción. Para obtener más información, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][1].

## <a name="prerequisites"></a>Requisitos previos
Este tutorial trata de una aplicación de Apache Cordova desarrollada con Visual Studio 2015 que se ejecuta en el emulador de Google Android hello, un dispositivo Android, un dispositivo de Windows y un dispositivo iOS.

toocomplete este tutorial, necesita:

* Un equipo con [Visual Studio Community 2015][2] o versiones posteriores.
* [Visual Studio Tools para Apache Cordova][4].
* Una [cuenta activa de Azure][3].
* Un proyecto de [inicio rápido de Apache Cordova][5] completado.
* (Android) Una [cuenta de Google][6] con una dirección de correo electrónico verificada.
* (iOS) La [pertenencia a un programa para desarrolladores de Apple][7] y un dispositivo iOS (el simulador de iOS no admite la inserción).
* (Windows) Una [cuenta de desarrollador para la Tienda Windows][8] y un dispositivo con Windows 10.

## <a name="configure-hub"></a>Configurar un Centro de notificaciones
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Ver un vídeo que muestra los pasos de esta sección][9]

## <a name="update-hello-server-project"></a>Actualizar el proyecto de servidor hello
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Modificación de la aplicación de Cordova
Asegúrese de que el proyecto de aplicación de Apache Cordova es notificaciones de inserción de listo toohandle instalar complemento de inserción de Cordova hello además de cualquier servicio de inserción específicos de la plataforma.

#### <a name="update-hello-cordova-version-in-your-project"></a>Actualizar la versión de Cordova hello en el proyecto.
Si el proyecto utiliza una versión anterior a v6.1.1 de Apache Cordova, actualice el proyecto de cliente de Hola. proyecto de Hola tooupdate:

* Haga clic en `config.xml` Diseñador de configuración de tooopen Hola.
* Seleccione la pestaña de plataformas de Hola.
* Elija 6.1.1 Hola **Cordova CLI** cuadro de texto.
* Elija **generar**, a continuación, **generar solución** proyecto de hello tooupdate.

#### <a name="install-hello-push-plugin"></a>Instalar el complemento de inserción de Hola
Las aplicaciones de Apache Cordova no controlan el dispositivo ni las funcionalidades de red de forma nativa.  Estas funcionalidades las proporcionan los complementos que se publican en [npm][10] o en GitHub.  Hola `phonegap-plugin-push` complemento es toohandle usa notificaciones de inserción de red.

Puede instalar el complemento de inserción de Hola en una de estas formas:

**Desde la línea de comandos hello:**

Ejecute el siguiente comando de hello:

    cordova plugin add phonegap-plugin-push

**Desde Visual Studio:**

1. En el Explorador de soluciones, abra hello `config.xml` archivo haga clic en **complementos** > **personalizado**, seleccione **Git** como el origen de instalación, a continuación, escriba `https://github.com/phonegap/phonegap-plugin-push`como origen de Hola.

   ![][img1]

2. Haga clic en el origen de instalación de hello flecha siguiente toohello.
3. En **SENDER_ID**, si ya tiene un identificador de proyecto numérico para el proyecto de Google Developers Console hello, puede agregarlo aquí. En caso contrario, escriba un valor de marcador de posición, como 777777.  Si su objetivo es Android, puede actualizar este valor en el archivo config.xml más adelante.
4. Haga clic en **Agregar**.

Hola inserción complemento ya está instalado.

#### <a name="install-hello-device-plugin"></a>Instalar el complemento de dispositivo de Hola
Seguimiento Hola mismo procedimiento que se usa el complemento de inserción de tooinstall Hola.  Agregar complemento de dispositivo de Hola desde la lista de complementos principales de hello (haga clic en **complementos** > **Core** toofind lo). Necesita este nombre de plataforma de complemento tooobtain Hola.

#### <a name="register-your-device-on-application-start-up"></a>Registro del dispositivo al inicio de la aplicación
Inicialmente, se incluirá el código mínimo para Android. Más adelante, modificar hello toorun de aplicación en iOS o Windows 10.

1. Agregue una llamada demasiado**registerForPushNotifications** durante la devolución de llamada de hello para el proceso de inicio de sesión de hello, o en parte inferior de Hola de hello **onDeviceReady** método:

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    Este ejemplo muestra la llamada a **registerForPushNotifications** después de que la autenticación se realiza correctamente.  Puede llamar a `registerForPushNotifications()` tantas veces como sea necesario.

2. Agregar nueva hello **registerForPushNotifications** método tal como se indica a continuación:

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. (Android) Hola anterior de código, reemplace `Your_Project_ID` con numérico Hola project Id. de la aplicación desde el [Google Developers Console][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Opcional) Configurar y ejecutar la aplicación hello en Android
Completar esta sección tooenable las notificaciones de inserción Android.

#### <a name="enable-gcm"></a>Habilitar la mensajería en la nube Firebase
Puesto que esperamos poner a su plataforma de Google Android Hola inicialmente, debe habilitar la mensajería de nube de Firebase.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Configurar Hola aplicación móvil back-end toosend inserción solicitudes que utilizan FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Configuración de una aplicación Cordova para Android
En la aplicación Cordova, abra el archivo config.xml y reemplace `Your_Project_ID` con numérico Hola project Id. de la aplicación de hello [Google Developers Console][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Abra index.js y actualice Hola código toouse el identificador numérico proyecto.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Configuración de un dispositivo Android para la depuración USB
Para poder implementar el dispositivo Android tooyour de aplicación, deberá tooenable depuración USB.  Realice los pasos siguientes en su teléfono Android:

1. Vaya demasiado**configuración** > **acerca del teléfono**, a continuación, puntee hello **número de compilación** hasta que se habilita el modo de desarrollador (aproximadamente siete veces).
2. En **configuración** > **opciones del desarrollador** habilitar **depuración USB**, a continuación, conecte el equipo de desarrollo de tooyour Teléfono Android con un Cable USB.

Cuando lo probamos, usamos un dispositivo Google Nexus 5X con Android 6.0 (Marshmallow).  Sin embargo, las técnicas de hello son comunes a cualquier versión de Android moderna.

#### <a name="install-google-play-services"></a>Instalación de Google Play Services
complemento de inserción de Hola se basa en Android servicios de Google Play para las notificaciones de inserción.

1. En Visual Studio, haga clic en **herramientas** > **Android** > **Administrador de Android SDK**, expanda hello **Extras** carpeta y verificación Hola cuadro toomake seguro de que cada uno de hello después SDK está instalado.

   * Android 2.3 o superior
   * Revisión de Google Repository 27 o superior
   * Google Play Services 9.0.2 o superior

2. Haga clic en **Install Packages** y espere Hola instalación toocomplete.

Hello actual requiere bibliotecas de aparecen en hello [documentación de la instalación de inserción de complemento de phonegap][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Notificaciones de inserción de prueba en la aplicación hello en Android
Ahora puede insertar elementos en la tabla TodoItem de Hola y aplicación Hola a notificaciones de inserción de prueba mediante la ejecución. Puede probar de Hola mismo dispositivo o desde otro dispositivo, siempre y cuando utilizas Hola mismo back-end. Probar la aplicación de Cordova en la plataforma Android hello en uno de hello siguientes maneras:

* **En un dispositivo físico:** conectar el equipo de desarrollo de dispositivos Android tooyour con un cable USB.  En lugar de **Emulador de Android de Google**, seleccione **Dispositivo**. Visual Studio implementa el dispositivo de toohello aplicación hello y, a continuación, ejecuta la aplicación hello.  A continuación, puede interactuar con la aplicación hello en dispositivo Hola.

  Mejore su experiencia de desarrollo.  Las aplicaciones de pantalla compartida, como [Mobizen][20] pueden ayudarle a desarrollar una aplicación Android.  Mobizen proyecta el Explorador de web tooa pantalla Android en su PC.

* **En un emulador de Android:** se requieren pasos de configuración adicionales cuando la ejecución se realiza en un emulador.

    Asegúrese de que se va a implementar tooa dispositivo virtual que tiene Google APIs establecer como destino de hello, tal como se muestra en el Administrador de dispositivos virtuales Android (AVD) Hola.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Si desea toouse una x86 más rápido emulador, [instalar el controlador HAXM de hello] [ 11] y configurar Hola emulador toouse lo.

    Agregar un dispositivo Android de Google cuenta toohello haciendo clic en **aplicaciones** > **configuración** > **Agregar cuenta**, siga las instrucciones de Hola.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Ejecutar la aplicación de todolist hello como antes e insertar un nuevo elemento de lista de tareas. Esta vez, se muestra un icono de notificación en el área de notificación de Hola. Puede abrir Hola notificación cajón tooview Hola texto completo de la notificación de Hola.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Optional) Configuración y ejecución en iOS
En esta sección es para ejecutar proyectos de Cordova Hola en dispositivos iOS. Puede omitir esta sección si no está trabajando con dispositivos iOS.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Instalación y ejecución Hola iOS remoto agente de compilación en un servicio de Mac o en la nube
Antes de poder ejecutar una aplicación de Cordova en iOS con Visual Studio, siga los pasos de Hola Hola [iOS Guía de instalación] [ 12] tooinstall y Hola ejecución remota de agente de compilación.

Asegúrese de que puede compilar la aplicación hello para iOS. Hello pasos descritos en la Guía de instalación de hello son toobuild necesario para iOS desde Visual Studio. Si no tiene un equipo Mac, puede compilar para iOS mediante el agente de compilación remoto hello en un servicio como MacInCloud. Para obtener más información, consulte [ejecutar la aplicación de iOS en la nube de hello][21].

> [!NOTE]
> XCode 7 o posterior es necesario toouse Hola inserción complemento en iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Buscar Hola identificador toouse como el identificador de la aplicación
Antes de registrar la aplicación para notificaciones de inserción, abra el archivo config.xml en su aplicación Cordova, busque hello `id` atributo valor de elemento de widget de Hola y cópielo para su uso posterior. Identificador de hello en Hola a continuación de XML es `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Posteriormente, utilice este identificador al crear un id. de aplicación en el portal para desarrolladores de Apple. Si crea un identificador de aplicación diferente en el portal para desarrolladores de hello, debe realizar algunos pasos adicionales más adelante en este tutorial. Id. de Hello en el elemento de widget debe coincidir con hello Id. de aplicación de portal para desarrolladores de Hola.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registrar la aplicación hello las notificaciones de inserción en el portal para desarrolladores de Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Visualización de un vídeo donde se muestren pasos similares](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Configurar notificaciones de inserción de Azure toosend
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Comprobación de que el id. de aplicación coincide con la aplicación de Cordova
Si Hola Id. de aplicación que creó en la cuenta de desarrollador de Apple ya coincide con Id. de hello del elemento de widget de hello en el archivo config.xml, puede omitir este paso. Sin embargo, si no coinciden los identificadores de hello, realizar Hola pasos:

1. Elimine la carpeta de plataformas de Hola desde el proyecto.
2. Elimine la carpeta de complementos de Hola desde el proyecto.
3. Eliminar carpeta de hello node_modules desde el proyecto.
4. Actualizar el atributo de Id. de Hola de elemento de widget de hello en config.xml toouse Hola Id. de aplicación que creó en la cuenta de desarrollador de Apple.
5. Vuelva a compilar el proyecto.

##### <a name="test-push-notifications-in-your-ios-app"></a>Prueba de las notificaciones push en su aplicación de iOS
1. En Visual Studio, asegúrese de que **iOS** está seleccionado como destino de la implementación de hello y, a continuación, elija **dispositivo** toorun en el dispositivo iOS conectado.

    Puede ejecutar en un tooyour de dispositivo conectado de iOS PC mediante iTunes. Simulador de iOS de Hello no admite notificaciones de inserción.

2. Hola presione **ejecutar** botón o **F5** en Visual Studio toobuild proyecto hello e inicio Hola aplicación en un dispositivo iOS, haga clic en **Aceptar** tooaccept notificaciones de inserción.

   > [!NOTE]
   > aplicación Hello solicita confirmación para las notificaciones de inserción durante Hola ejecuta por primera vez.

3. En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello más (+) icono.
4. Compruebe que una notificación se recibe, a continuación, haga clic en Aceptar toodismiss Hola notificación.

## <a name="optional-configure-and-run-on-windows"></a>(Optional) Configuración y ejecución en Windows
Esta sección es para ejecutar el proyecto de aplicación de Apache Cordova de hello en dispositivos Windows 10 (complemento de inserción de hello PhoneGap se admite en Windows 10). Puede omitir esta sección si no está trabajando con dispositivos Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Registro de la aplicación de Windows para notificaciones push con WNS
Opciones del almacén de hello toouse en Visual Studio, seleccione un destino de Windows de la lista de plataformas de solución de hello, como **Windows x64** o **Windows x86** (evitar **Windows AnyCPU** las notificaciones de inserción).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Visualización de un vídeo donde se muestren pasos similares][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Centro de notificaciones de Hola de configuración de WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Configurar las notificaciones de inserción de Windows de Cordova app toosupport
Diseñador de configuración de hello abierto (haga doble clic en el archivo config.xml y seleccione **Diseñador de vistas**), seleccione hello **Windows** y a **Windows 10** en **Versión de destino de windows**.

compilaciones de notificaciones de inserción de toosupport en su valor predeterminado (depurar), build.json abrir archivo. Copie la configuración de depuración de tooyour de configuración de "release".

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Después de la actualización de hello, hello build.json debe contener Hola siguiente código:

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

Compile la aplicación hello y compruebe que no dispone de ningún error. Ahora debe registrar la aplicación cliente para recibir notificaciones de hello del back-end de hello aplicación móvil. Repita esta sección para cada proyecto de Windows de la solución.

#### <a name="test-push-notifications-in-your-windows-app"></a>Prueba de las notificaciones push en su aplicación de Windows
En Visual Studio, asegúrese de que una plataforma de Windows está seleccionada como destino de implementación de hello, como **Windows x64** o **x86 Windows**. aplicación de hello toorun en un equipo con Windows 10 hospedaje de Visual Studio, elija **equipo Local**.

Presione Hola ejecutar botón toobuild Hola proyecto y de iniciar la aplicación hello.

En la aplicación hello, escriba un nombre para un todoitem nueva y, a continuación, haga clic en hello más (+) tooadd de icono.

Compruebe que se recibe una notificación cuando se agrega el elemento de saludo.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información sobre [centros de notificaciones] [ 17] toolearn acerca de las notificaciones de inserción.
* Si no lo ha hecho ya, continuar con tutorial Hola por [agregar autenticación] [ 14] tooyour aplicaciones de Apache Cordova.

Obtenga información acerca de cómo toouse Hola SDK.

* [SDK de Apache Cordova][15]
* [SDK de servidor ASP.NET][1]
* [SDK de servidor Node.js][16]

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
