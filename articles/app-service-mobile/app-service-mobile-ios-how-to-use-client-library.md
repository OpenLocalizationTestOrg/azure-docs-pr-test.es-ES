---
title: "aaaHow tooUse iOS SDK para aplicaciones móviles de Azure"
description: "¿Cómo tooUse iOS SDK para aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>¿Cómo tooUse iOS biblioteca de cliente para aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Esta guía le enseña con hello más reciente de escenarios comunes de tooperform [iOS de aplicaciones móviles de Azure SDK][1]. Si estás nuevas aplicaciones de Mobile tooAzure, complete primero [inicio rápido de Azure Mobile Apps] toocreate un back-end, cree una tabla y descargar un proyecto de Xcode pregenerado iOS. En esta guía se centra en SDK de iOS de Hola de cliente. toolearn Obtenga más información sobre Hola SDK de servidor de back-end de hello, vea Hola Server SDK explicativa.

## <a name="reference-documentation"></a>Documentación de referencia
Hello documentación de referencia de SDK de cliente de iOS de Hola se encuentra aquí: [aplicaciones móviles de Azure iOS referencia de cliente][2].

## <a name="supported-platforms"></a>Plataformas compatibles
SDK de iOS de Hello admite proyectos Objective-C, Swift 2.2 proyectos y proyectos de Swift 2.3 para iOS versiones 8.0 o posteriores.

la autenticación de "flujo de servidor" Hello usa un WebView para hello presentada la interfaz de usuario.  Si el dispositivo de hello no es capaz de toopresent una UI WebView, se requiere el otro método de autenticación es fuera Hola ámbito del producto Hola.  
Por tanto, este SDK no es adecuado para dispositivos de tipo reloj o con restricciones similares.

## <a name="Setup"></a>Configuración y requisitos previos
En esta guía se asume que ha creado un back-end con una tabla. Esta guía se da por supuesto que esa tabla hello tiene el mismo esquema como tablas de hello en los tutoriales. En esta guía también se supone que en el código se hace referencia a `MicrosoftAzureMobile.framework` e importa `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Creación del cliente
tooaccess un back-end de aplicaciones móviles de Azure en el proyecto, crear un `MSClient`. Reemplace `AppUrl` con la URL de la aplicación hello. Puede dejar `gatewayURLString` y `applicationKey` vacías. Si configura una puerta de enlace para la autenticación, rellenar `gatewayURLString` con la dirección URL de puerta de enlace de Hola.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**SWIFT**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Creación de una referencia de tabla
tooaccess o actualizar los datos, cree una tabla de referencia toohello back-end. Reemplace `TodoItem` con nombre hello de la tabla

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**SWIFT**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Consulta de datos
toocreate una consulta de base de datos, Hola consulta `MSTable` objeto. Hello consulta siguiente obtiene todos los elementos de hello `TodoItem` y registros de Hola texto de cada elemento.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**SWIFT**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Filtro de datos devueltos
resultados de toofilter, hay muchas opciones disponibles.

toofilter mediante un predicado, use un `NSPredicate` y `readWithPredicate`. siguiente Hola filtra los elementos de lista de tareas de datos devueltos toofind solo incompletos.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**SWIFT**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Uso de MSQuery
tooperform crear una consulta compleja (incluida la clasificación y paginación), un `MSQuery` de objeto, directamente o mediante un predicado:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**SWIFT**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` permite controlar varios comportamientos de consulta.

* Especificar el orden de los resultados
* Límite de campos tooreturn
* Limitar el número de registros tooreturn
* Especificar el recuento total en la respuesta
* Especificar parámetros de la cadena de consulta personalizados en la solicitud
* Aplicar funciones adicionales

Ejecutar un `MSQuery` consulta mediante una llamada a `readWithCompletion` en el objeto de Hola.

## <a name="sorting"></a>Ordenación de datos con MSQuery
resultados de toosort, echemos un vistazo a un ejemplo. invocar toosort por texto' campo' ascendente y luego por 'complete' en orden descendente, `MSQuery` así:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**SWIFT**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Limitación de campos y expansión de los parámetros de cadena de consulta con MSQuery
toolimit toobe de campos devuelto en una consulta, se especifican nombres de Hola de campos de Hola Hola **selectFields** propiedad. Este ejemplo devuelve solo texto hello y campos completados:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**SWIFT**:

