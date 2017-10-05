---
title: "Introducción a Windows Phone de Azure AD | Microsoft Docs"
description: "Creación de una aplicación de Windows Phone que se integra con Azure AD para el inicio de sesión y llama a las API protegidas de Azure AD mediante OAuth."
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="c4e3c-103">Integración de Azure AD con una aplicación de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="c4e3c-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="c4e3c-104">Los proyectos de Windows Phone 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="c4e3c-105">Para más información, consulte [Compatibilidad y destinatarios de la plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="c4e3c-106">Si está desarrollando una aplicación de Windows Phone 8.1, Azure AD le facilita la autenticación de sus usuarios con sus cuentas de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="c4e3c-107">También permite a la aplicación consumir con seguridad cualquier API web protegida por Azure AD, como las API de Office 365 o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="c4e3c-108">Este ejemplo de código usa ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="c4e3c-109">Si le interesa la tecnología más reciente, puede probar en su lugar nuestro [Tutorial de Windows Universal utilizando ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="c4e3c-110">Si realmente está creando una aplicación para Windows Phone 8.1, este es el lugar adecuado.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="c4e3c-111">ADAL v2.0 sigue siendo totalmente compatible y es la manera recomendada para el desarrollo de aplicaciones para Windows Phone 8.1 con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="c4e3c-112">Para los clientes nativos .NET que necesitan tener acceso a recursos protegidos, Azure AD proporciona la biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="c4e3c-113">El único propósito de ADAL es facilitar a su aplicación la obtención de tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="c4e3c-114">Para demostrar lo sencillo que es, crearemos a continuación una aplicación de Windows Phone 8.1 de "buscador de directorios" que:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="c4e3c-115">Obtenga tokens de acceso para llamar a la API de gráficos de Azure AD utilizando el [protocolo de autenticación OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="c4e3c-116">Busque un directorio para los usuarios con un UPN determinado.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="c4e3c-117">Cerrar la sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="c4e3c-117">Signs users out.</span></span>

