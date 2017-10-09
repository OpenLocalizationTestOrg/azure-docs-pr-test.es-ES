---
title: "aaaHow toobuild una aplicación que puede iniciar sesión en cualquier usuario de Azure AD | Documentos de Microsoft"
description: "Instrucciones paso a paso para crear una aplicación que pueda iniciar la sesión de un usuario desde cualquier inquilino de Azure Active Directory, lo que se conoce también como aplicación multiempresa."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>¿Cómo toosign en cualquier usuario de Azure Active Directory (AD) mediante Hola patrón de aplicación de varios inquilinos
Si ofrece un Software como un toomany de aplicación de servicio de las organizaciones, puede configurar sus aplicación tooaccept inicios de sesión desde cualquier inquilino de Azure AD.  En Azure AD, esto se conoce como convertir su aplicación en una aplicación multiempresa.  Los usuarios de cualquier inquilino de Azure AD será capaz de toosign en tooyour aplicación después de dar su consentimiento toouse su cuenta con la aplicación.  

Si tiene una aplicación existente que tiene su propio sistema de cuenta o es compatible con otros tipos de inicio de sesión de otros proveedores de nube, es sencillo agregar el inicio de sesión de Azure AD desde cualquier inquilino. Solo tiene que registrar la aplicación, agregar el código de inicio de sesión a través de OAuth2, OpenID Connect o SAML e incluir el botón "Iniciar sesión con Microsoft" en la aplicación. Haga clic en hello después botón toolearn más información acerca de la aplicación de personalización de marca.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

En este artículo se da por supuesto que ya está familiarizado con la creación de una aplicación de un solo inquilino para Azure AD.  Si no está, head respaldar toohello [página principal de guía para desarrolladores] [ AAD-Dev-Guide] y pruebe una de nuestras guías de inicio rápidos.

Hay cuatro tooconvert sencillos pasos de la aplicación en una aplicación de varios inquilinos de Azure AD:

1. Actualizar al inquilino de varios de toobe de registro de aplicación
2. Actualizar su/Common toohello de las solicitudes de código toosend extremo 
3. Actualizar el código toohandle varios valores de emisor
4. Comprenda el consentimiento de administrador y usuario y realice los cambios apropiados en el código

