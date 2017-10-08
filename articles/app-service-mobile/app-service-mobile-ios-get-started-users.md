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
# <a name="add-authentication-tooyour-ios-app"></a>Agregar aplicación de iOS de tooyour de autenticación
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

En este tutorial, agregará autenticación toohello [inicio rápido de iOS] proyecto utilizando un proveedor de identidades admitidos. Este tutorial se basa en hello [inicio rápido de iOS] tutorial, que debe completar primero.

## <a name="register"></a>Registrar la aplicación para la autenticación y configurar Hola servicio de aplicaciones
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello

La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.  Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.  En este tutorial, se usará el esquema de dirección URL _appname_.  Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.  Debe ser único tooyour aplicaciones móviles.  redirección de hello tooenable en th servidor:

1. Hola [portal de Azure], seleccione el servicio de aplicación.

2. Haga clic en hello **autenticación / autorización** opción de menú.

3. Haga clic en **Azure Active Directory** en hello **proveedores de autenticación** sección.

4. Conjunto hello **modo de administración** demasiado**avanzadas**.

5. Hola **permite redirigir direcciones URL externas de**, escriba `appname://easyauth.callback`.  Hola _appname_ de esta cadena es hello esquema de dirección URL para la aplicación móvil.  Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).  Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.

6. Haga clic en **Aceptar**.

7. Haga clic en **Guardar**.

## <a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

En Xcode, presione **ejecutar** toostart Hola aplicación. Se produce una excepción porque la aplicación hello intenta tooaccess el back-end como un usuario no autenticado, pero Hola *TodoItem* tabla ahora requiere autenticación.

## <a name="add-authentication"></a>Agregar autenticación tooapp
**Objective-C**:

1. En el equipo Mac, abra *QSTodoListViewController.m* en Xcode y agregue Hola siguiente método:

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

    Cambio *google* demasiado*cuenta de Microsoft*, *twitter*, *facebook*, o *windowsazureactivedirectory* si no usas Google como proveedor de identidades. Si utiliza Facebook, debe [incluir los dominios de Facebook en la lista blanca][1] en su aplicación.

    Reemplace hello **urlScheme** con un nombre único para la aplicación.  Hola urlScheme debe ser Hola igual como protocolo de esquema de dirección URL que especificó en Hola Hola **permite redirigir direcciones URL externas de** campo Hola portal de Azure. Hola autenticación devolución de llamada tooswitch tooyour atrás aplicación usa Hello urlScheme una vez completada la solicitud de autenticación.

2. Reemplace `[self refresh]` en `viewDidLoad` en *QSTodoListViewController.m* con hello siguiente código:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Abra hello `QSAppDelegate.h` de archivos y agregar el siguiente código de hello:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Abra hello `QSAppDelegate.m` de archivos y agregar el siguiente código de hello:

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

   Agregue este código directamente antes de la lectura de la línea de hello `#pragma mark - Core Data stack`.  Reemplace el _appname_ urlScheme valor invocando Hola utilizado en el paso 1.

5. Abra hello `AppName-Info.plist` archivo (AppName reemplace con el nombre de saludo de la aplicación) y agregar el siguiente código de hello:

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

    Este código debe colocarse dentro de hello `<dict>` elemento.  Reemplace hello _appname_ cadena (dentro de la matriz para **CFBundleURLSchemes**) con el nombre de la aplicación hello que eligió en el paso 1.  También puede realizar estos cambios en hello plist editor - haga clic en hello `AppName-Info.plist` archivo en XCode tooopen hello plist editor.

    Reemplace hello `com.microsoft.azure.zumo` de cadena de **CFBundleURLName** con su equipo Apple agrupar identificador.

6. Presione *ejecutar* toostart Hola aplicación y, a continuación, inicie sesión. Cuando haya iniciado sesión, debe estar lista de tareas de tooview capaz de Hola y realizar actualizaciones.

**SWIFT**:

1. En el equipo Mac, abra *ToDoTableViewController.swift* en Xcode y agregue Hola siguiente método:

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

    Cambio *google* demasiado*cuenta de Microsoft*, *twitter*, *facebook*, o *windowsazureactivedirectory* si no usas Google como proveedor de identidades. Si utiliza Facebook, debe [incluir los dominios de Facebook en la lista blanca][1] en su aplicación.

    Reemplace hello **urlScheme** con un nombre único para la aplicación.  Hola urlScheme debe ser Hola igual como protocolo de esquema de dirección URL que especificó en Hola Hola **permite redirigir direcciones URL externas de** campo Hola portal de Azure. Hola autenticación devolución de llamada tooswitch tooyour atrás aplicación usa Hello urlScheme una vez completada la solicitud de autenticación.

2. Quitar líneas de hello `self.refreshControl?.beginRefreshing()` y `self.onRefresh(self.refreshControl)` al final de `viewDidLoad()` en *ToDoTableViewController.swift*. Agregue una llamada demasiado`loginAndGetData()` en su lugar:

    ```swift
    loginAndGetData()
    ```

3. Abra hello `AppDelegate.swift` de archivos y agregar Hola después línea toohello `AppDelegate` clase:

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

    Reemplace hello _appname_ urlScheme valor invocando Hola utilizado en el paso 1.

4. Abra hello `AppName-Info.plist` archivo (AppName reemplace con el nombre de saludo de la aplicación) y agregar el siguiente código de hello:

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

    Este código debe colocarse dentro de hello `<dict>` elemento.  Reemplace hello _appname_ cadena (dentro de la matriz para **CFBundleURLSchemes**) con el nombre de la aplicación hello que eligió en el paso 1.  También puede realizar estos cambios en hello plist editor - haga clic en hello `AppName-Info.plist` archivo en XCode tooopen hello plist editor.

    Reemplace hello `com.microsoft.azure.zumo` de cadena de **CFBundleURLName** con su equipo Apple agrupar identificador.

5. Presione *ejecutar* toostart Hola aplicación y, a continuación, inicie sesión. Cuando haya iniciado sesión, debe estar lista de tareas de tooview capaz de Hola y realizar actualizaciones.

La autenticación de App Service utiliza Apple Inter-App Communication.  Para obtener más detalles sobre este tema, consulte toohello [documentación de Apple][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portal de Azure]: https://portal.azure.com

[inicio rápido de iOS]: app-service-mobile-ios-get-started.md

