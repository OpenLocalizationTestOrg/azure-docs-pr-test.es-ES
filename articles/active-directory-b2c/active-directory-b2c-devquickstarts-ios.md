---
title: "Adquisición de un token con una aplicación iOS - Azure AD B2C | Microsoft Docs"
description: "En este artículo le mostrará cómo toocreate una aplicación de iOS que utiliza AppAuth con identidades de usuario de Azure Active Directory B2C toomanage y autentica a los usuarios."
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
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="c9ea5-103">Azure AD B2C: Inicio de sesión con una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="c9ea5-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="c9ea5-104">plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="c9ea5-105">El uso de un protocolo estándar abierto ofrece más opciones a los desarrolladores al seleccionar un toointegrate de biblioteca con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="c9ea5-106">Hemos proporcionado en este tutorial y otros similares tooaid a los desarrolladores a escribir aplicaciones que se conectan toohello plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="c9ea5-107">La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) son tooconnect pueda toohello la plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="c9ea5-108">Microsoft no proporciona correcciones para bibliotecas de terceros y no se ha realizado ninguna revisión de esas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="c9ea5-109">Este ejemplo usa una biblioteca de terceros denominada AppAuth que se ha probado para la compatibilidad de escenarios básicos con hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="c9ea5-110">Problemas y las solicitudes de características deben ser el proyecto de código abierto de la biblioteca de toohello dirigida.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="c9ea5-111">Para obtener más información, consulte [este artículo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="c9ea5-112">Si es nuevo tooOAuth2 u OpenID Connect, gran parte de esta configuración de ejemplo puede que no tenga mucho sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="c9ea5-113">Se recomienda que examine un breve [información general del protocolo de hello nos hemos mostradas aquí](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="c9ea5-114">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c9ea5-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="c9ea5-115">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="c9ea5-116">Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="c9ea5-117">Antes de continuar, si no tiene un directorio B2C, [créelo](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="c9ea5-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="c9ea5-118">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="c9ea5-118">Create an application</span></span>
<span data-ttu-id="c9ea5-119">A continuación, debe toocreate una aplicación en el directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="c9ea5-120">registro de una aplicación Hola proporciona información de Azure AD que necesita toocommunicate forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="c9ea5-121">toocreate una aplicación móvil, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="c9ea5-122">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-122">Be sure to:</span></span>

