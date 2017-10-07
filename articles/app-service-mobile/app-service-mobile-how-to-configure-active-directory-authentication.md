---
title: "autenticación de Azure Active Directory aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure autenticación de Azure Active Directory para la aplicación de servicios de aplicaciones."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Azure Active Directory
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tema muestra cómo tooconfigure toouse de servicios de aplicaciones de Azure Active Directory como un proveedor de autenticación de Azure.

## <a name="express"></a>Configuración de Azure Active Directory mediante la configuración rápida
1. Hola [portal de Azure], navegar por la aplicación tooyour. Haga clic en **Configuración** y luego en **Autenticación/autorización**.
2. Si Hola autenticación / autorización característica no está habilitada, activar conmutador Hola demasiado**en**.
3. Haga clic en **Azure Active Directory** y luego en **Rápida** en **Modo de administración**.
4. Haga clic en **Aceptar** tooregister aplicación de hello en Azure Active Directory. Se creará un nuevo registro. Si desea toochoose un registro existente en su lugar, haga clic en **seleccionar una aplicación existente** y, a continuación, busque nombre Hola de un registro creado anteriormente en el inquilino.
   Haga clic en tooselect de registro de hello y haga clic en **Aceptar**. A continuación, haga clic en **Aceptar** en la hoja de configuración de hello Azure Active Directory.
   
   ![][0]
   
   De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API. Debe autorizar a los usuarios en el código de la aplicación.
5. (Opcional) toorestrict acceso tooyour tooonly los usuarios del sitio autenticados por Azure Active Directory, establezca **tootake de acción cuando no se autentica la solicitud** demasiado**iniciar sesión con Azure Active Directory**. Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están redirigida tooAzure Active Directory para la autenticación.
6. Haga clic en **Guardar**.

Ya estás listo toouse Azure Active Directory para la autenticación de la aplicación.

## <a name="advanced"></a>(Método alternativo) Configuración manual de Azure Active Directory con la configuración avanzada
También puede elegir tooprovide configuración manualmente. Ésta es la solución de hello preferido si inquilino de AAD Hola desea toouse es diferente del inquilino de hello con el que iniciar sesión en Azure. configuración de hello toocomplete, primero debe crear un registro en Azure Active Directory y, a continuación, debe proporcionar algunos tooApp de detalles de registro de hello servicio.

### <a name="register"></a>Registro de la aplicación con Azure Active Directory
1. Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour. Copie la **Dirección URL**. Utilizará este tooconfigure la aplicación de Azure Active Directory.
2. Inicie sesión en toohello [portal de Azure clásico] y navegue demasiado**Active Directory**.
   
    ![][2]
3. Seleccione el directorio y, a continuación, seleccione hello **aplicaciones** ficha situada en la parte superior de Hola. Haga clic en **agregar** en la parte inferior de hello toocreate un nuevo registro de aplicación.
4. Haga clic en **Agregar una aplicación que mi organización está desarrollando**.
5. Hola Asistente para agregar la aplicación en la consulta, escriba un **nombre** para su aplicación y haga clic en hello **aplicación Web Y/o API de Web** tipo. A continuación, haga clic en toocontinue.
6. Hola **dirección URL de inicio de sesión** cuadro, pegue la dirección URL de la aplicación hello que copió anteriormente. Escriba esa misma dirección URL en hello **App ID URI** cuadro. A continuación, haga clic en toocontinue.
7. Una vez que se ha agregado la aplicación hello, haga clic en hello **configurar** ficha. Editar hello **dirección URL de respuesta** en **Single Sign-on** toobe Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/aad/callback*. Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Asegúrese de que está usando el esquema de hello HTTPS.
   
    ![][3]
