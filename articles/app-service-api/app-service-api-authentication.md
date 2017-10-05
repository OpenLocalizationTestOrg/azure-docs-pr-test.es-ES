---
title: "Autenticación y autorización para API Apps en Azure App Service | Microsoft Docs"
description: "Obtenga información acerca de los servicios de autenticación y autorización que el Servicio de aplicaciones de Azure proporciona para Aplicaciones de API."
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
ms.openlocfilehash: f9fd533dfbd54517232f9dae5000ed4779baebd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Autenticación y autorización para Aplicaciones de API en el Servicio de aplicaciones de Azure
## <a name="overview"></a>Información general
> [!NOTE]
> Este tema se migrará al artículo consolidado [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md) , que abarca las aplicaciones web, móviles y de API.
> 
> 

Azure App Service ofrece servicios de autenticación y autorización integrados que implementan [OAuth 2.0](#oauth) y [OpenID Connect](#oauth). Este artículo describe los servicios y las opciones que están disponibles para aplicaciones de API en el Servicio de aplicaciones de Azure.

El siguiente diagrama ilustra algunas de las características clave de la autenticación de Servicio de aplicaciones:

* Preprocesa las solicitudes entrantes de API, lo que significa que funciona con cualquier lenguaje o marco admitido por el Servicio de aplicaciones.
* Le ofrece varias opciones para elegir cuánto trabajo de autenticación desea realizar en su propio código.
* Funciona para la autenticación tanto del usuario final como de la cuenta de servicio. 
* Admite cinco proveedores de identidades: Azure Active Directory, Facebook, Google, Twitter y cuenta de Microsoft.
* Funciona igual para Aplicaciones de API, Aplicaciones Web y Aplicaciones móviles.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Independencia de lenguajes
El procesamiento de la autenticación de Servicio de aplicaciones se produce antes de que las solicitudes lleguen a su aplicación de API, lo que significa que las características de autenticación funcionan para las aplicaciones de API escritas en cualquier lenguaje o marco.  La API se puede basar en ASP.NET, Java, Node.js o en cualquier marco compatible con el Servicio de aplicaciones.

El Servicio de aplicaciones pasa el token web JSON (JWT) en el encabezado de autorización de una solicitud HTTP y el código escrito en cualquier lenguaje o marco puede obtener la información que necesita del token. Además, el Servicio de aplicaciones facilita el acceso a las notificaciones más utilizadas, para lo que establece algunos encabezados especiales como:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

En una API de .NET se puede usar el atributo `Authorize` y, en el caso de una autorización específica, se puede escribir fácilmente código según las notificaciones, ya que la información de las notificaciones se rellena automáticamente en las clases .NET.

## <a name="multiple-protection-options"></a>Varias opciones de protección
El Servicio de aplicaciones puede impedir que las solicitudes anónimas de HTTP lleguen a su aplicación de API, puede pasar todas las solicitudes y validar los tokens para las solicitudes que los incluyen o puede dejar pasar todas las solicitudes sin realizar ninguna acción en ellas:

1. Permitir que solo lleguen a la aplicaciones de API las solicitudes autenticadas.
   
    Si se recibe una solicitud anónima desde un explorador, el Servicio de aplicaciones le redirigirá a una página de inicio de sesión para el proveedor de autenticación (Azure AD, Google, Twitter, etc.) que elija. 
   
    Con esta opción, no es preciso escribir código de autenticación en la aplicación y el código de autorización se simplifica, ya que las notificaciones más importantes se proporcionan en los encabezados HTTP.
2. Permitir que todas las solicitudes lleguen a la aplicación de API, pero validar las solicitudes autenticadas y pasar la información de autenticación en los encabezados HTTP.
   
    Esta opción le proporciona más flexibilidad en el tratamiento de solicitudes anónimas, pero tendrá que escribir código si desea impedir que los usuarios anónimos utilicen la API. Puesto que las notificaciones más populares se pasan en los encabezados de solicitudes HTTP, el código de autorización es relativamente sencillo.
3. Permitir que todas las solicitudes lleguen a la API, no realizar acciones relativas a la información de autenticación de las solicitudes.
   
    Esta opción deja las tareas de autenticación y autorización totalmente en manos del código de la aplicación.

En el [Portal de Azure](https://portal.azure.com/), seleccione la opción que desee en la hoja **Autenticación o autorización** .

![](./media/app-service-api-authentication/authblade.png)

Para las opciones 1 y 2, active **Autenticación de App Service** y en la lista desplegable **Acción necesaria cuando la solicitud no está autenticada** elija **Iniciar sesión** o **Permitir solicitud (ninguna acción)**.  Si elige **Iniciar sesión**, tendrá que elegir un proveedor de autenticación y configurarlo.

![](./media/app-service-api-authentication/actiontotake.png)

Para más información sobre cómo configurar la autenticación, consulte [Configuración de la aplicación del Servicio de aplicaciones para usar el inicio de sesión de Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). El artículo se aplica a aplicaciones de API, así como a aplicaciones móviles, e incluye vínculos a otros artículos para los demás proveedores de autenticación.

## <a id="internal"></a> Autenticación de cuentas de servicio
La autenticación del Servicio de aplicaciones también funciona en escenarios internos, como para la realización de llamadas de una aplicación de API a otra. En este escenario se puede obtener un token mediante credenciales para una cuenta de servicio, en lugar de las credenciales de usuario final. Las cuentas de servicio también se conocen como *entidades de servicio* en Azure Active Directory y la autenticación que usa dichas cuenta también se conoce como escenario entre servicios. 

En los escenarios entre servicios, proteja la aplicación de API llamada mediante Azure Active Directory y proporcione un token de autorización de la entidad de servicio de AAD al llamar a la aplicación de API. Puede obtener un token mediante la especificación del identificador de cliente y el secreto de cliente desde la aplicación de AAD. No se necesita ningún código especial solo para Azure, como el que se solía usar para controlar el token de Zumo de Servicios móviles. Un ejemplo del uso de este escenario por parte de aplicaciones de API de ASP.NET puede encontrarse en el tutorial [Autenticación de entidad de servicio para Aplicaciones de API en el Servicio de aplicaciones de Azure](app-service-api-dotnet-service-principal-auth.md).

Si desea administrar un escenario de servicio a servicio sin usar la autenticación del Servicio de aplicaciones, puede usar certificados de cliente o una autenticación básica. Para obtener información acerca de los certificados de cliente en Azure, consulte [Configuración de la autenticación mutua de TLS para una aplicación web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Para más información sobre la autenticación básica en ASP.NET, consulte [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters)(Filtros de autenticación en ASP.NET Web API 2).

La autenticación de cuentas de servicio desde una aplicación lógica de Servicio de aplicaciones en una aplicación de API es un caso especial que se explica en [Uso de la API personalizada hospedada en Servicio de aplicaciones con aplicaciones lógicas](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Autenticación de cliente móvil
Para más información sobre cómo controlar la autenticación desde clientes móviles, consulte la [documentación sobre la autenticación para aplicaciones móviles](../app-service-mobile/app-service-mobile-ios-get-started-users.md). La autenticación de Servicio de aplicaciones funciona igual para aplicaciones móviles y aplicaciones de API.

## <a name="more-information"></a>Más información
Para más información sobre la autenticación y la autorización del Servicio de aplicaciones de Azure, consulte los siguientes recursos:

* [Expanding App Service authentication / authorization](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (Cómo configurar la aplicación del Servicio de aplicaciones para usar el inicio de sesión de Azure Active Directory), con vínculos a otros proveedores de autenticación en la parte superior de la página. 

Para obtener más información sobre OAuth 2.0, OpenID Connect y JSON Web Tokens (JWT), consulte los siguientes recursos.

* [Introducción a OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [Introducción a OAuth2, OpenID Connect y JSON Web Tokens (JWT): curso de Pluralsight](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Cómo compilar una API de RESTful y garantizar su seguridad para varios clientes en ASP.NET: curso de PluralSight](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Para más información acerca de Azure Active Directory, consulte los siguientes recursos.

* [Escenarios de Azure AD](http://aka.ms/aadscenarios)
* [Guía para desarrolladores de Azure AD](http://aka.ms/aaddev)
* [Ejemplos de Azure AD](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Pasos siguientes
En este artículo se han explicado las características de autenticación y autorización del Servicio de aplicaciones que puede utilizar para las aplicaciones de API. En el siguiente tutorial de la serie de introducción, aprenderá a implementar la [autenticación de usuario para aplicaciones de API del Servicio de aplicaciones](app-service-api-dotnet-user-principal-auth.md).

