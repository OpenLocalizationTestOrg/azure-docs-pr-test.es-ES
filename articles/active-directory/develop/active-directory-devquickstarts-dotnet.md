---
title: "Introducción a .NET de Azure AD | Microsoft Docs"
description: "Creación de una aplicación de escritorio .NET de Windows que se integra con Azure AD para el inicio de sesión y llama a las API protegidas de Azure AD mediante OAuth."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="acf62-103">Integración de Azure AD en una aplicación WPF de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="acf62-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="acf62-104">Si está desarrollando una aplicación de escritorio, Azure AD le facilita la autenticación de sus usuarios mediante sus cuentas de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="acf62-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="acf62-105">También permite a la aplicación consumir con seguridad cualquier API web protegida por Azure AD, como las API de Office 365 o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf62-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="acf62-106">Para los clientes nativos .NET que necesitan tener acceso a recursos protegidos, Azure AD proporciona la Biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="acf62-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="acf62-107">El único propósito de ADAL es facilitar a su aplicación la obtención de tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="acf62-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="acf62-108">Para demostrar lo fácil que es, crearemos aquí una aplicación de lista de tareas pendientes (ToDo) de .NET WPF que permita realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="acf62-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="acf62-109">Obtener tokens de acceso para llamar a la API Graph de Azure AD utilizando el [protocolo de autenticación OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)</span><span class="sxs-lookup"><span data-stu-id="acf62-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="acf62-110">Buscar un directorio para los usuarios con un alias determinado</span><span class="sxs-lookup"><span data-stu-id="acf62-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="acf62-111">Cerrar la sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="acf62-111">Signs users out.</span></span>

