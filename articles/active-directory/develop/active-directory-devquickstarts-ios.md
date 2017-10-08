---
title: "aaaIntegrate Azure AD en una aplicación de iOS | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación de iOS que se integra con Azure AD para inicio de sesión y llamadas a Azure AD había protegido API mediante OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Integrar Azure AD en una aplicación iOS
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Probar la versión preliminar de Hola de nuestra nueva [portal para desarrolladores de](https://identity.microsoft.com/Docs/iOS) que le ayuda a ponerse a trabajar con Azure Active Directory en tan solo unos minutos.  portal para desarrolladores de Hello le guía a través del proceso de Hola de registrar una aplicación y la integración de Azure AD en el código.  Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones. 
> 
> 

Azure Active Directory (Azure AD) proporciona Hola biblioteca de autenticación de Active Directory o AAL, para los clientes de iOS que necesitan tooaccess los recursos protegidos. AAL simplifica el proceso de Hola que su aplicación usa los tokens de acceso tooobtain. toodemonstrate lo fácil es, en este artículo se compila una aplicación de lista de tareas pendientes de C de objetivo que:

* Obtiene acceso para llamar a API de Azure AD Graph hello mediante el uso de hello [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Buscar un directorio para los usuarios con un alias determinado

aplicación toobuild Hola completa trabajo, debe:

1. Registrar la aplicación con Azure AD
2. Instalar y configurar ADAL.
3. Usar AAL tooget tokens de Azure AD.

tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). También necesita a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación. Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).


