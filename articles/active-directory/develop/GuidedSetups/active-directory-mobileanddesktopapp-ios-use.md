---
title: "aaaAzure AD v2 iOS Introducción: uso | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones de iOS (Swift) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Usar Hola biblioteca de autenticación de Microsoft (MSAL) tooget un token para hello API Graph de Microsoft

Abra `ViewController.swift` y reemplace el código de hello con:

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Más información
#### <a name="getting-a-user-token-interactively"></a>Obtención de un token de usuario interactivamente
Llamar a hello `acquireToken` resultados del método en una ventana de explorador preguntar Hola toosign de usuario en. Las aplicaciones suelen requieran un toosign de usuario en forma interactiva Hola primera vez necesiten tooaccess un recurso protegido, o cuando una operación silenciosa tooacquire se produce un error en un token (por ejemplo, contraseña del usuario de hello expiró).

#### <a name="getting-a-user-token-silently"></a>Obtención de un token de usuario en silencio
Hola `acquireTokenSilent` método controla renovación sin ninguna interacción del usuario y adquisiciones de símbolo (token). Después de `acquireToken` se ejecuta para hello primera vez, `acquireTokenSilent` es Hola método usada tooobtain tokens utilizados tooaccess recursos para llamadas posteriores - protegidos como llamadas toorequest o renovar los tokens se realizan en modo silencioso.

Finalmente, `acquireTokenSilent` se producirá un error: por ejemplo, usuario de hello ha cerrado la sesión, o ha cambiado su contraseña en otro dispositivo. Cuando MSAL detecta que se puede resolver el problema de hello exigiendo una acción interactiva, que se activa un `MSALErrorCode.interactionRequired` excepción. La aplicación puede abordar esta excepción de dos maneras:

1.  Realizar una llamada con `acquireToken` inmediatamente, lo que produce preguntar Hola toosign de usuario en. Este patrón se utiliza normalmente en aplicaciones en línea que no hay ningún contenido sin conexión en la aplicación hello disponibles para el usuario de Hola. aplicación de ejemplo de Hola generado por este programa de instalación interactiva utiliza este patrón: puede verlo en Hola de acción a primera vez que ejecute la aplicación hello. Dado que ningún usuario utilizado alguna vez la aplicación hello, `applicationContext.users().first` contendrá un valor null y un ` MSALErrorCode.interactionRequired ` excepción. Hola código de ejemplo de Hola, a continuación, identificadores de Hola excepción mediante una llamada a `acquireToken` resultante en Preguntar Hola usuario toosign en.

2.  Las aplicaciones también pueden realizar un usuario de toohello de indicación visual en un inicio de sesión interactivo se requiere para el usuario de hello puede seleccionar Hola momento toosign en, o puede volver a intentar la aplicación hello `acquireTokenSilent` en un momento posterior. Se suele utilizar al usuario Hola puede usar otras funciones de aplicación hello sin que se va a interrumpir; por ejemplo, hay contenido sin conexión disponibles en la aplicación hello. En este caso, puede decidir usuario hello cuando quieran toosign en recursos de hello protegido tooaccess, o toorefresh Hola información obsoleta o la aplicación puede decidir tooretry `acquireTokenSilent` cuando se restaure la red después de estar disponible temporalmente.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Llamar a la API de Microsoft Graph hello mediante el símbolo (token) de hello que acabara de obtener

Agregar método de Hola de nuevo a continuación demasiado`ViewController.swift`. Este método es toomake usado un `GET` solicitud contra Hola API de Graph de Microsoft mediante un *encabezado de autorización HTTP*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a>Llamada de REST con una API protegida

En esta aplicación de ejemplo Hola `getContentWithToken()` método es toomake usa HTTP `GET` solicitud para un recurso protegido que requiera un llamador de contenido toohello Hola símbolo (token) y, a continuación, vuelva. Este método agrega el token de hello adquirido en hello *encabezado de autorización HTTP*. En este ejemplo, recurso de Hola es hello Microsoft Graph API *me* endpoint – que muestra información de perfil del usuario de Hola.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Configuración del cierre de sesión

Agregar Hola siguiente método demasiado`ViewController.swift` toosign usuario hello:

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Más información sobre el cierre de sesión

Hola `signoutButton` método quita usuario Hola Hola caché de usuario MSAL: Esto eficazmente indicará MSAL tooforget Hola actual usuario para una solicitud futura tooacquire un token solo tendrá éxito si se realiza toobe interactivo.

Aunque la aplicación hello en este ejemplo es compatible con un solo usuario, MSAL es compatible con escenarios donde pueden firmarse varias cuentas en hello vez: un ejemplo es una aplicación de correo electrónico donde un usuario tiene varias cuentas.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Registrar la devolución de llamada de Hola

Una vez que se autentica el usuario hello, Hola redirige Hola usuario espera toohello aplicación. Siga estos pasos hello tooregister esta devolución de llamada:

1.  Abra `AppDelegate.swift` e importe MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Agregar Hola siguiendo el método tooyour <code>AppDelegate</code> toohandle devoluciones de llamada de clase:
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

