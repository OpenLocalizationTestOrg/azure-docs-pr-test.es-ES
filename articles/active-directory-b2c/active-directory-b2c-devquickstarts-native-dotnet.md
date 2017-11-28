---
title: Azure Active Directory B2C | Microsoft Docs
description: "Creación de una aplicación de escritorio de Windows que incluye tareas de registro, inicio de sesión y administración de perfiles mediante Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="f7cf6-103">Azure AD B2C: creación de una aplicación de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="f7cf6-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="f7cf6-104">Con Azure Active Directory (Azure AD) B2C, puede agregar eficaces características de administración de identidades autoservicio a sus aplicaciones de escritorio en pocos pasos.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="f7cf6-105">En este artículo se le mostrará cómo crear una aplicación de "lista de tareas pendientes" de Windows Presentation Foundation (WPF) para .NET que incluya tareas de registro, inicio de sesión y administración de perfiles de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="f7cf6-106">La aplicación permitirá registrarse e iniciar sesión mediante un nombre de usuario o un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="f7cf6-107">También será posible registrarse e iniciar sesión con cuentas sociales, como Facebook y Google.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f7cf6-108">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f7cf6-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="f7cf6-109">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="f7cf6-110">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="f7cf6-111">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f7cf6-112">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="f7cf6-112">Create an application</span></span>
<span data-ttu-id="f7cf6-113">A continuación, debe crear una aplicación en su directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="f7cf6-114">Esto proporciona a Azure AD la información que necesita para comunicarse de forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="f7cf6-115">Para crear una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="f7cf6-116">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-116">Be sure to:</span></span>

