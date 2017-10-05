---
title: "Cambios en el punto de conexión de Azure AD v2.0 | Microsoft Docs"
description: "Una descripción de los cambios que se están realizando en los protocolos de vista previa pública del modelo de aplicación v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="2e586-103">Actualizaciones importantes de los protocolos de autenticación de la versión 2.0</span><span class="sxs-lookup"><span data-stu-id="2e586-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="2e586-104">¡Atención, desarrolladores!</span><span class="sxs-lookup"><span data-stu-id="2e586-104">Attention developers!</span></span> <span data-ttu-id="2e586-105">Durante las próximas dos semanas realizaremos algunas actualizaciones en nuestros protocolos de autenticación v2.0 que pueden suponer importantes cambios para cualquier aplicación que se haya escrito durante el período de vista previa.</span><span class="sxs-lookup"><span data-stu-id="2e586-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="2e586-106">¿Qué se ve afectado?</span><span class="sxs-lookup"><span data-stu-id="2e586-106">Who does this affect?</span></span>
<span data-ttu-id="2e586-107">Todas las aplicaciones que se hayan escrito para usar la versión 2.0 del punto de conexión de autenticación convergente.</span><span class="sxs-lookup"><span data-stu-id="2e586-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="2e586-108">Puede encontrar más información sobre el punto de conexión v2.0 [aquí](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e586-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="2e586-109">Si ha creado una aplicación con el punto de conexión v2.0 codificando directamente al protocolo v2.0, mediante cualquiera de nuestros productos de software intermedio de web: OpenID Connect o OAuth, o con otra biblioteca de terceros para realizar la autenticación, debe prepararse para realizar pruebas en sus proyectos y para hacer cambios si es necesario.</span><span class="sxs-lookup"><span data-stu-id="2e586-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="2e586-110">¿Qué no se ve afectado?</span><span class="sxs-lookup"><span data-stu-id="2e586-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="2e586-111">Las aplicaciones que se han escrito con el punto de conexión de autenticación de Azure AD de producción.</span><span class="sxs-lookup"><span data-stu-id="2e586-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="2e586-112">Este protocolo es inamovible y no experimentará ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="2e586-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="2e586-113">Además, si su aplicación usa **solo** nuestra biblioteca de autenticación de Azure AD (ADAL) para realizar la autenticación, no tendrá que cambiar nada.</span><span class="sxs-lookup"><span data-stu-id="2e586-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="2e586-114">ADAL ha protegido su aplicación de los cambios.</span><span class="sxs-lookup"><span data-stu-id="2e586-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="2e586-115">¿Cuáles son los cambios?</span><span class="sxs-lookup"><span data-stu-id="2e586-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="2e586-116">Eliminación del valor x5t de los encabezados JWT</span><span class="sxs-lookup"><span data-stu-id="2e586-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="2e586-117">El punto de conexión de la versión 2.0 usa ampliamente tokens JWT, los cuales contienen una sección de parámetros de encabezado con metadatos pertinentes sobre el token.</span><span class="sxs-lookup"><span data-stu-id="2e586-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="2e586-118">Si descodifica el encabezado de uno de nuestros JWT actuales, encontrará algo como esto:</span><span class="sxs-lookup"><span data-stu-id="2e586-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="2e586-119">En donde las propiedades "x5t" y "kid" identifican la clave pública que se debe usar para validar la firma del token, una vez recuperada del punto de conexión de metadatos OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2e586-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="2e586-120">El cambio que vamos a realizar consiste en eliminar la propiedad "x5t".</span><span class="sxs-lookup"><span data-stu-id="2e586-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="2e586-121">Puede seguir utilizando los mismos mecanismos para validar los tokens, pero debe basarse solo en la propiedad "kid" para recuperar la clave pública correcta, como se especifica en el protocolo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2e586-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2e586-122">**Su tarea: Asegúrese de que la aplicación no depende de la existencia del valor x5t.**</span><span class="sxs-lookup"><span data-stu-id="2e586-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="2e586-123">Eliminación de profile_info</span><span class="sxs-lookup"><span data-stu-id="2e586-123">Removing profile_info</span></span>
<span data-ttu-id="2e586-124">Anteriormente, el punto de conexión v2.0 ha estado devolviendo un objeto JSON con codificación base64 en las respuestas de token llamadas `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="2e586-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="2e586-125">Al solicitar un token de acceso al punto de conexión v2.0 enviando una solicitud a:</span><span class="sxs-lookup"><span data-stu-id="2e586-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="2e586-126">La respuesta era como el siguiente objeto JSON:</span><span class="sxs-lookup"><span data-stu-id="2e586-126">The response would look like the following JSON object:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="2e586-127">El valor `profile_info` contenía información sobre el usuario que había iniciado sesión en la aplicación: su nombre para mostrar, nombre, apellido, dirección de correo electrónico, identificador y demás.</span><span class="sxs-lookup"><span data-stu-id="2e586-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="2e586-128">Principalmente, `profile_info` se usaba para almacenar en caché los tokens y para la visualización.</span><span class="sxs-lookup"><span data-stu-id="2e586-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="2e586-129">Vamos a quitar el valor `profile_info` , pero no se preocupe, seguiremos proporcionando esta información a los desarrolladores en otro sitio.</span><span class="sxs-lookup"><span data-stu-id="2e586-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="2e586-130">En lugar de `profile_info`, el punto de conexión v2.0 devolverá ahora un valor `id_token` en cada respuesta de token:</span><span class="sxs-lookup"><span data-stu-id="2e586-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="2e586-131">Puede descodificar y analizar el id_token para recuperar la misma información que hasta ahora recibía de profile_info.</span><span class="sxs-lookup"><span data-stu-id="2e586-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="2e586-132">El id_token es un token web JSON (JWT), con el contenido especificado por OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2e586-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="2e586-133">El código para hacerlo es muy similar: basta con extraer el segmento central (el cuerpo) del id_token y descodificarlo en base64 para obtener acceso al objeto JSON que se encuentra dentro.</span><span class="sxs-lookup"><span data-stu-id="2e586-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="2e586-134">En las próximas dos semanas, debe codificar la aplicación para recuperar la información de usuario bien desde `id_token` o `profile_info`, lo que esté presente.</span><span class="sxs-lookup"><span data-stu-id="2e586-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="2e586-135">De este modo, cuando se realice el cambio, la aplicación podrá controlar sin problemas la transición desde `profile_info` a `id_token` sin interrupción.</span><span class="sxs-lookup"><span data-stu-id="2e586-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e586-136">**Su tarea: Asegúrese de que la aplicación no depende de la existencia del valor `profile_info`.**</span><span class="sxs-lookup"><span data-stu-id="2e586-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="2e586-137">Eliminación de id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="2e586-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="2e586-138">De forma similar a `profile_info`, también estamos quitando el parámetro `id_token_expires_in` de las respuestas.</span><span class="sxs-lookup"><span data-stu-id="2e586-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="2e586-139">Anteriormente, el punto de conexión v2.0 devolvía un valor para `id_token_expires_in` junto con cada respuesta id_token, por ejemplo, en una respuesta de autorización:</span><span class="sxs-lookup"><span data-stu-id="2e586-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="2e586-140">O en una respuesta de token:</span><span class="sxs-lookup"><span data-stu-id="2e586-140">Or in a token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="2e586-141">El valor `id_token_expires_in` indica el número de segundos durante los que el id_token mantiene su validez.</span><span class="sxs-lookup"><span data-stu-id="2e586-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="2e586-142">Ahora, vamos a quitar el valor `id_token_expires_in` completamente.</span><span class="sxs-lookup"><span data-stu-id="2e586-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="2e586-143">En su lugar, puede usar las notificaciones estándar de OpenID Connect `nbf` y `exp` para examinar la validez del id_token.</span><span class="sxs-lookup"><span data-stu-id="2e586-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="2e586-144">Consulte la [referencia de los tokens de la versión 2.0](active-directory-v2-tokens.md) para obtener más información sobre estas notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2e586-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e586-145">**Su tarea: Asegúrese de que la aplicación no depende de la existencia del valor `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="2e586-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="2e586-146">Modificación de las notificaciones devueltas por scope = openid</span><span class="sxs-lookup"><span data-stu-id="2e586-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="2e586-147">Este cambio será el más significativo, de hecho, afectará a casi todas las aplicaciones que utilizan el punto de conexión de la versión 2.0.</span><span class="sxs-lookup"><span data-stu-id="2e586-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="2e586-148">Muchas aplicaciones envían solicitudes al punto de conexión de v2.0 mediante el ámbito `openid`, como:</span><span class="sxs-lookup"><span data-stu-id="2e586-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="2e586-149">Hoy en día, cuando el usuario concede el consentimiento para el ámbito `openid`, la aplicación recibe una gran cantidad de información sobre el usuario en el id_token resultante.</span><span class="sxs-lookup"><span data-stu-id="2e586-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="2e586-150">Estas notificaciones pueden incluir su nombre, nombre de usuario preferido, dirección de correo electrónico, identificador de objeto y más.</span><span class="sxs-lookup"><span data-stu-id="2e586-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="2e586-151">En esta actualización se está cambiando la información a la que el ámbito `openid` permite el acceso a la aplicación, para cumplir mejor con la especificación de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2e586-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="2e586-152">El ámbito `openid` solo permitirá que el usuario inicie sesión en la aplicación y que esta reciba un identificador específico de aplicación para el usuario en la notificación `sub` de id_token.</span><span class="sxs-lookup"><span data-stu-id="2e586-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="2e586-153">Las notificaciones en id_token que tengan únicamente el ámbito `openid` concedido, estarán desprovistas de toda información personal identificable.</span><span class="sxs-lookup"><span data-stu-id="2e586-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="2e586-154">Algunos ejemplos de notificaciones id_token son:</span><span class="sxs-lookup"><span data-stu-id="2e586-154">Example id_token claims are:</span></span>

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

