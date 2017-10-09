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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="de0cf-103">Usar Hola biblioteca de autenticación de Microsoft (MSAL) tooget un token para hello API Graph de Microsoft</span><span class="sxs-lookup"><span data-stu-id="de0cf-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="de0cf-104">Abra `ViewController.swift` y reemplace el código de hello con:</span><span class="sxs-lookup"><span data-stu-id="de0cf-104">Open `ViewController.swift` and replace hello code with:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="de0cf-105">Más información</span><span class="sxs-lookup"><span data-stu-id="de0cf-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="de0cf-106">Obtención de un token de usuario interactivamente</span><span class="sxs-lookup"><span data-stu-id="de0cf-106">Getting a user token interactively</span></span>
<span data-ttu-id="de0cf-107">Llamar a hello `acquireToken` resultados del método en una ventana de explorador preguntar Hola toosign de usuario en.</span><span class="sxs-lookup"><span data-stu-id="de0cf-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="de0cf-108">Las aplicaciones suelen requieran un toosign de usuario en forma interactiva Hola primera vez necesiten tooaccess un recurso protegido, o cuando una operación silenciosa tooacquire se produce un error en un token (por ejemplo, contraseña del usuario de hello expiró).</span><span class="sxs-lookup"><span data-stu-id="de0cf-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="de0cf-109">Obtención de un token de usuario en silencio</span><span class="sxs-lookup"><span data-stu-id="de0cf-109">Getting a user token silently</span></span>
<span data-ttu-id="de0cf-110">Hola `acquireTokenSilent` método controla renovación sin ninguna interacción del usuario y adquisiciones de símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="de0cf-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="de0cf-111">Después de `acquireToken` se ejecuta para hello primera vez, `acquireTokenSilent` es Hola método usada tooobtain tokens utilizados tooaccess recursos para llamadas posteriores - protegidos como llamadas toorequest o renovar los tokens se realizan en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="de0cf-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="de0cf-112">Finalmente, `acquireTokenSilent` se producirá un error: por ejemplo, usuario de hello ha cerrado la sesión, o ha cambiado su contraseña en otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="de0cf-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="de0cf-113">Cuando MSAL detecta que se puede resolver el problema de hello exigiendo una acción interactiva, que se activa un `MSALErrorCode.interactionRequired` excepción.</span><span class="sxs-lookup"><span data-stu-id="de0cf-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="de0cf-114">La aplicación puede abordar esta excepción de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="de0cf-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="de0cf-115">Realizar una llamada con `acquireToken` inmediatamente, lo que produce preguntar Hola toosign de usuario en.</span><span class="sxs-lookup"><span data-stu-id="de0cf-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="de0cf-116">Este patrón se utiliza normalmente en aplicaciones en línea que no hay ningún contenido sin conexión en la aplicación hello disponibles para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="de0cf-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="de0cf-117">aplicación de ejemplo de Hola generado por este programa de instalación interactiva utiliza este patrón: puede verlo en Hola de acción a primera vez que ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="de0cf-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="de0cf-118">Dado que ningún usuario utilizado alguna vez la aplicación hello, `applicationContext.users().first` contendrá un valor null y un ` MSALErrorCode.interactionRequired ` excepción.</span><span class="sxs-lookup"><span data-stu-id="de0cf-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="de0cf-119">Hola código de ejemplo de Hola, a continuación, identificadores de Hola excepción mediante una llamada a `acquireToken` resultante en Preguntar Hola usuario toosign en.</span><span class="sxs-lookup"><span data-stu-id="de0cf-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="de0cf-120">Las aplicaciones también pueden realizar un usuario de toohello de indicación visual en un inicio de sesión interactivo se requiere para el usuario de hello puede seleccionar Hola momento toosign en, o puede volver a intentar la aplicación hello `acquireTokenSilent` en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="de0cf-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="de0cf-121">Se suele utilizar al usuario Hola puede usar otras funciones de aplicación hello sin que se va a interrumpir; por ejemplo, hay contenido sin conexión disponibles en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="de0cf-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="de0cf-122">En este caso, puede decidir usuario hello cuando quieran toosign en recursos de hello protegido tooaccess, o toorefresh Hola información obsoleta o la aplicación puede decidir tooretry `acquireTokenSilent` cuando se restaure la red después de estar disponible temporalmente.</span><span class="sxs-lookup"><span data-stu-id="de0cf-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="de0cf-123">Llamar a la API de Microsoft Graph hello mediante el símbolo (token) de hello que acabara de obtener</span><span class="sxs-lookup"><span data-stu-id="de0cf-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="de0cf-124">Agregar método de Hola de nuevo a continuación demasiado`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="de0cf-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="de0cf-125">Este método es toomake usado un `GET` solicitud contra Hola API de Graph de Microsoft mediante un *encabezado de autorización HTTP*:</span><span class="sxs-lookup"><span data-stu-id="de0cf-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="de0cf-126">Llamada de REST con una API protegida</span><span class="sxs-lookup"><span data-stu-id="de0cf-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="de0cf-127">En esta aplicación de ejemplo Hola `getContentWithToken()` método es toomake usa HTTP `GET` solicitud para un recurso protegido que requiera un llamador de contenido toohello Hola símbolo (token) y, a continuación, vuelva.</span><span class="sxs-lookup"><span data-stu-id="de0cf-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="de0cf-128">Este método agrega el token de hello adquirido en hello *encabezado de autorización HTTP*.</span><span class="sxs-lookup"><span data-stu-id="de0cf-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="de0cf-129">En este ejemplo, recurso de Hola es hello Microsoft Graph API *me* endpoint – que muestra información de perfil del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="de0cf-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="de0cf-130">Configuración del cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="de0cf-130">Set up sign-out</span></span>

<span data-ttu-id="de0cf-131">Agregar Hola siguiente método demasiado`ViewController.swift` toosign usuario hello:</span><span class="sxs-lookup"><span data-stu-id="de0cf-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="de0cf-132">Más información sobre el cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="de0cf-132">More info on sign-out</span></span>

<span data-ttu-id="de0cf-133">Hola `signoutButton` método quita usuario Hola Hola caché de usuario MSAL: Esto eficazmente indicará MSAL tooforget Hola actual usuario para una solicitud futura tooacquire un token solo tendrá éxito si se realiza toobe interactivo.</span><span class="sxs-lookup"><span data-stu-id="de0cf-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="de0cf-134">Aunque la aplicación hello en este ejemplo es compatible con un solo usuario, MSAL es compatible con escenarios donde pueden firmarse varias cuentas en hello vez: un ejemplo es una aplicación de correo electrónico donde un usuario tiene varias cuentas.</span><span class="sxs-lookup"><span data-stu-id="de0cf-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="de0cf-135">Registrar la devolución de llamada de Hola</span><span class="sxs-lookup"><span data-stu-id="de0cf-135">Register hello callback</span></span>

<span data-ttu-id="de0cf-136">Una vez que se autentica el usuario hello, Hola redirige Hola usuario espera toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="de0cf-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="de0cf-137">Siga estos pasos hello tooregister esta devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="de0cf-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="de0cf-138">Abra `AppDelegate.swift` e importe MSAL:</span><span class="sxs-lookup"><span data-stu-id="de0cf-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="de0cf-139">Agregar Hola siguiendo el método tooyour <code>AppDelegate</code> toohandle devoluciones de llamada de clase:</span><span class="sxs-lookup"><span data-stu-id="de0cf-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
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

