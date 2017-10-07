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
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Enviar notificaciones tooChrome aplicaciones con Azure centros de notificaciones de inserción
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Este tema muestra cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa aplicación de Chrome, que se mostrará en el contexto de Hola de hello explorador Google Chrome. En este tutorial, creará una aplicación de Chrome que recibirá notificaciones push mediante el [Servicio de mensajería en la nube de Google (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

Hola tutorial le guía a través de estas notificaciones de inserción de tooenable pasos básicos:

* [Habilitación del servicio de mensajería en la nube de Google](#register)
* [Configuración de su Centro de notificaciones](#configure-hub)
* [Conectar el centro de notificaciones de aplicación de Chrome toohello](#connect-app)
* [Enviar una tooyour de notificación de inserción aplicación Chrome](#send)
* [Funcionalidades y funciones adicionales](#next-steps)

> [!NOTE]
> Notificaciones de inserción de aplicación de Chrome no son genéricas notificaciones en el explorador: son modelo de extensibilidad de explorador específico toohello (consulte [información general de aplicaciones de Chrome] para obtener más información). Además toohello Explorador de escritorio, aplicaciones de Chrome ejecutan en móviles (iOS y Android) a través de Apache Cordova. Vea [aplicaciones Chrome en Mobile] toolearn más.
> 
> 

Configuración de GCM y centros de notificaciones de Azure es tooconfiguring idéntico para Android, ya que [Google Cloud Messaging para Chrome] ha quedado desusado y Hola GCM mismo ahora es compatible con los dispositivos Android y las instancias de Chrome.

## <a id="register"></a>Habilitación del servicio de mensajería en la nube de Google
1. Navegue toohello [consola en la nube de Google] de sitio Web, inicie sesión con sus credenciales de cuenta de Google y, a continuación, haga clic en hello **crear proyecto** botón. Proporcione un **nombre del proyecto**y, a continuación, haga clic en hello **crear** botón.
   
       ![Google Cloud Console - Create Project][1]
2. Tome nota de hello **número de proyecto** en hello **proyectos** página de proyecto de Hola que acaba de crear. Se usará como hello **Id. de remitente de GCM** en tooregister de Chrome aplicación Hola con GCM.
   
       ![Google Cloud Console - Project Number][2]
3. En el panel izquierdo de hello, haga clic en **API & auth**y, a continuación, desplácese hacia abajo y haga clic en hello alternar tooenable **Google Cloud Messaging para Android**. No tienes tooenable **Google Cloud Messaging para Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. En el panel izquierdo de hello, haga clic en **credenciales** > **crear nueva clave** > **clave Server** > **crear**.
   
       ![Google Cloud Console - Credentials][4]
5. Tome nota del servidor hello **clave de API**. Se configurará en su tooenable siguiente, del concentrador de notificación tooGCM de notificaciones de inserción de toosend.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Configuración de su Centro de notificaciones
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Hola **configuración** hoja, seleccione **Notification Services** y, a continuación, **Google (GCM)**. Escriba la clave de API de Hola y guardar.

&emsp;&emsp;![Centros de notificaciones de Azure: Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Conectar el centro de notificaciones de aplicación de Chrome toohello
El centro de notificaciones está ahora configurado toowork con GCM y tiene tooregister de cadenas de conexión de hello tooboth de la aplicación de recepción y envío de notificaciones de inserción. LK

### <a name="create-a-new-chrome-app"></a>Creación de una nueva aplicación Chrome
ejemplo de Hola a continuación se basa en hello [Chrome aplicación GCM ejemplo] y utiliza Hola recomienda forma toocreate una aplicación de Chrome. Nos centraremos en hello pasos relacionados específicamente con tooAzure centros de notificaciones. 

> [!NOTE]
> Recomendamos que descargue origen Hola para esta aplicación de Chrome desde [ejemplo de concentrador de notificación de aplicación de Chrome].
> 
> 

Hola Chrome aplicación se crea a través de JavaScript, y puede utilizar cualquiera de los editores de word preferido para crearlo. A continuación se muestra cuál será el aspecto de esta aplicación Chrome.

![Aplicación de Google Chrome][15]

1. Cree una carpeta y asígnele el nombre `ChromePushApp`. Por supuesto, el nombre de hello es arbitrario: si asigna un nombre algo diferente, asegúrese de que sustituir ruta de acceso de hello en segmentos de código de hello necesario.
2. Descargar hello [crypto-js biblioteca] en carpeta de Hola que creó en el segundo paso de Hola. Esta carpeta de biblioteca contendrá dos subcarpetas: `components` y `rollups`.
3. Cree un archivo `manifest.json` . Todas las aplicaciones de Chrome están respaldadas por un archivo de manifiesto que contiene los metadatos de la aplicación hello y, más importante aún, todos los permisos que se conceden toohello aplicación al usuario Hola lo instala.
   
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
   
    Hola aviso `permissions` elemento, que especifica que esta aplicación de Chrome será capaz de tooreceive notificaciones de inserción de GCM. También debe especificar Hola URI de centros de notificaciones de Azure donde hello Chrome aplicación hará que un tooregister de llamada REST.
    Nuestra aplicación de ejemplo también usa un archivo de icono, `gcm_128.png`, que encontrará en origen de Hola que reutiliza de muestra de Hola original GCM. Se puede sustituir por cualquier imagen que se adapte a hello [criterios de icono](https://developer.chrome.com/apps/manifest/icons).
4. Cree un archivo denominado `background.js` con hello siguiente código:
   
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
   
    Se trata de archivo hello que se abre una ventana de aplicación de Chrome Hola HTML (**register.html**) y también define el controlador de hello **messageReceived** notificación de inserción de toohandle Hola entrantes.
5. Cree un archivo denominado `register.html` -Esto define la interfaz de usuario de hello Chrome aplicación Hola. 
   
   > [!NOTE]
   > En este ejemplo se usa **CryptoJS v3.1.2**. Si descargó otra versión de biblioteca de hello, asegúrese de que se sustituye correctamente la versión de Hola Hola `src` ruta de acceso.
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
6. Cree un archivo denominado `register.js` con el siguiente código de hello. Este archivo especifica el script de Hola detrás de `register.html`. Aplicaciones de Chrome no permitir la ejecución de en línea, por lo que tendrá toocreate una secuencia de comandos de copia de seguridad independiente para la interfaz de usuario.
   
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
   
    Hola por encima de la secuencia de comandos tiene Hola parámetros claves siguientes:
   
   * **Window.OnLoad** define los eventos de clic de botón de Hola de botones de hello dos en hello interfaz de usuario. Uno se registra con GCM y Hola otro utiliza el Id. de registro de hello que aparece después del registro con GCM tooregister con centros de notificaciones de Azure.
   * **updateLog** es la función hello que nos permite toohandle capacidades de registro simple.
   * **registerWithGCM** es controlador de clic de botón primera hello, lo que hace hello `chrome.gcm.register` llamada tooGCM tooregister Hola Chrome aplicación instancia actual.
   * **registerCallback** es Hola función de devolución de llamada que se invoca cuando la devolución de llamada de registro GCM Hola.
   * **registerWithNH** es el controlador de clic de botón segundo hello, que se registra con centros de notificaciones. Obtiene `hubName` y `connectionString` (qué usuario Hola especificó) y manualidades Hola llamada API de REST de registro de bases de datos centrales de notificación.
   * **splitConnectionString** y **generateSaSToken** son aplicaciones auxiliares que representan la implementación de JavaScript de Hola de un proceso de creación del token de SaS, que debe usarse en todas las llamadas de API de REST. Para más información, vea [Conceptos comunes](http://msdn.microsoft.com/library/dn495627.aspx).
   * **sendNHRegistrationRequest** se tooAzure centros de notificaciones de llamadas a función hello que realiza un HTTP REST.
   * **registrationPayload** define la carga XML de registro de hello. Para obtener más información, consulte [Crear registro]. Actualizamos Id. del registro de hello en ella con lo que hemos recibido de GCM.
   * **cliente** es una instancia de **XMLHttpRequest** que usar la solicitud HTTP POST de toomake Hola. Tenga en cuenta que actualizamos hello `Authorization` encabezado con `sasToken`. La finalización correcta de esta llamada registrará esta instancia de la aplicación Chrome con Centros de notificaciones de Azure.

Hello general estructura de carpetas para este proyecto debe ser similar a este: ![aplicación de Google Chrome: estructura de carpetas][21]

### <a name="set-up-and-test-your-chrome-app"></a>Configuración y prueba de la aplicación Chrome
1. Abra el explorador Chrome. Abra las **extensiones de Chrome** y habilite el **modo de desarrollador**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Haga clic en **cargar la extensión desempaquetado** y desplazarse por las carpetas de toohello donde creó archivos Hola. Opcionalmente, también puede usar hello **aplicaciones Chrome & herramienta de desarrollo de extensiones**. Esta herramienta es una aplicación de Chrome en sí misma (instalada de hello almacén Web de Chrome) y proporciona funciones de depuración avanzadas para el desarrollo de aplicaciones de Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Si Hola Chrome aplicación se crea sin errores, a continuación, verá la aplicación de Chrome mostrarán.
   
       ![Google Chrome - Chrome App Display][18]
4. Escriba hello **número de proyecto** obtenido anteriormente de hello **consola en la nube de Google** como Id. de remitente de Hola y haga clic en **registrar con GCM**. Debe ver mensajes de bienvenida **registro con GCM se realizó correctamente.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Escriba su **nombre del concentrador de notificación** hello y **DefaultListenSharedAccessSignature** que obtuvo de portal de hello anteriormente y haga clic en **registrar con el centro de notificaciones de Azure**. Debe ver mensajes de bienvenida **registro de centro de notificaciones correctas.** y detalles de Hola de respuesta de registro de hello, que contiene el registro de los centros de notificaciones de Azure Hola por identificador.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Enviar una aplicación de Chrome tooyour de notificación
Para las pruebas, enviaremos notificaciones push de Chrome mediante la aplicación de consola de .NET. 

> [!NOTE]
> Puede enviar notificaciones push con los Centros de notificaciones desde cualquier back-end a través de la <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaz de REST</a>. Consulte el [portal de documentación](https://azure.microsoft.com/documentation/services/notification-hubs/) para obtener más ejemplos multiplataforma.
> 
> 

1. En Visual Studio, desde hello **archivo** menú, seleccione **New** y, a continuación, **proyecto**. En **Visual C#**, haga clic en **Windows** y **Aplicación de consola** y, luego, haga clic en **Aceptar**.  Esto crea un nuevo proyecto de aplicación de consola.
2. De hello **herramientas** menú, haga clic en **Administrador de paquetes de biblioteca** y, a continuación, **Package Manager Console**. Esto muestra hello Package Manager Console.
3. En la ventana de la consola de hello, ejecute Hola siguiente comando:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Abra `Program.cs` y agregue los siguiente hello `using` instrucción:
   
        using Microsoft.Azure.NotificationHubs;
5. Hola `Program` clase, agregue Hola siguiente método:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Asegúrese de que usar cadena de conexión de hello con **completa** acceso, no **escuchar** acceso. Hola **escuchar** cadena de conexión de acceso no conceder permisos de notificaciones de inserción de toosend.
   > 
   > 
6. Agregar llamadas a siguiente hello en hello `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Asegúrese de que se está ejecutando Chrome y ejecutar la aplicación de consola de Hola.
8. Debería ver Hola siguiente elemento emergente en el escritorio de notificación.
   
       ![Google Chrome - Notification][13]
9. También puede ver todas las notificaciones mediante la ventana de notificaciones de cromo de hello en la barra de tareas de hello (en Windows) cuando se está ejecutando Chrome.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> No es necesario toohave Hola Chrome aplicación abrir en el Explorador de Hola o en ejecución (aunque el propio explorador de Chrome Hola debe estar ejecutándose). También obtendrá una vista consolidada de todas las notificaciones en la ventana de notificaciones de Chrome hello.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre Centros de notificaciones en [Introducción a los centros de notificaciones].

tootarget usuarios específicos, consulte toohello [notificación centros de notificar a los usuarios de Azure] tutorial. 

Si desea toosegment los usuarios por grupos de interés, puede seguir hello [centros de notificaciones de Azure noticias de última hora] tutorial.

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
