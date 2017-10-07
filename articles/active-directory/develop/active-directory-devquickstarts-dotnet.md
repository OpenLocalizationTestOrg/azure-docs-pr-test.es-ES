---
title: ".NET aaaAzure AD Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de escritorio de Windows de .NET que se integra con Azure AD para inicio de sesión y llama a Azure AD había protegido con OAuth de API."
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
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="76893-103">Integración de Azure AD en una aplicación WPF de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="76893-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="76893-104">Si está desarrollando una aplicación de escritorio, Azure AD facilita simple y sencillo para tooauthenticate los usuarios con sus cuentas de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76893-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="76893-105">También permite que su aplicación toosecurely consumir cualquier web API protegida por Azure AD, como Hola API de Office 365 u Hola API de Azure.</span><span class="sxs-lookup"><span data-stu-id="76893-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="76893-106">Para clientes nativos de .NET que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory o AAL.</span><span class="sxs-lookup"><span data-stu-id="76893-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="76893-107">Único propósito de AAL en la vida es toomake más sencilla para los tokens de acceso de tooget de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="76893-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="76893-108">toodemonstrate lo fácil es, a continuación, crearemos una aplicación de lista de tareas de .NET WPF que:</span><span class="sxs-lookup"><span data-stu-id="76893-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="76893-109">Obtiene acceso a los tokens para llamar a la API de Azure AD Graph hello mediante Hola [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="76893-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="76893-110">Buscar un directorio para los usuarios con un alias determinado</span><span class="sxs-lookup"><span data-stu-id="76893-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="76893-111">Cerrar la sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="76893-111">Signs users out.</span></span>

