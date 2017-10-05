---
title: "Incorporación de autenticación en iOS con Aplicaciones móviles de Azure"
description: "Obtenga información acerca de cómo usar las Aplicaciones móviles de Azure para autenticar a los usuarios de su aplicación iOS en una variedad de proveedores de identidades, incluidos AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="7e832-103">Incorporación de la autenticación a la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="7e832-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="7e832-104">En este tutorial podrá agregar la autenticación al proyecto de [inicio rápido de iOS] mediante un proveedor de identidades compatible.</span><span class="sxs-lookup"><span data-stu-id="7e832-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="7e832-105">Este tutorial está basado en el tutorial de [inicio rápido de iOS] , que debe completar primero.</span><span class="sxs-lookup"><span data-stu-id="7e832-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="7e832-106"><a name="register"></a>Registro de la aplicación para la autenticación y configuración del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7e832-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="7e832-107"><a name="redirecturl"></a>Adición de la aplicación a las direcciones URL de redirección externa permitidas</span><span class="sxs-lookup"><span data-stu-id="7e832-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="7e832-108">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e832-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="7e832-109">Esto permite que el sistema de autenticación se redirija a la aplicación una vez completado el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7e832-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="7e832-110">En este tutorial, se usará el esquema de dirección URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="7e832-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="7e832-111">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="7e832-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="7e832-112">Debe ser único para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="7e832-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="7e832-113">Para habilitar la redirección en el lado de servidor:</span><span class="sxs-lookup"><span data-stu-id="7e832-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="7e832-114">En [Azure Portal], seleccione el servicio App Service.</span><span class="sxs-lookup"><span data-stu-id="7e832-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="7e832-115">Haga clic en la opción de menú **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="7e832-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="7e832-116">Haga clic en **Azure Active Directory** en la sección **Proveedores de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="7e832-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="7e832-117">Establezca el **modo de administración** en **Avanzado**.</span><span class="sxs-lookup"><span data-stu-id="7e832-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="7e832-118">En **URL de redirección externas permitidas**, introduzca `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="7e832-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="7e832-119">El valor de _appname_ de esta cadena es el esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="7e832-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="7e832-120">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="7e832-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="7e832-121">Debe tomar nota de la cadena que elija ya que necesitará ajustar el código de la aplicación móvil con el esquema de direcciones URL en varios sitios.</span><span class="sxs-lookup"><span data-stu-id="7e832-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="7e832-122">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7e832-122">Click **OK**.</span></span>

7. <span data-ttu-id="7e832-123">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="7e832-123">Click **Save**.</span></span>

## <span data-ttu-id="7e832-124"><a name="permissions"></a>Restricción de los permisos para los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="7e832-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="7e832-125">En Xcode, presione **Ejecutar** para iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e832-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="7e832-126">Se genera una excepción porque la aplicación intenta acceder al back-end como usuario sin autenticar, pero la tabla *TodoItem* ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="7e832-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="7e832-127"><a name="add-authentication"></a>Incorporación de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="7e832-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="7e832-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7e832-128">**Objective-C**:</span></span>

