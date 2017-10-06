---
title: "¿aaaWhat es diferente en el punto de conexión de hello Azure AD v2.0? | Microsoft Docs"
description: "Una comparación entre Hola original AD de Azure y los puntos de conexión de hello v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>¿Qué es diferente sobre el punto de conexión de hello v2.0?
Si está familiarizado con Azure Active Directory o ha integrado aplicaciones con Azure AD en hello anterior, puede haber algunas diferencias en el punto de conexión de v2.0 de Hola que no se esperaría.  Este documento describe esas diferencias para su comprensión.

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Cuentas de Microsoft y cuentas de Azure AD
el punto de conexión de Hello v2.0 permiten a los desarrolladores de aplicaciones toowrite que aceptan iniciar sesión desde cuentas de Microsoft Accounts y Azure AD, con un punto de conexión de autenticación único.  Esto deja Hola toowrite de capacidad de la aplicación completamente cuenta independiente; puede ser con omisión del tipo hello de cuenta que Hola usuario inicia sesión en.  Por supuesto, también *puede* hacer que la aplicación sea consciente de tipo hello de cuenta que se usa en una sesión determinada, pero no es necesario.

Por ejemplo, si su aplicación llama hello [Microsoft Graph](https://graph.microsoft.io), algunas funciones adicionales y los datos estarán tooenterprise disponibles a los usuarios, como sus sitios de SharePoint o datos de directorio.  Pero para muchas acciones, como [leer correo electrónico del usuario](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), se puede escribir código de hello exactamente Hola igual para las cuentas de Microsoft Accounts y Azure AD.  

La integración de su aplicación con las cuentas de Azure AD y las cuentas de Microsoft ahora es un proceso sencillo.  Puede usar un único conjunto de puntos de conexión y una única biblioteca, una única aplicación registro toogain acceso tooboth Hola consumidor y empresa mundos.  toolearn Obtenga más información sobre Hola extremo v2.0, visite [Hola información general sobre](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Nuevo portal de registro de aplicaciones
tooregister una aplicación que funciona con el punto de conexión de hello v2.0, debe usar un nuevo portal de registro de aplicación: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Esto es donde puede obtener un identificador de aplicación de portal de hello personalizar la apariencia de Hola de página de inicio de sesión de la aplicación y mucho más.  Todo lo que necesita el portal de hello tooaccess es una cuenta de Microsoft con la tecnología - cuenta personal o de trabajo o escuela.

## <a name="one-app-id-for-all-platforms"></a>Un solo identificador de aplicación para todas las plataformas
Si ha usado Azure Active Directory, es posible que haya registrado varias aplicaciones diferentes para un único proyecto.  Por ejemplo, si ha creado un sitio Web y una aplicación de iOS, había tooregister ellos por separado, con dos identificadores de aplicación diferentes. portal de registro de aplicación de Azure AD de Hola había forzada se toomake esta distinción durante el registro:

![Interfaz de usuario de registro de aplicación antigua](../../media/active-directory-v2-flows/old_app_registration.PNG)

De manera similar, si tenía un sitio web y una API web de back-end, puede que haya registrado cada uno como una aplicación independiente en Azure AD.  O bien, si tenía una aplicación de iOS y una aplicación Android, puede que también haya registrado dos aplicaciones diferentes.  Registro de cada componente de una aplicación ha provocado toosome comportamientos inesperados para los desarrolladores y a sus clientes:

* Cada componente aparece como una aplicación independiente de inquilino de Azure Active Directory Hola de cada cliente.
* Cuando un administrador de inquilinos intenta tooapply directiva para administrar el acceso a, o eliminar una aplicación, tendría toodo por cada componente de aplicación hello.
* Cuando los clientes aceptada tooan aplicación, cada componente aparecería en pantalla de consentimiento de bienvenida como una aplicación distintiva.

Con el punto de conexión de hello v2.0, ahora puede registrar todos los componentes del proyecto como un registro de una única aplicación y usar un identificador de aplicación único para el proyecto completo.  Puede agregar varios tooa "plataformas" cada proyecto y proporcionar datos apropiados de Hola para cada plataforma que agrega.  Por supuesto, puede crear tantas aplicaciones como desee, en función de sus requisitos, pero para la mayoría de Hola de los casos será necesario un único Id. de aplicación.

Nuestro objetivo es que esto provocar tooa más simplificada la administración de aplicaciones y la experiencia de desarrollo y crear una vista consolidada de más de un solo proyecto podría estar trabajando en.

## <a name="scopes-not-resources"></a>Ámbitos, no recursos
En Azure Active Directory, una aplicación puede comportarse como **recurso** o como destinatario de tokens.  Un recurso puede definir una serie de **ámbitos** o **oAuth2Permissions** que entienda, lo que permite a las aplicaciones cliente toorequest recursos de toothat de tokens para un determinado conjunto de ámbitos.  Considere la posibilidad de API de Azure AD Graph Hola como un ejemplo de un recurso:

* Identificador de recursos o `AppID URI`: `https://graph.windows.net/`
* Ámbitos o `OAuth2Permissions`: `Directory.Read`, `Directory.Write`, etc.  

Todo esto es aplicable para el punto de conexión de Hola Hola v2.0.  Una aplicación todavía se puede comportar como recurso, definir ámbitos y ser identificada por un URI.  Las aplicaciones cliente todavía pueden solicitar acceso toothose ámbitos.  Sin embargo, manera de hello en el que un cliente solicita esos permisos ha cambiado.  Hola después un OAuth 2.0 autorizar tooAzure solicitud que AD podría haber tenía el siguiente aspecto:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

Hola donde **recursos** parámetro indica qué aplicación de cliente de recursos hello solicita autorización para.  Azure AD calculadas permisos Hola requeridos por la aplicación de hello en función de la configuración estática en hello Portal de Azure y tokens emitidos en consecuencia.  Ahora, hello mismo OAuth 2.0 autorizar el aspecto de solicitud:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Hola donde **ámbito** parámetro indica qué aplicación hello permisos y recursos solicite la autorización de. Hola deseado recursos sigue siendo muy presente en la solicitud de hello: simplemente esté incluido en cada uno de los valores de hello del parámetro de ámbito de Hola.  Mediante el parámetro de ámbito de Hola de esta manera permite Hola v2.0 extremo toobe más compatible con la especificación de hello OAuth 2.0 y alinea más estrechamente con common prácticas recomendadas del sector.  También permite que las aplicaciones tooperform [consentimiento incremental](#incremental-and-dynamic-consent), que se describe en la sección siguiente Hola.

## <a name="incremental-and-dynamic-consent"></a>Consentimiento incremental y dinámico
Aplicaciones habían registrado en Azure AD necesita previamente toospecify sus permisos de OAuth 2.0 necesarios en hello Portal de Azure, en el momento de creación de la aplicación:

![Interfaz de usuario de registro de permisos](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

permisos de Hola se configuraron una aplicación requiere **estáticamente**.  Aunque esto permite la configuración de tooexist de aplicación hello en Hola Portal de Azure y mantiene el código de hello nice y simple, presenta una serie de problemas para los desarrolladores:

* Una aplicación tenía tooknow todos los permisos de Hola que nunca sería necesario en el momento de creación de la aplicación.  Agregar permisos con el tiempo era un proceso difícil.
* Una aplicación tenía tooknow todos los recursos de Hola que alguna vez podría tener acceso antelación.  Era difícil toocreate aplicaciones que pueden tener acceso a un número arbitrario de recursos.
* Una aplicación tenía toorequest todos los permisos de Hola que nunca sería necesario tras Hola primer inicio de sesión de usuario.  En algunos casos Esto causaba tooa muy larga lista de permisos, que no recomienda a los usuarios finales de aprobación de acceso de la aplicación hello en el inicio de sesión inicial.

Con el punto de conexión de hello v2.0, puede especificar permisos de hello sus necesidades de aplicación **dinámicamente**, en tiempo de ejecución, durante el uso normal de la aplicación.  toodo por lo tanto, puede especificar Hola ámbitos de sus necesidades de aplicación en un momento dado en el tiempo incluyéndolos en hello `scope` parámetro de una solicitud de autorización:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Hola anterior solicita permiso para hello aplicación tooread un usuario de Azure AD datos de directorio, así como escribir datos tootheir datos de directorio.  Si Hola haya consentido permisos toothose Hola anteriores para esta aplicación en concreto, simplemente deberá especificar sus credenciales y haya iniciado sesión en la aplicación hello.  Si hello no haya consentido tooany de estos permisos, el punto de conexión de hello v2.0 pedirá a Hola usuario consentimiento toothose permisos.  toolearn más, puede leer hasta en [permisos, ámbitos y consentimiento](active-directory-v2-scopes.md).

Que permite a una aplicación toorequest permisos dinámicamente a través de hello `scope` parámetro proporciona control total sobre la experiencia del usuario.  Si lo desea, puede elegir toofrontload su consentimiento experiencia y pregunte para todos los permisos en una solicitud de autorización inicial.  O bien, si su aplicación requiere un gran número de permisos, puede elegir toogather esos permisos de usuario de hello incrementalmente, tal y como se intentaron toouse ciertas características de la aplicación con el tiempo.

## <a name="well-known-scopes"></a>Ámbitos conocidos
#### <a name="offline-access"></a>Acceso sin conexión
Aplicaciones que usan el punto de conexión de hello v2.0 pueden requerir Hola uso de un nuevo permiso conocido para las aplicaciones: hello `offline_access` ámbito.  Todas las aplicaciones necesitará toorequest este permiso si necesitan recursos tooaccess en nombre de Hola de un usuario durante un período prolongado de tiempo, incluso cuando el usuario Hola puede no estar usando activamente aplicación hello.  Hola `offline_access` ámbito aparecerá toohello usuario consentimiento cuadros de diálogo como "Obtener acceso a los datos sin conexión", debe aceptar la qué usuario Hola.  Hola solicitante `offline_access` permiso habilitará la tooreceive de aplicación web refresh_tokens de OAuth 2.0 desde el punto de conexión de hello v2.0.  Los refresh_tokens son de larga duración y se pueden intercambiar por nuevos access_tokens de OAuth 2.0 durante largos períodos de acceso.  

Si la aplicación no solicita hello `offline_access` ámbito, no recibirá refresh_tokens.  Esto significa que cuando canjear un authorization_code en el flujo de código de autorización de hello OAuth 2.0, solo recibirá volver un access_token de hello `/token` punto de conexión.  Ese token de acceso seguirá siendo válido durante un breve período de tiempo (normalmente una hora), pero finalmente caducará.  En ese momento en el tiempo, la aplicación necesitará tooredirect Hola usuario espera toohello `/authorize` tooretrieve un nuevo authorization_code de punto de conexión.  Durante esta redirección, Hola usuario puede o puede no necesita tooenter sus credenciales de nuevo o volver a dar su consentimiento toopermissions, según el tipo de Hola Hola de aplicación.

más información acerca de OAuth 2.0, refresh_tokens y access_tokens, desprotección hello toolearn [referencia del protocolo v2.0](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>OpenID, perfil y correo electrónico
Históricamente, hello más OpenID Connect de inicio de sesión flujo básico con Azure Active Directory proporciona una gran cantidad de información acerca del usuario de hello en id_token resultante Hola.  las notificaciones de Hello en un id_token pueden incluir nombre de usuario de hello, preferido de nombre de usuario, dirección de correo electrónico, Id. de objeto y mucho más.

Se está ahora restringir la información de Hola que hello `openid` ámbito, obtienen su aplicación acceso a.  ámbito de Hello 'openid' solo permitir que al usuario de aplicación toosign hello en y recibir un identificador específico de la aplicación para usuario Hola.  Si desea tooobtain información personal identificable (PII) acerca del usuario de hello en la aplicación, la aplicación necesitará toorequest permisos adicionales del usuario de Hola.  Introducimos dos nuevos ámbitos: hello `email` y `profile` ámbitos, que le permiten toodo así.

Hola `email` ámbito es muy sencillo: permite la dirección de correo electrónico principal de aplicación acceso toohello de sus usuarios a través de hello `email` en id_token Hola de notificación.  Hola `profile` Id. de objeto de ámbito, obtienen los tooall de acceso de aplicación otro información básica sobre el usuario de Hola y su nombre, el nombre de usuario preferido y así sucesivamente.

Esto le permite toocode la aplicación de forma mínima divulgación: solo puede pedir usuario Hola para conjunto de Hola de información que la aplicación necesita toodo su trabajo.  Para obtener más información sobre estos ámbitos, consulte demasiado[Hola referencia de ámbito v2.0](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Notificaciones de token
notificaciones de Hello en tokens emitidos por el punto de conexión de hello v2.0 no serán tootokens idénticos emitidos por los puntos de conexión de hello AD de Azure disponible con carácter general: migrar toohello nuevo servicio de aplicaciones no deben suponer que una notificación determinada existirá en id_tokens o access_tokens. toolearn sobre notificaciones específicas de hello emitidos en los tokens de v2.0, consulte hello [referencia del token v2.0](active-directory-v2-tokens.md).

## <a name="limitations"></a>Limitaciones
Hay unos toobe de restricciones tenga en cuenta cuando se usa Hola v2.0 punto.  Consulte toohello [doc de limitaciones v2.0](active-directory-v2-limitations.md) toosee si alguna de estas restricciones aplican tooyour escenario en particular.
