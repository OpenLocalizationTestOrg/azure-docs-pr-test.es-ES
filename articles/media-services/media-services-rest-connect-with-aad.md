---
title: "aaaUse tooaccess de autenticación de Azure AD API de servicios multimedia de Azure con REST | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooaccess API de servicios multimedia de Azure con la autenticación de Azure Active Directory mediante el uso de REST."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Tooaccess de autenticación de Azure AD use Hola API de servicios multimedia de Azure con REST

equipo de servicios multimedia de Azure de Hello ha publicado la compatibilidad con la autenticación de Azure Active Directory (Azure AD) para el acceso de servicios multimedia de Azure. También anunció la autenticación del servicio de Control de acceso de Azure de planes toodeprecate para el acceso a los servicios multimedia. Dado que cada suscripción de Azure y cada cuenta de servicios multimedia son inquilino tooan adjunto Azure AD, compatibilidad con la autenticación de Azure AD ofrece muchos beneficios de seguridad. Para obtener más información acerca de este cambio y la migración (si se utiliza Hola SDK de .NET de servicios multimedia para la aplicación), consulte siguiente Hola entradas de blog y los artículos:

- [Azure Media Services announces support for Azure AD and deprecation of Access Control authentication](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation) (Azure Media Services anuncia la compatibilidad con Azure AD y el desuso de la autenticación de Access Control)
- [Access Azure Media Services API by using Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md) (Acceder a la API de Azure Media Services mediante la autenticación de Azure AD)
- [Usar autenticación de Azure AD tooaccess API de servicios multimedia de Azure mediante Microsoft .NET](media-services-dotnet-get-started-with-aad.md)
- [Introducción a la autenticación de Azure AD mediante el uso de Hola portal de Azure](media-services-portal-get-started-with-aad.md)

Algunos clientes necesitan toodevelop sus soluciones de servicios multimedia en hello siguiendo las restricciones:

*   Utiliza un lenguaje de programación que no sea Microsoft .NET o C# o entorno en tiempo de ejecución de hello no es Windows.
*   Bibliotecas de Azure AD, como bibliotecas de autenticación de Active Directory no están disponibles para el lenguaje de programación de Hola o no se puede usar para su entorno en tiempo de ejecución.

Algunos clientes han desarrollado aplicaciones mediante la API de REST para la autenticación de Access Control y el acceso a Azure Media Services. Para estos clientes, necesita un Hola solo API de REST toouse de manera para autenticación de Azure AD y acceso subsiguiente de los servicios de multimedia de Azure. Necesita toonot se basan en cualquiera de las bibliotecas de hello Azure AD o en hello SDK de .NET de servicios multimedia. En este artículo se describe una solución y se proporciona código de ejemplo para este escenario. Dado que el código de hello es todas las llamadas de API de REST, con ninguna dependencia de Azure AD o biblioteca de servicios multimedia de Azure, código de hello fácilmente puede ser traducido tooany otro lenguaje de programación.

> [!IMPORTANT]
> Actualmente, servicios multimedia admite el modelo de autenticación de servicios de Control de acceso de Azure Hola. No obstante, la autenticación de Access Control dejará de usarse el 1 de junio de 2018. Se recomienda que migre modelo de autenticación de Azure AD toohello tan pronto como sea posible.


## <a name="design"></a>Diseño

En este artículo, se utiliza Hola después de diseño de autenticación y autorización:

*  Protocolo de autorización: OAuth 2.0. OAuth 2.0 es un estándar de seguridad web que cubre la autenticación y la autorización. Es compatible con Google, Microsoft, Facebook y PayPal. Se ratificó en octubre de 2012. Microsoft es firme partidario de OAuth 2.0 y OpenID Connect. Ambos estándares son compatibles con varios servicios y bibliotecas de cliente, incluidos Azure Active Directory, Open Web Interface for .NET (OWIN), Katana y las bibliotecas de Azure AD.
*  Tipo de concesión: credenciales de cliente. Las credenciales del cliente es uno de los tipos de concesión de cuatro de hello en OAuth 2.0. A menudo se usa para el acceso a la API de Microsoft Graph de Azure AD.
*  Modo de autenticación: entidad de servicio. Hola otro modo de autenticación es autenticación interactiva o usuario.