8. Haga clic en **Guardar**. A continuación, Hola copia **Id. de cliente** para la aplicación hello. Va a configurar su aplicación toouse esto más adelante.
9. En la barra de comandos de la parte inferior de hello, haga clic en **ver extremos**y, a continuación, copia Hola **documento de metadatos de federación** dirección URL y descarga que documente o navegue tooit en un explorador.
10. En la raíz de Hola **EntityDescriptor** elemento, debería haber un **entityID** atributo de formato de hello `https://sts.windows.net/` seguido de un inquilino de tooyour específico de GUID (denominado una "Id. de inquilino"). Copie este valor, actuará como **URL del emisor**. Va a configurar su aplicación toouse esto más adelante.

### <a name="secrets"></a>Aplicación de agregar Azure Active Directory information tooyour
1. Nuevo en hello [portal de Azure], navegar por la aplicación tooyour. Haga clic en **Configuración** y luego en **Autenticación/autorización**.
2. Si no está habilitada la característica de autenticación/autorización de hello, activar conmutador Hola demasiado**en**.
3. Haga clic en **Azure Active Directory** y luego haga clic en **Avanzada** en **Modo de administración**. Pegar en hello Id. de cliente y la dirección URL del emisor de valor que se puede obtenida anteriormente. y, a continuación, haga clic en **Aceptar**.
   
   ![][1]
   
   De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API. Debe autorizar a los usuarios en el código de la aplicación.
4. (Opcional) toorestrict acceso tooyour tooonly los usuarios del sitio autenticados por Azure Active Directory, establezca **tootake de acción cuando no se autentica la solicitud** demasiado**iniciar sesión con Azure Active Directory**. Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están redirigida tooAzure Active Directory para la autenticación.
5. Haga clic en **Guardar**.

Ya estás listo toouse Azure Active Directory para la autenticación de la aplicación.

## <a name="optional-configure-a-native-client-application"></a>(Opcional) Configurar una aplicación de cliente nativo
Azure Active Directory también permite a tooregister clientes nativos, lo que proporciona mayor control sobre la asignación de permisos. Lo necesita si desea utilizar una biblioteca como Hola de inicios de sesión de tooperform **biblioteca de autenticación de Active Directory**.

1. Navegue demasiado**Active Directory** en hello [portal de Azure clásico].
2. Seleccione el directorio y, a continuación, seleccione hello **aplicaciones** ficha situada en la parte superior de Hola. Haga clic en **agregar** en la parte inferior de hello toocreate un nuevo registro de aplicación.
3. Haga clic en **Agregar una aplicación que mi organización está desarrollando**.
4. Hola Asistente para agregar la aplicación en la consulta, escriba un **nombre** para su aplicación y haga clic en hello **aplicación cliente nativa** tipo. A continuación, haga clic en toocontinue.
5. Hola **URI de redireccionamiento** cuadro, escriba su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS. Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*. Si crea una aplicación de Windows, en su lugar use hello [SID del paquete](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) como Hola URI.
6. Una vez que se ha agregado la aplicación nativa de hello, haga clic en hello **configurar** ficha. Buscar hello **Id. de cliente** y tome nota de este valor.
7. Desplazamiento Hola AV PÁG toohello **permisos tooother aplicaciones** sección y haga clic en **Agregar aplicación**.
8. Busque la aplicación web de Hola que registraron anteriormente y haga clic en el icono de hello más. A continuación, haga clic en el cuadro de diálogo de hello comprobación tooclose Hola. Si la aplicación web de hello no se puede encontrar, desplácese tooits registro y agregar una nueva dirección de URL de respuesta (p. ej., Hola versión HTTP de la dirección URL actual), haga clic en Guardar y, a continuación, repita estos pasos: aplicación hello debería aparecer en la lista de Hola.
9. En la que acaba de agregar la entrada nuevo a hello, abra hello **permisos delegados** lista desplegable y seleccione **acceso (appName)**. A continuación, haga clic en **Guardar**.

Ahora ha configurado una aplicación de cliente nativo que puede acceder a la aplicación del Servicio de aplicaciones.

## <a name="related-content"></a>Contenido relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[Portal de Azure]: https://portal.azure.com/
[Portal de Azure clásico]: https://manage.windowsazure.com/
[alternative method]:#advanced
