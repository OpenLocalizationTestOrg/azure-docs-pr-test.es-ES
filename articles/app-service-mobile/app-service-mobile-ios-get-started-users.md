---
title: "aaaAdd autenticación en iOS con aplicaciones móviles de Azure"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de Azure de la aplicación de iOS a través de una serie de proveedores de identidad, incluido AAD, Google, Facebook, Twitter y Microsoft."
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
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="c8b17-103">Agregar aplicación de iOS de tooyour de autenticación</span><span class="sxs-lookup"><span data-stu-id="c8b17-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="c8b17-104">En este tutorial, agregará autenticación toohello [inicio rápido de iOS] proyecto utilizando un proveedor de identidades admitidos.</span><span class="sxs-lookup"><span data-stu-id="c8b17-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="c8b17-105">Este tutorial se basa en hello [inicio rápido de iOS] tutorial, que debe completar primero.</span><span class="sxs-lookup"><span data-stu-id="c8b17-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="c8b17-106"><a name="register"></a>Registrar la aplicación para la autenticación y configurar Hola servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c8b17-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="c8b17-107"><a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="c8b17-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="c8b17-108">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="c8b17-109">Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8b17-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="c8b17-110">En este tutorial, se usará el esquema de dirección URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="c8b17-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="c8b17-111">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="c8b17-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="c8b17-112">Debe ser único tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="c8b17-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="c8b17-113">redirección de hello tooenable en th servidor:</span><span class="sxs-lookup"><span data-stu-id="c8b17-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="c8b17-114">Hola [portal de Azure], seleccione el servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="c8b17-115">Haga clic en hello **autenticación / autorización** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="c8b17-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="c8b17-116">Haga clic en **Azure Active Directory** en hello **proveedores de autenticación** sección.</span><span class="sxs-lookup"><span data-stu-id="c8b17-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="c8b17-117">Conjunto hello **modo de administración** demasiado**avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="c8b17-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="c8b17-118">Hola **permite redirigir direcciones URL externas de**, escriba `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="c8b17-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="c8b17-119">Hola _appname_ de esta cadena es hello esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8b17-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="c8b17-120">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="c8b17-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="c8b17-121">Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="c8b17-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="c8b17-122">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c8b17-122">Click **OK**.</span></span>

7. <span data-ttu-id="c8b17-123">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c8b17-123">Click **Save**.</span></span>

## <span data-ttu-id="c8b17-124"><a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="c8b17-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="c8b17-125">En Xcode, presione **ejecutar** toostart Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="c8b17-126">Se produce una excepción porque la aplicación hello intenta tooaccess el back-end como un usuario no autenticado, pero Hola *TodoItem* tabla ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="c8b17-127"><a name="add-authentication"></a>Agregar autenticación tooapp</span><span class="sxs-lookup"><span data-stu-id="c8b17-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="c8b17-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="c8b17-128">**Objective-C**:</span></span>

