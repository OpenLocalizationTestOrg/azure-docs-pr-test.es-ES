---
title: "autenticación de Google aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure autenticación de Google para la aplicación de servicios de aplicaciones."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Google
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Google como proveedor de autenticación.

procedimiento de hello toocomplete en este tema, debe tener una cuenta de Google que tiene una dirección de correo electrónico comprobada. toocreate una nueva cuenta de Google, vaya demasiado[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Registro de la aplicación con Google
1. Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour. Copia la **dirección URL**, que use tooconfigure posterior de la aplicación de Google.
2. Navegue toohello [API de Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) sitio Web, inicie sesión con sus credenciales de cuenta de Google, haga clic en **crear proyecto**, proporcionar un **nombre del proyecto**, a continuación, haga clic en  **Crear**.
3. En **Social APIs** (API sociales), haga clic en **Google+ API** (API de Google+") y, luego, en **Enable** (Habilitar).
4. Hola a la izquierda, **credenciales** > **pantalla de consentimiento de OAuth**, a continuación, seleccione la **dirección de correo electrónico**, escriba un **Product Name**y haga clic en **guardar**.
5. Hola **credenciales** , haga clic en **crear credenciales** > **identificador de cliente OAuth**, a continuación, seleccione **aplicación Web**.
6. Pegar Hola servicio de aplicaciones **URL** que copió anteriormente en **orígenes de JavaScript autorizados**, a continuación, pegue la redirección URI en **URI de redireccionamiento autorizados**. Hola redirección URI es Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/google/callback*. Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/google/callback`. Asegúrese de que está usando el esquema de hello HTTPS. A continuación, haga clic en **Crear**.
7. En la siguiente pantalla de bienvenida, tome nota de los valores de hello de cliente de Hola secreto de cliente y el identificador.

    > [!IMPORTANT]
    > secreto del cliente de Hello es una credencial de seguridad importante. No comparta este secreto con nadie ni lo distribuya en una aplicación cliente.


## <a name="secrets"></a>Tooyour aplicación de Google agregar información
1. Nuevo en hello [portal de Azure], navegar por la aplicación tooyour. Haga clic en **Configuración** y luego en **Autenticación/autorización**.
2. Si Hola autenticación / autorización característica no está habilitada, activar conmutador Hola demasiado**en**.
3. Haga clic en **Google**. Pegue en valores de identificador de la aplicación y el secreto de aplicación Hola que obtenida anteriormente y, opcionalmente, habilite los ámbitos de que la aplicación requiere. y, a continuación, haga clic en **Aceptar**.
   
   ![][1]
   
   De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API. Debe autorizar a los usuarios en el código de la aplicación.
4. (Opcional) toorestrict acceso tooyour sitio tooonly los usuarios autenticados por Google, establecer **tootake de acción cuando no se autentica la solicitud** demasiado**Google**. Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están tooGoogle redirigida para la autenticación.
5. Haga clic en **Guardar**.

Ya estás listo toouse Google para la autenticación de la aplicación.

## <a name="related-content"></a>Contenido relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal de Azure]: https://portal.azure.com/

