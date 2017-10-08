---
title: 'Azure Active Directory B2C: Registro de aplicaciones | Microsoft Docs'
description: "¿Cómo tooregister la aplicación con Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: Registro de la aplicación

Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos. Cuando haya terminado, la aplicación se registra para su uso en el inquilino de hello Azure B2C.

## <a name="prerequisites"></a>Requisitos previos

toobuild una aplicación que acepta consumidor registrarse e iniciar sesión, necesita primero la aplicación de hello tooregister con un inquilino de Azure Active Directory B2C. Obtener su propio inquilino mediante el uso de pasos de hello descritos en [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).

Aplicaciones creadas a partir de la hoja de Azure AD B2C Hola Hola portal de Azure deben administrarse desde Hola misma ubicación. Si edita las aplicaciones de B2C Hola con PowerShell u otro portal, que se convierten en no compatibles y no funcionan con Azure AD B2C. Ver detalles de hello [errores en aplicaciones](#faulted-apps) sección. 

## <a name="navigate-toob2c-settings"></a>Desplácese tooB2C configuración

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como Hola administrador Global del inquilino de hello B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Elija los pasos siguientes en función de tipo de aplicación Hola que va a registrar:

* [Registro de una aplicación web](#register-a-web-app)
* [Registro de una API web](#register-a-web-api)
* [Registro de una aplicación móvil o nativa](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Registro de una aplicación web

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Si la aplicación web llama a una API web protegida por Azure AD B2C, siga estos pasos:
   1. Crear un secreto de aplicación va toohello **claves** hoja y haga clic en hello **generar clave** botón. Tome nota de hello **clave de aplicación** valor. Utilice el valor de hello como secreto de aplicación hello en el código de la aplicación.
   2. Haga clic en **Acceso de API**, en **Agregar** y seleccione la API web y los ámbitos (permisos).

> [!NOTE]
> Un **secreto de aplicación** es una credencial de seguridad importante y debe protegerse correctamente.
> 

[Saltar demasiado**pasos siguientes**](#next-steps)

## <a name="register-a-web-api"></a>Registro de una API web

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Haga clic en **publicado ámbitos** tooadd más ámbitos según sea necesario. De forma predeterminada, se define el ámbito de "user_impersonation" Hola. ámbito user_impersonation de Hello ofrece otras tooaccess de capacidad de las aplicaciones Hola esta api en nombre de usuario que inició sesión Hola. Si lo desea, se puede quitar el ámbito de hello user_impersonation.

[Saltar demasiado**pasos siguientes**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Registro de una aplicación móvil o nativa

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Saltar demasiado**pasos siguientes**](#next-steps)

## <a name="limitations"></a>Limitaciones

### <a name="choosing-a-web-app-or-api-reply-url"></a>Selección de una dirección URL de respuesta de la aplicación web o API

Actualmente, las aplicaciones que se registran con Azure AD B2C son conjunto restringido tooa limitado de valores de dirección URL de respuesta. Hola respuesta dirección URL para aplicaciones web y servicios debe comenzar con el esquema de hello `https`, y responden a todos los valores de dirección URL deben compartir un único dominio DNS. Por ejemplo, no puede registrar una aplicación web con una de estas direcciones URL de respuesta:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

sistema de registro de Hello compara Hola de nombre DNS completo de hello existente respuesta URL toohello nombre DNS de la dirección URL de respuesta de Hola que va a agregar. tooadd Hola nombre DNS de Hello solicitud produce un error si se cumple alguna de hello condiciones siguientes:

* nombre DNS completo de Hola Hola nueva URL de respuesta no coincide con el nombre DNS de Hola Hola existente URL de respuesta.
* nombre DNS completo de Hola Hola nueva URL de respuesta no es un subdominio de hello URL de respuesta existente.

Por ejemplo, si hello aplicación tiene esta dirección URL de respuesta:

`https://login.contoso.com`

Puede agregar tooit, similar al siguiente:

`https://login.contoso.com/new`

En este caso, el nombre DNS de hello coincide exactamente. O bien, puede hacer lo siguiente:

`https://new.login.contoso.com`

En este caso, está haciendo referencia subdominio DNS de tooa de login.contoso.com. Si desea toohave una aplicación con inicio de sesión east.contoso.com y west.contoso.com-inicio de sesión como responder a las direcciones URL, debe agregar estas direcciones URL de respuesta en este orden:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Puede agregar Hola dos últimos porque son subdominios Hola primera URL de respuesta, contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Selección de un identificador URI de redireccionamiento de una aplicación nativa

Hay dos consideraciones importantes al elegir un URI de redirección para aplicaciones móviles o nativas:

* **Único**: esquema de Hola de URI de redireccionamiento de hello debe ser único para todas las aplicaciones. En nuestro ejemplo (com.onmicrosoft.contoso.appname://redirect/path), se utiliza com.onmicrosoft.contoso.appname como esquema de Hola. Se recomienda seguir este patrón. Si dos aplicaciones comparten Hola mismo esquema, hello usuario ve un cuadro de diálogo "elegir la aplicación". Si el usuario de hello realiza una opción incorrecta, se produce un error de inicio de sesión de Hola.
* **Completo**: el URI de redirección debe tener un esquema y una ruta de acceso. ruta de acceso de Hello debe contener al menos una barra diagonal después de dominio de hello (por ejemplo, //contoso/ funciona y se produce un error de //contoso).

Asegúrese de que no hay ningún carácter especial como carácter de subrayado en hello uri de redireccionamiento.

### <a name="faulted-apps"></a>Aplicaciones con errores

Las aplicaciones B2C NO se deben editar:

* En otros portales de administración de aplicaciones, como el [Portal de Azure clásico](https://manage.windowsazure.com/) o el [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/).
* Con la API Graph o PowerShell

Si edita la aplicación hello B2C tal y como se ha descrito anteriormente e intente tooedit nuevo en la hoja de características de Azure AD B2C hello en Hola portal de Azure, se convierte en una aplicación con errores y la aplicación ya no es utilizable con Azure AD B2C. Tiene toodelete Hola aplicación y vuelva a crearlo.

aplicación de hello toodelete, vaya toohello [Portal de registro de aplicación](https://apps.dev.microsoft.com/) y eliminar la aplicación hello no existe. En orden para hello aplicación toobe visible, necesitará propietario de hello toobe de aplicación hello (y no solo un administrador de inquilinos de hello).

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una aplicación registrada con Azure AD B2C, puede realizar uno de [nuestros tutoriales de inicio rápido](active-directory-b2c-overview.md#get-started) tooget activos y en funcionamiento.

> [!div class="nextstepaction"]
> [Crear una aplicación web de ASP.NET con registro, inicio de sesión y restablecimiento de contraseña](active-directory-b2c-devquickstarts-web-dotnet-susi.md)