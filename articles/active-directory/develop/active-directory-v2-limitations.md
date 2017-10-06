---
title: aaaAzure Active Directory v2.0 extremo limitaciones y restricciones | Documentos de Microsoft
description: "Una lista de limitaciones y restricciones para el punto de conexión de hello Azure AD v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>¿Debe usar el punto de conexión de hello v2.0?
Al compilar aplicaciones que se integran con Azure Active Directory, debe toodecide si protocolos de punto de conexión y autenticación v2.0 Hola satisfacen sus necesidades. El punto de conexión original de Azure Active Directory sigue siendo totalmente compatible y, en algunos aspectos, ofrece más características que el v2.0. Sin embargo, Hola extremo v2.0 [presenta ventajas significativas](active-directory-v2-compare.md) para desarrolladores.

Esta es nuestra recomendación simplificada para desarrolladores en este momento:

* Si debe utilizar cuentas personales de Microsoft en la aplicación, utilice el punto de conexión de hello v2.0. Pero antes de que lo hace, asegúrese de que comprende las limitaciones de Hola que analizamos en este artículo.
* Si la aplicación solo necesita toosupport trabajo de Microsoft y escolares, no use el punto de conexión de hello v2.0. En su lugar, consulte tooour [Guía del desarrollador de Azure AD](active-directory-developers-guide.md).

Con el tiempo, el punto de conexión de hello v2.0 crecerá restricciones de hello tooeliminate enumeradas aquí, por lo que siempre tendrá que el punto de conexión de toouse Hola v2.0. Hola mientras tanto, este artículo es toohelp previsto es determinar si el punto de conexión de hello v2.0 adecuado para usted. Seguiremos tooupdate este estado actual de artículo tooreflect Hola de punto de conexión de hello v2.0. Vuelva a tooreevaluate sus requisitos comparándola con las funciones de la versión 2.0.

Si tiene una aplicación de Azure AD existente que no usa el punto de conexión de hello v2.0, no hay ningún toostart necesario desde el principio. Hola futuras, se proporcionará una forma para toouse las aplicaciones de Azure AD existentes con el punto de conexión de hello v2.0.

