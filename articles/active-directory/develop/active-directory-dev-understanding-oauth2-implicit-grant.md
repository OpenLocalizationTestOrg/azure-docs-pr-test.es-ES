---
title: "flujo de concesión de hello aaaUnderstanding OAuth2 implícita en Azure AD | Documentos de Microsoft"
description: "Obtener más información sobre la implementación de Active Directory de Azure de flujo de concesión implícita OAuth2 hello, y si es adecuado para su aplicación."
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Hola descripción OAuth2 implícita conceder flujo en Azure Active Directory (AD)
concesión implícita OAuth2 Hello es famoso por la que se va a conceder Hola con la lista más larga de Hola de cuestiones de seguridad en la especificación de OAuth2 de Hola. Además, que es enfoque Hola implementada por AAL JS y Hola uno que se recomienda al escribir aplicaciones de SPA. ¿Qué ventajas aporta? Se trata todos los de contrapartidas entre: y resulta, concesión implícita de hello es recomendable hello, que puede seguir para las aplicaciones que consumen una API Web a través de JavaScript desde un explorador.

## <a name="what-is-hello-oauth2-implicit-grant"></a>¿Qué es la concesión implícita OAuth2 Hola?
Hola típico [concesión de código de autorización de OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.1) es la concesión de autorización de Hola que utiliza dos puntos de conexión independientes. extremo de autorización de Hola se usa para la fase de interacción de usuario de hello, que da como resultado un código de autorización. extremo de token de Hello, a continuación, se usa por cliente hello para intercambiar el código de hello para un token de acceso y a menudo también un token de actualización. Las aplicaciones Web es toopresent requiere su propia aplicación credenciales toohello extremo de token, de modo que hello servidor de autorización puede autenticar Hola cliente.

