---
title: "aplicación de plataforma Universal de Windows (UWP) de aaaAdd authentication tooyour | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de Azure aplicación servicio de la aplicación de plataforma Universal de Windows (UWP) mediante una variedad de proveedores de identidad, incluido: AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="eb3bc-103">Agregar aplicación de Windows de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="eb3bc-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="eb3bc-104">Este tema muestra cómo tooyour de autenticación basada en la nube tooadd aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="eb3bc-105">En este tutorial, agregará un proyecto de inicio rápido de autenticación toohello plataforma Universal de Windows (UWP) para las aplicaciones móviles utilizando un proveedor de identidad que es compatible con el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="eb3bc-106">Después de que se va a correctamente autenticados y autorizados por el aplicación móvil de back-end, se muestra el valor de identificador de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="eb3bc-107">Este tutorial se basa en Inicio rápido de aplicaciones móviles de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="eb3bc-108">Primero debe completar el tutorial de hello [empezar a trabajar con aplicaciones móviles](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb3bc-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="eb3bc-109"><a name="register"></a>Registrar la aplicación para la autenticación y configurar Hola servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="eb3bc-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="eb3bc-110"><a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="eb3bc-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="eb3bc-111">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="eb3bc-112">Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="eb3bc-113">En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="eb3bc-114">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="eb3bc-115">Debe ser único tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="eb3bc-116">redirección de hello tooenable en servidor hello:</span><span class="sxs-lookup"><span data-stu-id="eb3bc-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="eb3bc-117">Hola [portal de Azure], seleccione su servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="eb3bc-118">Haga clic en hello **autenticación / autorización** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="eb3bc-119">Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="eb3bc-120">Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="eb3bc-121">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="eb3bc-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="eb3bc-122">Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="eb3bc-123">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-123">Click **OK**.</span></span>

5. <span data-ttu-id="eb3bc-124">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-124">Click **Save**.</span></span>

## <span data-ttu-id="eb3bc-125"><a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="eb3bc-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="eb3bc-126">Ahora, puede comprobar que tooyour el acceso anónimo, back-end se ha deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="eb3bc-127">Con proyecto de aplicación UWP de hello establecer como proyecto de inicio de hello, implementar y ejecutar la aplicación hello; Compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="eb3bc-128">Esto sucede porque la aplicación hello intenta tooaccess código de la aplicación móvil como un usuario no autenticado, pero Hola *TodoItem* tabla ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="eb3bc-129">A continuación, se actualizará a los usuarios de hello aplicación tooauthenticate antes de solicitar recursos de su servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="eb3bc-130"><a name="add-authentication"></a>Agregar aplicación de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="eb3bc-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="eb3bc-131">En el proyecto de aplicación UWP Hola archivo MainPage.xaml.cs y agregue Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="eb3bc-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="eb3bc-132">Este código autentica el usuario Hola con un inicio de sesión de Facebook.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="eb3bc-133">Si está utilizando un proveedor de identidades distinto a Facebook, cambie el valor de Hola de **MobileServiceAuthenticationProvider** anteriormente toohello valor para el proveedor.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="eb3bc-134">Reemplace hello **OnNavigatedTo()** método en MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="eb3bc-135">A continuación, agregará un **iniciar sesión en** aplicación toohello de botón que desencadena la autenticación.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="eb3bc-136">Agregue Hola siguiente fragmento de código toohello MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="eb3bc-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="eb3bc-137">Abrir archivo de proyecto de MainPage.xaml hello, busque el elemento Hola que define hello **guardar** botón y reemplazarlo con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="eb3bc-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="eb3bc-138">Agregue Hola después toohello de fragmento de código App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="eb3bc-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="eb3bc-139">Abra el archivo Package.appxmanifest, navegue demasiado**declaraciones**, en **declaraciones disponibles** lista desplegable, seleccione **protocolo** y haga clic en **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="eb3bc-140">Configurar ahora hello **propiedades** de hello **protocolo** declaración.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="eb3bc-141">En **nombre para mostrar**, agregue nombre hello desea toodisplay toousers de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="eb3bc-142">En **Nombre**, agregue el {esquema_de_dirección_URL_de_la_aplicación}.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="eb3bc-143">Presione aplicación Hola de hello F5 toorun clave, haga clic en hello **iniciar sesión en** botón e inicie sesión en la aplicación hello con su proveedor de identidades elegido.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="eb3bc-144">Una vez en el inicio de sesión correctamente, aplicación hello se ejecuta sin errores y es capaz de tooquery el back-end y realizar actualizaciones toodata.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="eb3bc-145"><a name="tokens"></a>Almacenar el token de autenticación de hello en cliente hello</span><span class="sxs-lookup"><span data-stu-id="eb3bc-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="eb3bc-146">ejemplo anterior de Hola mostrada un estándar inicio de sesión de, lo que requiere Hola cliente toocontact ambos proveedor de identidades de Hola y Hola servicio de aplicación cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="eb3bc-147">No sólo es ineficaz, puede ejecutar este método en uso-está relacionada con problemas de muchos clientes pruebe toostart aplicación hello en el mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="eb3bc-148">Un enfoque más adecuado es toocache Hola autorización token devuelto por el servicio de aplicaciones y try toouse esto antes de utilizar un inicio de sesión de basada en el proveedor.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="eb3bc-149">Puede almacenar en caché símbolo (token) de hello emitido por servicios de aplicaciones independientemente de si está usando autenticación administrada por el cliente o servicio.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="eb3bc-150">Este tutorial utiliza la autenticación administrada por el servicio.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="eb3bc-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb3bc-151">Next steps</span></span>
<span data-ttu-id="eb3bc-152">Completado este tutorial de la autenticación básica, considere la posibilidad de continuar en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="eb3bc-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="eb3bc-153">Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="eb3bc-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="eb3bc-154">Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de toosend de aplicación móvil back-end toouse centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="eb3bc-155">Habilitación de la sincronización sin conexión para su aplicación</span><span class="sxs-lookup"><span data-stu-id="eb3bc-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="eb3bc-156">Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="eb3bc-157">Sincronización sin conexión permite a los usuarios finales toointeract con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="eb3bc-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