## <a name="restrictions-on-app-types"></a>Restricciones en los tipos de aplicación
Actualmente, hello siguientes tipos de aplicaciones no se admiten por el punto de conexión de hello v2.0. Para obtener una descripción de tipos de aplicaciones compatibles, consulte [tipos de aplicación para el punto de conexión de hello Azure Active Directory v2.0](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>API web independiente
Puede utilizar el punto de conexión de hello v2.0 demasiado[crear una API Web que está protegido con OAuth 2.0](active-directory-v2-flows.md#web-apis). Sin embargo, esa API Web puede recibir tokens solo desde una aplicación que ha Hola el mismo identificador de aplicación. No se puede obtener una API web desde un cliente con un identificador de aplicación distinto. cliente de Hello no ser capaz de toorequest u obtenga permisos tooyour API Web.

Hola a toosee toobuild una API Web que acepta los tokens de un cliente que tiene Hola mismo identificador de aplicación, vea ejemplos de API Web de punto de conexión de v2.0 en nuestro [Introducción](active-directory-appmodel-v2-overview.md#getting-started) sección.

## <a name="restrictions-on-app-registrations"></a>Restricciones en los registros de aplicaciones
Actualmente, para cada aplicación que desea que se toointegrate con el punto de conexión de hello v2.0, debe crear un registro de una aplicación Hola nueva [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). AD de Azure existente o aplicaciones de la cuenta de Microsoft no son compatibles con el punto de conexión de hello v2.0. Las aplicaciones que están registradas en cualquier portal distinto de hello Portal de registro de aplicación no son compatibles con el punto de conexión de hello v2.0. Hola futura, tenemos previsto tooprovide un toouse de manera una aplicación existente como una aplicación de la versión 2.0. Sin embargo, actualmente, hay ninguna ruta de acceso de migración para una toowork de aplicación existente con el punto de conexión de hello v2.0.

Asimismo, los registros de aplicación que se crean en hello [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tienen Hola después advertencias:

* Solo se permiten dos secretos de aplicación por cada identificador de aplicación.
* Un registro de aplicaciones realizado por un usuario con una cuenta personal de Microsoft solo se puede ver y administrar mediante una sola cuenta de desarrollador. No se puede compartir entre varios desarrolladores.  Si desea que tooshare el registro de una aplicación entre varios desarrolladores de software, puede crear la aplicación hello al iniciar sesión en el portal de registro de hello con una cuenta de Azure AD.
* Hay varias restricciones en formato de Hola de redirección de hello URI que se permite. Para obtener más información acerca de los URI de redirección, vea Hola siguiente sección.

## <a name="restrictions-on-redirect-uris"></a>Restricciones en los URI de redireccionamiento
Actualmente, las aplicaciones que están registradas en el Portal de registro de aplicación Hola son conjunto restringido tooa limitado de valores URI de redireccionamiento. Hola redirección URI de las aplicaciones web y servicios debe empezar con el esquema de hello `https`, y todos los valores URI de redireccionamiento deben compartir un único dominio DNS. Por ejemplo, no puede registrar una aplicación web con uno de estos URI de redirección:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

sistema de registro de Hello compara Hola de nombre DNS completo de hello existente redirección URI toohello nombre DNS de redirección de hello URI que se va a agregar. nombre DNS de Hello solicitud tooadd Hola se producirá un error si se cumple alguna de hello condiciones siguientes:  

* Hola todo DNS nombre de URI de redireccionamiento nueva hello no coincidir con hello DNS de URI de redireccionamiento existente Hola.
* Hola todo nombre DNS de hello nueva el URI de redireccionamiento no es un subdominio del URI de redireccionamiento existente Hola.

Por ejemplo, si la aplicación hello tiene este URI de redireccionamiento:

`https://login.contoso.com`

Puede agregar tooit, similar al siguiente:

`https://login.contoso.com/new`

En este caso, el nombre DNS de hello coincide exactamente. O bien, puede hacer lo siguiente:

`https://new.login.contoso.com`

En este caso, está haciendo referencia subdominio DNS de tooa de login.contoso.com. Si desea que una aplicación con inicio de sesión east.contoso.com y west.contoso.com-inicio de sesión como URI de redireccionamiento toohave, debe agregar que los URI de redireccionamiento en este orden:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Puede agregar Hola último dos porque son subdominios de hello primero URI de redireccionamiento, contoso.com. Esta limitación se eliminará en una próxima versión.

toolearn tooregister una aplicación Hola Portal de registro de aplicación, vea [cómo una aplicación con el punto de conexión de hello v2.0 tooregister](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Restricciones en los servicios y API
Actualmente, el punto de conexión de hello v2.0 admite inicio de sesión para cualquier aplicación que se registra en el Portal de registro de la aplicación hello y que se encuentra en la lista de Hola de [admite flujos de autenticación](active-directory-v2-flows.md). Sin embargo, estas aplicaciones pueden adquirir tokens de acceso OAuth 2.0 para un conjunto de recursos muy limitado. problemas de punto de conexión de Hello v2.0 acceso solo para:

* aplicación Hello que solicitó el token de Hola. Una aplicación puede adquirir un token de acceso para sí mismo, si la aplicación lógica de hello se compone de varios componentes diferentes o capas. toosee este escenario en acción, visite nuestro [Introducción](active-directory-appmodel-v2-overview.md#getting-started) tutoriales.
* Hola correo electrónico de Outlook, calendario y las API de REST de contactos, todos ellos se encuentran en https://outlook.office.com. toolearn toowrite una aplicación que tiene acceso a estas API, vea hello [Office Introducción](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) tutoriales.
* Las API de Microsoft Graph. Puede obtener más información acerca de [Microsoft Graph](https://graph.microsoft.io) y datos hello tooyou disponible.

No hay otros servicios compatibles en este momento. Más Microsoft Online Services se agregará en el futuro, hello además toosupport para sus propios servicios y API Web personalizadas.

## <a name="restrictions-on-libraries-and-sdks"></a>Restricciones en las bibliotecas y SDK
Actualmente, la compatibilidad con bibliotecas para el punto de conexión de hello v2.0 está limitado. Si desea que el punto de conexión de toouse Hola v2.0 en una aplicación de producción, tienes estas opciones:

* Si está creando una aplicación web, puede utilizar sin ningún riesgo tooperform de middleware de servidor disponible con carácter general de inicio de sesión y el token de validación de Microsoft. Incluyen middleware de OWIN abrir identificador conectarse Hola para hello Node.js Passport complemento y ASP.NET. Para ejemplos de código que usan el software intermedio de Microsoft, consulte nuestra sección de [introducción](active-directory-appmodel-v2-overview.md#getting-started).
* Si crea una aplicación de escritorio o para dispositivos móviles, puede usar una de las bibliotecas de autenticación de Microsoft (MSAL) de versión preliminar.  Estas bibliotecas están en una vista previa admite de producción, por lo que es seguro para la ejecución toouse ellas en las aplicaciones de producción. Puede obtener más información acerca de los términos de Hola de hello obtener una vista previa y Hola bibliotecas disponibles en nuestro [referencia de bibliotecas de autenticación](active-directory-v2-libraries.md).
* Para las plataformas no cubiertas por las bibliotecas de Microsoft, puede integrar con el punto de conexión de hello v2.0 directamente enviando y recibiendo mensajes de protocolo en el código de aplicación. Hola v2.0 OpenID Connect y OAuth protocolos [documentados explícitamente](active-directory-v2-protocols.md) toohelp realizar una integración de este tipo.
* Por último, puede usar código abierto abrir Id. de conexión y toointegrate de bibliotecas de OAuth con el punto de conexión de hello v2.0. Protocolo de Hello v2.0 debe ser compatible con muchas bibliotecas de código abierto protocolo sin cambios más importantes. disponibilidad de Hola de estos tipos de bibliotecas varía según el idioma y plataforma. Hola [conectarse de identificador abierto](http://openid.net/connect/) y [OAuth 2.0](http://oauth.net/2/) sitios Web mantener una lista de implementaciones conocidas. Para obtener más información, consulte [bibliotecas v2.0 y autenticación de Azure Active Directory](active-directory-v2-libraries.md)y lista de Hola de ejemplos que se han probado con el punto de conexión de hello v2.0 y bibliotecas de cliente de código abierto.

## <a name="restrictions-on-protocols"></a>Restricciones en los protocolos
el punto de conexión de Hello v2.0 no es compatible con SAML o WS-Federation; solo es compatible con OAuth 2.0 y conectarse de identificador abierto.  No todas las características y capacidades de los protocolos OAuth se han incorporado en el punto de conexión de hello v2.0. Estas capacidades y características del protocolo actualmente son *no está disponible* en el punto de conexión de hello v2.0:

* Los tokens de identificador que se emiten por el punto de conexión de hello v2.0 no contienen un `email` de notificación para el usuario de hello, incluso si adquiere permiso de hello usuario tooview correo electrónico.
* punto de conexión de información de usuario de OpenID conectarse Hello no está implementada en el punto de conexión de hello v2.0. Sin embargo, todos los datos de perfil de usuario que recibiría potencialmente en este extremo está disponible desde Microsoft Graph hello `/me` punto de conexión.
* extremo de v2.0 Hello no admite notificaciones de rol o grupo emisoras en tokens de identificador.
* Hola [concesión de credenciales de la contraseña de propietario de OAuth 2.0 recursos](https://tools.ietf.org/html/rfc6749#section-4.3) no es compatible con el punto de conexión de hello v2.0.

Además, el punto de conexión de hello v2.0 no admite ninguna forma de hello SAML o protocolos WS-Federation.

toobetter comprender el ámbito de Hola de funcionalidad de protocolo que se admite en el punto de conexión de hello v2.0, lea nuestra [referencia del protocolo OAuth 2.0 y OpenID Connect](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Restricciones de las cuentas profesionales y educativas
Si ha usado la biblioteca de autenticación de Active Directory (ADAL) en aplicaciones de Windows, se podrían haber aprovechado de autenticación integrada de Windows que usa permisos de aserción de lenguaje de marcado de aserción de seguridad (SAML) de Hola. Con esta concesión, los usuarios de los inquilinos de Azure AD federado pueden autenticarse de manera silenciosa con su instancia local de Active Directory sin escribir las credenciales. Actualmente, no se admiten permisos de aserción de SAML de hello en el punto de conexión de hello v2.0.
