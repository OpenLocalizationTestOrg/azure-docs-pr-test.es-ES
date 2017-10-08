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
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="4c3b9-103">Agregar aplicación de iOS de inicio de sesión tooan mediante una biblioteca de terceros con API Graph con el punto de conexión de hello v2.0</span><span class="sxs-lookup"><span data-stu-id="4c3b9-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="4c3b9-104">plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="4c3b9-105">Los desarrolladores pueden usar cualquier biblioteca que deseen toointegrate con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="4c3b9-106">toohelp a los desarrolladores usar nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este uno toodemonstrate la plataforma de identidad de Microsoft de tooconfigure bibliotecas de otros fabricantes tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="4c3b9-107">La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) toohello plataforma de identidad de Microsoft se pueden conectar.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="4c3b9-108">Con una aplicación Hola que crea en este tutorial, los usuarios pueden iniciar sesión en la organización de tootheir y, a continuación, busque otras personas de su organización mediante Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="4c3b9-109">Si es nuevo tooOAuth2 u OpenID Connect, gran parte de esta configuración de ejemplo puede que no tenga sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="4c3b9-110">Si este es el caso, le recomendamos que lea [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="4c3b9-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="4c3b9-111">Algunas características de la plataforma que tiene una expresión en Hola OAuth2 o estándares de OpenID Connect, como acceso condicional y administración de directivas de Intune, requieren toouse nuestro código abierto bibliotecas de identidad de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="4c3b9-112">el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="4c3b9-113">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4c3b9-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="4c3b9-114">Descarga del código desde GitHub</span><span class="sxs-lookup"><span data-stu-id="4c3b9-114">Download code from GitHub</span></span>
<span data-ttu-id="4c3b9-115">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="4c3b9-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="4c3b9-116">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="4c3b9-117">También se puede descargar el ejemplo de Hola y empezar a trabajar de forma inmediata:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="4c3b9-118">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="4c3b9-118">Register an app</span></span>
<span data-ttu-id="4c3b9-119">Crear una nueva aplicación en hello [portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga Hola pasos detallados en [cómo una aplicación con el punto de conexión de hello v2.0 tooregister](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4c3b9-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="4c3b9-120">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-120">Make sure to:</span></span>

* <span data-ttu-id="4c3b9-121">Hola copia **identificador de la aplicación** que está asignado tooyour aplicación porque lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="4c3b9-122">Agregar hello **Mobile** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="4c3b9-123">Hola copia **URI de redireccionamiento** desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="4c3b9-124">Debe usar el valor predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="4c3b9-125">Descargar Hola terceros NXOAuth2 biblioteca y crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="4c3b9-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="4c3b9-126">En este tutorial, usará hello OAuth2Client desde GitHub, que es una biblioteca de OAuth2 para Mac OS X y iOS (cacao y sus touch).</span><span class="sxs-lookup"><span data-stu-id="4c3b9-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="4c3b9-127">Esta biblioteca se basa en 10 de borrador de especificación de OAuth2 Hola. Implementa el perfil de aplicación nativa de Hola y es compatible con el extremo de autorización de saludo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="4c3b9-128">Éstos son todos los puntos de hello, deberá toointegrate a la plataforma de identidad de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="4c3b9-129">Agregar proyecto de biblioteca tooyour de hello mediante CocoaPods</span><span class="sxs-lookup"><span data-stu-id="4c3b9-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="4c3b9-130">CocoaPods es un administrador de dependencias para proyectos de Xcode.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="4c3b9-131">Administra automáticamente los pasos de la instalación anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="4c3b9-132">Agregue Hola después toothis podfile:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="4c3b9-133">Cargar hello podfile mediante CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="4c3b9-134">Así se creará una nueva área de trabajo de XCode que cargará.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="4c3b9-135">Explorar Hola estructura del proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="4c3b9-136">Hola siguiendo estructura está configurado para nuestro proyecto de esqueleto de hello:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="4c3b9-137">Una vista principal con una búsqueda UPN</span><span class="sxs-lookup"><span data-stu-id="4c3b9-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="4c3b9-138">Una vista de detalle para los datos de hello acerca del usuario seleccionado Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="4c3b9-139">Una vista de inicio de sesión donde un usuario puede iniciar sesión en el gráfico de toohello aplicación tooquery Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="4c3b9-140">Moveremos toovarious archivos en la autenticación de esqueleto tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="4c3b9-141">Otras partes del código de hello, como el código visual de hello, no pertenecen tooidentity pero se proporcionan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="4c3b9-142">Configure hello settings.plst archivo de biblioteca de Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="4c3b9-143">En el proyecto de inicio rápido de hello, abra hello `settings.plist` archivo.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="4c3b9-144">Reemplace los valores de hello de elementos de Hola de hello tooreflect Hola valores de una sección que usó en el portal de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="4c3b9-145">El código hará referencia a estos valores cada vez que usa Hola biblioteca de autenticación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="4c3b9-146">Hola `clientId` es Hola Id. de cliente de la aplicación que ha copiado desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="4c3b9-147">Hola `redirectUri` es dirección URL de redireccionamiento de hello ese portal Hola proporcionado.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="4c3b9-148">Configurar la biblioteca de NXOAuth2Client hello en su LoginViewController</span><span class="sxs-lookup"><span data-stu-id="4c3b9-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="4c3b9-149">biblioteca de Hello NXOAuth2Client requiere algunos tooget valores configurar.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="4c3b9-150">Después de completar esa tarea, puede usar Hola adquirida toocall token Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="4c3b9-151">Dado que `LoginView` se llamará cada vez que necesitamos tooauthenticate, tiene sentido tooput valores de configuración en el archivo toothat.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="4c3b9-152">Vamos a agregar algunos valores toohello `LoginViewController.m` de contexto del archivo tooset hello para la autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="4c3b9-153">Obtener más información acerca de los valores de hello seguir código de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-153">Details about hello values follow hello code.</span></span>
  
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

<span data-ttu-id="4c3b9-154">Echemos un vistazo a los detalles sobre el código de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="4c3b9-155">primera cadena de Hello es para `scopes`.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="4c3b9-156">Hola `User.Read` valor permite perfil básico de hello tooread de hello firmado en usuario.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="4c3b9-157">Puede aprender más acerca de todos los ámbitos disponibles de hello en [ámbitos de permiso de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="4c3b9-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="4c3b9-158">Para `authURL`, `loginURL`, `bhh`, y `tokenURL`, debe utilizar valores de hello indicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="4c3b9-159">Si utiliza código abierto de hello bibliotecas de identidad de Microsoft Azure, se extraen estos datos automáticamente mediante el uso de nuestro extremo de metadatos.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="4c3b9-160">Que hemos hecho esfuerzo Hola de extraer estos valores automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="4c3b9-161">Hola `keychain` valor es contenedor Hola Hola NXOAuth2Client biblioteca utilizará toocreate un toostore llaveros sus tokens.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="4c3b9-162">Si desea tooget inicio de sesión único (SSO) en numerosas aplicaciones, puede especificar Hola la misma cadena de claves en cada una de las aplicaciones y solicitar la utilización de Hola de esa cadena de claves en los derechos de Xcode.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="4c3b9-163">Esto se explica en hello documentación de Apple.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="4c3b9-164">rest Hola de estos valores son la biblioteca de hello toouse necesario y crear lugares para usted contexto toohello de toocarry valores.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="4c3b9-165">Creación de una caché de URL</span><span class="sxs-lookup"><span data-stu-id="4c3b9-165">Create a URL cache</span></span>
<span data-ttu-id="4c3b9-166">Dentro de `(void)viewDidLoad()`, siempre que se llama después de carga la vista hello, hello código siguiente primes de la memoria caché de nuestro uso.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="4c3b9-167">Agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-167">Add hello following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="4c3b9-168">Creación de una vista web para iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="4c3b9-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="4c3b9-169">Una vista Web puede solicitar al usuario de Hola de factores adicionales como mensaje de texto SMS (si está configurado) o devolver usuario de toohello de mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="4c3b9-170">Aquí configurará Hola WebView y, más adelante Hola de escritura código toohandle hello las devoluciones de llamada se realizarán en hello WebView de servicios de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

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

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="4c3b9-171">Invalidar la autenticación de hello WebView métodos toohandle</span><span class="sxs-lookup"><span data-stu-id="4c3b9-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="4c3b9-172">Hola tootell WebView lo que sucede cuando un usuario necesita toosign en según lo descrito anteriormente, puede pegar Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

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

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="4c3b9-173">Escribir código toohandle Hola resultado de solicitud de OAuth2 de Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="4c3b9-174">Hello código siguiente controlará redirectURL Hola que devuelve de hello WebView.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="4c3b9-175">Si la autenticación no era correcta, el código de hello volverá a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="4c3b9-176">Mientras tanto, biblioteca de hello proporcionará error Hola que puede ver en la consola de Hola o administrar de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

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

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="4c3b9-177">Configurar Hola contexto OAuth (denominado almacén de cuentas)</span><span class="sxs-lookup"><span data-stu-id="4c3b9-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="4c3b9-178">Aquí puede llamar a `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` en el almacén de una cuenta compartida de Hola para cada servicio que desea Hola aplicación toobe capaz de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="4c3b9-179">tipo de cuenta de Hello es una cadena que se utiliza como identificador para un servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="4c3b9-180">Dado que se obtiene acceso a API Graph hello, código de hello hace referencia tooit como `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="4c3b9-181">A continuación, configure un observador que le indicará cuando algo cambia con el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="4c3b9-182">Después de obtener el token de hello, devolver Hola usuario espera toohello `masterView`.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="4c3b9-183">Configurar hello toosearch de vista maestra y mostrar los usuarios Hola Hola API Graph</span><span class="sxs-lookup"><span data-stu-id="4c3b9-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="4c3b9-184">Una aplicación de Master-View-Controller (MVC) que se muestra hello devuelve datos en la cuadrícula de hello está más allá del ámbito de Hola de este tutorial y muchos tutoriales en línea se explican cómo toobuild uno.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="4c3b9-185">Todo este código está en archivo esqueleto Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="4c3b9-186">Sin embargo, deberá toodeal con algunas cosas en esta aplicación de MVC:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="4c3b9-187">Interceptar cuando un usuario escribe algo en el campo de búsqueda de Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="4c3b9-188">Proporcionar un objeto de datos back-toohello MasterView por lo que pueden mostrar los resultados de hello en cuadrícula Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="4c3b9-189">Lo haremos todo a continuación.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="4c3b9-190">Agregar un toosee de verificación si ha iniciado sesión</span><span class="sxs-lookup"><span data-stu-id="4c3b9-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="4c3b9-191">aplicación Hello no hace poco si Hola usuario no ha iniciado sesión, por lo que es toocheck inteligente si ya hay un token en memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="4c3b9-192">Si no es así, redirige toohello LoginView para hello usuario toosign en.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="4c3b9-193">Si recuerda, Hola mejor manera toodo acciones cuando se carga una vista es hello toouse `viewDidLoad()` método que nos proporciona Apple.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="4c3b9-194">Actualizar Hola vista de tabla cuando se reciben datos</span><span class="sxs-lookup"><span data-stu-id="4c3b9-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="4c3b9-195">Cuando Hola API Graph devuelve datos, necesita toodisplay Hola datos.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="4c3b9-196">Para simplificar, aquí tiene todos los Hola código tooupdate Hola la tabla.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="4c3b9-197">Solo puede pegar los valores correctos de hello en el código reutilizable MVC.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

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

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="4c3b9-198">Proporcionar un hello toocall de manera API Graph cuando alguien escribe en el campo de búsqueda de Hola</span><span class="sxs-lookup"><span data-stu-id="4c3b9-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="4c3b9-199">Cuando un usuario escribe una búsqueda en el cuadro de hello, necesita tooshove que, con toohello API Graph.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="4c3b9-200">Hola `GraphAPICaller` (clase), que van a generar en el siguiente código de hello, separa la funcionalidad de búsqueda de Hola de presentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="4c3b9-201">Por ahora, vamos a escribir código de hello que cualquier toohello de caracteres de búsqueda API Graph de fuentes de distribución.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="4c3b9-202">Para ello, proporciona un método denominado `lookupInGraph`, que toma la cadena de Hola que queremos toosearch para.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="4c3b9-203">Escribir un tooaccess de clase auxiliar Hola API Graph</span><span class="sxs-lookup"><span data-stu-id="4c3b9-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="4c3b9-204">Este es el núcleo de Hola de nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-204">This is hello core of our application.</span></span> <span data-ttu-id="4c3b9-205">Mientras que el resto de Hola inserta código en el modelo MVC predeterminada de Hola de Apple, aquí se pueden escribir gráfico de hello tooquery código como usuario de hello tipos y, a continuación, devolver los datos.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="4c3b9-206">Este es el código de hello y una explicación detallada lo sigue.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="4c3b9-207">Creación de un nuevo archivo de encabezado Objective C</span><span class="sxs-lookup"><span data-stu-id="4c3b9-207">Create a new Objective C header file</span></span>
<span data-ttu-id="4c3b9-208">Archivo de nombre hello `GraphAPICaller.h`y agregue el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="4c3b9-209">Se puede ver que estamos especificando un método que toma una cadena y devuelve un elemento completionBlock.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="4c3b9-210">Este completionBlock, tal y como habrá adivinado, actualizará Hola tabla proporcionando un objeto con datos rellenada en tiempo real como Hola búsquedas de usuario.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="4c3b9-211">Creación de un nuevo archivo Objective C</span><span class="sxs-lookup"><span data-stu-id="4c3b9-211">Create a new Objective C file</span></span>
<span data-ttu-id="4c3b9-212">Archivo de nombre hello `GraphAPICaller.m`y agregue Hola siguiendo el método.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

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

<span data-ttu-id="4c3b9-213">Analicemos pormenorizadamente este método.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="4c3b9-214">núcleo de Hola de este código es Hola `NXOAuth2Request`, método que toma parámetros de Hola que ya haya definido en el archivo de hello settings.plist.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="4c3b9-215">Hola primer paso es llamada de API Graph tooconstruct Hola right.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="4c3b9-216">Dado que se llama `/users`, especificar que mediante la anexión de recurso de la API de Graph toohello junto con la versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="4c3b9-217">Tiene sentido tooput estas opciones en un archivo de configuración externo ya estos pueden variar a medida que evoluciona Hola API.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="4c3b9-218">A continuación, hay parámetros de toospecify también proporcionará toohello llamada de API Graph.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="4c3b9-219">Es *muy importante* no coloque parámetros hello en el punto de conexión de hello recurso dado que se limpia para todos los caracteres de URI no conformes en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="4c3b9-220">Todo el código de consulta debe proporcionarse en parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="4c3b9-221">Es posible que observe que se llama a un método `convertParamsToDictionary` que todavía no se ha escrito.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="4c3b9-222">Vamos a hacer ahora al final de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="4c3b9-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="4c3b9-223">A continuación, vamos a usar hello `NXOAuth2Request` copia datos de tooget de método de hello API en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

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

<span data-ttu-id="4c3b9-224">Por último, echemos un vistazo a cómo devolver datos de hello toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="4c3b9-225">datos de Hello devuelve como en serie y necesita toobe deserializa y se cargan en un objeto puede usan ese hello MainViewController.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="4c3b9-226">Para ello, tiene el esqueleto de hello un `User.m/h` archivo que crea un objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="4c3b9-227">Rellenar ese objeto de usuario con información del gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-227">You populate that User object with information from hello graph.</span></span>

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


## <a name="run-hello-sample"></a><span data-ttu-id="4c3b9-228">Ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="4c3b9-228">Run hello sample</span></span>
<span data-ttu-id="4c3b9-229">Si ha utilizado el esqueleto de Hola o seguido junto con el tutorial Hola que ahora debe ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="4c3b9-230">Iniciar el simulador de Hola y haga clic en **iniciar sesión en** aplicación de hello toouse.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="4c3b9-231">Obtención de actualizaciones de seguridad para nuestro producto</span><span class="sxs-lookup"><span data-stu-id="4c3b9-231">Get security updates for our product</span></span>
<span data-ttu-id="4c3b9-232">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando hello [TechCenter de seguridad](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="4c3b9-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

