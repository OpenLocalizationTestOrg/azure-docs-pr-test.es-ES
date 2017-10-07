---
title: Hola aaaUnderstanding Azure Active Directory Application Manifest | Documentos de Microsoft
description: "Cobertura detallada del manifiesto de aplicación de Azure Active Directory hello, que representa la configuración de identidad de una aplicación en un inquilino de Azure AD y es la autorización de OAuth de toofacilitate usado, experiencia de consentimiento y mucho más."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Descripción de manifiesto de aplicación de Azure Active Directory Hola
Las aplicaciones que se integran con Azure Active Directory (AD) deben estar registradas con un inquilino de Azure AD, proporcionando una configuración persistente de identidad para la aplicación hello. Esta configuración se consulta en tiempo de ejecución, que permite escenarios que permiten a una aplicación toooutsource y agente de autenticación/autorización a través de Azure AD. Para obtener más información sobre el modelo de aplicación hello Azure AD, vea hello [agregar, actualizar y quitar una aplicación] [ ADD-UPD-RMV-APP] artículo.

## <a name="updating-an-applications-identity-configuration"></a>Actualización de la configuración de identidad de una aplicación
Hay realmente varias opciones disponibles para actualizar las propiedades de hello en la configuración de identidad de una aplicación, que varían en las capacidades y grados de dificultad, incluidos Hola siguientes:

* Hola ** [portal de Azure] [ AZURE-PORTAL] interfaz de usuario Web** permite propiedades más comunes de hello tooupdate de una aplicación. Esto es más rápida de hello y menos forma propensas a error de actualización de propiedades de la aplicación, pero no proporcionan propiedades de tooall de acceso completa, como Hola dos métodos.
* Para escenarios más avanzados en los que tenga propiedades tooupdate que no se exponen en hello portal de Azure clásico, puede modificar hello **manifiesto de aplicación**. Esto es Hola descrito en este artículo y se explica con más detalle a partir de la sección siguiente Hola.
* También es posible demasiado**escribir una aplicación que usa hello [API Graph] [ GRAPH-API] ** tooupdate Hola a la aplicación, lo que requiere la mayoría del trabajo. Sin embargo, esto puede ser una opción atractiva si está escribiendo un software de administración, o si necesita tooupdate propiedades de la aplicación de forma regular de forma automática.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Uso de tooupdate de manifiesto de aplicación Hola configuración de identidad de una aplicación
A través de hello [portal de Azure][AZURE-PORTAL], puede administrar configuración de la identidad de la aplicación al actualizar el manifiesto de aplicación Hola mediante el editor de manifiestos de hello en línea. También puede descargar y cargar el manifiesto de aplicación Hola como un archivo JSON. Ningún archivo real se almacena en el directorio de Hola. manifiesto de aplicación Hello es simplemente una operación GET de HTTP en la entidad de la aplicación hello Azure AD Graph API y carga hello es una operación HTTP PATCH en la entidad de aplicación Hola.

Como resultado, en formato de orden toounderstand hello y las propiedades de manifiesto de aplicación Hola, deberá tooreference Hola API Graph [entidad aplicaciones] [ APPLICATION-ENTITY] documentación. Ejemplos de actualizaciones que se pueden realizar mediante la carga del manifiesto de aplicación:

