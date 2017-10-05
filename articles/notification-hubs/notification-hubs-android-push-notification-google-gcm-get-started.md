---
title: "Envío de notificaciones push a Android con los Azure Notification Hubs | Microsoft Docs"
description: "En este tutorial aprenderá a usar los Centros de notificaciones de Azure para enviar notificaciones push a dispositivos Android."
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
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="c2427-104">Envío de notificaciones push a Android con los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c2427-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c2427-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c2427-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c2427-106">En este tema se muestran las notificaciones push con el servicio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="c2427-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="c2427-107">Si utiliza el Servicio de mensajería en la nube Firebase (FCM) de Google, consulte [Envío de notificaciones push a Android con los Centros de notificaciones de Azure](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2427-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="c2427-108">Este tutorial muestra cómo puede usar Centros de notificaciones de Azure para enviar notificaciones push a una aplicación de Android.</span><span class="sxs-lookup"><span data-stu-id="c2427-108">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an Android application.</span></span>
<span data-ttu-id="c2427-109">Creará una aplicación de Android en blanco que reciba notificaciones push mediante el servicio de mensajería en la nube de Google (GCM).</span><span class="sxs-lookup"><span data-stu-id="c2427-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="c2427-110">El código completo de este tutorial se puede descargar de GitHub, [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="c2427-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2427-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c2427-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c2427-112">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c2427-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c2427-113">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c2427-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c2427-114">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="c2427-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="c2427-115">Además de la cuenta de Azure activa mencionada anteriormente, este tutorial solo requiere la versión más reciente de [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="c2427-115">In addition to an active Azure account mentioned above, this tutorial only requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="c2427-116">La realización de este tutorial es un requisito previo para todos los tutoriales de Centros de notificaciones para aplicaciones Android.</span><span class="sxs-lookup"><span data-stu-id="c2427-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="c2427-117">Creación de un proyecto que admita el servicio de mensajería en la nube de Google</span><span class="sxs-lookup"><span data-stu-id="c2427-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="c2427-118">Configuración de un centro de notificaciones nuevo</span><span class="sxs-lookup"><span data-stu-id="c2427-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="c2427-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="c2427-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="c2427-120">En la hoja **Configuración**, seleccione **Servicios de notificaciones** y, luego, **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="c2427-120">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="c2427-121">Escriba la clave de API y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c2427-121">Enter the API key and click **Save**.</span></span>

&emsp;&emsp;![Centros de notificaciones de Azure: Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="c2427-123">El Centro de notificaciones está configurado para funcionar con GCM y el usuario dispone de las cadenas de conexión necesarias para registrar su aplicación para que reciba y envíe notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="c2427-123">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="c2427-124"><a id="connecting-app"></a>Conexión de la aplicación al Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="c2427-124"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="c2427-125">Creación de un nuevo proyecto de Android</span><span class="sxs-lookup"><span data-stu-id="c2427-125">Create a new Android project</span></span>
1. <span data-ttu-id="c2427-126">En Android Studio, inicie un nuevo proyecto de Android Studio.</span><span class="sxs-lookup"><span data-stu-id="c2427-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio: nuevo proyecto][13]
2. <span data-ttu-id="c2427-128">Elija el factor de forma **Teléfono y tableta** y el **SDK mínimo** que desea admitir.</span><span class="sxs-lookup"><span data-stu-id="c2427-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="c2427-129">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c2427-129">Then click **Next**.</span></span>
   
   ![Android Studio: flujo de trabajo de creación de proyecto][14]
3. <span data-ttu-id="c2427-131">Elija **Empty Activity** (Actividad vacía) para la actividad principal, haga clic en **Next** (Siguiente) y, luego, en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="c2427-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="c2427-132">Incorporación de los servicios de Google Play al proyecto</span><span class="sxs-lookup"><span data-stu-id="c2427-132">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="c2427-133">Incorporación de bibliotecas de Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c2427-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="c2427-134">En el archivo `Build.Gradle` de la **aplicación**, agregue las siguientes líneas en la sección **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="c2427-134">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="c2427-135">Agregue el repositorio siguiente después de la sección de **dependencias** .</span><span class="sxs-lookup"><span data-stu-id="c2427-135">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="c2427-136">Actualización de AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c2427-136">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="c2427-137">Para admitir GCM, debemos implementar un servicio de escucha Instance ID en el código, que se usa para [obtener tokens de registro](https://developers.google.com/cloud-messaging/android/client#sample-register) con la [API Instance ID de Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="c2427-137">To support GCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="c2427-138">En este tutorial, asignaremos el nombre `MyInstanceIDService`a la clase.</span><span class="sxs-lookup"><span data-stu-id="c2427-138">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="c2427-139">Agregue la siguiente definición de servicio al archivo AndroidManifest.xml, en la etiqueta `<application>` .</span><span class="sxs-lookup"><span data-stu-id="c2427-139">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="c2427-140">Reemplace el marcador de posición `<your package>` por el nombre real del paquete, que se muestra en la parte superior del archivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="c2427-140">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="c2427-141">Cuando recibamos el token de registro GCM de la API Instance ID, se usará para el [registro en el Centro de notificaciones de Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="c2427-141">Once we have received our GCM registration token from the Instance ID API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="c2427-142">Este registro se admite en segundo plano con un servicio `IntentService` llamado `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="c2427-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="c2427-143">Este servicio también será responsable de [actualizar nuestro token de registro GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="c2427-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="c2427-144">Agregue la siguiente definición de servicio al archivo AndroidManifest.xml, en la etiqueta `<application>` .</span><span class="sxs-lookup"><span data-stu-id="c2427-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="c2427-145">Reemplace el marcador de posición `<your package>` por el nombre real del paquete, que se muestra en la parte superior del archivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="c2427-145">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="c2427-146">También definiremos un receptor para recibir las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c2427-146">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="c2427-147">Agregue la siguiente definición de receptor al archivo AndroidManifest.xml, en la etiqueta `<application>` .</span><span class="sxs-lookup"><span data-stu-id="c2427-147">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="c2427-148">Reemplace el marcador de posición `<your package>` por el nombre real del paquete, que se muestra en la parte superior del archivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="c2427-148">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="c2427-149">Agregue los siguientes permisos de GCM necesarios bajo la etiqueta `</application>` .</span><span class="sxs-lookup"><span data-stu-id="c2427-149">Add the following necessary GCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="c2427-150">Asegúrese de reemplazar `<your package>` por el nombre del paquete que se muestra en la parte superior del archivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="c2427-150">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="c2427-151">Para más información sobre estos permisos, consulte [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest)(Configuración de una aplicación de cliente GCM para Android).</span><span class="sxs-lookup"><span data-stu-id="c2427-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="c2427-152">Incorporación de código</span><span class="sxs-lookup"><span data-stu-id="c2427-152">Adding code</span></span>
1. <span data-ttu-id="c2427-153">En la Vista de proyecto, expanda **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="c2427-153">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="c2427-154">Haga clic con el botón derecho en la carpeta del paquete en **java**, haga clic en **Nuevo** y, a continuación, haga clic en **Clase Java**.</span><span class="sxs-lookup"><span data-stu-id="c2427-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="c2427-155">Agregue una clase nueva llamada `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="c2427-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio: nueva clase Java][6]
   
    <span data-ttu-id="c2427-157">Asegúrese de actualizar estos tres marcadores de posición en el código siguiente para la clase `NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="c2427-157">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="c2427-158">**SenderId**: número de proyecto que obtuvo anteriormente en la [consola en la nube de Google](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="c2427-158">**SenderId**: The project number you obtained earlier in the [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="c2427-159">**HubListenConnectionString**: la cadena de conexión **DefaultListenAccessSignature** del centro.</span><span class="sxs-lookup"><span data-stu-id="c2427-159">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="c2427-160">Para copiar dicha cadena de conexión, haga clic en **Directivas de acceso** en la hoja **Configuración** de su centro en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c2427-160">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="c2427-161">**HubName**: use el nombre del centro de notificaciones que aparece en la hoja del centro en el [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c2427-161">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="c2427-162">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="c2427-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="c2427-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="c2427-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="c2427-164">}</span><span class="sxs-lookup"><span data-stu-id="c2427-164">}</span></span>
2. <span data-ttu-id="c2427-165">Use los pasos anteriores para agregar otra clase nueva llamada `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="c2427-165">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="c2427-166">Se trata de nuestra implementación de servicio de escucha de Instance ID.</span><span class="sxs-lookup"><span data-stu-id="c2427-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="c2427-167">El código de esta clase llamará a nuestro `IntentService` para [actualizar el token de GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="c2427-167">The code for this class will call our `IntentService` to [refresh the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
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


1. <span data-ttu-id="c2427-168">Agregue otra clase nueva, llamada `RegistrationIntentService`, al proyecto.</span><span class="sxs-lookup"><span data-stu-id="c2427-168">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="c2427-169">Se trata de la implementación de nuestro `IntentService` que controlará la [actualización del token de GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) y el [registro en el Centro de notificaciones](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="c2427-169">This will be the implementation for our `IntentService` that will handle [refreshing the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="c2427-170">Use el siguiente código para esta clase.</span><span class="sxs-lookup"><span data-stu-id="c2427-170">Use the following code for this class.</span></span>
   
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
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="c2427-171">En la clase `MainActivity`, agregue las siguientes instrucciones `import` encima de la declaración de la clase.</span><span class="sxs-lookup"><span data-stu-id="c2427-171">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="c2427-172">Agregue los siguientes miembros privados en la parte superior de la clase.</span><span class="sxs-lookup"><span data-stu-id="c2427-172">Add the following private members at the top of the class.</span></span> <span data-ttu-id="c2427-173">Los usaremos para [comprobar la disponibilidad de Google Play Services, tal como recomienda Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="c2427-173">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="c2427-174">En la clase `MainActivity` , agregue el método siguiente a la disponibilidad de Google Play Services.</span><span class="sxs-lookup"><span data-stu-id="c2427-174">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
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
5. <span data-ttu-id="c2427-175">En su clase `MainActivity`, agregue el siguiente código que se comprobará para Google Play Services antes de llamar a su `IntentService` para obtener el token de registro de GCM y registrarse en el Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c2427-175">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="c2427-176">En el método `OnCreate` de la clase `MainActivity`, agregue el código siguiente para iniciar el proceso de registro cuando se crea la actividad.</span><span class="sxs-lookup"><span data-stu-id="c2427-176">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="c2427-177">Agregue estos métodos adicionales a `MainActivity` para comprobar el estado de la aplicación y el del informe de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2427-177">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="c2427-178">El método `ToastNotify` usa el control *"Hello World"* `TextView` para informar del estado y de las notificaciones de forma persistente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2427-178">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="c2427-179">En el archivo activity_main.xml, agregue el siguiente identificador para ese control.</span><span class="sxs-lookup"><span data-stu-id="c2427-179">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="c2427-180">A continuación, agregaremos una subclase para el receptor que definimos en el archivo AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c2427-180">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="c2427-181">Agregue otra clase nueva, llamada `MyHandler`, al proyecto.</span><span class="sxs-lookup"><span data-stu-id="c2427-181">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="c2427-182">Agregue las siguientes instrucciones de importación en la parte superior de `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="c2427-182">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="c2427-183">Agregue el siguiente código para la clase `MyHandler` para convertirla en una subclase de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="c2427-183">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="c2427-184">Este código invalida el método `OnReceive` , por lo que el controlador informará de las notificaciones que se reciban.</span><span class="sxs-lookup"><span data-stu-id="c2427-184">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="c2427-185">El controlador también envía la notificación push al administrador de notificaciones de Android mediante el método `sendNotification()` .</span><span class="sxs-lookup"><span data-stu-id="c2427-185">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="c2427-186">El método `sendNotification()` se debe ejecutar cuando se reciba una notificación y la aplicación no se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="c2427-186">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="c2427-187">En la barra de menús de Android Studio, haga clic en **Build** (Compilar)  > **Rebuild Project** (Recompilar proyecto) para asegurarse de que no hay errores en el código.</span><span class="sxs-lookup"><span data-stu-id="c2427-187">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="c2427-188">Envío de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="c2427-188">Sending push notifications</span></span>
<span data-ttu-id="c2427-189">Para probar la recepción de notificaciones push en la aplicación, envíelas a través del [Azure Portal] (busque la sección **Solución del problemas** en la hoja del centro, como se muestra a continuación).</span><span class="sxs-lookup"><span data-stu-id="c2427-189">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Centros de notificaciones de Azure: envío de prueba](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="c2427-191">(Opcional) Envío de notificaciones push directamente desde la aplicación</span><span class="sxs-lookup"><span data-stu-id="c2427-191">(Optional) Send push notifications directly from the app</span></span>
<span data-ttu-id="c2427-192">Lo habitual es enviar notificaciones mediante un servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="c2427-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="c2427-193">En algunos casos, puede que quiera enviar notificaciones push directamente desde la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="c2427-193">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="c2427-194">En esta sección se explica cómo enviar notificaciones desde el cliente mediante la [API de REST del Centro de notificaciones de Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2427-194">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="c2427-195">En la vista de proyecto de Android Studio, expanda **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="c2427-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="c2427-196">Abra el archivo de diseño `activity_main.xml` y haga clic en la pestaña **Texto** para actualizar el contenido de texto del archivo.</span><span class="sxs-lookup"><span data-stu-id="c2427-196">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="c2427-197">Actualícelo con el siguiente código, que agrega nuevos controles `Button` y `EditText` para enviar mensajes de notificación push al Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c2427-197">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="c2427-198">Agregue este código al final, inmediatamente antes de `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="c2427-198">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="c2427-199">En la vista de proyecto de Android Studio, expanda **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="c2427-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="c2427-200">Abra el archivo `strings.xml` y agregue los valores de cadena a los que hacen referencia los nuevos controles `Button` y `EditText`.</span><span class="sxs-lookup"><span data-stu-id="c2427-200">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="c2427-201">Agréguelos al final del archivo, justo antes de `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="c2427-201">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="c2427-202">En su archivo `NotificationSetting.java`, agregue la siguiente configuración a la clase `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="c2427-202">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="c2427-203">Actualice `HubFullAccess` con la cadena de conexión **DefaultFullSharedAccessSignature** de su centro.</span><span class="sxs-lookup"><span data-stu-id="c2427-203">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="c2427-204">Esta cadena de conexión se puede copiar desde [Azure Portal]. Para ello, haga clic en **Directivas de acceso** en la hoja **Configuración** del Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c2427-204">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="c2427-205">En el archivo `MainActivity.java`, agregue las siguientes instrucciones `import` antes de la clase `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="c2427-205">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="c2427-206">En el archivo `MainActivity.java`, agregue los siguientes miembros al principio de la clase `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="c2427-206">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="c2427-207">Debe crear un token de firma de acceso a software (SaS) para autenticar una solicitud POST para enviar mensajes a su centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c2427-207">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="c2427-208">Para ello, analice los datos de clave de la cadena de conexión y, luego, cree el token SaS como se menciona en la referencia de API de REST de [Conceptos comunes](http://msdn.microsoft.com/library/azure/dn495627.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2427-208">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="c2427-209">El código siguiente es un ejemplo de implementación.</span><span class="sxs-lookup"><span data-stu-id="c2427-209">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="c2427-210">En `MainActivity.java`, agregue el método siguiente a la clase `MainActivity` para analizar la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="c2427-210">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. <span data-ttu-id="c2427-211">En `MainActivity.java`, agregue el método siguiente a la clase `MainActivity` para crear un token de autenticación SaS.</span><span class="sxs-lookup"><span data-stu-id="c2427-211">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. <span data-ttu-id="c2427-212">En `MainActivity.java`, agregue el método siguiente a la clase `MainActivity` para controlar si se hace clic en el botón **Enviar notificación** y envíe el mensaje de notificación push al centro mediante la API de REST integrada.</span><span class="sxs-lookup"><span data-stu-id="c2427-212">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="c2427-213">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c2427-213">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="c2427-214">Notificaciones push en el emulador</span><span class="sxs-lookup"><span data-stu-id="c2427-214">Push notifications in the emulator</span></span>
<span data-ttu-id="c2427-215">Si desea probar notificaciones push en un emulador, asegúrese de que la imagen del emulador admita el nivel de API de Google que elija para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2427-215">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="c2427-216">Si la imagen no es compatible con las API de Google nativas, aparecerá la excepción **SERVICE\_NOT\_AVAILABLE**.</span><span class="sxs-lookup"><span data-stu-id="c2427-216">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="c2427-217">Además, asegúrese de haber agregado su cuenta de Google al emulador en ejecución en **Configuración** > **Cuentas**.</span><span class="sxs-lookup"><span data-stu-id="c2427-217">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="c2427-218">De lo contrario, sus intentos de registrarse con GCM podrían generar la excepción **AUTHENTICATION\_FAILED**.</span><span class="sxs-lookup"><span data-stu-id="c2427-218">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="c2427-219">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c2427-219">Running the application</span></span>
1. <span data-ttu-id="c2427-220">Ejecute la aplicación y observe que el Id. de registro se informa para un registro correcto.</span><span class="sxs-lookup"><span data-stu-id="c2427-220">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
      ![Prueba en Android: registro de canal][18]
2. <span data-ttu-id="c2427-222">Escriba un mensaje de notificación que se enviará a todos los dispositivos Android registrados con el centro.</span><span class="sxs-lookup"><span data-stu-id="c2427-222">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
      ![Prueba en Android - envío de un mensaje][19]

3. <span data-ttu-id="c2427-224">Presione **Enviar notificación**.</span><span class="sxs-lookup"><span data-stu-id="c2427-224">Press **Send Notification**.</span></span> <span data-ttu-id="c2427-225">Los dispositivos en los que se ejecute la aplicación mostrarán un instancia de `AlertDialog` con el mensaje de notificación push.</span><span class="sxs-lookup"><span data-stu-id="c2427-225">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="c2427-226">Los dispositivos en que la aplicación no esté en ejecución, pero que anteriormente se hayan registrado para recibir notificaciones push, recibirán una notificación en el administrador de notificaciones de Android.</span><span class="sxs-lookup"><span data-stu-id="c2427-226">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="c2427-227">Para verlas, deslice el dedo hacia abajo desde la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="c2427-227">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
      ![Prueba en Android - notificaciones][21]

## <a name="next-steps"></a><span data-ttu-id="c2427-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2427-229">Next steps</span></span>
<span data-ttu-id="c2427-230">Se recomienda seguir el tutorial [Notificación a los usuarios con los Centros de notificaciones de Azure] como paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="c2427-230">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="c2427-231">Le mostrará cómo enviar notificaciones desde un back-end de ASP.NET mediante etiquetas para dirigirse a usuarios específicos.</span><span class="sxs-lookup"><span data-stu-id="c2427-231">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="c2427-232">Si desea segmentar los usuarios por grupos de interés, consulte el tutorial [Uso de Notification Hubs para enviar noticias de última hora] .</span><span class="sxs-lookup"><span data-stu-id="c2427-232">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="c2427-233">Para más información sobre los Centros de notificaciones, consulte [Introducción a los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="c2427-233">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="c2427-234">[Introducción a los centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="c2427-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="c2427-235">[Notificación a los usuarios con los Centros de notificaciones de Azure]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="c2427-235">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="c2427-236">[Uso de Notification Hubs para enviar noticias de última hora]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="c2427-236">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="c2427-237">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="c2427-237">[Azure Portal]: https://portal.azure.com</span></span>
