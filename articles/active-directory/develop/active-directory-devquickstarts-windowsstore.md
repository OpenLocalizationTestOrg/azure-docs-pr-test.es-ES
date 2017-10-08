---
title: "aaaAzure tienda de AD Windows Introducción | Documentos de Microsoft"
description: "Cree aplicaciones de la Tienda Windows que se integren con Azure AD para el inicio de sesión y la llamada a las API protegidas por Azure AD mediante OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="dd42d-103">Integración de Azure AD con aplicación de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="dd42d-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="dd42d-104">Los proyectos de Windows Store 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dd42d-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="dd42d-105">Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="dd42d-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="dd42d-106">Si está desarrollando aplicaciones para la tienda Windows hello, Azure Active Directory (Azure AD) resulta sencilla y directa tooauthenticate los usuarios con sus cuentas de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dd42d-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="dd42d-107">Mediante la integración con Azure AD, una aplicación segura puede consumir cualquier API que está protegido con Azure AD, como Hola API de Office 365 o hello Azure API web.</span><span class="sxs-lookup"><span data-stu-id="dd42d-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="dd42d-108">Tienda Windows para aplicaciones de escritorio que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="dd42d-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="dd42d-109">Hola único propósito de AAL es toomake más sencilla para los tokens de acceso de tooget de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="dd42d-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="dd42d-110">toodemonstrate lo fácil que es, este artículo muestra cómo toobuild una DirectorySearcher de la tienda Windows app que:</span><span class="sxs-lookup"><span data-stu-id="dd42d-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="dd42d-111">Obtiene acceso para llamar a API de Azure AD Graph hello mediante el uso de hello [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd42d-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="dd42d-112">Busca un directorio para usuarios con un nombre principal de usuario (UPN).</span><span class="sxs-lookup"><span data-stu-id="dd42d-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="dd42d-113">Cerrar la sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="dd42d-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="dd42d-114">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="dd42d-114">Before you get started</span></span>
* <span data-ttu-id="dd42d-115">Descargar hello [proyecto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), o descargar hello [ejemplo completo](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="dd42d-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="dd42d-116">Cada descarga es una solución de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="dd42d-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="dd42d-117">También necesita a un inquilino de Azure AD en las que los usuarios toocreate y la aplicación hello de registro.</span><span class="sxs-lookup"><span data-stu-id="dd42d-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="dd42d-118">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="dd42d-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="dd42d-119">Cuando esté listo, siga los procedimientos de hello en Hola tres secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="dd42d-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="dd42d-120">Paso 1: Registrar aplicación de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="dd42d-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="dd42d-121">tooenable Hola aplicación tooget símbolos (tokens), primero debe tooregister en Azure AD de inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="dd42d-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="dd42d-122">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="dd42d-122">Here's how:</span></span>

1. <span data-ttu-id="dd42d-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd42d-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dd42d-124">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="dd42d-124">On hello top bar, click your account.</span></span> <span data-ttu-id="dd42d-125">A continuación, en hello **Directory** inquilinos de Active Directory de hello seleccione donde desea que la aplicación de hello tooregister, la lista.</span><span class="sxs-lookup"><span data-stu-id="dd42d-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="dd42d-126">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd42d-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="dd42d-127">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dd42d-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="dd42d-128">Siga Hola indicaciones toocreate una **aplicación cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="dd42d-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="dd42d-129">**Nombre** describe hello toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd42d-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="dd42d-130">**URI de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn token respuestas.</span><span class="sxs-lookup"><span data-stu-id="dd42d-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="dd42d-131">Por ahora, escriba un valor de marcador de posición (por ejemplo, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="dd42d-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="dd42d-132">Reemplace el valor de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="dd42d-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="dd42d-133">Después de haber completado el registro de hello, Azure AD le asigna aplicación hello un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="dd42d-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="dd42d-134">Copiar valor de hello en hello **aplicación** ficha, porque lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="dd42d-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="dd42d-135">En hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="dd42d-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="dd42d-136">Para hello **Azure Active Directory** aplicación, seleccione **Microsoft Graph** como Hola API.</span><span class="sxs-lookup"><span data-stu-id="dd42d-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="dd42d-137">En **permisos delegados**, agregar hello **obtener acceso al directorio de hello como usuario con sesión iniciada hello** permiso.</span><span class="sxs-lookup"><span data-stu-id="dd42d-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="dd42d-138">Al hacerlo, permite Hola Hola tooquery API Graph aplicación para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="dd42d-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="dd42d-139">Paso 2: Instalación y configuración de ADAL</span><span class="sxs-lookup"><span data-stu-id="dd42d-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="dd42d-140">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="dd42d-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="dd42d-141">tooenable toocommunicate ADAL con Azure AD proporciona cierta información sobre el registro de una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="dd42d-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="dd42d-142">Agregar toohello AAL DirectorySearcher proyecto mediante el uso de la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="dd42d-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="dd42d-143">En el proyecto de DirectorySearcher hello, abra MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="dd42d-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="dd42d-144">Reemplace los valores de hello en hello **valores de configuración** región con valores de hello que escribió en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd42d-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="dd42d-145">El código hace referencia a valores de toothese cada vez que usa AAL.</span><span class="sxs-lookup"><span data-stu-id="dd42d-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="dd42d-146">Hola *inquilino* es Hola dominio del inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="dd42d-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="dd42d-147">Hola *clientId* es Hola Id. de cliente de la aplicación hello, que se copió desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd42d-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="dd42d-148">Ahora debe devolución de llamada de toodiscover Hola URI para la aplicación de la tienda de Windows.</span><span class="sxs-lookup"><span data-stu-id="dd42d-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="dd42d-149">Define un punto de interrupción en esta línea de hello `MainPage` método:</span><span class="sxs-lookup"><span data-stu-id="dd42d-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="dd42d-150">Crear solución de hello, asegurándose de que se restauran todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="dd42d-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="dd42d-151">Si faltan algunos paquetes, abra el Administrador de paquetes de NuGet Hola y restaurarlos.</span><span class="sxs-lookup"><span data-stu-id="dd42d-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="dd42d-152">Ejecutar aplicación hello y copie el valor de Hola de `redirectUri` cuando se visita el punto de interrupción de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd42d-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="dd42d-153">valor de Hello debe tener un aspecto similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="dd42d-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="dd42d-154">En hello **configuración** pestaña de aplicación Hola Hola portal de Azure, agregue un **RedirectUri** con hello anterior valor.</span><span class="sxs-lookup"><span data-stu-id="dd42d-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="dd42d-155">Paso 3: Usar AAL tooget los tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd42d-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="dd42d-156">Hello principio básico detrás de AAL es que cada vez que la aplicación hello necesita un token de acceso, simplemente llama `authContext.AcquireToken(…)`, y AAL Hola rest.</span><span class="sxs-lookup"><span data-stu-id="dd42d-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="dd42d-157">Inicializar la aplicación hello `AuthenticationContext`, que es la clase principal de hello de AAL.</span><span class="sxs-lookup"><span data-stu-id="dd42d-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="dd42d-158">Esta acción pasa coordenadas de hello AAL necesarios toocommunicate con Azure AD y le diga cómo toocache símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="dd42d-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="dd42d-159">Busque hello `Search(...)` método, que se invoca cuando los usuarios hacen clic hello **búsqueda** botón en la interfaz de usuario de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dd42d-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="dd42d-160">Este método realiza una tooquery de toohello Azure AD Graph API de solicitud get para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="dd42d-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="dd42d-161">Hola tooquery API Graph, incluir un token de acceso en la solicitud de hello **autorización** encabezado.</span><span class="sxs-lookup"><span data-stu-id="dd42d-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="dd42d-162">Aquí es donde entra en juego AAL.</span><span class="sxs-lookup"><span data-stu-id="dd42d-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="dd42d-163">Cuando la aplicación hello solicita un token mediante una llamada a `AcquireTokenAsync(...)`, AAL intenta tooreturn un token sin pedir las credenciales de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd42d-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="dd42d-164">Si AAL determina que el usuario hello toosign en tooget un token es necesario, muestra un cuadro de diálogo de inicio de sesión, recopila las credenciales de usuario de Hola y devuelve un token después de la autenticación se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="dd42d-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="dd42d-165">Si AAL está no se puede tooreturn un token por cualquier motivo, Hola *AuthenticationResult* estado es un error.</span><span class="sxs-lookup"><span data-stu-id="dd42d-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="dd42d-166">Ahora es el token de acceso de tiempo toouse Hola que acaba de adquirir.</span><span class="sxs-lookup"><span data-stu-id="dd42d-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="dd42d-167">También en hello `Search(...)` método, adjuntar hello toohello token solicitud de obtención de API Graph en hello **autorización** encabezado:</span><span class="sxs-lookup"><span data-stu-id="dd42d-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="dd42d-168">Puede usar hello `AuthenticationResult` toodisplay información acerca del usuario de hello en la aplicación hello, como un identificador de usuario de hello del objeto:</span><span class="sxs-lookup"><span data-stu-id="dd42d-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="dd42d-169">También puede usar ADAL toosign usuarios fuera de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dd42d-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="dd42d-170">Cuando el usuario de hello hace clic en hello **cerrar sesión** botón, asegúrese de esa llamada siguiente Hola demasiado`AcquireTokenAsync(...)` muestra una vista de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="dd42d-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="dd42d-171">Con AAL, esta acción es tan fácil como borrar la caché de tokens de hello:</span><span class="sxs-lookup"><span data-stu-id="dd42d-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="dd42d-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd42d-172">What's next</span></span>
<span data-ttu-id="dd42d-173">Ahora tiene una aplicación de la tienda de Windows que puede autenticar a los usuarios, seguro llamar a las API mediante OAuth 2.0 web y obtener información básica acerca del usuario de hello en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="dd42d-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="dd42d-174">Si ya no ha rellenado al inquilino con usuarios, ahora es Hola tiempo toodo para.</span><span class="sxs-lookup"><span data-stu-id="dd42d-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="dd42d-175">Ejecutar la aplicación DirectorySearcher y, a continuación, inicie sesión con uno de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd42d-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="dd42d-176">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="dd42d-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="dd42d-177">Cierre la aplicación hello y volver a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="dd42d-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="dd42d-178">Observe cómo la sesión del usuario de hello permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="dd42d-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="dd42d-179">Cerrar la sesión haciendo clic en la barra de toodisplay Hola inferior y, a continuación, vuelva a iniciarla como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="dd42d-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="dd42d-180">AAL resulta fácil tooincorporate todas estas características comunes de identidad en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dd42d-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="dd42d-181">Se encarga de todo el trabajo dirty Hola para usted, como la administración de memoria caché, compatibilidad con el protocolo OAuth, presentar usuario Hola con una interfaz de usuario de inicio de sesión y actualizar expirado símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="dd42d-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="dd42d-182">Necesita llamada tooknow solo una única API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="dd42d-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="dd42d-183">Como referencia, descargar hello [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sin los valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="dd42d-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="dd42d-184">Ahora puede mover en escenarios de identidad tooadditional.</span><span class="sxs-lookup"><span data-stu-id="dd42d-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="dd42d-185">Por ejemplo, pruebe [Protección de una API web de .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dd42d-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