* **Declarar los ámbitos de permiso (oauth2Permissions)** que expone la API web. Vea Hola "Las API Web de divulgación tooOther aplicaciones" tema en [integración de aplicaciones con Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD] para obtener información sobre cómo implementar la suplantación de usuario con hello ámbito de permisos delegados de oauth2Permissions. Como se mencionó anteriormente, propiedades de la entidad de aplicación se documentan en hello API Graph [entidad y el tipo complejo] [ APPLICATION-ENTITY] artículo de referencia, incluyendo hello oauth2Permissions propiedad que es un colección de tipo [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Declarar los roles de aplicación (appRoles) que expone la aplicación**. propiedad de la entidad de la aplicación appRoles Hello es una colección de tipo [AppRole][APPLICATION-ENTITY-APP-ROLE]. Vea hello [control de acceso en aplicaciones de nube con Azure AD basado en roles] [ RBAC-CLOUD-APPS-AZUREAD] artículo para obtener un ejemplo de implementación.
* **Declarar cliente conocidas aplicaciones (knownClientApplications)**, que le permiten consentimiento de hello toologically lazo de hello especificado cliente aplicaciones toohello/API web de recursos.
* **Solicitud de notificación de las pertenencias a grupos de Azure AD tooissue** para hello firmado de usuario (groupMembershipClaims).  También puede ser tooissue configurado notificaciones acerca de pertenencia a roles de directorio del usuario de Hola. Vea hello [autorización en aplicaciones de nube mediante grupos de AD] [ AAD-GROUPS-FOR-AUTHORIZATION] artículo para obtener un ejemplo de implementación.
* **Permitir la concesión de OAuth 2.0 implícita de toosupport de aplicación** flujos (oauth2AllowImplicitFlow). Este tipo de flujo de concesión se utiliza con páginas web JavaScript integradas o aplicaciones de página única (SPA). Para obtener más información sobre concesión de autorización implícita de hello, consulte [flujo en Azure Active Directory de concesión de hello descripción implícita OAuth2][IMPLICIT-GRANT].
* **Habilitar el uso de X509 certificados de clave secreta de hello** (keyCredentials). Vea hello [crear aplicaciones de servicio y el demonio en Office 365] [ O365-SERVICE-DAEMON-APPS] y [tooauth de guía del desarrollador con la API del Administrador de recursos de Azure] [ DEV-GUIDE-TO-AUTH-WITH-ARM] artículos para obtener ejemplos de implementación.
* **Agregar un nuevo URI de id. de aplicación ** para su aplicación (identifierURIs[]). URI de Id. de aplicación se pueden usar toouniquely identificar una aplicación dentro de su inquilino de Azure AD (o a través de varios inquilinos de Azure AD, para escenarios de varios inquilinos cuando se califica a través de dominio personalizado comprobado). Se utilizan cuando se solicita la aplicación de recursos de tooa de permisos, o adquirir un token de acceso para una aplicación de recursos. Al actualizar este elemento, hello misma actualización estará colección de [] servicePrincipalNames toohello correspondiente entidad de servicio, que se encuentra en el inquilino de inicio de la aplicación hello.

Hello manifiesto de aplicación también proporciona una buena manera tootrack Hola estado de su registro de la aplicación. Porque está disponible en formato JSON, se puede comprobar la representación en forma de archivo hello en el control de código fuente, junto con el código fuente de la aplicación.

## <a name="step-by-step-example"></a>Ejemplo paso a paso
Ahora permite recorrer Hola pasos necesarios tooupdate configuración de identidad de la aplicación a través de manifiesto de aplicación Hola. Nos centraremos en uno de hello anteriores ejemplos, que muestra cómo toodeclare un nuevo permiso en el ámbito en una aplicación de recursos:

1. Inicie sesión en toohello [portal de Azure][AZURE-PORTAL].
2. Después de que se ha autenticado, elija al inquilino de Azure AD seleccionándola de Hola superior derecho de la página de Hola.
3. Seleccione **Azure Active Directory** extensión de hello encendidos panel de navegación y haga clic en **registros de aplicación**.
4. Encontrar la aplicación de Hola que desee tooupdate en la lista de Hola y haga clic en él.
5. En la página de aplicación Hola, haga clic en **manifiesto** editor de manifiestos de tooopen hello en línea. 
6. Manifiesto de hello mediante este editor, puede editar directamente. Tenga en cuenta esa manifiesto Hola sigue el esquema de Hola para hello [entidad aplicaciones] [ APPLICATION-ENTITY] tal y como se ha mencionado anteriormente: por ejemplo, suponiendo que queremos tooimplement/exponen un permiso nuevo denominado "Employees.Read.All" en nuestra aplicación de recursos (API), que simplemente agregaría una colección oauth2Permissions de toohello nuevo/segundo elemento, Internet Explorer:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    entrada de Hello debe ser único y, por lo tanto, debe generar un nuevo globalmente único identificador (GUID) para hello `"id"` propiedad. En este caso, porque hemos especificado `"type": "User"`, este permiso puede ser consentido tooby cualquier autenticar la cuenta hello en qué Hola se registra la aplicación de recursos/API de inquilino de Azure AD. Este tooaccess concede Hola cliente aplicación permiso en nombre de la cuenta de hello. se utilizan cadenas de nombre de descripción y la presentación de Hola durante el consentimiento y para su presentación en hello portal de Azure.
6. Cuando haya terminado de actualizar el manifiesto de hello, haga clic en **guardar** toosave manifiesto de Hola.  
   
Ahora que hello manifiesto se guarda, puede conceder a un cliente registrado aplicación acceso toohello nuevo permiso que hemos agregado anteriormente. Este tiempo que puede usar Hola UI de Web del portal de Azure en lugar de modificar el manifiesto de la aplicación de cliente de hello:  

1. En primer lugar vaya toohello **configuración** hoja de hello toowhich de aplicación de cliente que se va tooadd acceso toohello nueva API, haga clic en **permisos necesarios** y elija **seleccionar una API** .
2. A continuación, aparecerá con la lista de Hola de recursos registrado aplicaciones (API) de inquilino de Hola. Haga clic en tooselect de aplicación de recursos de hello, o nombre de cuadro de búsqueda de hello aplicación Hola Hola de tipo. Cuando haya encontrado la aplicación hello, haga clic en **seleccione**.  
3. Esto le llevará toohello **permisos Select** página, que mostrará la lista de Hola de aplicación y los permisos delegados disponibles para la aplicación de recursos de Hola. Seleccione Hola nuevo permiso en orden tooadd se toohello cliente solicitada por la lista de permisos. Este nuevo permiso se almacenarán en la configuración de identidad de la aplicación de cliente de hello, en la propiedad de colección "requiredResourceAccess" Hola.


Eso es todo. Ahora las aplicaciones se ejecutarán con su nueva configuración de identidad.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más detalles sobre la relación de hello entre objetos de aplicación y entidad de servicio de una aplicación, consulte [aplicación y objetos de entidad de servicio en Azure AD][AAD-APP-OBJECTS].
* Vea hello [Glosario de Azure AD para desarrolladores] [ AAD-DEVELOPER-GLOSSARY] para obtener definiciones de algunos de los conceptos de desarrollador de hello principales Azure Active Directory (AD).

Use la sección de comentarios de Hola siguiente tooprovide comentarios y nos ayudan a refinar y dar forma a nuestro contenido.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