<span data-ttu-id="2e586-155">Si desea obtener información personal identificable (PII) acerca del usuario en la aplicación, esta tendrá que solicitar permisos adicionales al usuario.</span><span class="sxs-lookup"><span data-stu-id="2e586-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="2e586-156">Estamos introduciendo soporte para dos nuevos ámbitos de la especificación OpenID Connect: los ámbitos `email` y `profile`, que permiten hacerlo.</span><span class="sxs-lookup"><span data-stu-id="2e586-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="2e586-157">El ámbito `email` es muy sencillo: permite que la aplicación acceda a la dirección de correo electrónico principal del usuario a través de la notificación `email` en id_token.</span><span class="sxs-lookup"><span data-stu-id="2e586-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="2e586-158">Tenga en cuenta que la notificación `email` no siempre estará presente en los id_tokens, solo se incluye si está disponible en el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="2e586-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="2e586-159">El ámbito `profile` ofrece a la aplicación acceso a toda la demás información básica sobre el usuario: su nombre, el nombre de usuario preferido, identificador de objeto y demás.</span><span class="sxs-lookup"><span data-stu-id="2e586-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="2e586-160">Esto le permite codificar la aplicación en un modo de divulgación mínima, puede pedir al usuario solo el conjunto de información que la aplicación necesita para hacer su trabajo.</span><span class="sxs-lookup"><span data-stu-id="2e586-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="2e586-161">Si desea continuar obteniendo el conjunto completo de información de usuario que la aplicación está recibiendo actualmente, tiene que incluir los tres ámbitos en las solicitudes de autorización:</span><span class="sxs-lookup"><span data-stu-id="2e586-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="2e586-162">La aplicación puede comenzar enviando los ámbitos `email` y `profile` de forma inmediata, el punto de conexión v2.0 aceptará estos dos ámbitos e iniciará la solicitud de permisos a los usuarios según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2e586-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="2e586-163">Sin embargo, el cambio en la interpretación del ámbito `openid` no surtirá efecto durante unas semanas.</span><span class="sxs-lookup"><span data-stu-id="2e586-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e586-164">**Su tarea: Agregar los ámbitos `profile` y `email` si su aplicación necesita información sobre el usuario.**</span><span class="sxs-lookup"><span data-stu-id="2e586-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="2e586-165">Tenga en cuenta que la ADAL incluirá ambos permisos en las solicitudes de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2e586-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="2e586-166">Eliminación de la barra diagonal final del emisor.</span><span class="sxs-lookup"><span data-stu-id="2e586-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="2e586-167">Anteriormente, el valor de emisor que aparece en los tokens del punto de conexión v2.0 tenía la forma</span><span class="sxs-lookup"><span data-stu-id="2e586-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="2e586-168">Donde el GUID era el valor tenantId del inquilino de Azure AD que emitió el token.</span><span class="sxs-lookup"><span data-stu-id="2e586-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="2e586-169">Con estos cambios, el valor del emisor se convierte en</span><span class="sxs-lookup"><span data-stu-id="2e586-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="2e586-170">en ambos tokens y en el documento de detección de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2e586-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e586-171">**Su tarea: Asegúrese de que la aplicación acepta el valor del emisor con y sin una barra diagonal final durante la validación del emisor.**</span><span class="sxs-lookup"><span data-stu-id="2e586-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="2e586-172">¿Por qué se han hecho los cambios?</span><span class="sxs-lookup"><span data-stu-id="2e586-172">Why change?</span></span>
<span data-ttu-id="2e586-173">El motivo principal para la introducción de estos cambios es mantener la compatibilidad con la especificación estándar de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2e586-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="2e586-174">A través de la compatibilidad con OpenID Connect, esperamos minimizar las diferencias entre la integración con los servicios de identidad de Microsoft y con otros servicios de identidad en la industria.</span><span class="sxs-lookup"><span data-stu-id="2e586-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="2e586-175">Queremos que los desarrolladores puedan utilizar sus bibliotecas de autenticación de código abierto preferidas sin tener que modificar las bibliotecas para adaptarse a las diferencias de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e586-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="2e586-176">¿Qué puede hacer?</span><span class="sxs-lookup"><span data-stu-id="2e586-176">What can you do?</span></span>
<span data-ttu-id="2e586-177">En este momento, puede comenzar a realizar todos los cambios que se han descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2e586-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="2e586-178">Inmediatamente, debe:</span><span class="sxs-lookup"><span data-stu-id="2e586-178">You should immediately:</span></span>