```
query.selectFields = ["text", "complete"]
```

parámetros de cadena de consulta adicionales tooinclude en servidor hello solicitan (por ejemplo, porque utiliza un script de servidor personalizado), rellenar `query.parameters` así:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**SWIFT**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Procedimiento: configuración del tamaño de página
Con aplicaciones de Azure Mobile, controles de tamaño de página de Hola Hola número de registros que se extraigan de tablas de back-end de hello al mismo tiempo. Llamar demasiado`pull` datos, a continuación, podrían crear lotes de datos, basada en este tamaño de página, hasta que no haya ningún más toopull de registros.

Es posible tooconfigure un tamaño de página con **MSPullSettings** tal y como se muestra a continuación. tamaño de página predeterminado de Hello es 50 y ejemplo de Hola siguiente cambia too3.

Para mejorar el rendimiento es posible configurar otro tamaño de página. Si tiene un gran número de registros de datos pequeños, un tamaño de página alta reduce el número de Hola de ida y vuelta del servidor.

Esta configuración controla sólo tamaño de página de hello en el lado del cliente de Hola. Si el cliente de hello pide un tamaño de página que admite aplicaciones móviles de hello back-end, el tamaño de página de hello es limitado a back-end de Hola Hola máximo es toosupport configurado.

Esta configuración también es hello *número* de registros de datos, no Hola *tamaño en bytes*.

