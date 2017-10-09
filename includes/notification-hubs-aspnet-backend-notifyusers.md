## <a name="create-hello-webapi-project"></a><span data-ttu-id="59c29-101">Crear hello WebAPI proyecto</span><span class="sxs-lookup"><span data-stu-id="59c29-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="59c29-102">ASP.NET WebAPI back-end se creará en secciones de Hola que sigan y tendrá tres objetivos principales:</span><span class="sxs-lookup"><span data-stu-id="59c29-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="59c29-103">**Autenticación de clientes**: un controlador de mensajes se agregarán más adelante las solicitudes de cliente de tooauthenticate y usuario Hola asociado con la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="59c29-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="59c29-104">**Registros de notificación de cliente**: más adelante, agregará un controlador toohandle nuevo los registros para las notificaciones tooreceive un dispositivo cliente.</span><span class="sxs-lookup"><span data-stu-id="59c29-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="59c29-105">Hello nombre de usuario autenticado se agregará automáticamente el registro toohello como un [etiqueta](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="59c29-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="59c29-106">**Enviar notificaciones tooClients**: una versión posterior, también agregará un tooprovide controlador una manera para que un tootrigger un toodevices inserción segura de usuario y los clientes asociados a la etiqueta de Hola.</span><span class="sxs-lookup"><span data-stu-id="59c29-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="59c29-107">Hola pasos muestra cómo toocreate Hola back-end de ASP.NET WebAPI nueva:</span><span class="sxs-lookup"><span data-stu-id="59c29-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="59c29-108">Si está usando Visual Studio 2015 o versiones anteriores, antes de iniciar este tutorial, asegúrese de que ha instalado la versión más reciente de Hola de hello Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="59c29-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="59c29-109">toocheck, inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59c29-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="59c29-110">De hello **herramientas** menú, haga clic en **extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="59c29-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="59c29-111">Busque **Administrador de paquetes de NuGet** para su versión de Visual Studio y asegúrese de que tiene la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="59c29-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="59c29-112">Si no es así, desinstale y reinstale Hola Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="59c29-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="59c29-113">Asegúrese de que ha instalado Visual Studio hello [Azure SDK](https://azure.microsoft.com/downloads/) para la implementación del sitio Web.</span><span class="sxs-lookup"><span data-stu-id="59c29-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="59c29-114">Inicie Visual Studio o Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="59c29-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="59c29-115">Haga clic en **Explorador de servidores** e inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="59c29-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="59c29-116">Visual Studio debe iniciar su sesión en recursos de sitio web de hello toocreate en tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="59c29-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="59c29-117">En Visual Studio, haga clic en **archivo**, a continuación, haga clic en **New**, a continuación, **proyecto**, expanda **plantillas**, **Visual C#**, a continuación, haga clic en **Web** y **aplicación Web ASP.NET**, nombre de tipo hello **AppBackend**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="59c29-118">Hola **nuevo proyecto ASP.NET** cuadro de diálogo, haga clic en **API Web**, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="59c29-119">Hola **Configurar aplicación Web de Microsoft Azure** cuadro de diálogo, elija una suscripción y un **plan de servicio de aplicaciones** ya ha creado.</span><span class="sxs-lookup"><span data-stu-id="59c29-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="59c29-120">También puede elegir **crear un nuevo plan de servicio de aplicación** y crear uno en el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="59c29-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="59c29-121">No es necesario una base de datos para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="59c29-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="59c29-122">Una vez haya seleccionado el plan de servicio de aplicaciones, haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="59c29-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="59c29-123">Autenticar clientes toohello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="59c29-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="59c29-124">En esta sección, creará una nueva clase de controlador de mensaje denominada **AuthenticationTestHandler** para hello back-end.</span><span class="sxs-lookup"><span data-stu-id="59c29-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="59c29-125">Esta clase se deriva de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) y se agrega como un controlador de mensajes, por lo que puede procesar todas las solicitudes que entran en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="59c29-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="59c29-126">En el Explorador de soluciones, haga clic en hello **AppBackend** proyecto de equipo y haga clic en **agregar**, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="59c29-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="59c29-127">Hola nueva clase el nombre **AuthenticationTestHandler.cs**y haga clic en **agregar** clase de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="59c29-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="59c29-128">Esta clase será usuarios tooauthenticate usado con *la autenticación básica* para simplificar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="59c29-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="59c29-129">Tenga en cuenta que su aplicación puede utilizar cualquier esquema de autenticación.</span><span class="sxs-lookup"><span data-stu-id="59c29-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="59c29-130">En AuthenticationTestHandler.cs, agregue el siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="59c29-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="59c29-131">En AuthenticationTestHandler.cs, reemplazando hello `AuthenticationTestHandler` definición de la clase con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="59c29-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="59c29-132">Este controlador autorizará solicitud hello cuando Hola tres condiciones siguientes se cumplen:</span><span class="sxs-lookup"><span data-stu-id="59c29-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="59c29-133">solicitud de Hello incluida un *autorización* encabezado.</span><span class="sxs-lookup"><span data-stu-id="59c29-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="59c29-134">solicitud de Hello utiliza *básica* autenticación.</span><span class="sxs-lookup"><span data-stu-id="59c29-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="59c29-135">cadena de nombre de usuario de Hola y de cadena de contraseña de hello son Hola misma cadena.</span><span class="sxs-lookup"><span data-stu-id="59c29-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="59c29-136">En caso contrario, se rechazará la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="59c29-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="59c29-137">Este no es un enfoque de autorización y autenticación real.</span><span class="sxs-lookup"><span data-stu-id="59c29-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="59c29-138">Es solo un ejemplo muy simple para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="59c29-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="59c29-139">Si el mensaje de solicitud de saludo se autentican y autorizan en hello `AuthenticationTestHandler`, usuario de autenticación básica de hello será toohello adjunta la solicitud actual en hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="59c29-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="59c29-140">Se usará la información de usuario en hello HttpContext por otro controlador (RegisterController) tooadd más adelante un [etiqueta](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello solicitud de registro de notificación.</span><span class="sxs-lookup"><span data-stu-id="59c29-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="59c29-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="59c29-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="59c29-142">}</span><span class="sxs-lookup"><span data-stu-id="59c29-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="59c29-143">**Nota de seguridad**: Hola `AuthenticationTestHandler` clase no proporciona autenticación true.</span><span class="sxs-lookup"><span data-stu-id="59c29-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="59c29-144">Es toomimic solo usa la autenticación básica y no es segura.</span><span class="sxs-lookup"><span data-stu-id="59c29-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="59c29-145">Debe implementar un mecanismo de autenticación seguro en las aplicaciones y servicios de producción.</span><span class="sxs-lookup"><span data-stu-id="59c29-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="59c29-146">Agregar Hola siguiente código al final de Hola de hello `Register` método Hola **App_Start/WebApiConfig.cs** controlador de mensajes de Hola tooregister de clase:</span><span class="sxs-lookup"><span data-stu-id="59c29-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="59c29-147">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="59c29-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="59c29-148">Registrarse para recibir notificaciones mediante hello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="59c29-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="59c29-149">En esta sección, agregaremos que un nuevo toohandle back-end de controlador toohello WebAPI solicita tooregister un usuario y dispositivo para las notificaciones que utiliza la biblioteca de cliente de hello centrales de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="59c29-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="59c29-150">controlador de Hello agregará una etiqueta de usuario para el usuario de Hola que se ha autenticado y adjunta toohello HttpContext por hello `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="59c29-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="59c29-151">etiqueta de Hello tendrá el formato de cadena de hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="59c29-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="59c29-152">En el Explorador de soluciones, haga clic en hello **AppBackend** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="59c29-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="59c29-153">En el lado izquierdo de hello, haga clic en **en línea**y busque **Microsoft.Azure.NotificationHubs** en hello **búsqueda** cuadro.</span><span class="sxs-lookup"><span data-stu-id="59c29-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="59c29-154">En la lista de resultados de hello, haga clic en **centros de notificaciones de Microsoft Azure**y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="59c29-155">Completar la instalación de hello, a continuación, cierre la ventana del Administrador de paquetes de NuGet de Hola.</span><span class="sxs-lookup"><span data-stu-id="59c29-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="59c29-156">Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="59c29-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="59c29-157">Ahora, se creará un nuevo archivo de clase que representa la conexión de hello con notificación concentrador usa toosend notificaciones.</span><span class="sxs-lookup"><span data-stu-id="59c29-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="59c29-158">Hola el Explorador de soluciones, haga clic en hello **modelos** carpeta, haga clic en **agregar**, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="59c29-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="59c29-159">Hola nueva clase el nombre **Notifications.cs**, a continuación, haga clic en **agregar** clase de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="59c29-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="59c29-160">En Notifications.cs, agregue el siguiente hello `using` declaración en la parte superior de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="59c29-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="59c29-161">Reemplace hello `Notifications` definición por siguiente hello de la clase y hacer los marcadores de posición Hola dos tooreplace seguro con la cadena de conexión hello (con acceso completo) para el centro de notificaciones y Hola nombre del concentrador (disponible en [Portal clásico de Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="59c29-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="59c29-162">A continuación, creamos un nuevo controlador denominado **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="59c29-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="59c29-163">En el Explorador de soluciones, haga clic en hello **controladores** carpeta, a continuación, haga clic en **agregar**, a continuación, haga clic en **controlador**.</span><span class="sxs-lookup"><span data-stu-id="59c29-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="59c29-164">Haga clic en hello **Web API 2 Controller: vacío** de elemento y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="59c29-165">Hola nueva clase el nombre **RegisterController**y, a continuación, haga clic en **agregar** nuevo controlador de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="59c29-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="59c29-166">En RegisterController.cs, agregue el siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="59c29-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="59c29-167">Agregar Hola siguiente código dentro de hello `RegisterController` definición de clase.</span><span class="sxs-lookup"><span data-stu-id="59c29-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="59c29-168">Tenga en cuenta que en este código, se agrega una etiqueta de usuario para el usuario de hello es adjunta toohello HttpContext.</span><span class="sxs-lookup"><span data-stu-id="59c29-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="59c29-169">usuario de Hola se autenticó y adjunta toohello HttpContext agregamos, el filtro de mensajes de Hola `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="59c29-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="59c29-170">También puede agregar tooverify comprobaciones opcionales que Hola usuario tiene derechos tooregister para hello solicitado etiquetas.</span><span class="sxs-lookup"><span data-stu-id="59c29-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="59c29-171">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="59c29-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="59c29-172">Enviar notificaciones de hello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="59c29-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="59c29-173">En esta sección se agrega un nuevo controlador que expone una manera para que los dispositivos de cliente toosend una notificación basada en la etiqueta de nombre de usuario de hello en biblioteca de administración de servicio de Azure notificación concentradores Hola ASP.NET WebAPI back-end.</span><span class="sxs-lookup"><span data-stu-id="59c29-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="59c29-174">Cree otro controlador nuevo llamado **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="59c29-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="59c29-175">Crear Hola igual que creó hello **RegisterController** en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="59c29-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="59c29-176">En NotificationsController.cs, agregue el siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="59c29-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="59c29-177">Agregar Hola siguiendo el método toohello **NotificationsController** clase.</span><span class="sxs-lookup"><span data-stu-id="59c29-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="59c29-178">Este código enviar un tipo de notificación basado en hello servicio de notificación de plataforma (PNS) `pns` parámetro.</span><span class="sxs-lookup"><span data-stu-id="59c29-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="59c29-179">Hola valo `to_tag` es hello tooset usado *nombre de usuario* etiqueta en el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="59c29-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="59c29-180">Esta etiqueta debe coincidir con una etiqueta de nombre de usuario de un registro de un centro de notificaciones activo.</span><span class="sxs-lookup"><span data-stu-id="59c29-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="59c29-181">mensaje de notificación de Hello es extraído del cuerpo de saludo de solicitud POST de Hola y con formato de destino de hello PNS.</span><span class="sxs-lookup"><span data-stu-id="59c29-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="59c29-182">Función Hola servicio de notificación de plataforma (PNS) que los dispositivos compatibles usar notificaciones de tooreceive diferentes notificaciones se admiten mediante formatos distintos.</span><span class="sxs-lookup"><span data-stu-id="59c29-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="59c29-183">Por ejemplo, en dispositivos Windows, puede usar una [notificación del sistema con WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) que no sea compatible directamente con otro PNS.</span><span class="sxs-lookup"><span data-stu-id="59c29-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="59c29-184">Por lo que el back-end necesitaría tooformat notificación de hello en una notificación compatible para hello PNS de dispositivos tiene previsto toosupport.</span><span class="sxs-lookup"><span data-stu-id="59c29-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="59c29-185">A continuación, usar API de envío correspondiente de hello en hello [NotificationHubClient (clase)](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="59c29-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="59c29-186">Presione **F5** toorun Hola aplicación y tooensure Hola precisión de su trabajo hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="59c29-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="59c29-187">aplicación Hello debe iniciar un explorador web y mostrar la página principal de ASP.NET Hola.</span><span class="sxs-lookup"><span data-stu-id="59c29-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="59c29-188">Publicar Hola WebAPI Backend nuevo</span><span class="sxs-lookup"><span data-stu-id="59c29-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="59c29-189">Ahora se implementará esta aplicación tooan sitio Web de Azure en orden toomake, accesible desde todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="59c29-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="59c29-190">Haga doble clic en hello **AppBackend** de proyecto y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="59c29-191">Seleccione **Microsoft Azure App Service** como destino de publicación y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="59c29-192">Se abrirá Hola crear servicio en la aplicación cuadro de diálogo, que le ayudará a crear la aplicación de todos los hello recursos de Azure necesarios toorun Hola ASP.NET web en Azure.</span><span class="sxs-lookup"><span data-stu-id="59c29-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="59c29-193">Hola **crear servicio en la aplicación** cuadro de diálogo, seleccione su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="59c29-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="59c29-194">Haga clic en **Cambiar tipo** y seleccione **Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="59c29-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="59c29-195">Mantener hello **nombre de la aplicación Web** Hola determinado y seleccione **suscripción**, **grupo de recursos**, y **Plan de servicio de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="59c29-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="59c29-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="59c29-196">Click **Create**.</span></span>

4. <span data-ttu-id="59c29-197">Tome nota de hello **dirección URL del sitio** propiedad Hola **resumen** sección.</span><span class="sxs-lookup"><span data-stu-id="59c29-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="59c29-198">Nos referiremos toothis URL según su *punto de conexión de back-end* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="59c29-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="59c29-199">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="59c29-199">Click **Publish**.</span></span>

5. <span data-ttu-id="59c29-200">Una vez que se complete el Asistente de hello, publica Hola ASP.NET web app tooAzure y, a continuación, inicia Hola aplicación en el Explorador de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="59c29-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="59c29-201">La aplicación se podrá ver en Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="59c29-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="59c29-202">dirección URL de Hello usa Hola nombre de la aplicación que especificó anteriormente, con hello formato http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="59c29-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
