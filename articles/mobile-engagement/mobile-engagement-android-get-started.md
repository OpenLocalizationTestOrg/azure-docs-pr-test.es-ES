---
title: "Introducción a las aplicaciones Android de Azure Mobile Engagement"
description: "Aprenda a usar Azure Mobile Engagement con los análisis y las notificaciones de inserción para aplicaciones Android."
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
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="2a76b-103">Introducción a Azure Mobile Engagement para aplicaciones Android</span><span class="sxs-lookup"><span data-stu-id="2a76b-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2a76b-104">En este tema se muestra cómo usar Azure Mobile Engagement para comprender el uso de su aplicación y cómo enviar notificaciones push a los usuarios segmentados de una aplicación de Android.</span><span class="sxs-lookup"><span data-stu-id="2a76b-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="2a76b-105">En este tutorial se demuestra el escenario de difusión sencillo con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2a76b-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="2a76b-106">En él, creará una aplicación en blanco de Android que recopila datos básicos y recibe notificaciones de inserción con el Servicio de mensajería en la nube de Google (GCM).</span><span class="sxs-lookup"><span data-stu-id="2a76b-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a76b-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a76b-107">Prerequisites</span></span>
<span data-ttu-id="2a76b-108">Para completar este tutorial se requieren la [Herramientas para desarrolladores de Android](https://developer.android.com/sdk/index.html), que incluyen el entorno de desarrollo integrado de Android Studio y la última plataforma de Android.</span><span class="sxs-lookup"><span data-stu-id="2a76b-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="2a76b-109">Descargue el [SDK de Android para Mobile Engagement](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="2a76b-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a76b-110">Para completar este tutorial, deberá tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a76b-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="2a76b-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2a76b-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2a76b-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="2a76b-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="2a76b-113">Configuración de Mobile Engagement para una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="2a76b-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="2a76b-114">Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2a76b-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="2a76b-115">En este tutorial se presenta una "integración básica", que es el conjunto mínimo necesario para recopilar los datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="2a76b-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="2a76b-116">Va a crear una aplicación básica con Android Studio para demostrar la integración.</span><span class="sxs-lookup"><span data-stu-id="2a76b-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="2a76b-117">La documentación de integración completa se puede encontrar en la [integración del SDK de Android para Mobile Engagement](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a76b-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="2a76b-118">Creación de un proyecto de Android</span><span class="sxs-lookup"><span data-stu-id="2a76b-118">Create an Android project</span></span>
1. <span data-ttu-id="2a76b-119">Inicie **Android Studio** y, en el menú emergente, seleccione **Start a new Android Studio project** (Iniciar un nuevo proyecto de Android Studio).</span><span class="sxs-lookup"><span data-stu-id="2a76b-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="2a76b-120">Especifique el nombre de la aplicación y el dominio de la compañía.</span><span class="sxs-lookup"><span data-stu-id="2a76b-120">Provide an app name and company domain.</span></span> <span data-ttu-id="2a76b-121">Tome nota de los datos que especifique pues los necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="2a76b-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="2a76b-122">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2a76b-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="2a76b-123">Seleccione el factor de forma de destino y el nivel de la AP, y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2a76b-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2a76b-124">Compromiso de Mobile requiere el nivel de API mínimo de 10 (2.3.3 Android).</span><span class="sxs-lookup"><span data-stu-id="2a76b-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="2a76b-125">Seleccione **Blank Activity** (Actividad en blanco) aquí, que es la única pantalla para esta aplicación, y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2a76b-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="2a76b-126">Por último, deje el valor predeterminado como está y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="2a76b-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="2a76b-127">Ahora Android Studio crea la aplicación de demostración en la que integraremos Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2a76b-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="2a76b-128">Incluir la biblioteca de SDK en el proyecto</span><span class="sxs-lookup"><span data-stu-id="2a76b-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="2a76b-129">Descargue el [SDK de Android para Mobile Engagement](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="2a76b-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="2a76b-130">Extraiga el archivo a una carpeta en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2a76b-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="2a76b-131">Identifique la biblioteca .jar para la versión actual de este SDK y cópiela en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="2a76b-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="2a76b-132">Vaya a la sección **Proyecto** (1) y pegue el .jar en la carpeta libs (2).</span><span class="sxs-lookup"><span data-stu-id="2a76b-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="2a76b-133">Para cargar la biblioteca, sincronice el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2a76b-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="2a76b-134">Conectar la aplicación al back-end de Mobile Engagement mediante la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="2a76b-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="2a76b-135">Copie las siguientes líneas de código en la creación de la actividad (debe realizarse solo en un lugar de la aplicación, normalmente la actividad principal).</span><span class="sxs-lookup"><span data-stu-id="2a76b-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="2a76b-136">Para esta aplicación de ejemplo, abra MainActivity en la carpeta src -> main -> java y agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a76b-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="2a76b-137">Resuelva las referencias pulsando Alt + Intro o agregando las siguientes instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="2a76b-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="2a76b-138">Vuelva al Portal de Azure clásico en la página **Información de conexión** de la aplicación y copie el valor de **Cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="2a76b-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="2a76b-139">Péguelo en el parámetro `setConnectionString`, reemplazando la cadena completa que se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a76b-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="2a76b-140">Agregar permisos y una declaración de servicio</span><span class="sxs-lookup"><span data-stu-id="2a76b-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="2a76b-141">Agregue estos permisos al archivo Manifest.xml del proyecto inmediatamente anterior a la etiqueta `<application>`:</span><span class="sxs-lookup"><span data-stu-id="2a76b-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="2a76b-142">Agregue este código entre las etiquetas `<application>` y `</application>` para declarar el servicio del agente:</span><span class="sxs-lookup"><span data-stu-id="2a76b-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="2a76b-143">En el código que pegó, reemplace `"<Your application name>"` en la etiqueta que aparece en el menú **Configuración** donde puede ver los servicios que se ejecutan en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2a76b-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="2a76b-144">Puede agregar la palabra "Servicio" a la etiqueta, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2a76b-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="2a76b-145">Enviar una pantalla a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2a76b-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="2a76b-146">Para comenzar a enviar datos y asegurarse de que los usuarios estén activos, debe enviar al menos una pantalla (Actividad) al back-end de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2a76b-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="2a76b-147">Vaya a **MainActivity.java** y agregue la siguiente línea para reemplazar la clase base de **MainActivity** en **EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="2a76b-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="2a76b-148">Si la clase base no es *Activity*, consulte [Reporting Options with Engagement on Android](mobile-engagement-android-advanced-reporting.md) (Opciones de informes con Engagement en Android) sobre cómo heredar de clases diferentes.</span><span class="sxs-lookup"><span data-stu-id="2a76b-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="2a76b-149">Convierta en comentario la línea siguiente para este escenario de ejemplo simple:</span><span class="sxs-lookup"><span data-stu-id="2a76b-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="2a76b-150">Si desea mantener `ActionBar` en la aplicación, consulte [Opciones de informes con Engagement en Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="2a76b-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="2a76b-151">Conectar la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="2a76b-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="2a76b-152">Habilitación de las notificaciones push y la mensajería en aplicación</span><span class="sxs-lookup"><span data-stu-id="2a76b-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="2a76b-153">Durante una campaña, Mobile Engagement permite interactuar y llegar por REACH a los usuarios mediante notificaciones push y mensajería en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a76b-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="2a76b-154">Este módulo se denomina REACH en el portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2a76b-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="2a76b-155">En la sección siguiente se instala la aplicación para recibirlos.</span><span class="sxs-lookup"><span data-stu-id="2a76b-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="2a76b-156">Copia de recursos SDK en el proyecto</span><span class="sxs-lookup"><span data-stu-id="2a76b-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="2a76b-157">Vuelva al contenido de descarga del SDK y copie la carpeta **res** .</span><span class="sxs-lookup"><span data-stu-id="2a76b-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="2a76b-158">Vuelva a Android Studio, seleccione el directorio **main** de los archivos de proyecto y luego péguelo para agregar los recursos al proyecto.</span><span class="sxs-lookup"><span data-stu-id="2a76b-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="2a76b-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a76b-159">Next steps</span></span>
<span data-ttu-id="2a76b-160">Vaya a [SDK de Android](mobile-engagement-android-sdk-overview.md) para obtener información detallada sobre la integración de SDK.</span><span class="sxs-lookup"><span data-stu-id="2a76b-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

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