Vamos a examinar cada paso con detalle. También puede saltar directamente demasiado[esta lista de ejemplos de varios inquilinos][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Actualizar a varios inquilinos de registro toobe
De forma predeterminada, los registros de API y de aplicación web en Azure son de un solo inquilino.  Puede realizar el registro de varios inquilinos mediante la búsqueda de Hola "varios inquilinos" cambiar de página de propiedades de Hola de su registro de la aplicación Hola [portal de Azure] [ AZURE-portal] y si se establece demasiado "Sí".

También tenga en cuenta que para poder realizar una aplicación multiempresa, Azure AD necesita Hola App ID URI de hello aplicación toobe único global. Hola App ID URI es uno de los modos de hello que identifica a una aplicación en los mensajes de protocolo.  Para una aplicación de un solo inquilino, es suficiente para hello App ID URI toobe único dentro de ese inquilino.  Para una aplicación de varios inquilinos, debe ser único globalmente para que Azure AD pueda encontrar la aplicación hello entre todos los inquilinos.  Se aplica la unicidad global exigiendo Hola App ID URI toohave un nombre de host que coincida con un dominio comprobado del inquilino de Azure AD Hola.  Por ejemplo, si el nombre de hello del inquilino era contoso.onmicrosoft.com, a continuación, válido App ID URI sería `https://contoso.onmicrosoft.com/myapp`.  Si el inquilino tenía el dominio comprobado `contoso.com`, también sería un URI de id. de aplicación válido `https://contoso.com/myapp`.  Se producirá un error al configurar una aplicación como multiempresa si Hola App ID URI no sigue este patrón.

Los registros de cliente nativo son multiempresa de forma predeterminada.  No es necesario tootake cualquier toomake acción cliente nativo aplicación registro de varios inquilinos.

## <a name="update-your-code-toosend-requests-toocommon"></a>Actualizar el código toosend solicitudes demasiado/comunes
En una aplicación de un solo inquilino, las solicitudes de inicio de sesión se envían inicio de sesión de extremo del inquilino de toohello. Por ejemplo, para contoso.onmicrosoft.com extremo Hola sería:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Las solicitudes se envían el extremo del inquilino de tooa puede iniciar sesión en los usuarios (o invitados) en ese tooapplications inquilino en ese inquilino.  Con una aplicación de varios inquilinos, no sabe la aplicación hello por adelantado qué usuario Hola de inquilinos es, por lo que no se puede enviar solicitudes de punto de conexión del inquilino de tooa.  En su lugar, las solicitudes se envían extremo tooan que multiplexes entre AD de Azure todos los inquilinos:

    https://login.microsoftonline.com/common

Cuando Azure AD recibe una solicitud en hello/extremo común, inicia la sesión de usuario de hello en y como consecuencia detecta que el usuario inquilino Hola pertenece.  Hola/extremo común funciona con todos los protocolos de autenticación de hello compatibles con Azure AD: OpenID Connect, OAuth 2.0, SAML 2.0 y WS-Federation.

aplicación de toohello de respuesta de inicio de sesión de Hello, a continuación, contiene un token que representa el usuario de Hola.  valor de emisor de Hello en el token de hello indica que una aplicación qué usuario Hola de inquilinos es de.  Cuando devuelve una respuesta de Hola/extremo común, valor de emisor de hello en el token de hello corresponderá a inquilino del usuario toohello.  Es importante toonote Hola/extremo común no es un inquilino y no es un emisor, es simplemente un multiplexor.  Cuando se utiliza/Common, lógica de hello en los tokens de toovalidate de aplicación debe toobe actualiza tootake esto en cuenta. 

Como las aplicaciones de varios inquilinos mencionadas anteriormente, también deben proporcionar una experiencia de inicio de sesión coherente para los usuarios, siguiente Hola directrices de personalización de marca de aplicación de Azure AD. Haga clic en hello después botón toolearn más información acerca de la aplicación de personalización de marca.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

¡Eche un vistazo a la utilice Hola de/Common Hola punto de conexión y su implementación en el código con más detalle.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Actualizar el código toohandle varios valores de emisor
Las aplicaciones web y las API web reciben y validan los tokens desde Azure AD.  

> [!NOTE]
> Mientras que las aplicaciones cliente nativas solicitar y reciban tokens de Azure AD, lo hacen toosend por lo que les tooAPIs, en el que se validarán.  Las aplicaciones nativas no validan los tokens y deben tratarlos como opacos.
> 
> 

Veamos cómo una aplicación valida los tokens que recibe de Azure AD.  Una aplicación de un solo inquilino tomará normalmente un valor de punto de conexión como:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

y use tooconstruct como una dirección URL de metadatos (en este caso, OpenID Connect):

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

partes esenciales toodownload dos de información que son utilizados toovalidate tokens: inquilino Hola de firma de claves y el valor del emisor.  Cada inquilino de Azure AD tiene un valor único del emisor del formulario de hello:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

donde el valor GUID de hello es versión de Hola seguro para cambiar el nombre de identificador del inquilino Hola de Hola.  Si hace clic en hello anterior vínculo de metadatos para `contoso.onmicrosoft.com`, puede ver este valor del emisor en el documento de Hola.

Cuando una aplicación de un solo inquilino valida un token, comprueba la firma de hello del token de hello contra Hola claves de documento de metadatos de Hola de firma. Esto le permite toomake que el valor de emisor Hola Hola coincidencias token Hola uno que se encontró en el documento de metadatos de Hola.

Desde Hola/comunes punto de conexión no corresponde a tooa inquilino y no es un emisor, al examinar el valor de emisor de hello en los metadatos de Hola para/común tiene una dirección URL basada en plantilla en lugar de un valor real:

    https://sts.windows.net/{tenantid}/

Por lo tanto, una aplicación de varios inquilinos no puede validar los tokens simplemente comparando el valor de emisor de hello en los metadatos de hello con hello `issuer` valor de token de Hola.  Una aplicación multiempresa necesidades de lógica toodecide qué valores de emisor son válidos y que están no, tomando como base el inquilino de hello parte del identificador del valor de emisor de Hola.  

Por ejemplo, si una aplicación de varios inquilinos solo permite iniciar sesión de inquilinos específicos que se suscribieron para su servicio, a continuación, debe comprobar el valor del emisor de Hola o hello `tid` valor en hello token toomake seguro de ese inquilino está en su lista de notificación suscriptores.  Si una aplicación multiempresa sólo trabaja con usuarios y no tiene ninguna decisión relativa al acceso en función de los inquilinos, a continuación, puede omitir el valor del emisor de Hola por completo.

En los ejemplos de varios inquilinos de Hola Hola [Related Content](#related-content) sección Hola final de este artículo, la validación del emisor está deshabilitado tooenable cualquier toosign del inquilino de Azure AD en.

Ahora Echemos un vistazo a la experiencia del usuario de Hola para los usuarios que inician sesión en las aplicaciones de inquilinos toomulti.

## <a name="understanding-user-and-admin-consent"></a>Comprensión del consentimiento de usuario y administrador
Para toosign de usuario en la aplicación tooan en Azure AD, aplicación hello debe estar representado en el inquilino del usuario de Hola.  Esto permite organizar de hello toodo cosas como aplicar directivas únicas cuando los usuarios de su inquilino de sesión en la aplicación toohello.  En una aplicación de un solo inquilino, este registro es simple; ha Hola uno que se produce al registrar la aplicación hello en hello [portal de Azure][AZURE-portal].

Para una aplicación de varios inquilinos, Hola inicial en el registro para aplicación hello vive en hello inquilino de Azure AD utilizada Hola programador.  Cuando un usuario de un inquilino diferente inicia sesión en la aplicación de toohello para hello primera vez, Azure AD les pide tooconsent toohello permisos solicitados por la aplicación hello.  Si dar el consentimiento, a continuación, llama a una representación de la aplicación hello un *entidad de servicio* se crea en Hola inquilino del usuario y en el inicio de sesión puede continuar. También se crea una delegación en directorio de Hola que registra la aplicación de toohello de consentimiento del usuario de Hola. Vea [objetos de entidad de servicio y aplicación] [ AAD-App-SP-Objects] para obtener más información sobre la aplicación hello objetos Application y ServicePrincipal, y cómo se relacionan tooeach otro.

![Aplicación de toosingle-nivel de consentimiento][Consent-Single-Tier] 

Esta experiencia de consentimiento se ve afectada por permisos de hello solicitados por la aplicación hello.  Azure AD admite dos clases de permisos, solo de aplicación o delegado:

* Un permiso delegado concede un tooact de capacidad de aplicación Hola pueda realizar un usuario con sesión iniciada para un subconjunto de usuario de hello cosas Hola.  Por ejemplo, puede conceder a una aplicación Hola permisos delegados tooread Hola firmado en el calendario del usuario.
* Se concede un permiso de solo de aplicación directamente toohello identidad de aplicación hello.  Por ejemplo, puede conceder una lista de hello aplicación Hola permiso de solo aplicación tooread de usuarios en un inquilino, sin tener en cuenta que ha iniciado sesión en la aplicación toohello.

Algunos permisos pueden ser tooby con consentimiento de un usuario normal, mientras que otras requieren el consentimiento del Administrador de inquilinos. 

### <a name="admin-consent"></a>Consentimiento de administrador
Los permisos de solo aplicación siempre requieren el consentimiento del administrador de inquilinos.  Si la aplicación solicita un permiso de solo de aplicación y un usuario intenta toosign en toohello aplicación, se mostrará un mensaje de error que indica que el usuario de hello no es capaz de tooconsent.

Algunos permisos delegados también requieren el consentimiento del administrador de inquilinos.  Por ejemplo, hello capacidad toowrite atrás tooAzure AD como Hola firmado en usuario requiere consentimiento del Administrador de inquilinos.  Como los permisos de solo de aplicación, si trata de un usuario normal toosign en la aplicación de tooan que solicita un permiso delegado que requiere el consentimiento del administrador, la aplicación recibirá un error.  Si un permiso requiere consentimiento del administrador viene determinado por el desarrollador de Hola que publican los recursos de Hola y puede encontrarse en la documentación de hello para el recurso de Hola.  Vincula tootopics que describe los permisos disponibles de Hola para hello Azure AD Graph API y la API de Graph de Microsoft son Hola [Related Content](#related-content) sección de este artículo.

Si la aplicación usa los permisos que requieren el consentimiento del administrador, deberá toohave un movimiento como un botón o vínculo que Hola, administrador puede iniciar la acción de Hola.  solicitud de Hello envía su aplicación para esta acción es una solicitud de autorización de OAuth2/OpenID Connect habitual, pero que también incluye hello `prompt=admin_consent` parámetro de cadena de consulta.  Una vez que ha dado su consentimiento Hola, administrador y entidad de servicio de Hola se crea en el inquilino del cliente de hello, las solicitudes de inicio de sesión posteriores no es necesario hello `prompt=admin_consent` parámetro. Puesto que ha decidido administrador Hola Hola solicita permisos son aceptables, ningún otro usuario de inquilino de hello le pedirá su consentimiento a partir de ese punto.

Hola `prompt=admin_consent` parámetro también se puede utilizar con las aplicaciones que solicitan permisos que no se requiere el consentimiento del administrador. Esto se hace cuando la aplicación hello requiere una experiencia donde un administrador de inquilinos Hola "se suscribe" uno se piden a los usuarios de tiempo y ninguna otros consentimiento desde ese punto en.

Si una aplicación requiere el consentimiento del administrador y un administrador inicia sesión en pero hello `prompt=admin_consent` parámetro no se envía, Hola, administrador correctamente dar su consentimiento aplicación toohello **únicamente para su cuenta de usuario**.  Los usuarios regulares todavía no estará pueda toosign en y aplicación toohello de consentimiento.  Esto es útil si desea que Administrador de inquilinos de toogive Hola Hola capacidad tooexplore la aplicación antes de permitir el acceso a otros usuarios.

Un administrador de inquilinos puede deshabilitar la capacidad de Hola para los usuarios regulares tooconsent tooapplications.  Si se deshabilita esta capacidad, siempre es necesario para hello toobe de aplicación configurado en el inquilino de hello consentimiento del administrador.  Si desea que tootest su aplicación con consentimiento de usuario normal deshabilitada, encontrará modificador de configuración de hello en inquilino de Azure AD Hola sección de configuración del programa Hola a [portal de Azure][AZURE-portal].

> [!NOTE]
> Algunas aplicaciones desea una experiencia donde los usuarios normales son tooconsent capaz de inicialmente, y puede incluir la aplicación hello posterior administrador hello y solicitar los permisos que requieren el consentimiento del administrador.  No hay ningún toodo de manera esto con un registro de aplicación único en Azure AD hoy en día.  el punto de conexión de Hello próximo AD Azure v2 le permitirá aplicaciones toorequest permisos en tiempo de ejecución, en lugar de en tiempo de registro, lo que le permitirá este escenario.  Para obtener más información, vea hello [guía para desarrolladores de modelo de aplicación de Azure AD v2][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Consentimiento y aplicaciones de niveles múltiples
La aplicación puede tener varios niveles, cada uno representado por su propio registro en Azure AD.  Por ejemplo, una aplicación nativa que llama a una API web o una aplicación web que llama a una API web.  En ambos casos, cliente de hello (aplicación nativa o una aplicación web) solicita recursos Hola de toocall permisos (API de web).  Para hello cliente toobe aceptada correctamente en el inquilino de un cliente, todos los toowhich de recursos solicita permisos ya debe existir en el inquilino del cliente de Hola.  Si no se cumple esta condición, Azure AD devolverá un error que Hola recursos debe agregarse en primer lugar.

**Múltiples niveles en un solo inquilino**

Esto puede ser un problema si la aplicación lógica consta de dos o más registros de aplicación, por ejemplo, un cliente y un recurso independientes.  ¿Cómo se consigue recursos hello en el inquilino de cliente hello primera?  Azure AD trata este caso habilitando el cliente y el recurso toobe consentido en un solo paso. usuario de Hello ve la suma total de Hola de permisos de Hola solicitados por el cliente de Hola y recursos en la página de consentimiento de Hola.  tooenable este comportamiento, registro de la aplicación del recurso de Hola debe incluir el identificador de aplicación del cliente de Hola como un `knownClientApplications` en su manifiesto de aplicación.  Por ejemplo:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Esta propiedad se puede actualizar a través de recursos de hello [manifiesto de la aplicación][AAD-App-Manifest]. Esto se muestra en un cliente nativo de nivel múltiples llamar al ejemplo de API web de hello [Related Content](#related-content) sección Hola final de este artículo. Hello siguiente diagrama proporciona una visión general de consentimiento para una aplicación de varios nivel registrada en un solo inquilino:

![Aplicación de cliente conocidas de toomulti nivel de consentimiento][Consent-Multi-Tier-Known-Client] 

**Múltiples niveles en varios inquilinos**

Un caso similar se produce si se ha registrado distintos niveles de una aplicación de hello en varios inquilinos.  Por ejemplo, considere el caso de hello de la creación de una aplicación cliente nativa que llama Hola API de Office 365 Exchange Online.  toodevelop Hola nativos aplicaciones y versiones posteriores para toorun de la aplicación nativa de hello en el inquilino de un cliente, de entidad de servicio de Exchange Online de hello debe estar presente.  En este caso, hello desarrollador y el cliente deben adquirir Exchange Online para toobe principal del servicio Hola creado en sus inquilinos.  

En caso de hello de una API generada por una organización que no sea de Microsoft, el desarrollador de Hola de hello API debe tooprovide una manera para su aplicación de los clientes tooconsent hello en los inquilinos de sus clientes. Hola recomienda diseño es para Hola 3ª parte developer toobuild Hola API tal que también puede funcionar como un inicio de sesión de tooimplement de cliente web:

1. Siga Hola Hola de tooensure secciones anterior API implementa los requisitos / código de registro de aplicación de varios inquilinos de Hola
2. Además tooexposing Hola API ámbitos o roles, asegúrese de registro de hello incluye Hola "iniciar sesión y leer el perfil de usuario" permiso de Azure AD (proporcionada de forma predeterminada)
3. Implementar una página de inicio de sesión-en/sesión-up en el cliente web de hello, después de hello [consentimiento del administrador](#admin-consent) guía se ha descrito anteriormente 
4. Una vez que la aplicación toohello de consentimiento del usuario de hello, hello servicio principal y consentimiento delegación se crean los vínculos en su inquilino y aplicación nativa de hello puede obtener tokens para hello API

Hola siguiente diagrama proporciona una introducción de consentimiento para una aplicación de varios nivel registrada en distintos inquilinos:

![Aplicación de varias parte de toomulti-nivel de consentimiento][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Revocación del consentimiento
Los usuarios y administradores pueden revocar el consentimiento tooyour aplicación en cualquier momento:

* Las aplicaciones de access tooindividual revoke de los usuarios mediante la eliminación de sus [aplicaciones de Panel de acceso] [ AAD-Access-Panel] lista.
* Los administradores de revocación el acceso tooapplications quitándolos de Azure AD utilizando la sección de administración de hello Azure AD de hello [portal de Azure][AZURE-portal].

Si un administrador consiente tooan aplicación para todos los usuarios en un inquilino, los usuarios no pueden revocar el acceso individualmente.  Solo el Administrador de hello puede revocar el acceso y solo para toda aplicación Hola.

### <a name="consent-and-protocol-support"></a>Compatibilidad con el consentimiento y los protocolos
Consentimiento se admite en Azure AD a través de hello OAuth, OpenID Connect, WS-Federation y protocolos SAML.  Hello protocolos SAML y WS-Federation no admiten hello `prompt=admin_consent` parámetro, por lo que solo es posible a través de OAuth y OpenID Connect de consentimiento del administrador.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Aplicaciones multiempresa y almacenamiento en caché de los tokens de acceso
Aplicaciones de varios inquilinos también pueden obtener toocall de tokens de acceso a las API que están protegidas por Azure AD.  Un error común al utilizar Hola biblioteca de autenticación de Active Directory (ADAL) con una aplicación de varios inquilinos, es tooinitially solicitud un token para un usuario con/Common, recibir una respuesta y solicitar un token posterior para ese mismo usuario también usa/Common.  Puesto que la respuesta de Hola de Azure AD procede de un inquilino, no/común, AAL almacena en memoria caché de token de hello como procedente de inquilino de Hola. Hola subsiguientes, llame a tooget demasiado común o un token de acceso de entrada de caché de Hola de errores de usuario de Hola y Hola usuario vuelve a estar toosign solicitada en.  tooavoid falta memoria caché de hello, asegúrese de que seguidamente para un usuario de la sesión ya iniciada se realizan llamadas extremo del inquilino de toohello.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, se habrá aprendido cómo toobuild una aplicación que puede iniciar sesión en un usuario de cualquier inquilino de Azure Active Directory. Después de habilitar el inicio de sesión único entre la aplicación y Azure Active Directory, también puede actualizar su tooaccess aplicación API expuestas por los recursos de Microsoft, como Office 365. Por lo que puede ofrecer una experiencia personalizada en su aplicación, por ejemplo, que muestra información contextual toohello a los usuarios, como su imagen de perfil o su próxima cita de calendario. toolearn más acerca de cómo realizar API llama tooAzure Active Directory y servicios de Office 365 como Exchange, SharePoint, OneDrive, OneNote, Planner, Excel y obtener más información, visitan: [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>Contenido relacionado
* [Ejemplos de aplicación multiinquilino][AAD-Samples-MT]
* [Directrices de personalización de marca para aplicaciones][AAD-App-Branding]
* [Guía del desarrollador de Azure AD][AAD-Dev-Guide]
* [Objetos Application y objetos ServicePrincipal][AAD-App-SP-Objects]
* [Integración de aplicaciones con Azure Active Directory][AAD-Integrating-Apps]
* [Información general de hello marco de consentimiento][AAD-Consent-Overview]
* [Ámbitos de permiso de la API Graph de Microsoft][MSFT-Graph-permision-scopes]
* [Ámbitos de permiso de la API Graph de Azure AD][AAD-Graph-Perm-Scopes]

Use Hola después de comentarios de tooprovide de sección de comentarios y nos ayudan a refinar y dar forma a nuestro contenido.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














