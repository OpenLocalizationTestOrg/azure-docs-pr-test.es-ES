---
title: "aaaSending tooAndroid de notificaciones de inserción con centros de notificaciones de Azure | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo dispositivos tooAndroid de toouse centros de notificaciones de Azure toopush notificaciones."
services: notification-hubs
documentationcenter: android
keywords: "notificaciones push,notificación push,notificaciones push android"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="941b3-104">Enviar tooAndroid de notificaciones de inserción con centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="941b3-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="941b3-105">Información general</span><span class="sxs-lookup"><span data-stu-id="941b3-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="941b3-106">En este tema se muestran las notificaciones push con el servicio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="941b3-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="941b3-107">Si usas Firebase en la nube de mensajería (FCM de Google), consulte [tooAndroid de notificaciones de inserción de envío con centros de notificaciones de Azure y FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="941b3-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="941b3-108">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación Android tooan de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="941b3-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="941b3-109">Creará una aplicación de Android en blanco que reciba notificaciones push mediante el servicio de mensajería en la nube de Google (GCM).</span><span class="sxs-lookup"><span data-stu-id="941b3-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="941b3-110">código de Hello completado para este tutorial puede descargarse desde GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="941b3-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="941b3-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="941b3-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="941b3-112">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="941b3-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="941b3-113">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="941b3-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="941b3-114">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="941b3-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="941b3-115">Además la cuenta activa de Azure tooan mencionados anteriormente, este tutorial solo requiere la versión más reciente de Hola de [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="941b3-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="941b3-116">La realización de este tutorial es un requisito previo para todos los tutoriales de Centros de notificaciones para aplicaciones Android.</span><span class="sxs-lookup"><span data-stu-id="941b3-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="941b3-117">Creación de un proyecto que admita el servicio de mensajería en la nube de Google</span><span class="sxs-lookup"><span data-stu-id="941b3-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="941b3-118">Configuración de un centro de notificaciones nuevo</span><span class="sxs-lookup"><span data-stu-id="941b3-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="941b3-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="941b3-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="941b3-120">Hola **configuración** hoja, seleccione **Notification Services** y, a continuación, **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="941b3-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="941b3-121">Escriba la clave de API de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="941b3-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Centros de notificaciones de Azure: Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="941b3-123">El centro de notificaciones está ahora configurado toowork con GCM y tener tooboth de cadenas de conexión de hello registrar su aplicación tooreceive y enviar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="941b3-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="941b3-124"><a id="connecting-app"></a>Conectar el centro de notificaciones de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="941b3-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="941b3-125">Creación de un nuevo proyecto de Android</span><span class="sxs-lookup"><span data-stu-id="941b3-125">Create a new Android project</span></span>
1. <span data-ttu-id="941b3-126">En Android Studio, inicie un nuevo proyecto de Android Studio.</span><span class="sxs-lookup"><span data-stu-id="941b3-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio: nuevo proyecto][13]
2. <span data-ttu-id="941b3-128">Elija hello **teléfono y tableta** forman hello y factor **mínimo SDK** que desea toosupport.</span><span class="sxs-lookup"><span data-stu-id="941b3-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="941b3-129">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="941b3-129">Then click **Next**.</span></span>
   
   ![Android Studio: flujo de trabajo de creación de proyecto][14]
3. <span data-ttu-id="941b3-131">Elija **actividad vacía** para la actividad principal de hello, haga clic en **siguiente**y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="941b3-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="941b3-132">Agregar proyecto de Google Play services toohello</span><span class="sxs-lookup"><span data-stu-id="941b3-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="941b3-133">Incorporación de bibliotecas de Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="941b3-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="941b3-134">Hola `Build.Gradle` archivo para hello **aplicación**, agregar Hola después de las líneas de hello **dependencias** sección.</span><span class="sxs-lookup"><span data-stu-id="941b3-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="941b3-135">Agregar Hola después repositorio después de hello **dependencias** sección.</span><span class="sxs-lookup"><span data-stu-id="941b3-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="941b3-136">Actualizando hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="941b3-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="941b3-137">toosupport GCM, debemos implementar un servicio de agente de escucha de Id. de instancia en el código que se usa demasiado[obtener tokens de registro](https://developers.google.com/cloud-messaging/android/client#sample-register) con [API de Id. de instancia de Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="941b3-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="941b3-138">En este tutorial se denominará clase hello `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="941b3-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="941b3-139">Agregar Hola siguiente servicio definición toohello AndroidManifest.xml el archivo, dentro de hello `<application>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="941b3-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="941b3-140">Reemplace hello `<your package>` Hola de marcador de posición con el nombre del paquete real se muestran en la parte superior de Hola de hello `AndroidManifest.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="941b3-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="941b3-141">Una vez que hemos recibido el token de registro GCM de hello API de Id. de instancia, se usará demasiado[registrar con hello centro de notificaciones de Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="941b3-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="941b3-142">Se admite este registro de hello plano utilizando un `IntentService` denominado `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="941b3-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="941b3-143">Este servicio también será responsable de [actualizar nuestro token de registro GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="941b3-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="941b3-144">Agregar Hola siguiente servicio definición toohello AndroidManifest.xml el archivo, dentro de hello `<application>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="941b3-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="941b3-145">Reemplace hello `<your package>` Hola de marcador de posición con el nombre del paquete real se muestran en la parte superior de Hola de hello `AndroidManifest.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="941b3-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="941b3-146">También definirá un notificaciones de tooreceive de receptor.</span><span class="sxs-lookup"><span data-stu-id="941b3-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="941b3-147">Agregar Hola siguiente receptor definición toohello AndroidManifest.xml el archivo, dentro de hello `<application>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="941b3-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="941b3-148">Reemplace hello `<your package>` Hola de marcador de posición con el nombre del paquete real se muestran en la parte superior de Hola de hello `AndroidManifest.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="941b3-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="941b3-149">Agregar Hola después GCM necesario relacionados con permisos por debajo de hello `</application>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="941b3-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="941b3-150">Asegúrese de que tooreplace `<your package>` con el nombre del paquete Hola se muestran en la parte superior de Hola de hello `AndroidManifest.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="941b3-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="941b3-151">Para más información sobre estos permisos, consulte [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest)(Configuración de una aplicación de cliente GCM para Android).</span><span class="sxs-lookup"><span data-stu-id="941b3-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="941b3-152">Incorporación de código</span><span class="sxs-lookup"><span data-stu-id="941b3-152">Adding code</span></span>
1. <span data-ttu-id="941b3-153">Hola vista de proyecto, expanda **aplicación** > **src** > **principal** > **java**.</span><span class="sxs-lookup"><span data-stu-id="941b3-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="941b3-154">Haga clic con el botón derecho en la carpeta del paquete en **java**, haga clic en **Nuevo** y, a continuación, haga clic en **Clase Java**.</span><span class="sxs-lookup"><span data-stu-id="941b3-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="941b3-155">Agregue una clase nueva llamada `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="941b3-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio: nueva clase Java][6]
   
    <span data-ttu-id="941b3-157">Asegúrese de que tooupdate Hola estos tres marcadores de posición en hello después el código de hello `NotificationSettings` clase:</span><span class="sxs-lookup"><span data-stu-id="941b3-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="941b3-158">**Id. de remitente**: Hola número proyecto obtenido anteriormente en hello [consola en la nube de Google](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="941b3-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="941b3-159">**HubListenConnectionString**: Hola **DefaultListenAccessSignature** cadena de conexión para el concentrador.</span><span class="sxs-lookup"><span data-stu-id="941b3-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="941b3-160">Puede copiar esa cadena de conexión, haga clic en **las directivas de acceso** en hello **configuración** hoja de su centro de hello [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="941b3-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="941b3-161">**HubName**: usar el nombre de su centro de notificaciones que aparece en la hoja de concentrador de Hola Hola Hola [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="941b3-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="941b3-162">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="941b3-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="941b3-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="941b3-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="941b3-164">}</span><span class="sxs-lookup"><span data-stu-id="941b3-164">}</span></span>
2. <span data-ttu-id="941b3-165">Mediante pasos de hello anteriores, agregue otra nueva clase denominada `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="941b3-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="941b3-166">Se trata de nuestra implementación de servicio de escucha de Instance ID.</span><span class="sxs-lookup"><span data-stu-id="941b3-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="941b3-167">Llame código de Hello para esta clase nuestro `IntentService` demasiado[actualización Hola GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="941b3-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="941b3-168">Agregue otra clase tooyour proyecto denominado, `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="941b3-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="941b3-169">Se trata de implementación de Hola para nuestro `IntentService` que controlará [actualizar token GCM hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) y [registrar con el centro de notificaciones de hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="941b3-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="941b3-170">Usar hello siguiente código para esta clase.</span><span class="sxs-lookup"><span data-stu-id="941b3-170">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="941b3-171">En su `MainActivity` de clases, agregue los siguientes hello `import` instrucciones anteriores Hola declaración de clase.</span><span class="sxs-lookup"><span data-stu-id="941b3-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="941b3-172">Agregar Hola siguiendo los miembros privados en parte superior de hello de la clase hello.</span><span class="sxs-lookup"><span data-stu-id="941b3-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="941b3-173">Usaremos estos [comprobar la disponibilidad de hello de servicios de Google Play según las recomendaciones de Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="941b3-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="941b3-174">En su `MainActivity` clase, agregue Hola método toohello lanzamiento de servicios de Google Play.</span><span class="sxs-lookup"><span data-stu-id="941b3-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="941b3-175">En su `MainActivity` clase, agregue Hola después el código que se comprobará para servicios de Google Play antes de llamar a su `IntentService` tooget su token de registro GCM y registrarse con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="941b3-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="941b3-176">Hola `OnCreate` método de hello `MainActivity` clase, agregue Hola siguiendo el proceso de registro de hello toostart de código cuando se crea la actividad.</span><span class="sxs-lookup"><span data-stu-id="941b3-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="941b3-177">Agregar estos métodos adicionales toohello `MainActivity` tooverify estado y el informe Estado de la aplicación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="941b3-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="941b3-178">Hola `ToastNotify` método usa hello *"Hola mundo"* `TextView` tooreport estado y notificaciones de forma persistente en la aplicación hello de control.</span><span class="sxs-lookup"><span data-stu-id="941b3-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="941b3-179">En el diseño activity_main.xml, agregue Hola siguiente Id. de ese control.</span><span class="sxs-lookup"><span data-stu-id="941b3-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="941b3-180">A continuación, agregaremos una subclase para nuestro receptor que definimos en hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="941b3-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="941b3-181">Agregue otra clase tooyour proyecto denominado `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="941b3-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="941b3-182">Agregar Hola siguiendo las instrucciones de importación en la parte superior de Hola de `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="941b3-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="941b3-183">Agregar Hola después el código de hello `MyHandler` clase lo que una subclase de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="941b3-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="941b3-184">Este código invalida hello `OnReceive` método, por lo que el controlador de hello informará de las notificaciones que se reciben.</span><span class="sxs-lookup"><span data-stu-id="941b3-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="941b3-185">controlador de Hello envía también Administrador de Android notificaciones de toohello de notificación de inserción de hello mediante hello `sendNotification()` método.</span><span class="sxs-lookup"><span data-stu-id="941b3-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="941b3-186">Hola `sendNotification()` el método debe ejecutarse cuando no se está ejecutando la aplicación hello y se recibe una notificación.</span><span class="sxs-lookup"><span data-stu-id="941b3-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="941b3-187">En Android Studio en la barra de menús de hello, haga clic en **generar** > **volver a generar el proyecto** toomake seguro de que no están presentes en el código errores.</span><span class="sxs-lookup"><span data-stu-id="941b3-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="941b3-188">Envío de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="941b3-188">Sending push notifications</span></span>
<span data-ttu-id="941b3-189">Puede probar recibiendo notificaciones de inserción en la aplicación mediante el envío de ellos a través de hello [Portal de Azure] -busque hello **solución de problemas** sección en la hoja de la base de datos central de hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="941b3-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Centros de notificaciones de Azure: envío de prueba](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="941b3-191">(Opcional) Enviar notificaciones de inserción directamente desde la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="941b3-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="941b3-192">Lo habitual es enviar notificaciones mediante un servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="941b3-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="941b3-193">En algunos casos, conviene toobe toosend capaz de notificaciones de inserción directamente desde la aplicación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="941b3-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="941b3-194">Esta sección explica cómo Hola toosend notificaciones de cliente hello mediante [API de REST de concentrador de notificación de Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="941b3-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="941b3-195">En la vista de proyecto de Android Studio, expanda **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="941b3-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="941b3-196">Abra hello `activity_main.xml` diseño de archivo y haga clic en hello **texto** ficha tooupdate Hola contenido de texto hello archivo.</span><span class="sxs-lookup"><span data-stu-id="941b3-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="941b3-197">Actualícelo con código de hello siguiente, que agrega las nuevas `Button` y `EditText` centro de notificaciones de toohello de mensajes de notificación de inserción de controles para el envío.</span><span class="sxs-lookup"><span data-stu-id="941b3-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="941b3-198">Agregue este código en la parte inferior de hello, justo delante `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="941b3-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="941b3-199">En la vista de proyecto de Android Studio, expanda **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="941b3-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="941b3-200">Abra hello `strings.xml` de archivos y agregar valores de cadena de Hola que hace referencia Hola nueva `Button` y `EditText` controles.</span><span class="sxs-lookup"><span data-stu-id="941b3-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="941b3-201">Agregue estos elementos en la parte inferior de Hola de archivo hello, justo delante `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="941b3-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="941b3-202">En su `NotificationSetting.java` , agregue Hola después configuración toohello `NotificationSettings` clase.</span><span class="sxs-lookup"><span data-stu-id="941b3-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="941b3-203">Actualización `HubFullAccess` con hello **DefaultFullSharedAccessSignature** cadena de conexión para el concentrador.</span><span class="sxs-lookup"><span data-stu-id="941b3-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="941b3-204">Esta cadena de conexión se puede copiar desde hello [Portal de Azure] haciendo clic en **las directivas de acceso** en hello **configuración** hoja para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="941b3-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="941b3-205">En su `MainActivity.java` , agregue la siguiente hello `import` instrucciones anteriores hello `MainActivity` clase.</span><span class="sxs-lookup"><span data-stu-id="941b3-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="941b3-206">En su `MainActivity.java` , agregue Hola después de miembros en la parte superior de Hola de hello `MainActivity` clase.</span><span class="sxs-lookup"><span data-stu-id="941b3-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="941b3-207">Debe crear un tooauthenticate de token de firma de acceso de Software (SaS) en un centro de notificaciones de entrada solicitud toosend mensajes tooyour.</span><span class="sxs-lookup"><span data-stu-id="941b3-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="941b3-208">Esto se hace mediante el análisis Hola datos clave de cadena de conexión de hello y, a continuación, crear Hola token de SaS, tal y como se mencionó en hello [conceptos comunes](http://msdn.microsoft.com/library/azure/dn495627.aspx) referencia de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="941b3-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="941b3-209">Hola siguiente código es una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="941b3-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="941b3-210">En `MainActivity.java`, agregar Hola siguiendo el método toohello `MainActivity` clase tooparse la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="941b3-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="941b3-211">En `MainActivity.java`, agregar Hola siguiendo el método toohello `MainActivity` clase toocreate un token de autenticación de SaS.</span><span class="sxs-lookup"><span data-stu-id="941b3-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="941b3-212">En `MainActivity.java`, agregar Hola siguiendo el método toohello `MainActivity` Hola de clase toohandle **enviar notificación** clic de botón y enviar una notificación de inserción de hello concentrador de toohello de mensajes mediante el uso de Hola integrados API de REST.</span><span class="sxs-lookup"><span data-stu-id="941b3-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="941b3-213">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="941b3-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="941b3-214">Notificaciones de inserción en el emulador de Hola</span><span class="sxs-lookup"><span data-stu-id="941b3-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="941b3-215">Si desea que las notificaciones de inserción de tootest dentro de un emulador, asegúrese de que la imagen del emulador admite el nivel de API de Google de Hola que eligió para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="941b3-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="941b3-216">Si la imagen no es compatible con nativo APIs Google, terminará con hello **servicio\_no\_disponible** excepción.</span><span class="sxs-lookup"><span data-stu-id="941b3-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="941b3-217">Además toohello anterior, asegúrese de que ha agregado el tooyour de cuenta de Google ejecución del emulador en **configuración** > **cuentas**.</span><span class="sxs-lookup"><span data-stu-id="941b3-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="941b3-218">En caso contrario, está penada por la tooregister intentos con GCM en hello **autenticación\_error** excepción.</span><span class="sxs-lookup"><span data-stu-id="941b3-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="941b3-219">Ejecuta la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="941b3-219">Running hello application</span></span>
1. <span data-ttu-id="941b3-220">Ejecutar aplicación hello y observe que se notifica el Id. del registro de hello para un registro correcto.</span><span class="sxs-lookup"><span data-stu-id="941b3-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![Prueba en Android: registro de canal][18]
2. <span data-ttu-id="941b3-222">Escriba un toobe de mensaje de notificación enviado tooall dispositivos Android que han registrado con el concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="941b3-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![Prueba en Android - envío de un mensaje][19]

3. <span data-ttu-id="941b3-224">Presione **Enviar notificación**.</span><span class="sxs-lookup"><span data-stu-id="941b3-224">Press **Send Notification**.</span></span> <span data-ttu-id="941b3-225">Los dispositivos que tienen la ejecución de la aplicación de hello mostrará un `AlertDialog` instancia con el mensaje de notificación de inserción de saludo.</span><span class="sxs-lookup"><span data-stu-id="941b3-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="941b3-226">Dispositivos que no tienen la ejecución de la aplicación de hello pero que se registraron anteriormente para las notificaciones de inserción recibirá una notificación en hello Administrador de notificaciones Android.</span><span class="sxs-lookup"><span data-stu-id="941b3-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="941b3-227">Los pueden verse deslizando hacia abajo desde la esquina superior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="941b3-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![Prueba en Android - notificaciones][21]

## <a name="next-steps"></a><span data-ttu-id="941b3-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="941b3-229">Next steps</span></span>
<span data-ttu-id="941b3-230">Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial como paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="941b3-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="941b3-231">Le mostraremos cómo toosend notificaciones desde un back-end ASP.NET con etiquetas tootarget determinados usuarios.</span><span class="sxs-lookup"><span data-stu-id="941b3-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="941b3-232">Si desea toosegment los usuarios por grupos de interés, desproteger hello [toosend de centros de notificaciones utilice noticias de última hora] tutorial.</span><span class="sxs-lookup"><span data-stu-id="941b3-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="941b3-233">toolearn obtener más información sobre los centros de notificaciones, consulte nuestro [instrucciones de los centros de notificación].</span><span class="sxs-lookup"><span data-stu-id="941b3-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[instrucciones de los centros de notificación]: http://msdn.microsoft.com/library/jj927170.aspx
[toousers de notificaciones de los centros de notificaciones de uso toopush]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Portal de Azure]: https://portal.azure.com
