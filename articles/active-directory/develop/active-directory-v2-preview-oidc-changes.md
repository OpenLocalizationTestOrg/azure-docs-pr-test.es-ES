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
# <a name="important-updates-toohello-v20-authentication-protocols"></a>Importantes actualizaciones toohello v2.0 protocolos de autenticación
¡Atención, desarrolladores! A través de hello siguientes dos semanas, realizaremos algunas actualizaciones tooour v2.0 protocolos de autenticación que pueden significar últimos cambios para las aplicaciones que haya escrito durante el período de vista previa.  

## <a name="who-does-this-affect"></a>¿Qué se ve afectado?
Las aplicaciones que se han escrito toouse Hola v2.0 convergen extremo de autenticación

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Puede encontrar más información en el punto de conexión de hello v2.0 [aquí](active-directory-appmodel-v2-overview.md).

Si ha creado una aplicación con el punto de conexión de hello v2.0 codificando directamente toohello v2.0 protocolo, con cualquiera de nuestros middlewares web OpenID Connect o OAuth, o mediante otro 3rd autenticación de tooperform de bibliotecas de entidades, debe estar preparado tootest los proyectos y asegúrese de cambia si es necesario.

## <a name="who-doesnt-this-affect"></a>¿Qué no se ve afectado?
Las aplicaciones que se han escrito en el extremo de autenticación de Azure AD de producción de hello,

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Este protocolo es inamovible y no experimentará ningún cambio.

Además, si la aplicación **sólo** usa la biblioteca ADAL tooperform la autenticación, no tiene toochange nada.  AAL ha protegido la aplicación de los cambios de Hola.  

## <a name="what-are-hello-changes"></a>¿Qué cambios de hello?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Quitar el valor de hello x5t de encabezados JWT
el punto de conexión de Hello v2.0 usa tokens JWT exhaustivamente, que contiene una sección de parámetros de encabezado con metadatos relevantes sobre el token de Hola.  Si descodificar encabezado Hola de uno de nuestros JWTs actuales, encontrará algo parecido:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

En ambas propiedades de "x5t" y "kid" hello identifican la clave pública de Hola que debe ser la firma del token de toovalidate usado hello, una vez recuperados del extremo de metadatos de OpenID Connect de Hola.

cambio de Hello que estamos realizando aquí es propiedad de Hola "x5t" de tooremove.  Puede seguir toouse Hola mismo toovalidate mecanismos tokens, pero debe basarse solamente en Hola "kid" propiedad tooretrieve Hola una clave pública correcta, como Hola especificado en protocolo OpenID Connect. 

> [!IMPORTANT]
> **El trabajo: asegúrese de que la aplicación no depende de la existencia de hello del valor de x5t Hola.**
> 
> 

### <a name="removing-profileinfo"></a>Eliminación de profile_info
Anteriormente, el punto de conexión de hello v2.0 se ha devolver un objeto JSON con codificación base64 en las respuestas símbolo (token) que se llama `profile_info`.  Cuando se solicita un token de acceso de punto de conexión de hello v2.0 enviando una solicitud para:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

respuesta de Hello sería Hola siguiente objeto JSON:

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

Hola `profile_info` información de valor contenido acerca del usuario de hello inscrita en aplicación hello - su nombre para mostrar, nombre, apellido, dirección de correo electrónico, identificador y así sucesivamente.  Principalmente, Hola `profile_info` se usaron para almacenamiento en caché de tokens y la visualización.

Ahora estamos quitando hello `profile_info` valor, pero no se preocupe, proporcionamos sigue este toodevelopers información en un lugar ligeramente diferente.  En lugar de `profile_info`, el punto de conexión de hello v2.0 devolverá ahora una `id_token` en cada respuesta de token:

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