Un total de cuatro aplicaciones o servicios implicados en el flujo de autenticación y autorización de hello Azure AD para el uso de servicios multimedia. las aplicaciones de Hola y servicios de flujo de hello, se describen en hello en la tabla siguiente:

|Tipo de aplicación |Application |Flujo|
|---|---|---|
|Cliente | Aplicación o solución de cliente | Esta aplicación (en realidad, su proxy) se registra en el inquilino de Azure AD de hello en qué Hola multimedia de hello y suscripción de Azure se encuentra la cuenta de servicio. Hello entidad de servicio de aplicación hello registrado se le conceden con rol de propietario o colaborador en hello Access Control (IAM) de la cuenta de servicio de hello multimedia. entidad de servicio de Hola se representa mediante Hola aplicación cliente y el Id. de clave secreta de cliente. |
|Proveedor de identidades (IDP) | Azure AD como IDP | entidad de servicio de aplicación registrado Hello (Id. de cliente y el secreto de cliente) se autentica con Azure AD como Hola IDP. Esta autenticación se realiza interna e implícitamente. Como en el flujo de credenciales de cliente se autentica el cliente de hello en lugar de usuario de Hola. |
|Servicio de token seguro (STS) o servidor OAuth | Azure AD como STS | Después de la autenticación por hello IDP (o servidor de OAuth en términos de OAuth 2.0), Azure AD como servidor STS/OAuth para el recurso de nivel intermedio de acceso toohello emite un token de acceso o JSON Web Token (JWT): en nuestro caso, Hola extremo de API de REST de servicios multimedia. |
|Recurso | API de REST de Media Services | Todas las llamadas API de REST de servicios de multimedia está autorizada por un token de acceso que es emitido por Azure AD como servidor de OAuth de Hola o STS. |

Si ejecuta el código de ejemplo de Hola y capturar un JWT o un token de acceso, hello JWT tiene Hola siguientes atributos:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Estas son las asignaciones de Hola entre atributos Hola Hola hello y JWT cuatro las aplicaciones o servicios en la tabla anterior de Hola:

|Tipo de aplicación |Application |Atributo del JWT |
|---|---|---|
|Cliente |Aplicación o solución de cliente |appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". Id. de cliente de Hola de una aplicación registrará tooAzure AD en la sección siguiente Hola. |
|Proveedor de identidades (IDP) | Azure AD como IDP |idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Hola GUID es el inquilino de Id. de Microsoft de hello (microsoft.onmicrosoft.com). Cada inquilino tiene su propio identificador único. |
|Servicio de token seguro (STS) o servidor OAuth |Azure AD como STS | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Hola GUID es el inquilino de Id. de Microsoft de hello (microsoft.onmicrosoft.com). |
|Recurso | API de REST de Media Services |aud: "https://rest.media.azure.net". destinatario de Hola o audiencia del token de acceso de Hola. |

## <a name="steps-for-setup"></a>Pasos de configuración

tooregister y configurar una aplicación de Azure AD para autenticación de Azure AD y tooobtain un token de acceso para llamar a un extremo de API de REST de servicios multimedia de Azure de hello, Hola completa pasos:

1.  Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), registrar un inquilino de Azure AD toohello de aplicación (por ejemplo, wzmediaservice) de Azure AD (por ejemplo, microsoft.onmicrosoft.com). No importa si se ha registrado como aplicación web o nativa. Además, puede elegir cualquier dirección URL de inicio de sesión y de respuesta (por ejemplo, http://wzmediaservice.com para ambas).
2. Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), vaya toohello **configurar** pestaña de la aplicación. Hola Nota **Id. de cliente**. Luego, en **Claves**, genere una **clave de cliente** (secreto del cliente). 

    > [!NOTE] 
    > Tome nota de secreto del cliente Hola. No se volverá a mostrar.
    
