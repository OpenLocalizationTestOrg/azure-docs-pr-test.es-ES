---
title: Glosario de desarrollador de Active Directory aaaAzure | Documentos de Microsoft
description: "Una lista de términos con las características y conceptos normalmente utilizados por los desarrolladores de Azure Active Directory."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Guía del desarrollador de Azure Active Directory
Este artículo contiene definiciones para algunos de los conceptos para desarrolladores de hello core Azure Active Directory (AD), que son útiles para obtener información sobre el desarrollo de aplicaciones para Azure AD.

## <a name="access-token"></a>de la aplicación Twitter
Un tipo de [token de seguridad](#security-token) emitido por un [servidor de autorización](#authorization-server)y usa un [aplicación cliente](#client-application) en orden tooaccess un [recurso servidor protegido ](#resource-server). Normalmente en forma de Hola de un [JSON Web Token (JWT)][JWT], símbolo (token) de hello personifica autorización Hola concedido toohello cliente hello [propietario del recurso](#resource-owner), para un nivel solicitado de acceso. Hello símbolo (token) contiene todos los aplicable [notificaciones](#claim) sobre asunto Hola, habilitación toouse de aplicación de cliente de hello como una forma de credenciales al tener acceso a un recurso determinado. Esto también elimina Hola de emplear Hola recursos propietario tooexpose credenciales toohello de cliente.

Tokens de acceso a veces son tooas que se hace referencia "Aplicación de usuario +" o "Solo de aplicación", dependiendo de hello credenciales representado. Por ejemplo, cuando una aplicación cliente usa:

* [Concesión de autorización de "Código de autorización"](#authorization-grant), usuario final de hello autentica primero como propietario del recurso de hello, delegar la autorización toohello cliente tooaccess Hola recursos. cliente de Hello posteriormente autentica al obtener el token de acceso de Hola. el token de Hola a veces puede ser toomore que se hace referencia específicamente como un símbolo (token) de "Aplicación de usuario +", tal y como representa usuario Hola que autorizar la aplicación de cliente de Hola y aplicación hello.
* [Concesión de autorización "Credenciales de cliente"](#authorization-grant), cliente hello proporciona autenticación único hello, funcionando sin autorización o autenticación de hello-del propietario del recurso, por lo que el token de Hola a veces puede ser tooas que se hace referencia un símbolo (token) "Solo de aplicación".

Consulte [Referencia de tokens de Azure AD][AAD-Tokens-Claims] para obtener más información.

## <a name="application-manifest"></a>manifiesto de aplicación
Una característica proporcionada por hello [portal de Azure][AZURE-portal], lo que genera una representación JSON de configuración de identidad de la aplicación hello, utilizado como un mecanismo para actualizar su asociado [ Aplicación] [ AAD-Graph-App-Entity] y [ServicePrincipal] [ AAD-Graph-Sp-Entity] entidades. Vea [manifiesto de aplicación en Azure Active Directory descripción hello] [ AAD-App-Manifest] para obtener más detalles.

## <a name="application-object"></a>objeto de aplicación
Cuando se registre o actualizar una aplicación Hola [portal de Azure][AZURE-portal], Hola crea/actualizaciones del portal de un objeto de aplicación y su correspondiente [objeto de entidad de servicio](#service-principal-object)para ese inquilino. objeto de la aplicación Hello *define* Hola configuración de identidad de la aplicación global (entre todos los inquilinos que tiene acceso), lo que proporciona una plantilla desde la que son sus correspondientes objetos de entidad de seguridad de servicio  *derivado* para su uso localmente en tiempo de ejecución (en un inquilino específico).

Para más información, consulte [Objetos Application y objetos ServicePrincipal][AAD-App-SP-Objects].

## <a name="application-registration"></a>registro de la aplicación
En orden tooallow para una aplicación toointegrate con y el delegado tooAzure de funciones de administración de identidades y acceso de AD, debe registrarse con Azure AD [inquilino](#tenant). Al registrar la aplicación con Azure AD, que está proporcionando una configuración de identidad para la aplicación, lo que le toointegrate con Azure AD y usa características como:

* Administración sólida de inicio de sesión único mediante la administración de identidades de Azure AD y la implementación del protocolo [OpenID Connect][OpenIDConnect]
* Asíncrona acceso demasiado[recursos protegidos](#resource-server) por [aplicaciones cliente](#client-application), a través OAuth 2.0 de Azure AD [servidor de autorización](#authorization-server) implementación
* [Marco de consentimiento](#consent) para administrar recursos de tooprotected de acceso de cliente, en función de autorización de propietario del recurso.

Para más información, consulte [Integración de aplicaciones con Azure Active Directory][AAD-Integrating-Apps].

## <a name="authentication"></a>Autenticación
Hola consisten en un reto a una entidad de credenciales legítimas, proporcionando la base de hello para la creación de un toobe principal de seguridad utilizado para la identidad y control de acceso. Durante una [concesión de autorización de OAuth2](#authorization-grant) por ejemplo, va a rellenar entidad Hola autenticar rol Hola del [propietario del recurso](#resource-owner) o [aplicación cliente](#client-application), en función de concesión de Hello usa.

## <a name="authorization"></a>authorization
acto de Hola de otorgar un toodo de permiso principal de seguridad autenticado algo. Hay dos casos de uso principal en el modelo de programación de hello Azure AD:

* Durante una [concesión de autorización de OAuth2](#authorization-grant) flujo: Hola cuando [propietario del recurso](#resource-owner) concede autorización toohello [aplicación cliente](#client-application), permitiendo cliente hello tooaccess Hola recursos del propietario del recurso.
* Durante el acceso a los recursos por cliente hello: tal como lo implementan hello [servidor de recursos](#resource-server), con hello [notificación](#claim) valores presentes en hello [token de acceso](#access-token) toomake el control de acceso decisiones basadas en ellas.

## <a name="authorization-code"></a>código de autorización
Una breve duración "token" proporciona tooa [aplicación cliente](#client-application) por hello [extremo de autorización](#authorization-endpoint), como parte del flujo de "código de autorización" Hola, uno de Hola OAuth2 cuatro [concede autorización ](#authorization-grant). código de Hello se devuelve la aplicación de cliente de toohello en tooauthentication de respuesta de un [propietario del recurso](#resource-owner), que indica el propietario del recurso de hello ha delegado hello tooaccess de autorización de recursos solicitados. Como parte del flujo de hello, código de hello más tarde se canjea para un [token de acceso](#access-token).

## <a name="authorization-endpoint"></a>punto de conexión de autorización
Uno de los extremos de hello implementados por hello [servidor de autorización](#authorization-server), usa toointeract con hello [propietario del recurso](#resource-owner) en orden tooprovide una [concesión de autorización](#authorization-grant) durante un flujo de concesión de autorización de OAuth2. Dependiendo de la autorización de Hola flujo de concesión utilizado, Hola real grant proporcionado puede variar, incluidos un [código de autorización](#authorization-code) o [token de seguridad](#security-token).

Vea la especificación de hello OAuth2 [tipos de concesión de autorización] [ OAuth2-AuthZ-Grant-Types] y [extremo de autorización] [ OAuth2-AuthZ-Endpoint] secciones y hello [Especificación de OpenIDConnect] [ OpenIDConnect-AuthZ-Endpoint] para obtener más detalles.

## <a name="authorization-grant"></a>concesión de autorización
Una credencial que representa hello [del propietario del recurso](#resource-owner) [autorización](#authorization) tooaccess sus recursos protegidos, concedidos tooa [aplicación cliente](#client-application). Una aplicación cliente puede utilizar uno de hello [cuatro conceder tipos definidos por el marco de autorización de OAuth2 de hello] [ OAuth2-AuthZ-Grant-Types] tooobtain una instrucción grant, según los requisitos de tipo de cliente: "concesión de código de autorización", " concesión las credenciales del cliente","concesión implícita"y"concesión de credenciales de contraseña de propietario de recurso". credencial de Hello devuelto toohello cliente sea un [token de acceso](#access-token), o un [código de autorización](#authorization-code) (intercambia más adelante para un token de acceso), según el tipo de saludo de concesión de autorización que se utiliza.

## <a name="authorization-server"></a>servidor de autorización
Tal como se define por hello [marco de autorización de OAuth2][OAuth2-Role-Def], servidor hello responsable de emitir acceso tokens toohello [cliente](#client-application) después de la autenticación es correcta Hola [propietario del recurso](#resource-owner) y obtener su autorización. A [aplicación cliente](#client-application) interactúa con el servidor de autorización de hello en tiempo de ejecución a través de su [autorización](#authorization-endpoint) y [token](#token-endpoint) puntos de conexión, con arreglo a hello OAuth2 definido [concede autorización](#authorization-grant).

En caso de hello de integración de aplicaciones de Azure AD, Azure AD implementa rol de servidor de autorización de Hola para aplicaciones de Azure AD y el servicio de Microsoft de las API, por ejemplo [Microsoft Graph API][Microsoft-Graph].

## <a name="claim"></a>notificación
A [token de seguridad](#security-token) contiene notificaciones, que proporcionan las aserciones acerca de una entidad (como un [aplicación cliente](#client-application) o [propietario del recurso](#resource-owner)) tooanother entidad (por ejemplo, hello [servidor de recursos](#resource-server)). Las notificaciones son pares de nombre/valor que hechos acerca del asunto del token Hola de retransmisión (por ejemplo, entidad de seguridad de Hola que autenticó hello [servidor de autorización](#authorization-server)). Hola notificaciones presentes en un token determinado dependen de varias variables, incluido el tipo hello de token, tipo hello de credencial que usa tooauthenticate Hola asunto, configuración de la aplicación hello, etcetera.

Consulte [Referencia de tokens de Azure AD][AAD-Tokens-Claims] para obtener más información.

## <a name="client-application"></a>aplicación cliente
Tal como se define por hello [marco de autorización de OAuth2][OAuth2-Role-Def], protegido de una aplicación que realiza las solicitudes de recursos en nombre de hello [propietario del recurso](#resource-owner). término Hola "cliente" no implica ninguna característica de implementación de hardware determinado (por ejemplo, si aplicación hello se ejecuta en un servidor, un equipo de escritorio u otros dispositivos).  

Una aplicación cliente solicita [autorización](#authorization) desde un tooparticipate de propietario de recursos en un [concesión de autorización de OAuth2](#authorization-grant) flujo y puede tener acceso a datos o las API en nombre del propietario del recurso de Hola. Hola marco de autorización de OAuth2 [define dos tipos de clientes][OAuth2-Client-Types], "confidencial" y "pública", en función capacidad toomaintain Hola confidencialidad del cliente de hello sus credenciales. Las aplicaciones pueden implementar un [cliente web (confidencial)](#web-client) que se ejecuta en un servidor web, un [cliente nativo (público)](#native-client) instalado en un dispositivo y un [cliente basado en agente usuario (público)](#user-agent-based-client) que se ejecuta en el explorador de un dispositivo.

## <a name="consent"></a>consentimiento
Hola de proceso de un [propietario del recurso](#resource-owner) conceder autorización tooa [aplicación cliente](#client-application), tooaccess protegido recursos específicos de [permisos](#permissions), en nombre de Hola propietario del recurso. En función de permisos de hello solicitados por el cliente de hello, un administrador o usuario le pedirán datos organización/individual de consentimiento tooallow acceso tootheir respectivamente. Tenga en cuenta que en un [multiempresa](#multi-tenant-application) escenario, la aplicación hello [entidad de servicio](#service-principal-object) también se registra en el inquilino de Hola de usuario de consentimiento de Hola.

## <a name="id-token"></a>token de identificador
Un [OpenID Connect] [ OpenIDConnect-ID-Token] [token de seguridad](#security-token) proporcionada por un [del servidor de autorización](#authorization-server) [deextremodeautorización](#authorization-endpoint), que contiene [notificaciones](#claim) pertinentes de toohello de autenticación de un usuario final [propietario del recurso](#resource-owner). Al igual que un token de acceso, los tokens de identificador también se representan como [JSON Web Token (JWT)][JWT] firmados digitalmente. A diferencia de un token de acceso, notificaciones de un identificador de token no se utilizan para fines relacionados tooresource acceso y control de acceso de específicamente.

Consulte [Referencia de tokens de Azure AD][AAD-Tokens-Claims] para obtener más información.

## <a name="multi-tenant-application"></a>aplicación multiinquilino
Una clase de aplicación que habilita el inicio de sesión y [consentimiento](#consent) usuarios aprovisionado en Azure AD [inquilino](#tenant), incluidos los inquilinos distintos Hola uno donde se registra el cliente de Hola. [Cliente nativo](#native-client) aplicaciones son multiempresa de forma predeterminada, mientras que [cliente web](#web-client) y [web API derecursos/](#resource-server) aplicaciones tienen Hola capacidad tooselect entre uno o varios inquilinos. Por el contrario, una aplicación web había registrado como único inquilino, solo se permiten inicios de sesión de cuentas de usuario aprovisionados en hello mismo inquilino como Hola uno donde se registra la aplicación hello.

Vea [cómo toosign en cualquier usuario de Azure AD mediante Hola patrón de aplicación de varios inquilinos] [ AAD-Multi-Tenant-Overview] para obtener más detalles.

## <a name="native-client"></a>cliente nativo
Un tipo de [aplicación cliente](#client-application) que se instala de forma nativa en un dispositivo. Puesto que todo el código se ejecuta en un dispositivo, se considera a un cliente "público" pagar tooits incapacidad toostore credenciales privado o confidencial. Consulte los [tipos de cliente y perfiles de OAuth2][OAuth2-Client-Types] para más información.

## <a name="permissions"></a>permisos
A [aplicación cliente](#client-application) mejoras en el acceso a tooa [servidor de recursos](#resource-server) mediante la declaración de las solicitudes de permiso. Existen dos tipos:

* "Permisos", que especifican [basados en ámbitos](#scopes) acceso mediante delegado autorización de hello firmado en [propietario del recurso](#resource-owner), se presentan toohello recursos en tiempo de ejecución como ["scp "notificaciones](#claim) de cliente hello [token de acceso](#access-token).
* Permisos de "Aplicación", lo que especifiquen [basada en roles](#roles) tener acceso utilizando las credenciales de identidad o de la aplicación de cliente de hello, se presentan toohello recursos en tiempo de ejecución como [notificaciones "roles"](#claim) Hola token de acceso del cliente.

También se revelan durante hello [consentimiento](#consent) proceso, dando a Administrador de Hola o recursos propietario Hola oportunidad toogrant/denegar tooresources de acceso de cliente de hello en su inquilino.

Las solicitudes de permiso se configuran en hello "Applications" / ficha "Configuración" Hola [portal de Azure][AZURE-portal], en "Permisos necesarios", seleccionando Hola deseado "Permisos delegados" y " Permisos de la aplicación"(Hola último requiere la pertenencia al rol de administrador Global de hello). Dado que un [cliente público](#client-application) no firmemente credenciales, solo puede solicitar permisos delegados, mientras un [cliente confidencial](#client-application) tiene Hola capacidad toorequest delegado y de aplicación permisos. cliente de Hello [objeto application](#application-object) Hola almacenes declarado permisos en su [requiredResourceAccess propiedad][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>propietario del recurso
Tal como se define por hello [marco de autorización de OAuth2][OAuth2-Role-Def], una entidad con capacidad de conceder acceso tooa al recurso protegido. Cuando el propietario del recurso de hello es una persona, es que se hace referencia tooas un usuario final. Por ejemplo, cuando un [aplicación cliente](#client-application) desea tooaccess buzón de un usuario a través de hello [Microsoft Graph API][Microsoft-Graph], requiere el permiso del propietario del recurso de Hola de buzón de Hola.

## <a name="resource-server"></a>servidor de recursos
Tal como se define por hello [marco de autorización de OAuth2][OAuth2-Role-Def], solicita un servidor que hospeda recursos protegidos, capaces de acepta y responde tooprotected recursos [cliente aplicaciones](#client-application) que estén presentes un [token de acceso](#access-token). También se conoce como servidor de recursos protegidos, o aplicación de recursos.

Un servidor de recursos expone las API y aplica el acceso a los recursos protegidos de tooits a través de [ámbitos](#scopes) y [roles](#roles), utilizando Hola marco de autorización de OAuth 2.0. Los ejemplos incluyen hello Azure AD Graph API que proporciona acceso a datos de inquilino tooAzure AD y Hola API de Office 365 que proporcionan acceso toodata como correo electrónico y el calendario. Ambos también son accesibles a través de hello [Microsoft Graph API][Microsoft-Graph].  

Al igual que una aplicación cliente, se establece la configuración de la identidad de la aplicación de recursos a través de [registro](#application-registration) en un inquilino de Azure AD, proporcionando la aplicación hello y objeto de entidad de servicio. Algunas API proporcionada por Microsoft, como la API de Azure AD Graph, Hola han registrado previamente las entidades de servicio estará disponibles en todos los inquilinos durante el aprovisionamiento.

## <a name="roles"></a>roles
Al igual que [ámbitos](#scopes), los roles proporcionan una manera para que un [servidor de recursos](#resource-server) toogovern tooits de acceso a los recursos protegidos. Hay dos tipos: un rol "user" implementa el control de acceso basado en roles para los usuarios o grupos que requieren acceso a recursos de toohello, mientras que implementa un rol de "aplicación" hello mismo para [aplicaciones cliente](#client-application) que requieren acceso.

Roles son cadenas definidas por el recurso (por ejemplo "aprobación de gastos," "Solo lectura", "Directory.ReadWrite.All") y administrar en hello [portal de Azure] [ AZURE-portal] a través del recurso de hello [aplicación manifiesto](#application-manifest)y se almacenan en el recurso de hello [appRoles propiedad][AAD-Graph-Sp-Entity]. Hello portal de Azure también es usado tooassign usuarios demasiado funciones de "usuario" y configurar el cliente [permisos de aplicación](#permissions) tooaccess un rol de "aplicación".

Para obtener una explicación detallada de los roles de aplicación Hola expuestos por la API de Graph de Azure AD, consulte [ámbitos de permiso de API de Graph][AAD-Graph-Perm-Scopes]. Para ver un ejemplo de implementación paso a paso, consulte [Role based access control in cloud applications using Azure AD][Duyshant-Role-Blog] (Control de acceso basado en rol en aplicaciones en la nube con Azure AD).

## <a name="scopes"></a>ámbitos
Al igual que [roles](#roles), ámbitos proporcionan una manera para que un [servidor de recursos](#resource-server) toogovern tooits de acceso a los recursos protegidos. Los ámbitos son utilizado tooimplement [basados en ámbitos] [ OAuth2-Access-Token-Scopes] control de acceso, para un [aplicación cliente](#client-application) que se le han otorgado acceso delegado toohello recurso por su propietario.

Ámbitos son definidos por el recurso de cadenas (por ejemplo "Mail.Read", "Directory.ReadWrite.All"), administradas en hello [portal de Azure] [ AZURE-portal] a través del recurso de hello [manifiesto de aplicación](#application-manifest)y se almacenan en el recurso de hello [oauth2Permissions propiedad][AAD-Graph-Sp-Entity]. Hello portal de Azure también es aplicación de cliente usado tooconfigure [permisos delegados](#permissions) tooaccess un ámbito.

Una convención de nomenclatura de práctica recomendada, es toouse un formato de "recurso.operación.restricción". Para obtener una explicación detallada de los ámbitos de hello expuestos por la API de Graph de Azure AD, consulte [ámbitos de permiso de API de Graph][AAD-Graph-Perm-Scopes]. Para los ámbitos expuestos por los servicios de Office 365, consulte [Office 365 API permissions reference][O365-Perm-Ref] (Referencia a los permisos de la API de Office 365).

## <a name="security-token"></a>token de seguridad
Un documento firmado con notificaciones, como un token OAuth2 o una aserción SAML 2.0. En el caso de una [concesión de autorización](#authorization-grant) de OAuth2, un [token de acceso](#access-token) (OAuth2) y un [token de identificador](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) son tipos de token de seguridad, que se implementan como un [JSON Web Token (JWT)][JWT].

## <a name="service-principal-object"></a>objeto de entidad de servicio
Cuando se registre o actualizar una aplicación Hola [portal de Azure][AZURE-portal], portal de hello creaciones, actualizaciones tanto un [objeto application](#application-object) y una entidad de servicio correspondiente objeto de ese inquilino. objeto de la aplicación Hello *define* Hola configuración de identidad de la aplicación global (entre todos los inquilinos donde aplicación hello asociado se ha concedido acceso), y es Hola plantilla desde la que su servicio correspondiente objetos de entidad de seguridad son *derivado* para su uso localmente en tiempo de ejecución (en un inquilino específico).

Para más información, consulte [Objetos Application y objetos ServicePrincipal][AAD-App-SP-Objects].

## <a name="sign-in"></a>inicio de sesión
Hola de proceso de un [aplicación cliente](#client-application) inicia autenticación de usuario final y capturar relacionadas con el estado, a fin de Hola de adquisición de un [token de seguridad](#security-token) y toothat de sesión de aplicación Hola de ámbito estado. El estado puede incluir artefactos, como información de perfil de usuario, e información derivada de las notificaciones de tokens.

Hola inicio de sesión en función de una aplicación es usado normalmente tooimplement inicio de sesión único (SSO). También se puede precedido por una función de "inicio de sesión", como punto de entrada de Hola para una aplicación de usuario final toogain acceso tooan (después del primer inicio de sesión de entrada). Hello suscripción función toogather usado y usuario toohello específico de información de estado adicional se conservan y puede requerir [consentimiento del usuario](#consent).

## <a name="sign-out"></a>cierre de sesión
Hola proceso de autenticación sin un usuario final, separar el estado de usuario de hello asociado hello [aplicación cliente](#client-application) sesión durante [inicio de sesión](#sign-in)

## <a name="tenant"></a>tenant
Una instancia de un directorio de Azure AD es tooas que se hace referencia un inquilino de Azure AD. Proporciona una variedad de características, incluidos:

* Un servicio de registro de aplicaciones integradas
* Autenticación de cuentas de usuario y aplicaciones registradas
* Extremos REST necesario toosupport diversos protocolos incluyen OAuth2 y SAML, incluidos hello [extremo de autorización](#authorization-endpoint), [extremo de token](#token-endpoint) y Hola "comunes" extremo utilizado por [ aplicaciones de varios inquilinos](#multi-tenant-application).

Un inquilino también está asociado con un anuncio de Azure o una suscripción de Office 365 durante el aprovisionamiento de suscripción de hello, que proporciona características de administración de identidad y acceso para la suscripción de Hola. Vea [cómo inquilino de Azure Active Directory tooget] [ AAD-How-To-Tenant] para obtener detalles sobre Hola de diversas formas de obtener acceso tooa los inquilinos. Vea [suscripciones de Azure están asociadas con Azure Active Directory] [ AAD-How-Subscriptions-Assoc] para obtener más información sobre la relación de hello entre las suscripciones y un inquilino de Azure AD.

## <a name="token-endpoint"></a>punto de conexión de token
Uno de los extremos de hello implementados por hello [servidor de autorización](#authorization-server) toosupport OAuth2 [concede autorización](#authorization-grant). Dependiendo de la instrucción grant hello, puede ser usado tooacquire un [token de acceso](#access-token) (y el símbolo de "Actualizar" relacionados) tooa [cliente](#client-application), o [identificador de token](#ID-token) cuando se usa con hello [ OpenID Connect] [ OpenIDConnect] protocolo.

## <a name="user-agent-based-client"></a>cliente basada en agente usuario
Un tipo de [aplicación cliente](#client-application) que descarga código desde un servidor web y se ejecuta dentro de un agente usuario (por ejemplo, un explorador web), como una aplicación de página única (SPA). Puesto que todo el código se ejecuta en un dispositivo, se considera a un cliente "público" pagar tooits incapacidad toostore credenciales privado o confidencial. Consulte los [tipos de cliente y perfiles de OAuth2][OAuth2-Client-Types] para más información.

## <a name="user-principal"></a>entidad de seguridad de usuario
Manera de toohello que un objeto de entidad de servicio es toorepresent usa una instancia de aplicación similar, un objeto de entidad de usuario es otro tipo de entidad de seguridad, que representa a un usuario. Hello Azure AD Graph [entidad de usuario] [ AAD-Graph-User-Entity] define el esquema de Hola para un objeto de usuario, incluidas las propiedades relacionadas con el usuario, como el nombre y apellido, nombre principal de usuario, pertenencia al rol de directorio, etcetera. Esto proporciona una configuración de identidad de usuario de Hola para Azure AD tooestablish una entidad de seguridad en tiempo de ejecución de usuario. Hola principal de usuario es toorepresent usa un usuario autenticado para inicio de sesión único, grabación [consentimiento](#consent) delegación, hacer que las decisiones de control de acceso, etcetera.

## <a name="web-client"></a>cliente web
Un tipo de [aplicación cliente](#client-application) que ejecuta todo el código en un servidor web y puede toofunction como un cliente "confidencial" almacenar sus credenciales de forma segura en el servidor de Hola. Consulte los [tipos de cliente y perfiles de OAuth2][OAuth2-Client-Types] para más información.

## <a name="next-steps"></a>Pasos siguientes
Hola [Guía del desarrollador de Azure AD] [ AAD-Dev-Guide] es hello toouse portal para todo el desarrollo de Azure AD relacionadas con temas, incluida una descripción general de [integración de aplicaciones] [ AAD-How-To-Integrate] y conceptos básicos de Hola de [autenticación de Azure AD y escenarios de autenticación admitidos][AAD-Auth-Scenarios].

Use Hola después de comentarios de tooprovide de sección de comentarios y nos ayudan a refinar y dar forma a nuestro contenido, incluidas las solicitudes nuevas definiciones o actualizar las existentes.

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