1. <span data-ttu-id="7e832-129">En el Mac, abra *QSTodoListViewController.m* en Xcode y agregue el siguiente método:</span><span class="sxs-lookup"><span data-stu-id="7e832-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="7e832-130">Cambie *google* a *microsoftaccount*, *twitter*, *facebook* o *windowsazureactivedirectory* si no usa Google como su proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="7e832-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="7e832-131">Si utiliza Facebook, debe [incluir los dominios de Facebook en la lista blanca][1] en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e832-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="7e832-132">Reemplace **urlScheme** por un nombre único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e832-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="7e832-133">El valor de urlScheme debe ser el mismo que el protocolo de esquema de dirección URL que especificó en el campo **URL de redirección externas permitidas** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7e832-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="7e832-134">urlScheme se utiliza en la devolución de llamada de autenticación para volver a la aplicación una vez completada la solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7e832-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="7e832-135">Reemplace `[self refresh]` en `viewDidLoad` en *QSTodoListViewController.m* por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e832-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="7e832-136">Abra el archivo `QSAppDelegate.h` y agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e832-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="7e832-137">Abra el archivo `QSAppDelegate.m` y agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e832-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="7e832-138">Agregue este código directamente antes de la línea `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="7e832-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="7e832-139">Reemplace el valor de _appname_ por valor de urlScheme que utilizó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="7e832-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="7e832-140">Abra el archivo `AppName-Info.plist` (reemplazando AppName por el nombre de la aplicación) y agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e832-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="7e832-141">Este código debe colocarse dentro del elemento `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="7e832-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="7e832-142">Reemplace la cadena _appname_ (dentro de la matriz de **CFBundleURLSchemes**) por el nombre de la aplicación que eligió en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="7e832-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="7e832-143">También puede realizar estos cambios en el editor plist; haga clic en el archivo `AppName-Info.plist` en XCode para abrir el editor de plist.</span><span class="sxs-lookup"><span data-stu-id="7e832-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="7e832-144">Reemplace la cadena `com.microsoft.azure.zumo` de **CFBundleURLName** por el identificador del grupo Apple.</span><span class="sxs-lookup"><span data-stu-id="7e832-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="7e832-145">Presione *Ejecutar* para iniciar la aplicación y, después, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7e832-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="7e832-146">Una vez que haya iniciado sesión, debería poder ver la lista de tareas pendientes y realizar actualizaciones en ella.</span><span class="sxs-lookup"><span data-stu-id="7e832-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="7e832-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="7e832-147">**Swift**:</span></span>

1. <span data-ttu-id="7e832-148">En el Mac, abra *ToDoTableViewController.swift* en Xcode y agregue el siguiente método:</span><span class="sxs-lookup"><span data-stu-id="7e832-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="7e832-149">Cambie *google* a *microsoftaccount*, *twitter*, *facebook* o *windowsazureactivedirectory* si no usa Google como su proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="7e832-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="7e832-150">Si utiliza Facebook, debe [incluir los dominios de Facebook en la lista blanca][1] en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e832-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="7e832-151">Reemplace **urlScheme** por un nombre único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e832-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="7e832-152">El valor de urlScheme debe ser el mismo que el protocolo de esquema de dirección URL que especificó en el campo **URL de redirección externas permitidas** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7e832-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="7e832-153">urlScheme se utiliza en la devolución de llamada de autenticación para volver a la aplicación una vez completada la solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7e832-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="7e832-154">Quite las líneas `self.refreshControl?.beginRefreshing()` y `self.onRefresh(self.refreshControl)` al final de `viewDidLoad()` en *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="7e832-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="7e832-155">Agregue una llamada a `loginAndGetData()` en su lugar:</span><span class="sxs-lookup"><span data-stu-id="7e832-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="7e832-156">Abra el archivo `AppDelegate.swift` y agregue la siguiente línea a la clase `AppDelegate`:</span><span class="sxs-lookup"><span data-stu-id="7e832-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="7e832-157">Reemplace el valor de _appname_ por valor de urlScheme que utilizó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="7e832-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="7e832-158">Abra el archivo `AppName-Info.plist` (reemplazando AppName por el nombre de la aplicación) y agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e832-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="7e832-159">Este código debe colocarse dentro del elemento `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="7e832-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="7e832-160">Reemplace la cadena _appname_ (dentro de la matriz de **CFBundleURLSchemes**) por el nombre de la aplicación que eligió en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="7e832-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="7e832-161">También puede realizar estos cambios en el editor plist; haga clic en el archivo `AppName-Info.plist` en XCode para abrir el editor de plist.</span><span class="sxs-lookup"><span data-stu-id="7e832-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="7e832-162">Reemplace la cadena `com.microsoft.azure.zumo` de **CFBundleURLName** por el identificador del grupo Apple.</span><span class="sxs-lookup"><span data-stu-id="7e832-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="7e832-163">Presione *Ejecutar* para iniciar la aplicación y, después, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7e832-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="7e832-164">Una vez que haya iniciado sesión, debería poder ver la lista de tareas pendientes y realizar actualizaciones en ella.</span><span class="sxs-lookup"><span data-stu-id="7e832-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="7e832-165">La autenticación de App Service utiliza Apple Inter-App Communication.</span><span class="sxs-lookup"><span data-stu-id="7e832-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="7e832-166">Para más detalles sobre este tema, consulte la [documentación de Apple][2].</span><span class="sxs-lookup"><span data-stu-id="7e832-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="7e832-167">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7e832-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="7e832-168">[inicio rápido de iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="7e832-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