3.  Hola [portal de Azure](http://ms.portal.azure.com), vaya toohello cuenta de servicios multimedia. Seleccione hello **el Control de acceso** panel de (índices IAM). Agregar a un nuevo miembro que tenga Hola propietario o rol de colaborador de Hola. De entidad de seguridad de hello, busque el nombre de la aplicación hello registrado en el paso 1 (en este ejemplo, wzmediaservice).

## <a name="info-toocollect"></a>Toocollect de información

tooprepare de codificación de REST, recopilar Hola después tooinclude de puntos de datos en el código de hello:

*   Azure AD como punto de conexión de STS: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. Desde este punto de conexión se solicita un token de acceso JWT. Además tooserving como un IDP, Azure AD también actúa como un STS. Azure AD emite un JWT para el acceso a los recursos (un token de acceso). Un token JWT tiene distintas notificaciones.
*   API de REST de Azure Media Services como recurso o audiencia: https://rest.media.azure.net.
*   Id. de cliente: vea el paso 2 de [Pasos de configuración](#steps-for-setup).
*   Secreto del cliente: vea el paso 2 de [Pasos de configuración](#steps-for-setup).
*   El extremo de API de REST de servicios multimedia cuenta Hola siguiendo el formato:

    https://[media_service_account_name].restv2.[data_center].media.azure.net/API 

    Se trata de punto de conexión de hello en qué todas las API de REST de servicios multimedia se realizan llamadas de la aplicación. Por ejemplo, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

A continuación, puede colocar estos cinco parámetros en el archivo web.config o app.config, toouse en el código.

## <a name="sample-code"></a>Código de ejemplo

Puede encontrar código de ejemplo de Hola en [autenticación de Azure AD para el acceso de servicios multimedia de Azure: tanto a través de la API de REST](https://github.com/willzhan/WAMSRESTSoln).

código de ejemplo de Hola tiene dos partes:

*   Un proyecto de biblioteca DLL que tiene todo el código Hola API de REST para autenticación de Azure AD y la autorización. También tiene un método para hacer que el extremo de API de REST de servicios multimedia de API de REST llamadas toohello, con el token de acceso de Hola.
*   Un cliente de prueba de consola, que inicia la autenticación de Azure AD y llama a distintas API de REST de Media Services.

proyecto de ejemplo de Hola tiene tres características:

*   Autenticaciones de Azure AD a través de las credenciales del cliente hello conceder mediante Hola solo API de REST.
*   Acceso a los servicios multimedia Azure mediante Hola solo API de REST.
*   Acceso de almacenamiento de Azure mediante el uso de Hola solo API de REST (como toocreate usa una cuenta de servicios multimedia, mediante el uso de API de REST).


## <a name="where-is-hello-refresh-token"></a>¿Dónde está el token de actualización de hello?

¿Algunos de los lectores que se pregunte: donde es el token de actualización de hello? ¿Por qué no usar aquí un token de actualización?

propósito de Hola de un token de actualización no es toorefresh un token de acceso. En su lugar, está diseñada toobypass intervención del usuario o la autenticación del usuario final y sigue recibiendo un token de acceso válido cuando caduca un token anterior. Un nombre más adecuado para un token de actualización sería algo como "token de omisión de reinicio de sesión de usuario".

Si usas Hola flujo (nombre de usuario y una contraseña, que actúa en nombre del usuario) de la concesión de autorización de OAuth 2.0, un token de actualización le ayuda a obtener un acceso renovado token sin solicitar la intervención del usuario. Sin embargo, para hello flujo que se describe en este artículo de concesión de credenciales de cliente de OAuth 2.0, cliente hello actúa en su propio nombre. No necesita la intervención del usuario en absoluto, y servidor de autorización de hello no necesita demasiado (y no) proporcionan un token de actualización. Si depura hello **GetUrlEncodedJWT** método, observe que la respuesta de Hola de extremo de token de hello tiene un token de acceso, pero ningún token de actualización.

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-dotnet-upload-files.md).