* <span data-ttu-id="c9ea5-123">Incluir un **Native client** en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="c9ea5-124">Hola copia **Id. de aplicación** decir tooyour asignado aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="c9ea5-125">Necesitará este GUID más adelante.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-125">You need this GUID later.</span></span>
* <span data-ttu-id="c9ea5-126">Configure un **URI de redireccionamiento** con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="c9ea5-127">Necesitará este URI más adelante.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="c9ea5-128">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="c9ea5-128">Create your policies</span></span>
<span data-ttu-id="c9ea5-129">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c9ea5-130">Esta aplicación contiene una experiencia de identidad: una combinación de inicio de sesión y registro.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="c9ea5-131">Cree esta directiva, tal como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="c9ea5-132">Cuando se crea la directiva de hello, no olvide:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="c9ea5-133">En **atributos suscripción**, seleccione el atributo de hello **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="c9ea5-134">Puede seleccionar también otros atributos.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="c9ea5-135">En **notificaciones de la aplicación**, seleccione Hola notificaciones **nombre para mostrar** y **Id. de objeto del usuario**.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="c9ea5-136">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-136">You can select other claims as well.</span></span>
* <span data-ttu-id="c9ea5-137">Hola copia **nombre** de cada directiva después de haberlo creado.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="c9ea5-138">Tiene como prefijo el nombre de la directiva `b2c_1_` cuando se guarda la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="c9ea5-139">Necesita nombre de la directiva de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="c9ea5-140">Después de crear las directivas, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="c9ea5-141">Descargar código de muestra de Hola</span><span class="sxs-lookup"><span data-stu-id="c9ea5-141">Download hello sample code</span></span>
<span data-ttu-id="c9ea5-142">Hemos proporcionado un ejemplo de trabajo que usa AppAuth con Azure AD B2C [en GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="c9ea5-143">Puede descargar código de hello y ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-143">You can download hello code and run it.</span></span> <span data-ttu-id="c9ea5-144">toouse inquilino de su propia AD B2C de Azure, siga las instrucciones de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="c9ea5-145">En este ejemplo se creó siguiendo las instrucciones del archivo Léame de Hola por hello [iOS AppAuth del proyecto en GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="c9ea5-146">Para obtener más detalles sobre cómo funcionan los muestra de Hola y biblioteca de hello, hacer referencia a hello AppAuth README en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="c9ea5-147">Modificar la aplicación toouse Azure AD B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="c9ea5-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="c9ea5-148">AppAuth es compatible con iOS7 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="c9ea5-149">Sin embargo, es necesario toosupport sociales inicios de sesión de Google, SFSafariViewController que requiere iOS 9 o superior.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="c9ea5-150">Configuración</span><span class="sxs-lookup"><span data-stu-id="c9ea5-150">Configuration</span></span>

<span data-ttu-id="c9ea5-151">Puede configurar la comunicación con Azure AD B2C especificando el extremo de autorización de Hola y URI de extremo token.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="c9ea5-152">toogenerate estos URI, necesita Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="c9ea5-153">Identificador de inquilino (por ejemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="c9ea5-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="c9ea5-154">Nombre de la directiva (por ejemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="c9ea5-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="c9ea5-155">extremo de token de URI puede generarse mediante la sustitución Hola Hola inquilino\_hello directiva y el Id. de\_nombre Hola después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="c9ea5-156">extremo de autorización de URI puede generarse mediante la sustitución Hola Hola inquilino\_hello directiva y el Id. de\_nombre Hola después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="c9ea5-157">Siguiente ejecución Hola código toocreate AuthorizationServiceConfiguration objeto:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="c9ea5-158">Autorización</span><span class="sxs-lookup"><span data-stu-id="c9ea5-158">Authorizing</span></span>

<span data-ttu-id="c9ea5-159">Después de configurar o recuperar una configuración de servicio de autorización, es posible construir una autorización.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="c9ea5-160">solicitar toocreate hello, necesita Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="c9ea5-161">Id. de cliente (por ejemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="c9ea5-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="c9ea5-162">URI de redireccionamiento con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="c9ea5-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="c9ea5-163">Ambos elementos se deberían haber guardado cuando [registró la aplicación](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="c9ea5-164">tooset seguridad su toohello de redirección de Hola de toohandle aplicación URI con esquema personalizado de hello, necesita tooupdate lista de hello 'Esquemas de dirección URL' en su Info.pList:</span><span class="sxs-lookup"><span data-stu-id="c9ea5-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="c9ea5-165">Abra Info.pList.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-165">Open Info.pList.</span></span>
* <span data-ttu-id="c9ea5-166">Mantenga el mouse sobre una fila como 'Código de tipo de sistema operativo de agrupación' y haga clic en hello \+ símbolos.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="c9ea5-167">Cambie el nombre hello nueva fila 'tipos de URL'.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="c9ea5-168">Haga clic en hello flecha toohello a la izquierda del árbol de 'Tipos de dirección URL' tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="c9ea5-169">Haga clic en hello flecha toohello a la izquierda del árbol de hello tooopen 'Elemento 0'.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="c9ea5-170">Cambie el nombre del primer elemento bajo esquemas de elemento too'URL 0.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="c9ea5-171">Haga clic en hello flecha toohello a la izquierda del árbol de hello tooopen 'Esquemas de dirección URL'.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="c9ea5-172">En la columna de 'Value' hello, hay un campo en blanco toohello de 'Elemento 0' debajo 'Esquemas de dirección URL'.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="c9ea5-173">Establecer esquema único de la aplicación hello valor tooyour.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="c9ea5-174">valor de Hello debe coincidir con esquema de hello usado en URL de redireccionamiento al crear objeto de OIDAuthorizationRequest Hola.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="c9ea5-175">En nuestro ejemplo, hemos usado Hola esquema 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="c9ea5-176">Consulte toohello [AppAuth guía](https://openid.github.io/AppAuth-iOS/) en cómo toocomplete Hola resto del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="c9ea5-177">Si necesita tooquickly empezar a trabajar con una aplicación en funcionamiento, visite [nuestro ejemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="c9ea5-178">Siga los pasos de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter su propia configuración de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="c9ea5-179">Estamos siempre toofeedback abierta y sugerencias.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="c9ea5-180">Si tiene dificultades con este tema, o tiene las recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9ea5-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="c9ea5-181">Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="c9ea5-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
