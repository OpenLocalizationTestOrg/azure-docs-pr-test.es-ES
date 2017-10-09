---
title: aaaAzure B2C de Active Directory | Documentos de Microsoft
description: "¿Cómo toobuild una aplicación de escritorio de Windows que incluye el inicio de sesión, inicio de sesión y perfil de administración mediante el uso de Azure Active Directory B2C."
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
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="5f908-103">Azure AD B2C: creación de una aplicación de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="5f908-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="5f908-104">Mediante el uso de Azure Active Directory (Azure AD) B2C, puede agregar la aplicación de escritorio de tooyour de características de administración de identidad de autoservicio eficaz en unos cuantos pasos.</span><span class="sxs-lookup"><span data-stu-id="5f908-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="5f908-105">En este artículo le mostrará cómo toocreate una aplicación de "Lista de tareas pendientes" de Windows Presentation Foundation (WPF) de .NET que incluye el inicio de sesión, inicio de sesión de usuario y la administración de perfiles.</span><span class="sxs-lookup"><span data-stu-id="5f908-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="5f908-106">aplicación Hello incluirá compatibilidad para registrarse e iniciar sesión mediante un nombre de usuario o el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="5f908-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="5f908-107">También será posible registrarse e iniciar sesión con cuentas sociales, como Facebook y Google.</span><span class="sxs-lookup"><span data-stu-id="5f908-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="5f908-108">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5f908-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="5f908-109">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="5f908-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="5f908-110">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="5f908-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="5f908-111">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="5f908-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="5f908-112">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="5f908-112">Create an application</span></span>
<span data-ttu-id="5f908-113">A continuación, debe toocreate una aplicación en el directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="5f908-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="5f908-114">Esto proporciona información de Azure AD que necesita toosecurely comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f908-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="5f908-115">toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5f908-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="5f908-116">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="5f908-116">Be sure to:</span></span>

