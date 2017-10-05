---
title: "Aplicación nativa .NET v2.0 de Azure Active Directory | Microsoft Azure"
description: "Cómo crear una aplicación nativa .NET con la que los usuarios pueden iniciar sesión utilizando tanto la cuenta personal de Microsoft como sus cuentas profesionales o educativas."
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
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="a2521-103">Agregar inicio de sesión a una aplicación de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="a2521-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="a2521-104">Con el punto de conexión v2.0 puede agregar rápidamente la autenticación a sus aplicaciones de escritorio compatibles tanto con las cuentas personales de Microsoft como con las cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="a2521-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="a2521-105">También permite que la aplicación se comunique de forma segura con una API web back-end, así como con [Microsoft Graph](https://graph.microsoft.io) y algunas de las [API unificadas de Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="a2521-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="a2521-106">No todas las características y escenarios de Azure Active Directory (AD) son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="a2521-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a2521-107">Para determinar si debe usar el punto de conexión v2.0, lea acerca de las [limitaciones de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a2521-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="a2521-108">Para las [aplicaciones nativas .NET que se ejecutan en un dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD proporciona la biblioteca de autenticación de identidades de Microsoft o MSAL.</span><span class="sxs-lookup"><span data-stu-id="a2521-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="a2521-109">El único propósito de MSAL es facilitar a su aplicación la obtención de tokens de acceso para llamar a servicios web.</span><span class="sxs-lookup"><span data-stu-id="a2521-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="a2521-110">Para demostrar lo fácil que es, crearemos aquí una aplicación de lista de tareas pendientes de .NET WPF que permita realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="a2521-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="a2521-111">Iniciar la sesión del usuario y obtener token de acceso mediante el [protocolo de autenticación de OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a2521-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="a2521-112">Llama a un servicio web de lista de tareas pendientes back-end, que también está protegido con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a2521-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="a2521-113">Cierra la sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="a2521-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="a2521-114">Descarga de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a2521-114">Download sample code</span></span>
<span data-ttu-id="a2521-115">El código de este tutorial se conserva [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a2521-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="a2521-116">Para continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="a2521-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="a2521-117">La aplicación completa se ofrece también al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a2521-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="a2521-118">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="a2521-118">Register an app</span></span>
<span data-ttu-id="a2521-119">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a2521-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a2521-120">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="a2521-120">Make sure to:</span></span>

* <span data-ttu-id="a2521-121">Anotar el **Id. de aplicación** asignado a su aplicación; lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="a2521-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="a2521-122">Agregar la plataforma **Móvil** a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a2521-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="a2521-123">Instalación y configuración de MSAL</span><span class="sxs-lookup"><span data-stu-id="a2521-123">Install & Configure MSAL</span></span>
<span data-ttu-id="a2521-124">Ahora que ya tiene una aplicación registrada en Microsoft, puede instalar MSAL y escribir código relacionado con identidades.</span><span class="sxs-lookup"><span data-stu-id="a2521-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="a2521-125">Para que MSAL pueda comunicarse con el punto de conexión v2.0, tiene que proporcionarle información sobre el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a2521-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="a2521-126">Comience agregando MSAL al proyecto TodoListClient con la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a2521-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="a2521-127">En el proyecto TodoListClient, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="a2521-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="a2521-128">Reemplace los valores de los elementos de la sección `<appSettings>` para que reflejen los valores especificados en el portal de registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a2521-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="a2521-129">El código hará referencia a estos valores cada vez que use MSAL.</span><span class="sxs-lookup"><span data-stu-id="a2521-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="a2521-130">`ida:ClientId` es el **Id. de aplicación** de su aplicación que copió del portal.</span><span class="sxs-lookup"><span data-stu-id="a2521-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="a2521-131">En el proyecto de servicio de TodoList, abra `web.config` en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a2521-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="a2521-132">Reemplace el valor `ida:Audience` con el mismo **Id. de aplicación** desde el portal.</span><span class="sxs-lookup"><span data-stu-id="a2521-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="a2521-133">Uso de MSAL para obtener tokens</span><span class="sxs-lookup"><span data-stu-id="a2521-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="a2521-134">El principio básico inherente a MSAL es que cada vez que la aplicación necesite un token de acceso, basta con llamar a `app.AcquireToken(...)`y MSAL se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="a2521-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="a2521-135">En el proyecto `TodoListClient`, abra `MainWindow.xaml.cs` y busque el método `OnInitialized(...)`.</span><span class="sxs-lookup"><span data-stu-id="a2521-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="a2521-136">El primer paso consiste en inicializar la clase principal de MSAL de `PublicClientApplication` de la aplicación que representa las aplicaciones nativas.</span><span class="sxs-lookup"><span data-stu-id="a2521-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="a2521-137">Este es el lugar en el que pasa a MSAL las coordenadas que necesita para comunicarse con Azure AD e indicarle cómo almacenar en caché los tokens.</span><span class="sxs-lookup"><span data-stu-id="a2521-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="a2521-138">Cuando se inicia la aplicación, queremos comprobar y asegurarnos de si el usuario ya está registrado en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a2521-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="a2521-139">Sin embargo, no deseamos invocar una IU de inicio de sesión todavía, sino que haremos que el usuario haga clic en "Iniciar sesión" para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="a2521-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="a2521-140">En el método `OnInitialized(...)` también ocurre lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a2521-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
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

* <span data-ttu-id="a2521-141">Si el usuario no ha iniciado sesión y hace clic en el botón "Iniciar sesión", deseamos invocar una IU de inicio de sesión y que el usuario escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="a2521-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="a2521-142">Implementar el controlador del botón Inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="a2521-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

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
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
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

* <span data-ttu-id="a2521-143">Si el usuario inicia sesión correctamente, MSAL recibirá y almacenará en caché un token por usted y podrá proceder con la llamada al método `GetTodoList()` con confianza.</span><span class="sxs-lookup"><span data-stu-id="a2521-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="a2521-144">Lo único que queda para obtener las tareas del usuario es implementar el método `GetTodoList()` .</span><span class="sxs-lookup"><span data-stu-id="a2521-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

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

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

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

## <a name="run"></a><span data-ttu-id="a2521-145">Ejecute</span><span class="sxs-lookup"><span data-stu-id="a2521-145">Run</span></span>
<span data-ttu-id="a2521-146">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="a2521-146">Congratulations!</span></span> <span data-ttu-id="a2521-147">Ya tiene una aplicación .NET WPF en funcionamiento con la capacidad de autenticar a usuarios y API web de llamadas de forma segura mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a2521-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="a2521-148">Ejecute sus dos proyectos e inicie sesión con una cuenta de Microsoft personal o una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="a2521-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="a2521-149">Agregue tareas a la lista de tareas pendientes de ese usuario.  </span><span class="sxs-lookup"><span data-stu-id="a2521-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="a2521-150">Cierre sesión e iníciela de nuevo como otro usuario para ver su lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="a2521-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="a2521-151">Cierre la aplicación y vuelva a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="a2521-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="a2521-152">Observe que la sesión del usuario permanece intacta. Esto se debe a que la aplicación captura tokens de un archivo local.</span><span class="sxs-lookup"><span data-stu-id="a2521-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="a2521-153">MSAL facilita la incorporación de las características de identidades comunes a la aplicación, tanto mediante las cuentas personales como las profesionales.</span><span class="sxs-lookup"><span data-stu-id="a2521-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="a2521-154">Hace el trabajo sucio por usted: administración en caché, compatibilidad con protocolo OAuth, presentación del usuario con una interfaz de usuario de inicio de sesión, actualización de tokens expirados, etc.</span><span class="sxs-lookup"><span data-stu-id="a2521-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="a2521-155">Todo lo que necesita saber es una única llamada de API, `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="a2521-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="a2521-156">Como referencia, el ejemplo finalizado (sin sus valores de configuración) [se proporciona en forma de archivo .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), aunque también puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="a2521-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="a2521-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2521-157">Next steps</span></span>
<span data-ttu-id="a2521-158">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="a2521-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="a2521-159">Es posible que desee probar:</span><span class="sxs-lookup"><span data-stu-id="a2521-159">You may want to try:</span></span>

* [<span data-ttu-id="a2521-160">Proteger la API web TodoListService con el punto de conexión v2.0</span><span class="sxs-lookup"><span data-stu-id="a2521-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="a2521-161">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="a2521-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="a2521-162">La guía del desarrollador de v2.0 >></span><span class="sxs-lookup"><span data-stu-id="a2521-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a2521-163">Etiqueta "msal" de StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="a2521-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a2521-164">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="a2521-164">Get security updates for our products</span></span>
<span data-ttu-id="a2521-165">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite [esta página](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de avisos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a2521-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

