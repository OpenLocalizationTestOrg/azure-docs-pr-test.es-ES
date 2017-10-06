---
title: "aaaAuthentication y autorización para las aplicaciones de API de servicio de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los servicios de autenticación y autorización de Hola que proporciona el servicio de aplicaciones de Azure para aplicaciones de API."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Autenticación y autorización para Aplicaciones de API en el Servicio de aplicaciones de Azure
## <a name="overview"></a>Información general
> [!NOTE]
> En este tema será tooa migrada consolidado [aplicación de servicio de autenticación / autorización](../app-service/app-service-authentication-overview.md) tema, que cubre a Web, móviles y aplicaciones de API.
> 
> 

Azure App Service ofrece servicios de autenticación y autorización integrados que implementan [OAuth 2.0](#oauth) y [OpenID Connect](#oauth). Este artículo describen los servicios de Hola y opciones que están disponibles para las aplicaciones de API de servicio de aplicaciones de Azure.

Hola siguiente diagrama muestra algunas características clave de autenticación de servicio de aplicaciones:

* Preprocesa las solicitudes entrantes de API, lo que significa que funciona con cualquier lenguaje o marco admitido por el Servicio de aplicaciones.
* Ofrece varias opciones para el trabajo de autenticación de la cantidad desea toodo en su propio código.
* Funciona para la autenticación tanto del usuario final como de la cuenta de servicio. 
* Admite cinco proveedores de identidades: Azure Active Directory, Facebook, Google, Twitter y cuenta de Microsoft.
* Lo Hola funciona igual para aplicaciones de API, las aplicaciones Web y aplicaciones móviles.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Independencia de lenguajes
Procesamiento de autenticación de servicio de aplicaciones se produce antes de que las solicitudes llegan a la aplicación de API, lo que significa que las características de autenticación Hola funcionen para aplicaciones de API escritas en cualquier lenguaje o el marco de trabajo.  La API se puede basar en ASP.NET, Java, Node.js o en cualquier marco compatible con el Servicio de aplicaciones.

Servicio de aplicaciones que se pasa en el token de web JSON (JWT) de Hola Hola encabezado de autorización de una solicitud HTTP, y el código escrito en cualquier idioma o el marco de trabajo puede obtener información de Hola que necesita de hello símbolo (token). Además, servicio de aplicaciones proporciona acceso más fácil toohello suelen usada notificaciones estableciendo algunos encabezados especiales, como siguiente hello:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

En una API. NET, puede usar hello `Authorize` de atributo y para la autorización específica puede escribir fácilmente código en función de notificaciones porque la información de notificaciones se rellena automáticamente en las clases .NET.

## <a name="multiple-protection-options"></a>Varias opciones de protección
El Servicio de aplicaciones puede impedir que las solicitudes anónimas de HTTP lleguen a su aplicación de API, puede pasar todas las solicitudes y validar los tokens para las solicitudes que los incluyen o puede dejar pasar todas las solicitudes sin realizar ninguna acción en ellas:

1. Permitir sólo las solicitudes autenticadas tooreach a su aplicación de API.
   
    Si se recibe una solicitud anónima desde un explorador, el servicio de aplicaciones redirigirá tooa página de inicio de sesión de proveedor de autenticación de Hola (Twitter de AD, Google, Azure, etc.) que desee. 
   
    Con esta opción, no necesita toowrite cualquier código de autenticación en absoluto en la aplicación, y código de autorización se simplifica porque se proporcionan notificaciones más importantes de hello en encabezados HTTP Hola.
2. Permitir tooreach de todas las solicitudes a su aplicación de API, pero validar las solicitudes autenticadas y pasar información de autenticación en los encabezados de hello HTTP.
   
    Esta opción proporciona una mayor flexibilidad para controlar las solicitudes anónimas, pero tienes toowrite código si desea que los usuarios anónimos de tooprevent del uso de la API. Puesto que se pasan notificaciones más populares de hello en encabezados de Hola de solicitudes HTTP, el código de autorización es relativamente sencilla.
3. Permitir tooreach de todas las solicitudes de la API, no realizar ninguna acción en la información de autenticación de solicitudes de Hola.
   
    Esta opción deja tareas Hola de autenticación y autorización completamente el tooyour del código de aplicación.

Hola [portal de Azure](https://portal.azure.com/), Seleccionar opción de Hola que desee en hello **autenticación / autorización** hoja.

![](./media/app-service-api-authentication/authblade.png)

Para las opciones 1 y 2, activar **autenticación del servicio de aplicación**y en hello **tootake de acción cuando no se autentica la solicitud** lista desplegable y elija **sesión** o **Permitir solicitud (ninguna acción)**.  Si elige **sesión**, tiene un proveedor de autenticación de toochoose y configurar ese proveedor.

![](./media/app-service-api-authentication/actiontotake.png)

Para obtener información detallada acerca de cómo tooconfigure la autenticación, vea [cómo tooconfigure su inicio de sesión de Azure Active Directory de servicio de aplicaciones aplicación toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). aplica el artículo de Hello tooAPI aplicaciones, así como las aplicaciones móviles, e incluye vínculos a artículos de tooother para hello otros proveedores de autenticación.

## <a id="internal"></a> Autenticación de cuentas de servicio
Autenticación de servicio de aplicaciones funciona en escenarios internos como para llamar desde una aplicación de API tooanother de aplicación de API. En este escenario se puede obtener un token mediante credenciales para una cuenta de servicio, en lugar de las credenciales de usuario final. Las cuentas de servicio también se conocen como *entidades de servicio* en Azure Active Directory y la autenticación que usa dichas cuenta también se conoce como escenario entre servicios. 

Para los escenarios de servicio al servicio, proteja Hola llamada a aplicación de API con Azure Active Directory y proporcionar un token de autorización principal de servicio AAD cuando se llama a la aplicación hello API. Obtener un token proporcionando Hola Id. de cliente y secreto de aplicación AAD de Hola de cliente. Se requiere, como true toobe usado para controlar el token de Zumo de servicios móviles de hello ningún código de solo Azure especial. Un ejemplo de este escenario mediante aplicaciones de API de ASP.NET está cubierto por el tutorial Hola [autenticación principal del servicio para las aplicaciones de la API](app-service-api-dotnet-service-principal-auth.md).

Si desea toohandle un escenario de servicio a servicio sin usar la autenticación de servicio de aplicaciones, puede utilizar certificados de cliente o la autenticación básica. Para obtener información acerca de los certificados de cliente en Azure, consulte [cómo tooConfigure autenticación mutua de TLS para las aplicaciones Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Para más información sobre la autenticación básica en ASP.NET, consulte [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters)(Filtros de autenticación en ASP.NET Web API 2).

Autenticación de cuentas de servicio desde una aplicación de servicio de aplicación lógica tooan API aplicaciones es un caso especial que se explica en [mediante la API personalizada hospedada en el servicio de aplicaciones a las aplicaciones lógicas](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Autenticación de cliente móvil
Para obtener información acerca de cómo toohandle autenticación desde clientes móviles, vea hello [documentación sobre la autenticación para aplicaciones móviles](../app-service-mobile/app-service-mobile-ios-get-started-users.md). Autenticación de servicio de aplicaciones funciona Hola igual para aplicaciones móviles y aplicaciones de API.

## <a name="more-information"></a>Más información
Para obtener más información sobre la autenticación y autorización en el servicio de aplicación de Azure, vea Hola recursos siguientes:

* [Expanding App Service authentication / authorization](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Cómo tooconfigure su inicio de sesión de Azure Active Directory de servicio de aplicaciones aplicación toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (incluye enlaces para otros proveedores de autenticación al principio de Hola de página de hello). 

Para obtener más información acerca de OAuth 2.0, OpenID Connect y Tokens de Web JSON (JWT), vea Hola recursos siguientes.

* [Introducción a OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [Introducción tooOAuth2, OpenID Connect y Tokens de Web JSON (JWT) - curso Pluralsight](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Cómo compilar una API de RESTful y garantizar su seguridad para varios clientes en ASP.NET: curso de PluralSight](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Para obtener más información acerca de Active Directory de Azure, vea Hola recursos siguientes.

* [Escenarios de Azure AD](http://aka.ms/aadscenarios)
* [Guía para desarrolladores de Azure AD](http://aka.ms/aaddev)
* [Ejemplos de Azure AD](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Pasos siguientes
En este artículo se han explicado las características de autenticación y autorización del Servicio de aplicaciones que puede utilizar para las aplicaciones de API. tutorial siguiente de Hello para la obtención de hello iniciado serie se muestra cómo tooimplement [autenticación de usuario en aplicaciones de API de servicio de aplicación](app-service-api-dotnet-user-principal-auth.md).

