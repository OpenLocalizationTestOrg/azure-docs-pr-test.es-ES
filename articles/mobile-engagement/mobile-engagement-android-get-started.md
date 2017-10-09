---
title: "aaaGet partió Android aplicaciones de Azure Mobile Engagement"
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción y de análisis para aplicaciones Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="48c28-103">Introducción a Azure Mobile Engagement para aplicaciones Android</span><span class="sxs-lookup"><span data-stu-id="48c28-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="48c28-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="48c28-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="48c28-105">Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="48c28-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="48c28-106">En él, creará una aplicación en blanco de Android que recopila datos básicos y recibe notificaciones de inserción con el Servicio de mensajería en la nube de Google (GCM).</span><span class="sxs-lookup"><span data-stu-id="48c28-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48c28-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48c28-107">Prerequisites</span></span>
<span data-ttu-id="48c28-108">Completar este tutorial requiere hello [Android Developer Tools](https://developer.android.com/sdk/index.html), que incluye el entorno de desarrollo integrado de Android Studio hello y plataforma de Android más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="48c28-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="48c28-109">También requiere hello [Android SDK de Mobile Engagement](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="48c28-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48c28-110">toocomplete este tutorial, necesita una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="48c28-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="48c28-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="48c28-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="48c28-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="48c28-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="48c28-113">Configuración de Mobile Engagement para una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="48c28-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="48c28-114">Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="48c28-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="48c28-115">Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="48c28-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="48c28-116">Crear una aplicación básica con la integración de Android Studio toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="48c28-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="48c28-117">Encontrará documentación de integración completa de Hola Hola [integración con el SDK de Mobile Engagement Android](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48c28-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="48c28-118">Creación de un proyecto de Android</span><span class="sxs-lookup"><span data-stu-id="48c28-118">Create an Android project</span></span>
1. <span data-ttu-id="48c28-119">Iniciar **Android Studio**y en el menú emergente de hello, seleccione **iniciar un nuevo proyecto de Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="48c28-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="48c28-120">Especifique el nombre de la aplicación y el dominio de la compañía.</span><span class="sxs-lookup"><span data-stu-id="48c28-120">Provide an app name and company domain.</span></span> <span data-ttu-id="48c28-121">Tome nota de los datos que especifique pues los necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="48c28-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="48c28-122">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48c28-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="48c28-123">Seleccione el factor de forma de destino de Hola y el nivel de API y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48c28-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="48c28-124">Compromiso de Mobile requiere el nivel de API mínimo de 10 (2.3.3 Android).</span><span class="sxs-lookup"><span data-stu-id="48c28-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="48c28-125">Seleccione **actividad en blanco** aquí, que es la única pantalla de bienvenida para esta aplicación y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48c28-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="48c28-126">Por último, deje los valores predeterminados de hello tal y como está y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="48c28-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="48c28-127">Android Studio ahora crea la aplicación de demostración de hello en el que se integran Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="48c28-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="48c28-128">Incluir biblioteca del SDK de hello en el proyecto</span><span class="sxs-lookup"><span data-stu-id="48c28-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="48c28-129">Descargar hello [Android SDK de Mobile Engagement](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="48c28-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="48c28-130">Extraer carpeta tooa archivos para archivar faxes hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="48c28-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="48c28-131">Identificar Hola .jar biblioteca para la versión actual de Hola de este SDK y cópielo toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="48c28-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="48c28-132">Navegue toohello **proyecto** sección (1) y pegue .jar hello en la carpeta de bibliotecas de hello (2).</span><span class="sxs-lookup"><span data-stu-id="48c28-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="48c28-133">biblioteca de hello tooload, proyecto de Hola la sincronización.</span><span class="sxs-lookup"><span data-stu-id="48c28-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="48c28-134">Conectar el back-end de aplicación tooMobile interacción con hello cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="48c28-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="48c28-135">Copie Hola siguientes líneas de código en la creación de la actividad de hello (debe realizarse solo en un lugar de la aplicación, normalmente actividad principal de hello).</span><span class="sxs-lookup"><span data-stu-id="48c28-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="48c28-136">Para esta aplicación de ejemplo, abra hello MainActivity en src -> main -> carpeta de java y agregue Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="48c28-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="48c28-137">Resolver las referencias de hello presionando Alt + ENTRAR o agregando Hola siguiendo las instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="48c28-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="48c28-138">Volver atrás toohello Portal de Azure clásico en la aplicación **información de conexión** Hola de página y copiar **cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="48c28-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="48c28-139">Pegue en hello `setConnectionString` parámetro, reemplazando la cadena completa de Hola se muestra en el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="48c28-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="48c28-140">Agregar permisos y una declaración de servicio</span><span class="sxs-lookup"><span data-stu-id="48c28-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="48c28-141">Agregar estos toohello permisos Manifest.xml del proyecto inmediatamente antes o después de hello `<application>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="48c28-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="48c28-142">toodeclare Hola servicio del agente, agregue este código entre hello `<application>` y `</application>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="48c28-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="48c28-143">En el código de hello que pegó, reemplace `"<Your application name>"` en etiqueta de hello, que se muestra en hello **configuración** menú donde puede ver los servicios que se ejecutan en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="48c28-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="48c28-144">Por ejemplo puede agregar palabra Hola "Servicio" en esa etiqueta.</span><span class="sxs-lookup"><span data-stu-id="48c28-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="48c28-145">Enviar una interacción de pantalla tooMobile</span><span class="sxs-lookup"><span data-stu-id="48c28-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="48c28-146">toostart enviar datos y asegurarse de que los usuarios de hello están activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).</span><span class="sxs-lookup"><span data-stu-id="48c28-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="48c28-147">Vaya demasiado**MainActivity.java** y agregue Hola después de la clase base de hello tooreplace de **MainActivity** demasiado**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="48c28-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="48c28-148">Si la clase base no es *actividad*, consulte [avanzada Reporting Android](mobile-engagement-android-advanced-reporting.md) para saber cómo tooinherit partir de clases diferentes.</span><span class="sxs-lookup"><span data-stu-id="48c28-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="48c28-149">Comente Hola después de línea para este escenario de ejemplo simple:</span><span class="sxs-lookup"><span data-stu-id="48c28-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="48c28-150">Si desea que hello tookeep `ActionBar` en la aplicación, consulte [avanzada Reporting Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="48c28-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="48c28-151">Conectar la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="48c28-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="48c28-152">Habilitación de las notificaciones push y la mensajería en aplicación</span><span class="sxs-lookup"><span data-stu-id="48c28-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="48c28-153">Durante una campaña, Mobile Engagement permite interactuar y llegar por REACH a los usuarios mediante notificaciones push y mensajería en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c28-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="48c28-154">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="48c28-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="48c28-155">Hola pasos de la sección configura su aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="48c28-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="48c28-156">Copia de recursos SDK en el proyecto</span><span class="sxs-lookup"><span data-stu-id="48c28-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="48c28-157">Navegue Hola de contenido y copia de la descarga SDK tooyour back- **res** carpeta.</span><span class="sxs-lookup"><span data-stu-id="48c28-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="48c28-158">Volver atrás tooAndroid Studio, seleccione hello **principal** directorio de los archivos de proyecto y, a continuación, péguelo recursos tooyour project de tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="48c28-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="48c28-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48c28-159">Next steps</span></span>
<span data-ttu-id="48c28-160">Vaya demasiado[SDK de Android](mobile-engagement-android-sdk-overview.md) tooget un conocimiento acerca de la integración con el SDK de hello detallado.</span><span class="sxs-lookup"><span data-stu-id="48c28-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