* <span data-ttu-id="5f908-117">Incluir un **cliente nativo** en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5f908-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="5f908-118">Hola copia **URI de redireccionamiento** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="5f908-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="5f908-119">Es dirección URL predeterminada de Hola para este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="5f908-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="5f908-120">Hola copia **Id. de aplicación** decir tooyour asignado aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f908-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="5f908-121">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="5f908-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="5f908-122">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="5f908-122">Create your policies</span></span>
<span data-ttu-id="5f908-123">En Azure AD B2C, cada experiencia de usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5f908-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5f908-124">Este ejemplo de código contiene tres experiencias de identidad: registro, inicio de sesión y edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="5f908-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="5f908-125">Deberá toocreate una directiva para cada tipo, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="5f908-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="5f908-126">Cuando se crea tres directivas de hello, no olvide:</span><span class="sxs-lookup"><span data-stu-id="5f908-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="5f908-127">Elija **ID. de inicio de sesión** o **inicio de sesión de correo electrónico** en la hoja de proveedores de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f908-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="5f908-128">Seleccionar **Nombre para mostrar** y otros atributos de registro en la directiva de registro.</span><span class="sxs-lookup"><span data-stu-id="5f908-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="5f908-129">Elegir las notificaciones **Nombre para mostrar** e **Id. de objeto** como notificaciones de aplicación en todas las directivas.</span><span class="sxs-lookup"><span data-stu-id="5f908-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="5f908-130">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5f908-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="5f908-131">Hola copia **nombre** de cada directiva después de haberlo creado.</span><span class="sxs-lookup"><span data-stu-id="5f908-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="5f908-132">Deberían tener el prefijo de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="5f908-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="5f908-133">Necesitará estos nombres de directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="5f908-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="5f908-134">Una vez haya creado correctamente Hola tres directivas, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f908-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="5f908-135">Descargar código de hello</span><span class="sxs-lookup"><span data-stu-id="5f908-135">Download hello code</span></span>
<span data-ttu-id="5f908-136">Hola código para este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="5f908-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="5f908-137">ejemplo de Hola a toobuild que vaya, también puede [descargar un proyecto como un archivo .zip esqueleto](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="5f908-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="5f908-138">También puede clonar el esqueleto de hello:</span><span class="sxs-lookup"><span data-stu-id="5f908-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="5f908-139">aplicación Hello completado también es [disponible como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) o en hello `complete` rama de hello mismo repositorio.</span><span class="sxs-lookup"><span data-stu-id="5f908-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="5f908-140">Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f908-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="5f908-141">Hola `TaskClient` proyecto es Hola aplicación de escritorio de WPF que Hola usuario interactúa con.</span><span class="sxs-lookup"><span data-stu-id="5f908-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="5f908-142">Para fines de Hola de este tutorial, llama a una tarea de back-end API web, hospedado en Azure, que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="5f908-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="5f908-143">No es necesario toobuild hello web API, tenemos ya se ejecuta automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5f908-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="5f908-144">toolearn cómo una API web autentica las solicitudes de forma segura mediante el uso de Azure AD B2C, consulte el [API web Introducción artículo](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5f908-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="5f908-145">Ejecución de directivas</span><span class="sxs-lookup"><span data-stu-id="5f908-145">Execute policies</span></span>
<span data-ttu-id="5f908-146">La aplicación se comunica con Azure AD B2C mediante el envío de mensajes de autenticación que especifican la directiva de hello desean tooexecute como parte de la solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="5f908-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="5f908-147">.NET para aplicaciones de escritorio, puede usar hello obtener una vista previa de los mensajes de autenticación de biblioteca de autenticación de Microsoft (MSAL) toosend OAuth 2.0, ejecuta las directivas y obtener tokens que llamen a API web.</span><span class="sxs-lookup"><span data-stu-id="5f908-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="5f908-148">Instalación de MSAL</span><span class="sxs-lookup"><span data-stu-id="5f908-148">Install MSAL</span></span>
<span data-ttu-id="5f908-149">Agregar MSAL toohello `TaskClient` proyecto usando Hola consola de administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f908-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="5f908-150">Escribir los detalles de B2C</span><span class="sxs-lookup"><span data-stu-id="5f908-150">Enter your B2C details</span></span>
<span data-ttu-id="5f908-151">Archivo abierto hello `Globals.cs` y cada uno de los valores de propiedad de hello reemplazar por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="5f908-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="5f908-152">Esta clase se utiliza a lo largo de `TaskClient` valores tooreference de uso frecuente.</span><span class="sxs-lookup"><span data-stu-id="5f908-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="5f908-153">Crear hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="5f908-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="5f908-154">clase principal de Hola de MSAL es `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="5f908-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="5f908-155">Esta clase representa la aplicación de sistema de hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5f908-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="5f908-156">Cuando hello inicializa de aplicación, crea una instancia de `PublicClientApplication` en `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="5f908-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="5f908-157">Esto puede usarse en toda la ventana hello.</span><span class="sxs-lookup"><span data-stu-id="5f908-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="5f908-158">Inicio de un flujo de registro</span><span class="sxs-lookup"><span data-stu-id="5f908-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="5f908-159">Cuando un usuario opts toosigns seguridad, desea tooinitiate un flujo de inicio de sesión que usa la directiva de inicio de sesión de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="5f908-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="5f908-160">Con MSAL, simplemente llama a `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="5f908-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="5f908-161">Hola parámetros que se pasan demasiado`AcquireTokenAsync(...)` determinan qué token recibir, directiva de hello usada en la solicitud de autenticación de Hola y mucho más.</span><span class="sxs-lookup"><span data-stu-id="5f908-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="5f908-162">Inicio de un flujo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="5f908-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="5f908-163">También puede iniciar un flujo de inicio de sesión en hello igual que iniciar un flujo de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5f908-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="5f908-164">Cuando un usuario inicia sesión, asegúrese de Hola mismo llamar tooMSAL, esta vez utilizando la directiva de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="5f908-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="5f908-165">Inicio de un flujo de edición de perfiles</span><span class="sxs-lookup"><span data-stu-id="5f908-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="5f908-166">Una vez más, puede ejecutar una directiva de perfil de edición en hello mismo modo:</span><span class="sxs-lookup"><span data-stu-id="5f908-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="5f908-167">En todos estos casos, MSAL devuelve un token en `AuthenticationResult` o genera una excepción.</span><span class="sxs-lookup"><span data-stu-id="5f908-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="5f908-168">Cada vez que se obtendrá un token de MSAL, puede usar hello `AuthenticationResult.User` tooupdate Hola usuario datos de aplicación de hello, como Hola interfaz de usuario del objeto.</span><span class="sxs-lookup"><span data-stu-id="5f908-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="5f908-169">AAL también cachés Hola token para su uso en otras partes de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5f908-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="5f908-170">Búsqueda de tokens en el inicio de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5f908-170">Check for tokens on app start</span></span>
<span data-ttu-id="5f908-171">También puede utilizar el seguimiento de tookeep MSAL Hola del inicio de sesión de estado del usuario.</span><span class="sxs-lookup"><span data-stu-id="5f908-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="5f908-172">En esta aplicación, es deseable Hola usuario tooremain iniciado sesión, incluso después de que cierre la aplicación hello y vuelva a abrirlo.</span><span class="sxs-lookup"><span data-stu-id="5f908-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="5f908-173">Dentro de hello `OnInitialized` reemplazar, utilice del MSAL `AcquireTokenSilent` toocheck de método para los tokens almacenados en caché:</span><span class="sxs-lookup"><span data-stu-id="5f908-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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

## <a name="call-hello-task-api"></a><span data-ttu-id="5f908-174">Llamar a la API de la tarea de Hola</span><span class="sxs-lookup"><span data-stu-id="5f908-174">Call hello task API</span></span>
<span data-ttu-id="5f908-175">Ahora se ha usado las directivas de tooexecute MSAL y obtener tokens.</span><span class="sxs-lookup"><span data-stu-id="5f908-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="5f908-176">Cuando quiera toouse uno estas API de tarea de tokens toocall hello, puede volver a usar del MSAL `AcquireTokenSilent` toocheck de método para los tokens almacenados en caché:</span><span class="sxs-lookup"><span data-stu-id="5f908-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
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

<span data-ttu-id="5f908-177">Cuando Hola llamada demasiado`AcquireTokenSilentAsync(...)` se realiza correctamente y se encuentra un token en memoria caché de hello, puede agregar Hola token toohello `Authorization` encabezado de solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="5f908-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="5f908-178">API de web de tarea de Hola usará la lista de tareas pendientes de este encabezado tooauthenticate Hola solicitud tooread Hola del usuario:</span><span class="sxs-lookup"><span data-stu-id="5f908-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="5f908-179">Usuario de inicio de sesión Hola out</span><span class="sxs-lookup"><span data-stu-id="5f908-179">Sign hello user out</span></span>
<span data-ttu-id="5f908-180">Por último, puede usar MSAL tooend una sesión de usuario con la aplicación de hello cuando selecciona usuario hello **cerrar sesión**.  Al utilizar MSAL, esto se consigue mediante la desactivación de todos los tokens de Hola de caché de tokens de Hola de:</span><span class="sxs-lookup"><span data-stu-id="5f908-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="5f908-181">Ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="5f908-181">Run hello sample app</span></span>
<span data-ttu-id="5f908-182">Por último, compile y ejecute el ejemplo hello.</span><span class="sxs-lookup"><span data-stu-id="5f908-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="5f908-183">Registrarse para la aplicación hello usando un nombre de usuario o la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="5f908-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="5f908-184">Cerrar sesión e iniciar sesión en como Hola mismo usuario.</span><span class="sxs-lookup"><span data-stu-id="5f908-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="5f908-185">Edite el perfil de ese usuario.</span><span class="sxs-lookup"><span data-stu-id="5f908-185">Edit that user's profile.</span></span> <span data-ttu-id="5f908-186">Cierre la sesión y regístrese con otro usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="5f908-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="5f908-187">Agregar IDP sociales</span><span class="sxs-lookup"><span data-stu-id="5f908-187">Add social IDPs</span></span>
<span data-ttu-id="5f908-188">Actualmente, la aplicación hello admite solo inicio de sesión de usuario e inicio de sesión que usan **cuentas locales**.</span><span class="sxs-lookup"><span data-stu-id="5f908-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="5f908-189">Se trata de cuentas almacenadas en el directorio B2C que utilizan un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="5f908-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="5f908-190">Con Azure AD B2C, puede agregar compatibilidad con otros proveedores de identidades (IDP) sin cambiar el código.</span><span class="sxs-lookup"><span data-stu-id="5f908-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="5f908-191">tooadd sociales IDPs tooyour aplicación, para comenzar, siga Hola detallada instrucciones que aparecen en estos artículos.</span><span class="sxs-lookup"><span data-stu-id="5f908-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="5f908-192">Para cada IDP desea toosupport, necesita tooregister una aplicación en ese sistema y obtener un identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="5f908-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="5f908-193">Configurar Facebook como una IDP</span><span class="sxs-lookup"><span data-stu-id="5f908-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="5f908-194">Configurar Google como una IDP</span><span class="sxs-lookup"><span data-stu-id="5f908-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="5f908-195">Configurar Amazon como una IDP</span><span class="sxs-lookup"><span data-stu-id="5f908-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="5f908-196">Configurar LinkedIn como una IDP</span><span class="sxs-lookup"><span data-stu-id="5f908-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="5f908-197">Después de Agregar directorio de tooyour B2C de proveedores de identidad de hello, necesita tooedit cada una de las tres directivas tooinclude Hola IDPs nuevas, como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5f908-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5f908-198">Después de guardar las directivas, vuelva a ejecutar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5f908-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="5f908-199">Debería ver Hola que IDPS nueva se agregan como opciones de inicio de sesión y suscripción en cada una de sus experiencias de identidad.</span><span class="sxs-lookup"><span data-stu-id="5f908-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="5f908-200">Puede experimentar con las directivas y observar los efectos de hello en la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5f908-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="5f908-201">Agregue o quite proveedores de identidades, manipule notificaciones de aplicación o cambie atributos de registro.</span><span class="sxs-lookup"><span data-stu-id="5f908-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="5f908-202">Experimente para ver cómo se combinan directivas, solicitudes de autenticación y MSAL.</span><span class="sxs-lookup"><span data-stu-id="5f908-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="5f908-203">Como referencia, Hola completado ejemplo [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5f908-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="5f908-204">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="5f908-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
