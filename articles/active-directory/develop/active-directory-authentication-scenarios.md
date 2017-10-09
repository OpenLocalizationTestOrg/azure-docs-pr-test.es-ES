---
title: aaaAuthentication escenarios para Azure AD | Documentos de Microsoft
description: "Información general de escenarios de autenticación más comunes de hello cinco para Azure Active Directory (AAD)"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Escenarios de autenticación para Azure AD
Azure Active Directory (Azure AD) simplifica la autenticación para los desarrolladores proporcionando identidad como un servicio, con compatibilidad para protocolos de estándar del sector como OAuth 2.0 y OpenID Connect, así como las bibliotecas de código abierto para distintas plataformas toohelp empezar a codificar rápidamente. Este documento le ayudará a comprender Hola diversos admite escenarios de Azure AD y le mostrará cómo tooget iniciado. Se divide en hello las secciones siguientes:

* [Conceptos básicos sobre autenticación en Azure AD](#basics-of-authentication-in-azure-ad)
* [Notificaciones de tokens de seguridad de Azure AD](#claims-in-azure-ad-security-tokens)
* [Conceptos básicos sobre el registro de una aplicación en Azure AD](#basics-of-registering-an-application-in-azure-ad)
* [Tipos de aplicaciones y escenarios](#application-types-and-scenarios)
  
  * [Explorador de Web tooWeb aplicación](#web-browser-to-web-application)
  * [Aplicación de una sola página (SPA)](#single-page-application-spa)
  * [TooWeb nativo de aplicación API](#native-application-to-web-api)
  * [TooWeb de aplicación Web API](#web-application-to-web-api)
  * [TooWeb demonio o una aplicación de servidor de API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Conceptos básicos sobre autenticación en Azure AD
Si no está familiarizado con los conceptos básicos de la autenticación en Azure AD, lea esta sección. En caso contrario, puede que desee tooskip hacia abajo demasiado[tipos de aplicaciones y escenarios](#application-types-and-scenarios).

Veamos el escenario más básico de Hola que es necesario identificarse: un usuario en un explorador web necesita la aplicación web de tooauthenticate tooa. Este escenario se describe con más detalle en hello [tooWeb aplicación de explorador Web](#web-browser-to-web-application) sección, pero un útil iniciar punto tooillustrate Hola capacidades de Azure AD y conceptualizar el funcionamiento del escenario de Hola. Considere la posibilidad de hello siguiente diagrama para este escenario:

![Información general de la aplicación de inicio de sesión tooweb](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Con el diagrama de hello anterior en mente, aquí es lo que necesita tooknow sobre los diversos componentes:

* Azure AD es el proveedor de identidades de hello, responsable de comprobar la identidad de Hola de usuarios y aplicaciones que existen en el directorio de la organización y en última instancia emitir tokens de seguridad tras una autenticación correcta de los usuarios y aplicaciones.
* Una aplicación que desea toooutsource autenticación tooAzure AD debe registrarse en Azure AD, que registra e identifica de forma única la aplicación hello en el directorio de Hola.
* Los desarrolladores pueden usar Hola código abierto de Azure AD bibliotecas toomake autenticación fácil controlando los detalles del protocolo Hola para usted. Consulte [Bibliotecas de autenticación de Azure Active Directory](active-directory-authentication-libraries.md) para obtener más información.

• Una vez un usuario se ha autenticado, la aplicación hello debe validar tooensure de token de seguridad del usuario de Hola que la autenticación fue correcta para las partes que vayan Hola. Los desarrolladores pueden usar Hola proporcionada validación de toohandle de bibliotecas de autenticación de cualquier token de Azure AD, incluidos los Tokens de Web JSON (JWT) o SAML 2.0. Si desea tooperform validación manualmente, vea hello [controlador de Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) documentación.

> [!IMPORTANT]
> Azure AD usa criptografía de clave pública toosign tokens y verificar que son válidos. Vea [importante información sobre la firma de sustitución de clave en Azure AD](active-directory-signing-key-rollover.md) para más información sobre la lógica necesaria hello, debe tener en su aplicación tooensure siempre está actualizada con claves más recientes de Hola.
> 
> 

flujo de hello • de solicitudes y respuestas para el proceso de autenticación de hello viene determinado por el protocolo de autenticación de Hola que se usa, por ejemplo, OAuth 2.0, OpenID Connect, WS-Federation o SAML 2.0. Estos protocolos se tratan con más detalle en hello [protocolos de autenticación de Azure Active Directory](active-directory-authentication-protocols.md) tema y en secciones de hello siguientes.

> [!NOTE]
> Azure AD admite hello OAuth 2.0 y estándares de OpenID Connect que hacen un uso de tokens de portador, incluidos los tokens portadores representados como Jwt. Un token de portador es un token de seguridad ligero que concede Hola tooa de "portador" acceso al recurso protegido. En este sentido, Hola "portador" es cualquier persona que puede presentar el token de Hola. Aunque una entidad debe autenticarse primero con el token de acceso de Azure AD tooreceive hello, si es necesario de hello no se toman medidas toosecure Hola símbolo (token) de transmisión y el almacenamiento, puede interceptar y utilizado por una entidad no deseada. Mientras que algunos tokens de seguridad disponen de un mecanismo integrado para evitar ser usados por partes no autorizadas, los tokens portadores no tienen este mecanismo y deben transportarse en un canal seguro como, por ejemplo, la seguridad de la capa de transporte (HTTPS). Si se transmite un token de portador en hello claro, un ataque de intermedio de hello man en puede usarse en un token de usuario malintencionado tooacquire hello y usarlo para un recurso de tooa protegido del acceso no autorizado. Hola mismos principios de seguridad que se aplican al almacenamiento o almacenamiento en caché de tokens portadores para su uso posterior. Asegúrese siempre de que la aplicación transmite y almacena los tokens portadores de manera segura. Para otras consideraciones sobre la seguridad de los tokens portadores, consulte la [Sección 5 de RFC 6750](http://tools.ietf.org/html/rfc6750).
> 
> 

Ahora que tiene una visión general de conceptos básicos de hello, lea las secciones de hello debajo toounderstand cómo funciona el aprovisionamiento en Azure AD y es compatible con escenarios comunes de hello Azure AD.

## <a name="claims-in-azure-ad-security-tokens"></a>Notificaciones de tokens de seguridad de Azure AD
Tokens de seguridad emitidos por Azure AD contienen notificaciones o aserciones de información sobre el sujeto de Hola que se ha autenticado. Estas notificaciones se pueden utilizar por aplicación hello para varias tareas. Por ejemplo, puede ser usado toovalidate Hola token, identificar a inquilino de directorio del sujeto hello, mostrar información de usuario, determinar la autorización del firmante de Hola y así sucesivamente. Hola notificaciones presentes en cualquier token de seguridad dependen del tipo de Hola de símbolo (token), tipo de Hola de credencial que usa tooauthenticate Hola usuario y configuración de la aplicación hello. En tabla de Hola a continuación se proporciona una breve descripción de cada tipo de notificación que se genera mediante Azure AD. Para obtener más información, consulte demasiado[admite tokens y los tipos de notificación](active-directory-token-and-claims.md).

| Notificación | Description |
| --- | --- |
| Identificador de aplicación |Identifica la aplicación hello que usa el token de Hola. |
| Público |Identifica el recurso de destinatario Hola Hola token está dirigido a. |
| Referencia de clase de contexto de autenticación de aplicación |Indica cómo el cliente de Hola fue autenticado (cliente público frente a cliente confidencial). |
| Instante de autenticación |Registros Hola fecha y hora en que se realizó la autenticación de Hola. |
| Método de autenticación |Indica cómo se autenticó Hola sujeto del token de hello (contraseña, certificado, etcetera). |
| Nombre |Proporciona Hola nombre de usuario de hello como conjunto de Azure AD. |
| Grupos |Contiene grupos de identificadores de Azure AD de objeto Hola usuario es miembro de. |
| Proveedor de identidades |Registros Hola proveedor de identidades que autenticó Hola sujeto del token de Hola. |
| Emitido a las |Hora de Hola de registros a qué Hola se emitió el token, a menudo se usa para la actualización del token. |
| Emisor |Identifica el STS de Hola que emitió el token de hello, así como inquilino de Azure AD Hola. |
| Apellido |Proporciona el apellido Hola de usuario de Hola como conjunto en Azure AD. |
| Nombre |Proporciona un valor legible que identifica a Hola sujeto del token de Hola. |
| Identificador de objeto |Contiene un identificador único e inmutable del sujeto de hello en Azure AD. |
| Roles |Contiene los nombres descriptivos de los Roles de aplicación de Azure AD se ha concedido ese usuario de Hola. |
| Scope |Indica la aplicación de cliente de hello permisos concedidos toohello. |
| Asunto |Indica la entidad de seguridad de hello sobre qué Hola token valida información. |
| Identificador de inquilino |Contiene un identificador único e inmutable del inquilino de directorio de Hola que emitió el token de Hola. |
| Vigencia del token |Define el intervalo de tiempo de hello dentro del cual un token es válido. |
| Nombre principal de usuario |Contiene el nombre principal de usuario de Hola de asunto Hola. |
| Versión |Contiene el número de versión de Hola de token de Hola. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Conceptos básicos sobre el registro de una aplicación en Azure AD
Cualquier aplicación que externalice tooAzure autenticación que AD debe estar registrado en un directorio. Este paso implica informar a Azure AD acerca de la aplicación, incluida la dirección URL de Hola donde se encuentra, Hola URL toosend responde después de la autenticación, Hola URI tooidentify la aplicación y mucho más. Esta información es necesaria por algunos motivos importantes:

* Azure AD necesita coordenadas toocommunicate con la aplicación hello al administrar los tokens de inicio de sesión o de intercambio. Estos Hola siguientes:
  
  * URI del Id. de aplicación: Hola identificador de una aplicación. Este valor se envía tooAzure AD durante tooindicate autenticación qué aplicación Hola autor de la llamada quiere un token. Además, este valor se incluye en el token de Hola para que sepa de aplicación hello era Hola pensado destino.
  * Responder a dirección URL y el URI de redireccionamiento: en caso de hello de una API web o aplicación web, Hola dirección URL de respuesta es toowhich de ubicación de hello Azure AD enviará la respuesta de autenticación de hello, incluido un token si la autenticación fue correcta. En caso de hello de una aplicación nativa, Hola URI de redireccionamiento es que un toowhich de identificador único Azure AD redirigirá a Hola user-agent en una solicitud de OAuth 2.0.
  * Id. de aplicación: Hola Id. de una aplicación, que se genera cuando se registra la aplicación hello de Azure AD. Cuando se solicita un token o código de autorización, Hola Id. de aplicación y la clave se envían tooAzure AD durante la autenticación.
  * : Hola clave que se envía junto con un identificador de aplicación al autenticar tooAzure AD toocall una API web.
* Las necesidades de Azure AD tooensure Hola aplicación tiene Hola tooaccess permisos necesarios a los datos del directorio, otras aplicaciones de su organización y así sucesivamente

El aprovisionamiento se entiende mejor cuando se comprende que existen dos categorías de aplicaciones que se pueden desarrollar e integrarse con Azure AD:

* Aplicación de un solo inquilino: el uso de una aplicación de un solo inquilino se destina a una sola organización. Suele tratarse de aplicaciones de línea de negocio (LOB) escritas por un desarrollador de la empresa. Una aplicación de un solo inquilino solo necesita toobe tienen acceso los usuarios en un directorio y, como resultado, solo necesita toobe aprovisiona en un directorio. Normalmente, estas aplicaciones se registran por un desarrollador de organización de Hola.
* Aplicación multiempresa (de varios inquilinos): el uso de una aplicación multiempresa se destina a varias organizaciones, no solo a una. Suele tratarse de aplicaciones de software como servicio (SaaS) escritas por un proveedor de software independiente (ISV). Las aplicaciones de varios inquilinos necesitan toobe aprovisionado en cada directorio donde se van a utilizar, lo que requiere tooregister de consentimiento de usuario o administrador de ellos. Este proceso de consentimiento se inicia cuando una aplicación se ha registrado en el directorio de Hola y se concede acceso toohello Graph API o quizás a otra API web. Cuando un usuario o un administrador de otra organización se suscribe aplicación hello de toouse, se muestra un cuadro de diálogo que muestra los permisos de Hola Hola aplicación requiere. Hola usuario o un administrador puede consentimiento toohello aplicación, lo que se consigue toohello de acceso de aplicación Hola indica datos, y finalmente registros Hola aplicación en su directorio. Para obtener más información, consulte [información general del marco de consentimiento de hello](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Cuando se desarrolla una aplicación multiempresa en lugar de una aplicación de un solo inquilino hay que tener en cuenta otros aspectos. Por ejemplo, si está realizando la toousers disponibles de la aplicación en varios directorios, necesita un mecanismo toodetermine qué inquilino se encuentran en. Una aplicación de un solo inquilino solo necesita toolook en su propio directorio para un usuario, mientras que una aplicación de varios inquilinos debe tooidentify un usuario específico en todos los directorios de hello en Azure AD. tooaccomplish esta tarea, Azure AD proporciona un punto de conexión de autenticación común donde cualquier aplicación de varios inquilinos puede dirigir solicitudes de inicio de sesión, en lugar de un extremo específico del inquilino. Este extremo es https://login.microsoftonline.com/common para todos los directorios en Azure AD, mientras que un extremo específico del inquilino podría ser https://login.microsoftonline.com/contoso.onmicrosoft.com. punto de conexión común de Hello es especialmente importante tooconsider al desarrollar la aplicación porque necesitará Hola lógica necesaria toohandle varios inquilinos durante el inicio de sesión, cierre de sesión y validación de tokens.

Si actualmente se está desarrollando una aplicación de un solo inquilino pero desea toomake organizaciones toomany disponibles, se pueden realizar fácilmente cambios toohello aplicación y su configuración en Azure AD toomake se compatible con multiempresa. Además, Azure AD usa Hola misma clave para todos los tokens de todos los directorios de firma, si se va a proporcionar autenticación en un solo inquilino o una aplicación de varios inquilinos.

Cada uno de los escenarios incluidos en este documento incluye una subsección en donde se describen sus requisitos de aprovisionamiento. Para obtener información más detallada sobre el aprovisionamiento de una aplicación en Azure AD y hello las diferencias entre las aplicaciones únicas y de varios inquilinos, consulte [integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md) para obtener más información. Seguir leyendo toounderstand escenarios comunes de aplicación hello en Azure AD.

## <a name="application-types-and-scenarios"></a>Tipos de aplicaciones y escenarios
Cada uno de los escenarios de hello descritos en este documento puede desarrollarse con diversos lenguajes y plataformas. Que se hayan incluido en los ejemplos de código completo que están disponibles en nuestro [ejemplos de código guía](active-directory-code-samples.md), o directamente desde Hola correspondiente [repositorios de GitHub ejemplo](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). Además, si la aplicación necesita un determinado fragmento o segmento de un escenario de un extremo a otro, dicha funcionalidad se podrá agregar de manera independiente en la mayoría de los casos. Por ejemplo, si tiene una aplicación nativa que llama a una API web, puede agregar fácilmente una aplicación web que también llama hello web API. Hello siguiente diagrama muestra estos escenarios y tipos de aplicación, y cómo se pueden agregar distintos componentes:

![Tipos de aplicaciones y escenarios](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Estos son los escenarios de aplicación principal cinco Hola compatibles con Azure AD:

* [Web Browser tooWeb aplicación](#web-browser-to-web-application): un usuario necesita toosign en aplicación web de tooa que está protegida por Azure AD.
* [Única aplicación de página (SPA)](#single-page-application-spa): un usuario necesita toosign en la aplicación de una página tooa que está protegida por Azure AD.
* [Native aplicación tooWeb API](#native-application-to-web-api): una aplicación nativa que se ejecuta en un teléfono, tableta o PC necesidades tooauthenticate un tooget usuario recursos desde una API web protegida por Azure AD.
* [Web Application tooWeb API](#web-application-to-web-api): una aplicación web necesita recursos tooget desde una API web protegida por Azure AD.
* [Demonio o una aplicación de servidor tooWeb API](#daemon-or-server-application-to-web-api): una aplicación de demonio o una aplicación de servidor sin interfaz de usuario web necesita recursos tooget desde una API web protegida por Azure AD.

### <a name="web-browser-tooweb-application"></a>Explorador de Web tooWeb aplicación
Esta sección describe una aplicación que autentica a un usuario en una aplicación de web de tooa de explorador web. En este escenario, la aplicación web de hello dirige toosign de explorador del usuario de Hola en tooAzure AD. Azure AD devuelve una respuesta de inicio de sesión a través de explorador del usuario de hello, que contiene notificaciones acerca del usuario de hello en un token de seguridad. Este escenario admite inicios de sesión mediante protocolos WS-Federation, SAML 2.0 y OpenID Connect de Hola.

#### <a name="diagram"></a>Diagrama
![Flujo de autenticación para aplicación de explorador tooweb](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descripción del flujo de protocolo
1. Cuando un usuario visita la aplicación hello y necesita toosign en, se le redirige a través de un punto de conexión de autenticación de inicio de sesión de la solicitud toohello en Azure AD.
2. usuario de Hola se inicia sesión en la página de inicio de sesión de Hola.
3. Si la autenticación es correcta, Azure AD crea un token de autenticación y devuelve la dirección URL de respuesta de la aplicación de toohello de respuesta de inicio de sesión que se configuró en hello Portal de Azure. En el caso de una aplicación de producción, esta URL de respuesta debe ser HTTPS. Hola devolvió el token incluye notificaciones sobre el usuario de Hola y Azure AD requeridos por el token de hello aplicación toovalidate Hola.
4. aplicación Hello valida el token de hello mediante el uso de una clave de firma pública e información del emisor disponible en el documento de metadatos de federación de Hola para Azure AD. Después de aplicación hello valida el token de hello, Azure AD inicia una nueva sesión con el usuario de Hola. Esta sesión permite Hola usuario tooaccess aplicación hello hasta que expire.

#### <a name="code-samples"></a>Ejemplos de código
Vea los ejemplos de código de hello para escenarios de aplicación de explorador Web tooWeb. Y consultarlos con frecuencia; agregamos nuevos ejemplos todo tiempo Hola. [Web Browser tooWeb aplicación](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Registro
* Un solo inquilino: Si está generando una aplicación únicamente para la organización, se debe registrar en el directorio de su empresa mediante el uso de hello Portal de Azure.
* Multiempresa: Si está creando una aplicación que se puede usar los usuarios ajenos a su organización, debe estar registrado en el directorio de su empresa, pero también debe estar registrado en el directorio de cada organización que se va a utilizar la aplicación hello. toomake la aplicación disponible en su directorio, puede incluir un proceso de inicio de sesión para los clientes que les permite tooconsent tooyour aplicación. Cuando se registren para su aplicación, se presentará un cuadro de diálogo que muestra la aplicación Hola de hello permisos requiere y, a continuación, Hola tooconsent de opción. Dependiendo de los permisos de hello necesario, un administrador de hello otra organización puede ser necesario toogive consentimiento. Cuando el usuario de Hola o el administrador consiente, aplicación hello queda registrada en su directorio. Para obtener más información, vea [Integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiración del token
sesión del usuario de Hello expira cuando expira el período de duración de Hola de hello símbolo (token) emitido por Azure AD. Si lo desea, la aplicación puede reducir este período de tiempo; por ejemplo, cerrar sesiones de usuario en función de un período de inactividad. Cuando expira la sesión de hello, usuario de Hola será toosign solicitada de nuevo.

### <a name="single-page-application-spa"></a>Aplicación de una sola página (SPA)
Esta sección describe la autenticación para una aplicación de página única, que usa Azure AD y autorización de OAuth 2.0 implícita hello conceda toosecure finalizar su API web. Aplicaciones de una única página normalmente están estructuradas como una capa de presentación (front-end) de JavaScript que se ejecuta en un back-end Web API que se ejecuta en un servidor y el Explorador de Hola e implementa Hola lógica de negocios de la aplicación. toolearn más información sobre concesión de autorización implícita de Hola y ayudarle a decidir si es adecuado para su escenario de aplicaciones, consulte [Hola descripción OAuth2 implícita conceder flujo en Azure Active Directory](active-directory-dev-understanding-oauth2-implicit-grant.md).

En este escenario, cuando Hola usuario inicia sesión, Hola JavaScript front-end usa [biblioteca de autenticación de Active Directory para JavaScript (AAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) y autorización implícita Hola conceder tooobtain un identificador de token (id_token) de Azure AD. se almacena en caché el token de Hola y Hola cliente lo adjunta toohello solicitud como token de portador de hello cuando se realizan llamadas tooits API Web back-end, que se protege con middleware de OWIN Hola. 

#### <a name="diagram"></a>Diagrama
![Diagrama de aplicación de una sola página](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Descripción del flujo de protocolo
1. usuario Hola navega por la aplicación web de toohello.
2. aplicación Hello devuelve explorador toohello de hello JavaScript front-end (capa de presentación).
3. usuario de Hello inicia sesión, por ejemplo, haga clic en un vínculo de inicio de sesión. Explorador de Hello envía una toorequest de extremo de autorización de Azure AD de GET toohello un identificador de token. Esta solicitud incluye las URL de Id. y la respuesta de aplicación Hola hello en parámetros de consulta.
4. Azure AD valida Hola que dirección URL de respuesta contra Hola había registrado dirección URL de respuesta que se configuró en hello Portal de Azure.
5. usuario de Hola se inicia sesión en la página de inicio de sesión de Hola.
6. Si la autenticación es correcta, Azure AD crea un identificador de token y lo devuelve como dirección URL de respuesta de la aplicación toohello de fragmento (#) de dirección URL. En el caso de una aplicación de producción, esta URL de respuesta debe ser HTTPS. Hola devolvió el token incluye notificaciones sobre el usuario de Hola y Azure AD requeridos por el token de hello aplicación toovalidate Hola.
7. código de cliente de JavaScript de Hello en el Explorador de hello extrae token Hola Hola respuesta toouse para proteger las llamadas al backend de la API toohello la aplicación web.
8. Hola web de la aplicación de explorador llamadas Hola backend de la API con el token de acceso de hello en el encabezado de autorización de Hola.

#### <a name="code-samples"></a>Ejemplos de código
Vea los ejemplos de código de hello para escenarios de aplicación de página única (SPA). Ser seguro toocheck back con frecuencia; agregamos nuevos ejemplos todo tiempo Hola. [Aplicación de una sola página (SPA)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Registro
* Un solo inquilino: Si está generando una aplicación únicamente para la organización, se debe registrar en el directorio de su empresa mediante el uso de hello Portal de Azure.
* Multiempresa: Si está creando una aplicación que se puede usar los usuarios ajenos a su organización, debe estar registrado en el directorio de su empresa, pero también debe estar registrado en el directorio de cada organización que se va a utilizar la aplicación hello. toomake la aplicación disponible en su directorio, puede incluir un proceso de inicio de sesión para los clientes que les permite tooconsent tooyour aplicación. Cuando se registren para su aplicación, se presentará un cuadro de diálogo que muestra la aplicación Hola de hello permisos requiere y, a continuación, Hola tooconsent de opción. Dependiendo de los permisos de hello necesario, un administrador de hello otra organización puede ser necesario toogive consentimiento. Cuando el usuario de Hola o el administrador consiente, aplicación hello queda registrada en su directorio. Para obtener más información, vea [Integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).

Después de registrar la aplicación hello, debe estar configurado toouse protocolo de concesión implícita OAuth 2.0. De forma predeterminada, este protocolo está deshabilitado para las aplicaciones. Hola tooenable protocolo de concesión implícita OAuth2 para su aplicación, editar el manifiesto de aplicación de Portal de Azure de Hola y establecer tootrue de valor de "oauth2AllowImplicitFlow" Hola. Para obtener instrucciones detalladas, consulte [Habilitar la concesión implícita de OAuth 2.0 para aplicaciones de una sola página](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiración del token
Al utilizar la autenticación de toomanage ADAL.js con Azure AD, se beneficia de varias características que facilitan la actualización de un token caducado, así como obtener tokens de recursos de la API de web adicionales que pueden ser llamados por la aplicación hello. Cuando el usuario de Hola se autentica correctamente con Azure AD, se establece una sesión protegida por una cookie para el usuario de hello entre explorador hello y Azure AD. Es importante toonote que existe una sesión de hello entre usuarios de Hola y Azure AD y no entre el usuario de Hola y aplicación web de hello ejecutando en el servidor de Hola. Cuando caduca un token, ADAL.js usa esta sesión toosilently obtener otro token. Lo hace al utilizar un iFrame oculto toosend y recibir la solicitud de hello mediante Protocolo de concesión implícita OAuth Hola. ADAL.js también puede utilizar este mismo mecanismo toosilently obtener tokens de acceso de Azure AD para otro web recursos de la API que se registra Hola aplicación llama siempre y cuando dichos recursos admitan recursos entre orígenes (CORS), de uso compartido en el directorio del usuario de hello, y usuario de hello facilitó el consentimiento requerido durante el inicio de sesión.

### <a name="native-application-tooweb-api"></a>TooWeb nativo de aplicación API
En esta sección se describe una aplicación nativa que llama a una API web en nombre de un usuario. Este escenario se basa en el tipo de concesión de código de autorización de hello OAuth 2.0 con un cliente público, tal como se describe en la sección 4.1 de hello [especificación de OAuth 2.0](http://tools.ietf.org/html/rfc6749). aplicación nativa de Hello Obtiene un token de acceso de usuario de hello mediante Protocolo de hello OAuth 2.0. Este token de acceso, a continuación, se envía en hello solicitud toohello API web, que autoriza al usuario de Hola y devuelve el recurso de hello deseado.

#### <a name="diagram"></a>Diagrama
![Native aplicación tooWeb diagrama de API](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Flujo de autenticación para aplicación nativa tooAPI
#### <a name="description-of-protocol-flow"></a>Descripción del flujo de protocolo
Si está utilizando las bibliotecas de autenticación de hello AD, la mayoría de los detalles del protocolo Hola que se describe a continuación se administra automáticamente, como menú emergente del explorador de hello, símbolo (token) de almacenamiento en caché y control de los tokens de actualización.

1. Aplicación nativa de hello mediante una ventana emergente del explorador, hace que un extremo de autorización de solicitud toohello en Azure AD. Esta solicitud incluye hello Id. de aplicación y Hola URI de redirección de aplicación nativa de hello tal y como se muestra en hello Portal de Azure y el identificador URI de la aplicación de Hola para API web de Hola. Si el usuario de hello ya no se ha iniciado sesión, vuelven a estar toosign solicitada en
2. Azure AD autentica el usuario Hola. Si es una aplicación multiempresa y consentimiento es necesario toouse Hola aplicación, usuario de hello será necesario tooconsent si aún no lo ha hecho. Después de la concesión de consentimiento y tras una autenticación correcta, Azure AD emite URI de redireccionamiento de una autorización código respuesta toohello atrás de la aplicación cliente.
3. Cuando Azure AD envía una respuesta de código de autorización nuevo toohello URI de redireccionamiento, Hola cliente aplicación deja de explorador interacción y extrae Hola código de autorización de respuesta de Hola. Con este código de autorización, aplicación de cliente de hello envía extremo de token de un tooAzure de solicitud de AD que incluye código de autorización de hello, detalles sobre Hola aplicación de cliente (identificador de la aplicación y el URI de redireccionamiento) y Hola recurso deseado (Id. de aplicación URI de la API web de hello).
4. código de autorización de Hola y obtener información acerca de la aplicación de cliente de Hola y API web se validan en Azure AD. Tras la correcta validación, Azure AD devuelve dos tokens: un token de acceso de JWT y un token de actualización de JWT. Además, Azure AD devuelve información básica sobre el usuario de hello, como su identificador de inquilinos y el nombre de presentación.
5. A través de HTTPS, la aplicación de cliente de hello usa Hola devuelve Hola de tooadd de token de acceso JWT cadena JWT con una designación "Bearer" en encabezado de autorización de Hola de toohello web API de hello solicitud. API de web Hello, a continuación, valida el token JWT de Hola y si la validación es correcta, devuelve Hola deseado recursos.
6. Cuando expira el token de acceso de hello, aplicación de cliente de hello recibirá un error que indica el usuario de hello necesita tooauthenticate de nuevo. Si la aplicación hello tiene un token de actualización válido, puede ser usado tooacquire un nuevo token de acceso sin pedir confirmación Hola toosign de usuario de nuevo. Si expira el token de actualización de hello, será necesario aplicación hello toointeractively autenticar usuario Hola de nuevo.

> [!NOTE]
> token de actualización de Hello emitido por Azure AD puede ser usado tooaccess varios recursos. Por ejemplo, si tiene una aplicación cliente que tenga permiso toocall dos web API, token de actualización de hello puede ser usado tooget una acceso token toohello otra API web también.
> 
> 

#### <a name="code-samples"></a>Ejemplos de código
Vea los ejemplos de código de hello para escenarios de aplicación nativa tooWeb API. Y consultarlos con frecuencia; agregamos nuevos ejemplos todo tiempo Hola. [Native aplicación tooWeb API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Registro
* Un solo inquilino: Ambos Hola aplicación nativa y API web de hello debe estar registrado en hello mismo directorio en Azure AD. API de web Hola puede ser tooexpose configurado un conjunto de permisos, que son los recursos de la aplicación nativa de toolimit usado Hola acceso tooits. a continuación, la aplicación de cliente de Hello selecciona permisos Hola deseado del menú desplegable "Permisos tooOther aplicaciones" Hola Hola Portal de Azure.
* Multiempresa: en primer lugar, aplicación nativa de hello siempre se registra en Programador de Hola o directorio del publicador. En segundo lugar, aplicación nativa de hello es tooindicate configurado Hola permisos requiere toobe funcional. Esta lista de permisos necesarios se muestra en un cuadro de diálogo cuando un usuario o administrador en el directorio de destino de hello da su consentimiento toohello aplicación, lo que facilita la organización de tootheir disponible. Algunas aplicaciones requieren solo permisos de usuario, que cualquier usuario de hello organización puede dar el consentimiento. Otras aplicaciones necesitan permisos de nivel de administrador, lo que no se acepta un usuario de organización de Hola. Sólo un administrador de directorios puede dar consentimiento tooapplications que requieren este nivel de permisos. Cuando el usuario de Hola o el administrador consiente, API web de hello solo está registrado en su directorio. Para obtener más información, vea [Integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiración del token
Cuando la aplicación nativa de hello usa su tooget de código de autorización un token de acceso JWT, también recibe un token de actualización JWT. Cuando expira el token de acceso de hello, token de actualización de hello puede ser usado toore-autenticar usuario Hola sin solicitarle toosign de nuevo. Este token de actualización es, a continuación, usa tooauthenticate Hola usuario, que se traduce en un nuevo acceso símbolo (token) y actualiza símbolo (token).

### <a name="web-application-tooweb-api"></a>TooWeb de aplicación Web API
Esta sección describe una aplicación web que necesita recursos tooget de una API web. En este escenario, hay dos tipos de identidad que Hola aplicación web pueden usar tooauthenticate y llamar a API web de hello: una identidad de aplicación o una identidad de usuario delegado.

*Identidad de aplicación:* esta usa escenario las credenciales del cliente de OAuth 2.0 otorgar tooauthenticate hello de acceso y la aplicación hello web API. Cuando se utiliza una identidad de aplicación web de hello API solo puede detectar que aplicación de hello web llama, como Hola API web no recibió ninguna información acerca del usuario de Hola. Si la aplicación hello recibe información sobre los usuarios de hello, se enviará a través del protocolo de aplicación hello y no está firmado por Azure AD. API de web Hola confía en que aplicación de hello web autenticado usuario Hola. Por ello, este patrón se conoce como subsistema de confianza.

*Identidad de usuario delegado:* este escenario se puede conseguir de dos maneras: OpenID Connect y concesión de código de autorización OAuth 2.0 con un cliente confidencial. aplicación web de Hello Obtiene un token de acceso de usuario de hello, que demuestra toohello web API esa aplicación de web hello toohello de usuario que se autenticó correctamente y que era de aplicación web de hello tooobtain capaz de un usuario delegado identidad toocall Hola API web. Este token de acceso se envía en hello solicitud toohello API web, que autoriza al usuario de Hola y devuelve el recurso de hello deseado.

#### <a name="diagram"></a>Diagrama
![Diagrama de aplicaciones tooWeb API de Web](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descripción del flujo de protocolo
Ambos Hola identidad de aplicaciones y tipos de identidad de usuario delegado se tratan en el flujo de hello siguiente. Hola principal diferencia entre ellos es que identidad de usuario de hello delegado debe adquirir primero un código de autorización antes de hello usuario puede iniciar sesión y obtener acceso toohello web API.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identidad de aplicación con concesión de credenciales de cliente OAuth 2.0 
1. Un usuario ha iniciado sesión tooAzure AD en la aplicación web de hello (vea hello [tooWeb aplicación de explorador Web](#web-browser-to-web-application) anteriormente).
2. aplicación web de Hello debe tooacquire un token de acceso para que pueda autenticar toohello web API y recuperar recursos de hello deseado. Realiza una tooAzure de solicitud de AD extremo de token y proporcionar credenciales de hello, Id. de aplicación y URI de Id. de la aplicación de API de web.
3. Azure AD autentica la aplicación hello y devuelve un token de acceso JWT que es usado toocall hello web API.
4. A través de HTTPS, aplicación web de hello usa Hola devuelve Hola de tooadd de token de acceso JWT cadena JWT con una designación "Bearer" en encabezado de autorización de Hola de toohello web API de hello solicitud. API de web Hello, a continuación, valida el token JWT de Hola y si la validación es correcta, devuelve Hola deseado recursos.

##### <a name="delegated-user-identity-with-openid-connect"></a>Identidad de usuario delegado con OpenID Connect
1. Un usuario ha iniciado sesión en la aplicación web de tooa mediante Azure AD (vea hello [tooWeb aplicación de explorador Web](#web-browser-to-web-application) sección anterior). Si el usuario Hola de aplicación web de hello ha no ha dado su consentimiento tooallowing hello web aplicación toocall Hola API web en su nombre, el usuario de hello deberá tooconsent. aplicación Hello mostrará los permisos de Hola que necesita y si alguno de estos permisos de nivel de administrador, un usuario normal en el directorio de hello no será capaz de tooconsent. Este proceso de consentimiento solo aplica a aplicaciones de inquilinos de toomulti, las aplicaciones de inquilinos no único, como aplicación hello ya tendrá los permisos necesarios de Hola. Cuando hello usuario inició sesión, aplicación de hello web recibe un identificador de token con información sobre el usuario de hello, así como un código de autorización.
2. Con código de autorización de hello emitido por Azure AD, aplicación web de hello envía extremo de token de un tooAzure de solicitud de AD que incluye código de autorización de hello, detalles acerca de la aplicación de cliente de hello (Id. de aplicación y el URI de redireccionamiento) y Hola deseado recurso) aplicación URI del Id. de API web de hello).
3. código de autorización de Hola y obtener información acerca de la aplicación web de hello y API web se validan en Azure AD. Tras la correcta validación, Azure AD devuelve dos tokens: un token de acceso de JWT y un token de actualización de JWT.
4. A través de HTTPS, aplicación web de hello usa Hola devuelve Hola de tooadd de token de acceso JWT cadena JWT con una designación "Bearer" en encabezado de autorización de Hola de toohello web API de hello solicitud. API de web Hello, a continuación, valida el token JWT de Hola y si la validación es correcta, devuelve Hola deseado recursos.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Identidad de usuario delegado con concesión de código de autorización OAuth 2.0
1. Un usuario ya ha iniciado en la aplicación web de tooa, cuyo mecanismo de autenticación es independiente de Azure AD.
2. Hello aplicación web requiere una autorización de código tooacquire un token de acceso, por lo que envía una solicitud a través del extremo de autorización de hello explorador tooAzure de AD y proporciona Hola Id. de aplicación y URI de redirección de la aplicación web de hello después correcta autenticación. Hola usuario inicia sesión en tooAzure AD.
3. Si el usuario Hola de aplicación web de hello ha no ha dado su consentimiento tooallowing hello web aplicación toocall Hola API web en su nombre, el usuario de hello deberá tooconsent. aplicación Hello mostrará los permisos de Hola que necesita y si alguno de estos permisos de nivel de administrador, un usuario normal en el directorio de hello no será capaz de tooconsent. Este consentimiento aplica tooboth único y de varios inquilinos de la aplicación.  En caso de un solo inquilino de hello, un administrador puede realizar tooconsent de consentimiento del administrador en nombre de sus usuarios.  Esto puede hacerse mediante hello `Grant Permissions` botón en hello [Portal de Azure](https://portal.azure.com). 
4. Una vez haya consentido hello, aplicación web de hello recibe código de autorización de Hola que necesita tooacquire un token de acceso.
5. Con código de autorización de hello emitido por Azure AD, aplicación web de hello envía extremo de token de un tooAzure de solicitud de AD que incluye código de autorización de hello, detalles acerca de la aplicación de cliente de hello (Id. de aplicación y el URI de redireccionamiento) y Hola deseado recurso) aplicación URI del Id. de API web de hello).
6. código de autorización de Hola y obtener información acerca de la aplicación web de hello y API web se validan en Azure AD. Tras la correcta validación, Azure AD devuelve dos tokens: un token de acceso de JWT y un token de actualización de JWT.
7. A través de HTTPS, aplicación web de hello usa Hola devuelve Hola de tooadd de token de acceso JWT cadena JWT con una designación "Bearer" en encabezado de autorización de Hola de toohello web API de hello solicitud. API de web Hello, a continuación, valida el token JWT de Hola y si la validación es correcta, devuelve Hola deseado recursos.

#### <a name="code-samples"></a>Ejemplos de código
Vea los ejemplos de código de hello para escenarios de aplicación Web tooWeb API. Y consultarlos con frecuencia; agregamos nuevos ejemplos todo tiempo Hola. Web [tooWeb aplicación API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Registro
* Un solo inquilino: Hola aplicación web para la identidad de la aplicación hello y casos de identidad de usuario delegado, y debe estar registrado API web de Hola Hola mismo directorio en Azure AD. API de web Hola puede ser tooexpose configurado un conjunto de permisos, que son acceso tooits recursos utilizados toolimit hello de la aplicación web. Si es que se va a usar un tipo de identidad de usuario delegado, aplicación de hello web necesita permisos de hello deseado de tooselect del menú desplegable "Permisos tooOther aplicaciones" Hola Hola Portal de Azure. Este paso no es necesario si se está usando el tipo de identidad de aplicación Hola.
* Multiempresa: en primer lugar, aplicación web de hello es tooindicate configurado Hola permisos requiere toobe funcional. Esta lista de permisos necesarios se muestra en un cuadro de diálogo cuando un usuario o administrador en el directorio de destino de hello da su consentimiento toohello aplicación, lo que facilita la organización de tootheir disponible. Algunas aplicaciones requieren solo permisos de usuario, que cualquier usuario de hello organización puede dar el consentimiento. Otras aplicaciones necesitan permisos de nivel de administrador, lo que no se acepta un usuario de organización de Hola. Sólo un administrador de directorios puede dar consentimiento tooapplications que requieren este nivel de permisos. Cuando el usuario o administrador de autorizaciones, hello hello web hello y aplicación de API de web se registran en su directorio.

#### <a name="token-expiration"></a>Expiración del token
Cuando la aplicación web de hello usa su tooget de código de autorización un token de acceso JWT, también recibe un token de actualización JWT. Cuando expira el token de acceso de hello, token de actualización de hello puede ser usado toore-autenticar usuario Hola sin solicitarle toosign de nuevo. Este token de actualización es, a continuación, usa tooauthenticate Hola usuario, que se traduce en un nuevo acceso símbolo (token) y actualiza símbolo (token).

### <a name="daemon-or-server-application-tooweb-api"></a>TooWeb demonio o una aplicación de servidor de API
Esta sección describe una aplicación demonio o de servidor que necesita recursos tooget de una API web. Hay dos Subescenarios a los que se aplican toothis sección: un demonio que necesita toocall una API web, basada en el tipo de concesión de credenciales de cliente de OAuth 2.0; y una aplicación de servidor (por ejemplo, una API web) que necesita toocall una API web, depende de la especificación de borrador de OAuth 2.0 On-Behalf-Of.

Para el escenario de hello cuando una aplicación necesita toocall una API web, es importante toounderstand algunas cosas. En primer lugar, la interacción del usuario no es posible con una aplicación demonio, que requiere su propia identidad de hello toohave de aplicación. Un ejemplo de una aplicación de demonio es un proceso por lotes o un servicio de sistema operativo que se ejecuta en segundo plano de Hola. Este tipo de aplicación solicita un token de acceso mediante su identidad de aplicación y presentar su Id. de aplicación, credenciales (contraseña o certificado) y tooAzure URI del Id. de aplicación AD. Tras la autenticación correcta, el demonio de hello recibe un token de acceso de Azure AD, que es usado toocall Hola API web.

Para el escenario de hello cuando una aplicación de servidor necesita toocall una API web, resulta útil toouse muestra un ejemplo. Imagine que un usuario se autenticó en una aplicación nativa y aplicación nativa necesita toocall una API web. Azure AD emite un JWT acceso toocall token Hola API web. Si web Hola API necesita toocall otra API de web de nivel inferior, puede usar la identidad del usuario de hello en nombre de flujo toodelegate hello y autenticar la API web de segundo nivel de toohello.

#### <a name="diagram"></a>Diagrama
![Diagrama de tooWeb API demonio o una aplicación de servidor](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descripción del flujo de protocolo
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identidad de aplicación con concesión de credenciales de cliente OAuth 2.0 
1. En primer lugar, la aplicación de servidor de hello necesita tooauthenticate con Azure AD por sí misma, sin ninguna interacción como un cuadro de diálogo de inicio de sesión interactivo. Realiza una tooAzure de solicitud de AD extremo de token y proporcionar credenciales de hello, Id. de aplicación y URI de Id. de la aplicación.
2. Azure AD autentica la aplicación hello y devuelve un token de acceso JWT que es usado toocall hello web API.
3. A través de HTTPS, aplicación web de hello usa Hola devuelve Hola de tooadd de token de acceso JWT cadena JWT con una designación "Bearer" en encabezado de autorización de Hola de toohello web API de hello solicitud. API de web Hello, a continuación, valida el token JWT de Hola y si la validación es correcta, devuelve Hola deseado recursos.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>Identidad de usuario delegado con la especificación provisional "On-Behalf-Of" de OAuth 2.0
flujo de Hello descrito a continuación se da por supuesto que se ha autenticado un usuario en otra aplicación (por ejemplo, una aplicación nativa), y su identidad de usuario se ha usado tooacquire una API web de primer nivel de toohello de token de acceso.

1. aplicación nativa de Hello envía web de primer nivel de toohello de token de acceso de hello API.
2. API de web de primer nivel de Hello envía extremo de token de un tooAzure de solicitud de AD y proporcionar las credenciales y su identificador de la aplicación, así como token de acceso del usuario de Hola. Además, se envía la solicitud de hello con un on_behalf_of parámetro que indica hello web API solicita nuevos tokens toocall una API web de nivel inferior en nombre de usuario original Hola.
3. Azure AD comprueba esa API de web de primer nivel hello tiene API web de segundo nivel de permisos tooaccess hello y valida las solicitudes de hello, devuelve que un token de acceso JWT y un JWT de actualización de token toohello API de web de primer nivel.
4. A través de HTTPS, web de primer nivel de hello, a continuación, llama a API Hola API web de segundo nivel anexando la cadena de token de hello en el encabezado de autorización de hello en solicitud de Hola. API de web de primer nivel de Hello puede continuar web de segundo nivel de hello toocall API como token de acceso de Hola y tokens de actualización son válidos.

#### <a name="code-samples"></a>Ejemplos de código
Vea los ejemplos de código de hello para escenarios de tooWeb API demonio o aplicación de servidor. Y consultarlos con frecuencia; agregamos nuevos ejemplos todo tiempo Hola. [Aplicación de servidor o demonio tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Registro
* Un solo inquilino: Para la identidad de la aplicación hello y casos de identidad de usuario delegado, Hola demonio o aplicación de servidor debe estar registrada en hello mismo directorio en Azure AD. API de web Hola puede ser tooexpose configurado un conjunto de permisos, que son utilizados toolimit Hola demonio o recursos de tooits de acceso del servidor. Si es que se va a usar un tipo de identidad de usuario delegado, aplicación de servidor hello necesita permisos de hello deseado de tooselect del menú desplegable "Permisos tooOther aplicaciones" Hola Hola Portal de Azure. Este paso no es necesario si se está usando el tipo de identidad de aplicación Hola.
* Multiempresa: en primer lugar, aplicación de demonio o de servidor hello es tooindicate configurado Hola permisos requiere toobe funcional. Esta lista de permisos necesarios se muestra en un cuadro de diálogo cuando un usuario o administrador en el directorio de destino de hello da su consentimiento toohello aplicación, lo que facilita la organización de tootheir disponible. Algunas aplicaciones requieren solo permisos de usuario, que cualquier usuario de hello organización puede dar el consentimiento. Otras aplicaciones necesitan permisos de nivel de administrador, lo que no se acepta un usuario de organización de Hola. Sólo un administrador de directorios puede dar consentimiento tooapplications que requieren este nivel de permisos. Cuando el usuario de Hola o el administrador consiente, tanto de las API web de Hola se registran en su directorio.

#### <a name="token-expiration"></a>Expiración del token
Cuando la primera aplicación de hello usa su tooget de código de autorización un token de acceso JWT, también recibe un token de actualización JWT. Cuando expira el token de acceso de hello, token de actualización de hello puede ser usado toore-autenticar usuario Hola sin pedir credenciales. Este token de actualización es, a continuación, usa tooauthenticate Hola usuario, que se traduce en un nuevo acceso símbolo (token) y actualiza símbolo (token).

## <a name="see-also"></a>Otras referencias
[Guía del desarrollador de Azure Active Directory](active-directory-developers-guide.md)

[Ejemplos de código de Azure Active Directory](active-directory-code-samples.md)

[Información importante acerca de la cadencia de sustitución de clave en Azure AD](active-directory-signing-key-rollover.md)

[OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)