<span data-ttu-id="acf62-112">Para crear la aplicación de trabajo completa, deberá realizar estas acciones:</span><span class="sxs-lookup"><span data-stu-id="acf62-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="acf62-113">Registrar la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf62-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="acf62-114">Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="acf62-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="acf62-115">Usar ADAL para obtener tokens de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf62-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="acf62-116">Para empezar, [descargue el esquema de la aplicación](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) o [descargue el ejemplo finalizado](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="acf62-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="acf62-117">También necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="acf62-118">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="acf62-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="acf62-119">1. Registro de la aplicación DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="acf62-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="acf62-120">Para habilitar la aplicación para obtener tokens, primero deberá registrarla en su inquilino de Azure AD y concederle permiso de acceso a la API Graph de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="acf62-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="acf62-121">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="acf62-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="acf62-122">En la barra superior, haga clic en su cuenta y, en la lista **Directorio**, elija el inquilino de Active Directory en el que desee registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="acf62-123">Haga clic en **Más servicios** en el panel de navegación izquierdo y elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acf62-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="acf62-124">Haga clic en **Registros de aplicaciones** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="acf62-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="acf62-125">Siga las indicaciones y cree una nueva **Aplicación de cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="acf62-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="acf62-126">El **nombre** de la aplicación servirá de descripción de la aplicación para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="acf62-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="acf62-127">El **URI de redirección** es una combinación de esquema y cadena que utilizará Azure AD para devolver las respuestas de los tokens.</span><span class="sxs-lookup"><span data-stu-id="acf62-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="acf62-128">Escriba un valor específico para la aplicación, por ejemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="acf62-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="acf62-129">Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="acf62-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="acf62-130">Necesitará este valor en las secciones siguientes, así que cópielo de la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="acf62-131">En la página **Configuración**, elija **Permisos necesarios** y luego **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="acf62-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="acf62-132">Seleccione **Microsoft Graph** como API y agregue el permiso **Leer datos de directorio** en **Permisos delegados**.</span><span class="sxs-lookup"><span data-stu-id="acf62-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="acf62-133">Esto permitirá a su aplicación consultar la API Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="acf62-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="acf62-134">2. Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="acf62-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="acf62-135">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="acf62-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="acf62-136">Para que ADAL pueda comunicarse con Azure AD, hay que proporcionarle información sobre el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="acf62-137">Comience agregando ADAL al proyecto DirectorySearcher con la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="acf62-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="acf62-138">En el proyecto de buscador de directorios, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="acf62-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="acf62-139">Reemplace los valores de los elementos de la sesión `<appSettings>` para que reflejen los valores especificados en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf62-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="acf62-140">El código hará referencia a estos valores siempre que use ADAL.</span><span class="sxs-lookup"><span data-stu-id="acf62-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="acf62-141">`ida:Tenant` es el dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="acf62-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="acf62-142">`ida:ClientId` es el identificador de cliente de la aplicación que copió del portal.</span><span class="sxs-lookup"><span data-stu-id="acf62-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="acf62-143">El `ida:RedirectUri` es la URL de redirección que ha registrado en el portal.</span><span class="sxs-lookup"><span data-stu-id="acf62-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="acf62-144">3.    Usar ADAL para obtener tokens de AAD</span><span class="sxs-lookup"><span data-stu-id="acf62-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="acf62-145">El principio básico inherente a ADAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama a  `authContext.AcquireTokenAsync(...)` y ADAL se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="acf62-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="acf62-146">En el proyecto `DirectorySearcher`, abra `MainWindow.xaml.cs` y busque el método `MainWindow()`.</span><span class="sxs-lookup"><span data-stu-id="acf62-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="acf62-147">El primer paso consiste en inicializar el `AuthenticationContext` de la aplicación, que es la clase principal de ADAL.</span><span class="sxs-lookup"><span data-stu-id="acf62-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="acf62-148">Este es el lugar en el que se pasan a ADAL las coordenadas necesarias para comunicarse con Azure AD e indicarle cómo almacenar en caché los tokens.</span><span class="sxs-lookup"><span data-stu-id="acf62-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="acf62-149">Ahora busque el método `Search(...)` , que se invoca cuando el usuario hace clic en el botón de búsqueda en la interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="acf62-150">Este método realiza una solicitud GET a la API Graph de Azure AD para realizar una consulta sobre los usuarios cuyo UPN comienza con el término de búsqueda especificado.</span><span class="sxs-lookup"><span data-stu-id="acf62-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="acf62-151">Sin embargo, para realizar una consulta a la API Graph, tiene que incluir un access_token en el encabezado `Authorization` de la solicitud, que es donde entra ADAL.</span><span class="sxs-lookup"><span data-stu-id="acf62-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="acf62-152">Cuando la aplicación solicita un token mediante una llamada a `AcquireTokenAsync(...)`, ADAL intentará devolver un token sin solicitar al usuario las credenciales.</span><span class="sxs-lookup"><span data-stu-id="acf62-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="acf62-153">Si ADAL determina que el usuario debe iniciar sesión para obtener un token, mostrará un cuadro de diálogo de inicio de sesión, recopilará las credenciales del usuario y devolverá un token tras una autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="acf62-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="acf62-154">Si ADAL no puede devolver un token por alguna razón, mostrará una `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="acf62-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="acf62-155">Observe que el objeto `AuthenticationResult` contiene un objeto `UserInfo` que puede usarse para recopilar información puede necesitar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="acf62-156">En el DirectorySearcher, se usa `UserInfo` para personalizar la interfaz de usuario de la aplicación con el identificador del usuario.</span><span class="sxs-lookup"><span data-stu-id="acf62-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="acf62-157">Cuando el usuario hace clic en el botón "Cerrar sesión", queremos asegurarnos de que la próxima llamada a `AcquireTokenAsync(...)` solicite al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="acf62-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="acf62-158">Con ADAL, esto es tan fácil como borrar la caché de tokens:</span><span class="sxs-lookup"><span data-stu-id="acf62-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="acf62-159">Sin embargo, si el usuario no hace clic en el botón "Cerrar sesión", puede que desee mantener la sesión del usuario para la próxima vez que ejecute DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="acf62-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="acf62-160">Cuando se inicie la aplicación, puede comprobar la caché de tokens de ADAL para un token existente y actualizar la interfaz de usuario en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="acf62-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="acf62-161">En el método `CheckForCachedToken()`, realice otra llamada a `AcquireTokenAsync(...)`, pero esta vez pasando en el parámetro `PromptBehavior.Never`.</span><span class="sxs-lookup"><span data-stu-id="acf62-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="acf62-162">`PromptBehavior.Never` indicará a ADAL que no se debe solicitar al usuario que inicie sesión. En lugar de ello, ADAL debe iniciar una excepción si no puede devolver un token.</span><span class="sxs-lookup"><span data-stu-id="acf62-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="acf62-163">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="acf62-163">Congratulations!</span></span> <span data-ttu-id="acf62-164">Ahora tiene una aplicación de WPF de .NET operativa que tiene la capacidad de autenticar usuarios, realizar llamadas seguras a las API web que usan OAuth 2.0 y obtener información básica sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="acf62-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="acf62-165">Si todavía no lo ha hecho, ahora es el momento de completar el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="acf62-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="acf62-166">Ejecute la aplicación DirectorySearcher e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="acf62-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="acf62-167">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="acf62-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="acf62-168">Cierre la aplicación y vuelva a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="acf62-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="acf62-169">Observe cómo la sesión del usuario permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="acf62-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="acf62-170">Cierre la sesión y vuelva a iniciarla como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="acf62-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="acf62-171">ADAL facilita la incorporación de todas estas características comunes de identidad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="acf62-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="acf62-172">Hace el trabajo sucio por usted: administración en caché, compatibilidad con protocolo OAuth, presentación del usuario con una interfaz de usuario de inicio de sesión, actualización de tokens expirados, etc.</span><span class="sxs-lookup"><span data-stu-id="acf62-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="acf62-173">Todo lo que necesita saber es una única llamada de API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="acf62-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="acf62-174">Como referencia, [aquí](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)puede ver el ejemplo finalizado (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="acf62-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="acf62-175">Ahora puede pasar a otros escenarios.</span><span class="sxs-lookup"><span data-stu-id="acf62-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="acf62-176">Es posible que desee probar:</span><span class="sxs-lookup"><span data-stu-id="acf62-176">You may want to try:</span></span>

[<span data-ttu-id="acf62-177">Protección de una API Web .NET con Azure AD >></span><span class="sxs-lookup"><span data-stu-id="acf62-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

