---
title: "Incorporación de autenticación a una aplicación de la Plataforma universal de Windows (UWP) | Microsoft Docs"
description: "Obtenga información acerca de cómo usar Aplicaciones móviles del Servicio de aplicaciones de Azure para autenticar a los usuarios de la aplicación de la Plataforma universal de Windows (UWP) en una variedad de proveedores de identidades, incluidos AAD,Google, Facebook, Twitter y Microsoft."
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
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="9b297-103">Incorporación de la autenticación a la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="9b297-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="9b297-104">En este tema se muestra cómo agregar la autenticación basada en la nube a su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="9b297-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="9b297-105">En este tutorial podrá agregar la autenticación al proyecto de inicio rápido de la Plataforma universal de Windows (UWP) para Aplicaciones móviles mediante un proveedor de identidades compatible con el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b297-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="9b297-106">Una vez que el back-end de la aplicación móvil haya realizado la autenticación y autorización correctamente, se mostrará el valor de identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="9b297-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="9b297-107">Este tutorial se basa en el inicio rápido de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="9b297-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="9b297-108">Primero debe completar el tutorial [Introducción a las aplicaciones móviles](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b297-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="9b297-109"><a name="register"></a>Registro de la aplicación para la autenticación y configuración del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9b297-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="9b297-110"><a name="redirecturl"></a>Adición de la aplicación a las direcciones URL de redirección externa permitidas</span><span class="sxs-lookup"><span data-stu-id="9b297-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="9b297-111">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b297-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="9b297-112">Esto permite que el sistema de autenticación se redirija a la aplicación una vez completado el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="9b297-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="9b297-113">En este tutorial, se usará el esquema de dirección URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="9b297-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="9b297-114">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="9b297-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="9b297-115">Debe ser único para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="9b297-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="9b297-116">Para habilitar la redirección en el lado de servidor:</span><span class="sxs-lookup"><span data-stu-id="9b297-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="9b297-117">En [Azure Portal], seleccione App Service.</span><span class="sxs-lookup"><span data-stu-id="9b297-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="9b297-118">Haga clic en la opción de menú **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="9b297-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="9b297-119">En **URL de redirección externas permitidas**, introduzca `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="9b297-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="9b297-120">El valor de **esquema_de_dirección_URL_de_la_aplicación** de esta cadena es el esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="9b297-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="9b297-121">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="9b297-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="9b297-122">Debe tomar nota de la cadena que elija ya que necesitará ajustar el código de la aplicación móvil con el esquema de direcciones URL en varios sitios.</span><span class="sxs-lookup"><span data-stu-id="9b297-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="9b297-123">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9b297-123">Click **OK**.</span></span>

5. <span data-ttu-id="9b297-124">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="9b297-124">Click **Save**.</span></span>

## <span data-ttu-id="9b297-125"><a name="permissions"></a>Restricción de los permisos para los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="9b297-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="9b297-126">Ahora, puede comprobar que se deshabilitó el acceso anónimo a su back-end.</span><span class="sxs-lookup"><span data-stu-id="9b297-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="9b297-127">Con el proyecto de aplicación para UWP configurado como proyecto de inicio, implemente y ejecute la aplicación; compruebe que, cuando esta se inicia, se genera una excepción no controlada con el código de estado 401 (No autorizado).</span><span class="sxs-lookup"><span data-stu-id="9b297-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="9b297-128">Esto se produce porque la aplicación intenta obtener acceso a su Código de aplicación móvil como usuario sin autenticar, pero la tabla *TodoItem* requiere ahora autenticación.</span><span class="sxs-lookup"><span data-stu-id="9b297-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="9b297-129">A continuación, actualizará la aplicación para autenticar usuarios antes de solicitar recursos del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b297-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="9b297-130"><a name="add-authentication"></a>Incorporación de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="9b297-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="9b297-131">En el archivo de proyecto de aplicación para UWP MainPage.xaml.cs, agregue el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="9b297-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="9b297-132">Este código autentica al usuario con un inicio de sesión de Facebook.</span><span class="sxs-lookup"><span data-stu-id="9b297-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="9b297-133">Si está usando un proveedor de identidades diferente al de Facebook, cambie el valor de **MobileServiceAuthenticationProvider** anterior por el valor de su proveedor.</span><span class="sxs-lookup"><span data-stu-id="9b297-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="9b297-134">Reemplace el método **OnNavigatedTo()** en MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="9b297-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="9b297-135">A continuación, agregará un botón **Iniciar sesión** a la aplicación que desencadena la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9b297-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="9b297-136">Agregue el siguiente fragmento de código a MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="9b297-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="9b297-137">Abra el archivo de proyecto MainPage.xaml, busque el elemento que define el botón **Guardar** y reemplácelo por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b297-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="9b297-138">Agregue el siguiente fragmento de código a App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="9b297-138">Add the following code snippet to the App.xaml.cs:</span></span>

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
6. <span data-ttu-id="9b297-139">Abra el archivo Package.appxmanifest, vaya a **Declaraciones**, en la lista desplegable **Declaraciones disponibles** seleccione **Protocolo** y haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9b297-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="9b297-140">Configure ahora las **Propiedades** de la declaración **Protocolo**.</span><span class="sxs-lookup"><span data-stu-id="9b297-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="9b297-141">En **Nombre para mostrar**, agregue el nombre que quiere mostrar a los usuarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b297-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="9b297-142">En **Nombre**, agregue el {esquema_de_dirección_URL_de_la_aplicación}.</span><span class="sxs-lookup"><span data-stu-id="9b297-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="9b297-143">Presione la tecla F5 para ejecutar la aplicación, haga clic en el botón **Iniciar sesión** e inicie sesión en la aplicación con el proveedor de identidad que haya elegido.</span><span class="sxs-lookup"><span data-stu-id="9b297-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="9b297-144">Una vez iniciada la sesión correctamente, la aplicación se ejecutará sin errores y podrá consultar al back-end y realizar actualizaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="9b297-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="9b297-145"><a name="tokens"></a>Almacenamiento del token de autorización en el cliente</span><span class="sxs-lookup"><span data-stu-id="9b297-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="9b297-146">En el ejemplo anterior se mostró un inicio de sesión estándar, que requiere que el cliente se ponga en contacto con el proveedor de identidades y con el servicio de la aplicación cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b297-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="9b297-147">Este método no solo es ineficaz, sino que también puede enfrentarse a problemas relacionados con el uso si varios clientes inician la aplicación al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9b297-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="9b297-148">Un método mejor es almacenar en caché el token de autorización devuelto por su servicio de aplicación e intentar usarlo primero antes de utilizar un inicio de sesión basado en proveedores.</span><span class="sxs-lookup"><span data-stu-id="9b297-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="9b297-149">Puede almacenar en caché el token emitido por los servicios de aplicaciones con independencia de si es una autenticación administrada por el cliente o por el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b297-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="9b297-150">Este tutorial utiliza la autenticación administrada por el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b297-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="9b297-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b297-151">Next steps</span></span>
<span data-ttu-id="9b297-152">Ahora que ha completado este tutorial de autenticación básica, considere la posibilidad de continuar con uno de los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="9b297-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="9b297-153">Incorporación de notificaciones push a su aplicación</span><span class="sxs-lookup"><span data-stu-id="9b297-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="9b297-154">: aprenda a agregar a la aplicación compatibilidad con notificaciones push y a configurar su back-end de aplicación móvil para usar Azure Notification Hubs para enviar notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="9b297-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="9b297-155">Habilitación de la sincronización sin conexión para su aplicación</span><span class="sxs-lookup"><span data-stu-id="9b297-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="9b297-156">: aprenda a agregar compatibilidad sin conexión a su aplicación con un back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="9b297-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="9b297-157">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos) aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="9b297-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
