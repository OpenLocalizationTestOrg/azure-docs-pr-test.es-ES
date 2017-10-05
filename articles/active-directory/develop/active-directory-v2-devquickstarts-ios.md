---
title: "Incorporación del inicio de sesión a una aplicación iOS mediante el punto de conexión de Azure AD v2.0 | Microsoft Docs"
description: "Procedimiento para compilar una aplicación iOS con la que los usuarios pueden iniciar sesión utilizando su cuenta personal de Microsoft como sus cuentas profesionales o educativas mediante bibliotecas de terceros"
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
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="a14a2-103">Adición de inicio de sesión a una aplicación iOS mediante una biblioteca de terceros con la API Graph mediante la versión 2.0 del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="a14a2-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="a14a2-104">La plataforma Microsoft Identity utiliza estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a14a2-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="a14a2-105">Los desarrolladores pueden usar la biblioteca que quieran integrar con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="a14a2-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="a14a2-106">Para ayudar a los desarrolladores a utilizar nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este para demostrar cómo configurar bibliotecas de terceros con el objetivo de conectarse a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="a14a2-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="a14a2-107">La mayoría de las bibliotecas que implementan [la especificación OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) pueden conectarse a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="a14a2-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="a14a2-108">Con la aplicación que se crea en este tutorial, los usuarios podrán iniciar sesión en su organización y, después, buscar a otros de la misma organización mediante la API Graph.</span><span class="sxs-lookup"><span data-stu-id="a14a2-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="a14a2-109">Si no está familiarizado con OAuth2 o con OpenID Connect, es posible que gran parte de esta configuración de ejemplo no le sea relevante.</span><span class="sxs-lookup"><span data-stu-id="a14a2-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="a14a2-110">Si este es el caso, le recomendamos que lea [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="a14a2-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="a14a2-111">Algunas características de nuestra plataforma mencionadas en los estándares OAuth2 u OpenID Connect, como el acceso condicional y la administración de directivas de Intune, deben usar nuestras bibliotecas de código abierto de Microsoft Azure Identity.</span><span class="sxs-lookup"><span data-stu-id="a14a2-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="a14a2-112">No todas las características y escenarios de Azure Active Directory son compatibles con la versión 2.0 del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="a14a2-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="a14a2-113">Para determinar si debe utilizar la versión 2.0 del punto de conexión, obtenga información sobre las [limitaciones de esta versión](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a14a2-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="a14a2-114">Descarga del código desde GitHub</span><span class="sxs-lookup"><span data-stu-id="a14a2-114">Download code from GitHub</span></span>
<span data-ttu-id="a14a2-115">El código de este tutorial se conserva [en GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="a14a2-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="a14a2-116">Para continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="a14a2-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="a14a2-117">También puede descargar el ejemplo y comenzar a trabajar inmediatamente:</span><span class="sxs-lookup"><span data-stu-id="a14a2-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="a14a2-118">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="a14a2-118">Register an app</span></span>
<span data-ttu-id="a14a2-119">Cree una aplicación en el [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga los pasos que se detallan en [Cómo registrar una aplicación con el punto de conexión v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a14a2-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a14a2-120">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="a14a2-120">Make sure to:</span></span>

* <span data-ttu-id="a14a2-121">Copie el **id. de aplicación** asignado a su aplicación, ya que lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="a14a2-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="a14a2-122">Agregar la plataforma **Móvil** a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="a14a2-123">Copie el **URI de redireccionamiento** del portal.</span><span class="sxs-lookup"><span data-stu-id="a14a2-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="a14a2-124">Debe usar el valor predeterminado de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="a14a2-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="a14a2-125">Descarga de la biblioteca de terceros NXOAuth2 y creación de un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a14a2-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="a14a2-126">Para este tutorial, usaremos OAuth2Client desde GitHub, que es una biblioteca de OAuth2 para Mac OS X e iOS (Cocoa y Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="a14a2-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="a14a2-127">Esta biblioteca se basa en el borrador 10 de la especificación OAuth2.</span><span class="sxs-lookup"><span data-stu-id="a14a2-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="a14a2-128">Implementa el perfil de la aplicación nativa y admite el punto de conexión de autorización del usuario.</span><span class="sxs-lookup"><span data-stu-id="a14a2-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="a14a2-129">Esto es todo lo que vamos a necesitar para integrarlo con la plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="a14a2-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="a14a2-130">Adición de la biblioteca al proyecto mediante CocoaPods</span><span class="sxs-lookup"><span data-stu-id="a14a2-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="a14a2-131">CocoaPods es un administrador de dependencias para proyectos de Xcode.</span><span class="sxs-lookup"><span data-stu-id="a14a2-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="a14a2-132">Administra automáticamente los pasos de instalación anteriores.</span><span class="sxs-lookup"><span data-stu-id="a14a2-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="a14a2-133">Agregue lo siguiente a este podfile:</span><span class="sxs-lookup"><span data-stu-id="a14a2-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="a14a2-134">Cargue el archivo podfile mediante CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="a14a2-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="a14a2-135">Así se creará una nueva área de trabajo de XCode que cargará.</span><span class="sxs-lookup"><span data-stu-id="a14a2-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="a14a2-136">Exploración de la estructura del proyecto</span><span class="sxs-lookup"><span data-stu-id="a14a2-136">Explore the structure of the project</span></span>
<span data-ttu-id="a14a2-137">Hemos configurado la siguiente estructura para nuestro proyecto en el esquema:</span><span class="sxs-lookup"><span data-stu-id="a14a2-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="a14a2-138">Una vista principal con una búsqueda UPN</span><span class="sxs-lookup"><span data-stu-id="a14a2-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="a14a2-139">Una vista de detalle para los datos sobre el usuario seleccionado</span><span class="sxs-lookup"><span data-stu-id="a14a2-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="a14a2-140">Una vista de inicio de sesión que permite al usuario iniciar sesión en la aplicación para consultar el gráfico</span><span class="sxs-lookup"><span data-stu-id="a14a2-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="a14a2-141">Pasaremos por varios archivos del esquema para agregar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="a14a2-142">Aunque otras partes del código, como el código visual, no son relevantes para la identidad, se incluyen también.</span><span class="sxs-lookup"><span data-stu-id="a14a2-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="a14a2-143">Configuración del archivo settings.plst en la biblioteca</span><span class="sxs-lookup"><span data-stu-id="a14a2-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="a14a2-144">En el proyecto QuickStart, abra el archivo `settings.plist` .</span><span class="sxs-lookup"><span data-stu-id="a14a2-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="a14a2-145">Reemplace los valores de los elementos de la sección para que reflejen los usados en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a14a2-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="a14a2-146">El código hará referencia a estos valores cada vez que use la biblioteca de autenticación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a14a2-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="a14a2-147">`clientId` es el identificador de cliente de la aplicación que copió del portal.</span><span class="sxs-lookup"><span data-stu-id="a14a2-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="a14a2-148">`redirectUri` es la URL de redirección que ha proporcionado el portal.</span><span class="sxs-lookup"><span data-stu-id="a14a2-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="a14a2-149">Configuración de la biblioteca de NXOAuth2Client en LoginViewController</span><span class="sxs-lookup"><span data-stu-id="a14a2-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="a14a2-150">La biblioteca NXOAuth2Client requiere que se configuren algunos valores.</span><span class="sxs-lookup"><span data-stu-id="a14a2-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="a14a2-151">Después de completar esa tarea, puede usar el token obtenido para llamar a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="a14a2-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="a14a2-152">Como se llamará a `LoginView` cada vez que tengamos que autenticarnos, procede insertar los valores de configuración en ese archivo.</span><span class="sxs-lookup"><span data-stu-id="a14a2-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="a14a2-153">Vamos a agregar algunos valores al archivo `LoginViewController.m` para establecer el contexto de la autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="a14a2-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="a14a2-154">Después del código, encontrará los detalles de los valores.</span><span class="sxs-lookup"><span data-stu-id="a14a2-154">Details about the values follow the code.</span></span>
  
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

<span data-ttu-id="a14a2-155">Analicemos los detalles del código.</span><span class="sxs-lookup"><span data-stu-id="a14a2-155">Let's look at details about the code.</span></span>

<span data-ttu-id="a14a2-156">La primera cadena es para `scopes`.</span><span class="sxs-lookup"><span data-stu-id="a14a2-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="a14a2-157">El valor `User.Read` permite leer el perfil básico del usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="a14a2-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="a14a2-158">Puede obtener más información sobre todos los ámbitos disponibles en [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes)(Ámbitos de los permisos de Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="a14a2-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="a14a2-159">Para `authURL`, `loginURL`, `bhh` y `tokenURL`, debe utilizar los valores indicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a14a2-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="a14a2-160">Si usa las bibliotecas de código abierto de Microsoft Azure Identity, podemos obtener estos datos para que se utilice nuestro punto de conexión de metadatos.</span><span class="sxs-lookup"><span data-stu-id="a14a2-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="a14a2-161">Hemos hecho lo más difícil al extraer estos valores.</span><span class="sxs-lookup"><span data-stu-id="a14a2-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="a14a2-162">`keychain` es el contenedor que la biblioteca NXOAuth2Client utilizará para crear una cadena de claves con el fin de almacenar los tokens.</span><span class="sxs-lookup"><span data-stu-id="a14a2-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="a14a2-163">Si quiere obtener el inicio de sesión único (SSO) en varias aplicaciones, puede especificar la misma cadena de claves en cada una de las aplicaciones, así como solicitar el uso de esa cadena de claves en los derechos de XCode.</span><span class="sxs-lookup"><span data-stu-id="a14a2-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="a14a2-164">Esto se explica en la documentación de Apple.</span><span class="sxs-lookup"><span data-stu-id="a14a2-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="a14a2-165">El resto de estos valores se necesitan para usar la biblioteca y crear sitios para agregar los valores al contexto.</span><span class="sxs-lookup"><span data-stu-id="a14a2-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="a14a2-166">Creación de una caché de URL</span><span class="sxs-lookup"><span data-stu-id="a14a2-166">Create a URL cache</span></span>
<span data-ttu-id="a14a2-167">Dentro de `(void)viewDidLoad()`, que siempre se invoca después de cargar la vista, el código siguiente prepara una memoria caché para que podamos utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="a14a2-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="a14a2-168">Agregue el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="a14a2-168">Add the following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="a14a2-169">Creación de una vista web para iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="a14a2-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="a14a2-170">Gracias a las vistas web, podemos solicitar al usuario factores adicionales, como mensajes de texto SMS (si están configurados) o devolver mensajes de error al usuario.</span><span class="sxs-lookup"><span data-stu-id="a14a2-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="a14a2-171">Aquí también configuraremos la vista web y, después, escribiremos el código para controlar las devoluciones de llamada que se realizarán en la vista web de los servicios de identidad.</span><span class="sxs-lookup"><span data-stu-id="a14a2-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="a14a2-172">Invalidación de los métodos de la vista web para controlar la autenticación</span><span class="sxs-lookup"><span data-stu-id="a14a2-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="a14a2-173">Tal y como hemos explicado anteriormente, para indicar a la vista web lo que sucederá cuando un usuario tenga que iniciar sesión, puede pegar el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="a14a2-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

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

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="a14a2-174">Escriba el código para controlar el resultado de la solicitud de OAuth2.</span><span class="sxs-lookup"><span data-stu-id="a14a2-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="a14a2-175">El siguiente código controlará la URL de redireccionamiento que se devuelve desde la vista web.</span><span class="sxs-lookup"><span data-stu-id="a14a2-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="a14a2-176">Si la autenticación no se realizó correctamente, el código volverá a tratar de realizar la operación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="a14a2-177">Mientras tanto, la biblioteca proporcionará el error que se puede ver en la consola, o bien lo controlará de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="a14a2-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="a14a2-178">Configuración del contexto de OAuth (denominado "almacén de cuentas")</span><span class="sxs-lookup"><span data-stu-id="a14a2-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="a14a2-179">Aquí se puede llamar a `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` en el almacén de cuentas compartidas para cada servicio al que quiere que acceda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="a14a2-180">El tipo de cuenta es una cadena que se utiliza como identificador para un servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="a14a2-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="a14a2-181">Como va a acceder a la API Graph, el código hará referencia a ella como `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="a14a2-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="a14a2-182">Después, configuramos un observador que nos indicará cuándo cambia algo con el token.</span><span class="sxs-lookup"><span data-stu-id="a14a2-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="a14a2-183">Una vez obtenido el token, devolvemos al usuario a la `masterView`.</span><span class="sxs-lookup"><span data-stu-id="a14a2-183">After you get the token, you return the user back to the `masterView`.</span></span>

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

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="a14a2-184">Configuración de la vista principal para buscar y mostrar los usuarios de la API Graph</span><span class="sxs-lookup"><span data-stu-id="a14a2-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="a14a2-185">Las aplicaciones de control de vista principal (MVC) que muestran los datos devueltos en la cuadrícula no se tratan en este tutorial. Hay varios en línea que explican cómo crear una.</span><span class="sxs-lookup"><span data-stu-id="a14a2-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="a14a2-186">Todo este código se encuentra en el archivo de esquema.</span><span class="sxs-lookup"><span data-stu-id="a14a2-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="a14a2-187">Sin embargo, debemos tratar algunos aspectos en esta aplicación MVC:</span><span class="sxs-lookup"><span data-stu-id="a14a2-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="a14a2-188">Interceptar cuando el usuario escribe algo en el campo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="a14a2-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="a14a2-189">Proporcionar un objeto de datos a la vista principal para que pueda mostrar los resultados en la cuadrícula</span><span class="sxs-lookup"><span data-stu-id="a14a2-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="a14a2-190">Lo haremos todo a continuación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="a14a2-191">Adición de una comprobación para ver si hemos iniciado sesión</span><span class="sxs-lookup"><span data-stu-id="a14a2-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="a14a2-192">La aplicación no sirve de mucho si el usuario no ha iniciado sesión, por lo que se recomienda comprobar si ya hay un token en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="a14a2-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="a14a2-193">De lo contrario, volveremos a la vista de inicio de sesión para que el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="a14a2-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="a14a2-194">Como recordará, la mejor manera de realizar acciones cuando se carga una vista es usar el método `viewDidLoad()` que proporciona Apple.</span><span class="sxs-lookup"><span data-stu-id="a14a2-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="a14a2-195">Actualizar la vista de tabla cuando se reciben datos</span><span class="sxs-lookup"><span data-stu-id="a14a2-195">Update the Table View when data is received</span></span>
<span data-ttu-id="a14a2-196">Cuando la API Graph devuelve los datos, debe mostrarlos.</span><span class="sxs-lookup"><span data-stu-id="a14a2-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="a14a2-197">Para simplificar, este es todo el código que necesita si quiere actualizar la tabla.</span><span class="sxs-lookup"><span data-stu-id="a14a2-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="a14a2-198">Solo tiene que pegar los valores correctos en el código reutilizable de MVC.</span><span class="sxs-lookup"><span data-stu-id="a14a2-198">You can just paste the right values in your MVC boilerplate code.</span></span>

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


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="a14a2-199">Proporcionar una manera de llamar a la API Graph cuando alguien escribe en el campo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="a14a2-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="a14a2-200">Cuando un usuario escribe una búsqueda en el cuadro, hay que llevarla a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="a14a2-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="a14a2-201">La clase `GraphAPICaller` , que creará en el código siguiente, separa la funcionalidad de búsqueda de la de presentación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="a14a2-202">Por ahora, vamos a escribir el código que transmite los caracteres de búsqueda a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="a14a2-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="a14a2-203">Para ello, se proporciona el método denominado " `lookupInGraph`", que toma la cadena que queremos buscar.</span><span class="sxs-lookup"><span data-stu-id="a14a2-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

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

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="a14a2-204">Escritura de una clase auxiliar para acceder a la API Graph</span><span class="sxs-lookup"><span data-stu-id="a14a2-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="a14a2-205">Se trata del núcleo de nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-205">This is the core of our application.</span></span> <span data-ttu-id="a14a2-206">Mientras que el resto consistía en insertar código en el patrón MVC predeterminado de Apple, aquí escribimos código para consultar el gráfico cuando el usuario escribe y devolver los datos.</span><span class="sxs-lookup"><span data-stu-id="a14a2-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="a14a2-207">Aquí se muestra el código y, abajo de este, proporcionamos una explicación detallada.</span><span class="sxs-lookup"><span data-stu-id="a14a2-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="a14a2-208">Creación de un nuevo archivo de encabezado Objective C</span><span class="sxs-lookup"><span data-stu-id="a14a2-208">Create a new Objective C header file</span></span>
<span data-ttu-id="a14a2-209">Denomine al archivo `GraphAPICaller.h`y agregue el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="a14a2-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="a14a2-210">Se puede ver que estamos especificando un método que toma una cadena y devuelve un elemento completionBlock.</span><span class="sxs-lookup"><span data-stu-id="a14a2-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="a14a2-211">Este elemento completionBlock, como se habrá imaginado, actualizará la tabla proporcionando un objeto con datos rellenados en tiempo real cuando el usuario realiza las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="a14a2-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="a14a2-212">Creación de un nuevo archivo Objective C</span><span class="sxs-lookup"><span data-stu-id="a14a2-212">Create a new Objective C file</span></span>
<span data-ttu-id="a14a2-213">Denomine al archivo `GraphAPICaller.m`y agregue el método siguiente.</span><span class="sxs-lookup"><span data-stu-id="a14a2-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

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
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
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

<span data-ttu-id="a14a2-214">Analicemos pormenorizadamente este método.</span><span class="sxs-lookup"><span data-stu-id="a14a2-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="a14a2-215">El núcleo de este código se encuentra en el método `NXOAuth2Request`, que toma los parámetros que ya hemos definido dentro del archivo settings.plist.</span><span class="sxs-lookup"><span data-stu-id="a14a2-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="a14a2-216">El primer paso consiste en crear la llamada correcta a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="a14a2-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="a14a2-217">Como vamos a llamar a `/users`, lo especificamos anexándolo a nuestro recurso de API Graph junto con la versión.</span><span class="sxs-lookup"><span data-stu-id="a14a2-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="a14a2-218">Se recomienda colocarlos en un archivo de configuración externo, ya que pueden cambiar cuando evolucione la API.</span><span class="sxs-lookup"><span data-stu-id="a14a2-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="a14a2-219">Después, tenemos que especificar los parámetros, que también proporcionaremos a la llamada de API Graph.</span><span class="sxs-lookup"><span data-stu-id="a14a2-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="a14a2-220">Es *muy importante* que no coloque los parámetros en el punto de conexión de los recursos, ya que se eliminan todos los caracteres del identificador URI no compatibles en el entorno de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a14a2-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="a14a2-221">Todo el código de consulta debe indicarse en los parámetros.</span><span class="sxs-lookup"><span data-stu-id="a14a2-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="a14a2-222">Es posible que observe que se llama a un método `convertParamsToDictionary` que todavía no se ha escrito.</span><span class="sxs-lookup"><span data-stu-id="a14a2-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="a14a2-223">Lo haremos ahora al final del archivo:</span><span class="sxs-lookup"><span data-stu-id="a14a2-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="a14a2-224">A continuación, vamos a usar el método `NXOAuth2Request` para obtener los datos de la API en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a14a2-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

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
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="a14a2-225">Finalmente, veamos cómo se devuelven los datos al método MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="a14a2-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="a14a2-226">Los datos los obtenemos serializados; tenemos que deserializarlos y cargarlos en un objeto que pueda utilizar MainViewController.</span><span class="sxs-lookup"><span data-stu-id="a14a2-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="a14a2-227">Por este motivo, el esquema tiene un archivo `User.m/h` que crea un objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="a14a2-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="a14a2-228">Rellenamos ese objeto de usuario con la información del gráfico.</span><span class="sxs-lookup"><span data-stu-id="a14a2-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
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


## <a name="run-the-sample"></a><span data-ttu-id="a14a2-229">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="a14a2-229">Run the sample</span></span>
<span data-ttu-id="a14a2-230">Si ha utilizado el esquema o ha seguido todo el tutorial, la aplicación debería ejecutarse ahora.</span><span class="sxs-lookup"><span data-stu-id="a14a2-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="a14a2-231">Inicie el simulador y haga clic en **Iniciar sesión** para usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a14a2-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="a14a2-232">Obtención de actualizaciones de seguridad para nuestro producto</span><span class="sxs-lookup"><span data-stu-id="a14a2-232">Get security updates for our product</span></span>
<span data-ttu-id="a14a2-233">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite la página [TechCenter de seguridad](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de documentos informativos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a14a2-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

