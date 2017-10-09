## <a name="create-hello-webapi-project"></a>Crear hello WebAPI proyecto
ASP.NET WebAPI back-end se creará en secciones de Hola que sigan y tendrá tres objetivos principales:

1. **Autenticación de clientes**: un controlador de mensajes se agregarán más adelante las solicitudes de cliente de tooauthenticate y usuario Hola asociado con la solicitud de saludo.
2. **Registros de notificación de cliente**: más adelante, agregará un controlador toohandle nuevo los registros para las notificaciones tooreceive un dispositivo cliente. Hello nombre de usuario autenticado se agregará automáticamente el registro toohello como un [etiqueta](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Enviar notificaciones tooClients**: una versión posterior, también agregará un tooprovide controlador una manera para que un tootrigger un toodevices inserción segura de usuario y los clientes asociados a la etiqueta de Hola. 

Hola pasos muestra cómo toocreate Hola back-end de ASP.NET WebAPI nueva: 

> [!IMPORTANT]
> Si está usando Visual Studio 2015 o versiones anteriores, antes de iniciar este tutorial, asegúrese de que ha instalado la versión más reciente de Hola de hello Administrador de paquetes de NuGet. toocheck, inicie Visual Studio. De hello **herramientas** menú, haga clic en **extensiones y actualizaciones**. Busque **Administrador de paquetes de NuGet** para su versión de Visual Studio y asegúrese de que tiene la versión más reciente de Hola. Si no es así, desinstale y reinstale Hola Administrador de paquetes de NuGet.
> 
> ![][B4]
> 
> [!NOTE]
> Asegúrese de que ha instalado Visual Studio hello [Azure SDK](https://azure.microsoft.com/downloads/) para la implementación del sitio Web.
> 
> 

1. Inicie Visual Studio o Visual Studio Express. Haga clic en **Explorador de servidores** e inicie sesión en tooyour cuenta de Azure. Visual Studio debe iniciar su sesión en recursos de sitio web de hello toocreate en tu cuenta.
2. En Visual Studio, haga clic en **archivo**, a continuación, haga clic en **New**, a continuación, **proyecto**, expanda **plantillas**, **Visual C#**, a continuación, haga clic en **Web** y **aplicación Web ASP.NET**, nombre de tipo hello **AppBackend**y, a continuación, haga clic en **Aceptar**. 
   
    ![][B1]
3. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, haga clic en **API Web**, a continuación, haga clic en **Aceptar**.
   
    ![][B2]
4. Hola **Configurar aplicación Web de Microsoft Azure** cuadro de diálogo, elija una suscripción y un **plan de servicio de aplicaciones** ya ha creado. También puede elegir **crear un nuevo plan de servicio de aplicación** y crear uno en el cuadro de diálogo de Hola. No es necesario una base de datos para este tutorial. Una vez haya seleccionado el plan de servicio de aplicaciones, haga clic en **Aceptar** proyecto de hello toocreate.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>Autenticar clientes toohello WebAPI Backend
En esta sección, creará una nueva clase de controlador de mensaje denominada **AuthenticationTestHandler** para hello back-end. Esta clase se deriva de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) y se agrega como un controlador de mensajes, por lo que puede procesar todas las solicitudes que entran en hello back-end. 

1. En el Explorador de soluciones, haga clic en hello **AppBackend** proyecto de equipo y haga clic en **agregar**, a continuación, haga clic en **clase**. Hola nueva clase el nombre **AuthenticationTestHandler.cs**y haga clic en **agregar** clase de hello toogenerate. Esta clase será usuarios tooauthenticate usado con *la autenticación básica* para simplificar el trabajo. Tenga en cuenta que su aplicación puede utilizar cualquier esquema de autenticación.
2. En AuthenticationTestHandler.cs, agregue el siguiente hello `using` instrucciones:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. En AuthenticationTestHandler.cs, reemplazando hello `AuthenticationTestHandler` definición de la clase con el siguiente código de hello. 
   
    Este controlador autorizará solicitud hello cuando Hola tres condiciones siguientes se cumplen:
   
   * solicitud de Hello incluida un *autorización* encabezado. 
   * solicitud de Hello utiliza *básica* autenticación. 
   * cadena de nombre de usuario de Hola y de cadena de contraseña de hello son Hola misma cadena.
     
     En caso contrario, se rechazará la solicitud de saludo. Este no es un enfoque de autorización y autenticación real. Es solo un ejemplo muy simple para este tutorial.
     
     Si el mensaje de solicitud de saludo se autentican y autorizan en hello `AuthenticationTestHandler`, usuario de autenticación básica de hello será toohello adjunta la solicitud actual en hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Se usará la información de usuario en hello HttpContext por otro controlador (RegisterController) tooadd más adelante un [etiqueta](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello solicitud de registro de notificación.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Nota de seguridad**: Hola `AuthenticationTestHandler` clase no proporciona autenticación true. Es toomimic solo usa la autenticación básica y no es segura. Debe implementar un mecanismo de autenticación seguro en las aplicaciones y servicios de producción.                
     > 
     > 
4. Agregar Hola siguiente código al final de Hola de hello `Register` método Hola **App_Start/WebApiConfig.cs** controlador de mensajes de Hola tooregister de clase:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Guarde los cambios.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Registrarse para recibir notificaciones mediante hello WebAPI Backend
En esta sección, agregaremos que un nuevo toohandle back-end de controlador toohello WebAPI solicita tooregister un usuario y dispositivo para las notificaciones que utiliza la biblioteca de cliente de hello centrales de notificaciones. controlador de Hello agregará una etiqueta de usuario para el usuario de Hola que se ha autenticado y adjunta toohello HttpContext por hello `AuthenticationTestHandler`. etiqueta de Hello tendrá el formato de cadena de hello, `"username:<actual username>"`.

1. En el Explorador de soluciones, haga clic en hello **AppBackend** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.
2. En el lado izquierdo de hello, haga clic en **en línea**y busque **Microsoft.Azure.NotificationHubs** en hello **búsqueda** cuadro.
3. En la lista de resultados de hello, haga clic en **centros de notificaciones de Microsoft Azure**y, a continuación, haga clic en **instalar**. Completar la instalación de hello, a continuación, cierre la ventana del Administrador de paquetes de NuGet de Hola.
   
    Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.
4. Ahora, se creará un nuevo archivo de clase que representa la conexión de hello con notificación concentrador usa toosend notificaciones. Hola el Explorador de soluciones, haga clic en hello **modelos** carpeta, haga clic en **agregar**, a continuación, haga clic en **clase**. Hola nueva clase el nombre **Notifications.cs**, a continuación, haga clic en **agregar** clase de hello toogenerate. 
   
    ![][B6]
5. En Notifications.cs, agregue el siguiente hello `using` declaración en la parte superior de hello del archivo hello:
   
        using Microsoft.Azure.NotificationHubs;
6. Reemplace hello `Notifications` definición por siguiente hello de la clase y hacer los marcadores de posición Hola dos tooreplace seguro con la cadena de conexión hello (con acceso completo) para el centro de notificaciones y Hola nombre del concentrador (disponible en [Portal clásico de Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. A continuación, creamos un nuevo controlador denominado **RegisterController**. En el Explorador de soluciones, haga clic en hello **controladores** carpeta, a continuación, haga clic en **agregar**, a continuación, haga clic en **controlador**. Haga clic en hello **Web API 2 Controller: vacío** de elemento y, a continuación, haga clic en **agregar**. Hola nueva clase el nombre **RegisterController**y, a continuación, haga clic en **agregar** nuevo controlador de hello toogenerate.
   
    ![][B7]
   
    ![][B8]
8. En RegisterController.cs, agregue el siguiente hello `using` instrucciones:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Agregar Hola siguiente código dentro de hello `RegisterController` definición de clase. Tenga en cuenta que en este código, se agrega una etiqueta de usuario para el usuario de hello es adjunta toohello HttpContext. usuario de Hola se autenticó y adjunta toohello HttpContext agregamos, el filtro de mensajes de Hola `AuthenticationTestHandler`. También puede agregar tooverify comprobaciones opcionales que Hola usuario tiene derechos tooregister para hello solicitado etiquetas.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Guarde los cambios.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Enviar notificaciones de hello WebAPI Backend
En esta sección se agrega un nuevo controlador que expone una manera para que los dispositivos de cliente toosend una notificación basada en la etiqueta de nombre de usuario de hello en biblioteca de administración de servicio de Azure notificación concentradores Hola ASP.NET WebAPI back-end.

1. Cree otro controlador nuevo llamado **NotificationsController**. Crear Hola igual que creó hello **RegisterController** en la sección anterior de Hola.
2. En NotificationsController.cs, agregue el siguiente hello `using` instrucciones:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Agregar Hola siguiendo el método toohello **NotificationsController** clase.
   
    Este código enviar un tipo de notificación basado en hello servicio de notificación de plataforma (PNS) `pns` parámetro. Hola valo `to_tag` es hello tooset usado *nombre de usuario* etiqueta en el mensaje de bienvenida. Esta etiqueta debe coincidir con una etiqueta de nombre de usuario de un registro de un centro de notificaciones activo. mensaje de notificación de Hello es extraído del cuerpo de saludo de solicitud POST de Hola y con formato de destino de hello PNS. 
   
    Función Hola servicio de notificación de plataforma (PNS) que los dispositivos compatibles usar notificaciones de tooreceive diferentes notificaciones se admiten mediante formatos distintos. Por ejemplo, en dispositivos Windows, puede usar una [notificación del sistema con WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) que no sea compatible directamente con otro PNS. Por lo que el back-end necesitaría tooformat notificación de hello en una notificación compatible para hello PNS de dispositivos tiene previsto toosupport. A continuación, usar API de envío correspondiente de hello en hello [NotificationHubClient (clase)](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Presione **F5** toorun Hola aplicación y tooensure Hola precisión de su trabajo hasta ahora. aplicación Hello debe iniciar un explorador web y mostrar la página principal de ASP.NET Hola. 

## <a name="publish-hello-new-webapi-backend"></a>Publicar Hola WebAPI Backend nuevo
1. Ahora se implementará esta aplicación tooan sitio Web de Azure en orden toomake, accesible desde todos los dispositivos. Haga doble clic en hello **AppBackend** de proyecto y seleccione **publicar**.
2. Seleccione **Microsoft Azure App Service** como destino de publicación y haga clic en **Publicar**. Se abrirá Hola crear servicio en la aplicación cuadro de diálogo, que le ayudará a crear la aplicación de todos los hello recursos de Azure necesarios toorun Hola ASP.NET web en Azure.

    ![][B15]
3. Hola **crear servicio en la aplicación** cuadro de diálogo, seleccione su cuenta de Azure. Haga clic en **Cambiar tipo** y seleccione **Aplicación web**. Mantener hello **nombre de la aplicación Web** Hola determinado y seleccione **suscripción**, **grupo de recursos**, y **Plan de servicio de aplicaciones**.  Haga clic en **Crear**.

4. Tome nota de hello **dirección URL del sitio** propiedad Hola **resumen** sección. Nos referiremos toothis URL según su *punto de conexión de back-end* más adelante en este tutorial. Haga clic en **Publicar**.

5. Una vez que se complete el Asistente de hello, publica Hola ASP.NET web app tooAzure y, a continuación, inicia Hola aplicación en el Explorador de Hola de forma predeterminada.  La aplicación se podrá ver en Azure App Services.

dirección URL de Hello usa Hola nombre de la aplicación que especificó anteriormente, con hello formato http://<app_name>.azurewebsites.net.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