* <span data-ttu-id="f7cf6-117">Incluir un **cliente nativo** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="f7cf6-118">Copie la **URI de redirección** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="f7cf6-119">Es la dirección URL predeterminada para este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="f7cf6-120">Copiar el **id. de aplicación** asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="f7cf6-121">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f7cf6-122">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="f7cf6-122">Create your policies</span></span>
<span data-ttu-id="f7cf6-123">En Azure AD B2C, cada experiencia de usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f7cf6-124">Este ejemplo de código contiene tres experiencias de identidad: registro, inicio de sesión y edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="f7cf6-125">Tendrá que crear una directiva de cada tipo, como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="f7cf6-126">Cuando cree las tres directivas, asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="f7cf6-127">Elegir **User ID sign-up** (Registro con id. de usuario) o **Email sign-up** (Registro con correo electrónico) en la hoja de proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="f7cf6-128">Seleccionar **Nombre para mostrar** y otros atributos de registro en la directiva de registro.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="f7cf6-129">Elegir las notificaciones **Nombre para mostrar** e **Id. de objeto** como notificaciones de aplicación en todas las directivas.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="f7cf6-130">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="f7cf6-131">Copiar el **nombre** de cada directiva después de crearla.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="f7cf6-132">Debe tener el prefijo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="f7cf6-133">Necesitará estos nombres de directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f7cf6-134">Cuando haya creado correctamente las tres directivas, estará listo para crear su aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="f7cf6-135">Descargar el código</span><span class="sxs-lookup"><span data-stu-id="f7cf6-135">Download the code</span></span>
<span data-ttu-id="f7cf6-136">El código de este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="f7cf6-137">Para generar el ejemplo a medida que avanza, puede [descargar un proyecto de esqueleto como archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="f7cf6-138">También puede clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="f7cf6-139">La aplicación completada también estará [disponible como archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) o en la rama `complete` del mismo repositorio.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="f7cf6-140">Una vez descargado el código de ejemplo, abra el archivo .sln de Visual Studio para empezar.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="f7cf6-141">El proyecto `TaskClient` es una aplicación web MVC con la que el usuario interactúa.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="f7cf6-142">Para los fines de este tutorial, llama a una tarea de back-end de API web, hospedada en Azure, que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="f7cf6-143">No es necesario crear la API web, ya que se ejecuta automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="f7cf6-144">Para saber de qué forma una API web autentica de forma segura las solicitudes con Azure AD B2C, consulte nuestro [artículo de introducción a la API web](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="f7cf6-145">Ejecución de directivas</span><span class="sxs-lookup"><span data-stu-id="f7cf6-145">Execute policies</span></span>
<span data-ttu-id="f7cf6-146">Su aplicación se comunica con Azure AD B2C mediante el envío de solicitudes de autenticación HTTP que especifican la directiva que desea ejecutar como parte de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="f7cf6-147">Para aplicaciones de escritorio .NET, puede usar la versión preliminar de la Biblioteca de autenticación de Microsoft (MSAL) para enviar mensajes de autenticación de OAuth 2.0, ejecutar directivas y obtener tokens para llamar a las API web.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="f7cf6-148">Instalación de MSAL</span><span class="sxs-lookup"><span data-stu-id="f7cf6-148">Install MSAL</span></span>
<span data-ttu-id="f7cf6-149">Agregue MSAL al proyecto `TaskClient` mediante la Consola del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="f7cf6-150">Escribir los detalles de B2C</span><span class="sxs-lookup"><span data-stu-id="f7cf6-150">Enter your B2C details</span></span>
<span data-ttu-id="f7cf6-151">Abra el archivo `Globals.cs` y reemplace cada uno de los valores de propiedad por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="f7cf6-152">Esta clase se usa en todo `TaskClient` para hacer referencia a valores de uso frecuente.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="f7cf6-153">Creación de PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="f7cf6-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="f7cf6-154">La clase principal de MSAL es `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="f7cf6-155">Esta clase representa la aplicación en el sistema de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="f7cf6-156">Cuando se inicializa la aplicación, cree una instancia de `PublicClientApplication` en `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="f7cf6-157">Esta puede usarse en toda la ventana.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="f7cf6-158">Inicio de un flujo de registro</span><span class="sxs-lookup"><span data-stu-id="f7cf6-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="f7cf6-159">Cuando un usuario decide registrarse, quiere iniciar un flujo de registro que usa la directiva de registro que ha creado.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="f7cf6-160">Con MSAL, simplemente llama a `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="f7cf6-161">Los parámetros que pasa a `AcquireTokenAsync(...)` determinan el token que recibe, la directiva usada en la solicitud de autenticación, etc.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="f7cf6-162">Inicio de un flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f7cf6-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="f7cf6-163">Puede iniciar un flujo de inicio de sesión de la misma manera que inicia un flujo de registro.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="f7cf6-164">Cuando un usuario inicia sesión, realiza la misma llamada a MSAL, pero esta vez usando la directiva de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="f7cf6-165">Inicio de un flujo de edición de perfiles</span><span class="sxs-lookup"><span data-stu-id="f7cf6-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="f7cf6-166">De nuevo, puede ejecutar una directiva de edición de perfiles de la misma manera:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="f7cf6-167">En todos estos casos, MSAL devuelve un token en `AuthenticationResult` o genera una excepción.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="f7cf6-168">Cada vez que reciba un token de MSAL, puede usar el objeto `AuthenticationResult.User` para actualizar los datos de usuario en la aplicación, como la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="f7cf6-169">ADAL también almacena en caché el token para usarlo en otras partes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="f7cf6-170">Búsqueda de tokens en el inicio de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f7cf6-170">Check for tokens on app start</span></span>
<span data-ttu-id="f7cf6-171">También puede utilizar MSAL para realizar el seguimiento del estado de inicio de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="f7cf6-172">En esta aplicación, queremos que el usuario continúe con la sesión, incluso después de haber cerrado la aplicación y de volver a abrirla.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="f7cf6-173">De vuelta a la invalidación de `OnInitialized`, utilice el método `AcquireTokenSilent` de MSAL para buscar tokens en caché:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
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
```

## <a name="call-the-task-api"></a><span data-ttu-id="f7cf6-174">Llamada a la API de tarea</span><span class="sxs-lookup"><span data-stu-id="f7cf6-174">Call the task API</span></span>
<span data-ttu-id="f7cf6-175">Ya hemos usado MSAL para ejecutar directivas y obtener tokens.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="f7cf6-176">Si desea usar uno estos tokens para llamar a la API de la tarea, puede usar nuevamente el `AcquireTokenSilent` método de MSAL para buscar tokens en caché:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

<span data-ttu-id="f7cf6-177">Cuando la llamada a `AcquireTokenSilentAsync(...)` se realiza correctamente y hay un token en la memoria caché, puede agregarlo al encabezado `Authorization` de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="f7cf6-178">La API web de la tarea usará este encabezado para autenticar la solicitud para leer la lista de tareas pendientes del usuario:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="f7cf6-179">Cerrar la sesión del usuario</span><span class="sxs-lookup"><span data-stu-id="f7cf6-179">Sign the user out</span></span>
<span data-ttu-id="f7cf6-180">Finalmente, puede usar MSAL para finalizar la sesión de un usuario en la aplicación cuando el usuario selecciona **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="f7cf6-181">Con MSAL, esto se logra borrando todos los tokens de la caché de tokens:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="f7cf6-182">Ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7cf6-182">Run the sample app</span></span>
<span data-ttu-id="f7cf6-183">Finalmente, compile y ejecute el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="f7cf6-184">Regístrese en la aplicación con una dirección de correo electrónico o un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="f7cf6-185">Cierre la sesión y vuelva a iniciarla como el mismo usuario.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="f7cf6-186">Edite el perfil de ese usuario.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-186">Edit that user's profile.</span></span> <span data-ttu-id="f7cf6-187">Cierre la sesión y regístrese con otro usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="f7cf6-188">Agregar IDP sociales</span><span class="sxs-lookup"><span data-stu-id="f7cf6-188">Add social IDPs</span></span>
<span data-ttu-id="f7cf6-189">Actualmente, la aplicación solo admite registros e inicios de sesión de usuarios que usan **cuentas locales**.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="f7cf6-190">Se trata de cuentas almacenadas en el directorio B2C que utilizan un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="f7cf6-191">Con Azure AD B2C, puede agregar compatibilidad con otros proveedores de identidades (IDP) sin cambiar el código.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="f7cf6-192">Para agregar proveedores de identidades sociales a su aplicación, comience siguiendo las instrucciones detalladas en estos artículos.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="f7cf6-193">Para cada proveedor de identidades que desee admitir, necesitará registrar una aplicación en ese sistema y obtener un identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="f7cf6-194">Configurar Facebook como una IDP</span><span class="sxs-lookup"><span data-stu-id="f7cf6-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="f7cf6-195">Configurar Google como una IDP</span><span class="sxs-lookup"><span data-stu-id="f7cf6-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="f7cf6-196">Configurar Amazon como una IDP</span><span class="sxs-lookup"><span data-stu-id="f7cf6-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="f7cf6-197">Configurar LinkedIn como una IDP</span><span class="sxs-lookup"><span data-stu-id="f7cf6-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="f7cf6-198">Después de agregar los proveedores de identidades a su directorio B2C, tendrá que editar cada una de las tres directivas para incluir los nuevos proveedores de identidades, tal y como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f7cf6-199">Después de guardar las directivas, vuelva a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="f7cf6-200">Debería ver los proveedores de identidades nuevos agregados como opciones de inicio de sesión y registro en cada una de sus experiencias de identidad.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="f7cf6-201">Puede experimentar con las directivas y observar los efectos en la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="f7cf6-202">Agregue o quite proveedores de identidades, manipule notificaciones de aplicación o cambie atributos de registro.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="f7cf6-203">Experimente para ver cómo se combinan directivas, solicitudes de autenticación y MSAL.</span><span class="sxs-lookup"><span data-stu-id="f7cf6-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="f7cf6-204">Como referencia, el ejemplo completo [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f7cf6-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f7cf6-205">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="f7cf6-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