Si aumenta el tamaño de página de cliente hello, también debe aumentar el tamaño de página de hello en el servidor de Hola. Vea ["Cómo: ajustar el tamaño de paginación de tabla Hola"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para hello pasos toodo esto.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**SWIFT**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Insertar datos
crear una nueva fila de tabla, tooinsert una `NSDictionary` e invocar `table insert`. Si [esquema dinámico] está habilitada, back-end de hello servicio de aplicaciones de Azure mobile genera automáticamente nuevas columnas en función de hello `NSDictionary`.

Si `id` es no siempre, Hola back-end genera automáticamente un nuevo identificador único. Proporcionar su propia `id` toouse de correo electrónico direcciones, nombres de usuario o sus propios valores personalizados como identificador. Proporcionar su propio ID puede facilitar las combinaciones y la lógica de la base de datos de tipo empresarial.

Hola `result` contiene Hola nuevo elemento que se ha insertado. Según la lógica del servidor, toowhat de datos modificados en comparación con se ha pasado toohello server o puede tener adicionales.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Modificación de datos
tooupdate una fila existente, modificar un elemento y la llamada `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

O bien, especifique Id. de fila de Hola y campo Hola actualizado:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

Como mínimo, Hola `id` atributo debe establecerse al realizar las actualizaciones.

## <a name="deleting"></a>Eliminación de datos
toodelete un elemento, invocar `delete` con elemento hello:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**SWIFT**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

O bien elimínelo proporcionando un identificador de fila:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**SWIFT**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Como mínimo, Hola `id` atributo debe establecerse al hacer que se elimina.

## <a name="customapi"></a>Llamada a una API personalizada
Con una API personalizada, puede exponer cualquier funcionalidad de back-end. No tiene toomap tooa la operación de tabla. No sólo obtendrá más control sobre la mensajería, incluso puede leer o establecer los encabezados y cambiar el formato del cuerpo de respuesta de Hola. toolearn cómo leer toocreate una API personalizada en el back-end de hello, [API personalizadas](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

llamar una API personalizada, toocall `MSClient.invokeAPI`. solicitud de Hola y el contenido de la respuesta se tratan como JSON. toouse otros tipos de medios, [uso Hola otra sobrecarga de `invokeAPI` ] [ 5].  toomake una `GET` solicitar en lugar de un `POST` solicitar, parámetro de conjunto de `HTTPMethod` demasiado`"GET"` y parámetro `body` demasiado`nil` (ya que las solicitudes GET no tener cuerpos de mensaje). Si la API personalizada es compatible con otros verbos HTTP, cambie `HTTPMethod` de acuerdo a ello.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**SWIFT**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Cómo: notificaciones de registro inserción plantillas toosend multiplataforma
plantillas de tooregister, pasar plantillas con su **client.push registerDeviceToken** método en la aplicación cliente.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**SWIFT**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Las plantillas son del tipo NSDictionary y pueden contener varias plantillas en hello siguiendo el formato:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**SWIFT**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Se eliminan todas las etiquetas de solicitud de hello para la seguridad.  tooadd etiquetas tooinstallations o plantillas en las instalaciones, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][4].  notificaciones de toosend mediante estas plantillas registradas, trabajar con [API de los centros de notificación][3].

## <a name="errors"></a>Gestión de errores
Cuando se llama a un servicio de aplicaciones de Azure de back-end móvil, bloque de finalización de hello contiene un `NSError` parámetro. En caso de producirse un error, este parámetro no será nulo. En el código, debe comprobar este parámetro y controlar el error de hello según sea necesario, como se muestra en hello anterior fragmentos de código.

archivo hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] define las constantes de hello `MSErrorResponseKey`, `MSErrorRequestKey`, y `MSErrorServerItemKey`. tooget más datos relacionados con error de toohello:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**SWIFT**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Además, el archivo hello define constantes para cada código de error:

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**SWIFT**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Cómo: autenticar a los usuarios con hello biblioteca de autenticación de Active Directory
Puede usar los usuarios de toosign de hello biblioteca de autenticación de Active Directory (ADAL) en la aplicación con Azure Active Directory. Autenticación de flujo del cliente mediante un proveedor de identidades SDK es preferible toousing hello `loginWithProvider:completion:` método.  Este tipo de autenticación proporciona una experiencia de usuario más nativa y permite realizar más personalizaciones.

1. Configurar el aplicación móvil de back-end para el inicio de sesión AAD Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory] [ 7] tutorial. Asegúrese de que paso opcional de Hola de toocomplete de registrar una aplicación cliente nativa. Para iOS, se recomienda que redirección Hola URI tiene forma de Hola `<app-scheme>://<bundle-id>`. Para obtener más información, vea hello [inicio rápido de iOS ADAL][8].
2. Instale ADAL mediante Cocoapods. Editar el Hola de tooinclude Podfile después de la definición, reemplazar **su proyecto** con nombre de Hola de su proyecto de Xcode:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   hello Pod y:

        pod 'ADALiOS'
3. Usar Hola Terminal, ejecute `pod install` desde el directorio de hello, que contiene el proyecto y abra Hola genera Xcode área de trabajo (no en proyecto de hello).
4. Agregar Hola tras la aplicación de código tooyour, según el idioma de toohello que está usando. En cada uno, realice estas sustituciones:

   * Reemplace **aquí de autoridad de INSERCIÓN** por nombre de Hola de inquilino de hello en el que se aprovisiona la aplicación. El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Este valor se puede copiar desde la pestaña del dominio hello en Azure Active Directory en hello [portal de Azure clásico].
   * Reemplace **Insertar recurso identificador aquí** con el identificador de cliente de Hola para su aplicación móvil de back-end. Puede obtener el identificador de cliente de hello **avanzadas** en la ficha **configuración de Azure Active Directory** en el portal de Hola.
   * Reemplace **INSERT-CLIENT-ID-aquí** con el Id. de cliente de Hola que copió de la aplicación de cliente nativo de Hola.
   * Reemplace **INSERT-REDIRECT-URI-aquí** con su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS. Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**SWIFT**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Cómo: autenticar a los usuarios con hello Facebook SDK para iOS
Puede usar Hola Facebook SDK para los usuarios de toosign de iOS en la aplicación con Facebook.  Mediante la autenticación de un flujo de cliente es preferible toousing hello `loginWithProvider:completion:` método.  autenticación de flujo de cliente de Hello proporciona una idea UX más nativa y permite la personalización adicional.

1. Configure su aplicación móvil de back-end para el inicio de sesión Facebook siguiendo el [cómo tooconfigure aplicación de servicio de inicio de sesión de Facebook] [ 9] tutorial.
2. Instalar Hola Facebook SDK para iOS por hello siguiente [Facebook SDK para iOS: Introducción a] [ 10] documentación. En lugar de crear una aplicación, puede agregar el registro existente de tooyour la plataforma iOS Hola.
3. Documentación de Facebook incluye algún código Objective-C en hello delegado de la aplicación. Si utilizas **Swift**, puede usar Hola siguiendo las traducciones de AppDelegate.swift:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. En suma tooadding `FBSDKCoreKit.framework` tooyour proyecto de equipo y agregar una referencia demasiado`FBSDKLoginKit.framework` Hola igual.
5. Agregar Hola tras la aplicación de código tooyour, según el idioma de toohello que está usando.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**SWIFT**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Autenticación de usuarios con Fabric de Twitter para iOS
Puede usar a tejido para los usuarios de toosign de iOS en la aplicación con Twitter. Flujo de autenticación del cliente es preferible toousing hello `loginWithProvider:completion:` método, tal como se proporciona una idea UX más nativa y permite la personalización adicional.

1. Configurar el aplicación móvil de back-end para el inicio de sesión Twitter Hola después [cómo tooconfigure aplicación de servicio de inicio de sesión de Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.
2. Agregar proyecto de tejido tooyour Hola siguiente [tejidos para iOS: Getting Started] documentación y la configuración de TwitterKit.

   > [!NOTE]
   > De forma predeterminada, Fabric creará automáticamente una aplicación de Twitter. Puede evitar la creación de una aplicación registrando hello clave de consumidor y secreto de consumidor que se creó anteriormente con hello siguientes fragmentos de código.    Como alternativa, puede reemplazar Hola clave de consumidor y valores de secreto de consumidor que proporcione valores tooApp servicio con hello, vea Hola [panel del tejido]. Si elige esta opción, ser seguro tooset Hola devolución de llamada URL tooa valor marcador de posición, como `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Si elige toouse secretos de Hola que creó anteriormente, agregue Hola después código tooyour delegado de la aplicación:

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **SWIFT**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Agregar Hola tras la aplicación de código tooyour, según el idioma de toohello que está usando.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**SWIFT**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Cómo: autenticar a los usuarios con hello SDK de inicio de sesión de Google para iOS
Puede usar Hola SDK de inicio de sesión de Google para los usuarios de toosign de iOS en su aplicación mediante una cuenta de Google.  Google ha anunciado recientemente directivas de seguridad de OAuth de tootheir de cambios.  Estos cambios de directiva requerirá el uso de hello del SDK de Google en hello futuras.

1. Configurar el aplicación móvil de back-end para el inicio de sesión en Google Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Google](app-service-mobile-how-to-configure-google-authentication.md) tutorial.
2. Instalar Hola Google SDK para iOS por hello siguiente [Google Sign-In for iOS: empezar a integrar](https://developers.google.com/identity/sign-in/ios/start-integrating) documentación. Puede omitir la sección de "Autenticar con un servidor de back-end" Hola.
3. Agregar Hola después del delegado tooyour `signIn:didSignInForUser:withError:` método, según el idioma de toohello que está usando.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**SWIFT**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Asegúrese de que también agregar Hola después demasiado`application:didFinishLaunchingWithOptions:` en su aplicación, delegado, sustituyendo "SERVER_CLIENT_ID" hello mismo identificador que utilizó tooconfigure servicio de aplicaciones en el paso 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **SWIFT**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Agregar Hola tras la aplicación de tooyour de código en un UIViewController que implementa hello `GIDSignInUIDelegate` protocolo, según el idioma de toohello que está usando.  Cierre sesión antes de iniciar sesión nuevo y, aunque no es necesario tooenter sus credenciales de nuevo, verá un cuadro de diálogo de consentimiento.  Solo llame a este método cuando ha expirado el token de sesión Hola.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[inicio rápido de Azure Mobile Apps]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[esquema dinámico]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[panel del tejido]: https://www.fabric.io/home
[tejidos para iOS: Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
