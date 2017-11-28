---
title: "aaaAzure de Windows Phone AD Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de Windows Phone que se integra con Azure AD para inicio de sesión y llama a Azure AD había protegido con OAuth de API."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="7c0a0-103">Integración de Azure AD con una aplicación de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="7c0a0-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="7c0a0-104">Los proyectos de Windows Phone 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="7c0a0-105">Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="7c0a0-106">Si está desarrollando una aplicación de Windows Phone 8.1, Azure AD facilita simple y sencillo para tooauthenticate los usuarios con sus cuentas de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="7c0a0-107">También permite que su aplicación toosecurely consumir cualquier web API protegida por Azure AD, como Hola API de Office 365 u Hola API de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="7c0a0-108">Este ejemplo de código usa ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="7c0a0-109">Para la tecnología más reciente de hello, puede que desee tooinstead try nuestro [Tutorial Universal de Windows mediante AAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="7c0a0-110">Si realmente está creando una aplicación para Windows Phone 8.1, éste es el lugar de derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="7c0a0-111">AAL v2.0 sigue siendo totalmente compatible y está hello forma recomendada de desarrollo de aplicaciones de agianst Windows Phone 8.1 con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="7c0a0-112">Para clientes nativos de .NET que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory o AAL.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="7c0a0-113">Único propósito de AAL en la vida es toomake más sencilla para los tokens de acceso de tooget de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="7c0a0-114">toodemonstrate lo fácil es, a continuación, crearemos una aplicación de Windows Phone 8.1 "directorio buscador" que:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="7c0a0-115">Obtiene acceso a los tokens para llamar a la API de Azure AD Graph hello mediante Hola [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="7c0a0-116">Busque un directorio para los usuarios con un UPN determinado.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="7c0a0-117">Cerrar la sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="7c0a0-117">Signs users out.</span></span>

