---
title: "aplicación de iOS de inicio de sesión tooan de aaaAdd con Hola extremo v2.0 de Azure AD | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación de iOS que inicia sesión en los usuarios con ambos cuenta personal de Microsoft y cuentas profesionales o educativas mediante el uso de bibliotecas de otros fabricantes."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Agregar aplicación de iOS de inicio de sesión tooan mediante una biblioteca de terceros con API Graph con el punto de conexión de hello v2.0
plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect. Los desarrolladores pueden usar cualquier biblioteca que deseen toointegrate con nuestros servicios. toohelp a los desarrolladores usar nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este uno toodemonstrate la plataforma de identidad de Microsoft de tooconfigure bibliotecas de otros fabricantes tooconnect toohello. La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) toohello plataforma de identidad de Microsoft se pueden conectar.

Con una aplicación Hola que crea en este tutorial, los usuarios pueden iniciar sesión en la organización de tootheir y, a continuación, busque otras personas de su organización mediante Hola API Graph.

Si es nuevo tooOAuth2 u OpenID Connect, gran parte de esta configuración de ejemplo puede que no tenga sentido tooyou. Si este es el caso, le recomendamos que lea [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

> [!NOTE]
> Algunas características de la plataforma que tiene una expresión en Hola OAuth2 o estándares de OpenID Connect, como acceso condicional y administración de directivas de Intune, requieren toouse nuestro código abierto bibliotecas de identidad de Microsoft Azure.
> 
> 

el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory.

> [!NOTE]
> toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Descarga del código desde GitHub
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

También se puede descargar el ejemplo de Hola y empezar a trabajar de forma inmediata:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Registrar una aplicación
Crear una nueva aplicación en hello [portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga Hola pasos detallados en [cómo una aplicación con el punto de conexión de hello v2.0 tooregister](active-directory-v2-app-registration.md).  Asegúrese de que:

* Hola copia **identificador de la aplicación** que está asignado tooyour aplicación porque lo necesitará pronto.
* Agregar hello **Mobile** plataforma para la aplicación.
* Hola copia **URI de redireccionamiento** desde el portal de Hola. Debe usar el valor predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Descargar Hola terceros NXOAuth2 biblioteca y crear un área de trabajo
En este tutorial, usará hello OAuth2Client desde GitHub, que es una biblioteca de OAuth2 para Mac OS X y iOS (cacao y sus touch). Esta biblioteca se basa en 10 de borrador de especificación de OAuth2 Hola. Implementa el perfil de aplicación nativa de Hola y es compatible con el extremo de autorización de saludo del usuario de Hola. Éstos son todos los puntos de hello, deberá toointegrate a la plataforma de identidad de Microsoft de Hola.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Agregar proyecto de biblioteca tooyour de hello mediante CocoaPods
CocoaPods es un administrador de dependencias para proyectos de Xcode. Administra automáticamente los pasos de la instalación anterior de Hola.

```
$ vi Podfile
```
1. Agregue Hola después toothis podfile:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Cargar hello podfile mediante CocoaPods. Así se creará una nueva área de trabajo de XCode que cargará.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Explorar Hola estructura del proyecto de Hola
Hola siguiendo estructura está configurado para nuestro proyecto de esqueleto de hello:

* Una vista principal con una búsqueda UPN
* Una vista de detalle para los datos de hello acerca del usuario seleccionado Hola
* Una vista de inicio de sesión donde un usuario puede iniciar sesión en el gráfico de toohello aplicación tooquery Hola

Moveremos toovarious archivos en la autenticación de esqueleto tooadd Hola. Otras partes del código de hello, como el código visual de hello, no pertenecen tooidentity pero se proporcionan automáticamente.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Configure hello settings.plst archivo de biblioteca de Hola
* En el proyecto de inicio rápido de hello, abra hello `settings.plist` archivo. Reemplace los valores de hello de elementos de Hola de hello tooreflect Hola valores de una sección que usó en el portal de Azure Hola. El código hará referencia a estos valores cada vez que usa Hola biblioteca de autenticación de Active Directory.
  * Hola `clientId` es Hola Id. de cliente de la aplicación que ha copiado desde el portal de Hola.
  * Hola `redirectUri` es dirección URL de redireccionamiento de hello ese portal Hola proporcionado.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Configurar la biblioteca de NXOAuth2Client hello en su LoginViewController
biblioteca de Hello NXOAuth2Client requiere algunos tooget valores configurar. Después de completar esa tarea, puede usar Hola adquirida toocall token Hola API Graph. Dado que `LoginView` se llamará cada vez que necesitamos tooauthenticate, tiene sentido tooput valores de configuración en el archivo toothat.

* Vamos a agregar algunos valores toohello `LoginViewController.m` de contexto del archivo tooset hello para la autenticación y autorización. Obtener más información acerca de los valores de hello seguir código de hello.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Echemos un vistazo a los detalles sobre el código de hello.

primera cadena de Hello es para `scopes`.  Hola `User.Read` valor permite perfil básico de hello tooread de hello firmado en usuario.

Puede aprender más acerca de todos los ámbitos disponibles de hello en [ámbitos de permiso de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Para `authURL`, `loginURL`, `bhh`, y `tokenURL`, debe utilizar valores de hello indicados anteriormente. Si utiliza código abierto de hello bibliotecas de identidad de Microsoft Azure, se extraen estos datos automáticamente mediante el uso de nuestro extremo de metadatos. Que hemos hecho esfuerzo Hola de extraer estos valores automáticamente.

Hola `keychain` valor es contenedor Hola Hola NXOAuth2Client biblioteca utilizará toocreate un toostore llaveros sus tokens. Si desea tooget inicio de sesión único (SSO) en numerosas aplicaciones, puede especificar Hola la misma cadena de claves en cada una de las aplicaciones y solicitar la utilización de Hola de esa cadena de claves en los derechos de Xcode. Esto se explica en hello documentación de Apple.

rest Hola de estos valores son la biblioteca de hello toouse necesario y crear lugares para usted contexto toohello de toocarry valores.

### <a name="create-a-url-cache"></a>Creación de una caché de URL
Dentro de `(void)viewDidLoad()`, siempre que se llama después de carga la vista hello, hello código siguiente primes de la memoria caché de nuestro uso.

Agregue Hola siguiente código:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Creación de una vista web para iniciar sesión
Una vista Web puede solicitar al usuario de Hola de factores adicionales como mensaje de texto SMS (si está configurado) o devolver usuario de toohello de mensajes de error. Aquí configurará Hola WebView y, más adelante Hola de escritura código toohandle hello las devoluciones de llamada se realizarán en hello WebView de servicios de identidad de Hola.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Invalidar la autenticación de hello WebView métodos toohandle
Hola tootell WebView lo que sucede cuando un usuario necesita toosign en según lo descrito anteriormente, puede pegar Hola siguiente código.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Escribir código toohandle Hola resultado de solicitud de OAuth2 de Hola
Hello código siguiente controlará redirectURL Hola que devuelve de hello WebView. Si la autenticación no era correcta, el código de hello volverá a intentarlo. Mientras tanto, biblioteca de hello proporcionará error Hola que puede ver en la consola de Hola o administrar de forma asincrónica.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Configurar Hola contexto OAuth (denominado almacén de cuentas)
Aquí puede llamar a `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` en el almacén de una cuenta compartida de Hola para cada servicio que desea Hola aplicación toobe capaz de tooaccess. tipo de cuenta de Hello es una cadena que se utiliza como identificador para un servicio determinado. Dado que se obtiene acceso a API Graph hello, código de hello hace referencia tooit como `"myGraphService"`. A continuación, configure un observador que le indicará cuando algo cambia con el token de Hola. Después de obtener el token de hello, devolver Hola usuario espera toohello `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Configurar hello toosearch de vista maestra y mostrar los usuarios Hola Hola API Graph
Una aplicación de Master-View-Controller (MVC) que se muestra hello devuelve datos en la cuadrícula de hello está más allá del ámbito de Hola de este tutorial y muchos tutoriales en línea se explican cómo toobuild uno. Todo este código está en archivo esqueleto Hola. Sin embargo, deberá toodeal con algunas cosas en esta aplicación de MVC:

* Interceptar cuando un usuario escribe algo en el campo de búsqueda de Hola
* Proporcionar un objeto de datos back-toohello MasterView por lo que pueden mostrar los resultados de hello en cuadrícula Hola

Lo haremos todo a continuación.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Agregar un toosee de verificación si ha iniciado sesión
aplicación Hello no hace poco si Hola usuario no ha iniciado sesión, por lo que es toocheck inteligente si ya hay un token en memoria caché de Hola. Si no es así, redirige toohello LoginView para hello usuario toosign en. Si recuerda, Hola mejor manera toodo acciones cuando se carga una vista es hello toouse `viewDidLoad()` método que nos proporciona Apple.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Actualizar Hola vista de tabla cuando se reciben datos
Cuando Hola API Graph devuelve datos, necesita toodisplay Hola datos. Para simplificar, aquí tiene todos los Hola código tooupdate Hola la tabla. Solo puede pegar los valores correctos de hello en el código reutilizable MVC.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Proporcionar un hello toocall de manera API Graph cuando alguien escribe en el campo de búsqueda de Hola
Cuando un usuario escribe una búsqueda en el cuadro de hello, necesita tooshove que, con toohello API Graph. Hola `GraphAPICaller` (clase), que van a generar en el siguiente código de hello, separa la funcionalidad de búsqueda de Hola de presentación de Hola. Por ahora, vamos a escribir código de hello que cualquier toohello de caracteres de búsqueda API Graph de fuentes de distribución. Para ello, proporciona un método denominado `lookupInGraph`, que toma la cadena de Hola que queremos toosearch para.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Escribir un tooaccess de clase auxiliar Hola API Graph
Este es el núcleo de Hola de nuestra aplicación. Mientras que el resto de Hola inserta código en el modelo MVC predeterminada de Hola de Apple, aquí se pueden escribir gráfico de hello tooquery código como usuario de hello tipos y, a continuación, devolver los datos. Este es el código de hello y una explicación detallada lo sigue.

### <a name="create-a-new-objective-c-header-file"></a>Creación de un nuevo archivo de encabezado Objective C
Archivo de nombre hello `GraphAPICaller.h`y agregue el siguiente código de hello.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Se puede ver que estamos especificando un método que toma una cadena y devuelve un elemento completionBlock. Este completionBlock, tal y como habrá adivinado, actualizará Hola tabla proporcionando un objeto con datos rellenada en tiempo real como Hola búsquedas de usuario.

### <a name="create-a-new-objective-c-file"></a>Creación de un nuevo archivo Objective C
Archivo de nombre hello `GraphAPICaller.m`y agregue Hola siguiendo el método.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

Analicemos pormenorizadamente este método.

núcleo de Hola de este código es Hola `NXOAuth2Request`, método que toma parámetros de Hola que ya haya definido en el archivo de hello settings.plist.

Hola primer paso es llamada de API Graph tooconstruct Hola right. Dado que se llama `/users`, especificar que mediante la anexión de recurso de la API de Graph toohello junto con la versión de Hola. Tiene sentido tooput estas opciones en un archivo de configuración externo ya estos pueden variar a medida que evoluciona Hola API.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

A continuación, hay parámetros de toospecify también proporcionará toohello llamada de API Graph. Es *muy importante* no coloque parámetros hello en el punto de conexión de hello recurso dado que se limpia para todos los caracteres de URI no conformes en tiempo de ejecución. Todo el código de consulta debe proporcionarse en parámetros de Hola.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Es posible que observe que se llama a un método `convertParamsToDictionary` que todavía no se ha escrito. Vamos a hacer ahora al final de hello del archivo hello:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
A continuación, vamos a usar hello `NXOAuth2Request` copia datos de tooget de método de hello API en formato JSON.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Por último, echemos un vistazo a cómo devolver datos de hello toohello MasterViewController. datos de Hello devuelve como en serie y necesita toobe deserializa y se cargan en un objeto puede usan ese hello MainViewController. Para ello, tiene el esqueleto de hello un `User.m/h` archivo que crea un objeto de usuario. Rellenar ese objeto de usuario con información del gráfico de Hola.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Ejecutar el ejemplo hello
Si ha utilizado el esqueleto de Hola o seguido junto con el tutorial Hola que ahora debe ejecutar la aplicación. Iniciar el simulador de Hola y haga clic en **iniciar sesión en** aplicación de hello toouse.

## <a name="get-security-updates-for-our-product"></a>Obtención de actualizaciones de seguridad para nuestro producto
Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando hello [TechCenter de seguridad](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.

