---
title: "aaaAuthentication y la autorización en el servicio de aplicación de Azure | Documentos de Microsoft"
description: "Referencia conceptual e información general sobre Hola autenticación / autorización características de servicio de aplicaciones de Azure"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Autenticación y autorización en el Servicio de aplicaciones de Azure
## <a name="what-is-app-service-authentication--authorization"></a>¿Qué es la autenticación o autorización del Servicio de aplicaciones?
Aplicación servicio de autenticación o autorización es una característica que proporciona una manera para su toosign de aplicación en los usuarios para que no tengan código toochange de backend de la aplicación hello. Proporciona una manera sencilla de tooprotect la aplicación y el trabajo con datos por usuario.

El Servicio de aplicaciones usa la identidad federada, en la cual un proveedor de identidades de terceros almacena cuentas y autentica usuarios. aplicación Hello se basa en información de identidad del proveedor de Hola para que hello aplicación no tiene toostore esa información en Sí. Servicio de aplicaciones admite cinco proveedores de identidad fuera del cuadro de hello: Twitter, Facebook, Google, Microsoft Account y Azure Active Directory. La aplicación puede usar cualquier número de estos tooprovide de proveedores de identidad a los usuarios con opciones de cómo iniciar sesión en. compatibilidad integrada de tooexpand hello, se puede integrar con otro proveedor de identidades o [su propia solución de identidad personalizada][custom-auth].

Si desea tooget iniciado de forma inmediata, consulte uno de hello tutoriales:

