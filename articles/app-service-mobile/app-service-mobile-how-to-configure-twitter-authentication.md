---
title: "autenticación de Twitter aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure autenticación de Twitter para la aplicación de servicios de aplicaciones."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Twitter
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Twitter como proveedor de autenticación.

procedimiento de hello toocomplete en este tema, debe tener una cuenta de Twitter que tiene un número de dirección y el teléfono de correo electrónico comprobada. toocreate una nueva cuenta de Twitter, vaya demasiado<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Registro de la aplicación con Twitter
1. Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour. Copie la **Dirección URL**. Utilizará este tooconfigure la aplicación de Twitter.
2. Navegue toohello [desarrolladores Twitter] de sitio Web, inicie sesión con sus credenciales de cuenta de Twitter y haga clic en **crear una aplicación nueva**.
3. Tipo de hello **nombre** y un **descripción** para la nueva aplicación. Pegar en la aplicación **URL** para hello **sitio Web** valor. A continuación, en hello **dirección URL de devolución de llamada**, pegue hello **dirección URL de devolución de llamada** que copió anteriormente. Se trata de la puerta de enlace de la aplicación móvil anexado con ruta de acceso de hello, */.auth/login/twitter/callback*. Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Asegúrese de que está usando el esquema de hello HTTPS.
4. En las páginas de hello en parte inferior de hello, lea y acepte los términos de Hola. A continuación, haga clic en **Crear aplicación de Twitter**. Esta aplicación de hello registros muestra detalles de la aplicación hello.
5. Haga clic en hello **configuración** ficha, comprobación de **permitir este toosign de toobe usa de la aplicación con Twitter**, a continuación, haga clic en **configuración de actualización de**.
6. Seleccione hello **claves y Tokens de acceso** ficha. Tome nota de los valores de hello de **consumidor clave (API)** y **secreto del consumidor (secreto de API)**.
   
   > [!NOTE]
   > secreto del consumidor Hello es una credencial de seguridad importante. por lo que no debe compartirlo con nadie ni distribuirlo con su aplicación.
   > 
   > 

## <a name="secrets"></a>Agregar Twitter aplicación tooyour de información
1. Nuevo en hello [portal de Azure], navegar por la aplicación tooyour. Haga clic en **Configuración** y luego en **Autenticación/autorización**.
2. Si Hola autenticación / autorización característica no está habilitada, activar conmutador Hola demasiado**en**.
3. Haga clic en **Twitter**. Pegue en hello Id. de aplicación y el secreto de aplicación valores que obtenida anteriormente. y, a continuación, haga clic en **Aceptar**.
   
   ![][1]
   
   De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API. Debe autorizar a los usuarios en el código de la aplicación.
4. (Opcional) toorestrict acceso tooyour sitio tooonly los usuarios autenticados por Twitter, establecer **tootake de acción cuando no se autentica la solicitud** demasiado**Twitter**. Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están tooTwitter redirigida para la autenticación.
5. Haga clic en **Guardar**.

Ya estás listo toouse Twitter para la autenticación de la aplicación.

## <a name="related-content"></a>Contenido relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[desarrolladores Twitter]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portal de Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
