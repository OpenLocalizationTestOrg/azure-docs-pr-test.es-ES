---
title: "aaaAzure Active Directory v2.0 ámbitos, los permisos y consentimiento | Documentos de Microsoft"
description: "Una descripción de la autorización en el punto de conexión de v2.0 de hello Azure AD, incluidos los ámbitos, los permisos y consentimiento."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Ámbitos, permisos y consentimiento en el punto de conexión de hello Azure Active Directory v2.0
Las aplicaciones que se integran con Azure Active Directory (Azure AD) siguen un modelo de autorización que ofrece a los usuarios control sobre el modo en que una aplicación puede acceder a sus datos. se ha actualizado la implementación de Hello v2.0 de modelo de autorización de hello, y se cambia cómo una aplicación debe interactuar con Azure AD. Este artículo tratan los conceptos básicos de este modelo de autorización, incluidos los ámbitos, los permisos y consentimiento Hola.

> [!NOTE]
> el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory. toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Permisos y ámbitos
Azure AD implementa hello [OAuth 2.0](active-directory-v2-protocols.md) protocolo de autorización. OAuth 2.0 es un método a través del cual una aplicación de terceros puede acceder a recursos hospedados en Web en nombre de un usuario. Cualquier recurso hospedado en Web que se integre con Azure AD tiene un identificador de recursos o *URI de id. de aplicación*. Por ejemplo, algunos de los recursos de Microsoft hospedados en la web incluyen:

* Hola API de correo electrónico unificado de Office 365:`https://outlook.office.com`
* Hola API de Azure AD Graph:`https://graph.windows.net`
* Microsoft Graph: `https://graph.microsoft.com`

