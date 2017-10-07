---
title: 'Azure Active Directory B2C: solicitud de tokens de acceso | Microsoft Docs'
description: "En este artículo le mostrará cómo toosetup una aplicación cliente y adquirir un token de acceso."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: solicitud de tokens de acceso

Un token de acceso (se denomina **acceso\_token** en las respuestas de saludo de Azure AD B2C) es una forma de token de seguridad que un cliente puede utilizar tooaccess recursos que está protegido por un [servidor de autorización](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), como una API web. Tokens de acceso se representan como [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) y contienen información sobre el servidor de recursos previsto de Hola y el servidor de toohello de permisos concedidos de Hola. Al llamar al servidor de recursos de hello, token de acceso de hello debe estar presente en la solicitud HTTP de Hola.

Este artículo describe cómo tooconfigure una aplicación cliente y API web en orden tooobtain una **acceso\_token**.

> [!NOTE]
> **Las cadenas de la API web (en nombre de) no son compatibles con Azure AD B2C.**
>
> Muchas arquitecturas incluyen una API que necesita toocall web otra API de web de nivel inferior, ambos protegen por Azure AD B2C. Este escenario es común en los clientes nativos que tienen un API web back-end, que a su vez llama a un servicio en línea de Microsoft como Hola API de Azure AD Graph.
>
> Este escenario de API de web encadenadas puede ser compatibles con hello concesión de credenciales de portador JWT de OAuth 2.0, en caso contrario denomina hello en nombre de flujo. Sin embargo, hello en nombre de flujo no está implementada actualmente en Azure AD B2C.

## <a name="register-a-web-api-and-publish-permissions"></a>Registro de una API web y publicación de permisos

Antes de solicitar un token de acceso, primero necesita tooregister una API web y permisos (ámbitos) que se pueden conceder a aplicaciones de cliente de toohello de publicación.

### <a name="register-a-web-api"></a>Registro de una API web

1. En la hoja de características de hello B2C en hello portal de Azure, haga clic en **aplicaciones**.
1. Haga clic en **+ agregar** princip Hola de hoja de Hola.
1. Escriba un **nombre** para aplicación Hola que describirá el tooconsumers de aplicación. Por ejemplo, puede escribir "API Contoso".
1. Hola de alternancia **incluyen la aplicación web / web API** cambiar demasiado**Sí**.
1. Escriba un valor arbitrario de hello **direcciones URL de respuesta**. Por ejemplo, escriba: `https://localhost:44316/`. No importa el valor de Hello ya que debería recibir a una API no token Hola directamente desde Azure AD B2C.
1. Escriba un **URI de identificador de aplicación**. Se trata de identificador hello que se usa para la API web. Por ejemplo, escriba "notas" en el cuadro de Hola. Hola **App ID URI** , a continuación, sería `https://{tenantName}.onmicrosoft.com/notes`.
1. Haga clic en **crear** tooregister la aplicación.
1. Haga clic en aplicación Hola que acaba de crear y copiar Hola globalmente único **Id. de aplicación cliente** que va a utilizar más adelante en el código.

### <a name="publishing-permissions"></a>Publicación de permisos

Los ámbitos, que son análogos toopermissions, son necesarios cuando la aplicación llama a una API. Algunos ejemplos de ámbitos son "lectura" o "escritura". Imagine que desea que su aplicación nativa demasiado "lectura" a través de una API o el web. La aplicación debería llamar a Azure AD B2C y solicitud de token de acceso que proporciona acceso toohello ámbito "lectura". Para Azure AD B2C tooemit un token de acceso de este tipo, aplicación hello debe toobe concedido permiso demasiado "lectura" a través de API específica de Hola. toodo, primero necesita de su API toopublish Hola "lectura" ámbito.

1. Dentro de Azure AD B2C hello **aplicaciones** hoja, web Hola abrir aplicación API ("API de Contoso").
1. Haga clic en **Ámbitos publicados**. Esto es donde se definen permisos de hello (ámbitos) que se pueden conceder tooother aplicaciones.
1. Agregue **Valores de ámbito** según sea necesario (por ejemplo, "lectura"). De forma predeterminada, se definirá el ámbito de "user_impersonation" Hola. Puede omitir esto si lo desea. Escriba una descripción del ámbito de Hola Hola **nombre de ámbito** columna.
1. Haga clic en **Guardar**.

> [!IMPORTANT]
> Hola **nombre de ámbito** es una descripción de Hola de hello **valor de ámbito**. Cuando se usa el ámbito de hello, que seguro Hola de toouse **valor de ámbito**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Conceder a nativo o web API web de aplicación permisos tooa

