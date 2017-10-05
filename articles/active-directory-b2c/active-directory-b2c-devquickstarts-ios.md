---
title: "Adquisición de un token con una aplicación iOS - Azure AD B2C | Microsoft Docs"
description: "En este artículo se mostrará cómo crear una aplicación iOS que usa AppAuth con Azure Active Directory B2C para administrar las identidades de usuario y autenticar usuarios."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="858ce-103">Azure AD B2C: Inicio de sesión con una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="858ce-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="858ce-104">La plataforma Microsoft Identity utiliza estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="858ce-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="858ce-105">Usar un protocolo estándar abierto ofrece más opciones a los desarrolladores cuando se selecciona una biblioteca para integrarla con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="858ce-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="858ce-106">Proporcionamos este tutorial y otros similares para ayudar a los desarrolladores a escribir aplicaciones que se conecten con la plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="858ce-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="858ce-107">La mayoría de las bibliotecas que implementan [la especificación OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) pueden conectarse a la plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="858ce-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="858ce-108">Microsoft no proporciona correcciones para bibliotecas de terceros y no se ha realizado ninguna revisión de esas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="858ce-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="858ce-109">Este ejemplo usa una biblioteca de terceros llamada AppAuth cuya compatibilidad se ha probado en escenarios básicos con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="858ce-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="858ce-110">Los problemas y las solicitudes de características deben dirigirse al proyecto de código abierto de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="858ce-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="858ce-111">Para obtener más información, consulte [este artículo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="858ce-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="858ce-112">Si no está familiarizado con OAuth2 o con OpenID Connect, es posible que gran parte de esta configuración de ejemplo no tenga mucho sentido para usted.</span><span class="sxs-lookup"><span data-stu-id="858ce-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="858ce-113">Se recomienda que consulte una breve [información general sobre el protocolo que hemos documentado aquí](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="858ce-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="858ce-114">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="858ce-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="858ce-115">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="858ce-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="858ce-116">Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="858ce-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="858ce-117">Antes de continuar, si no tiene un directorio B2C, [créelo](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="858ce-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="858ce-118">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="858ce-118">Create an application</span></span>
<span data-ttu-id="858ce-119">A continuación, debe crear una aplicación en su directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="858ce-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="858ce-120">El registro de la aplicación proporciona a Azure AD la información que necesita para comunicarse de forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="858ce-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="858ce-121">Para crear una aplicación móvil, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="858ce-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="858ce-122">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="858ce-122">Be sure to:</span></span>

* <span data-ttu-id="858ce-123">Incluir un **cliente nativo** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="858ce-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="858ce-124">Copiar el **identificador de aplicación** asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="858ce-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="858ce-125">Necesitará este GUID más adelante.</span><span class="sxs-lookup"><span data-stu-id="858ce-125">You need this GUID later.</span></span>
* <span data-ttu-id="858ce-126">Configure un **URI de redireccionamiento** con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="858ce-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="858ce-127">Necesitará este URI más adelante.</span><span class="sxs-lookup"><span data-stu-id="858ce-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="858ce-128">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="858ce-128">Create your policies</span></span>
<span data-ttu-id="858ce-129">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="858ce-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="858ce-130">Esta aplicación contiene una experiencia de identidad: una combinación de inicio de sesión y registro.</span><span class="sxs-lookup"><span data-stu-id="858ce-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="858ce-131">Cree esta directiva, tal como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="858ce-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="858ce-132">Al crear la directiva, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="858ce-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="858ce-133">En **Atributos de registro**, seleccione **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="858ce-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="858ce-134">Puede seleccionar también otros atributos.</span><span class="sxs-lookup"><span data-stu-id="858ce-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="858ce-135">En **Notificaciones de aplicación**, seleccione las notificaciones **Nombre para mostrar** e **Identificador de objeto del usuario**.</span><span class="sxs-lookup"><span data-stu-id="858ce-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="858ce-136">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="858ce-136">You can select other claims as well.</span></span>
* <span data-ttu-id="858ce-137">Copiar el **nombre** de cada directiva después de crearla.</span><span class="sxs-lookup"><span data-stu-id="858ce-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="858ce-138">El nombre de la directiva tiene como prefijo `b2c_1_` al guardarla.</span><span class="sxs-lookup"><span data-stu-id="858ce-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="858ce-139">Necesitará el nombre de la directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="858ce-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="858ce-140">Después de crear las directivas, está listo para compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="858ce-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="858ce-141">Descarga del código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="858ce-141">Download the sample code</span></span>
<span data-ttu-id="858ce-142">Hemos proporcionado un ejemplo de trabajo que usa AppAuth con Azure AD B2C [en GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="858ce-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="858ce-143">Puede descargar el código y ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="858ce-143">You can download the code and run it.</span></span> <span data-ttu-id="858ce-144">Para usar su propio inquilino de Azure AD B2C, siga las instrucciones que aparecen en el archivo [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="858ce-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="858ce-145">Este ejemplo se creó con las instrucciones del archivo README del [proyecto AppAuth de iOS en GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="858ce-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="858ce-146">Para más detalles sobre cómo funcionan el ejemplo y la biblioteca, haga referencia al archivo README de AppAuth en GitHub.</span><span class="sxs-lookup"><span data-stu-id="858ce-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="858ce-147">Modificación de la aplicación para usar Azure AD B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="858ce-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="858ce-148">AppAuth es compatible con iOS7 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="858ce-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="858ce-149">Sin embargo, para admitir inicios de sesión sociales en Google, se necesita SFSafariViewController, que requiere iOS 9 o superior.</span><span class="sxs-lookup"><span data-stu-id="858ce-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="858ce-150">Configuración</span><span class="sxs-lookup"><span data-stu-id="858ce-150">Configuration</span></span>

<span data-ttu-id="858ce-151">Puede configurar la comunicación con Azure AD B2C si especifica tanto los URI del punto de conexión de autorización como del punto de conexión del token.</span><span class="sxs-lookup"><span data-stu-id="858ce-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="858ce-152">Para generar estos URI, necesita la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="858ce-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="858ce-153">Identificador de inquilino (por ejemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="858ce-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="858ce-154">Nombre de la directiva (por ejemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="858ce-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="858ce-155">El URI de punto de conexión de token se puede generar si se reemplaza Tenant\_ID y Policy\_Name en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="858ce-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="858ce-156">El URI de punto de conexión de autorización se puede generar si se reemplaza Tenant\_ID y Policy\_Name en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="858ce-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="858ce-157">Ejecute el código siguiente para crear el objeto AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="858ce-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="858ce-158">Autorización</span><span class="sxs-lookup"><span data-stu-id="858ce-158">Authorizing</span></span>

<span data-ttu-id="858ce-159">Después de configurar o recuperar una configuración de servicio de autorización, es posible construir una autorización.</span><span class="sxs-lookup"><span data-stu-id="858ce-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="858ce-160">Para crear la solicitud, necesita la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="858ce-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="858ce-161">Id. de cliente (por ejemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="858ce-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="858ce-162">URI de redireccionamiento con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="858ce-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="858ce-163">Ambos elementos se deberían haber guardado cuando [registró la aplicación](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="858ce-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="858ce-164">Para configurar la aplicación y controlar el redireccionamiento al URI con el esquema personalizado, deberá actualizar la lista de "Esquemas de dirección URL" en Info.pList:</span><span class="sxs-lookup"><span data-stu-id="858ce-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="858ce-165">Abra Info.pList.</span><span class="sxs-lookup"><span data-stu-id="858ce-165">Open Info.pList.</span></span>
* <span data-ttu-id="858ce-166">Mantenga el puntero sobre una fila como "Código de tipo de SO del lote" y haga clic en el símbolo \+.</span><span class="sxs-lookup"><span data-stu-id="858ce-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="858ce-167">Cambie el nombre de la fila nueva "Tipos de dirección URL".</span><span class="sxs-lookup"><span data-stu-id="858ce-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="858ce-168">Haga clic en la flecha a la izquierda de "Tipos de dirección URL" para abrir el árbol.</span><span class="sxs-lookup"><span data-stu-id="858ce-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="858ce-169">Haga clic en la flecha situada a la izquierda de "Elemento 0" para abrir el árbol.</span><span class="sxs-lookup"><span data-stu-id="858ce-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="858ce-170">Cambie el nombre del primer elemento de Elemento 0 a "Combinaciones de URL".</span><span class="sxs-lookup"><span data-stu-id="858ce-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="858ce-171">Haga clic en la flecha a la izquierda de "Combinaciones de URL" para abrir el árbol.</span><span class="sxs-lookup"><span data-stu-id="858ce-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="858ce-172">En la columna "Valor", hay un campo en blanco a la izquierda de "Elemento 0" debajo "Combinaciones de URL".</span><span class="sxs-lookup"><span data-stu-id="858ce-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="858ce-173">Establezca el valor al esquema único de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="858ce-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="858ce-174">Debe coincidir con el esquema de redirectURL cuando se crea el objeto OIDAuthorizationRequest.</span><span class="sxs-lookup"><span data-stu-id="858ce-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="858ce-175">En el ejemplo, usamos el esquema "com.onmicrosoft.fabrikamb2c.exampleapp".</span><span class="sxs-lookup"><span data-stu-id="858ce-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="858ce-176">Consulte la [guía de AppAuth](https://openid.github.io/AppAuth-iOS/) sobre cómo completar el resto del proceso.</span><span class="sxs-lookup"><span data-stu-id="858ce-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="858ce-177">Si necesita comenzar rápidamente con una aplicación de trabajo, revise [nuestro ejemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="858ce-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="858ce-178">Siga los pasos que aparecen en el archivo [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) para escribir su propia configuración de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="858ce-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="858ce-179">Siempre estamos abiertos a todo tipo de comentarios y sugerencias.</span><span class="sxs-lookup"><span data-stu-id="858ce-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="858ce-180">Si tiene dificultades para completar este tema o tiene recomendaciones para mejorar este contenido, agradecemos que escriba sus comentarios en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="858ce-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="858ce-181">Si tiene solicitudes de características, agréguelas a [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="858ce-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
