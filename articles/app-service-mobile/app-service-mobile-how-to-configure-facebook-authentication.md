---
title: "autenticación de Facebook aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure la autenticación de Facebook para la aplicación de servicios de aplicaciones."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Facebook
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Facebook como proveedor de autenticación.

procedimiento de hello toocomplete en este tema, debe tener una cuenta de Facebook que tiene una dirección de correo electrónico comprobado y un número de teléfono móvil. toocreate una nueva cuenta de Facebook, vaya demasiado[facebook.com].

## <a name="register"></a>Registro de la aplicación con Facebook
1. Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour. Copie la **Dirección URL**. Utilizará este tooconfigure la aplicación de Facebook.
2. En otra ventana del explorador, navegue toohello [a los desarrolladores de Facebook] credenciales de cuenta de sitio Web e inicie sesión con su Facebook.
3. (Opcional) Si no ya ha registrado, haga clic en **aplicaciones** > **registrar como desarrollador**, a continuación, acepte la política de Hola y siga los pasos de registro de hello.
4. Haga clic en **My Apps** (Mis aplicaciones) > **Add a New App** (Agregar una nueva aplicación) > **Website** (Sitio web) > **Skip and Create App ID** (Omitir y crear id. de aplicación). 
5. En **nombre para mostrar**, escriba un nombre único para la aplicación, el tipo de su **correo electrónico de contacto**, elija un **categoría** para la aplicación, a continuación, haga clic en **crear Id. de aplicación**y completar la comprobación de seguridad de Hola. Esto le llevará toohello panel del desarrollador para la nueva aplicación de Facebook.
6. En "Inicio de sesión de Facebook", haga clic en **Comenzar**. Agregar la aplicación **URI de redireccionamiento** demasiado**URI de redireccionamiento válido OAuth**, a continuación, haga clic en **guardar cambios**. 
   
   > [!NOTE]
   > La redirección URI es Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/facebook/callback*. Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Asegúrese de que está usando el esquema de hello HTTPS.
   > 
   > 
7. En el panel de navegación izquierdo hello, haga clic en **configuración**. En hello **secreto de la aplicación** , a continuación, haga clic en **mostrar**, proporcione la contraseña si solicitado, a continuación, tome nota de los valores de hello de **Id. de aplicación** y **secreto de la aplicación**. Use estos tooconfigure posterior de la aplicación en Azure.
   
   > [!IMPORTANT]
   > secreto de la aplicación Hello es una credencial de seguridad importante. No comparta este secreto con nadie ni lo distribuya en una aplicación cliente.
   > 
   > 
8. cuenta de Facebook que era usado tooregister Hola aplicación Hello es un administrador de la aplicación hello. En este momento, solo los administradores pueden iniciar sesión en esta aplicación. tooauthenticate otras cuentas de Facebook, haga clic en **revisión de aplicación** y habilitar **hagan < your--nombre de la aplicación > público** acceso público general tooenable mediante la autenticación de Facebook.

## <a name="secrets"></a>Tooyour aplicación de Facebook agregar información
1. Nuevo en hello [portal de Azure], navegar por la aplicación tooyour. Haga clic en **Configuración** > **Autenticación/autorización** y asegúrese de que **Autenticación de App Service** está **Activada**.
2. Haga clic en **Facebook**, pegue en valores de identificador de la aplicación y el secreto de aplicación Hola que obtenida anteriormente, si lo desea habilitar los ámbitos necesarios para la aplicación y luego haga clic en **Aceptar**.
   
    ![][0]
   
    De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API. Debe autorizar a los usuarios en el código de la aplicación.
3. (Opcional) toorestrict acceso tooyour sitio tooonly los usuarios autenticados por Facebook, establecer **tootake de acción cuando no se autentica la solicitud** demasiado**Facebook**. Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están tooFacebook redirigida para la autenticación.
4. Cuando termine de configurar la autenticación, haga clic en **Guardar**.

Ya estás listo toouse Facebook para la autenticación de la aplicación.

## <a name="related-content"></a>Contenido relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[a los desarrolladores de Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portal de Azure]: https://portal.azure.com/