Una vez una API toopublish configurado ámbitos, aplicación de cliente de hello necesita toobe conceder esos ámbitos a través de hello portal de Azure.

1. Navegue toohello **aplicaciones** menú en la hoja de características de hello B2C.
1. Registre una aplicación cliente ([aplicación web](active-directory-b2c-app-registration.md#register-a-web-app) o [cliente nativo](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) si no tiene una todavía. Si se sigue a esta guía como punto de partida, deberá tooregister una aplicación cliente.
1. Haga clic en **Acceso de API**.
1. Haga clic en **Agregar**.
1. Seleccione sus web hello y API ámbitos le gustaría toogrant (permisos).
1. Haga clic en **Aceptar**.

> [!NOTE]
> Azure AD B2C no pide el consentimiento de los usuarios de la aplicación cliente. En su lugar, consentimiento todos lo proporciona Hola, administrador, según los permisos de hello configurados entre aplicaciones de Hola que se ha descrito anteriormente. Si se revoca un permiso concedido para una aplicación, todos los usuarios que estaban previamente podía tooacquire ese permiso dejará de ser capaz de toodo así.

## <a name="requesting-a-token"></a>Solicitud de un token

Cuando se solicita un token de acceso, aplicación de cliente de hello necesita permisos de hello deseado de toospecify en hello **ámbito** parámetro de solicitud de saludo. Por ejemplo, toospecify hello **valor de ámbito** "lectura" para hello API que tiene hello **App ID URI** de `https://contoso.onmicrosoft.com/notes`, ámbito Hola sería `https://contoso.onmicrosoft.com/notes/read`. A continuación se muestra un ejemplo de un toohello de solicitud del código de autorización `/authorize` punto de conexión.

> [!NOTE]
> Actualmente, los dominios personalizados no se admiten junto con los tokens de acceso. Debe utilizar su dominio tenantName.onmicrosoft.com en dirección URL de solicitud de saludo.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire varios permisos en hello mismo solicitar, puede agregar varias entradas en hello único **ámbito** parámetro, separado por espacios. Por ejemplo:

Dirección URL descodificada:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

Dirección URL codificada:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

También puede solicitar más ámbitos (permisos) para un recurso que lo que se concede para la aplicación cliente. Si este es el caso de hello, llamada Hola se realizará correctamente si se concede permiso al menos uno. Hola resultante **acceso\_token** tendrá su notificación "scp" rellena con solo permisos de hello concedidas correctamente.

> [!NOTE] 
> No admitimos solicitar permisos en dos recursos web diferente en hello misma solicitud. Este tipo de solicitud generará un error.

### <a name="special-cases"></a>Casos especiales

Hola OpenID Connect estándar especifica varios valores especiales "ámbito". Hola después demasiado ámbitos especiales representan Hola permiso "acceso al perfil de usuario de hello":

* **openid**: solicita un token de id.
* **offline\_access**: solicita un token de actualización (con [flujos de código de autenticación](active-directory-b2c-reference-oauth-code.md)).

Si hello `response_type` parámetro en un `/authorize` solicitud incluye `token`, hello `scope` parámetro debe incluir el ámbito de al menos un recurso (excepto `openid` y `offline_access`) que se le concederá. En caso contrario, Hola `/authorize` solicitud se terminará con un error.

## <a name="hello-returned-token"></a>Hola devolvió el token

En un correctamente minted **acceso\_token** (desde cualquier hello `/authorize` o `/token` extremo), siguiente Hola notificaciones estará presente:

| Nombre | Notificación | Descripción |
| --- | --- | --- |
|Público |`aud` |Hola **Id. de aplicación** de recurso único de hello ese token Hola concede acceso a. |
|Scope |`scp` |Hola permisos de recurso toohello. Si se trata de varios permisos concedidos, se separarán con un espacio. |
|Entidad autorizada |`azp` |Hola **Id. de aplicación** de aplicación de cliente de Hola que inició la solicitud de saludo. |

Cuando su API recibe hello **acceso\_token**, debe [validar el token de hello](active-directory-b2c-reference-tokens.md) tooprove que Hola token es auténtico y tiene notificaciones correctas de Hola.

Estamos siempre toofeedback abierta y sugerencias. Si tiene dificultades con este tema, publique acerca del desbordamiento de pila con la etiqueta de hello ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Pasos siguientes

* Creación de una API web mediante [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)
* Creación de una API web mediante [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)
