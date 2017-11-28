---
title: "aaaAzure AD Xamarin Introducción | Documentos de Microsoft"
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="8ac28-103">Integración de Azure AD con aplicaciones de Xamarin</span><span class="sxs-lookup"><span data-stu-id="8ac28-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="8ac28-104">Con Xamarin, puede escribir aplicaciones móviles en C# que se pueden ejecutar en iOS, Android y Windows (dispositivos móviles y PC).</span><span class="sxs-lookup"><span data-stu-id="8ac28-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="8ac28-105">Si va a compilar una aplicación con Xamarin, Azure Active Directory (Azure AD) hace tooauthenticate simple a los usuarios con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ac28-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="8ac28-106">aplicación Hello también segura puede consumir cualquier API web protegida por Azure AD, como la API de Office 365 Hola o hello API de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ac28-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="8ac28-107">Para las aplicaciones de Xamarin que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="8ac28-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="8ac28-108">Hola único propósito de AAL es toomake más sencilla para los tokens de acceso de tooget de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8ac28-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="8ac28-109">toodemonstrate lo fácil es, este artículo se muestra cómo toobuild DirectorySearcher aplicaciones que:</span><span class="sxs-lookup"><span data-stu-id="8ac28-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="8ac28-110">Se ejecute en iOS, Android, Escritorio de Windows, Windows Phone y Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="8ac28-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="8ac28-111">Usar una sola clase portable (PCL) de la biblioteca tooauthenticate usuarios y obtener tokens para hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="8ac28-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="8ac28-112">Busque un directorio para los usuarios con un UPN determinado.</span><span class="sxs-lookup"><span data-stu-id="8ac28-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="8ac28-113">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="8ac28-113">Before you get started</span></span>
* <span data-ttu-id="8ac28-114">Descargar hello [proyecto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), o descargar hello [ejemplo completo](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="8ac28-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="8ac28-115">Cada descarga es una solución de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8ac28-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="8ac28-116">También necesita a un inquilino de Azure AD en las que los usuarios toocreate y la aplicación hello de registro.</span><span class="sxs-lookup"><span data-stu-id="8ac28-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="8ac28-117">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8ac28-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="8ac28-118">Cuando esté listo, siga los procedimientos de hello en Hola cuatro secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="8ac28-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="8ac28-119">Paso 1: Configuración del entorno de desarrollo de Xamarin</span><span class="sxs-lookup"><span data-stu-id="8ac28-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="8ac28-120">Como este tutorial incluye proyectos de iOS, Android y Windows, necesitará tanto Visual Studio como Xamarin.</span><span class="sxs-lookup"><span data-stu-id="8ac28-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="8ac28-121">entorno necesarias toocreate hello, proceso de hello completa en [establecer una copia de seguridad e instale Visual Studio y Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="8ac28-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="8ac28-122">instrucciones de Hello incluyen material que puede revisar toolearn más información sobre Xamarin mientras está esperando Hola instalaciones toobe completado.</span><span class="sxs-lookup"><span data-stu-id="8ac28-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="8ac28-123">Después de haber completado el programa de instalación de hello, abra la solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ac28-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="8ac28-124">Encontrará seis proyectos: cinco proyectos específicos de la plataforma y una PLC, DirectorySearcher.cs, que se compartirá entre todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="8ac28-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="8ac28-125">Paso 2: Registrar aplicación de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="8ac28-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="8ac28-126">tooenable Hola aplicación tooget símbolos (tokens), primero debe tooregister en Azure AD de inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="8ac28-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="8ac28-127">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="8ac28-127">Here's how:</span></span>

1. <span data-ttu-id="8ac28-128">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ac28-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8ac28-129">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="8ac28-129">On hello top bar, click your account.</span></span> <span data-ttu-id="8ac28-130">A continuación, en hello **Directory** inquilinos de Active Directory de hello seleccione donde desea que la aplicación de hello tooregister, la lista.</span><span class="sxs-lookup"><span data-stu-id="8ac28-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="8ac28-131">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ac28-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="8ac28-132">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8ac28-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="8ac28-133">toocreate un nuevo **aplicación cliente nativa**, siga las indicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ac28-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="8ac28-134">**Nombre** describe hello toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8ac28-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="8ac28-135">**URI de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn token respuestas.</span><span class="sxs-lookup"><span data-stu-id="8ac28-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="8ac28-136">Escriba un valor (por ejemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="8ac28-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="8ac28-137">Una vez completado el registro, Azure AD le asigna aplicación hello un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="8ac28-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="8ac28-138">Copiar valor de Hola de hello **aplicación** ficha, porque lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="8ac28-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="8ac28-139">En hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="8ac28-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="8ac28-140">Seleccione **Microsoft Graph** como Hola API.</span><span class="sxs-lookup"><span data-stu-id="8ac28-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="8ac28-141">En **permisos delegados**, agregar hello **leer datos de directorio** permiso.</span><span class="sxs-lookup"><span data-stu-id="8ac28-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="8ac28-142">Esta acción habilita Hola Hola tooquery API Graph aplicación para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8ac28-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="8ac28-143">Paso 3: Instalación y configuración de ADAL</span><span class="sxs-lookup"><span data-stu-id="8ac28-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="8ac28-144">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="8ac28-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="8ac28-145">tooenable toocommunicate ADAL con Azure AD proporciona cierta información sobre el registro de una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="8ac28-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="8ac28-146">Agregar toohello AAL DirectorySearcher proyecto mediante el uso de la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="8ac28-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

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

    <span data-ttu-id="8ac28-147">Tenga en cuenta que se han agregado dos referencias de biblioteca de proyecto tooeach: Hola PCL parte de AAL y una parte específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="8ac28-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="8ac28-148">En el proyecto DirectorySearcherLib de hello, abra DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="8ac28-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="8ac28-149">Reemplazar valores de miembro de clase de hello con valores de hello que escribió en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ac28-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="8ac28-150">El código hace referencia a valores de toothese cada vez que usa AAL.</span><span class="sxs-lookup"><span data-stu-id="8ac28-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="8ac28-151">Hola *inquilino* es Hola dominio del inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="8ac28-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="8ac28-152">Hola *clientId* es Hola Id. de cliente de la aplicación hello, que se copió desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ac28-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="8ac28-153">Hola *returnUri* es Hola redirección URI especificado en el portal de hello (por ejemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="8ac28-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="8ac28-154">Paso 4: Usar AAL tooget los tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac28-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="8ac28-155">Casi todo de lógica de autenticación de la aplicación hello se encuentra en `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="8ac28-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="8ac28-156">Todo lo que es necesario en los proyectos específicos de la plataforma de hello es toopass un toohello parámetro contextual `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="8ac28-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="8ac28-157">Abra DirectorySearcher.cs y, a continuación, agregue un nuevo toohello parámetro `SearchByAlias(...)` método.</span><span class="sxs-lookup"><span data-stu-id="8ac28-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="8ac28-158">`IPlatformParameters`es que la autenticación de ADAL necesidades tooperform Hola de objetos de parámetro contextual hello que encapsula Hola específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="8ac28-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="8ac28-159">Inicializar `AuthenticationContext`, que es la clase principal de hello de AAL.</span><span class="sxs-lookup"><span data-stu-id="8ac28-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="8ac28-160">Este Hola AAL de fases de acción coordina necesidades toocommunicate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ac28-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="8ac28-161">Llame a `AcquireTokenAsync(...)`, que acepta hello `IPlatformParameters` objeto e invoca el flujo de autenticación de Hola que sea necesario tooreturn una aplicación toohello símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="8ac28-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

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

    <span data-ttu-id="8ac28-162">`AcquireTokenAsync(...)`primer intentos tooreturn un token para hello requerido recurso (Hola API Graph en este caso) sin preguntar tooenter a los usuarios sus credenciales (mediante el almacenamiento en caché o actualizar tokens anteriores).</span><span class="sxs-lookup"><span data-stu-id="8ac28-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="8ac28-163">Según sea necesario, muestra a los usuarios hello Azure AD inicio de sesión página antes de adquirir el token solicitado Hola.</span><span class="sxs-lookup"><span data-stu-id="8ac28-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="8ac28-164">Asociar la solicitud de API Graph de toohello token de acceso de Hola Hola **autorización** encabezado:</span><span class="sxs-lookup"><span data-stu-id="8ac28-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="8ac28-165">Eso es todo para hello `DirectorySearcher` código relacionadas con la identidad de hello y PCL la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8ac28-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="8ac28-166">Todo lo que queda es hello toocall `SearchByAlias(...)` método en las vistas de cada plataforma y, en caso necesario, tooadd código para controlar correctamente Hola del ciclo de vida de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8ac28-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="8ac28-167">Android</span><span class="sxs-lookup"><span data-stu-id="8ac28-167">Android</span></span>
1. <span data-ttu-id="8ac28-168">En MainActivity.cs, agregue una llamada demasiado`SearchByAlias(...)` botón Hola de controlador de clic:</span><span class="sxs-lookup"><span data-stu-id="8ac28-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="8ac28-169">Invalidar hello `OnActivityResult` tooforward de método de ciclo de vida cualquier autenticación redirige el método adecuado de toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="8ac28-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="8ac28-170">ADAL proporciona un método auxiliar para esto en Android:</span><span class="sxs-lookup"><span data-stu-id="8ac28-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="8ac28-171">Escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="8ac28-171">Windows Desktop</span></span>
<span data-ttu-id="8ac28-172">En MainWindow.xaml.cs, realizar una llamada demasiado`SearchByAlias(...)` pasando un `WindowInteropHelper` en desktop hello `PlatformParameters` objeto:</span><span class="sxs-lookup"><span data-stu-id="8ac28-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="8ac28-173">iOS</span><span class="sxs-lookup"><span data-stu-id="8ac28-173">iOS</span></span>
<span data-ttu-id="8ac28-174">En DirSearchClient_iOSViewController.cs, Hola iOS `PlatformParameters` objeto toma un controlador de vista de toohello de referencia:</span><span class="sxs-lookup"><span data-stu-id="8ac28-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="8ac28-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="8ac28-175">Windows Universal</span></span>
<span data-ttu-id="8ac28-176">En universales de Windows, abra MainPage.xaml.cs y, a continuación, implementar hello `Search` método.</span><span class="sxs-lookup"><span data-stu-id="8ac28-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="8ac28-177">Este método usa un método auxiliar en un proyecto compartido de tooupdate interfaz de usuario según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8ac28-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="8ac28-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ac28-178">What's next</span></span>
<span data-ttu-id="8ac28-179">Ahora dispone de una aplicación de Xamarin que funciona que puede autenticar a los usuarios y llamar a API web de forma segura mediante OAuth 2.0 en cinco plataformas diferentes.</span><span class="sxs-lookup"><span data-stu-id="8ac28-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="8ac28-180">Si ya no ha rellenado al inquilino con usuarios, ahora es Hola tiempo toodo para.</span><span class="sxs-lookup"><span data-stu-id="8ac28-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="8ac28-181">Ejecutar la aplicación DirectorySearcher y, a continuación, inicie sesión con uno de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ac28-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="8ac28-182">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="8ac28-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="8ac28-183">ADAL facilita la fácil tooincorporate características de identidad comunes en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8ac28-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="8ac28-184">Se encarga de todo el trabajo dirty Hola para usted, como la administración de memoria caché, compatibilidad con el protocolo OAuth, presentar usuario Hola con una interfaz de usuario de inicio de sesión y actualizar expirado símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="8ac28-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="8ac28-185">Necesita llamada tooknow solo una única API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="8ac28-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="8ac28-186">Como referencia, descargar hello [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sin los valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="8ac28-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="8ac28-187">Ahora puede mover en escenarios de identidad tooadditional.</span><span class="sxs-lookup"><span data-stu-id="8ac28-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="8ac28-188">Por ejemplo, pruebe [Protección de una API web de .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8ac28-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
