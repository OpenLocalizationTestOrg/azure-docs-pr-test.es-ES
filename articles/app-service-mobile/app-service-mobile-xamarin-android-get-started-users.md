---
title: "Introducción a la autenticación de Aplicaciones móviles en Xamarin Android"
description: "Obtenga información acerca de cómo utilizar Aplicaciones móviles para autenticar usuarios de su aplicación Xamarin Android a través de una variedad de proveedores de identidad, incluidos AAD, Google, Facebook, Twitter y Microsoft."
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
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="e4f3b-103">Adición de la autenticación a la aplicación Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="e4f3b-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="e4f3b-104">En este tema se muestra cómo autenticar usuarios de una aplicación móvil desde la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="e4f3b-105">En este tutorial podrá agregar la autenticación al proyecto de inicio rápido mediante un proveedor de identidades compatible con Aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="e4f3b-106">Una vez que la aplicación móvil finalice la autenticación y autorización correctamente, se mostrará el valor del identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="e4f3b-107">Este tutorial se basa en el inicio rápido de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="e4f3b-108">Primero debe completar el tutorial [Creación de una aplicación Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="e4f3b-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="e4f3b-109">Si no usa el proyecto de servidor de inicio rápido descargado, debe agregar el paquete de extensión de autenticación al proyecto.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="e4f3b-110">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [Trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e4f3b-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="e4f3b-111"><a name="register"></a>Registro de la aplicación para la autenticación y configuración de Servicios de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e4f3b-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="e4f3b-112"><a name="redirecturl"></a>Adición de la aplicación a las direcciones URL de redirección externa permitidas</span><span class="sxs-lookup"><span data-stu-id="e4f3b-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="e4f3b-113">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e4f3b-114">Esto permite que el sistema de autenticación se redirija a la aplicación una vez completado el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="e4f3b-115">En este tutorial, se usará el esquema de dirección URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e4f3b-116">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e4f3b-117">Debe ser único para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="e4f3b-118">Para habilitar la redirección en el lado de servidor:</span><span class="sxs-lookup"><span data-stu-id="e4f3b-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="e4f3b-119">En [Azure Portal], seleccione App Service.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e4f3b-120">Haga clic en la opción de menú **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e4f3b-121">En **URL de redirección externas permitidas**, introduzca `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e4f3b-122">El valor de **esquema_de_dirección_URL_de_la_aplicación** de esta cadena es el esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e4f3b-123">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="e4f3b-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e4f3b-124">Debe tomar nota de la cadena que elija ya que necesitará ajustar el código de la aplicación móvil con el esquema de direcciones URL en varios sitios.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="e4f3b-125">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-125">Click **OK**.</span></span>

5. <span data-ttu-id="e4f3b-126">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-126">Click **Save**.</span></span>

## <span data-ttu-id="e4f3b-127"><a name="permissions"></a>Restricción de los permisos para los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="e4f3b-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="e4f3b-128">En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente en un dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="e4f3b-129">Compruebe que se produce una excepción no controlada con el código de estado 401 (No autorizado) después de iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e4f3b-130">Esto sucede porque la aplicación intenta obtener acceso al back-end de la aplicación móvil como usuario sin autenticar.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="e4f3b-131">La tabla *TodoItem* ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="e4f3b-132">Luego, actualizará la aplicación cliente para solicitar recursos del back-end de la aplicación móvil con un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="e4f3b-133"><a name="add-authentication"></a>Incorporación de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="e4f3b-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="e4f3b-134">La aplicación se actualiza para requerir a los usuarios que pulsen el botón **Iniciar sesión** y que se autentiquen para que se muestren los datos.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="e4f3b-135">Agregue el siguiente código a la clase **TodoActivity** :</span><span class="sxs-lookup"><span data-stu-id="e4f3b-135">Add the following code to the **TodoActivity** class:</span></span>
   
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
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="e4f3b-136">Esto crea un método nuevo para autenticar un usuario y un controlador de método para un nuevo botón **Iniciar sesión** .</span><span class="sxs-lookup"><span data-stu-id="e4f3b-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="e4f3b-137">El usuario del código de ejemplo anterior se autentica mediante el inicio de sesión en Facebook.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="e4f3b-138">Se usa un cuadro de diálogo para mostrar el identificador de usuario una vez autenticado.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4f3b-139">Si usa un proveedor de identidades que no sea una cuenta de Facebook, cambie el valor que usó con **LoginAsync** por uno de los siguientes: *MicrosoftAccount*, *Twitter*, *Google* o *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="e4f3b-140">En el método **OnCreate** , elimine o convierta en comentario la siguiente línea de código:</span><span class="sxs-lookup"><span data-stu-id="e4f3b-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="e4f3b-141">En el archivo Activity_To_Do.axml, agregue la siguiente definición del botón *LoginUser* antes del botón *AddItem* existente:</span><span class="sxs-lookup"><span data-stu-id="e4f3b-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="e4f3b-142">Agregue el siguiente elemento al archivo de recursos Strings.xml:</span><span class="sxs-lookup"><span data-stu-id="e4f3b-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="e4f3b-143">Abra el archivo AndroidManifest.xml, agregue el código siguiente dentro del elemento XML `<application>`:</span><span class="sxs-lookup"><span data-stu-id="e4f3b-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="e4f3b-144">En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente en un dispositivo o emulador, e inicie sesión con el proveedor de identidades elegido.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="e4f3b-145">Una vez iniciada la sesión correctamente, la aplicación mostrará el identificador de inicio de sesión y la lista de tareas pendientes, y podrá realizar actualizaciones en los datos.</span><span class="sxs-lookup"><span data-stu-id="e4f3b-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="e4f3b-146">[Creación de una aplicación Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="e4f3b-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>