1. <span data-ttu-id="c8b17-129">En el equipo Mac, abra *QSTodoListViewController.m* en Xcode y agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="c8b17-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="c8b17-130">Cambio *google* demasiado*cuenta de Microsoft*, *twitter*, *facebook*, o *windowsazureactivedirectory* si no usas Google como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="c8b17-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="c8b17-131">Si utiliza Facebook, debe [incluir los dominios de Facebook en la lista blanca][1] en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="c8b17-132">Reemplace hello **urlScheme** con un nombre único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="c8b17-133">Hola urlScheme debe ser Hola igual como protocolo de esquema de dirección URL que especificó en Hola Hola **permite redirigir direcciones URL externas de** campo Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b17-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="c8b17-134">Hola autenticación devolución de llamada tooswitch tooyour atrás aplicación usa Hello urlScheme una vez completada la solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="c8b17-135">Reemplace `[self refresh]` en `viewDidLoad` en *QSTodoListViewController.m* con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="c8b17-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="c8b17-136">Abra hello `QSAppDelegate.h` de archivos y agregar el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c8b17-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="c8b17-137">Abra hello `QSAppDelegate.m` de archivos y agregar el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c8b17-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

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

   <span data-ttu-id="c8b17-138">Agregue este código directamente antes de la lectura de la línea de hello `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="c8b17-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="c8b17-139">Reemplace el _appname_ urlScheme valor invocando Hola utilizado en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="c8b17-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="c8b17-140">Abra hello `AppName-Info.plist` archivo (AppName reemplace con el nombre de saludo de la aplicación) y agregar el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c8b17-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="c8b17-141">Este código debe colocarse dentro de hello `<dict>` elemento.</span><span class="sxs-lookup"><span data-stu-id="c8b17-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="c8b17-142">Reemplace hello _appname_ cadena (dentro de la matriz para **CFBundleURLSchemes**) con el nombre de la aplicación hello que eligió en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="c8b17-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="c8b17-143">También puede realizar estos cambios en hello plist editor - haga clic en hello `AppName-Info.plist` archivo en XCode tooopen hello plist editor.</span><span class="sxs-lookup"><span data-stu-id="c8b17-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="c8b17-144">Reemplace hello `com.microsoft.azure.zumo` de cadena de **CFBundleURLName** con su equipo Apple agrupar identificador.</span><span class="sxs-lookup"><span data-stu-id="c8b17-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="c8b17-145">Presione *ejecutar* toostart Hola aplicación y, a continuación, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="c8b17-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="c8b17-146">Cuando haya iniciado sesión, debe estar lista de tareas de tooview capaz de Hola y realizar actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c8b17-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="c8b17-147">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="c8b17-147">**Swift**:</span></span>

1. <span data-ttu-id="c8b17-148">En el equipo Mac, abra *ToDoTableViewController.swift* en Xcode y agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="c8b17-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="c8b17-149">Cambio *google* demasiado*cuenta de Microsoft*, *twitter*, *facebook*, o *windowsazureactivedirectory* si no usas Google como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="c8b17-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="c8b17-150">Si utiliza Facebook, debe [incluir los dominios de Facebook en la lista blanca][1] en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="c8b17-151">Reemplace hello **urlScheme** con un nombre único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="c8b17-152">Hola urlScheme debe ser Hola igual como protocolo de esquema de dirección URL que especificó en Hola Hola **permite redirigir direcciones URL externas de** campo Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b17-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="c8b17-153">Hola autenticación devolución de llamada tooswitch tooyour atrás aplicación usa Hello urlScheme una vez completada la solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c8b17-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="c8b17-154">Quitar líneas de hello `self.refreshControl?.beginRefreshing()` y `self.onRefresh(self.refreshControl)` al final de `viewDidLoad()` en *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="c8b17-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="c8b17-155">Agregue una llamada demasiado`loginAndGetData()` en su lugar:</span><span class="sxs-lookup"><span data-stu-id="c8b17-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="c8b17-156">Abra hello `AppDelegate.swift` de archivos y agregar Hola después línea toohello `AppDelegate` clase:</span><span class="sxs-lookup"><span data-stu-id="c8b17-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

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

    <span data-ttu-id="c8b17-157">Reemplace hello _appname_ urlScheme valor invocando Hola utilizado en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="c8b17-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="c8b17-158">Abra hello `AppName-Info.plist` archivo (AppName reemplace con el nombre de saludo de la aplicación) y agregar el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c8b17-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="c8b17-159">Este código debe colocarse dentro de hello `<dict>` elemento.</span><span class="sxs-lookup"><span data-stu-id="c8b17-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="c8b17-160">Reemplace hello _appname_ cadena (dentro de la matriz para **CFBundleURLSchemes**) con el nombre de la aplicación hello que eligió en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="c8b17-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="c8b17-161">También puede realizar estos cambios en hello plist editor - haga clic en hello `AppName-Info.plist` archivo en XCode tooopen hello plist editor.</span><span class="sxs-lookup"><span data-stu-id="c8b17-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="c8b17-162">Reemplace hello `com.microsoft.azure.zumo` de cadena de **CFBundleURLName** con su equipo Apple agrupar identificador.</span><span class="sxs-lookup"><span data-stu-id="c8b17-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="c8b17-163">Presione *ejecutar* toostart Hola aplicación y, a continuación, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="c8b17-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="c8b17-164">Cuando haya iniciado sesión, debe estar lista de tareas de tooview capaz de Hola y realizar actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c8b17-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="c8b17-165">La autenticación de App Service utiliza Apple Inter-App Communication.</span><span class="sxs-lookup"><span data-stu-id="c8b17-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="c8b17-166">Para obtener más detalles sobre este tema, consulte toohello [documentación de Apple][2]</span><span class="sxs-lookup"><span data-stu-id="c8b17-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portal de Azure]: https://portal.azure.com

[inicio rápido de iOS]: app-service-mobile-ios-get-started.md

