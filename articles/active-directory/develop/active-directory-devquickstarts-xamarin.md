---
title: "Introducción a Xamarin de Azure AD | Microsoft Docs"
description: "Cree aplicaciones de Xamarin que se integren con Azure AD para el inicio de sesión y la llamada a las API protegidas por Azure AD mediante OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="1d6b3-103">Integración de Azure AD con aplicaciones de Xamarin</span><span class="sxs-lookup"><span data-stu-id="1d6b3-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="1d6b3-104">Con Xamarin, puede escribir aplicaciones móviles en C# que se pueden ejecutar en iOS, Android y Windows (dispositivos móviles y PC).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="1d6b3-105">Si va a compilar una aplicación con Xamarin, Azure Active Directory (Azure AD) simplifica la autenticación de los usuarios con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="1d6b3-106">La aplicación también puede consumir de forma segura cualquier API web protegida por Azure AD, como las API de Office 365 o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="1d6b3-107">Para aplicaciones de Xamarin que necesitan acceso a recursos protegidos, Azure AD proporciona la Biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="1d6b3-108">El único objetivo de ADAL es simplificar para las aplicaciones el acceso a los tokens.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="1d6b3-109">Para demostrar lo sencillo que es, en este artículo se muestra cómo compilar una aplicación de DirectorySearcher que:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="1d6b3-110">Se ejecute en iOS, Android, Escritorio de Windows, Windows Phone y Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="1d6b3-111">Use una biblioteca de clases portable (PCL) única para autenticar a los usuarios y obtener tokens para la API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="1d6b3-112">Busque un directorio para los usuarios con un UPN determinado.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="1d6b3-113">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="1d6b3-113">Before you get started</span></span>
* <span data-ttu-id="1d6b3-114">Descargue el [esqueleto del proyecto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip) o el [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="1d6b3-115">Cada descarga es una solución de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="1d6b3-116">También necesita a un inquilino de Azure AD en el que crear usuarios y registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="1d6b3-117">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="1d6b3-118">Cuando esté listo, siga los procedimientos descritos en las cuatro secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="1d6b3-119">Paso 1: Configuración del entorno de desarrollo de Xamarin</span><span class="sxs-lookup"><span data-stu-id="1d6b3-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="1d6b3-120">Como este tutorial incluye proyectos de iOS, Android y Windows, necesitará tanto Visual Studio como Xamarin.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="1d6b3-121">Para crear el entorno es necesario, realice el proceso que se describe en [Establecimiento e instalación de Visual Studio y Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="1d6b3-122">Estas instrucciones incluyen material que puede examinar para aprender más sobre Xamarin mientras espera a que finalicen los instaladores.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="1d6b3-123">Después de que finalice la instalación, abra la solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="1d6b3-124">Encontrará seis proyectos: cinco proyectos específicos de la plataforma y una PLC, DirectorySearcher.cs, que se compartirá entre todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="1d6b3-125">Paso 2: Registro de la aplicación DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="1d6b3-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="1d6b3-126">Para permitir que la aplicación obtenga tokens, primero debe registrarla en su inquilino de Azure AD y concederle permiso de acceso a la API de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="1d6b3-127">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-127">Here's how:</span></span>

1. <span data-ttu-id="1d6b3-128">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1d6b3-129">En la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-129">On the top bar, click your account.</span></span> <span data-ttu-id="1d6b3-130">A continuación, en la lista **Directorio**, seleccione el inquilino de Active Directory donde quiere registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="1d6b3-131">Haga clic en **Más servicios** en el panel izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="1d6b3-132">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="1d6b3-133">Para crear una nueva **aplicación cliente nativa**, siga las indicaciones.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="1d6b3-134">**Nombre**: describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="1d6b3-135">El **URI de redirección** es una combinación de esquema y cadena que usará Azure AD para devolver respuestas de tokens.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="1d6b3-136">Escriba un valor (por ejemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="1d6b3-137">Una vez completado el registro, Azure AD asigna a la aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="1d6b3-138">Copie el valor de la pestaña **Aplicación**, ya que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="1d6b3-139">En la página **Configuración**, seleccione **Permisos necesarios** y **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="1d6b3-140">Seleccione **Microsoft Graph** como la API.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="1d6b3-141">En **Permisos delegados**, agregue el permiso **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="1d6b3-142">Esta acción permite que la aplicación consulte la API Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="1d6b3-143">Paso 3: Instalación y configuración de ADAL</span><span class="sxs-lookup"><span data-stu-id="1d6b3-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="1d6b3-144">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="1d6b3-145">Para permitir que AAL se comunique con Azure AD, proporciónele alguna información sobre el registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="1d6b3-146">Agregue ADAL al proyecto DirectorySearcher mediante la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="1d6b3-147">Observe que se agregan dos referencias de biblioteca a cada proyecto: la parte PCL de ADAL y una parte específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="1d6b3-148">En el proyecto DirectorySearcherLib, abra DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="1d6b3-149">Reemplace los valores de miembro de clase por los valores que escribió en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="1d6b3-150">El código hace referencia a estos valores cada vez que usa AAL.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="1d6b3-151">El *inquilino* es el dominio de su inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="1d6b3-152">*clientId* es e id. de cliente de la aplicación, que se copia del portal.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="1d6b3-153">*returnUri* es el URI que de redirección que especificó en el portal (por ejemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="1d6b3-154">Paso 4: Uso de ADAL para obtener tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d6b3-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="1d6b3-155">Casi toda la lógica de autenticación de la aplicación se basa en `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="1d6b3-156">En los proyectos específicos de la plataforma, lo único que hace falta es pasar un parámetro contextual a la PCL `DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="1d6b3-157">Abra DirectorySearcher.cs y agregue un nuevo parámetro al método `SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="1d6b3-158">`IPlatformParameters` es el parámetro contextual que encapsula los objetos específicos de la plataforma que ADAL necesita para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="1d6b3-159">Inicialice `AuthenticationContext`, que es la clase principal de ADAL.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="1d6b3-160">Esta acción pasa a ADAL las coordenadas que necesita para comunicarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="1d6b3-161">Llame a `AcquireTokenAsync(...)`, que acepta el objeto `IPlatformParameters` e inicia el flujo de autenticación necesario para devolver un token a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="1d6b3-162">`AcquireTokenAsync(...)` primero intenta devolver un token para el recurso solicitado (la API Graph API en este caso) sin solicitar a los usuarios que escriban sus credenciales (mediante el almacenamiento en caché o la actualización de tokens antiguos).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="1d6b3-163">Solo si es necesario, muestra a los usuarios la página de inicio de sesión de Azure AD antes de adquirir el token solicitado.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="1d6b3-164">Adjunte el token de acceso a la solicitud de API Graph en la cabecera de **autorización**:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="1d6b3-165">Eso es todo para la PCL `DirectorySearcher` y el código relacionado con la identidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="1d6b3-166">Ya solo queda llamar al método `SearchByAlias(...)` en las vistas de cada plataforma y, si es necesario, agregar código para administrar correctamente el ciclo de vida de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="1d6b3-167">Android</span><span class="sxs-lookup"><span data-stu-id="1d6b3-167">Android</span></span>
1. <span data-ttu-id="1d6b3-168">En MainActivity.cs, agregue una llamada a `SearchByAlias(...)` en el controlador de clic de botón:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="1d6b3-169">Reemplace el método de ciclo de vida `OnActivityResult` para reenviar cualquier redirección de autenticación de vuelta al método de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="1d6b3-170">ADAL proporciona un método auxiliar para esto en Android:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="1d6b3-171">Escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="1d6b3-171">Windows Desktop</span></span>
<span data-ttu-id="1d6b3-172">En MainWindow.xaml.cs, realice una llamada a `SearchByAlias(...)` pasando `WindowInteropHelper` al objeto `PlatformParameters` del escritorio:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="1d6b3-173">iOS</span><span class="sxs-lookup"><span data-stu-id="1d6b3-173">iOS</span></span>
<span data-ttu-id="1d6b3-174">En DirSearchClient_iOSViewController.cs, el objeto `PlatformParameters` de iOS toma una referencia al controlador de vista:</span><span class="sxs-lookup"><span data-stu-id="1d6b3-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="1d6b3-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="1d6b3-175">Windows Universal</span></span>
<span data-ttu-id="1d6b3-176">En Windows Universal, abra MainPage.xaml.cs y luego implemente el método `Search`.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="1d6b3-177">Este método usa un método auxiliar en un proyecto compartido para actualizar la interfaz de usuario según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="1d6b3-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d6b3-178">What's next</span></span>
<span data-ttu-id="1d6b3-179">Ahora dispone de una aplicación de Xamarin que funciona que puede autenticar a los usuarios y llamar a API web de forma segura mediante OAuth 2.0 en cinco plataformas diferentes.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="1d6b3-180">Si aún no ha rellenado al inquilino con usuarios, ahora es el momento de hacerlo.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="1d6b3-181">Ejecute la aplicación DirectorySearcher y luego inicie sesión con uno de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="1d6b3-182">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="1d6b3-183">ADAL facilita la incorporación de características de identidad comunes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="1d6b3-184">Hace el trabajo sucio por usted: administración en caché, compatibilidad con el protocolo OAuth, presentación al usuario de una interfaz de usuario de inicio de sesión y actualización de tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="1d6b3-185">Solo debe conocer una única llamada de API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="1d6b3-186">Como referencia, descargue el [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="1d6b3-187">Ahora puede trasladarse a escenarios de identidad adicionales.</span><span class="sxs-lookup"><span data-stu-id="1d6b3-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="1d6b3-188">Por ejemplo, pruebe [Protección de una API web de .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b3-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
