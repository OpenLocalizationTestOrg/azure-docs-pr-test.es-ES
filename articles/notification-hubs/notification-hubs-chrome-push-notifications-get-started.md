---
title: "aplicaciones de tooChrome de notificaciones de inserción de aaaSend con centros de notificaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa aplicación Chrome."
services: notification-hubs
keywords: "notificaciones push móviles,notificaciones push,notificación push,notificaciones push android"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="db1cc-104">Enviar notificaciones tooChrome aplicaciones con Azure centros de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="db1cc-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="db1cc-105">Este tema muestra cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa aplicación de Chrome, que se mostrará en el contexto de Hola de hello explorador Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="db1cc-106">En este tutorial, creará una aplicación de Chrome que recibirá notificaciones push mediante el [Servicio de mensajería en la nube de Google (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="db1cc-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="db1cc-107">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="db1cc-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="db1cc-108">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="db1cc-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="db1cc-109">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="db1cc-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="db1cc-110">Hola tutorial le guía a través de estas notificaciones de inserción de tooenable pasos básicos:</span><span class="sxs-lookup"><span data-stu-id="db1cc-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="db1cc-111">Habilitación del servicio de mensajería en la nube de Google</span><span class="sxs-lookup"><span data-stu-id="db1cc-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="db1cc-112">Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="db1cc-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="db1cc-113">Conectar el centro de notificaciones de aplicación de Chrome toohello</span><span class="sxs-lookup"><span data-stu-id="db1cc-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="db1cc-114">Enviar una tooyour de notificación de inserción aplicación Chrome</span><span class="sxs-lookup"><span data-stu-id="db1cc-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="db1cc-115">Funcionalidades y funciones adicionales</span><span class="sxs-lookup"><span data-stu-id="db1cc-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="db1cc-116">Notificaciones de inserción de aplicación de Chrome no son genéricas notificaciones en el explorador: son modelo de extensibilidad de explorador específico toohello (consulte [información general de aplicaciones de Chrome] para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="db1cc-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="db1cc-117">Además toohello Explorador de escritorio, aplicaciones de Chrome ejecutan en móviles (iOS y Android) a través de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="db1cc-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="db1cc-118">Vea [aplicaciones Chrome en Mobile] toolearn más.</span><span class="sxs-lookup"><span data-stu-id="db1cc-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="db1cc-119">Configuración de GCM y centros de notificaciones de Azure es tooconfiguring idéntico para Android, ya que [Google Cloud Messaging para Chrome] ha quedado desusado y Hola GCM mismo ahora es compatible con los dispositivos Android y las instancias de Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="db1cc-120"><a id="register"></a>Habilitación del servicio de mensajería en la nube de Google</span><span class="sxs-lookup"><span data-stu-id="db1cc-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="db1cc-121">Navegue toohello [consola en la nube de Google] de sitio Web, inicie sesión con sus credenciales de cuenta de Google y, a continuación, haga clic en hello **crear proyecto** botón.</span><span class="sxs-lookup"><span data-stu-id="db1cc-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="db1cc-122">Proporcione un **nombre del proyecto**y, a continuación, haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="db1cc-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="db1cc-123">Tome nota de hello **número de proyecto** en hello **proyectos** página de proyecto de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="db1cc-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="db1cc-124">Se usará como hello **Id. de remitente de GCM** en tooregister de Chrome aplicación Hola con GCM.</span><span class="sxs-lookup"><span data-stu-id="db1cc-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="db1cc-125">En el panel izquierdo de hello, haga clic en **API & auth**y, a continuación, desplácese hacia abajo y haga clic en hello alternar tooenable **Google Cloud Messaging para Android**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="db1cc-126">No tienes tooenable **Google Cloud Messaging para Chrome**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="db1cc-127">En el panel izquierdo de hello, haga clic en **credenciales** > **crear nueva clave** > **clave Server** > **crear**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="db1cc-128">Tome nota del servidor hello **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="db1cc-129">Se configurará en su tooenable siguiente, del concentrador de notificación tooGCM de notificaciones de inserción de toosend.</span><span class="sxs-lookup"><span data-stu-id="db1cc-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="db1cc-130"><a id="configure-hub"></a>Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="db1cc-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="db1cc-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="db1cc-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="db1cc-132">Hola **configuración** hoja, seleccione **Notification Services** y, a continuación, **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="db1cc-133">Escriba la clave de API de Hola y guardar.</span><span class="sxs-lookup"><span data-stu-id="db1cc-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Centros de notificaciones de Azure: Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="db1cc-135"><a id="connect-app"></a>Conectar el centro de notificaciones de aplicación de Chrome toohello</span><span class="sxs-lookup"><span data-stu-id="db1cc-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="db1cc-136">El centro de notificaciones está ahora configurado toowork con GCM y tiene tooregister de cadenas de conexión de hello tooboth de la aplicación de recepción y envío de notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="db1cc-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="db1cc-137">LK</span><span class="sxs-lookup"><span data-stu-id="db1cc-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="db1cc-138">Creación de una nueva aplicación Chrome</span><span class="sxs-lookup"><span data-stu-id="db1cc-138">Create a new Chrome App</span></span>
<span data-ttu-id="db1cc-139">ejemplo de Hola a continuación se basa en hello [Chrome aplicación GCM ejemplo] y utiliza Hola recomienda forma toocreate una aplicación de Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="db1cc-140">Nos centraremos en hello pasos relacionados específicamente con tooAzure centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="db1cc-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="db1cc-141">Recomendamos que descargue origen Hola para esta aplicación de Chrome desde [ejemplo de concentrador de notificación de aplicación de Chrome].</span><span class="sxs-lookup"><span data-stu-id="db1cc-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="db1cc-142">Hola Chrome aplicación se crea a través de JavaScript, y puede utilizar cualquiera de los editores de word preferido para crearlo.</span><span class="sxs-lookup"><span data-stu-id="db1cc-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="db1cc-143">A continuación se muestra cuál será el aspecto de esta aplicación Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-143">Below is what this Chrome App will look like.</span></span>