* [Agregar aplicación de iOS de autenticación tooyour] [ iOS] (o [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [Xamarin.Forms], o [Cordova])
* [Autenticación de usuario para aplicaciones de API en Azure App Service][apia-user]
* [Introducción a Azure App Service: parte 2][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Funcionamiento de la autenticación en el Servicio de aplicaciones
En orden tooauthenticate mediante uno de los proveedores de identidades de hello, primero debe tooknow de proveedor de identidad de hello tooconfigure acerca de la aplicación. proveedor de identidades de Hello, a continuación, proporcionará los identificadores y secretos que proporcione servicio tooApp. Con esto finaliza la relación de confianza de Hola para que el servicio de aplicaciones puede validar las aserciones de usuario, como los tokens de autenticación del proveedor de identidades de Hola.

toosign en un usuario mediante uno de estos proveedores, el usuario de hello debe ser redirigido tooan extremo que inicia sesión a los usuarios para dicho proveedor. Si los clientes están utilizando un explorador web, puede tener el servicio de aplicación dirigir automáticamente todos los extremos de toohello de los usuarios no autenticados que inicia sesión a los usuarios. En caso contrario, deberá toodirect sus clientes demasiado`{your App Service base URL}/.auth/login/<provider>`, donde `<provider>` es uno de hello siguientes valores: aad, facebook, google, microsoft o twitter. En secciones posteriores de este artículo se explican los escenarios móviles y API.

Los usuarios que interactúan con su aplicación a través de un explorador web tendrán una cookie establecida de modo que puedan permanecer autenticados a medida que se desplazan por la aplicación. Para otros tipos de cliente, como dispositivos móviles, un token de web JSON (JWT), que debe presentarse en hello `X-ZUMO-AUTH` encabezado, se emitirá toohello cliente. SDK de cliente de aplicaciones móviles de Hello también controlarán esto por usted. Como alternativa, un token de acceso o el token de identidad de Azure Active Directory directamente en puede incluirse hello `Authorization` encabezado como un [token de portador](https://tools.ietf.org/html/rfc6750).

Servicio de aplicaciones se validará las cookies o símbolo (token) que la aplicación emite tooauthenticate a los usuarios. toorestrict quién puede acceder a la aplicación, vea hello [autorización](#authorization) sección más adelante en este artículo.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Funcionamiento de la autenticación con un SDK del proveedor
Después de que todo está configurado en hello back-end, puede modificar toosign clientes móviles con el servicio de aplicaciones. Hay dos enfoques aquí:

* Usar un SDK que un proveedor de identidad dada publica tooestablish identidad y, a continuación, obtener acceso tooApp servicio.
* Utilice una sola línea de código para que ese cliente de aplicaciones móviles de hello SDK puedan iniciar sesión en los usuarios.

> [!TIP]
> Mayoría de las aplicaciones debe usar un proveedor SDK tooget una experiencia más coherente cuando los usuarios inician sesión, la compatibilidad de actualización de toouse y tooget especifica ese proveedor Hola de otras ventajas.
> 
> 

Cuando se usa un proveedor de SDK, los usuarios pueden iniciar sesión tooan experiencia que se integra más estrechamente con sistema operativo de hello esa aplicación Hola se está ejecutando. Esto le brinda un token del proveedor y cierta información de usuario en el cliente de hello, que resulta mucho más fácil de gráfico de tooconsume API y personalizar la experiencia del usuario Hola. Ocasionalmente en blogs y foros, verá este hello tooas denominado "flujo de cliente" o "flujo dirigida por el cliente" porque el código de cliente de hello inicia sesión en los usuarios y el código de cliente de hello tiene el token del proveedor de acceso tooa.

Una vez obtenido un token del proveedor, debe toobe envía tooApp servicio para la validación. Después de servicio de aplicaciones se valida el token de hello, servicio de aplicaciones crea un nuevo token de servicio de aplicaciones que se devuelve a toohello cliente. SDK de cliente de aplicaciones móviles de Hello tiene toomanage de métodos de aplicación auxiliar de este intercambio y hello tooall token solicitudes toohello aplicación back-end se asocia automáticamente. Los desarrolladores también pueden guardar un token del proveedor de toohello de referencia si así lo deciden.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Autenticación móvil sin un SDK del proveedor
Si no desea tooset un proveedor de SDK, puede permitir la característica de aplicaciones móviles de Hola de toosign de servicio de aplicaciones de Azure en automáticamente. SDK de cliente de aplicaciones móviles de Hola se abra un proveedor de toohello de vista web de su elección e inicie sesión usuario Hola. En ocasiones, en blogs y foros, verá este hello tooas denominado "flujo de servidor" o "flujo dirigida por el servidor" porque servidor hello administra el proceso de Hola que inicia sesión a los usuarios y SDK de cliente de hello nunca recibe el token del proveedor Hola.

El código de toostart que este flujo se incluye en el tutorial de autenticación de Hola para cada plataforma. Al final de Hola de flujo de hello, Hola cliente SDK tiene un token de servicio de aplicaciones y el token de hello es tooall unido automáticamente las solicitudes toohello aplicación back-end.

### <a name="service-to-service-authentication"></a>Autenticación entre servicios
Aunque puede dar a los usuarios acceso tooyour aplicación, también puede confiar su propias API toocall de otra aplicación. Por ejemplo, podría hacer que una aplicación web llame a una API en otra aplicación web. En este escenario, usa credenciales para una cuenta de servicio en lugar de las credenciales de usuario tooget un token. Las cuentas de servicio también se conocen como *entidades de servicio* en la jerga de Azure Active Directory y la autenticación que usa dichas cuentas también se conoce como escenario entre servicios.

> [!IMPORTANT]
> Al ejecutarse en dispositivos de cliente, las aplicaciones móviles *no* se consideran aplicaciones de confianza y no deberían usar un flujo de la entidad de servicio. En su lugar, deben utilizar un flujo de usuario que se ha mencionado anteriormente.
> 
> 

En los escenarios entre servicios, el Servicio de aplicaciones puede proteger la aplicación mediante Azure Active Directory. aplicación que realiza la llamada de Hello solo necesita tooprovide un token de autorización principal de servicio de Azure Active Directory que se obtiene proporcionando el identificador de cliente de Hola y secreto de Azure Active Directory del cliente. Un ejemplo de este escenario que utiliza aplicaciones de API de ASP.NET se explica por tutorial Hola, [autenticación principal del servicio para las aplicaciones de API][apia-service].

Si desea toouse toohandle de autenticación de servicio de aplicaciones un escenario de servicio al servicio, puede utilizar certificados de cliente o la autenticación básica. Para obtener información acerca de los certificados de cliente en Azure, consulte [cómo tooConfigure autenticación mutua de TLS para las aplicaciones Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Para más información sobre la autenticación básica en ASP.NET, consulte [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters)(Filtros de autenticación en ASP.NET Web API 2).

Autenticación de cuentas de servicio desde una aplicación de servicio de aplicación lógica tooan API aplicaciones es un caso especial que se detalla en [mediante la API personalizada hospedada en el servicio de aplicaciones a las aplicaciones lógicas](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Funcionamiento de la autorización en el Servicio de aplicaciones
Tiene control total sobre las solicitudes de Hola que puede tener acceso a la aplicación. Aplicación servicio de autenticación / autorización se puede configurar con cualquiera de hello siguientes comportamientos:

* Permitir sólo las solicitudes autenticadas tooreach a la aplicación.
  
    Si un explorador recibe una solicitud anónima, servicio de aplicaciones le redirigirá página tooa para proveedor de identidades de Hola que elija para que los usuarios pueden iniciar sesión. Si la solicitud de hello procede de un dispositivo móvil, Hola devuelve la respuesta es HTTP *401 no autorizado* respuesta.
  
    Con esta opción, no es necesario toowrite cualquier código de autenticación en absoluto en la aplicación. Si necesita autorización más preciso, información acerca del usuario de hello es código tooyour disponible.
* Permitir tooreach de todas las solicitudes a la aplicación, pero validar las solicitudes autenticadas y pasar información de autenticación en los encabezados de hello HTTP.
  
    Esta opción difiere el código de aplicación de tooyour de las decisiones de autorización. Proporciona más flexibilidad para controlar las solicitudes anónimas, pero tiene código toowrite.
* Permitir tooreach de todas las solicitudes a la aplicación y no realizar ninguna acción en la información de autenticación de solicitudes de Hola.
  
    En este caso, Hola autenticación / autorización característica está desactivada. Hola las tareas de autenticación y autorización son completamente el tooyour del código de aplicación.

comportamientos de Hello anterior se controlan mediante hello **tootake de acción cuando no se autentica la solicitud** opción Hola portal de Azure. Si elige ** iniciar sesión *nombre de proveedor* **, todas las solicitudes tienen toobe autenticado. **Permitir solicitud (ninguna acción)** aplaza código de tooyour de decisión de autorización de hello, pero sigue ofreciendo información de autenticación. Si desea que toohave el código administrar todo el contenido, puede deshabilitar la autenticación de Hola o característica de autorización.

## <a name="working-with-user-identities-in-your-application"></a>Trabajo con identidades de usuario en la aplicación
Servicio de aplicaciones pasa alguna aplicación tooyour de información de usuario mediante el uso de encabezados especiales. Las solicitudes externas prohíben estos encabezados y solo estarán presentes si así se ha establecido mediante la autenticación o autorización del Servicio de aplicaciones. A continuación puede ver algunos encabezados de ejemplo:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Código escrito en cualquier idioma o el marco de trabajo puede obtener información de Hola que necesita de estos encabezados. Para las aplicaciones de ASP.NET 4.6, Hola **ClaimsPrincipal** se establece automáticamente con los valores adecuados de Hola.

La aplicación también puede obtener detalles de usuario adicionales a través de una solicitud HTTP GET en hello `/.auth/me` punto de conexión de la aplicación. Un token válido que se incluye con la solicitud de hello devuelvan una carga JSON con detalles acerca del proveedor de Hola que se está usando, Hola token del proveedor subyacente y otra información de usuario. servidor de aplicaciones móviles SDK Hello ofrecen métodos auxiliares toowork con estos datos. Para obtener más información, consulte [cómo toouse Hola SDK de Azure Mobile aplicaciones Node.js](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), y [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Documentación y recursos adicionales
### <a name="identity-providers"></a>Proveedores de identidades
Hola siguientes tutoriales muestran cómo tooconfigure servicio de aplicaciones toouse diferentes proveedores de autenticación:

* [Cómo tooconfigure su inicio de sesión de Azure Active Directory de toouse de aplicación][AAD]
* [Cómo tooconfigure su inicio de sesión de Facebook de toouse de aplicación][Facebook]
* [Cómo tooconfigure su inicio de sesión de Google de toouse de aplicación][Google]
* [Cómo tooconfigure su inicio de sesión de aplicación toouse Account de Microsoft][MSA]
* [Cómo tooconfigure su inicio de sesión de Twitter de toouse de aplicación][Twitter]

Si desea toouse un sistema de identidades distinto de hello los proporcionados en este caso, también puede usar hello [obtener una vista previa de compatibilidad con la autenticación personalizada en servidor de .NET de aplicaciones móviles de hello SDK][custom-auth], que se puede utilizar en las aplicaciones web, las aplicaciones móviles, o aplicaciones de API.

### <a name="web-applications"></a>Aplicaciones web
Hola tutoriales muestra cómo tooadd autenticación tooa web aplicación:

* [Introducción a Azure App Service: parte 2][web-getstarted]

### <a name="mobile-applications"></a>Aplicaciones móviles
Hola tutoriales muestra cómo tooadd autenticación tooyour los clientes móviles mediante el uso de Hola dirigida por el servidor de flujo:

* [Agregar aplicación de iOS de tooyour de autenticación][iOS]
* [Agregar aplicación de Android Authentication tooyour][Android]
* [Agregar aplicación de Windows de autenticación tooyour][Windows]
* [Agregar aplicación de autenticación tooyour Xamarin.iOS][Xamarin.iOS]
* [Agregar aplicación de autenticación tooyour Xamarin.Android][ Xamarin.Android]
* [Agregar aplicación de autenticación tooyour Xamarin.Forms][Xamarin.Forms]
* [Agregar aplicación de Cordova de autenticación tooyour][Cordova]

Usar hello recursos siguientes si desea que el flujo de dirigida por el cliente de toouse Hola para Azure Active Directory:

* [Usar hello biblioteca de autenticación de Active Directory para iOS][ADAL-iOS]
* [Usar hello biblioteca de autenticación de Active Directory para Android][ADAL-Android]
* [Usar Hola Active Directory Authentication Library para Windows y Xamarin][ADAL-dotnet]

Usar hello recursos siguientes si desea que el flujo de dirigida por el cliente de toouse Hola para Facebook:

* [Usar hello Facebook SDK para iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Usar hello recursos siguientes si desea que el flujo de dirigida por el cliente de toouse Hola de Twitter:

* [Uso de Fabric de Twitter para iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Usar hello recursos siguientes si desea que el flujo de dirigida por el cliente de toouse Hola para Google:

* [Usar hello SDK de inicio de sesión de Google para iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>Aplicaciones de API
Hola siguientes tutoriales muestran cómo tooprotect las aplicaciones de API:

* [Autenticación de usuario para aplicaciones de API en Azure App Service][apia-user]
* [Autenticación de entidad de servicio para Aplicaciones de API en Azure App Service][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
