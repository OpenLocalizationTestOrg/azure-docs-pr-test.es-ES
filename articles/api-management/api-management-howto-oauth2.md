---
title: "las cuentas de desarrollador aaaAuthorize mediante OAuth 2.0 en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthorize mediante OAuth 2.0 en administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Cómo tooauthorize developer cuentas con OAuth 2.0 en la administración de API de Azure
Muchas API admiten [OAuth 2.0](http://oauth.net/2/) toosecure Hola API y asegúrese de que sólo los usuarios válidos tienen acceso y sólo puede tener acceso a recursos toowhich que tienen derecho. En consola para desarrolladores interactiva de administración de API de orden toouse Azure con estas API, Hola servicio le permite tooconfigure su toowork de la instancia de servicio con su OAuth 2.0 habilitado API.

## <a name="prerequisites"></a>Requisitos previos
Esta guía le mostrará cómo tooconfigure su toouse de instancia de servicio de administración de API autorización de OAuth 2.0 para desarrolladores de cuentas, pero no muestra cómo el proveedor de tooconfigure un OAuth 2.0. configuración de Hola para cada proveedor es diferente, aunque Hola pasos son similares, y partes de hello necesaria de información que se usa para configurar OAuth 2.0 en su instancia de servicio de administración de API de OAuth 2.0 Hola igual. Este tema muestra ejemplos donde Azure Active Directory actúa como proveedor de OAuth 2.0.

> [!NOTE]
> Para obtener más información sobre la configuración de OAuth 2.0 con Azure Active Directory, vea hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] ejemplo.
> 
> 

## <a name="step1"></a>Configurar un servidor de autorización OAuth 2.0 en Administración de API
tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.

![Portal del publicador][api-management-management-console]

> [!NOTE]
> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Haga clic en **seguridad** de hello **administración de API** menú hello, haga clic en **OAuth 2.0**y, a continuación, haga clic en **Agregar servidor de autorización**.

![OAuth 2.0][api-management-oauth2]

Después de hacer clic **Agregar servidor de autorización**, se muestra el formulario de servidor de autorización nuevo Hola.

![Nuevo servidor][api-management-oauth2-server-1]

Escriba un nombre y una descripción opcional en hello **nombre** y **descripción** campos. 

> [!NOTE]
> Estos campos son servidor de autorización de hello OAuth 2.0 tooidentify utilizados dentro de la instancia del servicio de administración de API actual de Hola y sus valores no proceden de servidor hello OAuth 2.0.
> 
> 

Escriba hello **dirección URL de página de registro de cliente**. Esta página es donde los usuarios pueden crear y administrar sus cuentas y varía en función de proveedor de hello OAuth 2.0 que se utiliza. Hola **dirección URL de página de registro de cliente** puntos de toohello página que los usuarios pueden usar toocreate y configurar sus propias cuentas para los proveedores de OAuth 2.0 que admiten la administración de usuarios de cuentas. Algunas organizaciones no configurar ni utilizar esta funcionalidad, incluso si el proveedor de hello OAuth 2.0 lo admite. Si el proveedor de OAuth 2.0 no tiene administración de usuarios de cuentas configuradas, escriba una marcador de posición URL aquí como dirección URL de Hola de su empresa, o una dirección URL como `https://placeholder.contoso.com`.

Hola siguiente sección de formulario de hello contiene hello **tipos de concesión de código de autorización**, **dirección URL del extremo de autorización**, y **método de solicitud de autorización** configuración.

![Nuevo servidor][api-management-oauth2-server-2]

Especificar hello **tipos de concesión de código de autorización** mediante la comprobación de tipos de hello deseado. **Código de autorización** se especifica de forma predeterminada.

Escriba hello **dirección URL del extremo de autorización**. Para Azure Active Directory, esta URL será similar toohello después de la dirección URL, donde `<client_id>` se reemplaza con el Id. de cliente de Hola que identifica el servidor de aplicaciones toohello OAuth 2.0.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Hola **método de solicitud de autorización** especifica la solicitud de autorización de Hola se envía server toohello OAuth 2.0. El valor predeterminado es **GET** .

