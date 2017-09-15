## <a name="create-the-webapi-project"></a><span data-ttu-id="3890b-101">Creación del proyecto WebAPI</span><span class="sxs-lookup"><span data-stu-id="3890b-101">Create the WebAPI Project</span></span>
<span data-ttu-id="3890b-102">El nuevo back-end ASP.NET WebAPI se creará en las secciones siguientes y tendrá tres propósitos principales:</span><span class="sxs-lookup"><span data-stu-id="3890b-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="3890b-103">**Autenticación de clientes**: más adelante se agregará un controlador de mensajes para autenticar las solicitudes de cliente y asociar al usuario con la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3890b-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="3890b-104">**Registros de notificaciones de cliente**: más adelante agregará un controlador para manejar los registros nuevos de un dispositivo cliente para que reciba notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3890b-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="3890b-105">El nombre de usuario autenticado se agregará automáticamente al registro como una [etiqueta](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="3890b-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="3890b-106">**Envío de notificaciones a clientes**: más adelante, también agregará un controlador para proporcionar una forma en que un usuario desencadenará una inserción segura a los dispositivos y clientes asociados con la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="3890b-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="3890b-107">Los pasos siguientes muestran cómo crear el nuevo back-end de ASP.NET WebAPI:</span><span class="sxs-lookup"><span data-stu-id="3890b-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3890b-108">Si usa Visual Studio 2015 o una versión anterior, asegúrese de que ha instalado la versión más reciente del Administrador de paquetes NuGet antes de comenzar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3890b-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="3890b-109">Para comprobarlo, inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3890b-109">To check, start Visual Studio.</span></span> <span data-ttu-id="3890b-110">En el menú **Herramientas**, haga clic en **Extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="3890b-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="3890b-111">Busque el **Administrador de paquetes NuGet** correspondiente a su versión de Visual Studio y asegúrese de que tiene la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="3890b-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="3890b-112">Si no es así, desinstale e instale de nuevo el Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="3890b-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="3890b-113">Asegúrese de que ha instalado el [SDK de Azure](https://azure.microsoft.com/downloads/) para Visual Studio para la implementación de sitios web.</span><span class="sxs-lookup"><span data-stu-id="3890b-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="3890b-114">Inicie Visual Studio o Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="3890b-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="3890b-115">Haga clic en **Explorador de servidores** e inicie sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3890b-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="3890b-116">Visual Studio necesitará que inicies sesión para crear los recursos del sitio web en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3890b-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="3890b-117">En Visual Studio, haga clic en **Archivo** y, a continuación, en **Nuevo** y en **Proyecto**, expanda **Plantillas**, **Visual C#** y, a continuación, haga clic en **Web** y **Aplicación web ASP.NET**, escriba el nombre **AppBackend** y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="3890b-118">En el cuadro de diálogo **Nuevo proyecto ASP.NET**, haga clic en **API web** y, a continuación, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="3890b-119">En el cuadro de diálogo **Configurar aplicación web de Microsoft Azure**, elija una suscripción y un **plan de App Service** que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="3890b-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="3890b-120">También puede elegir **Crear un nuevo plan de App Service** y crear uno desde el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3890b-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="3890b-121">No es necesario una base de datos para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3890b-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="3890b-122">Una vez seleccionado el plan de App Service, haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3890b-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="3890b-123">Autenticación de clientes en el back-end de WebAPI</span><span class="sxs-lookup"><span data-stu-id="3890b-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="3890b-124">En esta sección creará una nueva clase de controlador de mensajes llamada **AuthenticationTestHandler** para el back-end nuevo.</span><span class="sxs-lookup"><span data-stu-id="3890b-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="3890b-125">Esta clase deriva de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) y se agrega como controlador de mensajes, para que así pueda procesar todas las solicitudes entrantes en el back-end.</span><span class="sxs-lookup"><span data-stu-id="3890b-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="3890b-126">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **AppBackend**, haga clic en **Agregar** y, a continuación, haga clic en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="3890b-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="3890b-127">Asigne a la nueva clase el nombre **AuthenticationTestHandler.cs** y haga clic en **Agregar** para generar la clase.</span><span class="sxs-lookup"><span data-stu-id="3890b-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="3890b-128">Para simplificar, esta clase se usa para autenticar a los usuarios con *Autenticación básica* .</span><span class="sxs-lookup"><span data-stu-id="3890b-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="3890b-129">Tenga en cuenta que su aplicación puede utilizar cualquier esquema de autenticación.</span><span class="sxs-lookup"><span data-stu-id="3890b-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="3890b-130">En AuthenticationTestHandler.cs, agregue las siguientes instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="3890b-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="3890b-131">En AuthenticationTestHandler.cs, reemplace la definición de clase `AuthenticationTestHandler` con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3890b-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="3890b-132">Este controlador autorizará la solicitud cuando se cumplan las tres condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="3890b-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="3890b-133">La solicitud incluía un encabezado *Autorización* .</span><span class="sxs-lookup"><span data-stu-id="3890b-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="3890b-134">La solicitud utiliza la autenticación *básica* .</span><span class="sxs-lookup"><span data-stu-id="3890b-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="3890b-135">La cadena de nombre de usuario y la cadena de contraseña son la misma cadena.</span><span class="sxs-lookup"><span data-stu-id="3890b-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="3890b-136">De lo contrario, se rechazará la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3890b-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="3890b-137">Este no es un enfoque de autorización y autenticación real.</span><span class="sxs-lookup"><span data-stu-id="3890b-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="3890b-138">Es solo un ejemplo muy simple para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3890b-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="3890b-139">Si el mensaje de solicitud es autenticado y autorizado por el `AuthenticationTestHandler`, el usuario de autenticación básica se adjuntará a la solicitud actual en el [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="3890b-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="3890b-140">Otro controlador (RegisterController) usará después la información de usuario en HttpContext para agregar una [etiqueta](https://msdn.microsoft.com/library/azure/dn530749.aspx) a la solicitud de registro de notificación.</span><span class="sxs-lookup"><span data-stu-id="3890b-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="3890b-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="3890b-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
                       // Attach the new principal object to the current HttpContext object
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
       <span data-ttu-id="3890b-142">}</span><span class="sxs-lookup"><span data-stu-id="3890b-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="3890b-143">**Nota de seguridad**: la clase `AuthenticationTestHandler` no proporciona una autenticación verdadera.</span><span class="sxs-lookup"><span data-stu-id="3890b-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="3890b-144">Se utiliza únicamente para simular una autenticación básica y no es segura.</span><span class="sxs-lookup"><span data-stu-id="3890b-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="3890b-145">Debe implementar un mecanismo de autenticación seguro en las aplicaciones y servicios de producción.</span><span class="sxs-lookup"><span data-stu-id="3890b-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="3890b-146">Agregue el siguiente código al final del método `Register` en la clase **App_Start/WebApiConfig.cs** para registrar el controlador de mensajes:</span><span class="sxs-lookup"><span data-stu-id="3890b-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="3890b-147">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="3890b-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="3890b-148">Registro para recibir notificaciones mediante el back-end de WebAPI</span><span class="sxs-lookup"><span data-stu-id="3890b-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="3890b-149">En esta sección, agregaremos un nuevo controlador al back-end de WebAPI para gestionar las solicitudes de registro de un usuario y un dispositivo para recibir notificaciones mediante la biblioteca de cliente de Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="3890b-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="3890b-150">El controlador agregará una etiqueta de usuario al usuario que el `AuthenticationTestHandler`autenticó y adjuntó al HttpContext.</span><span class="sxs-lookup"><span data-stu-id="3890b-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="3890b-151">La etiqueta tendrá el formato de cadena, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="3890b-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="3890b-152">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **AppBackend** y, a continuación, seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3890b-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="3890b-153">A la izquierda, haga clic en **En línea** y busque **Microsoft.Azure.NotificationHubs** en el cuadro **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="3890b-154">En la lista de resultados, haga clic en **Microsoft Azure Notification Hubs** y luego en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="3890b-155">Complete la instalación y, a continuación, cierre la ventana del administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="3890b-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="3890b-156">Así se agrega una referencia al SDK de Azure Notification Hubs mediante el <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="3890b-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="3890b-157">Ahora creará un archivo de clase que representa la conexión con el Centro de notificaciones usado para enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3890b-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="3890b-158">En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Modelos**, haga clic en **Agregar** y, a continuación, haga clic en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="3890b-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="3890b-159">Después de asignar el nombre a la nueva clase **Notifications.cs**, haga clic en **Agregar** para generar la clase.</span><span class="sxs-lookup"><span data-stu-id="3890b-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="3890b-160">En Notifications.cs, agregue la siguiente instrucción `using` en la parte superior del archivo:</span><span class="sxs-lookup"><span data-stu-id="3890b-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="3890b-161">Reemplace la definición de clase `Notifications` por lo siguiente y asegúrese de reemplazar los dos marcadores de posición por la cadena de conexión (con acceso total) de su centro de notificaciones, y el nombre del centro (disponible en el [Portal de Azure clásico](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="3890b-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="3890b-162">A continuación, creamos un nuevo controlador denominado **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="3890b-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="3890b-163">En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Controladores**, a continuación en **Agregar** y, por último, en **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="3890b-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="3890b-164">Haga clic en el elemento **Controlador Web API 2 - Vacío** y, a continuación, en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="3890b-165">Nombre a la nueva clase **RegisterController** y luego haga clic de nuevo en **Agregar** para generar el controlador.</span><span class="sxs-lookup"><span data-stu-id="3890b-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="3890b-166">En RegisterController.cs, agregue las siguientes instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="3890b-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="3890b-167">Agregue el siguiente código a la definición de clase `RegisterController` .</span><span class="sxs-lookup"><span data-stu-id="3890b-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="3890b-168">Observe que, en este código, agregamos una etiqueta de usuario para el usuario adjunto a HttpContext.</span><span class="sxs-lookup"><span data-stu-id="3890b-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="3890b-169">El usuario se autenticó y adjuntó a HttpContext a través del filtro de mensaje que agregamos, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="3890b-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="3890b-170">También puede realizar comprobaciones opcionales para comprobar que el usuario puede registrarse para las etiquetas solicitadas.</span><span class="sxs-lookup"><span data-stu-id="3890b-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
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
        // This creates or updates a registration (with provided channelURI) at the specified id
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
   
            // add check if user is allowed to add these tags
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
10. <span data-ttu-id="3890b-171">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="3890b-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="3890b-172">Envío de notificaciones desde el back-end de WebAPI</span><span class="sxs-lookup"><span data-stu-id="3890b-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="3890b-173">En esta sección agregará un nuevo controlador que expone una forma de que los dispositivos cliente envíen una notificación basándose en la etiqueta de nombre de usuario; para ello, se usará la biblioteca de administración del servicio Azure Notification Hubs en el back-end WebAPI de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3890b-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="3890b-174">Cree otro controlador nuevo llamado **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="3890b-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="3890b-175">Créelo del mismo modo que creó el **RegisterController** en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="3890b-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="3890b-176">En NotificationsController.cs, agregue las siguientes instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="3890b-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="3890b-177">Agregue el método siguiente a la clase **NotificationsController** .</span><span class="sxs-lookup"><span data-stu-id="3890b-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="3890b-178">Este código envía un tipo de notificación basado en el parámetro `pns` del Servicio de notificación de plataforma (PNS).</span><span class="sxs-lookup"><span data-stu-id="3890b-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="3890b-179">El valor de `to_tag` se usa para definir la etiqueta *username* en el mensaje.</span><span class="sxs-lookup"><span data-stu-id="3890b-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="3890b-180">Esta etiqueta debe coincidir con una etiqueta de nombre de usuario de un registro de un centro de notificaciones activo.</span><span class="sxs-lookup"><span data-stu-id="3890b-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="3890b-181">El mensaje de notificación se extrae del cuerpo de la solicitud POST y se formatea para el PNS de destino.</span><span class="sxs-lookup"><span data-stu-id="3890b-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="3890b-182">Dependiendo del Servicio de notificación de plataforma (PNS) que usan los dispositivos compatibles para recibir notificaciones, se admiten notificaciones diferentes con distintos formatos.</span><span class="sxs-lookup"><span data-stu-id="3890b-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="3890b-183">Por ejemplo, en dispositivos Windows, puede usar una [notificación del sistema con WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) que no sea compatible directamente con otro PNS.</span><span class="sxs-lookup"><span data-stu-id="3890b-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="3890b-184">Por lo tanto, el back-end deberá dar formato a la notificación en una notificación compatible para el PNS de dispositivos que tiene previsto admitir.</span><span class="sxs-lookup"><span data-stu-id="3890b-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="3890b-185">Posteriormente, use la API de envío adecuada en la [clase NotificationHubClient](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="3890b-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="3890b-186">Presione **F5** para ejecutar la aplicación y comprobar que hasta ahora todo es correcto.</span><span class="sxs-lookup"><span data-stu-id="3890b-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="3890b-187">La aplicación debería iniciar un explorador web y mostrar la página principal de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3890b-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="3890b-188">Publicación del nuevo back-end de WebAPI</span><span class="sxs-lookup"><span data-stu-id="3890b-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="3890b-189">Ahora implementaremos esta aplicación en un sitio web de Azure a fin de que sea accesible para todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3890b-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="3890b-190">Haga clic con el botón derecho en el proyecto **AppBackend** y, a continuación, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="3890b-191">Seleccione **Microsoft Azure App Service** como destino de publicación y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="3890b-192">Se abre el cuadro de diálogo Crear App Service, que le ayuda a crear todos los recursos de Azure necesarios para ejecutar la aplicación web de ASP.NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="3890b-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="3890b-193">En el cuadro de diálogo **Crear App Service**, seleccione la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3890b-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="3890b-194">Haga clic en **Cambiar tipo** y seleccione **Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="3890b-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="3890b-195">Mantenga el **nombre dado a la aplicación web** y seleccione los valores de **Suscripción**, **Grupo de recursos** y **Plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="3890b-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="3890b-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3890b-196">Click **Create**.</span></span>

4. <span data-ttu-id="3890b-197">Anote la propiedad **Dirección URL del sitio** de la sección **Resumen**.</span><span class="sxs-lookup"><span data-stu-id="3890b-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="3890b-198">Más tarde en este tutorial haremos referencia a esta dirección URL como *extremo de backend* .</span><span class="sxs-lookup"><span data-stu-id="3890b-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="3890b-199">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="3890b-199">Click **Publish**.</span></span>

5. <span data-ttu-id="3890b-200">Una vez completado el asistente, publica la aplicación web ASP.NET en Azure y, a continuación, inicia la aplicación en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3890b-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="3890b-201">La aplicación se podrá ver en Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="3890b-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="3890b-202">La dirección URL usa el nombre de la aplicación web que especificó anteriormente, con el formato http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="3890b-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

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