Se puede descodificar y analizar hello id_token tooretrieve Hola la misma información que ha recibido de profile_info.  Hola id_token es un JSON Web Token (JWT), con el contenido tal y como especifica OpenID Connect.  Hello código para hacerlo debe ser muy similar; simplemente necesita intermedio de hello tooextract descodificarlo tooaccess Hola JSON objeto segmento (cuerpo hello) de hello id_token y base64.

A través de Hola siguientes dos semanas, debe codificar la información de usuario de aplicación tooretrieve Hola desde cualquier hello `id_token` o `profile_info`; lo que está presente.  De este modo, cuando se modifican los hello, la aplicación puede controlar perfectamente transición Hola de `profile_info` demasiado`id_token` sin interrupción.

> [!IMPORTANT]
> **El trabajo: asegúrese de que la aplicación no depende de la existencia de Hola de hello `profile_info` valor.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Eliminación de id_token_expires_in
Similar demasiado`profile_info`, también la Estamos quitando hello `id_token_expires_in` parámetro de respuestas.  Anteriormente, el punto de conexión de hello v2.0 devolvería un valor para `id_token_expires_in` junto con cada respuesta id_token, por ejemplo, en una respuesta de autorizar:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

O en una respuesta de token:

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

Hola `id_token_expires_in` valor indicaría número Hola de segundos hello id_token seguirían siendo válido para.  Ahora, quitaremos hello `id_token_expires_in` valor completamente.  En su lugar, puede usar el estándar de OpenID Connect hello `nbf` y `exp` validez de hello tooexamine de un id_token de notificaciones.  Vea hello [referencia del token v2.0](active-directory-v2-tokens.md) para obtener más información sobre estas notificaciones.

> [!IMPORTANT]
> **El trabajo: asegúrese de que la aplicación no depende de la existencia de Hola de hello `id_token_expires_in` valor.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Cambiar notificaciones de hello devuelta por ámbito = openid
Este cambio será hello más significativo, de hecho, afectará a casi todas las aplicaciones que utiliza el punto de conexión de hello v2.0.  Muchas aplicaciones enviar solicitudes toohello v2.0 extremo mediante hello `openid` establecer el ámbito, como:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Hoy en día, cuando el usuario de hello concede el consentimiento para hello `openid` ámbito, la aplicación recibe una gran cantidad de información acerca del usuario de Hola Hola resultante id_token.  Estas notificaciones pueden incluir su nombre, nombre de usuario preferido, dirección de correo electrónico, identificador de objeto y más.

En esta actualización, cambiar información de Hola que hello `openid` ámbito, obtienen su aplicación acceso a toobetter comform con hello especificación OpenID Connect.  Hola `openid` ámbito, solo permitir que el usuario de aplicación toosign hello en, de recepción y un identificador específico de la aplicación para usuario Hola Hola `sub` de notificación de hello id_token.  Hola notificaciones en un id_token con solo hello `openid` ámbito otorga será desprovista de toda la información que le identifique personalmente.  Algunos ejemplos de notificaciones id_token son:

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

Si desea tooobtain información personal identificable (PII) acerca del usuario de hello en la aplicación, la aplicación necesitará toorequest permisos adicionales del usuario de Hola.  Estamos incorporando compatibilidad para dos nuevos ámbitos de especificación de OpenID Connect de hello: hello `email` y `profile` ámbitos, que le permiten toodo así.

* Hola `email` ámbito es muy sencillo: permite la dirección de correo electrónico principal de aplicación acceso toohello de sus usuarios a través de hello `email` en id_token Hola de notificación.  Tenga en cuenta que hello `email` no siempre estará presente en id_tokens notificación: solo se incluirá en si está disponible en el perfil de usuario de Hola.
* Hola `profile` Id. de objeto de ámbito, obtienen los tooall de acceso de aplicación otro información básica sobre el usuario de Hola y su nombre, el nombre de usuario preferido y así sucesivamente.