Hola siguiente sección es donde hello **dirección URL del extremo de Token**, **métodos de autenticación de cliente**, **token de acceso de método de envío**, y **ámbitopredeterminado** se especifican.

![Nuevo servidor][api-management-oauth2-server-3]

Para un servidor de Azure Active Directory OAuth 2.0, Hola **dirección URL del extremo de Token** tendrá Hola siguiendo el formato, donde `<APPID>` tiene el formato de Hola de `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

Hola configuración predeterminada para **métodos de autenticación de cliente** es **básica**, y **token de acceso de método de envío** es **encabezado de autorización**. Estos valores se configuran en esta sección del formulario de hello, junto con hello **ámbito predeterminado**.

Hola **las credenciales de cliente** sección contiene Hola **Id. de cliente** y **secreto de cliente**, que se obtiene durante el proceso de creación y configuración de Hola de su OAuth 2.0 servidor. Una vez Hola **Id. de cliente** y **secreto de cliente** se especifican, hello **redirect_uri** para hello **código de autorización** se genera. Este URI es la dirección URL de respuesta de hello tooconfigure usado en la configuración del servidor de OAuth 2.0.

![Nuevo servidor][api-management-oauth2-server-4]

Si **tipos de concesión de código de autorización** se establece demasiado**contraseña de propietario de recurso**, hello **credenciales de contraseña de propietario de recurso** sección es toospecify usa las credenciales; en caso contrario, puede dejarlo en blanco.

![Nuevo servidor][api-management-oauth2-server-5]

Una vez completada la forma de hello, haga clic en **guardar** configuración del servidor de autorización de toosave Hola API administración OAuth 2.0. Una vez que se guarda la configuración del servidor hello, puede configurar las API toouse esta configuración, tal y como se muestra en la siguiente sección de Hola.

## <a name="step2"></a>Configurar un toouse API autorización de usuario de OAuth 2.0
Haga clic en **API** de hello **administración de API** menú Hola izquierda, haga clic en nombre de Hola de API de hello deseado, haga clic en **seguridad**y, a continuación, active casilla de Hola de **OAuth 2.0**.

![Autorización de usuario][api-management-user-authorization]

Seleccione Hola deseado **servidor de autorización** desde la lista desplegable de Hola y haga clic en **guardar**.

![Autorización de usuario][api-management-user-authorization-save]

## <a name="step3"></a>Probar la autorización del usuario hello OAuth 2.0 en hello Portal para desarrolladores
Una vez configurado el servidor de autorización de OAuth 2.0 y configura su toouse API ese servidor, puede probarlo va toohello Portal para desarrolladores y llamando a una API.  Haga clic en **portal para desarrolladores de** en el menú superior derecho de Hola.

![portal para desarrolladores][api-management-developer-portal-menu]

Haga clic en **API** en el menú superior de Hola y seleccione **API de eco**.

![API eco][api-management-apis-echo-api]

> [!NOTE]
> Si tiene sólo una API configurada o cuenta tooyour visible, a continuación, haga clic en las API le lleva directamente operaciones toohello para la API.
> 
> 

Seleccione hello **obtener recursos** operación, haga clic en **abrir la consola de**y, a continuación, seleccione **código de autorización** en Hola de lista desplegable.

![Open console][api-management-open-console]

Cuando **código de autorización** está seleccionado, se muestra una ventana emergente con forma de inicio de sesión de hello del proveedor de hello OAuth 2.0. En este ejemplo se proporciona formulario de inicio de sesión de hello Azure Active Directory.

> [!NOTE]
> Si tiene elementos emergentes deshabilitado estará solicita tooenable les explorador Hola. Después de habilitarlas, seleccione **código de autorización** nuevo y Hola se mostrará el formulario de inicio de sesión.
> 
> 

![Iniciar sesión][api-management-oauth2-signin]

Una vez que haya iniciado sesión, Hola **encabezados de solicitud** se rellenan con un `Authorization : Bearer` encabezado que autoriza la solicitud de saludo.

![Token de encabezado de solicitud][api-management-request-header-token]

En este momento puede configurar los valores de hello deseado de los parámetros restantes de Hola y enviar solicitud de saludo. 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el uso de OAuth 2.0 y administración de API, consulte el siguiente de Hola que lo acompaña y vídeo [artículo](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

