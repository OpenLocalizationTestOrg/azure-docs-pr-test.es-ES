---
title: "el punto de conexión de aaaChanges toohello Azure AD v2.0 | Documentos de Microsoft"
description: "Una descripción de los cambios que se están realizando protocolos de versión preliminar pública de toohello aplicación modelo v2.0."
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
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="923c3-103">Importantes actualizaciones toohello v2.0 protocolos de autenticación</span><span class="sxs-lookup"><span data-stu-id="923c3-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="923c3-104">¡Atención, desarrolladores!</span><span class="sxs-lookup"><span data-stu-id="923c3-104">Attention developers!</span></span> <span data-ttu-id="923c3-105">A través de hello siguientes dos semanas, realizaremos algunas actualizaciones tooour v2.0 protocolos de autenticación que pueden significar últimos cambios para las aplicaciones que haya escrito durante el período de vista previa.</span><span class="sxs-lookup"><span data-stu-id="923c3-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="923c3-106">¿Qué se ve afectado?</span><span class="sxs-lookup"><span data-stu-id="923c3-106">Who does this affect?</span></span>
<span data-ttu-id="923c3-107">Las aplicaciones que se han escrito toouse Hola v2.0 convergen extremo de autenticación</span><span class="sxs-lookup"><span data-stu-id="923c3-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="923c3-108">Puede encontrar más información en el punto de conexión de hello v2.0 [aquí](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="923c3-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="923c3-109">Si ha creado una aplicación con el punto de conexión de hello v2.0 codificando directamente toohello v2.0 protocolo, con cualquiera de nuestros middlewares web OpenID Connect o OAuth, o mediante otro 3rd autenticación de tooperform de bibliotecas de entidades, debe estar preparado tootest los proyectos y asegúrese de cambia si es necesario.</span><span class="sxs-lookup"><span data-stu-id="923c3-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="923c3-110">¿Qué no se ve afectado?</span><span class="sxs-lookup"><span data-stu-id="923c3-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="923c3-111">Las aplicaciones que se han escrito en el extremo de autenticación de Azure AD de producción de hello,</span><span class="sxs-lookup"><span data-stu-id="923c3-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="923c3-112">Este protocolo es inamovible y no experimentará ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="923c3-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="923c3-113">Además, si la aplicación **sólo** usa la biblioteca ADAL tooperform la autenticación, no tiene toochange nada.</span><span class="sxs-lookup"><span data-stu-id="923c3-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="923c3-114">AAL ha protegido la aplicación de los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="923c3-115">¿Qué cambios de hello?</span><span class="sxs-lookup"><span data-stu-id="923c3-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="923c3-116">Quitar el valor de hello x5t de encabezados JWT</span><span class="sxs-lookup"><span data-stu-id="923c3-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="923c3-117">el punto de conexión de Hello v2.0 usa tokens JWT exhaustivamente, que contiene una sección de parámetros de encabezado con metadatos relevantes sobre el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="923c3-118">Si descodificar encabezado Hola de uno de nuestros JWTs actuales, encontrará algo parecido:</span><span class="sxs-lookup"><span data-stu-id="923c3-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="923c3-119">En ambas propiedades de "x5t" y "kid" hello identifican la clave pública de Hola que debe ser la firma del token de toovalidate usado hello, una vez recuperados del extremo de metadatos de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="923c3-120">cambio de Hello que estamos realizando aquí es propiedad de Hola "x5t" de tooremove.</span><span class="sxs-lookup"><span data-stu-id="923c3-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="923c3-121">Puede seguir toouse Hola mismo toovalidate mecanismos tokens, pero debe basarse solamente en Hola "kid" propiedad tooretrieve Hola una clave pública correcta, como Hola especificado en protocolo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="923c3-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="923c3-122">**El trabajo: asegúrese de que la aplicación no depende de la existencia de hello del valor de x5t Hola.**</span><span class="sxs-lookup"><span data-stu-id="923c3-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="923c3-123">Eliminación de profile_info</span><span class="sxs-lookup"><span data-stu-id="923c3-123">Removing profile_info</span></span>
<span data-ttu-id="923c3-124">Anteriormente, el punto de conexión de hello v2.0 se ha devolver un objeto JSON con codificación base64 en las respuestas símbolo (token) que se llama `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="923c3-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="923c3-125">Cuando se solicita un token de acceso de punto de conexión de hello v2.0 enviando una solicitud para:</span><span class="sxs-lookup"><span data-stu-id="923c3-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="923c3-126">respuesta de Hello sería Hola siguiente objeto JSON:</span><span class="sxs-lookup"><span data-stu-id="923c3-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="923c3-127">Hola `profile_info` información de valor contenido acerca del usuario de hello inscrita en aplicación hello - su nombre para mostrar, nombre, apellido, dirección de correo electrónico, identificador y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="923c3-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="923c3-128">Principalmente, Hola `profile_info` se usaron para almacenamiento en caché de tokens y la visualización.</span><span class="sxs-lookup"><span data-stu-id="923c3-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="923c3-129">Ahora estamos quitando hello `profile_info` valor, pero no se preocupe, proporcionamos sigue este toodevelopers información en un lugar ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="923c3-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="923c3-130">En lugar de `profile_info`, el punto de conexión de hello v2.0 devolverá ahora una `id_token` en cada respuesta de token:</span><span class="sxs-lookup"><span data-stu-id="923c3-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="923c3-131">Se puede descodificar y analizar hello id_token tooretrieve Hola la misma información que ha recibido de profile_info.</span><span class="sxs-lookup"><span data-stu-id="923c3-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="923c3-132">Hola id_token es un JSON Web Token (JWT), con el contenido tal y como especifica OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="923c3-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="923c3-133">Hello código para hacerlo debe ser muy similar; simplemente necesita intermedio de hello tooextract descodificarlo tooaccess Hola JSON objeto segmento (cuerpo hello) de hello id_token y base64.</span><span class="sxs-lookup"><span data-stu-id="923c3-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="923c3-134">A través de Hola siguientes dos semanas, debe codificar la información de usuario de aplicación tooretrieve Hola desde cualquier hello `id_token` o `profile_info`; lo que está presente.</span><span class="sxs-lookup"><span data-stu-id="923c3-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="923c3-135">De este modo, cuando se modifican los hello, la aplicación puede controlar perfectamente transición Hola de `profile_info` demasiado`id_token` sin interrupción.</span><span class="sxs-lookup"><span data-stu-id="923c3-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="923c3-136">**El trabajo: asegúrese de que la aplicación no depende de la existencia de Hola de hello `profile_info` valor.**</span><span class="sxs-lookup"><span data-stu-id="923c3-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="923c3-137">Eliminación de id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="923c3-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="923c3-138">Similar demasiado`profile_info`, también la Estamos quitando hello `id_token_expires_in` parámetro de respuestas.</span><span class="sxs-lookup"><span data-stu-id="923c3-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="923c3-139">Anteriormente, el punto de conexión de hello v2.0 devolvería un valor para `id_token_expires_in` junto con cada respuesta id_token, por ejemplo, en una respuesta de autorizar:</span><span class="sxs-lookup"><span data-stu-id="923c3-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="923c3-140">O en una respuesta de token:</span><span class="sxs-lookup"><span data-stu-id="923c3-140">Or in a token response:</span></span>

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

<span data-ttu-id="923c3-141">Hola `id_token_expires_in` valor indicaría número Hola de segundos hello id_token seguirían siendo válido para.</span><span class="sxs-lookup"><span data-stu-id="923c3-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="923c3-142">Ahora, quitaremos hello `id_token_expires_in` valor completamente.</span><span class="sxs-lookup"><span data-stu-id="923c3-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="923c3-143">En su lugar, puede usar el estándar de OpenID Connect hello `nbf` y `exp` validez de hello tooexamine de un id_token de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="923c3-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="923c3-144">Vea hello [referencia del token v2.0](active-directory-v2-tokens.md) para obtener más información sobre estas notificaciones.</span><span class="sxs-lookup"><span data-stu-id="923c3-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="923c3-145">**El trabajo: asegúrese de que la aplicación no depende de la existencia de Hola de hello `id_token_expires_in` valor.**</span><span class="sxs-lookup"><span data-stu-id="923c3-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="923c3-146">Cambiar notificaciones de hello devuelta por ámbito = openid</span><span class="sxs-lookup"><span data-stu-id="923c3-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="923c3-147">Este cambio será hello más significativo, de hecho, afectará a casi todas las aplicaciones que utiliza el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="923c3-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="923c3-148">Muchas aplicaciones enviar solicitudes toohello v2.0 extremo mediante hello `openid` establecer el ámbito, como:</span><span class="sxs-lookup"><span data-stu-id="923c3-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="923c3-149">Hoy en día, cuando el usuario de hello concede el consentimiento para hello `openid` ámbito, la aplicación recibe una gran cantidad de información acerca del usuario de Hola Hola resultante id_token.</span><span class="sxs-lookup"><span data-stu-id="923c3-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="923c3-150">Estas notificaciones pueden incluir su nombre, nombre de usuario preferido, dirección de correo electrónico, identificador de objeto y más.</span><span class="sxs-lookup"><span data-stu-id="923c3-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="923c3-151">En esta actualización, cambiar información de Hola que hello `openid` ámbito, obtienen su aplicación acceso a toobetter comform con hello especificación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="923c3-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="923c3-152">Hola `openid` ámbito, solo permitir que el usuario de aplicación toosign hello en, de recepción y un identificador específico de la aplicación para usuario Hola Hola `sub` de notificación de hello id_token.</span><span class="sxs-lookup"><span data-stu-id="923c3-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="923c3-153">Hola notificaciones en un id_token con solo hello `openid` ámbito otorga será desprovista de toda la información que le identifique personalmente.</span><span class="sxs-lookup"><span data-stu-id="923c3-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="923c3-154">Algunos ejemplos de notificaciones id_token son:</span><span class="sxs-lookup"><span data-stu-id="923c3-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="923c3-155">Si desea tooobtain información personal identificable (PII) acerca del usuario de hello en la aplicación, la aplicación necesitará toorequest permisos adicionales del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="923c3-156">Estamos incorporando compatibilidad para dos nuevos ámbitos de especificación de OpenID Connect de hello: hello `email` y `profile` ámbitos, que le permiten toodo así.</span><span class="sxs-lookup"><span data-stu-id="923c3-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="923c3-157">Hola `email` ámbito es muy sencillo: permite la dirección de correo electrónico principal de aplicación acceso toohello de sus usuarios a través de hello `email` en id_token Hola de notificación.</span><span class="sxs-lookup"><span data-stu-id="923c3-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="923c3-158">Tenga en cuenta que hello `email` no siempre estará presente en id_tokens notificación: solo se incluirá en si está disponible en el perfil de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="923c3-159">Hola `profile` Id. de objeto de ámbito, obtienen los tooall de acceso de aplicación otro información básica sobre el usuario de Hola y su nombre, el nombre de usuario preferido y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="923c3-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="923c3-160">Esto le permite toocode la aplicación de forma mínima divulgación – puede pedir usuario Hola simplemente Hola un conjunto de información que la aplicación necesita toodo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="923c3-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="923c3-161">Si desea toocontinue obtener el conjunto completo de Hola de información de usuario que la aplicación está recibiendo actualmente, debe incluir todos los ámbitos de tres de las solicitudes de autorización:</span><span class="sxs-lookup"><span data-stu-id="923c3-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="923c3-162">La aplicación puede comenzar a enviar hello `email` y `profile` ámbitos inmediatamente y el punto de conexión de hello v2.0 aceptará estos dos ámbitos y empezar a solicitar permisos de los usuarios según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="923c3-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="923c3-163">Sin embargo, cambiar hello en la interpretación de Hola de hello `openid` ámbito no surtirá efecto de unas cuantas semanas.</span><span class="sxs-lookup"><span data-stu-id="923c3-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="923c3-164">**El trabajo: agregar hello `profile` y `email` ámbitos si la aplicación necesita información acerca del usuario de Hola.**</span><span class="sxs-lookup"><span data-stu-id="923c3-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="923c3-165">Tenga en cuenta que la ADAL incluirá ambos permisos en las solicitudes de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="923c3-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="923c3-166">Quitar Hola emisor barra diagonal final.</span><span class="sxs-lookup"><span data-stu-id="923c3-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="923c3-167">Anteriormente, valor de emisor de Hola que aparece en símbolos (token) de punto de conexión de hello v2.0 tardó formulario Hola</span><span class="sxs-lookup"><span data-stu-id="923c3-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="923c3-168">Donde hello guid no era hello tenantId del inquilino de hello Azure AD que emitió el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="923c3-169">Con estos cambios, se convierte en el valor del emisor de Hola</span><span class="sxs-lookup"><span data-stu-id="923c3-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="923c3-170">en ambos tokens y en el documento de detección de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="923c3-171">**El trabajo: asegúrese de que la aplicación acepta el valor del emisor Hola con y sin una barra diagonal final durante la validación de emisor.**</span><span class="sxs-lookup"><span data-stu-id="923c3-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="923c3-172">¿Por qué se han hecho los cambios?</span><span class="sxs-lookup"><span data-stu-id="923c3-172">Why change?</span></span>
<span data-ttu-id="923c3-173">motivación principal de Hola para introducir estos cambios es compatible con la especificación estándar de OpenID Connect de hello toobe.</span><span class="sxs-lookup"><span data-stu-id="923c3-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="923c3-174">Al que se va a OpenID Connect conforme, esperamos toominimize diferencias entre la integración con los servicios de identidad de Microsoft y con otros servicios de identidad en el sector de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="923c3-175">Queremos tooenable a los desarrolladores toouse sus bibliotecas de autenticación de código abierto sin necesidad de diferencias de tooalter Hola bibliotecas tooaccommodate Microsoft.</span><span class="sxs-lookup"><span data-stu-id="923c3-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="923c3-176">¿Qué puede hacer?</span><span class="sxs-lookup"><span data-stu-id="923c3-176">What can you do?</span></span>
<span data-ttu-id="923c3-177">A partir de ahora, puede comenzar a crear todos los cambios de Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="923c3-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="923c3-178">Inmediatamente, debe:</span><span class="sxs-lookup"><span data-stu-id="923c3-178">You should immediately:</span></span>

1. <span data-ttu-id="923c3-179">**Quite las dependencias de hello `x5t` parámetro header.**</span><span class="sxs-lookup"><span data-stu-id="923c3-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="923c3-180">**Controlar correctamente la transición de Hola de `profile_info` demasiado`id_token` en las respuestas de símbolo (token).**</span><span class="sxs-lookup"><span data-stu-id="923c3-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="923c3-181">**Quite las dependencias de hello `id_token_expires_in` parámetro de respuesta.**</span><span class="sxs-lookup"><span data-stu-id="923c3-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="923c3-182">**Agregar hello `profile` y `email` ámbitos tooyour aplicación si la aplicación necesita información básica del usuario.**</span><span class="sxs-lookup"><span data-stu-id="923c3-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="923c3-183">**Aceptar los valores de emisor en los tokens con y sin una barra diagonal final.**</span><span class="sxs-lookup"><span data-stu-id="923c3-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="923c3-184">Nuestro [documentación del protocolo v2.0](active-directory-v2-protocols.md) ya se ha actualizado tooreflect estos cambios, por lo que puede usar como referencia para ayudar a actualizar el código.</span><span class="sxs-lookup"><span data-stu-id="923c3-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="923c3-185">Si tiene alguna pregunta adicional en el ámbito de Hola de cambios de hello, póngase tooreach libre insuficiente toous en Twitter en @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="923c3-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="923c3-186">¿Con qué frecuencia se realizan cambios en los protocolos?</span><span class="sxs-lookup"><span data-stu-id="923c3-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="923c3-187">No se prevé los últimos cambios toohello protocolos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="923c3-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="923c3-188">Le estamos intencionadamente cómo agrupar estos cambios en una versión para que no tenga toogo a través de este tipo de proceso de actualización de nuevo siempre que pronto.</span><span class="sxs-lookup"><span data-stu-id="923c3-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="923c3-189">Por supuesto, continuaremos tooadd características toohello convergente v2.0 servicio de autenticación que pueden aprovechar, pero deben ser esos cambios aditivos y no salto de código existente.</span><span class="sxs-lookup"><span data-stu-id="923c3-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="923c3-190">Por último, nos gustaría toosay le agradecemos que probar cosas durante el período de vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c3-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="923c3-191">visión de Hola y experiencias de nuestro pioneros han sido inestimable hasta el momento, y esperamos que seguirá tooshare sus opiniones e ideas.</span><span class="sxs-lookup"><span data-stu-id="923c3-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="923c3-192">¡ Feliz codificación!</span><span class="sxs-lookup"><span data-stu-id="923c3-192">Happy coding!</span></span>

<span data-ttu-id="923c3-193">Hola división de identidad de Microsoft</span><span class="sxs-lookup"><span data-stu-id="923c3-193">hello Microsoft Identity Division</span></span>

