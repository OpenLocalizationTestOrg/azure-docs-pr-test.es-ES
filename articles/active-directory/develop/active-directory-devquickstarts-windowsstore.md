---
title: "Introducción a Tienda Windows de Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="b7208-103">Integración de Azure AD con aplicación de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="b7208-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="b7208-104">Los proyectos de Windows Store 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b7208-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="b7208-105">Para más información, consulte [Compatibilidad y destinatarios de la plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="b7208-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="b7208-106">Si va a desarrollar aplicaciones para la Tienda Windows, Azure Active Directory (Azure AD) simplifica la autenticación de los usuarios con sus cuentas de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b7208-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="b7208-107">Mediante la integración con Azure AD, una aplicación puede consumir de forma segura cualquier API web protegida por Azure AD, como las API de Office 365 o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7208-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="b7208-108">Para aplicaciones de escritorio de la Tienda Windows que necesitan acceder a recursos protegidos, Azure AD proporciona la Biblioteca de autenticación de Active Directory o ADAL.</span><span class="sxs-lookup"><span data-stu-id="b7208-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="b7208-109">El único propósito de ADAL es facilitar que la aplicación obtenga acceso a los tokens.</span><span class="sxs-lookup"><span data-stu-id="b7208-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="b7208-110">Para demostrar lo sencillo que es, en este artículo se muestra cómo compilar una aplicación de la Tienda Windows de DirectorySearcher que:</span><span class="sxs-lookup"><span data-stu-id="b7208-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="b7208-111">Obtiene tokens de acceso para llamar a la API Graph de Azure AD mediante el [protocolo de autenticación OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7208-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b7208-112">Busca un directorio para usuarios con un nombre principal de usuario (UPN).</span><span class="sxs-lookup"><span data-stu-id="b7208-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="b7208-113">Cerrar la sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="b7208-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="b7208-114">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="b7208-114">Before you get started</span></span>
* <span data-ttu-id="b7208-115">Descargue el [esqueleto del proyecto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip) o el [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b7208-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="b7208-116">Cada descarga es una solución de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b7208-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="b7208-117">También necesita a un inquilino de Azure AD en el que crear usuarios y registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7208-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="b7208-118">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b7208-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="b7208-119">Cuando esté listo, siga los procedimientos que se describen en las tres secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="b7208-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="b7208-120">Paso 1: Registro de la aplicación DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="b7208-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="b7208-121">Para permitir que la aplicación obtenga tokens, primero debe registrarla en su inquilino de Azure AD y concederle permiso de acceso a la API de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="b7208-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="b7208-122">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="b7208-122">Here's how:</span></span>

1. <span data-ttu-id="b7208-123">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b7208-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b7208-124">En la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b7208-124">On the top bar, click your account.</span></span> <span data-ttu-id="b7208-125">A continuación, en la lista **Directorio**, seleccione el inquilino de Active Directory donde quiere registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7208-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="b7208-126">Haga clic en **Más servicios** en el panel izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7208-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b7208-127">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b7208-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b7208-128">Siga las indicaciones y cree una **aplicación de cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="b7208-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="b7208-129">**Nombre**: describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b7208-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="b7208-130">El **URI de redirección** es una combinación de esquema y cadena que usará Azure AD para devolver respuestas de tokens.</span><span class="sxs-lookup"><span data-stu-id="b7208-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="b7208-131">Por ahora, escriba un valor de marcador de posición (por ejemplo, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="b7208-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="b7208-132">Este valor lo remplazará más adelante.</span><span class="sxs-lookup"><span data-stu-id="b7208-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="b7208-133">Después de haber completado el registro, Azure AD asigna la aplicación a un id. de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="b7208-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="b7208-134">Copie el valor de la pestaña **Aplicación**, ya que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="b7208-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="b7208-135">En la página **Configuración**, seleccione **Permisos necesarios** y **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b7208-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="b7208-136">Para la aplicación **Azure Active Directory**, seleccione **Microsoft Graph** como la API.</span><span class="sxs-lookup"><span data-stu-id="b7208-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="b7208-137">En **Permisos delegados**, agregue el permiso **Acceder al directorio como usuario con sesión iniciada**.</span><span class="sxs-lookup"><span data-stu-id="b7208-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="b7208-138">Así se permite que la aplicación realice consultas en la API Graph sobre usuarios.</span><span class="sxs-lookup"><span data-stu-id="b7208-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="b7208-139">Paso 2: Instalación y configuración de ADAL</span><span class="sxs-lookup"><span data-stu-id="b7208-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="b7208-140">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="b7208-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="b7208-141">Para permitir que AAL se comunique con Azure AD, proporciónele alguna información sobre el registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7208-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="b7208-142">Agregue ADAL al proyecto DirectorySearcher mediante la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="b7208-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="b7208-143">En el proyecto de DirectorySearcher, abra MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="b7208-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="b7208-144">Reemplace los valores de la región **Valores configurados** por los valores que escribió en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b7208-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="b7208-145">El código hace referencia a estos valores cada vez que usa AAL.</span><span class="sxs-lookup"><span data-stu-id="b7208-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b7208-146">El *inquilino* es el dominio de su inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b7208-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="b7208-147">*clientId* es e id. de cliente de la aplicación, que se copia del portal.</span><span class="sxs-lookup"><span data-stu-id="b7208-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="b7208-148">Ahora debe detectar el URI de devolución de llamada para la aplicación de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="b7208-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="b7208-149">Establezca un punto de interrupción en esta línea en el método `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="b7208-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="b7208-150">Compile la solución y asegúrese de que se haya restaurado las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="b7208-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="b7208-151">Si faltan paquetes, abra el Administrador de paquetes de Nuget y restáurelos.</span><span class="sxs-lookup"><span data-stu-id="b7208-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="b7208-152">Ejecute la aplicación y copie el valor de `redirectUri` cuando se alcance el punto de interrupción.</span><span class="sxs-lookup"><span data-stu-id="b7208-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="b7208-153">El valor debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7208-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="b7208-154">De nuevo en la pestaña **Configuración** de la aplicación en Azure Portal, agregue un valor de **RedirectUri** como el anterior.</span><span class="sxs-lookup"><span data-stu-id="b7208-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="b7208-155">Paso 3: Uso de ADAL para obtener tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7208-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="b7208-156">El principio básico inherente a ADAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama a `authContext.AcquireToken(…)` y ADAL se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="b7208-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="b7208-157">Inicialice la clase `AuthenticationContext`, que es la clase principal de AAL.</span><span class="sxs-lookup"><span data-stu-id="b7208-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="b7208-158">Esta acción pasa a ADAL las coordenadas necesarias para comunicarse con Azure AD e indicarle cómo almacenar en caché los tokens.</span><span class="sxs-lookup"><span data-stu-id="b7208-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="b7208-159">Busque el método `Search(...)`, que se invoca cuando los usuarios hacen clic en el botón **Buscar** en la interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7208-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="b7208-160">Este método realiza una solicitud GET a la API de Azure AD Graph para realizar una consulta sobre los usuarios cuyo UPN comienza con el término de búsqueda especificado.</span><span class="sxs-lookup"><span data-stu-id="b7208-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="b7208-161">Para consultar la API Graph, incluya un token de acceso en el encabezado de **autorización** de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b7208-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="b7208-162">Aquí es donde entra en juego AAL.</span><span class="sxs-lookup"><span data-stu-id="b7208-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="b7208-163">Cuando la aplicación llama a `AcquireTokenAsync(...)` para solicitar un token, ADAL intenta devolver uno sin pedir al usuario credenciales.</span><span class="sxs-lookup"><span data-stu-id="b7208-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="b7208-164">Si ADAL determina que el usuario necesita iniciar sesión para obtener un token, muestra un cuadro de diálogo de inicio de sesión, recopila las credenciales del usuario y devuelve un token después de que la autenticación se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="b7208-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="b7208-165">Si por algún motivo ADAL no puede devolver un token, el estado *AuthenticationResult* es un error.</span><span class="sxs-lookup"><span data-stu-id="b7208-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="b7208-166">Ahora es el momento de usar el token de acceso que acaba de adquirir.</span><span class="sxs-lookup"><span data-stu-id="b7208-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="b7208-167">También en el método `Search(...)`, adjunte el token a la solicitud GET de API Graph en el encabezado de **autorización**:</span><span class="sxs-lookup"><span data-stu-id="b7208-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="b7208-168">Puede usar el objeto `AuthenticationResult` para mostrar información sobre el usuario de la aplicación, como su id.:</span><span class="sxs-lookup"><span data-stu-id="b7208-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="b7208-169">También puede usar ADAL para cerrar la sesión de los usuarios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7208-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="b7208-170">Cuando el usuario haga clic en el botón **Cerrar sesión**, asegúrese de que la siguiente llamada a `AcquireTokenAsync(...)` muestre una vista de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b7208-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="b7208-171">Con ADAL, esta acción es tan fácil como borrar la caché de tokens:</span><span class="sxs-lookup"><span data-stu-id="b7208-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="b7208-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7208-172">What's next</span></span>
<span data-ttu-id="b7208-173">Ahora tiene una aplicación de la Tienda Windows en funcionamiento que puede autenticar a los usuarios, realizar llamadas seguras a las API web que usan OAuth 2.0 y obtener información básica sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="b7208-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="b7208-174">Si aún no ha rellenado al inquilino con usuarios, ahora es el momento de hacerlo.</span><span class="sxs-lookup"><span data-stu-id="b7208-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="b7208-175">Ejecute la aplicación DirectorySearcher y luego inicie sesión con uno de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b7208-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="b7208-176">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="b7208-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="b7208-177">Cierre la aplicación y vuelva a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="b7208-177">Close the app, and rerun it.</span></span> <span data-ttu-id="b7208-178">Observe cómo la sesión del usuario permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="b7208-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="b7208-179">Cierre la sesión; para ello, haga clic con el botón derecho para mostrar la barra inferior y vuelva a iniciar sesión con otro usuario.</span><span class="sxs-lookup"><span data-stu-id="b7208-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="b7208-180">ADAL facilita la incorporación de todas estas características comunes de identidad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7208-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="b7208-181">Hace el trabajo sucio por usted: administración en caché, compatibilidad con el protocolo OAuth, presentación al usuario de una interfaz de usuario de inicio de sesión y actualización de tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="b7208-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="b7208-182">Solo debe conocer una única llamada de API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="b7208-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="b7208-183">Como referencia, descargue el [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="b7208-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="b7208-184">Ahora puede trasladarse a escenarios de identidad adicionales.</span><span class="sxs-lookup"><span data-stu-id="b7208-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="b7208-185">Por ejemplo, pruebe [Protección de una API web de .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b7208-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