> [!TIP]
> Probar la versión preliminar de Hola de nuestra nueva [portal para desarrolladores de](https://identity.microsoft.com/Docs/iOS) que le ayuda a ponerse en marcha con Azure AD en tan solo unos minutos. portal para desarrolladores de Hello le guía a través del proceso de Hola de registrar una aplicación y la integración de Azure AD en el código. Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Determinación de cuál es el URI de redireccionamiento para iOS
toosecurely iniciar las aplicaciones en ciertos escenarios SSO, debe crear un *URI de redireccionamiento* en un formato determinado. Una redirección URI es tooensure usado que Hola tokens toohello devuelto correcta aplicación que solicitó para ellos.


formato de iOS de Hello en una redirección URI es:

```
<app-scheme>://<bundle-id>
```

* **aap-scheme**: está registrado en el proyecto de XCode. Es el modo en que otras aplicaciones pueden llamarlo. Puede encontrarlo en Info.plist -> Tipos de URL -> Identificador de URL. Debe crear uno si aún no tiene ninguno configurado.
* **identificador de paquete** -esto es hello bajo "identidad" se encuentra el identificador de paquete anula la configuración del proyecto en XCode.

Ejemplo de este código de inicio rápido: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***.

## <a name="2-register-hello-directorysearcher-application"></a>2. Registrar aplicación de DirectorySearcher hello
tooset seguridad sus tokens de tooget de aplicación, primero debe tooregister en Azure AD de inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta. En hello **Directory** lista, seleccione la aplicación de inquilino de Active Directory de Hola donde desea tooregister.
3. Haga clic en **más servicios** en Hola panel de navegación izquierda y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Siga Hola solicita toocreate un nuevo **aplicación cliente nativa**.
  * Hola **nombre** de hello aplicación describe los usuarios de tooend de aplicación.
  * Hola **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn token respuestas.  Escriba un valor que es específico tooyour aplicación y se basa en información del identificador URI de redireccionamiento anterior de Hola.
6. Después de haber completado el registro de hello, Azure AD le asigna la aplicación un identificador de aplicación único.  Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.
7. De hello **configuración** página, seleccione **permisos necesarios** y, a continuación, seleccione **agregar**. Seleccione **Microsoft Graph** como Hola API y, a continuación, agregue hello **leer datos de directorio** permiso en **permisos delegados**.  Esta acción configura la Hola de tooquery aplicación API de Azure AD Graph para los usuarios.

## <a name="3-install-and-configure-adal"></a>3. Instalación y configuración de ADAL
Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.  Para obtener toocommunicate ADAL con Azure AD, deberá tooprovide con cierta información sobre el registro de aplicación.

1. Comienza agregando toohello AAL DirectorySearcher proyecto mediante el uso de CocoaPods.

    ```
    $ vi Podfile
    ```
2. Agregue Hola después toothis podfile:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Ahora cargue hello podfile utilizando CocoaPods. Mediante este paso se crea un área de trabajo de XCode que cargará.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. En proyecto de inicio rápido de hello, abra el archivo plist de hello `settings.plist`.  Reemplace los valores de hello de elementos de Hola de hello sección tooreflect Hola valores especificados en hello portal de Azure. El código hace referencia a estos valores cada vez que usa ADAL.
  * Hola `tenant` es Hola dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.
  * Hola `clientId` es Hola Id. de cliente de la aplicación que ha copiado desde el portal de Hola.
  * Hola `redirectUri` es la dirección URL de redireccionamiento de Hola que registró en el portal de Hola.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Usar AAL tooget tokens de Azure AD
Hello principio básico detrás de AAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama un completionBlock `+(void) getToken : `, y AAL Hola rest.  

1. Hola `QuickStart` proyecto abierto `GraphAPICaller.m` y busque hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comentario cerca de la parte superior de Hola.  Aquí es donde pasan coordenadas Hola AAL a través de un CompletionBlock, toocommunicate con Azure AD y le diga cómo toocache símbolos (tokens).

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. Ahora necesitamos toouse este token toosearch para los usuarios en el gráfico de Hola. Buscar hello `// TODO: implement SearchUsersList` comentario. Este método realiza una tooquery de toohello Azure AD Graph API de solicitud GET para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.  tooquery hello Azure AD Graph API, deberá tooinclude un access_token Hola `Authorization` encabezado de solicitud de saludo. Aquí es donde entra en juego AAL.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. Cuando la aplicación solicita un token mediante una llamada a `getToken(...)`, AAL intenta tooreturn un token sin pedir las credenciales de usuario de Hola.  Si AAL determina que el usuario hello toosign en tooget un token es necesario, mostrar un cuadro de diálogo de inicio de sesión, recopilar las credenciales de usuario de hello y, a continuación, devuelve un token después de una autenticación correcta.  Si AAL no es capaz de tooreturn un token por cualquier motivo, produce un `AdalException`.

> [!Note] 
> Hola `AuthenticationResult` objeto contiene un `tokenCacheStoreItem` objeto que puede ser usado toocollect Hola información que necesite la aplicación. Hola de inicio rápido, `tokenCacheStoreItem` es toodetermine usado si ya se realiza la autenticación.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Compilar y ejecutar la aplicación hello
¡Enhorabuena! Ahora tiene una aplicación de iOS de trabajo que puede autenticar a los usuarios, seguro llamar a las API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.  Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.  Inicie la aplicación QuickStart e inicie sesión con uno de esos usuarios.  Busque otros usuarios según su UPN.  Cierre la aplicación hello y, a continuación, vuelva a abrirlo.  Tenga en cuenta que la sesión del usuario de hello permanece intacta.

AAL resulta fácil tooincorporate todas estas características de identidad comunes en la aplicación.  Se encarga de todo el trabajo dirty Hola para usted, como la administración de memoria caché, compatibilidad con protocolos de OAuth, presentaciones usuario Hola con un toosign de interfaz de usuario en y actualizar tokens caducados.  Todo lo que realmente necesita tooknow es una sola llamada API, `getToken`.

Como referencia, ejemplo de Hola finalizado (sin los valores de configuración) se proporciona en [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Pasos siguientes
Ahora puede mover en escenarios de tooadditional.  Puede que desee tootry:

* [Proteger una API web de Node.js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md)
* Obtenga información acerca de [cómo tooenable SSO de aplicación cruzado en iOS mediante AAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

