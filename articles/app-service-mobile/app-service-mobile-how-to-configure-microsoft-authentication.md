---
title: "autenticación de Microsoft Account aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de la autenticación de Microsoft Account tooconfigure para la aplicación de servicios de aplicaciones."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Account de Microsoft
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Account de Microsoft como un proveedor de autenticación. 

## <a name="register-microsoft-account"></a>Registro de la aplicación con la cuenta de Microsoft
1. Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour. Copia la **dirección URL**, que posteriormente utiliza tooconfigure la aplicación con Microsoft Account.
2. Navegue toohello [mis aplicaciones] página Hola Microsoft Account Developer Center e inicie sesión con su cuenta de Microsoft, si es necesario.
3. Haga clic en **Agregar una aplicación**, escriba el nombre de la aplicación y haga clic en **Crear aplicación**.
4. Tome nota de hello **Id. de aplicación**, ya que la necesitará más adelante. 
5. En "Plataformas", haga clic en **Agregar plataforma** y seleccione "Web".
6. En "URI de redireccionamiento" suministro Hola punto de conexión para la aplicación, a continuación, haga clic en **guardar**. 
   
   > [!NOTE]
   > La redirección URI es Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/microsoftaccount/callback*. Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Asegúrese de que está usando el esquema de hello HTTPS.
   
7. En "Secretos de aplicación", haga clic en **Generar nueva contraseña**. Tome nota del valor de Hola que aparece. Una vez que abandona la página de hello, no se vuelva a mostrar.

    > [!IMPORTANT]
    > contraseña de Hello es una credencial de seguridad importante. No comparta Hola contraseña con nadie ni distribuir dentro de una aplicación de cliente.

## <a name="secrets"></a>Agregar una cuenta Microsoft información tooyour aplicación de servicio de aplicaciones
1. Nuevo en hello [portal de Azure], navegue tooyour aplicación, haga clic en **configuración** > **autenticación / autorización**.
2. Si Hola autenticación / autorización característica no está habilitada, conéctelo **en**.
3. Haga clic en **Cuenta Microsoft**. Pegue en valores de identificador de la aplicación y la contraseña de Hola que obtenida anteriormente y, opcionalmente, habilite los ámbitos de que la aplicación requiere. y, a continuación, haga clic en **Aceptar**.
   
    ![][1]
   
    De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API. Debe autorizar a los usuarios en el código de la aplicación.
4. (Opcional) toorestrict acceso tooyour tooonly los usuarios del sitio autenticados la cuenta de Microsoft, establezca **tootake de acción cuando no se autentica la solicitud** demasiado**Account Microsoft**. Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas se redirigen tooMicrosoft cuenta para la autenticación.
5. Haga clic en **Guardar**.

Ya estás listo toouse Account de Microsoft para la autenticación de la aplicación.

## <a name="related-content"></a>Contenido relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[mis aplicaciones]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portal de Azure]: https://portal.azure.com/
