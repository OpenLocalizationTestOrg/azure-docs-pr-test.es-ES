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
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="1bf28-103">Introducción a Azure Mobile Engagement para Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="1bf28-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="1bf28-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand desarrollado su aplicación uso y envío inserción notificaciones toosegmented a los usuarios para una aplicación móvil con Cordova.</span><span class="sxs-lookup"><span data-stu-id="1bf28-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="1bf28-105">En este tutorial, se creará una aplicación de Cordova vacía usando Mac y, después, se integrará el SDK de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1bf28-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="1bf28-106">Recopila datos de análisis básicos y recibe notificaciones push usando Apple Push Notification System (APNS) para iOS y Google Cloud Messaging (GCM) para Android.</span><span class="sxs-lookup"><span data-stu-id="1bf28-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="1bf28-107">Se implementará esta tooan dispositivo iOS o Android para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="1bf28-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bf28-108">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf28-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1bf28-109">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1bf28-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1bf28-110">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="1bf28-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="1bf28-111">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="1bf28-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="1bf28-112">XCode, que se puede instalar desde la tienda de aplicaciones de Mac (para la implementación de tooiOS)</span><span class="sxs-lookup"><span data-stu-id="1bf28-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="1bf28-113">[Android SDK & emulador](http://developer.android.com/sdk/installing/index.html) (para la implementación de tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="1bf28-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="1bf28-114">Certificado de notificaciones push (.p12), que puede obtener en el centro de desarrolladores de Apple para APNS.</span><span class="sxs-lookup"><span data-stu-id="1bf28-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="1bf28-115">Número de proyecto de GCM, que puede obtener en la consola de Google para desarrolladores para GCM.</span><span class="sxs-lookup"><span data-stu-id="1bf28-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="1bf28-116">Complemento Cordova para Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bf28-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="1bf28-117">Puede buscar código fuente de Hola y Hola Léame para el complemento de Cordova hello en [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="1bf28-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="1bf28-118"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Cordova</span><span class="sxs-lookup"><span data-stu-id="1bf28-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="1bf28-119"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bf28-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="1bf28-120">Este tutorial presenta una "integración básica de" hello mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="1bf28-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="1bf28-121">Se creará una aplicación básica con la integración de hello toodemonstrate Cordova:</span><span class="sxs-lookup"><span data-stu-id="1bf28-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="1bf28-122">Creación de un nuevo proyecto de Cordova</span><span class="sxs-lookup"><span data-stu-id="1bf28-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="1bf28-123">Iniciar *Terminal* ventana en su Hola de máquina y el tipo de Mac después de que creará un nuevo proyecto de Cordova de plantilla predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="1bf28-124">Asegúrese de que la publicación Hola perfil que finalmente toodeploy de uso la aplicación de iOS usa 'com.mycompany.myapp' como Hola identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1bf28-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="1bf28-125">Ejecutar Hola después tooconfigure el proyecto para **iOS** y lo ejecuta en el simulador de iOS de hello:</span><span class="sxs-lookup"><span data-stu-id="1bf28-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="1bf28-126">Ejecutar Hola después tooconfigure el proyecto para **Android** y lo ejecuta en el emulador de Android Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="1bf28-127">Asegúrese de que la configuración del emulador de Android SDK tiene su destino como Google APIs (Google Inc.) con hello CPU / ABI como Google APIs ARM.</span><span class="sxs-lookup"><span data-stu-id="1bf28-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="1bf28-128">Agregar Hola complemento Cordova Console.</span><span class="sxs-lookup"><span data-stu-id="1bf28-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="1bf28-129">Conectar el backend de interacción de tooMobile de aplicación</span><span class="sxs-lookup"><span data-stu-id="1bf28-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="1bf28-130">Instale el complemento de Azure Mobile Engagement Cordova de hello proporcionando Hola valores de las variables tooconfigure Hola complemento:</span><span class="sxs-lookup"><span data-stu-id="1bf28-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="1bf28-131">*Icono de llegar a Android* : debe ser Hola nombre de recurso de hello sin ninguna extensión, ni puede dibujar prefijo (p. ej: mynotificationicon), y se debe copiar el archivo de icono de hello en el proyecto de android (plataformas android/res/activa)</span><span class="sxs-lookup"><span data-stu-id="1bf28-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="1bf28-132">*iOS alcanzar icono* : debe ser Hola nombre de recurso de hello con su extensión (p. ej: mynotificationicon.png), y archivo de icono de hello debe agregarse al proyecto de iOS con XCode (mediante Hola menú de archivos de complemento)</span><span class="sxs-lookup"><span data-stu-id="1bf28-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="1bf28-133"><a id="monitor"></a>Habilitar supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="1bf28-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="1bf28-134">En el proyecto de Cordova Hola - editar **www/js/index.js** tooadd llamada de hello tooMobile interacción toodeclare una nueva actividad una vez Hola *deviceReady* recibe el evento.</span><span class="sxs-lookup"><span data-stu-id="1bf28-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="1bf28-135">Ejecute la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="1bf28-135">Run hello application:</span></span>
   
   * <span data-ttu-id="1bf28-136">**Para iOS**</span><span class="sxs-lookup"><span data-stu-id="1bf28-136">**For iOS**</span></span>
     
       <span data-ttu-id="1bf28-137">En `Terminal` ventana inicie la aplicación en una nueva instancia de simulador ejecutando Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1bf28-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="1bf28-138">**Para Android**</span><span class="sxs-lookup"><span data-stu-id="1bf28-138">**For Android**</span></span>
     
       <span data-ttu-id="1bf28-139">En `Terminal` ventana inicie la aplicación en una nueva instancia de emulador ejecutando Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1bf28-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="1bf28-140">Puede ver la siguiente de hello en registros de la consola de hello:</span><span class="sxs-lookup"><span data-stu-id="1bf28-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="1bf28-141"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="1bf28-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="1bf28-142"><a id="integrate-push"></a>Habilitación de las notificaciones de inserción y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="1bf28-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="1bf28-143">Mobile Engagement le permite toointeract con los usuarios mediante las notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="1bf28-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="1bf28-144">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="1bf28-145">Hello las secciones siguientes se configurará la aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="1bf28-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="1bf28-146">Configuración de las credenciales Push para Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bf28-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="1bf28-147">tooallow Mobile Engagement toosend notificaciones de inserción en su nombre, debe toogrant obtener acceso a tooyour el certificado de iOS de Apple o la clave de API de servidor de GCM.</span><span class="sxs-lookup"><span data-stu-id="1bf28-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="1bf28-148">Navegue tooyour portal de interacción móvil.</span><span class="sxs-lookup"><span data-stu-id="1bf28-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="1bf28-149">Asegúrese de que está en aplicación de hello se usa para este proyecto y, a continuación, haga clic en hello **implique** situado en la parte inferior de hello:</span><span class="sxs-lookup"><span data-stu-id="1bf28-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="1bf28-150">Se colocará en la página de configuración de hello en el Portal de interacción.</span><span class="sxs-lookup"><span data-stu-id="1bf28-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="1bf28-151">Desde allí, haga clic en hello **inserción nativa** sección:</span><span class="sxs-lookup"><span data-stu-id="1bf28-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="1bf28-152">Configuración del certificado de iOS o la clave de API del servidor de GCM</span><span class="sxs-lookup"><span data-stu-id="1bf28-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="1bf28-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="1bf28-153">**[iOS]**</span></span>
   
    <span data-ttu-id="1bf28-154">a.</span><span class="sxs-lookup"><span data-stu-id="1bf28-154">a.</span></span> <span data-ttu-id="1bf28-155">Elija el certificado .p12, cárguelo y escriba la contraseña:</span><span class="sxs-lookup"><span data-stu-id="1bf28-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="1bf28-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="1bf28-156">**[Android]**</span></span>
   
    <span data-ttu-id="1bf28-157">a.</span><span class="sxs-lookup"><span data-stu-id="1bf28-157">a.</span></span> <span data-ttu-id="1bf28-158">Haga clic en el icono de edición de hello delante del **clave de API** en la sección de configuración de GCM hello en ventana emergente de Hola que se muestra, pegue Hola GCM clave del servidor y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1bf28-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="1bf28-159">Habilitar las notificaciones de inserción en la aplicación de Cordova hello</span><span class="sxs-lookup"><span data-stu-id="1bf28-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="1bf28-160">Editar **www/js/index.js** tooadd Hola llamada tooMobile interacción toorequest notificaciones de inserción y declare un controlador:</span><span class="sxs-lookup"><span data-stu-id="1bf28-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="1bf28-161">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="1bf28-161">Run hello app</span></span>
<span data-ttu-id="1bf28-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="1bf28-162">**[iOS]**</span></span>

1. <span data-ttu-id="1bf28-163">Se utilizará XCode toobuild e implementar aplicación hello en notificaciones de inserción de hello dispositivo tootest puesto que iOS permite solo dispositivo real de tooan de notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="1bf28-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="1bf28-164">Vaya a ubicación toohello donde se crea el proyecto de Cordova y navegue demasiado**...\platforms\ios** ubicación.</span><span class="sxs-lookup"><span data-stu-id="1bf28-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="1bf28-165">Abra el archivo .xcodeproj nativo de hello en XCode.</span><span class="sxs-lookup"><span data-stu-id="1bf28-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="1bf28-166">Compilar e implementar hello Cordova aplicación toohello el dispositivo iOS con cuenta de hello que tiene el perfil que contiene el certificado de Hola que acaba de cargar hello Id. de aplicación que coincide con hello uno que proporcionó durante la creación y el portal de interacción móvil toohello de aprovisionamiento de Hola aplicación de Cordova Hello.</span><span class="sxs-lookup"><span data-stu-id="1bf28-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="1bf28-167">Es posible desproteger hello *identificador de paquete* en su **recursos\*-info.plist** archivo en XCode toomatch seguridad.</span><span class="sxs-lookup"><span data-stu-id="1bf28-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="1bf28-168">Verá el elemento emergente de iOS estándar de hello en el dispositivo que indica que la aplicación hello solicita las notificaciones de toosend de permiso.</span><span class="sxs-lookup"><span data-stu-id="1bf28-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="1bf28-169">Conceda el permiso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-169">Grant hello permission.</span></span> 

<span data-ttu-id="1bf28-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="1bf28-170">**[Android]**</span></span>

<span data-ttu-id="1bf28-171">Puede usar simplemente aplicación Android de hello emulador toorun Hola tal y como se admiten las notificaciones de GCM en el emulador de Android Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="1bf28-172"><a id="send"></a>Enviar una aplicación de tooyour de notificación</span><span class="sxs-lookup"><span data-stu-id="1bf28-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="1bf28-173">Se creará una campaña de notificación de inserción simple que se va a enviar una aplicación de tooyour de inserción ejecuta en el dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="1bf28-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="1bf28-174">Navegue toohello **alcanzar** ficha en el portal de interacción móvil</span><span class="sxs-lookup"><span data-stu-id="1bf28-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="1bf28-175">Haga clic en **nuevo anuncio** toocreate la campaña de inserción</span><span class="sxs-lookup"><span data-stu-id="1bf28-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="1bf28-176">Proporcionar entradas toocreate la campaña **[Android]**</span><span class="sxs-lookup"><span data-stu-id="1bf28-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="1bf28-177">Proporcione un **Nombre** para la campaña.</span><span class="sxs-lookup"><span data-stu-id="1bf28-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="1bf28-178">Seleccione hello **tipo de entrega** como *notificación del sistema* *Simple*</span><span class="sxs-lookup"><span data-stu-id="1bf28-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="1bf28-179">Seleccione hello **hora de entrega** como *"Cualquier hora"*</span><span class="sxs-lookup"><span data-stu-id="1bf28-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="1bf28-180">Proporcionar un **título** para la notificación que será la primera línea de Hola de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="1bf28-181">Proporcionar un **mensaje** para la notificación que servirá como cuerpo del mensaje Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="1bf28-182">Proporcionar entradas toocreate la campaña **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="1bf28-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="1bf28-183">Proporcione un **Nombre** para la campaña.</span><span class="sxs-lookup"><span data-stu-id="1bf28-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="1bf28-184">Seleccione hello **hora de entrega** como *"fuera de la aplicación solo"*</span><span class="sxs-lookup"><span data-stu-id="1bf28-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="1bf28-185">Proporcionar un **título** para la notificación que será la primera línea de Hola de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="1bf28-186">Proporcionar un **mensaje** para la notificación que servirá como cuerpo del mensaje Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="1bf28-187">Desplácese hacia abajo y, en hello seleccione sección contenido **solo notificación**</span><span class="sxs-lookup"><span data-stu-id="1bf28-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="1bf28-188">[Opcional] También puede proporcionar la dirección URL de una acción.</span><span class="sxs-lookup"><span data-stu-id="1bf28-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="1bf28-189">Asegúrese de que utiliza un esquema de dirección URL proporcionado durante la configuración del complemento de hello **AZME\_REDIRIGIR\_URL** variable p. ej. *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="1bf28-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="1bf28-190">Ha terminado la posible de campaña más básica de configuración Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf28-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="1bf28-191">Ahora, desplácese hacia abajo en nuevo y haga clic en hello **crear** botón toosave la campaña.</span><span class="sxs-lookup"><span data-stu-id="1bf28-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="1bf28-192">Por último, **active** la campaña.</span><span class="sxs-lookup"><span data-stu-id="1bf28-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="1bf28-193">Ahora verá una notificación push en el dispositivo o en el emulador como parte de esta campaña.</span><span class="sxs-lookup"><span data-stu-id="1bf28-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="1bf28-194"><a id="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bf28-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="1bf28-195">Información general de todos los métodos disponibles con el SDK de Mobile Engagement para Cordova</span><span class="sxs-lookup"><span data-stu-id="1bf28-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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