Hola que mismo puede decirse de los recursos de terceros que se han integrado con Azure AD. Cualquiera de estos recursos también puede definir un conjunto de permisos que pueden ser utilizados toodivide Hola funcionalidad de ese recurso en fragmentos menores. Por ejemplo, [Microsoft Graph](https://graph.microsoft.io) definió Hola de toodo permisos después de tareas, entre otros:

* Leer el calendario de un usuario
* Calendario del usuario de escritura tooa
* Enviar correo como un usuario

Mediante la definición de estos tipos de permisos, el recurso de hello tiene control específico sobre sus datos y cómo se exponen los datos de Hola. Una aplicación de terceros puede solicitar estos permisos a un usuario de la aplicación. usuario de aplicación Hola debe aprobar permisos Hola para que aplicación hello puede actuar en nombre de usuario de Hola. Por fragmentación funcionalidad del recurso de hello en conjuntos de permisos más pequeños, aplicaciones de terceros pueden ser toorequest integrado solo Hola específicos los permisos que necesitan tooperform su función. Los usuarios de la aplicación pueden sabe exactamente cómo una aplicación va a utilizar sus datos y pueden ser más seguros de que la aplicación hello no se comporta con malas intenciones.

En Azure AD y OAuth, estos tipos de permisos se denominan *ámbitos*. A veces también son tooas que se hace referencia *oAuth2Permissions*. Un ámbito se representa en Azure AD como un valor de cadena. Continuando con el ejemplo de Hola a Microsoft Graph, valor de ámbito de Hola para cada permiso es:

* Leer el calendario de un usuario mediante `Calendar.Read`
* Escribir calendario del usuario tooa mediante`Mail.ReadWrite`
* Enviar correo electrónico con un usuario mediante `Mail.Send`

Una aplicación puede solicitar estos permisos mediante la especificación de ámbitos de hello en el punto de conexión de solicitudes toohello v2.0.

## <a name="openid-connect-scopes"></a>Ámbitos de OpenID Connect
implementación de la versión 2.0 de Hola de OpenID Connect tiene unos ámbitos bien definidos que no son aplicables a recursos específicos de tooa: `openid`, `email`, `profile`, y `offline_access`.

### <a name="openid"></a>openid
Si una aplicación realiza inicio de sesión mediante el uso de [OpenID Connect](active-directory-v2-protocols.md), debe solicitar hello `openid` ámbito. Hola `openid` ámbito se muestra en la cuenta de trabajo de hello página de consentimiento Hola permiso "Iniciar sesión en" y en la cuenta de Microsoft personal Hola página de consentimiento como Hola permiso "Ver su perfil y conectar tooapps y los servicios con su cuenta de Microsoft". Con este permiso, una aplicación puede recibir un identificador único para el usuario de hello en forma de Hola de hello `sub` de notificación. También proporciona el punto de conexión de hello aplicación acceso toohello información de usuario. Hola `openid` ámbito puede usarse en hello v2.0 extremo de token tooacquire identificador tokens, que pueden ser utilizados toosecure HTTP llamadas entre distintos componentes de una aplicación.

### <a name="email"></a>email
Hola `email` ámbito puede usarse con hello `openid` ámbito y cualquier otra. Proporciona la dirección de correo electrónico principal del usuario de hello aplicación acceso toohello en forma Hola Hola `email` de notificación. Hola `email` notificación se incluye en un token solo si una dirección de correo electrónico está asociada a la cuenta de usuario de hello, que no siempre es el caso de hello. Si utiliza hello `email` ámbito, la aplicación debe ser preparado toohandle un caso en que hello `email` notificación no existe en el símbolo (token) de Hola.

### <a name="profile"></a>Perfil
Hola `profile` ámbito puede usarse con hello `openid` ámbito y cualquier otra. Proporciona Hola aplicación acceso tooa considerable cantidad de información acerca del usuario de Hola. incluye información de Hola que pueda tener acceso, pero no está limitado para Hola nombre dado del usuario, apellido, nombre de usuario preferido e identificador de objeto Para obtener una lista completa de hello perfil notificaciones disponibles en el parámetro de hello id_tokens para un usuario específico, vea hello [v2.0 tokens referencia](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Hola [ `offline_access` ámbito](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) da su tooresources de acceso de la aplicación en nombre de usuario de Hola durante un período prolongado. En la página de consentimiento de cuenta de trabajo hello, este ámbito aparece como "Obtener acceso a los datos en cualquier momento" permiso de Hola. En hello personal consentimiento página la cuenta Microsoft, aparece como "Obtener acceso a la información en cualquier momento" permiso de Hola. Cuando un usuario aprueba hello `offline_access` ámbito, la aplicación puede recibir tokens de actualización de extremo de token de hello v2.0. Los tokens de actualización tienen una duración larga. La aplicación puede obtener nuevos tokens de acceso cuando expiren los antiguos.

Si la aplicación no solicita hello `offline_access` ámbito, que no recibir tokens de actualización. Esto significa que cuando canjear un código de autorización en hello [flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols.md), recibirá solo un token de acceso de hello `/token` punto de conexión. token de acceso de Hello es válida durante un breve período. token de acceso de Hello normalmente expira en una hora. En ese momento, la aplicación necesita tooredirect Hola usuario espera toohello `/authorize` tooget un nuevo código de autorización de punto de conexión. Durante esta redirección, según el tipo de saludo de aplicación, usuario Hola podría necesitará tooenter sus credenciales de nuevo o nuevo consentimiento toopermissions.

Para obtener más información acerca de cómo tooget y use tokens de actualización, vea hello [referencia del protocolo v2.0](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Solicitud de consentimiento de usuario individual
En un [OpenID Connect o OAuth 2.0](active-directory-v2-protocols.md) solicitar autorización, una aplicación puede solicitar permisos de Hola que necesita mediante el uso de hello `scope` parámetro de consulta. Por ejemplo, cuando un usuario inicia sesión en la aplicación tooan, aplicación hello envía una solicitud como Hola siguiente ejemplo (con saltos de línea agregados por legibilidad):

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Hola `scope` parámetro es una lista separada por espacios de ámbitos que Hola aplicación está solicitando. Cada ámbito se indica mediante la anexión de identificador del recurso de hello ámbito valor toohello (Hola URI de Id. de la aplicación). En el ejemplo de solicitud de hello, aplicación hello necesita calendario del usuario de permiso tooread hello y enviar correo electrónico como usuario de Hola.

Después de hello usuario escribe sus credenciales, el punto de conexión de hello v2.0 busca un registro coincidente de *consentimiento del usuario*. Si no ha dado su consentimiento del usuario de hello tooany de hello permisos solicitados en hello anterior, el punto de conexión de hello v2.0 pide toogrant de usuario de Hola Hola permisos solicitados.

![Consentimiento de la cuenta de trabajo](../../media/active-directory-v2-flows/work_account_consent.png)

Cuando el usuario de hello aprueba permiso hello, consentimiento Hola se registra para que hello el usuario no tiene tooconsent nuevo en inicios de sesión de cuentas subsiguientes.

## <a name="requesting-consent-for-an-entire-tenant"></a>Solicitud de consentimiento para un inquilino al completo
A menudo, cuando una organización adquiere una licencia o una suscripción para una aplicación, la organización de hello quiere toofully aplicación de hello aprovisionar para sus empleados. Como parte de este proceso, un administrador puede conceder consentimiento para tooact de aplicación hello en nombre de cualquier empleado. Si Hola, administrador concede el consentimiento para el inquilino todo hello, los empleados de la organización de hello no verán una página de consentimiento para la aplicación hello.

toorequest consentimiento para todos los usuarios en un inquilino, la aplicación puede utilizar el extremo de consentimiento de administración de Hola.

## <a name="admin-restricted-scopes"></a>Ámbitos restringidos para los administradores
Se pueden establecer algunos permisos con privilegios elevados en el ecosistema de Microsoft hello demasiado*restringido a administradores*. Algunos ejemplos de estos tipos de ámbitos son Hola los siguientes permisos:

* Leer datos del directorio de una organización mediante `Directory.Read`
* Escribir el directorio de la organización de datos tooan mediante`Directory.ReadWrite`
* Leer grupos de seguridad del directorio de una organización mediante: `Groups.Read.All`

Aunque un usuario de consumidor puede conceder un toothis de acceso de la aplicación de tipo de datos, los usuarios de la organización están restringidos conceder toohello acceso mismo conjunto de datos confidenciales de la empresa. Si la aplicación solicita acceso tooone de estos permisos de un usuario de la organización, usuario de hello recibe un mensaje de error que indica que no son los permisos de la aplicación de tooconsent autorizados tooyour.

Si la aplicación necesita acceso restringido tooadmin ámbitos para las organizaciones, se debe solicitan directamente desde un administrador de empresa, también mediante el uso de extremo de consentimiento de administración de hello, que se describe a continuación.

Cuando un administrador le conceda que estos permisos a través de Hola, Administrador de consentimiento punto de conexión, se ha dado consentimiento para todos los usuarios de inquilinos de Hola.

## <a name="using-hello-admin-consent-endpoint"></a>Uso de extremo de consentimiento de administración de Hola
Si sigue estos pasos, la aplicación puede recopilar permisos para todos los usuarios de un inquilino, incluidos los ámbitos restringido para los administradores. toosee un ejemplo de código que implementa los pasos de hello, vea hello [ejemplo restringido por el Administrador de ámbitos](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Solicitar permisos de hello en el portal de registro de aplicación Hola
1. Vaya tooyour aplicación Hola [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o [crear una aplicación](active-directory-v2-app-registration.md) si no lo ha hecho ya.
2. Busque hello **Microsoft Graph permisos** sección y, a continuación, agregue permisos de Hola que requiere la aplicación.
3. Asegúrese de que **guardar** Hola de registro de la aplicación.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Recomendado: Usuario de inicio de sesión hello en tooyour aplicación
Normalmente, cuando se compila una aplicación que utiliza el punto de conexión de consentimiento de administración de hello, aplicación hello necesita una página o una vista en qué Hola administrador puede aprobar los permisos de la aplicación hello. Esta página puede formar parte del flujo de registro de la aplicación hello, parte de la configuración de la aplicación hello, o bien puede ser dedicado "conectar" flujo. En muchos casos, tiene sentido para hello aplicación tooshow esto "conectar" vista sólo después de que un usuario haya iniciado sesión con un trabajo o escuela cuenta Microsoft.

Al iniciar la sesión de usuario de hello en tooyour aplicación, puede identificar la organización de hello toowhich Hola, Administrador pertenece antes de que se les solicita permisos necesarios de tooapprove Hola. Aunque no es estrictamente necesario, puede ayudarle a crear una experiencia más intuitiva para los usuarios de la organización. usuario de hello toosign en siguen nuestro [tutoriales de protocolo v2.0](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Hola solicitar los permisos de un administrador de directorio
Cuando esté listo toorequest permisos de administrador de su organización, puede redirigir Hola usuario toohello v2.0 *extremo de consentimiento de administración*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parámetro | Condición | Descripción |
| --- | --- | --- |
| tenant |Obligatorio |inquilino de directorio de Hola que desee toorequest permiso de. Se puede proporcionar en formato de nombre descriptivo o GUID. |
| client_id |Obligatorio |Hola aplicación Id. que hello [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) asignado tooyour aplicación. |
| redirect_uri |Obligatorio |Hola redirigir URI donde desee hello toobe de respuesta enviado para su toohandle de aplicación. Debe coincidir exactamente con uno de redirección de hello URI que se ha registrado en el portal de registro de aplicación Hola. |
| state |Recomendado |Un valor incluido en la solicitud de Hola que también se devolverán en respuesta de token de Hola. Puede ser una cadena de cualquier contenido que desee. Utilice tooencode información de estado de hello acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o vista que estaban en. |

En este momento, Azure AD necesita un toosign del Administrador de inquilinos en solicitud de hello toocomplete. Administrador de Hola se solicita tooapprove que todos Hola permisos que han solicitado para la aplicación de portal de registro de aplicación Hola.

#### <a name="successful-response"></a>Respuesta correcta
Si Hola, administrador aprueba permisos hello para la aplicación, la respuesta es correcta Hola se ve así:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parámetro | Description |
| --- | --- | --- |
| tenant |inquilino de directorio de Hola que conceden los permisos de aplicación Hola solicita, en formato GUID. |
| state |Un valor incluido en la solicitud de Hola que también se devolverá como respuesta de token de Hola. Puede ser una cadena de cualquier contenido que desee. estado de Hello es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| admin_consent |Se establece demasiado**true**. |

#### <a name="error-response"></a>Respuesta de error
Si Hola, administrador no puede aprobar los permisos de hello para la aplicación, Hola error respuesta es similar al siguiente:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parámetro | Description |
| --- | --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error. |

Una vez que ha recibido una respuesta correcta desde el punto de conexión de hello administrador consentimiento, la aplicación ha obtenido permisos de Hola que solicita. A continuación, puede solicitar un token de recurso de Hola que desee.

## <a name="using-permissions"></a>Uso de permisos
Después de consentimiento del usuario de hello toopermissions para la aplicación, la aplicación puede adquirir tokens de acceso que representan tooaccess de permiso de la aplicación un recurso cierta capacidad. Un token de acceso puede utilizarse solo para un único recurso, pero se codifica dentro del token de acceso de hello es cada permiso que se ha concedido a la aplicación para ese recurso. tooacquire un token de acceso, la aplicación puede realizar un solicitud toohello v2.0 extremo de token, similar al siguiente:

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

Puede usar el token de acceso resultante de hello en recursos de toohello de las solicitudes HTTP. Forma confiable indica recursos toohello que tu aplicación tiene Hola el permiso adecuado tooperform una tarea específica.  

Para obtener más información acerca de hello OAuth 2.0 del protocolo y tokens de acceso de tooget, vea hello [referencia del protocolo de extremo v2.0](active-directory-v2-protocols.md).