<span data-ttu-id="7c0a0-118">aplicación toobuild Hola completa trabajo, debe:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="7c0a0-119">Registrar la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c0a0-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="7c0a0-120">Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="7c0a0-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="7c0a0-121">Usar AAL tooget tokens de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="7c0a0-122">tooget iniciado, [descargar un proyecto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="7c0a0-123">Cualquiera de los dos es una solución de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="7c0a0-124">También necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="7c0a0-125">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="7c0a0-126">1. Registrar Hola aplicación buscador de directorio</span><span class="sxs-lookup"><span data-stu-id="7c0a0-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="7c0a0-127">tooenable sus tokens de tooget aplicación, primero deberá tooregister en Azure AD de los inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="7c0a0-128">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7c0a0-129">En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="7c0a0-130">Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7c0a0-131">Haga clic en **Registros de aplicaciones** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="7c0a0-132">Siga las indicaciones de Hola y crear un nuevo **aplicación cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="7c0a0-133">Hola **nombre** de hello aplicación describirá los tooend-usuarios de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7c0a0-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="7c0a0-134">Hola **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD utilizará las respuestas de símbolo (token) de tooreturn.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="7c0a0-135">Escriba un valor de marcador de posición por ahora, por ejemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="7c0a0-136">Reemplazaremos este valor más adelante.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="7c0a0-137">Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="7c0a0-138">Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="7c0a0-139">De hello **configuración** página, elija **permisos necesarios** y elija **agregar**.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="7c0a0-140">Seleccione hello **Microsoft Graph** como Hola API y agregar hello **leer datos de directorio** permiso en **permisos delegados**.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="7c0a0-141">Esto le permitirá la Hola de tooquery aplicación API Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="7c0a0-142">2. Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="7c0a0-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="7c0a0-143">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="7c0a0-144">Para toocommunicate capaz de toobe ADAL con Azure AD, deberá tooprovide con cierta información sobre el registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="7c0a0-145">Comienza agregando toohello AAL DirectorySearcher proyecto mediante la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="7c0a0-146">En el proyecto de DirectorySearcher hello, abra `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="7c0a0-147">Reemplace los valores de hello en hello `Config Values` Hola de región tooreflect valores entrada en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="7c0a0-148">El código hará referencia a estos valores siempre que use ADAL.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="7c0a0-149">Hola `tenant` es Hola dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="7c0a0-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="7c0a0-150">Hola `clientId` es clientId hello de la aplicación copian desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="7c0a0-151">Ahora debe uri de devolución de llamada de hello toodiscover para la aplicación de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="7c0a0-152">Define un punto de interrupción en esta línea de hello `MainPage` método:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="7c0a0-153">Ejecutar aplicación hello y reserva Copiar valor de Hola de `redirectUri` cuando se visita el punto de interrupción de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="7c0a0-154">Debe tener un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="7c0a0-155">En hello **configurar** pestaña de la aplicación Hola Portal de administración de Azure, reemplace el valor de Hola de hello **RedirectUri** con este valor.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="7c0a0-156">3. Usar Tokens ADAL tooGet de AAD</span><span class="sxs-lookup"><span data-stu-id="7c0a0-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="7c0a0-157">Hello principio básico detrás de AAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama `authContext.AcquireToken(…)`, y AAL Hola rest.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="7c0a0-158">primer paso de Hello es la aplicación de tooinitialize `AuthenticationContext` -ADAL de la clase principal.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="7c0a0-159">Esto es donde pasas AAL Hola coordenadas debe toocommunicate con Azure AD y le indique cómo toocache símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="7c0a0-160">Ahora busque hello `Search(...)` método, que se invocará cuando cliks de usuario de Hola Hola botón "Buscar" en la interfaz de usuario de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="7c0a0-161">Este método realiza una tooquery de toohello Azure AD Graph API de solicitud GET para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="7c0a0-162">Pero en hello tooquery de orden API Graph, debe tooinclude un access_token Hola `Authorization` solicitud de encabezado de hello - aquí es donde entra AAL.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="7c0a0-163">Si es necesaria la autenticación interactiva, AAL usará Broker de autenticación de Web de Windows Phone (WAB) y [modelo de continuación](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD iniciar sesión en la página.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="7c0a0-164">Cuando Hola usuario inicia sesión, la aplicación debe toopass resultados de AAL hello de interacción de WAB Hola.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="7c0a0-165">Esto es tan sencillo como implementar hello `ContinueWebAuthentication` interfaz:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="7c0a0-166">Ahora es Hola de tiempo toouse `AuthenticationResult` que AAL devuelve tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="7c0a0-167">Hola `QueryGraph(...)` devolución de llamada, adjuntar access_token Hola adquirió toohello GET solicitud en el encabezado de autorización de hello:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="7c0a0-168">También puede usar hello `AuthenticationResult` toodisplay información acerca del usuario de hello en la aplicación del objeto.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="7c0a0-169">Hola  `QueryGraph(...)` /método siguiente, Id. del usuario de uso Hola resultado tooshow hello en la página de hello:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="7c0a0-170">Por último, puede usar ADAL toosign Hola usuario fuera de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="7c0a0-171">Al usuario Hola hace clic en botón "Inicio de sesión salida" Hola, queremos tooensure que Hola siguiente llamada demasiado`AcquireTokenSilentAsync(...)` se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="7c0a0-172">Con AAL, esto es tan fácil como borrar la caché de tokens de hello:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="7c0a0-173">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="7c0a0-173">Congratulations!</span></span> <span data-ttu-id="7c0a0-174">Ahora tiene una aplicación de Windows Phone que tiene Hola capacidad tooauthenticate usuarios en funcionamiento, segura llamar a API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="7c0a0-175">Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="7c0a0-176">Ejecute la aplicación DirectorySearcher e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="7c0a0-177">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="7c0a0-178">Cierre la aplicación hello y volver a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="7c0a0-179">Observe cómo la sesión del usuario de hello permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="7c0a0-180">Cierre la sesión y vuelva a iniciarla como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="7c0a0-181">AAL resulta fácil tooincorporate todas estas características de identidad comunes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="7c0a0-182">Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentaciones usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="7c0a0-183">Todo lo que realmente necesita tooknow es una sola llamada API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="7c0a0-184">Como referencia, se proporciona el ejemplo de Hola finalizado (sin los valores de configuración) [aquí](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7c0a0-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="7c0a0-185">Ahora puede mover en escenarios de identidad tooadditional.</span><span class="sxs-lookup"><span data-stu-id="7c0a0-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="7c0a0-186">Puede que desee tootry:</span><span class="sxs-lookup"><span data-stu-id="7c0a0-186">You may want tootry:</span></span>

[<span data-ttu-id="7c0a0-187">Protección de una API Web .NET con Azure AD &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="7c0a0-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