![Aplicación de Google Chrome][15]

1. <span data-ttu-id="db1cc-145">Cree una carpeta y asígnele el nombre `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="db1cc-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="db1cc-146">Por supuesto, el nombre de hello es arbitrario: si asigna un nombre algo diferente, asegúrese de que sustituir ruta de acceso de hello en segmentos de código de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="db1cc-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="db1cc-147">Descargar hello [crypto-js biblioteca] en carpeta de Hola que creó en el segundo paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="db1cc-148">Esta carpeta de biblioteca contendrá dos subcarpetas: `components` y `rollups`.</span><span class="sxs-lookup"><span data-stu-id="db1cc-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="db1cc-149">Cree un archivo `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="db1cc-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="db1cc-150">Todas las aplicaciones de Chrome están respaldadas por un archivo de manifiesto que contiene los metadatos de la aplicación hello y, más importante aún, todos los permisos que se conceden toohello aplicación al usuario Hola lo instala.</span><span class="sxs-lookup"><span data-stu-id="db1cc-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="db1cc-151">Hola aviso `permissions` elemento, que especifica que esta aplicación de Chrome será capaz de tooreceive notificaciones de inserción de GCM.</span><span class="sxs-lookup"><span data-stu-id="db1cc-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="db1cc-152">También debe especificar Hola URI de centros de notificaciones de Azure donde hello Chrome aplicación hará que un tooregister de llamada REST.</span><span class="sxs-lookup"><span data-stu-id="db1cc-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="db1cc-153">Nuestra aplicación de ejemplo también usa un archivo de icono, `gcm_128.png`, que encontrará en origen de Hola que reutiliza de muestra de Hola original GCM.</span><span class="sxs-lookup"><span data-stu-id="db1cc-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="db1cc-154">Se puede sustituir por cualquier imagen que se adapte a hello [criterios de icono](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="db1cc-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="db1cc-155">Cree un archivo denominado `background.js` con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="db1cc-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="db1cc-156">Se trata de archivo hello que se abre una ventana de aplicación de Chrome Hola HTML (**register.html**) y también define el controlador de hello **messageReceived** notificación de inserción de toohandle Hola entrantes.</span><span class="sxs-lookup"><span data-stu-id="db1cc-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="db1cc-157">Cree un archivo denominado `register.html` -Esto define la interfaz de usuario de hello Chrome aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="db1cc-158">En este ejemplo se usa **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="db1cc-159">Si descargó otra versión de biblioteca de hello, asegúrese de que se sustituye correctamente la versión de Hola Hola `src` ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="db1cc-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="db1cc-160">Cree un archivo denominado `register.js` con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="db1cc-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="db1cc-161">Este archivo especifica el script de Hola detrás de `register.html`.</span><span class="sxs-lookup"><span data-stu-id="db1cc-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="db1cc-162">Aplicaciones de Chrome no permitir la ejecución de en línea, por lo que tendrá toocreate una secuencia de comandos de copia de seguridad independiente para la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="db1cc-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="db1cc-163">Hola por encima de la secuencia de comandos tiene Hola parámetros claves siguientes:</span><span class="sxs-lookup"><span data-stu-id="db1cc-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="db1cc-164">**Window.OnLoad** define los eventos de clic de botón de Hola de botones de hello dos en hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="db1cc-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="db1cc-165">Uno se registra con GCM y Hola otro utiliza el Id. de registro de hello que aparece después del registro con GCM tooregister con centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="db1cc-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="db1cc-166">**updateLog** es la función hello que nos permite toohandle capacidades de registro simple.</span><span class="sxs-lookup"><span data-stu-id="db1cc-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="db1cc-167">**registerWithGCM** es controlador de clic de botón primera hello, lo que hace hello `chrome.gcm.register` llamada tooGCM tooregister Hola Chrome aplicación instancia actual.</span><span class="sxs-lookup"><span data-stu-id="db1cc-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="db1cc-168">**registerCallback** es Hola función de devolución de llamada que se invoca cuando la devolución de llamada de registro GCM Hola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="db1cc-169">**registerWithNH** es el controlador de clic de botón segundo hello, que se registra con centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="db1cc-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="db1cc-170">Obtiene `hubName` y `connectionString` (qué usuario Hola especificó) y manualidades Hola llamada API de REST de registro de bases de datos centrales de notificación.</span><span class="sxs-lookup"><span data-stu-id="db1cc-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="db1cc-171">**splitConnectionString** y **generateSaSToken** son aplicaciones auxiliares que representan la implementación de JavaScript de Hola de un proceso de creación del token de SaS, que debe usarse en todas las llamadas de API de REST.</span><span class="sxs-lookup"><span data-stu-id="db1cc-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="db1cc-172">Para más información, vea [Conceptos comunes](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="db1cc-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="db1cc-173">**sendNHRegistrationRequest** se tooAzure centros de notificaciones de llamadas a función hello que realiza un HTTP REST.</span><span class="sxs-lookup"><span data-stu-id="db1cc-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="db1cc-174">**registrationPayload** define la carga XML de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="db1cc-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="db1cc-175">Para obtener más información, consulte [Crear registro].</span><span class="sxs-lookup"><span data-stu-id="db1cc-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="db1cc-176">Actualizamos Id. del registro de hello en ella con lo que hemos recibido de GCM.</span><span class="sxs-lookup"><span data-stu-id="db1cc-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="db1cc-177">**cliente** es una instancia de **XMLHttpRequest** que usar la solicitud HTTP POST de toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="db1cc-178">Tenga en cuenta que actualizamos hello `Authorization` encabezado con `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="db1cc-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="db1cc-179">La finalización correcta de esta llamada registrará esta instancia de la aplicación Chrome con Centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="db1cc-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="db1cc-180">Hello general estructura de carpetas para este proyecto debe ser similar a este: ![aplicación de Google Chrome: estructura de carpetas][21]</span><span class="sxs-lookup"><span data-stu-id="db1cc-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="db1cc-181">Configuración y prueba de la aplicación Chrome</span><span class="sxs-lookup"><span data-stu-id="db1cc-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="db1cc-182">Abra el explorador Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-182">Open your Chrome browser.</span></span> <span data-ttu-id="db1cc-183">Abra las **extensiones de Chrome** y habilite el **modo de desarrollador**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="db1cc-184">Haga clic en **cargar la extensión desempaquetado** y desplazarse por las carpetas de toohello donde creó archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="db1cc-185">Opcionalmente, también puede usar hello **aplicaciones Chrome & herramienta de desarrollo de extensiones**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="db1cc-186">Esta herramienta es una aplicación de Chrome en sí misma (instalada de hello almacén Web de Chrome) y proporciona funciones de depuración avanzadas para el desarrollo de aplicaciones de Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="db1cc-187">Si Hola Chrome aplicación se crea sin errores, a continuación, verá la aplicación de Chrome mostrarán.</span><span class="sxs-lookup"><span data-stu-id="db1cc-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="db1cc-188">Escriba hello **número de proyecto** obtenido anteriormente de hello **consola en la nube de Google** como Id. de remitente de Hola y haga clic en **registrar con GCM**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="db1cc-189">Debe ver mensajes de bienvenida **registro con GCM se realizó correctamente.**</span><span class="sxs-lookup"><span data-stu-id="db1cc-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="db1cc-190">Escriba su **nombre del concentrador de notificación** hello y **DefaultListenSharedAccessSignature** que obtuvo de portal de hello anteriormente y haga clic en **registrar con el centro de notificaciones de Azure**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="db1cc-191">Debe ver mensajes de bienvenida **registro de centro de notificaciones correctas.**</span><span class="sxs-lookup"><span data-stu-id="db1cc-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="db1cc-192">y detalles de Hola de respuesta de registro de hello, que contiene el registro de los centros de notificaciones de Azure Hola por identificador.</span><span class="sxs-lookup"><span data-stu-id="db1cc-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="db1cc-193"><a name="send"></a>Enviar una aplicación de Chrome tooyour de notificación</span><span class="sxs-lookup"><span data-stu-id="db1cc-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="db1cc-194">Para las pruebas, enviaremos notificaciones push de Chrome mediante la aplicación de consola de .NET.</span><span class="sxs-lookup"><span data-stu-id="db1cc-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="db1cc-195">Puede enviar notificaciones push con los Centros de notificaciones desde cualquier back-end a través de la <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaz de REST</a>.</span><span class="sxs-lookup"><span data-stu-id="db1cc-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="db1cc-196">Consulte el [portal de documentación](https://azure.microsoft.com/documentation/services/notification-hubs/) para obtener más ejemplos multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="db1cc-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="db1cc-197">En Visual Studio, desde hello **archivo** menú, seleccione **New** y, a continuación, **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="db1cc-198">En **Visual C#**, haga clic en **Windows** y **Aplicación de consola** y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="db1cc-199">Esto crea un nuevo proyecto de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="db1cc-200">De hello **herramientas** menú, haga clic en **Administrador de paquetes de biblioteca** y, a continuación, **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="db1cc-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="db1cc-201">Esto muestra hello Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="db1cc-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="db1cc-202">En la ventana de la consola de hello, ejecute Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db1cc-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="db1cc-203">Abra `Program.cs` y agregue los siguiente hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="db1cc-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="db1cc-204">Hola `Program` clase, agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="db1cc-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="db1cc-205">Asegúrese de que usar cadena de conexión de hello con **completa** acceso, no **escuchar** acceso.</span><span class="sxs-lookup"><span data-stu-id="db1cc-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="db1cc-206">Hola **escuchar** cadena de conexión de acceso no conceder permisos de notificaciones de inserción de toosend.</span><span class="sxs-lookup"><span data-stu-id="db1cc-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="db1cc-207">Agregar llamadas a siguiente hello en hello `Main` método:</span><span class="sxs-lookup"><span data-stu-id="db1cc-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="db1cc-208">Asegúrese de que se está ejecutando Chrome y ejecutar la aplicación de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="db1cc-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="db1cc-209">Debería ver Hola siguiente elemento emergente en el escritorio de notificación.</span><span class="sxs-lookup"><span data-stu-id="db1cc-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="db1cc-210">También puede ver todas las notificaciones mediante la ventana de notificaciones de cromo de hello en la barra de tareas de hello (en Windows) cuando se está ejecutando Chrome.</span><span class="sxs-lookup"><span data-stu-id="db1cc-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="db1cc-211">No es necesario toohave Hola Chrome aplicación abrir en el Explorador de Hola o en ejecución (aunque el propio explorador de Chrome Hola debe estar ejecutándose).</span><span class="sxs-lookup"><span data-stu-id="db1cc-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="db1cc-212">También obtendrá una vista consolidada de todas las notificaciones en la ventana de notificaciones de Chrome hello.</span><span class="sxs-lookup"><span data-stu-id="db1cc-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="db1cc-213"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db1cc-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="db1cc-214">Obtenga más información sobre Centros de notificaciones en [Introducción a los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="db1cc-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="db1cc-215">tootarget usuarios específicos, consulte toohello [notificación centros de notificar a los usuarios de Azure] tutorial.</span><span class="sxs-lookup"><span data-stu-id="db1cc-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="db1cc-216">Si desea toosegment los usuarios por grupos de interés, puede seguir hello [centros de notificaciones de Azure noticias de última hora] tutorial.</span><span class="sxs-lookup"><span data-stu-id="db1cc-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[ejemplo de concentrador de notificación de aplicación de Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[consola en la nube de Google]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Introducción a los centros de notificaciones]: notification-hubs-push-notification-overview.md
[información general de aplicaciones de Chrome]: https://developer.chrome.com/apps/about_apps
[Chrome aplicación GCM ejemplo]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[aplicaciones Chrome en Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Crear registro]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js biblioteca]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging para Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[notificación centros de notificar a los usuarios de Azure]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[centros de notificaciones de Azure noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