Hola [concesión implícita OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.2) es una variante de otros concede autorización. Permite a un cliente tooobtain un token de acceso (y id_token, al usar [OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) directamente desde el extremo de autorización de hello, sin ponerse en contacto con el extremo de token de hello ni autenticar el cliente de Hola. Esta variante se diseñó específicamente para aplicaciones que se ejecutan en un explorador Web basado en JavaScript: en la especificación OAuth2 Hola original, símbolos (tokens) se devuelve en un fragmento URI. Hace que bits token hello toohello disponible código de JavaScript de cliente hello, pero garantiza que no se incluirán en redirecciones hacia el servidor de Hola. Devolver tokens a través de explorador redirige directamente desde el extremo de autorización de Hola. También tiene la ventaja Hola de eliminación de todos los requisitos de entre las llamadas de origen, que son necesarios si Hola aplicación de JavaScript es el punto de conexión de token de hello toocontact necesarios.

Una característica importante de concesión implícita OAuth2 hello es hechos Hola que tales flujos no devuelven nunca actualización tokens toohello cliente. Como se verá en la siguiente sección de hello, que no es realmente necesario y de hecho sería un problema de seguridad.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Conceder escenarios adecuados para hello OAuth2 implícita
Tal y como se declara en la propia especificación de OAuth2 hello, hello concesión implícita ha sido ideada tooenable usuario-agente aplicaciones: es decir, toosay, aplicaciones de JavaScript que se ejecutan dentro de un explorador. Hola definición de característica de estas aplicaciones es que el código de JavaScript se utiliza para tener acceso a recursos del servidor (normalmente una API Web) y para actualizar la aplicación hello UX en consecuencia. Piense en aplicaciones como Gmail o Outlook Web Access: cuando se selecciona un mensaje de la Bandeja de entrada, sólo mensajes de bienvenida del panel de visualización cambia toodisplay Hola nueva selección, al resto de Hola de página de hello permanecen sin cambios. Esto es en contraste con tradicional basada en redirección las aplicaciones Web, donde cada interacción del usuario produce un postback de página completa y una representación de página completa de la respuesta del servidor nuevo Hola.

Las aplicaciones que toman Hola basada en JavaScript enfoque tooits extreme se denominan aplicaciones de una única página o SPAs: Hola idea es siempre que esas aplicaciones solo servir una página inicial de HTML y JavaScript asociado, con todas las interacciones subsiguientes se controla mediante Llamadas a API Web se realizan a través de JavaScript. Sin embargo, los enfoques híbrida, donde aplicación hello es principalmente controlada por la devolución de datos, pero realiza llamadas JS ocasionales, no son habituales: discusión Hola sobre el uso de flujo implícito también es relevante para los.

Por lo general, las aplicaciones basadas en redirecciones protegen sus solicitudes a través de las cookies; sin embargo, este enfoque no funciona tan bien para aplicaciones JavaScript. Las cookies solo funcionan con dominio Hola que se han generado, mientras que las llamadas de JavaScript se podrían dirigidas a otros dominios. De hecho, que con frecuencia es el caso de hello: reflexión de invocación de API de Azure de Microsoft Graph API, API de Office: todos los que residen fuera del dominio de Hola desde donde se sirve la aplicación hello de aplicaciones. Una tendencia al alza para aplicaciones de JavaScript no es toohave ningún back-end en absoluto, 100% en 3 tooimplement de las API Web de entidad de confianza de su función de negocio.

Actualmente, hello método preferido para proteger las llamadas tooa API Web es toouse enfoque de token de portador de hello OAuth2, donde cada llamada está acompañado por un token de acceso OAuth2. Hola API Web examina el token de acceso de Hola entrantes y, si encuentra en lo hello ámbitos necesarios, concede acceso toohello la operación solicitada. flujo implícito Hola proporciona un mecanismo conveniente para las aplicaciones de JavaScript tooobtain los tokens de acceso para una API Web, que ofrece que numerosas ventajas en respetan toocookies:

* Símbolos (tokens) se puede obtener de forma confiable sin necesidad de entre las llamadas de origen: registro obligatorio de toowhich URI de redireccionamiento Hola se devuelven los tokens garantiza que no se desplaza símbolos (tokens)
* Las aplicaciones JavaScript pueden obtener tantos tokens de acceso como necesiten para la cantidad de API web que tengan como destino; sin restricciones de dominios.
* Características de HTML5 como la sesión o almacenamiento local conceder control total sobre el almacenamiento en caché de tokens y administración de la duración, mientras que la administración de cookies es opaco toohello aplicación
* Tokens de acceso no son ataques de falsificación (CSRF) de solicitud de tooCross susceptible a sitio

flujo de concesión implícita de Hello no emite tokens de actualización, principalmente por motivos de seguridad. Los tokens de actualización no tienen tantas limitaciones como los de acceso, que conceden muchos más permisos y, por tanto, pueden producir más daños en caso de que se filtren. En flujo implícito de hello, símbolos (tokens) se entrega en la dirección URL de hello, por lo tanto, es superior en la concesión de código de autorización de Hola riesgo Hola de interceptación.

Sin embargo, tenga en cuenta que una aplicación de JavaScript tiene otro mecanismo a su disposición para renovar los tokens de acceso sin pedir varias veces las credenciales del usuario de Hola. Hello aplicación puede usar un iframe oculto tooperform nuevas solicitudes de token en el extremo de autorización de Hola de Azure AD: como explorador Hola todavía tiene una sesión activa (leer: tiene una cookie de sesión) en el dominio de hello Azure AD, Hola solicitud de autenticación puede producirse correctamente sin necesidad de interacción del usuario.

Este modelo permite Hola JavaScript aplicación Hola tooindependently renovar los tokens de acceso e incluso adquirir nuevos para una nueva API (siempre que hello usuario consentido previamente para ellos. Esto evita Hola carga añadida de adquisición, el mantenimiento y la protección de un artefacto de gran valor, como un token de actualización. artefacto de Hola que posibilita la renovación silenciosa hello, cookie de sesión de Azure AD de hello, se administra fuera de la aplicación hello. Otra ventaja de este enfoque es que un usuario puede cerrar sesión de Azure AD, mediante cualquiera de las aplicaciones de hello firmadas en Azure AD, que se ejecute en cualquiera de las pestañas del explorador de Hola. Esto da lugar a eliminación Hola de cookie de sesión de Azure AD de Hola y Hola aplicación JavaScript perderás automáticamente capacidad hello toorenew tokens para hello cerrado la sesión de usuario.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>¿Es la concesión implícita de hello adecuado para mi aplicación?
concesión implícita de Hello presenta riesgos más que otras concesiones y áreas de hello necesita toopay atención tooare bien documentada. Por ejemplo, [tooImpersonate uso indebido de Token de acceso de propietario del recurso de flujo implícito] [ OAuth2-Spec-Implicit-Misuse] y [modelo de amenazas de OAuth 2.0 y consideraciones de seguridad] [ OAuth2-Threat-Model-And-Security-Implications]). Sin embargo, el perfil de riesgo más alto de hello es en gran medida debido toohello hechos que está diseñado tooenable aplicaciones que ejecutan código activo, atendido por un explorador de tooa recurso remoto. Si está planeando una arquitectura SPA, no tiene ningún componente de back-end o previsto tooinvoke una API Web a través de JavaScript, se recomienda el uso de flujo implícitos de hello para la adquisición de tokens.

Si la aplicación es un cliente nativo, flujo implícito hello no es una buena elección. ausencia de Hola de cookie de sesión de hello Azure AD en el contexto de Hola de un cliente nativo prive su aplicación desde el medio de Hola para mantener una sesión de larga duración. Lo que significa que la aplicación le pedirá repetidamente usuario Hola al obtener los tokens de acceso para los nuevos recursos.

Si está desarrollando una aplicación Web que incluye un back-end y utilizando una API de su código de back-end, flujo implícito hello también no es una buena opción. Otras concesiones ofrecen muchas más posibilidades. Por ejemplo, concesión de credenciales de cliente hello OAuth2 proporciona tokens de tooobtain de capacidad de Hola que reflejan permisos Hola asignan toohello propia aplicación, como las delegaciones toouser opuestos. Esto significa cliente hello tiene Hola capacidad toomaintain acceso mediante programación tooresources incluso cuando un usuario no estará activamente relacionado en una sesión y así sucesivamente. No solo eso, sino que dichas concesiones ofrecen mayores garantías de seguridad. Por ejemplo, tokens de acceso de tránsito nunca a través del explorador del usuario de hello, no el riesgo de que se va a guardarse en el historial del explorador de Hola y así sucesivamente. aplicación de cliente de Hello también puede realizar una autenticación segura al solicitar un token.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una lista completa de recursos para desarrolladores, incluida la información de referencia para los protocolos de Hola y autorización de OAuth2 conceden flujos compatibilidad con Azure AD, consulte toohello [Guía del desarrollador de Azure AD][AAD-Developers-Guide]
* Vea [cómo una aplicación con Azure AD toointegrate] [ ACOM-How-To-Integrate] profundidad adicional en el proceso de integración de aplicación Hola.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
