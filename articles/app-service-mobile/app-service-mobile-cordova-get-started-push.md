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
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="392ef-103">Agregar aplicación de Apache Cordova de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="392ef-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="392ef-104">Información general</span><span class="sxs-lookup"><span data-stu-id="392ef-104">Overview</span></span>
<span data-ttu-id="392ef-105">En este tutorial, agregue un proyecto de toohello [inicio rápido de Apache Cordova] de notificaciones de inserción para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="392ef-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="392ef-106">Si no usa Hola descarga el proyecto de servidor de inicio rápido, necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="392ef-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="392ef-107">Para obtener más información, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][1].</span><span class="sxs-lookup"><span data-stu-id="392ef-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="392ef-108"><a name="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="392ef-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="392ef-109">Este tutorial trata de una aplicación de Apache Cordova desarrollada con Visual Studio 2015 que se ejecuta en el emulador de Google Android hello, un dispositivo Android, un dispositivo de Windows y un dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="392ef-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="392ef-110">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="392ef-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="392ef-111">Un equipo con [Visual Studio Community 2015][2] o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="392ef-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="392ef-112">[Visual Studio Tools para Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="392ef-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="392ef-113">Una [cuenta activa de Azure][3].</span><span class="sxs-lookup"><span data-stu-id="392ef-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="392ef-114">Un proyecto de [inicio rápido de Apache Cordova][5] completado.</span><span class="sxs-lookup"><span data-stu-id="392ef-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="392ef-115">(Android) Una [cuenta de Google][6] con una dirección de correo electrónico verificada.</span><span class="sxs-lookup"><span data-stu-id="392ef-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="392ef-116">(iOS) La [pertenencia a un programa para desarrolladores de Apple][7] y un dispositivo iOS (el simulador de iOS no admite la inserción).</span><span class="sxs-lookup"><span data-stu-id="392ef-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="392ef-117">(Windows) Una [cuenta de desarrollador para la Tienda Windows][8] y un dispositivo con Windows 10.</span><span class="sxs-lookup"><span data-stu-id="392ef-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="392ef-118"><a name="configure-hub"></a>Configurar un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="392ef-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="392ef-119">[Ver un vídeo que muestra los pasos de esta sección][9]</span><span class="sxs-lookup"><span data-stu-id="392ef-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="392ef-120">Actualizar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="392ef-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="392ef-121"><a name="add-push-to-app"></a>Modificación de la aplicación de Cordova</span><span class="sxs-lookup"><span data-stu-id="392ef-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="392ef-122">Asegúrese de que el proyecto de aplicación de Apache Cordova es notificaciones de inserción de listo toohandle instalar complemento de inserción de Cordova hello además de cualquier servicio de inserción específicos de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="392ef-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="392ef-123">Actualizar la versión de Cordova hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="392ef-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="392ef-124">Si el proyecto utiliza una versión anterior a v6.1.1 de Apache Cordova, actualice el proyecto de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="392ef-125">proyecto de Hola tooupdate:</span><span class="sxs-lookup"><span data-stu-id="392ef-125">tooupdate hello project:</span></span>

* <span data-ttu-id="392ef-126">Haga clic en `config.xml` Diseñador de configuración de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="392ef-127">Seleccione la pestaña de plataformas de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="392ef-128">Elija 6.1.1 Hola **Cordova CLI** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="392ef-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="392ef-129">Elija **generar**, a continuación, **generar solución** proyecto de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="392ef-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="392ef-130">Instalar el complemento de inserción de Hola</span><span class="sxs-lookup"><span data-stu-id="392ef-130">Install hello push plugin</span></span>
<span data-ttu-id="392ef-131">Las aplicaciones de Apache Cordova no controlan el dispositivo ni las funcionalidades de red de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="392ef-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="392ef-132">Estas funcionalidades las proporcionan los complementos que se publican en [npm][10] o en GitHub.</span><span class="sxs-lookup"><span data-stu-id="392ef-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="392ef-133">Hola `phonegap-plugin-push` complemento es toohandle usa notificaciones de inserción de red.</span><span class="sxs-lookup"><span data-stu-id="392ef-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="392ef-134">Puede instalar el complemento de inserción de Hola en una de estas formas:</span><span class="sxs-lookup"><span data-stu-id="392ef-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="392ef-135">**Desde la línea de comandos hello:**</span><span class="sxs-lookup"><span data-stu-id="392ef-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="392ef-136">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="392ef-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="392ef-137">**Desde Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="392ef-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="392ef-138">En el Explorador de soluciones, abra hello `config.xml` archivo haga clic en **complementos** > **personalizado**, seleccione **Git** como el origen de instalación, a continuación, escriba `https://github.com/phonegap/phonegap-plugin-push`como origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="392ef-139">Haga clic en el origen de instalación de hello flecha siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="392ef-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="392ef-140">En **SENDER_ID**, si ya tiene un identificador de proyecto numérico para el proyecto de Google Developers Console hello, puede agregarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="392ef-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="392ef-141">En caso contrario, escriba un valor de marcador de posición, como 777777.</span><span class="sxs-lookup"><span data-stu-id="392ef-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="392ef-142">Si su objetivo es Android, puede actualizar este valor en el archivo config.xml más adelante.</span><span class="sxs-lookup"><span data-stu-id="392ef-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="392ef-143">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="392ef-143">Click **Add**.</span></span>

<span data-ttu-id="392ef-144">Hola inserción complemento ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="392ef-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="392ef-145">Instalar el complemento de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="392ef-145">Install hello device plugin</span></span>
<span data-ttu-id="392ef-146">Seguimiento Hola mismo procedimiento que se usa el complemento de inserción de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="392ef-147">Agregar complemento de dispositivo de Hola desde la lista de complementos principales de hello (haga clic en **complementos** > **Core** toofind lo).</span><span class="sxs-lookup"><span data-stu-id="392ef-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="392ef-148">Necesita este nombre de plataforma de complemento tooobtain Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="392ef-149">Registro del dispositivo al inicio de la aplicación</span><span class="sxs-lookup"><span data-stu-id="392ef-149">Register your device on application start-up</span></span>
<span data-ttu-id="392ef-150">Inicialmente, se incluirá el código mínimo para Android.</span><span class="sxs-lookup"><span data-stu-id="392ef-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="392ef-151">Más adelante, modificar hello toorun de aplicación en iOS o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="392ef-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="392ef-152">Agregue una llamada demasiado**registerForPushNotifications** durante la devolución de llamada de hello para el proceso de inicio de sesión de hello, o en parte inferior de Hola de hello **onDeviceReady** método:</span><span class="sxs-lookup"><span data-stu-id="392ef-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

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

    <span data-ttu-id="392ef-153">Este ejemplo muestra la llamada a **registerForPushNotifications** después de que la autenticación se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="392ef-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="392ef-154">Puede llamar a `registerForPushNotifications()` tantas veces como sea necesario.</span><span class="sxs-lookup"><span data-stu-id="392ef-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="392ef-155">Agregar nueva hello **registerForPushNotifications** método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="392ef-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

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
3. <span data-ttu-id="392ef-156">(Android) Hola anterior de código, reemplace `Your_Project_ID` con numérico Hola project Id. de la aplicación desde el [Google Developers Console][18].</span><span class="sxs-lookup"><span data-stu-id="392ef-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="392ef-157">(Opcional) Configurar y ejecutar la aplicación hello en Android</span><span class="sxs-lookup"><span data-stu-id="392ef-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="392ef-158">Completar esta sección tooenable las notificaciones de inserción Android.</span><span class="sxs-lookup"><span data-stu-id="392ef-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="392ef-159"><a name="enable-gcm"></a>Habilitar la mensajería en la nube Firebase</span><span class="sxs-lookup"><span data-stu-id="392ef-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="392ef-160">Puesto que esperamos poner a su plataforma de Google Android Hola inicialmente, debe habilitar la mensajería de nube de Firebase.</span><span class="sxs-lookup"><span data-stu-id="392ef-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="392ef-161"><a name="configure-backend"></a>Configurar Hola aplicación móvil back-end toosend inserción solicitudes que utilizan FCM</span><span class="sxs-lookup"><span data-stu-id="392ef-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="392ef-162">Configuración de una aplicación Cordova para Android</span><span class="sxs-lookup"><span data-stu-id="392ef-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="392ef-163">En la aplicación Cordova, abra el archivo config.xml y reemplace `Your_Project_ID` con numérico Hola project Id. de la aplicación de hello [Google Developers Console][18].</span><span class="sxs-lookup"><span data-stu-id="392ef-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="392ef-164">Abra index.js y actualice Hola código toouse el identificador numérico proyecto.</span><span class="sxs-lookup"><span data-stu-id="392ef-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="392ef-165"><a name="configure-device"></a>Configuración de un dispositivo Android para la depuración USB</span><span class="sxs-lookup"><span data-stu-id="392ef-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="392ef-166">Para poder implementar el dispositivo Android tooyour de aplicación, deberá tooenable depuración USB.</span><span class="sxs-lookup"><span data-stu-id="392ef-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="392ef-167">Realice los pasos siguientes en su teléfono Android:</span><span class="sxs-lookup"><span data-stu-id="392ef-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="392ef-168">Vaya demasiado**configuración** > **acerca del teléfono**, a continuación, puntee hello **número de compilación** hasta que se habilita el modo de desarrollador (aproximadamente siete veces).</span><span class="sxs-lookup"><span data-stu-id="392ef-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="392ef-169">En **configuración** > **opciones del desarrollador** habilitar **depuración USB**, a continuación, conecte el equipo de desarrollo de tooyour Teléfono Android con un Cable USB.</span><span class="sxs-lookup"><span data-stu-id="392ef-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="392ef-170">Cuando lo probamos, usamos un dispositivo Google Nexus 5X con Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="392ef-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="392ef-171">Sin embargo, las técnicas de hello son comunes a cualquier versión de Android moderna.</span><span class="sxs-lookup"><span data-stu-id="392ef-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="392ef-172">Instalación de Google Play Services</span><span class="sxs-lookup"><span data-stu-id="392ef-172">Install Google Play Services</span></span>
<span data-ttu-id="392ef-173">complemento de inserción de Hola se basa en Android servicios de Google Play para las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="392ef-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="392ef-174">En Visual Studio, haga clic en **herramientas** > **Android** > **Administrador de Android SDK**, expanda hello **Extras** carpeta y verificación Hola cuadro toomake seguro de que cada uno de hello después SDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="392ef-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="392ef-175">Android 2.3 o superior</span><span class="sxs-lookup"><span data-stu-id="392ef-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="392ef-176">Revisión de Google Repository 27 o superior</span><span class="sxs-lookup"><span data-stu-id="392ef-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="392ef-177">Google Play Services 9.0.2 o superior</span><span class="sxs-lookup"><span data-stu-id="392ef-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="392ef-178">Haga clic en **Install Packages** y espere Hola instalación toocomplete.</span><span class="sxs-lookup"><span data-stu-id="392ef-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="392ef-179">Hello actual requiere bibliotecas de aparecen en hello [documentación de la instalación de inserción de complemento de phonegap][19].</span><span class="sxs-lookup"><span data-stu-id="392ef-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="392ef-180">Notificaciones de inserción de prueba en la aplicación hello en Android</span><span class="sxs-lookup"><span data-stu-id="392ef-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="392ef-181">Ahora puede insertar elementos en la tabla TodoItem de Hola y aplicación Hola a notificaciones de inserción de prueba mediante la ejecución.</span><span class="sxs-lookup"><span data-stu-id="392ef-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="392ef-182">Puede probar de Hola mismo dispositivo o desde otro dispositivo, siempre y cuando utilizas Hola mismo back-end.</span><span class="sxs-lookup"><span data-stu-id="392ef-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="392ef-183">Probar la aplicación de Cordova en la plataforma Android hello en uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="392ef-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="392ef-184">**En un dispositivo físico:** conectar el equipo de desarrollo de dispositivos Android tooyour con un cable USB.</span><span class="sxs-lookup"><span data-stu-id="392ef-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="392ef-185">En lugar de **Emulador de Android de Google**, seleccione **Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="392ef-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="392ef-186">Visual Studio implementa el dispositivo de toohello aplicación hello y, a continuación, ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="392ef-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="392ef-187">A continuación, puede interactuar con la aplicación hello en dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="392ef-188">Mejore su experiencia de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="392ef-188">Improve your development experience.</span></span>  <span data-ttu-id="392ef-189">Las aplicaciones de pantalla compartida, como [Mobizen][20] pueden ayudarle a desarrollar una aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="392ef-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="392ef-190">Mobizen proyecta el Explorador de web tooa pantalla Android en su PC.</span><span class="sxs-lookup"><span data-stu-id="392ef-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="392ef-191">**En un emulador de Android:** se requieren pasos de configuración adicionales cuando la ejecución se realiza en un emulador.</span><span class="sxs-lookup"><span data-stu-id="392ef-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="392ef-192">Asegúrese de que se va a implementar tooa dispositivo virtual que tiene Google APIs establecer como destino de hello, tal como se muestra en el Administrador de dispositivos virtuales Android (AVD) Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="392ef-193">Si desea toouse una x86 más rápido emulador, [instalar el controlador HAXM de hello] [ 11] y configurar Hola emulador toouse lo.</span><span class="sxs-lookup"><span data-stu-id="392ef-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="392ef-194">Agregar un dispositivo Android de Google cuenta toohello haciendo clic en **aplicaciones** > **configuración** > **Agregar cuenta**, siga las instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="392ef-195">Ejecutar la aplicación de todolist hello como antes e insertar un nuevo elemento de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="392ef-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="392ef-196">Esta vez, se muestra un icono de notificación en el área de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="392ef-197">Puede abrir Hola notificación cajón tooview Hola texto completo de la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="392ef-198">(Optional) Configuración y ejecución en iOS</span><span class="sxs-lookup"><span data-stu-id="392ef-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="392ef-199">En esta sección es para ejecutar proyectos de Cordova Hola en dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="392ef-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="392ef-200">Puede omitir esta sección si no está trabajando con dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="392ef-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="392ef-201">Instalación y ejecución Hola iOS remoto agente de compilación en un servicio de Mac o en la nube</span><span class="sxs-lookup"><span data-stu-id="392ef-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="392ef-202">Antes de poder ejecutar una aplicación de Cordova en iOS con Visual Studio, siga los pasos de Hola Hola [iOS Guía de instalación] [ 12] tooinstall y Hola ejecución remota de agente de compilación.</span><span class="sxs-lookup"><span data-stu-id="392ef-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="392ef-203">Asegúrese de que puede compilar la aplicación hello para iOS.</span><span class="sxs-lookup"><span data-stu-id="392ef-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="392ef-204">Hello pasos descritos en la Guía de instalación de hello son toobuild necesario para iOS desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="392ef-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="392ef-205">Si no tiene un equipo Mac, puede compilar para iOS mediante el agente de compilación remoto hello en un servicio como MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="392ef-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="392ef-206">Para obtener más información, consulte [ejecutar la aplicación de iOS en la nube de hello][21].</span><span class="sxs-lookup"><span data-stu-id="392ef-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="392ef-207">XCode 7 o posterior es necesario toouse Hola inserción complemento en iOS.</span><span class="sxs-lookup"><span data-stu-id="392ef-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="392ef-208">Buscar Hola identificador toouse como el identificador de la aplicación</span><span class="sxs-lookup"><span data-stu-id="392ef-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="392ef-209">Antes de registrar la aplicación para notificaciones de inserción, abra el archivo config.xml en su aplicación Cordova, busque hello `id` atributo valor de elemento de widget de Hola y cópielo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="392ef-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="392ef-210">Identificador de hello en Hola a continuación de XML es `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="392ef-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="392ef-211">Posteriormente, utilice este identificador al crear un id. de aplicación en el portal para desarrolladores de Apple.</span><span class="sxs-lookup"><span data-stu-id="392ef-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="392ef-212">Si crea un identificador de aplicación diferente en el portal para desarrolladores de hello, debe realizar algunos pasos adicionales más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="392ef-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="392ef-213">Id. de Hello en el elemento de widget debe coincidir con hello Id. de aplicación de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="392ef-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="392ef-214">Registrar la aplicación hello las notificaciones de inserción en el portal para desarrolladores de Apple</span><span class="sxs-lookup"><span data-stu-id="392ef-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="392ef-215">Visualización de un vídeo donde se muestren pasos similares</span><span class="sxs-lookup"><span data-stu-id="392ef-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="392ef-216">Configurar notificaciones de inserción de Azure toosend</span><span class="sxs-lookup"><span data-stu-id="392ef-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="392ef-217">Comprobación de que el id. de aplicación coincide con la aplicación de Cordova</span><span class="sxs-lookup"><span data-stu-id="392ef-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="392ef-218">Si Hola Id. de aplicación que creó en la cuenta de desarrollador de Apple ya coincide con Id. de hello del elemento de widget de hello en el archivo config.xml, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="392ef-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="392ef-219">Sin embargo, si no coinciden los identificadores de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="392ef-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="392ef-220">Elimine la carpeta de plataformas de Hola desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="392ef-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="392ef-221">Elimine la carpeta de complementos de Hola desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="392ef-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="392ef-222">Eliminar carpeta de hello node_modules desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="392ef-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="392ef-223">Actualizar el atributo de Id. de Hola de elemento de widget de hello en config.xml toouse Hola Id. de aplicación que creó en la cuenta de desarrollador de Apple.</span><span class="sxs-lookup"><span data-stu-id="392ef-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="392ef-224">Vuelva a compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="392ef-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="392ef-225">Prueba de las notificaciones push en su aplicación de iOS</span><span class="sxs-lookup"><span data-stu-id="392ef-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="392ef-226">En Visual Studio, asegúrese de que **iOS** está seleccionado como destino de la implementación de hello y, a continuación, elija **dispositivo** toorun en el dispositivo iOS conectado.</span><span class="sxs-lookup"><span data-stu-id="392ef-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="392ef-227">Puede ejecutar en un tooyour de dispositivo conectado de iOS PC mediante iTunes.</span><span class="sxs-lookup"><span data-stu-id="392ef-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="392ef-228">Simulador de iOS de Hello no admite notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="392ef-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="392ef-229">Hola presione **ejecutar** botón o **F5** en Visual Studio toobuild proyecto hello e inicio Hola aplicación en un dispositivo iOS, haga clic en **Aceptar** tooaccept notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="392ef-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="392ef-230">aplicación Hello solicita confirmación para las notificaciones de inserción durante Hola ejecuta por primera vez.</span><span class="sxs-lookup"><span data-stu-id="392ef-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="392ef-231">En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello más (+) icono.</span><span class="sxs-lookup"><span data-stu-id="392ef-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="392ef-232">Compruebe que una notificación se recibe, a continuación, haga clic en Aceptar toodismiss Hola notificación.</span><span class="sxs-lookup"><span data-stu-id="392ef-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="392ef-233">(Optional) Configuración y ejecución en Windows</span><span class="sxs-lookup"><span data-stu-id="392ef-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="392ef-234">Esta sección es para ejecutar el proyecto de aplicación de Apache Cordova de hello en dispositivos Windows 10 (complemento de inserción de hello PhoneGap se admite en Windows 10).</span><span class="sxs-lookup"><span data-stu-id="392ef-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="392ef-235">Puede omitir esta sección si no está trabajando con dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="392ef-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="392ef-236">Registro de la aplicación de Windows para notificaciones push con WNS</span><span class="sxs-lookup"><span data-stu-id="392ef-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="392ef-237">Opciones del almacén de hello toouse en Visual Studio, seleccione un destino de Windows de la lista de plataformas de solución de hello, como **Windows x64** o **Windows x86** (evitar **Windows AnyCPU** las notificaciones de inserción).</span><span class="sxs-lookup"><span data-stu-id="392ef-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="392ef-238">[Visualización de un vídeo donde se muestren pasos similares][13]</span><span class="sxs-lookup"><span data-stu-id="392ef-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="392ef-239">Centro de notificaciones de Hola de configuración de WNS</span><span class="sxs-lookup"><span data-stu-id="392ef-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="392ef-240">Configurar las notificaciones de inserción de Windows de Cordova app toosupport</span><span class="sxs-lookup"><span data-stu-id="392ef-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="392ef-241">Diseñador de configuración de hello abierto (haga doble clic en el archivo config.xml y seleccione **Diseñador de vistas**), seleccione hello **Windows** y a **Windows 10** en **Versión de destino de windows**.</span><span class="sxs-lookup"><span data-stu-id="392ef-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="392ef-242">compilaciones de notificaciones de inserción de toosupport en su valor predeterminado (depurar), build.json abrir archivo.</span><span class="sxs-lookup"><span data-stu-id="392ef-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="392ef-243">Copie la configuración de depuración de tooyour de configuración de "release".</span><span class="sxs-lookup"><span data-stu-id="392ef-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="392ef-244">Después de la actualización de hello, hello build.json debe contener Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="392ef-244">After hello update, hello build.json should contain hello following code:</span></span>

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

<span data-ttu-id="392ef-245">Compile la aplicación hello y compruebe que no dispone de ningún error.</span><span class="sxs-lookup"><span data-stu-id="392ef-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="392ef-246">Ahora debe registrar la aplicación cliente para recibir notificaciones de hello del back-end de hello aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="392ef-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="392ef-247">Repita esta sección para cada proyecto de Windows de la solución.</span><span class="sxs-lookup"><span data-stu-id="392ef-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="392ef-248">Prueba de las notificaciones push en su aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="392ef-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="392ef-249">En Visual Studio, asegúrese de que una plataforma de Windows está seleccionada como destino de implementación de hello, como **Windows x64** o **x86 Windows**.</span><span class="sxs-lookup"><span data-stu-id="392ef-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="392ef-250">aplicación de hello toorun en un equipo con Windows 10 hospedaje de Visual Studio, elija **equipo Local**.</span><span class="sxs-lookup"><span data-stu-id="392ef-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="392ef-251">Presione Hola ejecutar botón toobuild Hola proyecto y de iniciar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="392ef-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="392ef-252">En la aplicación hello, escriba un nombre para un todoitem nueva y, a continuación, haga clic en hello más (+) tooadd de icono.</span><span class="sxs-lookup"><span data-stu-id="392ef-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="392ef-253">Compruebe que se recibe una notificación cuando se agrega el elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="392ef-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="392ef-254"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="392ef-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="392ef-255">Obtenga información sobre [centros de notificaciones] [ 17] toolearn acerca de las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="392ef-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="392ef-256">Si no lo ha hecho ya, continuar con tutorial Hola por [agregar autenticación] [ 14] tooyour aplicaciones de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="392ef-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="392ef-257">Obtenga información acerca de cómo toouse Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="392ef-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="392ef-258">[SDK de Apache Cordova][15]</span><span class="sxs-lookup"><span data-stu-id="392ef-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="392ef-259">[SDK de servidor ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="392ef-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="392ef-260">[SDK de servidor Node.js][16]</span><span class="sxs-lookup"><span data-stu-id="392ef-260">[Node.js Server SDK][16]</span></span>

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
