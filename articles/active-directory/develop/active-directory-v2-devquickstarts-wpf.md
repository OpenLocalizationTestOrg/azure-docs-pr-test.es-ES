---
title: "v2.0 de Active Directory aaaAzure aplicación nativa de .NET | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación nativa de .NET firma los usuarios con ambos Account personal de Microsoft y cuentas profesionales o educativas."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="64870-103">Agregar aplicación de escritorio de Windows de inicio de sesión tooa</span><span class="sxs-lookup"><span data-stu-id="64870-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="64870-104">Con el punto de conexión de Hola Hola v2.0, puede agregar rápidamente aplicaciones de escritorio de tooyour de autenticación con la compatibilidad para ambas cuentas de Microsoft personales y cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="64870-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="64870-105">También habilita la toosecurely aplicación comunicarse con un back-end web api, así como [Hola Microsoft Graph](https://graph.microsoft.io) y algunos de hello [API unificada de Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="64870-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="64870-106">No todas las características y escenarios de Azure Active Directory (AD) son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="64870-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="64870-107">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="64870-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="64870-108">Para [aplicaciones nativas de .NET que se ejecutan en un dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD proporciona Hola biblioteca de autenticación de identidad de Microsoft o MSAL.</span><span class="sxs-lookup"><span data-stu-id="64870-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="64870-109">Propósitos del MSAL en la vida es toomake más sencilla para su aplicación tooget tokens para llamar a servicios web.</span><span class="sxs-lookup"><span data-stu-id="64870-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="64870-110">toodemonstrate lo fácil es, a continuación, crearemos una aplicación de la lista de tareas de .NET WPF que:</span><span class="sxs-lookup"><span data-stu-id="64870-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="64870-111">Signos de Hola usuario en & obtiene acceso a los tokens utilizando hello [protocolo de autenticación de OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="64870-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="64870-112">Llama a un servicio web de lista de tareas pendientes back-end, que también está protegido con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="64870-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="64870-113">Usuario de hello signos out.</span><span class="sxs-lookup"><span data-stu-id="64870-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="64870-114">Descarga de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="64870-114">Download sample code</span></span>
<span data-ttu-id="64870-115">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="64870-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="64870-116">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="64870-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="64870-117">final de Hola de este tutorial también se incluye aplicación Hello completado.</span><span class="sxs-lookup"><span data-stu-id="64870-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="64870-118">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="64870-118">Register an app</span></span>
<span data-ttu-id="64870-119">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="64870-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="64870-120">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="64870-120">Make sure to:</span></span>

* <span data-ttu-id="64870-121">Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="64870-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="64870-122">Agregar hello **Mobile** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64870-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="64870-123">Instalación y configuración de MSAL</span><span class="sxs-lookup"><span data-stu-id="64870-123">Install & Configure MSAL</span></span>
<span data-ttu-id="64870-124">Ahora que ya tiene una aplicación registrada en Microsoft, puede instalar MSAL y escribir código relacionado con identidades.</span><span class="sxs-lookup"><span data-stu-id="64870-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="64870-125">Para el punto de conexión MSAL toobe toocommunicate capaz de hello v2.0, deberá tooprovide con cierta información sobre el registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="64870-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="64870-126">Comience por agregar MSAL toohello TodoListClient proyecto mediante la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="64870-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="64870-127">En hello TodoListClient proyecto, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="64870-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="64870-128">Reemplace los valores de hello de elementos de Hola Hola `<appSettings>` Hola de sección tooreflect valores proporcionados en el portal de registro de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="64870-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="64870-129">El código hará referencia a estos valores cada vez que use MSAL.</span><span class="sxs-lookup"><span data-stu-id="64870-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="64870-130">Hola `ida:ClientId` es hello **Id. de aplicación** de la aplicación copian desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64870-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="64870-131">En el proyecto de servicio TodoList hello, abra `web.config` en raíz de Hola de proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="64870-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="64870-132">Reemplace hello `ida:Audience` valor con hello mismo **Id. de aplicación** desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64870-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="64870-133">Usar tokens de tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="64870-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="64870-134">Hello principio básico detrás de MSAL es cada vez que la aplicación necesita un token de acceso, basta con llamar a `app.AcquireToken(...)`, y MSAL Hola rest.</span><span class="sxs-lookup"><span data-stu-id="64870-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="64870-135">Hola `TodoListClient` proyecto abierto `MainWindow.xaml.cs` y busque hello `OnInitialized(...)` método.</span><span class="sxs-lookup"><span data-stu-id="64870-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="64870-136">primer paso de Hello es la aplicación de tooinitialize `PublicClientApplication` -clase principal del MSAL que representa las aplicaciones nativas.</span><span class="sxs-lookup"><span data-stu-id="64870-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="64870-137">Esto es donde pasas MSAL Hola coordenadas debe toocommunicate con Azure AD y le indique cómo toocache símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="64870-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="64870-138">Cuando se inicia aplicación hello, se desea toocheck y vea si el usuario de hello ya ha iniciado en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="64870-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="64870-139">Sin embargo, todavía no queremos tooinvoke una interfaz de usuario de inicio de sesión, nos aseguraremos de hacer el usuario de Hola por lo que haga clic en "Iniciar sesión" toodo.</span><span class="sxs-lookup"><span data-stu-id="64870-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="64870-140">También en hello `OnInitialized(...)` método:</span><span class="sxs-lookup"><span data-stu-id="64870-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="64870-141">Si usuario hello no ha iniciado sesión y haga clic en el botón "Iniciar sesión" Hola, se desea tooinvoke una interfaz de usuario de inicio de sesión y usuario Hola escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="64870-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="64870-142">Implementar el controlador del botón Hola inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="64870-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="64870-143">Si Hola usuario correctamente inicia sesión, MSAL recibirá y almacenar en caché un token para usted y puede continuar hello toocall `GetTodoList()` método con confianza.</span><span class="sxs-lookup"><span data-stu-id="64870-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="64870-144">Todo lo que ha dejado tooget las tareas de un usuario es tooimplement hello `GetTodoList()` método.</span><span class="sxs-lookup"><span data-stu-id="64870-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="64870-145">Ejecute</span><span class="sxs-lookup"><span data-stu-id="64870-145">Run</span></span>
<span data-ttu-id="64870-146">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="64870-146">Congratulations!</span></span> <span data-ttu-id="64870-147">Ahora tiene una aplicación .NET WPF que tiene Hola capacidad tooauthenticate usuarios en funcionamiento & seguro llamar a las API Web mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="64870-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="64870-148">Ejecute sus dos proyectos e inicie sesión con una cuenta de Microsoft personal o una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="64870-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="64870-149">Agregue la lista de tareas del usuario de las tareas toothat.</span><span class="sxs-lookup"><span data-stu-id="64870-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="64870-150">Cierre la sesión y vuelva a iniciarla como tooview de otro usuario su lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="64870-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="64870-151">Cierre la aplicación hello y volver a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="64870-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="64870-152">Tenga en cuenta la sesión del usuario de hello permanece intacta, esto es así porque la aplicación hello almacena en memoria caché de símbolos (tokens) en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="64870-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="64870-153">MSAL resulta fácil tooincorporate características de identidad comunes en la aplicación, con cuentas personales y profesionales.</span><span class="sxs-lookup"><span data-stu-id="64870-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="64870-154">Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentaciones usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="64870-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="64870-155">Todo lo que realmente necesita tooknow es una sola llamada API, `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="64870-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="64870-156">Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), o se puede clonar desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="64870-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="64870-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64870-157">Next steps</span></span>
<span data-ttu-id="64870-158">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="64870-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="64870-159">Puede que desee tootry:</span><span class="sxs-lookup"><span data-stu-id="64870-159">You may want tootry:</span></span>

* [<span data-ttu-id="64870-160">Proteger hello TodoListService Web API con el punto de conexión de hello v2.0</span><span class="sxs-lookup"><span data-stu-id="64870-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="64870-161">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="64870-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="64870-162">Guía del desarrollador de Hello v2.0 >></span><span class="sxs-lookup"><span data-stu-id="64870-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="64870-163">Etiqueta "msal" de StackOverflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="64870-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="64870-164">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="64870-164">Get security updates for our products</span></span>
<span data-ttu-id="64870-165">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="64870-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

