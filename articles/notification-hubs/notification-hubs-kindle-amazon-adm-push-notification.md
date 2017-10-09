---
title: aaaGet comenzar con centros de notificaciones de Azure para aplicaciones Kindle | Documentos de Microsoft
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push aplicación de notificaciones de tooa Kindle."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="2a2cc-103">Introducción a Centros de notificaciones para aplicaciones Kindle</span><span class="sxs-lookup"><span data-stu-id="2a2cc-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2a2cc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2a2cc-104">Overview</span></span>
<span data-ttu-id="2a2cc-105">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de notificaciones de tooa Kindle.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="2a2cc-106">Creará una aplicación Kindle vacía que recibirá notificaciones push mediante Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a2cc-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a2cc-107">Prerequisites</span></span>
<span data-ttu-id="2a2cc-108">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="2a2cc-109">Obtener Hola Android SDK (se supone que va a usar Eclipse) de hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sitio Android</a>.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="2a2cc-110">Siga los pasos de hello en <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">configuración del entorno de desarrollo</a> tooset del entorno de desarrollo para Kindle.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="2a2cc-111">Agregar un nuevo portal para desarrolladores de aplicaciones toohello</span><span class="sxs-lookup"><span data-stu-id="2a2cc-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="2a2cc-112">En primer lugar, cree una aplicación Hola [portal para desarrolladores de Amazon].</span><span class="sxs-lookup"><span data-stu-id="2a2cc-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="2a2cc-113">Hola copia **clave de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="2a2cc-114">En el portal de hello, haga clic en nombre de saludo de la aplicación y, a continuación, haga clic en hello **Device Messaging** ficha.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="2a2cc-115">Haga clic en **Create a New Security Profile** (Crear un nuevo perfil de seguridad) y, luego, cree un nuevo perfil de seguridad (por ejemplo, **perfil de seguridad TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="2a2cc-116">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="2a2cc-117">Haga clic en **seguridad perfiles** perfil de seguridad de hello tooview que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="2a2cc-118">Hola copia **Id. de cliente** y **secreto de cliente** valores para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="2a2cc-119">Creación de una clave de API</span><span class="sxs-lookup"><span data-stu-id="2a2cc-119">Create an API key</span></span>
1. <span data-ttu-id="2a2cc-120">Abra un símbolo del sistema con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="2a2cc-121">Desplazarse por las carpetas del SDK de Android toohello.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="2a2cc-122">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="2a2cc-123">Para hello **keystore** contraseña, escriba **android**.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="2a2cc-124">Hola copia **MD5** huellas digitales.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="2a2cc-125">En el portal para desarrolladores de hello, en hello **mensajería** , haga clic en **Android/Kindle** y escriba el nombre hello del paquete de hello para la aplicación (por ejemplo, **com.sample.notificationhubtest**) hello y **MD5** valor y, a continuación, haga clic en **generar clave de API**.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="2a2cc-126">Agregar credenciales toohello centro</span><span class="sxs-lookup"><span data-stu-id="2a2cc-126">Add credentials toohello hub</span></span>
<span data-ttu-id="2a2cc-127">En el portal de hello, agregar toohello del Id. de cliente y secreto de cliente hello **configurar** ficha del centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="2a2cc-128">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2a2cc-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="2a2cc-129">Al crear un aplicación, use al menos el nivel de API 17.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="2a2cc-130">Agregar proyecto de Eclipse de hello ADM bibliotecas tooyour:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="2a2cc-131">biblioteca ADM de tooobtain hello, [descargar Hola SDK].</span><span class="sxs-lookup"><span data-stu-id="2a2cc-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="2a2cc-132">Extraiga el archivo zip del SDK Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="2a2cc-133">En Eclipse, haga clic con el botón derecho en el proyecto y, a continuación, haga clic en **Propiedades**(Propiedades).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="2a2cc-134">Seleccione **Java Build Path** en Hola deja y, a continuación, seleccione Hola ** bibliotecas ** ficha situada en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="2a2cc-135">Haga clic en **agregar Jar externo**y el archivo hello seleccione `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` del directorio de hello en la que extrajo Hola SDK de Amazon.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="2a2cc-136">Descargar hello NotificationHubs Android SDK (vínculo).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="2a2cc-137">Descomprima el paquete de hello y, a continuación, arrastre el archivo hello `notification-hubs-sdk.jar` en hello `libs` carpeta en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="2a2cc-138">Edite el ADM de toosupport manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="2a2cc-139">Agregue el espacio de nombres de hello Amazon en elemento de manifiesto Hola raíz:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="2a2cc-140">Agregue permisos como primer elemento de hello en el elemento manifiesto Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="2a2cc-141">SUBSTITUTE **[el nombre del paquete]** con paquete de hello usa toocreate la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="2a2cc-142">Insertar Hola siguiente elemento como primer elemento secundario del elemento de la aplicación Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="2a2cc-143">Recuerde toosubstitute **[su nombre de servicio]** con el nombre de Hola de su controlador de mensajes ADM que cree en la sección siguiente de hello (paquete de hello incluidos) y reemplace **[el nombre del paquete]** con hello nombre del paquete con la que se creó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="2a2cc-144">Creación del controlador de mensajes de ADM</span><span class="sxs-lookup"><span data-stu-id="2a2cc-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="2a2cc-145">Cree una nueva clase que hereda de `com.amazon.device.messaging.ADMMessageHandlerBase` y asígnele el nombre `MyADMMessageHandler`, tal y como se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="2a2cc-146">Agregue los siguiente hello `import` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="2a2cc-147">Agregar Hola después el código de clase de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="2a2cc-148">Recuerde toosubstitute Hola concentrador nombre de cadena de conexión y (escuchar):</span><span class="sxs-lookup"><span data-stu-id="2a2cc-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="2a2cc-149">Agregar Hola después código toohello `OnMessage()` método:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="2a2cc-150">Agregar Hola después código toohello `OnRegistered` método:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="2a2cc-151">Agregar Hola después código toohello `OnUnregistered` método:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="2a2cc-152">Hola `MainActivity` método, agregue Hola después de la instrucción import:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="2a2cc-153">Agregar Hola siguiente código al final de Hola de hello `OnCreate` método:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="2a2cc-154">Agregar la aplicación de tooyour clave de API</span><span class="sxs-lookup"><span data-stu-id="2a2cc-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="2a2cc-155">En Eclipse, cree un nuevo archivo denominado **api_key.txt** en activos de hello directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="2a2cc-156">Hola abrir archivo y copie Hola clave de API que generó en el portal para desarrolladores de Amazon Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="2a2cc-157">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="2a2cc-157">Run hello app</span></span>
1. <span data-ttu-id="2a2cc-158">Inicie el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-158">Start hello emulator.</span></span>
2. <span data-ttu-id="2a2cc-159">En el emulador de Windows hello, deslice el dedo desde la parte superior de Hola y haga clic en **configuración**y, a continuación, haga clic en **mi cuenta** y se registre con una cuenta válida de Amazon.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="2a2cc-160">En Eclipse, ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="2a2cc-161">Si se produce un problema, compruebe la hora de hello del emulador de hello (o dispositivo).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="2a2cc-162">valor de tiempo de Hello debe ser precisa.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-162">hello time value must be accurate.</span></span> <span data-ttu-id="2a2cc-163">tiempo de hello toochange del emulador en hello Kindle, puede ejecutar Hola siguiente comando desde el directorio de herramientas de la plataforma de SDK de Android:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="2a2cc-164">Envío de un mensaje</span><span class="sxs-lookup"><span data-stu-id="2a2cc-164">Send a message</span></span>
<span data-ttu-id="2a2cc-165">toosend un mensaje mediante el uso de. NET:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portal para desarrolladores de Amazon]: https://developer.amazon.com/home.html
[descargar Hola SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
