---
title: aaaAzure Active Directory v2.0 tokens referencia | Documentos de Microsoft
description: tipos de Hola de notificaciones y tokens emiten por hello extremo v2.0 de Azure AD
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Referencia de tokens de Azure Active Directory v2.0
el punto de conexión de Azure Active Directory (Azure AD) v2.0 Hello emite varios tipos de tokens de seguridad en cada uno de ellos [flujo de autenticación](active-directory-v2-flows.md). Esta referencia describe el formato de hello, características de seguridad y el contenido de cada tipo de símbolo (token).

> [!NOTE]
> el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory. toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Tipos de tokens
Hello v2.0 extremo admite hello [protocolo de autorización de OAuth 2.0](active-directory-v2-protocols.md), que usa tokens de acceso y tokens de actualización. el punto de conexión de Hello v2.0 también admite la autenticación e inicio de sesión a través de [OpenID Connect](active-directory-v2-protocols.md). OpenID Connect presenta a un tercer tipo de token de Id. de token, Hola. Todos estos tokens se representan como un token de *portador*.

Un token de portador es un token de seguridad ligero que concede Hola portador tooa de acceso al recurso protegido. portador de Hello es cualquier entidad que puede presentar el token de Hola. Aunque una parte debe autenticarse con el token de acceso de Azure AD tooreceive hello, si no se toman medidas token de hello toosecure durante la transmisión y el almacenamiento, puede interceptar y utilizado por una entidad no deseada. Algunos tokens de seguridad tienen un entidades de tooprevent no autorizado de mecanismo integrado del uso de ellos, pero no de tokens de portador no. Los tokens de portador deben ser transportados en un canal seguro, como Seguridad de la capa de transporte (HTTPS). Si se transmite un token de portador sin este tipo de seguridad, un tercero malintencionado podría usar un símbolo (token) "man-in-the-middle ataque" tooacquire hello y usarlo para el recurso de tooa protegido del acceso no autorizado. Hola mismos principios de seguridad que se aplican al almacenamiento o almacenamiento en caché de tokens portadores para su uso posterior. Siempre debe asegurarse de que la aplicación transmite y almacena los tokens de portador de manera segura. Para otras consideraciones de seguridad sobre los tokens de portador, consulte la [sección 5 de RFC 6750](http://tools.ietf.org/html/rfc6750).

Muchos de los tokens de hello emitidos por el punto de conexión de hello v2.0 se implementan como Tokens de Web JSON (Jwt). Un JWT es una manera compacta, seguridad de la dirección URL, tootransfer más información entre dos entidades. información de Hello en un JWT se denomina un *notificación*. Es una aserción de información sobre el portador de Hola y el asunto del token de Hola. notificaciones de Hello en un JWT son objetos de JavaScript Object Notation (JSON) que están codificados y se serializan para la transmisión. Dado que hello Jwt emitido por el punto de conexión de hello v2.0 se firma pero no cifrado, fácilmente puede inspeccionar el contenido de Hola de un JWT para fines de depuración. Para obtener más información acerca de Jwt, consulte hello [especificación JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Tokens de identificador
Un token de identificador es una forma de token de seguridad de inicio de sesión que recibe la aplicación cuando realiza la autenticación mediante [OpenID Connect](active-directory-v2-protocols.md). Tokens de identificador se representan como [JWTs](#types-of-tokens), y contienen notificaciones que puede usar toosign Hola usuario en aplicaciones de tooyour. Puede usar notificaciones de hello en un identificador de token de varias maneras. Por lo general, administradores utilizan información de cuenta de identificación de tokens toodisplay o toomake decisiones de control de acceso en una aplicación. el punto de conexión de Hello v2.0 emite solo un tipo de identificador de token, que tiene un conjunto coherente de notificaciones, independientemente del tipo de saludo del usuario que ha iniciado sesión. formato de Hola y el contenido de los tokens de Id. de se Hola igual para los usuarios de cuentas de Microsoft personales y para cuentas profesionales o educativas.

Actualmente, los tokens de identificador están firmados pero no cifrados. Cuando la aplicación recibe un identificador de token, debe [validar la firma de hello](#validating-tokens) tooprove Hola autenticidad del token y validar las reclamaciones unos en hello token tooprove su validez. Hello validados por una aplicación de notificaciones varían según los requisitos de escenario, aunque la aplicación debe realizar algunas [validaciones de notificación comunes](#validating-tokens) en cada escenario.

Se proporcionan detalles completos de hello sobre notificaciones en tokens de Id. de Hola siguientes secciones, además tooa token de Id. de ejemplo. Tenga en cuenta que las notificaciones en los tokens de identificador no se devuelven en ningún orden específico. Además, se pueden agregar nuevas notificaciones en tokens de identificador en cualquier momento. La aplicación no se debe interrumpir cuando se agregan notificaciones nuevas. Hola lista siguiente incluye las notificaciones de Hola que la aplicación actualmente puede confiable interpretar. Puede encontrar más detalles en hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Token de identificador de ejemplo
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Para practicar, tooinspect Hola de notificaciones en el token de Id. de ejemplo de Hola, pegue token de Id. de ejemplo de Hola en [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Notificaciones en tokens de identificador
| Nombre | Notificación | Valor de ejemplo | Descripción |
| --- | --- | --- | --- |
| audience |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Identifica a Hola pensado destinatario del token de Hola. En los tokens de Id., audiencia hello es Id. de aplicación de la aplicación, asigna tooyour aplicación Hola Portal de registro de aplicación de Microsoft. La aplicación debe validar este valor y rechazar el token de hello si no coincide con el valor de Hola. |
| issuer |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Identifica Hola símbolo (token) servicio de seguridad (STS) que construye y devuelve el símbolo (token) de Hola e inquilino de Azure AD de hello en qué Hola se ha autenticado el usuario. La aplicación debe validar la notificación de emisor de hello tooensure que Hola token procede de punto de conexión de hello v2.0. También debe usar parte GUID de Hola de hello toorestrict Hola conjunto de notificaciones los inquilinos que puede iniciar sesión en la aplicación toohello. GUID que indica que el usuario Hola Hello es un usuario de consumidor de una cuenta de Microsoft `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| issued at |`iat` |`1452285331` |hora de Hello en qué Hola se emitió el token, representado en tiempo base. |
| expiration time |`exp` |`1452289231` |hora de Hello en qué Hola token deja de ser válido, se representa en tiempo base. La aplicación debe utilizar este validez de hello tooverify de notificación de duración del token Hola. |
| not before |`nbf` |`1452285331` |tiempo de Hello en qué hello es válida, símbolo (token) se representan en tiempo base. Resulta igual Hola normalmente como hora de emisión de Hola. La aplicación debe utilizar este validez de hello tooverify de notificación de duración del token Hola. |
| versión |`ver` |`2.0` |versión de Hola de token de Id. de hello, tal como se define por Azure AD. Punto de conexión de hello v2.0, valor de hello es `2.0`. |
| tenant ID |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |Un GUID que representa el inquilino de hello Azure AD que Hola usuario procede. Para cuentas profesionales o educativas, Hola GUID es inquilino inmutable Hola Id. de organización de Hola que Hola usuario pertenece. Para las cuentas personales, el valor de hello es `9188040d-6c67-4c5b-b112-36a304b66dad`. Hola `profile` se requiere el ámbito en orden tooreceive esta notificación. |
| code hash |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hash de código de Hello se incluye en los tokens de identificador solo cuando se emite el token de Id. de hello con un código de autorización de OAuth 2.0. Puede ser usado toovalidate Hola autenticidad de un código de autorización. Para obtener más información acerca de cómo realizar esta validación, vea hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html). |
| access token hash |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hash de token de acceso de Hola se incluye en los tokens de identificador solo cuando se emite el token de Id. de hello con un token de acceso de OAuth 2.0. Puede ser usado toovalidate Hola autenticidad de un token de acceso. Para obtener más información acerca de cómo realizar esta validación, vea hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html). |
| valor de seguridad |`nonce` |`12345` |nonce Hello es una estrategia para mitigar los ataques de reproducción de tokens. La aplicación puede especificar un valor nonce en una solicitud de autorización mediante hello `nonce` parámetro de consulta. valor de Hola que proporcione en solicitud de saludo se emite en del token de Id. de hello `nonce` notificación, sin modificar. La aplicación puede comprobar el valor Hola respecto al valor de hello que lo especificado en la solicitud de hello, que asocia la sesión de la aplicación hello con un token de Id. específico. La aplicación debe realizar esta validación durante el proceso de validación del token de Id. de Hola. |
| name |`name` |`Babe Ruth` |notificación de nombre de Hello proporciona un valor legible que identifica a Hola sujeto del token de Hola. no se garantiza el valor de Hello toobe único es mutable y está diseñado toobe utilizada solo con fines de visualización. Hola `profile` se requiere el ámbito en orden tooreceive esta notificación. |
| email |`email` |`thegreatbambino@nyy.onmicrosoft.com` |dirección de correo electrónico principal de Hello asociado con la cuenta de usuario de hello, si existe. Su valor es mutable y podría cambiar en el tiempo. Hola `email` se requiere el ámbito en orden tooreceive esta notificación. |
| preferred username |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Hola nombre principal de usuario que representa al usuario de hello en el punto de conexión de hello v2.0. Puede ser una dirección de correo electrónico, un número de teléfono o un nombre de usuario genérico sin un formato especificado. Su valor es mutable y podría cambiar en el tiempo. Hola `profile` se requiere el ámbito en orden tooreceive esta notificación. |
| subject |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | entidad de seguridad de Hello sobre qué Hola token valida información, como el usuario de una aplicación Hola. Este valor es inmutable y no se puede reasignar ni volver a usar. Puede ser usado tooperform las comprobaciones de autorización de forma segura, como al símbolo (token) de hello es tooaccess usa un recurso y puede utilizarse como clave en las tablas de base de datos. Porque Hola sujeto siempre está presente en los tokens de Hola que emite Azure AD, se recomienda usar este valor en un sistema de autorización de uso general. asunto Hola es, sin embargo, un identificador en pares: tooa único Id. de aplicación en particular.  Por lo tanto, si un usuario inicia sesión en dos aplicaciones diferentes con dos identificadores de cliente diferente, esas aplicaciones recibirán dos valores diferentes para la notificación de asunto Hola.  Esto puede ser o no deseable dependiendo de los requisitos de arquitectura y privacidad. |
| object ID |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | Hola identificador inmutable de un objeto en hello identidad sistema de Microsoft, en este caso, una cuenta de usuario.  También puede ser usado tooperform las comprobaciones de autorización como una clave en tablas de base de datos y de forma segura. Este identificador identifica de forma única el usuario de hello en todas las aplicaciones: dos aplicaciones diferentes que iniciar sesión en hello recibirá el mismo usuario Hola mismo valor en hello `oid` de notificación.  Esto significa que puede usarse al realizar consultas tooMicrosoft los servicios en línea, como Hola Microsoft Graph.  Hola Microsoft Graph devuelve este identificador como hello `id` propiedad para una cuenta de usuario determinada.  Dado que hello `oid` permite varias aplicaciones toocorrelate a los usuarios, hello `profile` se requiere el ámbito en orden tooreceive esta notificación. Tenga en cuenta que si un usuario existe en varios inquilinos, usuario Hola contendrá un identificador de un objeto distinto en cada inquilino, se consideran cuentas diferentes, aunque Hola usuario inicia sesión en cada cuenta con Hola mismas credenciales. |

### <a name="access-tokens"></a>Tokens de acceso
Actualmente, los tokens de acceso emitidos por el punto de conexión de hello v2.0 pueden utilizarse solo en Microsoft Services. Las aplicaciones no es necesario tooperform ninguna validación o la inspección de tokens de acceso en cualquiera de las situaciones de hello admite actualmente. Los tokens de acceso se pueden tratar como completamente opacos. Son simplemente cadenas que su aplicación pasa tooMicrosoft en las solicitudes HTTP.

Hola cerca futuras, v2.0 Hola extremo incorporará capacidad de Hola para sus tokens de acceso de aplicación tooreceive desde otros clientes. En ese momento, información de hello en este tema de referencia se actualizará con la información de Hola que necesite para la validación del token de acceso de aplicación tooperform y otras tareas similares.

Cuando se solicita un token de acceso de punto de conexión de hello v2.0, el punto de conexión de hello v2.0 también devuelve metadatos sobre el token de acceso de Hola para su toouse de aplicación. Esta información incluye la hora de expiración Hola de token de acceso de Hola y ámbitos de hello para el que es válido. La aplicación usa este metadatos tooperform inteligente almacenamiento en caché de tokens de acceso sin necesidad de token de acceso de hello abierto tooparse propio.

### <a name="refresh-tokens"></a>Tokens de actualización
Tokens de actualización son tokens de seguridad que puede usar su aplicación tooget nuevos tokens de acceso en un flujo de OAuth 2.0. Puede usar su aplicación tooresources a largo plazo de acceso de actualización de tokens tooachieve en nombre del usuario sin necesidad de interacción con el usuario de Hola.

Los tokens de actualización tienen varios recursos. Un token de actualización recibido durante una solicitud de token para un recurso se puede canjear para recursos completamente diferente de tooa de tokens de acceso.

tooreceive una actualización en una respuesta de token, la aplicación debe solicitar y recibir hello `offline_acesss` ámbito. más información acerca de hello toolearn `offline_access` ámbito, vea hello [consentimiento y ámbitos](active-directory-v2-scopes.md) artículo.

Tokens de actualización son y siempre será, aplicación tooyour completamente opaco. Están emitidos por el punto de conexión de hello Azure AD v2.0 y puede solo inspeccionar e interpretados por el punto de conexión de hello v2.0. Son de larga duración, pero la aplicación no debe escribirse tooexpect que un token de actualización durarán durante cualquier período de tiempo. Los tokens de actualización pueden invalidarse en cualquier momento por diversos motivos. Hola solo manera para que su tooknow de aplicación si un token de actualización es válido es tooattempt tooredeem, mediante la realización de un punto de conexión de solicitud de token toohello v2.0.

Al canjear un token de actualización para un nuevo token de acceso (y si la aplicación se hubiesen garantizada hello `offline_access` ámbito), recibirá un nuevo token de actualización en la respuesta de token de Hola. Guardar Hola recién emitido actualización Hola tooreplace token, que ha utilizado en la solicitud de saludo. Esto garantiza que los tokens de actualización sigan siendo válidos mientras sea posible.

## <a name="validating-tokens"></a>Validación de los tokens
Hola actualmente, solo deberían ser necesario las aplicaciones de la validación del token tooperform es validar los tokens de identificador. toovalidate un identificador de token, la aplicación debe validar notificaciones hello y firma del ambos Hola el token del identificador token de Id. de Hola.

<!-- TODO: Link -->
Microsoft proporciona las bibliotecas y ejemplos de código que muestran cómo tooeasily administran la validación de token. En las secciones siguientes de hello, describimos Hola subyacente de proceso. Varias bibliotecas de código abierto de terceros también están disponibles para validación de JWT. Hay al menos una opción de biblioteca para casi cualquier plataforma y lenguaje.

### <a name="validate-hello-signature"></a>Validar la firma de Hola
Un JWT contiene tres segmentos, que están separados por hello `.` caracteres. primer segmento de Hola se conoce como hello *encabezado*, segundo segmento de hello es hello *cuerpo*, y tercer segmento de hello es hello *firma*. segmento de firma de Hello puede ser usado toovalidate Hola autenticidad del token de Id. de Hola para que lo puede ser de confianza para la aplicación.

Los tokens de identificador se firman con algoritmos de cifrado asimétrico estándar del sector, como RSA 256. encabezado de token de Id. de hello Hello tiene información acerca de la clave de Hola y método de cifrado usa el token de hello toosign. Por ejemplo:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Hola `alg` notificación indica el algoritmo de Hola que era el token de hello toosign usado. Hola `kid` notificación indica la clave pública de Hola que era el token de hello toosign usado.

En cualquier momento, el punto de conexión de hello v2.0 puede firmar un identificador de token mediante uno de un determinado conjunto de pares de claves pública y privada. el punto de conexión de Hello v2.0 periódicamente gira posible conjunto de Hola de claves, por lo que la aplicación debe escribirse toohandle esos clave cambia automáticamente. Un toocheck frecuencia razonable para claves públicas de las actualizaciones toohello utilizado por el punto de conexión de hello v2.0 es cada 24 horas.

Puede adquirir Hola firmar datos claves que necesita firma de hello toovalidate mediante Hola OpenID Connect metadatos documento que se encuentra en:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Intente Hola URL en un explorador.
>
>

Este documento de metadatos es un objeto JSON que tiene varias piezas útiles de información, como ubicación de Hola de hello varios extremos requeridos para la autenticación de OpenID Connect.  documento de Hello también incluye una *jwks_uri*, que proporciona la ubicación de Hola de hello del conjunto de claves públicas utiliza toosign símbolos (tokens). documento JSON de Hello ubicado en hello jwks_uri tiene todos los Hola información de clave pública que está actualmente en uso. Puede usar su aplicación Hola `kid` un token de notificación en hello JWT encabezado tooselect qué clave pública en este documento ha sido toosign usado. A continuación, realiza la validación de firma mediante una clave pública correcta Hola y Hola indicado algoritmo.

Realizar la validación de la firma es el ámbito de hello fuera de este documento. Muchas bibliotecas de código abierto están disponible toohelp a esto.

### <a name="validate-hello-claims"></a>Validar las reclamaciones de Hola
Cuando la aplicación recibe un identificador de token al inicio de sesión de usuario, también debe realizar algunas comprobaciones frente a las notificaciones de hello en el token del identificador hello. Estas incluyen, pero no se limitan a:

* **audiencia** de notificación, tooverify que Hola identificador de token estaba previsto toobe dado tooyour aplicación
* **antes de no** y **tiempo de expiración** de notificaciones, tooverify que Hola identificador de token no ha expirado
* **emisor** de notificación, tooverify que Hola token emitido tooyour aplicación por el punto de conexión de hello v2.0
* **nonce**, como mitigación de ataques de reproducción de tokens.

Para obtener una lista completa de las validaciones de notificación que se debe realizar la aplicación, vea hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

Detalles de los valores esperados de Hola para estas notificaciones se incluyen en hello [tokens de identificador](# ID tokens) sección.

## <a name="token-lifetimes"></a>Vigencia de los tokens
Proporcionamos Hola siguiendo la vigencia de los tokens solo para fines informativos. Hola información puede ayudarle a desarrollar y depurar aplicaciones. Las aplicaciones no deben estar escrito tooexpect cualquiera de estos constante de tooremain duraciones. La vigencia de los tokens puede cambiar en cualquier momento, y así será.

| SWT | Vigencia | Descripción |
| --- | --- | --- |
| Tokens de identificador (cuentas profesionales o educativas) |1 hora |Habitualmente, los tokens de identificador son válidos durante 1 hora. La aplicación web puede utilizar este mismo toomaintain de duración su propia sesión de usuario de hello (recomendado), o puede elegir una duración de sesión completamente diferente. Si la aplicación necesita tooget un nuevo token de Id., necesita toohello v2.0 extremo authorize de solicitud de toomake un inicio de sesión de nuevo. Si el usuario de hello tiene una sesión de explorador válidas con el punto de conexión de hello v2.0, usuario Hola podría no ser necesario tooenter sus credenciales de nuevo. |
| Tokens de identificador (cuentas personales) |24 horas |Habitualmente, los tokens de identificador para cuentas personales son válidos durante 24 horas. La aplicación web puede utilizar este mismo toomaintain de duración su propia sesión de usuario de hello (recomendado), o puede elegir una duración de sesión completamente diferente. Si la aplicación necesita tooget un nuevo token de Id., necesita toohello v2.0 extremo authorize de solicitud de toomake un inicio de sesión de nuevo. Si el usuario de hello tiene una sesión de explorador válidas con el punto de conexión de hello v2.0, usuario Hola podría no ser necesario tooenter sus credenciales de nuevo. |
| Tokens de acceso (cuentas profesionales o educativas) |1 hora |Como parte de los metadatos del token Hola indicados en respuestas símbolo (token). |
| Tokens de acceso (cuentas personales) |1 hora |Como parte de los metadatos del token Hola indicados en respuestas símbolo (token). Los tokens de acceso que se emiten en nombre de las cuentas personales se pueden configurar para que tengan una vigencia distinta, pero lo habitual suele ser 1 hora. |
| Tokens de actualización (cuentas profesionales o educativas) |Los días de too14 |Un token de actualización solo es válido durante un máximo de 14 días. Sin embargo, token de actualización de hello podría dejan de ser válido en cualquier momento por diversas razones, por lo que la aplicación debe continuar tootry toouse un token de actualización hasta que se produce un error, o hasta que la aplicación lo reemplaza con un nuevo token de actualización. Un token de actualización también deja de ser válido si ha transcurrido 90 días desde que ha entrado en sus credenciales de usuario de Hola. |
| Tokens de actualización (cuentas personales) |Año too1 |Un token de actualización solo es válido durante un máximo de 1 año. Sin embargo, token de actualización de hello podría no ser válido en cualquier momento por diversas razones, por lo que la aplicación debe continuar tootry toouse un token de actualización hasta que se produce un error. |
| Códigos de autorización (cuentas profesionales o educativas) |10 minutos |Códigos de autorización son de corta duración deliberadamente y deben pueden canjear inmediatamente para los tokens de acceso y tokens de actualización cuando se reciben los tokens de Hola. |
| Códigos de autorización (cuentas personales) |5 minutos |Códigos de autorización son de corta duración deliberadamente y deben pueden canjear inmediatamente para los tokens de acceso y tokens de actualización cuando se reciben los tokens de Hola. Los códigos de autorización emitidos en nombre de las cuentas personales son de un solo uso. |