<span data-ttu-id="c4e3c-118">Para crear la aplicación de trabajo completa, deberá:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="c4e3c-119">Registrar la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4e3c-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="c4e3c-120">Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="c4e3c-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="c4e3c-121">Usar ADAL para obtener tokens de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="c4e3c-122">Para empezar, [descargue el proyecto del esquema](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) o [descargue el ejemplo finalizado](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="c4e3c-123">Cualquiera de los dos es una solución de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="c4e3c-124">También necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="c4e3c-125">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="c4e3c-126">1. Registro de la aplicación de buscador de directorios</span><span class="sxs-lookup"><span data-stu-id="c4e3c-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="c4e3c-127">Para habilitar la aplicación para obtener tokens, primero deberá registrarla en su inquilino de Azure AD y concederle permiso de acceso a la API de gráficos de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="c4e3c-128">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c4e3c-129">En la barra superior, haga clic en su cuenta y, en la lista **Directorio**, elija el inquilino de Active Directory en el que desee registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="c4e3c-130">Haga clic en **Más servicios** en el panel de navegación izquierdo y elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c4e3c-131">Haga clic en **Registros de aplicaciones** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="c4e3c-132">Siga las indicaciones y cree una nueva **Aplicación de cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="c4e3c-133">El **nombre** de la aplicación servirá de descripción de la aplicación para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="c4e3c-134">El **URI de redirección** es una combinación de esquema y cadena que utilizará Azure AD para devolver las respuestas de los tokens.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="c4e3c-135">Escriba un valor de marcador de posición por ahora, por ejemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="c4e3c-136">Reemplazaremos este valor más adelante.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="c4e3c-137">Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="c4e3c-138">Necesitará este valor en las secciones siguientes, así que cópielo de la pestaña de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="c4e3c-139">En la página **Configuración**, elija **Permisos necesarios** y luego **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="c4e3c-140">Seleccione **Microsoft Graph** como API y agregue el permiso **Leer datos de directorio** en **Permisos delegados**.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="c4e3c-141">Esto permitirá a su aplicación consultar la API Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="c4e3c-142">2. Instalar y configurar ADAL</span><span class="sxs-lookup"><span data-stu-id="c4e3c-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="c4e3c-143">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="c4e3c-144">Para que ADAL pueda comunicarse con Azure AD, hay que proporcionarle información sobre el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="c4e3c-145">Comience agregando ADAL al proyecto DirectorySearcher con la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="c4e3c-146">En el proyecto de buscador de directorios, abra `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="c4e3c-147">Reemplace los valores de la región `Config Values` para que reflejen los valores especificados en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="c4e3c-148">El código hará referencia a estos valores siempre que use ADAL.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="c4e3c-149">`tenant` es el dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="c4e3c-150">`clientId` es el identificador de cliente de la aplicación que copió del portal.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="c4e3c-151">Ahora deberá detectar el URI de devolución de llamada para la aplicación de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="c4e3c-152">Establezca un punto de interrupción en esta línea en el método `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="c4e3c-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="c4e3c-153">Ejecute la aplicación y copie aparte el valor de `redirectUri` cuando se alcance el punto de interrupción.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="c4e3c-154">Debe tener un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="c4e3c-155">En la pestaña **Configurar** de la aplicación en el Portal de administración de Azure, reemplace el valor de **RedirectUri** por este valor.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="c4e3c-156">3. Usar ADAL para obtener tokens de AAD</span><span class="sxs-lookup"><span data-stu-id="c4e3c-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="c4e3c-157">El principio básico inherente a ADAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama a  `authContext.AcquireToken(…)` y ADAL se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="c4e3c-158">El primer paso consiste en inicializar `AuthenticationContext` de la aplicación: clase principal de ADAL.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="c4e3c-159">Este es el lugar en el que pasa a ADAL las coordenadas que necesita para comunicarse con Azure AD e indicarle cómo almacenar en caché los tokens.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="c4e3c-160">Ahora busque el método `Search(...)` , que se invoca cuando el usuario hace clic en el botón de búsqueda en la interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="c4e3c-161">Este método realiza una solicitud GET a la API Graph de Azure AD para realizar una consulta sobre los usuarios cuyo UPN comienza con el término de búsqueda especificado.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="c4e3c-162">Sin embargo, para realizar una consulta a la API Graph, tiene que incluir un access_token en el encabezado `Authorization` de la solicitud, que es donde entra ADAL.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="c4e3c-163">Si es necesaria la autenticación interactiva, ADAL utilizará el agente de autenticación Web (WAB) de Windows Phone y el [modelo de continuación](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) para mostrar la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="c4e3c-164">Cuando el usuario inicia sesión, la aplicación necesita pasar a ADAL los resultados de la interacción de WAB.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="c4e3c-165">Esto es tan sencillo como implementar la interfaz `ContinueWebAuthentication` :</span><span class="sxs-lookup"><span data-stu-id="c4e3c-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="c4e3c-166">Ahora es el momento de usar el `AuthenticationResult` que ADAL ha devuelto a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="c4e3c-167">En la devolución de llamada `QueryGraph(...)`, adjunte access_token adquirido a la solicitud GET en el encabezado de autorización:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="c4e3c-168">También puede utilizar el objeto `AuthenticationResult` para mostrar información sobre el usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="c4e3c-169">En el método `QueryGraph(...)` , utilice el resultado para mostrar el identificador del usuario en la página:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="c4e3c-170">Por último, también puede usar ADAL para cerrar la sesión del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="c4e3c-171">Cuando el usuario hace clic en el botón "Cerrar sesión", queremos asegurarnos de que la próxima llamada a `AcquireTokenSilentAsync(...)` fallará.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="c4e3c-172">Con ADAL, esto es tan fácil como borrar la caché de tokens:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="c4e3c-173">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="c4e3c-173">Congratulations!</span></span> <span data-ttu-id="c4e3c-174">Ahora tiene una aplicación de Windows Phone en funcionamiento que tiene la capacidad de autenticar usuarios, realizar llamadas seguras a las API Web que usan OAuth 2.0 e y obtener información básica sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="c4e3c-175">Si no lo ha hecho ya, ahora es el momento de completar el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="c4e3c-176">Ejecute la aplicación DirectorySearcher e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="c4e3c-177">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="c4e3c-178">Cierre la aplicación y vuelva a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="c4e3c-179">Observe cómo la sesión del usuario permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="c4e3c-180">Cierre la sesión y vuelva a iniciarla como otro usuario.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="c4e3c-181">ADAL facilita la incorporación de todas estas características comunes de identidad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="c4e3c-182">Hace el trabajo sucio por usted: administración en caché, compatibilidad con protocolo OAuth, presentación del usuario con una interfaz de usuario de inicio de sesión, actualización de tokens expirados, etc.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="c4e3c-183">Todo lo que necesita saber es una única llamada de API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="c4e3c-184">Como referencia, se proporciona el ejemplo finalizado (sin sus valores de configuración) [aquí](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c4e3c-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="c4e3c-185">Ahora puede trasladarse a escenarios de identidad adicionales.</span><span class="sxs-lookup"><span data-stu-id="c4e3c-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="c4e3c-186">Es posible que desee probar:</span><span class="sxs-lookup"><span data-stu-id="c4e3c-186">You may want to try:</span></span>

[<span data-ttu-id="c4e3c-187">Protección de una API Web .NET con Azure AD >></span><span class="sxs-lookup"><span data-stu-id="c4e3c-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

