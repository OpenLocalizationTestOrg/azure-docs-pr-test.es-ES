---
title: "Introducción al uso de iOS de Azure AD v2 | Microsoft Docs"
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="9ffbb-103">Utilice la biblioteca de autenticación de Microsoft (MSAL) para obtener un token para la API Graph de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="9ffbb-104">Abra `ViewController.swift` y reemplace el código por:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="9ffbb-105">Más información</span><span class="sxs-lookup"><span data-stu-id="9ffbb-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="9ffbb-106">Obtención de un token de usuario interactivamente</span><span class="sxs-lookup"><span data-stu-id="9ffbb-106">Getting a user token interactively</span></span>
<span data-ttu-id="9ffbb-107">La llamada al método `acquireToken` genera una ventana en el explorador que pide al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="9ffbb-108">Las aplicaciones suelen requerir que un usuario inicie sesión interactivamente la primera vez que requieren acceso a un recurso protegido, o cuando se produce un error en una operación silenciosa para adquirir un token (por ejemplo, si la contraseña de usuario caducó).</span><span class="sxs-lookup"><span data-stu-id="9ffbb-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="9ffbb-109">Obtención de un token de usuario en silencio</span><span class="sxs-lookup"><span data-stu-id="9ffbb-109">Getting a user token silently</span></span>
<span data-ttu-id="9ffbb-110">El método `acquireTokenSilent` controla la renovación y las adquisiciones de tokens sin la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="9ffbb-111">Después de ejecutar `acquireToken` por primera vez, `acquireTokenSilent` es el método usado habitualmente para obtener los tokens empleados para acceder a recursos protegidos en las llamadas posteriores, ya que las llamadas para solicitar o renovar los tokens se realizan en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="9ffbb-112">Es posible que `acquireTokenSilent` genere eventualmente un error; por ejemplo, si el usuario ha cerrado la sesión o ha cambiado su contraseña en otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="9ffbb-113">Si MSAL detecta que el problema puede solucionarse requiriendo una acción interactiva, desencadena una excepción `MSALErrorCode.interactionRequired`.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="9ffbb-114">La aplicación puede abordar esta excepción de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="9ffbb-115">Realizar una llamada a `acquireToken` inmediatamente, lo que ocasiona que el usuario tenga que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="9ffbb-116">Este patrón se da normalmente en aplicaciones en línea en las que no hay ningún contenido sin conexión en la aplicación disponible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="9ffbb-117">La aplicación de ejemplo generada en esta instalación guiada utiliza este patrón: puede verla en acción la primera vez que se ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="9ffbb-118">Dado que ningún usuario usó la aplicación, `applicationContext.users().first` contendrá un valor null y se iniciará una excepción ` MSALErrorCode.interactionRequired `.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="9ffbb-119">El código del ejemplo entonces trata la excepción llamando a `acquireToken`, lo que provoca que se pida al usuario que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="9ffbb-120">Las aplicaciones también pueden hacer una indicación visual al usuario de que se requiere un inicio de sesión interactivo, de manera que el usuario pueda seleccionar el momento adecuado para iniciar sesión, o la aplicación puede reintentar `acquireTokenSilent` en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="9ffbb-121">Esto se utiliza normalmente cuando el usuario puede utilizar otras funciones de la aplicación sin que se le interrumpa: por ejemplo, hay contenido sin conexión disponible en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="9ffbb-122">En este caso, el usuario puede decidir el momento en que desea iniciar sesión para tener acceso al recurso protegido, o actualizar la información no actualizada; o puede decidir que la aplicación vuelva a intentar `acquireTokenSilent` cuando se restaure la red después de estar no disponible temporalmente.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="9ffbb-123">Llamada a la API Graph de Microsoft con el token que acaba de obtener</span><span class="sxs-lookup"><span data-stu-id="9ffbb-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="9ffbb-124">Agregue el siguiente método nuevo a `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="9ffbb-125">El método se utiliza para realizar una solicitud `GET` a la API de Microsoft Graph con un *encabezado de autorización HTTP*:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="9ffbb-126">Llamada de REST con una API protegida</span><span class="sxs-lookup"><span data-stu-id="9ffbb-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="9ffbb-127">En esta aplicación de ejemplo, el método `getContentWithToken()` se usa para realizar una solicitud HTTP `GET` a un recurso protegido que requiere un token y, a continuación, devolver el contenido al autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="9ffbb-128">Este método agrega el token adquirido al *encabezado de autorización HTTP*.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="9ffbb-129">En este ejemplo, el recurso es el punto de conexión *me* de la API Graph de Microsoft, que muestra información de perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="9ffbb-130">Configuración del cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="9ffbb-130">Set up sign-out</span></span>

<span data-ttu-id="9ffbb-131">Agregue el método siguiente a `ViewController.swift` para cerrar la sesión del usuario:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="9ffbb-132">Más información sobre el cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="9ffbb-132">More info on sign-out</span></span>

<span data-ttu-id="9ffbb-133">El método `signoutButton` anterior quita al usuario de la caché de usuario MSAL: esto indicará a MSAL de manera eficaz que olvide al usuario actual de forma que una solicitud futura para adquirir un token solo se completará correctamente si se realiza para ser interactiva.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="9ffbb-134">Aunque la aplicación en este ejemplo es compatible con un solo usuario, MSAL admite escenarios en los que es posible iniciar sesión en varias cuentas al mismo tiempo: un ejemplo es una aplicación de correo electrónico donde un usuario tiene varias cuentas.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="9ffbb-135">Registro de la devolución de llamada</span><span class="sxs-lookup"><span data-stu-id="9ffbb-135">Register the callback</span></span>

<span data-ttu-id="9ffbb-136">Una vez que el usuario se autentica, el explorador lo redirige a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ffbb-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="9ffbb-137">Siga estos pasos para registrar esta devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="9ffbb-138">Abra `AppDelegate.swift` e importe MSAL:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="9ffbb-139">Agregue el método siguiente a su clase <code>AppDelegate</code> para administrar las devoluciones de llamada:</span><span class="sxs-lookup"><span data-stu-id="9ffbb-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

