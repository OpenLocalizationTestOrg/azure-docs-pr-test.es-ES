### <span data-ttu-id="d71cb-101"><a name="server-auth"></a>Autenticación con un proveedor (flujo de servidor)</span><span class="sxs-lookup"><span data-stu-id="d71cb-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="d71cb-102">Aplicaciones de Mobile toohave administre el proceso de autenticación de hello en la aplicación, debe registrar la aplicación con el proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="d71cb-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="d71cb-103">A continuación, en el servicio de aplicación de Azure, debe tooconfigure Hola identificador de la aplicación y el secreto proporcionada por el proveedor.</span><span class="sxs-lookup"><span data-stu-id="d71cb-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="d71cb-104">Para obtener más información, vea el tutorial de hello [agregar autenticación tooyour aplicación](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="d71cb-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="d71cb-105">Una vez que ha registrado el proveedor de identidad, llame a hello `.login()` método con nombre hello del proveedor.</span><span class="sxs-lookup"><span data-stu-id="d71cb-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="d71cb-106">Por ejemplo, toologin con Facebook usar hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d71cb-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="d71cb-107">los valores válidos para el proveedor de Hola Hola son 'aad', 'facebook', 'google', 'cuenta de Microsoft' y 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="d71cb-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="d71cb-108">Autenticación de Google no funciona actualmente a través del flujo de servidor.</span><span class="sxs-lookup"><span data-stu-id="d71cb-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="d71cb-109">tooauthenticate con Google, debe usar un [método de flujo de cliente](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="d71cb-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="d71cb-110">En este caso, el servicio de aplicaciones de Azure administra flujo de autenticación de hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d71cb-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="d71cb-111">Muestra la página de inicio de sesión de Hola de proveedor seleccionado hello y genera un token de autenticación de servicio de aplicaciones después de iniciar sesión correctamente con el proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="d71cb-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="d71cb-112">función de inicio de sesión de Hello, cuando haya finalizado, devuelve un objeto JSON que expone el Id. de usuario de Hola y el servicio de aplicaciones de token de autenticación en los campos de identificador de usuario y authenticationToken hello, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d71cb-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="d71cb-113">El token puede almacenarse en caché y volver a usarse hasta que expire.</span><span class="sxs-lookup"><span data-stu-id="d71cb-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="d71cb-114"><a name="client-auth"></a>Autenticación con un proveedor (flujo de cliente)</span><span class="sxs-lookup"><span data-stu-id="d71cb-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="d71cb-115">La aplicación puede también independientemente en contacto con el proveedor de identidades de hello y, a continuación, proporcionar Hola devuelve token tooyour servicio de aplicaciones para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d71cb-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="d71cb-116">Este flujo de cliente le permite tooprovide una experiencia de inicio de sesión única para los usuarios o los datos de usuario adicionales tooretrieve Hola del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="d71cb-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="d71cb-117">Ejemplo básico de autenticación social</span><span class="sxs-lookup"><span data-stu-id="d71cb-117">Social Authentication basic example</span></span>

<span data-ttu-id="d71cb-118">Este ejemplo usa el SDK de cliente de Facebook para la autenticación:</span><span class="sxs-lookup"><span data-stu-id="d71cb-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="d71cb-119">En este ejemplo se da por supuesto ese token Hola proporcionado por el proveedor respectivos Hola SDK se almacena en la variable de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="d71cb-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="d71cb-120">Ejemplo de Cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="d71cb-120">Microsoft Account example</span></span>

<span data-ttu-id="d71cb-121">Hola siguiendo el ejemplo se utiliza Hola SDK de Live, que admite el inicio de sesión único para aplicaciones de la tienda de Windows mediante Account de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="d71cb-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="d71cb-122">Este ejemplo obtiene un token de Live Connect, que es proporcionado tooyour servicio de aplicaciones mediante una llamada a función de inicio de sesión de hello.</span><span class="sxs-lookup"><span data-stu-id="d71cb-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="d71cb-123"><a name="auth-getinfo"></a>Cómo: obtener información acerca del usuario autenticado de Hola</span><span class="sxs-lookup"><span data-stu-id="d71cb-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="d71cb-124">se puede recuperar la información de autenticación de Hola de hello `/.auth/me` llamar al punto de conexión mediante HTTP con cualquier biblioteca de AJAX.</span><span class="sxs-lookup"><span data-stu-id="d71cb-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="d71cb-125">Asegúrese de establecer hello `X-ZUMO-AUTH` token de autenticación de encabezado tooyour.</span><span class="sxs-lookup"><span data-stu-id="d71cb-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="d71cb-126">token de autenticación Hello se almacena una en `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="d71cb-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="d71cb-127">Por ejemplo, toouse Hola fetch API:</span><span class="sxs-lookup"><span data-stu-id="d71cb-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="d71cb-128">La captura está disponible como [un paquete npm](https://www.npmjs.com/package/whatwg-fetch) o para descarga desde el explorador desde [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="d71cb-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="d71cb-129">También podría usar jQuery u otra información de Hola de toofetch de API de AJAX.</span><span class="sxs-lookup"><span data-stu-id="d71cb-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="d71cb-130">Los datos se recibieron como un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="d71cb-130">Data is received as a JSON object.</span></span>
