---
title: "Azure Active Directory B2C: adquisición de un token con una aplicación Android | Microsoft Docs"
description: "En este artículo se mostrará cómo crear una aplicación Android que usa AppAuth con Azure Active Directory B2C para administrar las identidades de usuario y autenticar usuarios."
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
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="12acd-103">Azure AD B2C: Inicio de sesión con una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="12acd-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="12acd-104">La plataforma Microsoft Identity utiliza estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="12acd-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="12acd-105">Esto permite a los desarrolladores aprovechar cualquier biblioteca que deseen integrar con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="12acd-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="12acd-106">Para ayudar a los desarrolladores en el uso de nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales, como este, para demostrar cómo configurar bibliotecas de terceros para conectarse a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="12acd-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="12acd-107">La mayoría de las bibliotecas que implementan [la especificación OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) podrán conectarse a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="12acd-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="12acd-108">No se proporcionan correcciones para bibliotecas de terceros y no se ha realizado ninguna revisión de esas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="12acd-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="12acd-109">Este ejemplo usa una biblioteca de terceros llamada AppAuth cuya compatibilidad se ha probado en escenarios básicos con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="12acd-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="12acd-110">Los problemas y las solicitudes de características deben dirigirse al proyecto de código abierto de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="12acd-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="12acd-111">Vea [este](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) artículo para más información.</span><span class="sxs-lookup"><span data-stu-id="12acd-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="12acd-112">Si no está familiarizado con OAuth2 o con OpenID Connect, es posible que gran parte de esta configuración de ejemplo no tenga mucho sentido para usted.</span><span class="sxs-lookup"><span data-stu-id="12acd-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="12acd-113">Se recomienda que consulte una breve [información general sobre el protocolo que hemos documentado aquí](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="12acd-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="12acd-114">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="12acd-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="12acd-115">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="12acd-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="12acd-116">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="12acd-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="12acd-117">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="12acd-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="12acd-118">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="12acd-118">Create an application</span></span>

<span data-ttu-id="12acd-119">A continuación, debe crear una aplicación en su directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="12acd-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="12acd-120">Esto proporciona a Azure AD la información que necesita para comunicarse de forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12acd-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="12acd-121">Para crear una aplicación móvil, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="12acd-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="12acd-122">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="12acd-122">Be sure to:</span></span>

* <span data-ttu-id="12acd-123">Incluir un **cliente nativo** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12acd-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="12acd-124">Copiar el **identificador de aplicación** asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12acd-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="12acd-125">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="12acd-125">You will need this later.</span></span>
* <span data-ttu-id="12acd-126">Configurar un **URI de redireccionamiento** del cliente nativo (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="12acd-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="12acd-127">También lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="12acd-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="12acd-128">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="12acd-128">Create your policies</span></span>

<span data-ttu-id="12acd-129">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="12acd-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="12acd-130">Esta aplicación contiene una experiencia de identidad: una combinación de inicio de sesión y registro.</span><span class="sxs-lookup"><span data-stu-id="12acd-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="12acd-131">Es necesario crear esta directiva, tal como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="12acd-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="12acd-132">Al crear la directiva, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12acd-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="12acd-133">Elija el **nombre para mostrar** como atributo de registro en la directiva.</span><span class="sxs-lookup"><span data-stu-id="12acd-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="12acd-134">Elija las notificaciones de aplicación de **nombre para mostrar** e **id. de objeto** de cada directiva.</span><span class="sxs-lookup"><span data-stu-id="12acd-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="12acd-135">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="12acd-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="12acd-136">Copiar el **nombre** de cada directiva después de crearla.</span><span class="sxs-lookup"><span data-stu-id="12acd-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="12acd-137">Debe tener el prefijo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="12acd-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="12acd-138">Necesitará el nombre de la directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="12acd-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="12acd-139">Después de crear las directivas, está listo para compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12acd-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="12acd-140">Descarga del código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="12acd-140">Download the sample code</span></span>

<span data-ttu-id="12acd-141">Hemos proporcionado un ejemplo de trabajo que usa AppAuth con Azure AD B2C [en GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="12acd-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="12acd-142">Puede descargar el código y ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="12acd-142">You can download the code and run it.</span></span> <span data-ttu-id="12acd-143">Puede comenzar rápidamente con su propia aplicación con su propia configuración de Azure AD B2C si sigue las instrucciones que aparecen en el archivo [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="12acd-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="12acd-144">El ejemplo es una modificación del ejemplo que proporciona [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="12acd-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="12acd-145">Visite la página para más información sobre AppAuth y sus características.</span><span class="sxs-lookup"><span data-stu-id="12acd-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="12acd-146">Modificación de la aplicación para usar Azure AD B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="12acd-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="12acd-147">AppAuth admite Android API 16 (Jellybean) y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="12acd-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="12acd-148">Se recomienda usar API 23 y superior.</span><span class="sxs-lookup"><span data-stu-id="12acd-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="12acd-149">Configuración</span><span class="sxs-lookup"><span data-stu-id="12acd-149">Configuration</span></span>

<span data-ttu-id="12acd-150">Puede configurar la comunicación con Azure AD B2C si especifica el URI de detección o tanto los URI del punto de conexión de autorización y del punto de conexión del token.</span><span class="sxs-lookup"><span data-stu-id="12acd-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="12acd-151">Cualquiera sea el caso, necesitará la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="12acd-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="12acd-152">Id. de inquilino (por ejemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="12acd-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="12acd-153">Nombre de la directiva (por ejemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="12acd-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="12acd-154">Si elige detectar automáticamente los URI de punto de conexión de autorización y token, deberá recuperar información del URI de detección.</span><span class="sxs-lookup"><span data-stu-id="12acd-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="12acd-155">El URI de detección se puede generar si se reemplaza Tenant\_ID y Policy\_Name en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="12acd-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="12acd-156">A continuación, puede adquirir los URI de punto de conexión de autenticación y token y, además, crear un objeto AuthorizationServiceConfiguration; para ello, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12acd-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

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
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="12acd-157">En lugar de usar la detección para obtener los URI de punto de conexión de autorización y token, también puede especificarlos si reemplaza Tenant\_ID y Policy\_Name en las direcciones URL que aparecen a continuación:</span><span class="sxs-lookup"><span data-stu-id="12acd-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="12acd-158">Ejecute el código siguiente para crear el objeto AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="12acd-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="12acd-159">Autorización</span><span class="sxs-lookup"><span data-stu-id="12acd-159">Authorizing</span></span>

<span data-ttu-id="12acd-160">Después de configurar o recuperar una configuración de servicio de autorización, es posible construir una autorización.</span><span class="sxs-lookup"><span data-stu-id="12acd-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="12acd-161">Para crear la solicitud, necesitará la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="12acd-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="12acd-162">Id. de cliente (ejemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="12acd-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="12acd-163">URI de redireccionamiento con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="12acd-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="12acd-164">Ambos elementos se deberían haber guardado cuando [registró la aplicación](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="12acd-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="12acd-165">Consulte la [guía de AppAuth](https://openid.github.io/AppAuth-Android/) sobre cómo completar el resto del proceso.</span><span class="sxs-lookup"><span data-stu-id="12acd-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="12acd-166">Si necesita comenzar rápidamente con una aplicación de trabajo, revise [nuestro ejemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="12acd-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="12acd-167">Siga los pasos que aparecen en el archivo [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) para escribir su propia configuración de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="12acd-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="12acd-168">Siempre estamos abiertos a todo tipo de comentarios y sugerencias.</span><span class="sxs-lookup"><span data-stu-id="12acd-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="12acd-169">Si tiene dificultades para completar este tema o tiene recomendaciones para mejorar este contenido, agradecemos que escriba sus comentarios en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="12acd-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="12acd-170">Si tiene solicitudes de características, agréguelas a [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="12acd-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

