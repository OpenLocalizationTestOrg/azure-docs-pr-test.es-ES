---
title: "Azure Active Directory B2C: adquisición de un token con una aplicación Android | Microsoft Docs"
description: "En este artículo le mostrará cómo toocreate una aplicación Android que utiliza AppAuth con identidades de usuario de Azure Active Directory B2C toomanage y autentica a los usuarios."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="6463f-103">Azure AD B2C: Inicio de sesión con una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="6463f-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="6463f-104">plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6463f-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="6463f-105">Esto permite a los desarrolladores tooleverage cualquier biblioteca desean toointegrate con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="6463f-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="6463f-106">tooaid a los desarrolladores en el uso de nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este una toodemonstrate forma tooconfigure 3ª parte bibliotecas tooconnect toohello Microsoft plataforma de identidad.</span><span class="sxs-lookup"><span data-stu-id="6463f-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="6463f-107">La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) será capaz de tooconnect toohello Microsoft Identity plataforma.</span><span class="sxs-lookup"><span data-stu-id="6463f-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="6463f-108">No se proporcionan correcciones para bibliotecas de terceros y no se ha realizado ninguna revisión de esas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="6463f-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="6463f-109">En este ejemplo se usa una biblioteca de entidad 3rd piden AppAuth que se ha probado la compatibilidad de escenarios básicos con hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6463f-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="6463f-110">Problemas y las solicitudes de características deben ser el proyecto de código abierto de la biblioteca de toohello dirigida.</span><span class="sxs-lookup"><span data-stu-id="6463f-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="6463f-111">Vea [este](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) artículo para más información.</span><span class="sxs-lookup"><span data-stu-id="6463f-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="6463f-112">Si es nuevo tooOAuth2 o OpenID Connect gran parte de esta configuración de ejemplo puede que no tenga mucho sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="6463f-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="6463f-113">Se recomienda que examine un breve [información general del protocolo de hello nos hemos mostradas aquí](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="6463f-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="6463f-114">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6463f-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="6463f-115">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="6463f-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="6463f-116">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="6463f-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="6463f-117">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="6463f-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="6463f-118">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6463f-118">Create an application</span></span>

<span data-ttu-id="6463f-119">A continuación, debe toocreate una aplicación en el directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="6463f-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="6463f-120">Esto proporciona información de Azure AD que necesita toocommunicate forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6463f-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="6463f-121">toocreate una aplicación móvil, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6463f-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="6463f-122">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="6463f-122">Be sure to:</span></span>

* <span data-ttu-id="6463f-123">Incluir un **Native Client** en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6463f-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="6463f-124">Hola copia **Id. de aplicación** decir tooyour asignado aplicación.</span><span class="sxs-lookup"><span data-stu-id="6463f-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="6463f-125">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="6463f-125">You will need this later.</span></span>
* <span data-ttu-id="6463f-126">Configurar un **URI de redireccionamiento** del cliente nativo (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="6463f-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="6463f-127">También lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="6463f-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="6463f-128">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="6463f-128">Create your policies</span></span>

<span data-ttu-id="6463f-129">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6463f-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6463f-130">Esta aplicación contiene una experiencia de identidad: una combinación de inicio de sesión y registro.</span><span class="sxs-lookup"><span data-stu-id="6463f-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="6463f-131">Deberá toocreate esta directiva, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="6463f-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="6463f-132">Cuando se crea la directiva de hello, no olvide:</span><span class="sxs-lookup"><span data-stu-id="6463f-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="6463f-133">Elija hello **nombre para mostrar** como un atributo de inicio de sesión en la directiva.</span><span class="sxs-lookup"><span data-stu-id="6463f-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="6463f-134">Elija hello **nombre para mostrar** y **Id. de objeto** notificaciones de la aplicación en cada directiva.</span><span class="sxs-lookup"><span data-stu-id="6463f-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="6463f-135">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="6463f-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="6463f-136">Hola copia **nombre** de cada directiva después de haberlo creado.</span><span class="sxs-lookup"><span data-stu-id="6463f-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="6463f-137">Deberían tener el prefijo de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="6463f-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="6463f-138">Necesitará el nombre de directiva de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="6463f-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="6463f-139">Después de crear las directivas, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6463f-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="6463f-140">Descargar código de muestra de Hola</span><span class="sxs-lookup"><span data-stu-id="6463f-140">Download hello sample code</span></span>

<span data-ttu-id="6463f-141">Hemos proporcionado un ejemplo de trabajo que usa AppAuth con Azure AD B2C [en GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="6463f-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="6463f-142">Puede descargar código de hello y ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="6463f-142">You can download hello code and run it.</span></span> <span data-ttu-id="6463f-143">Rápidamente puede empezar a trabajar con su propia aplicación con su propia configuración de Azure AD B2C siguiendo las instrucciones de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="6463f-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="6463f-144">ejemplo Hello es una modificación del ejemplo de Hola proporcionado por [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="6463f-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="6463f-145">Visite su toolearn de página más sobre AppAuth y sus características.</span><span class="sxs-lookup"><span data-stu-id="6463f-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="6463f-146">Modificar la aplicación toouse Azure AD B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="6463f-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="6463f-147">AppAuth admite Android API 16 (Jellybean) y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="6463f-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="6463f-148">Se recomienda usar API 23 y superior.</span><span class="sxs-lookup"><span data-stu-id="6463f-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="6463f-149">Configuración</span><span class="sxs-lookup"><span data-stu-id="6463f-149">Configuration</span></span>

<span data-ttu-id="6463f-150">Puede configurar la comunicación con Azure AD B2C detectar Hola especificar URI o especificando el extremo de autorización de Hola y URI de extremo token.</span><span class="sxs-lookup"><span data-stu-id="6463f-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="6463f-151">En cualquier caso, necesitará Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="6463f-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="6463f-152">Id. de inquilino (por ejemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="6463f-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="6463f-153">Nombre de la directiva (por ejemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="6463f-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="6463f-154">Si decide tooautomatically detectar extremo de autorización y token de hello URI, necesitará información de toofetch de la detección de hello URI.</span><span class="sxs-lookup"><span data-stu-id="6463f-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="6463f-155">detección de Hello URI puede generarse mediante la sustitución Hola inquilino\_hello directiva y el Id. de\_nombre Hola después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="6463f-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="6463f-156">A continuación, puede adquirir autorización hello y URI de extremo de token y crear un objeto de AuthorizationServiceConfiguration ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="6463f-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="6463f-157">En lugar de utilizar la autorización de detección tooobtain hello y URI de extremo de token, también puede especificar ellos explícitamente mediante la sustitución Hola inquilino\_hello directiva y el Id. de\_nombre en la dirección URL de hello:</span><span class="sxs-lookup"><span data-stu-id="6463f-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="6463f-158">Siguiente ejecución Hola código toocreate AuthorizationServiceConfiguration objeto:</span><span class="sxs-lookup"><span data-stu-id="6463f-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="6463f-159">Autorización</span><span class="sxs-lookup"><span data-stu-id="6463f-159">Authorizing</span></span>

<span data-ttu-id="6463f-160">Después de configurar o recuperar una configuración de servicio de autorización, es posible construir una autorización.</span><span class="sxs-lookup"><span data-stu-id="6463f-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="6463f-161">solicitar toocreate hello, necesitará Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="6463f-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="6463f-162">Id. de cliente (ejemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="6463f-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="6463f-163">URI de redireccionamiento con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="6463f-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="6463f-164">Ambos elementos se deberían haber guardado cuando [registró la aplicación](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="6463f-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="6463f-165">Consulte toohello [AppAuth guía](https://openid.github.io/AppAuth-Android/) en cómo toocomplete Hola resto del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="6463f-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="6463f-166">Si necesita tooquickly empezar a trabajar con una aplicación en funcionamiento, visite [nuestro ejemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="6463f-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="6463f-167">Siga los pasos de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter su propia configuración de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6463f-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="6463f-168">Estamos siempre toofeedback abierta y sugerencias.</span><span class="sxs-lookup"><span data-stu-id="6463f-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="6463f-169">Si tiene dificultades con este tema, o tiene las recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="6463f-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="6463f-170">Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="6463f-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