Esto le permite toocode la aplicación de forma mínima divulgación – puede pedir usuario Hola simplemente Hola un conjunto de información que la aplicación necesita toodo su trabajo.  Si desea toocontinue obtener el conjunto completo de Hola de información de usuario que la aplicación está recibiendo actualmente, debe incluir todos los ámbitos de tres de las solicitudes de autorización:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

La aplicación puede comenzar a enviar hello `email` y `profile` ámbitos inmediatamente y el punto de conexión de hello v2.0 aceptará estos dos ámbitos y empezar a solicitar permisos de los usuarios según sea necesario.  Sin embargo, cambiar hello en la interpretación de Hola de hello `openid` ámbito no surtirá efecto de unas cuantas semanas.

> [!IMPORTANT]
> **El trabajo: agregar hello `profile` y `email` ámbitos si la aplicación necesita información acerca del usuario de Hola.**  Tenga en cuenta que la ADAL incluirá ambos permisos en las solicitudes de forma predeterminada. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Quitar Hola emisor barra diagonal final.
Anteriormente, valor de emisor de Hola que aparece en símbolos (token) de punto de conexión de hello v2.0 tardó formulario Hola

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Donde hello guid no era hello tenantId del inquilino de hello Azure AD que emitió el token de Hola.  Con estos cambios, se convierte en el valor del emisor de Hola

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

en ambos tokens y en el documento de detección de OpenID Connect de Hola.

> [!IMPORTANT]
> **El trabajo: asegúrese de que la aplicación acepta el valor del emisor Hola con y sin una barra diagonal final durante la validación de emisor.**
> 
> 

## <a name="why-change"></a>¿Por qué se han hecho los cambios?
motivación principal de Hola para introducir estos cambios es compatible con la especificación estándar de OpenID Connect de hello toobe.  Al que se va a OpenID Connect conforme, esperamos toominimize diferencias entre la integración con los servicios de identidad de Microsoft y con otros servicios de identidad en el sector de Hola.  Queremos tooenable a los desarrolladores toouse sus bibliotecas de autenticación de código abierto sin necesidad de diferencias de tooalter Hola bibliotecas tooaccommodate Microsoft.

## <a name="what-can-you-do"></a>¿Qué puede hacer?
A partir de ahora, puede comenzar a crear todos los cambios de Hola que se ha descrito anteriormente.  Inmediatamente, debe:

1. **Quite las dependencias de hello `x5t` parámetro header.**
2. **Controlar correctamente la transición de Hola de `profile_info` demasiado`id_token` en las respuestas de símbolo (token).**
3. **Quite las dependencias de hello `id_token_expires_in` parámetro de respuesta.**
4. **Agregar hello `profile` y `email` ámbitos tooyour aplicación si la aplicación necesita información básica del usuario.**
5. **Aceptar los valores de emisor en los tokens con y sin una barra diagonal final.**

Nuestro [documentación del protocolo v2.0](active-directory-v2-protocols.md) ya se ha actualizado tooreflect estos cambios, por lo que puede usar como referencia para ayudar a actualizar el código.

Si tiene alguna pregunta adicional en el ámbito de Hola de cambios de hello, póngase tooreach libre insuficiente toous en Twitter en @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>¿Con qué frecuencia se realizan cambios en los protocolos?
No se prevé los últimos cambios toohello protocolos de autenticación.  Le estamos intencionadamente cómo agrupar estos cambios en una versión para que no tenga toogo a través de este tipo de proceso de actualización de nuevo siempre que pronto.  Por supuesto, continuaremos tooadd características toohello convergente v2.0 servicio de autenticación que pueden aprovechar, pero deben ser esos cambios aditivos y no salto de código existente.

Por último, nos gustaría toosay le agradecemos que probar cosas durante el período de vista previa de Hola.  visión de Hola y experiencias de nuestro pioneros han sido inestimable hasta el momento, y esperamos que seguirá tooshare sus opiniones e ideas.

¡ Feliz codificación!

Hola división de identidad de Microsoft

