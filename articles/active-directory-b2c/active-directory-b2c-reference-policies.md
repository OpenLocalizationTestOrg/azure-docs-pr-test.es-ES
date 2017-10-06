---
title: 'Azure Active Directory B2C: directivas integradas | Microsoft Docs'
description: "Un tema de marco de directivas extensible Hola de Azure Active Directory B2C y cómo toocreate diversos tipos de directiva"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: directivas integradas


marco de directivas extensible Hola de Azure Active Directory (Azure AD) B2C es intensidad de núcleo de hello del servicio de Hola. Las directivas describen totalmente las experiencias de identidad del consumidor como el registro, el inicio de sesión y la edición de perfil. Por ejemplo, una directiva de inicio de sesión permite toocontrol comportamientos configurando Hola después de configuración:

* Tipos (cuentas sociales como Facebook) o las cuentas locales, como las direcciones de correo electrónico que los consumidores pueden usar toosign hacia arriba para la aplicación hello de cuenta
* Atributos (por ejemplo, nombre, código postal y calzado) toobe recopila de consumidor de Hola durante el inicio de sesión
* Uso de Azure Multi-Factor Authentication
* Hola apariencia y funcionamiento de todas las páginas de inicio de sesión
* Información (que se manifiesta como notificaciones en un token) que Hola aplicación recibe cuando finaliza la ejecución de la directiva de Hola

Puede crear varias directivas de diferentes tipos en su inquilino y usarlas en sus aplicaciones según sea necesario. Las directivas se pueden volver a usar en todas las aplicaciones. Esta flexibilidad permite a los desarrolladores toodefine y modificar ningún código de tootheir de cambios o las experiencias de identidad de consumidor con mínimo.

Las directivas están disponibles para usarlas mediante una interfaz de usuario sencilla. La aplicación desencadena una directiva mediante una solicitud de autenticación HTTP estándar (pasar un parámetro de directiva de solicitud de saludo) y recibe un token personalizado como respuesta. Por ejemplo, hello única diferencia entre las solicitudes que invocación una directiva de inicio de sesión y las solicitudes que invocación una directiva de inicio de sesión es nombre de la directiva de Hola que se utiliza en el parámetro de cadena de consulta de Hola "p":

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Para obtener más información sobre el marco de directivas de hello, consulte [esta entrada de blog sobre Azure AD B2C en hello la movilidad empresarial y el Blog de seguridad](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Creación de una directiva de registro o de inicio de sesión

Esta directiva controla las experiencias de registro y de inicio de sesión del cliente con una sola configuración. Se ha llevado a los consumidores hacia abajo Hola ruta de acceso correcta (inicio de sesión o inicio de sesión) según el contexto de Hola. También se describe el contenido de Hola de tokens que van a recibir aplicación hello al inicio de sesión de seguridad correcta o inicios de sesión.  Es un ejemplo de código de directiva de inicio de sesión o inicio de sesión de hello [disponible aquí](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  Le recomendamos que use esta directiva en vez de una directiva de registro y una directiva de inicio de sesión.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Creación de una directiva de registro

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Uso de una directiva de inicio de sesión

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Creación de una directiva de edición de perfil

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Crear una directiva de restablecimiento de contraseña

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>¿Cómo puedo vincular una directiva de inicio de sesión o de registro con una directiva de restablecimiento de contraseña?
Cuando se crea una directiva de inicio de sesión o inicio de sesión (con las cuentas locales), verá un **contraseña olvidada?** vínculo en la primera página de Hola de experiencia de Hola. Al hacer clic en este vínculo, no se desencadena automáticamente ninguna directiva de restablecimiento de contraseña, 

Hola en su lugar, el código de error  **`AADB2C90118`**  se devuelve tooyour aplicación. La aplicación debe toohandle este código de error mediante la invocación de una directiva de restablecimiento de contraseña específica. Para obtener más información, vea un [ejemplo que muestra el enfoque de Hola de vinculación de las directivas](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>¿Debo usar una directiva de inicio de sesión o de registro o una directiva de inicio de sesión y una directiva de registro?
Le recomendamos que use una directiva de inicio de sesión o de registro en vez de una directiva de inicio de sesión y una directiva de registro.  

Directiva de inicio de sesión o inicio de sesión de Hello tiene más capacidades que la directiva de inicio de sesión de Hola. También habilita la personalización de interfaz de usuario de página de toouse y tiene una mejor compatibilidad para la localización. 

Directiva de inicio de sesión de Hola se recomienda si no es necesario toolocalize las directivas, solo necesita las capacidades de personalización secundaria para la personalización de marca y desea contraseña restablecimiento que se crean en ella.

## <a name="next-steps"></a>Pasos siguientes
* [Configuración de token, sesión e inicio de sesión único](active-directory-b2c-token-session-sso.md)
* [Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores](active-directory-b2c-reference-disable-ev.md)