1. <span data-ttu-id="2e586-179">**Eliminar las dependencias del parámetro de encabezado `x5t`.**</span><span class="sxs-lookup"><span data-stu-id="2e586-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="2e586-180">**Controlar correctamente la transición de `profile_info` a `id_token` en las respuestas de token.**</span><span class="sxs-lookup"><span data-stu-id="2e586-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="2e586-181">**Eliminar las dependencias del parámetro de respuesta `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="2e586-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="2e586-182">**Agregar los ámbitos `profile` y `email` a la aplicación si la aplicación necesita información básica del usuario.**</span><span class="sxs-lookup"><span data-stu-id="2e586-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="2e586-183">**Aceptar los valores de emisor en los tokens con y sin una barra diagonal final.**</span><span class="sxs-lookup"><span data-stu-id="2e586-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="2e586-184">Nuestra documentación [Vista previa del modelo de aplicaciones v2.0: protocolos - OAuth 2.0 y OpenID Connect](active-directory-v2-protocols.md) ya se ha actualizado para reflejar estos cambios, por lo que puede utilizarla como referencia a la hora de actualizar el código.</span><span class="sxs-lookup"><span data-stu-id="2e586-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="2e586-185">Si tiene más preguntas relacionadas con los cambios, no dude en ponerse en contacto con nosotros en Twitter en @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="2e586-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="2e586-186">¿Con qué frecuencia se realizan cambios en los protocolos?</span><span class="sxs-lookup"><span data-stu-id="2e586-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="2e586-187">No se prevén más cambios sustanciales en los protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2e586-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="2e586-188">Hemos juntado todos estos cambios en una sola versión de forma intencionada, para que no tenga que volver a pasar pronto por este tipo de proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="2e586-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="2e586-189">Por supuesto que seguiremos agregando características al servicio de autenticación convergente de v2.0, de las que esperamos que saque provecho, pero estos cambios deberían ser aditivos y por tanto no será necesario cambiar el código existente.</span><span class="sxs-lookup"><span data-stu-id="2e586-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="2e586-190">Por último, queremos darles las gracias por probar las funciones durante el período de vista previa.</span><span class="sxs-lookup"><span data-stu-id="2e586-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="2e586-191">Las ideas y las experiencias de nuestros primeros usuarios han tenido un valor inestimables hasta ahora, y esperamos que sigan compartiendo sus opiniones e ideas con nosotros.</span><span class="sxs-lookup"><span data-stu-id="2e586-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="2e586-192">¡ Feliz codificación!</span><span class="sxs-lookup"><span data-stu-id="2e586-192">Happy coding!</span></span>

<span data-ttu-id="2e586-193">Microsoft Identity Division</span><span class="sxs-lookup"><span data-stu-id="2e586-193">The Microsoft Identity Division</span></span>