<span data-ttu-id="76893-112">aplicación toobuild Hola completa trabajo, debe:</span><span class="sxs-lookup"><span data-stu-id="76893-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="76893-113">Registrar la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="76893-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="76893-114">Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="76893-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="76893-115">Usar AAL tooget tokens de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76893-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="76893-116">tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="76893-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="76893-117">También necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="76893-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="76893-118">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="76893-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="76893-119">1. Registrar Hola DirectorySearcher aplicación</span><span class="sxs-lookup"><span data-stu-id="76893-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="76893-120">tooenable sus tokens de tooget aplicación, primero deberá tooregister en Azure AD de los inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="76893-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="76893-121">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76893-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="76893-122">En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="76893-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="76893-123">Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76893-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="76893-124">Haga clic en **Registros de aplicaciones** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="76893-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="76893-125">Siga las indicaciones de Hola y crear un nuevo **aplicación cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="76893-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="76893-126">Hola **nombre** de hello aplicación describirá los tooend-usuarios de la aplicación</span><span class="sxs-lookup"><span data-stu-id="76893-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="76893-127">Hola **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD utilizará las respuestas de símbolo (token) de tooreturn.</span><span class="sxs-lookup"><span data-stu-id="76893-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="76893-128">Escriba una aplicación de tooyour específico de valor, por ejemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="76893-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="76893-129">Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="76893-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="76893-130">Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="76893-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="76893-131">De hello **configuración** página, elija **permisos necesarios** y elija **agregar**.</span><span class="sxs-lookup"><span data-stu-id="76893-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="76893-132">Seleccione hello **Microsoft Graph** como Hola API y agregar hello **leer datos de directorio** permiso en **permisos delegados**.</span><span class="sxs-lookup"><span data-stu-id="76893-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="76893-133">Esto le permitirá la Hola de tooquery aplicación API Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="76893-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="76893-134">2. Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="76893-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="76893-135">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="76893-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="76893-136">Para toocommunicate capaz de toobe ADAL con Azure AD, deberá tooprovide con cierta información sobre el registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="76893-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="76893-137">Comienza agregando toohello AAL DirectorySearcher proyecto mediante la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="76893-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="76893-138">En el proyecto de DirectorySearcher hello, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="76893-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="76893-139">Reemplace los valores de hello de elementos de Hola Hola `<appSettings>` Hola de sección tooreflect valores entrada en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76893-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="76893-140">El código hará referencia a estos valores siempre que use ADAL.</span><span class="sxs-lookup"><span data-stu-id="76893-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="76893-141">Hola `ida:Tenant` es Hola dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="76893-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="76893-142">Hola `ida:ClientId` es clientId hello de la aplicación copian desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="76893-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="76893-143">Hola `ida:RedirectUri` es hello que registró en el portal de Hola de dirección url de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="76893-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="76893-144">3.    Usar Tokens ADAL tooGet de AAD</span><span class="sxs-lookup"><span data-stu-id="76893-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="76893-145">Hello principio básico detrás de AAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama `authContext.AcquireTokenAsync(...)`, y AAL Hola rest.</span><span class="sxs-lookup"><span data-stu-id="76893-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="76893-146">Hola `DirectorySearcher` proyecto abierto `MainWindow.xaml.cs` y busque hello `MainWindow()` método.</span><span class="sxs-lookup"><span data-stu-id="76893-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="76893-147">primer paso de Hello es la aplicación de tooinitialize `AuthenticationContext` -ADAL de la clase principal.</span><span class="sxs-lookup"><span data-stu-id="76893-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="76893-148">Esto es donde pasas AAL Hola coordenadas debe toocommunicate con Azure AD y le indique cómo toocache símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="76893-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="76893-149">Ahora busque hello `Search(...)` método, que se invocará cuando cliks de usuario de Hola Hola botón "Buscar" en la interfaz de usuario de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="76893-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="76893-150">Este método realiza una tooquery de toohello Azure AD Graph API de solicitud GET para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="76893-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="76893-151">Pero en hello tooquery de orden API Graph, debe tooinclude un access_token Hola `Authorization` solicitud de encabezado de hello - aquí es donde entra AAL.</span><span class="sxs-lookup"><span data-stu-id="76893-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="76893-152">Cuando la aplicación solicita un token mediante una llamada a `AcquireTokenAsync(...)`, AAL intentará tooreturn un token sin pedir las credenciales de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="76893-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="76893-153">Si AAL determina que el usuario hello toosign en tooget un token es necesario, mostrar un cuadro de diálogo de inicio de sesión, recopilar las credenciales de usuario de Hola y devuelve un token después de autenticarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="76893-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="76893-154">Si AAL está no se puede tooreturn un token por cualquier motivo, se producirá un `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="76893-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="76893-155">Tenga en cuenta que hello `AuthenticationResult` objeto contiene un `UserInfo` objeto que puede ser información de uso toocollect que necesite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="76893-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="76893-156">Hola DirectorySearcher, `UserInfo` es la interfaz de la aplicación de uso toocustomize Hola con el Id. de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="76893-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="76893-157">Al usuario Hola hace clic en botón "Inicio de sesión salida" Hola, queremos tooensure que Hola siguiente llamada demasiado`AcquireTokenAsync(...)` le preguntará Hola usuario toosign en.</span><span class="sxs-lookup"><span data-stu-id="76893-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="76893-158">Con AAL, esto es tan fácil como borrar la caché de tokens de hello:</span><span class="sxs-lookup"><span data-stu-id="76893-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="76893-159">Sin embargo, si el usuario hello no haga clic en botón "Inicio de sesión salida" Hola, le interesará sesión del usuario de toomaintain Hola para hello próxima vez que ejecuten Hola DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="76893-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="76893-160">Cuando se inicia la aplicación hello, puede comprobar la caché de tokens de AAL para un token existente y actualizar Hola interfaz de usuario según corresponda.</span><span class="sxs-lookup"><span data-stu-id="76893-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="76893-161">Hola `CheckForCachedToken()` método, realizar otra llamada demasiado`AcquireTokenAsync(...)`, pero esta vez pasando hello `PromptBehavior.Never` parámetro.</span><span class="sxs-lookup"><span data-stu-id="76893-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="76893-162">`PromptBehavior.Never`le indicará AAL que no debe pedirse Hola usuario para iniciar sesión, y AAL debe en su lugar producirá una excepción si resulta que no se puede tooreturn un token.</span><span class="sxs-lookup"><span data-stu-id="76893-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
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

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="76893-163">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="76893-163">Congratulations!</span></span> <span data-ttu-id="76893-164">Ahora tiene una aplicación .NET WPF que tiene Hola capacidad tooauthenticate usuarios y en funcionamiento, segura llamar a API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="76893-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="76893-165">Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="76893-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="76893-166">Ejecute la aplicación DirectorySearcher e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="76893-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="76893-167">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="76893-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="76893-168">Cierre la aplicación hello y volver a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="76893-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="76893-169">Observe cómo la sesión del usuario de hello permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="76893-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="76893-170">Cierre la sesión y vuelva a iniciarla como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="76893-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="76893-171">AAL resulta fácil tooincorporate todas estas características de identidad comunes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="76893-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="76893-172">Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentaciones usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="76893-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="76893-173">Todo lo que realmente necesita tooknow es una sola llamada API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="76893-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="76893-174">Como referencia, se proporciona el ejemplo de Hola finalizado (sin los valores de configuración) [aquí](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="76893-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="76893-175">Ahora puede mover en escenarios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="76893-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="76893-176">Puede que desee tootry:</span><span class="sxs-lookup"><span data-stu-id="76893-176">You may want tootry:</span></span>

[<span data-ttu-id="76893-177">Protección de una API Web .NET con Azure AD &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="76893-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

