---
title: "aaaGet iniciado con autenticación para aplicaciones móviles en Xamarin para Android"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de la aplicación de Xamarin para Android a través de una serie de proveedores de identidad, incluido AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="7c749-103">Agregar aplicación de autenticación tooyour Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="7c749-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="7c749-104">Este tema muestra cómo tooauthenticate a los usuarios de una aplicación móvil de la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="7c749-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="7c749-105">En este tutorial, agregará el proyecto de inicio rápido de toohello de autenticación utilizando un proveedor de identidad que es compatible con aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c749-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="7c749-106">Después de que se va a correctamente autenticado y autorizado en hello aplicación móvil, se muestra el valor de identificador de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c749-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="7c749-107">Este tutorial se basa en Inicio rápido de aplicación móvil de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c749-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="7c749-108">En primer lugar también debe completar el tutorial Hola [crear una aplicación de Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="7c749-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="7c749-109">Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto de tooyour de paquete de extensión de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c749-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="7c749-110">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7c749-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="7c749-111"><a name="register"></a>Registro de la aplicación para la autenticación y configuración de Servicios de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7c749-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="7c749-112"><a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="7c749-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="7c749-113">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c749-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="7c749-114">Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c749-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="7c749-115">En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo.</span><span class="sxs-lookup"><span data-stu-id="7c749-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="7c749-116">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="7c749-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="7c749-117">Debe ser único tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="7c749-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="7c749-118">redirección de hello tooenable en servidor hello:</span><span class="sxs-lookup"><span data-stu-id="7c749-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="7c749-119">Hola [portal de Azure], seleccione su servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c749-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="7c749-120">Haga clic en hello **autenticación / autorización** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="7c749-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="7c749-121">Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="7c749-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="7c749-122">Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="7c749-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="7c749-123">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="7c749-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="7c749-124">Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="7c749-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="7c749-125">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7c749-125">Click **OK**.</span></span>

5. <span data-ttu-id="7c749-126">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7c749-126">Click **Save**.</span></span>

## <span data-ttu-id="7c749-127"><a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="7c749-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="7c749-128">En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente de hello en un dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="7c749-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="7c749-129">Compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7c749-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="7c749-130">Esto sucede porque la aplicación hello intenta tooaccess su aplicación móvil de back-end como un usuario no autenticado.</span><span class="sxs-lookup"><span data-stu-id="7c749-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="7c749-131">Hola *TodoItem* tabla ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="7c749-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="7c749-132">A continuación, actualizará recursos de toorequest Hola la aplicación cliente de aplicación móvil de hello back-end a un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="7c749-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="7c749-133"><a name="add-authentication"></a>Agregar aplicación de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="7c749-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="7c749-134">aplicación Hello es Hola de toorequire actualizada a los usuarios tootap **iniciar sesión en** botón y autenticarse antes de que se muestran los datos.</span><span class="sxs-lookup"><span data-stu-id="7c749-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="7c749-135">Agregar Hola después código toohello **TodoActivity** clase:</span><span class="sxs-lookup"><span data-stu-id="7c749-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="7c749-136">Esto crea un nuevo tooauthenticate método un usuario y un controlador de método para un nuevo **iniciar sesión en** botón.</span><span class="sxs-lookup"><span data-stu-id="7c749-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="7c749-137">usuario de Hello en el código de ejemplo de Hola anterior se autentica mediante un inicio de sesión de Facebook.</span><span class="sxs-lookup"><span data-stu-id="7c749-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="7c749-138">Un cuadro de diálogo es una vez autenticado, Id. de usuario de Hola de toodisplay usado.</span><span class="sxs-lookup"><span data-stu-id="7c749-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7c749-139">Si está utilizando un proveedor de identidades distinto a Facebook, cambie el valor de Hola que se pasan demasiado**LoginAsync** anteriormente tooone de siguientes hello: *cuenta de Microsoft*, *Twitter*, *Google*, o *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="7c749-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="7c749-140">Hola **OnCreate** (método), delete u Hola Comente después de la línea de código:</span><span class="sxs-lookup"><span data-stu-id="7c749-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="7c749-141">En el archivo de Activity_To_Do.axml hello, agregue siguientes de hello *LoginUser* botón definición antes de hello existente *AddItem* botón:</span><span class="sxs-lookup"><span data-stu-id="7c749-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="7c749-142">Agregue Hola elemento toohello Strings.xml recursos archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7c749-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="7c749-143">Abra el archivo AndroidManifest.xml Hola, agregue Hola siguiente código dentro de `<application>` elemento XML:</span><span class="sxs-lookup"><span data-stu-id="7c749-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="7c749-144">En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente de hello en un dispositivo o emulador e inicie sesión con su proveedor de identidades elegido.</span><span class="sxs-lookup"><span data-stu-id="7c749-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="7c749-145">Una vez que ha iniciado sesión correctamente, aplicación hello mostrará el identificador de inicio de sesión y lista de Hola de elementos de lista de tareas y realizar toohello una actualización de datos.</span><span class="sxs-lookup"><span data-stu-id="7c749-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[crear una aplicación de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md