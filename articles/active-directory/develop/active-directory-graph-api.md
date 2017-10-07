---
title: aaaAzure Active Directory Graph API | Documentos de Microsoft
description: "Una guía de introducción y tutorial rápido para hello API Graph que permite mediante programación a tooAzure AD a través de extremos de la API de REST."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>API Graph de Azure Active Directory
> [!IMPORTANT]
> Se recomienda encarecidamente que utilice [Microsoft Graph](https://graph.microsoft.io/) en lugar de Azure AD Graph API tooaccess recursos de Active Directory. Nuestros esfuerzos de desarrollo ahora se centran en Microsoft Graph y no están previstas realizar mejoras adicionales para la API de Azure AD Graph. Hay un número muy limitado de escenarios para los que Azure AD Graph API todavía podría ser adecuado; Para obtener más información, vea hello [Microsoft Graph o hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) entrada de blog en hello centro de desarrollo de Office.
> 
> 

Hola API Graph de Azure Active Directory proporciona acceso mediante programación tooAzure AD a través de extremos de API de REST. Las aplicaciones pueden usar Hola API Graph tooperform crear, leer, actualizar y eliminar operaciones (CRUD) en objetos y datos de directorio. Por ejemplo, hello API Graph admite hello las siguientes operaciones comunes para un objeto de usuario:

* Crear un usuario nuevo en un directorio
* Obtener las propiedades detalladas de un usuario, como sus grupos
* Actualizar las propiedades de un usuario, como su ubicación y número de teléfono, o cambiar su contraseña
* Consultar la pertenencia a grupos de un usuario para el acceso basado en roles
* Deshabilitar la cuenta de un usuario o eliminarla por completo

En los objetos de toouser de suma, puede realizar las mismas operaciones en otros objetos como los grupos y las aplicaciones. toocall Hola API Graph en un directorio, la aplicación hello debe estar registrado con Azure AD y puede configura toohello de tooallow obtener acceso al directorio. Esto se logra normalmente a través de un flujo de consentimiento de usuario o administrador.

toobegin utilizando hello Azure Active Directory Graph API, vea hello [Guía de inicio rápido de API de Graph](active-directory-graph-api-quickstart.md), o vista hello [documentación de referencia de API Graph interactiva](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Características
Hola API Graph proporciona Hola siguientes características:

* **Los extremos de la API de REST**: Hola API Graph es un servicio RESTful compuesto de extremos que se tiene acceso mediante solicitudes HTTP estándares. Hola API Graph admite tipos de contenido XML o Javascript Object Notation (JSON) para las solicitudes y respuestas. Para obtener más información, consulte [Referencia de la API Graph de REST de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Autenticación con Azure AD**: cada toohello de solicitud API Graph deben autenticarse mediante la anexión de un símbolo (token) para la Web de JSON (JWT) en el encabezado de autorización de saludo de solicitud de saludo. Este token se adquiere realizando el extremo de token de un tooAzure de solicitud de AD y proporcionar las credenciales válidas. Puede usar Hola flujo de credenciales de cliente de OAuth 2.0 o tooacquire de flujo de concesión de código de autorización de hello un gráfico de token toocall Hola. Para obtener más información, vea [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Autorización basada en roles (RBAC)**: grupos de seguridad son usado tooperform RBAC en hello API Graph. Por ejemplo, si desea toodetermine si un usuario tiene acceso tooa determinado recurso, Hola aplicación puede llamar a hello [comprobar pertenencia a grupos (transitiva)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) operación, que devuelve true o false.
* **Consulta diferencial**: si desea toocheck para cambios en un directorio entre dos períodos de tiempo sin necesidad de toomake frecuentan consultas toohello API Graph, puede realizar una solicitud de consulta diferencial. Este tipo de solicitud devolverá solo los cambios Hola realizados entre una solicitud de consulta diferencial anterior hello y solicitud de hello actual. Para más información, vea [Consulta diferencial de la API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Extensiones de directorio**: si está desarrollando una aplicación que necesite tooread o escribir propiedades únicas para los objetos de directorio, puede registrar y usar valores de extensión mediante Hola API Graph. Por ejemplo, si la aplicación requiere una propiedad de identificador de Skype para cada usuario, puede registrar Hola nueva propiedad en el directorio de Hola y estará disponible en cada objeto de usuario. Para obtener más información, consulte [Extensiones de esquema de directorio de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Protegida por ámbitos de permiso**: API de AAD Graph expone los ámbitos de permiso que permiten proteger/consentido acceder a los datos de tooAAD y admiten una variedad de tipos de aplicación de cliente, incluidos:
  
  * aquellos con una interfaz de usuario que reciben delegado acceso a toodata a través de autorización desde Hola usuario con sesión iniciada (delegado)
  * Aquellos que usan el control de acceso basado en roles definido por las aplicaciones, como clientes de servicio o demonio (roles de aplicación).
    
    Los delegados y ámbitos de permiso de rol de aplicación representan un privilegio expuesto por hello API Graph y se pueden solicitar por aplicaciones cliente a través de los permisos de registro de aplicación [características en el portal de Azure hello](https://portal.azure.com). Los clientes pueden comprobar los ámbitos de permiso de hello concedido toothem mediante la inspección de notificación de ámbito ("scp") de hello recibido en el token de acceso de Hola para permisos delegados y Hola funciones ("") de notificación para permisos de rol de aplicación. Obtenga más información sobre los [ámbitos de permiso de API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Escenarios
Hola API Graph permite muchos escenarios de aplicación. Hola los escenarios siguientes es hello más comunes:

* **Aplicación de línea de negocio (un solo inquilino)**: en este escenario, un desarrollador empresarial trabaja para una organización que tiene una suscripción a Office 365. Hola desarrollador compila una aplicación web que interactúa con las tareas de tooperform de Azure AD como asignar una licencia tooa un usuario. Esta tarea requiere acceso toohello API de Graph, por lo que el desarrollador de hello registra la aplicación de un solo inquilino de hello en Azure AD y configura permisos lectura / escritura para hello API Graph. Hola, a continuación, la aplicación es toouse configurado sus propias credenciales o los de hello tooacquire de inicio de sesión de usuario actualmente un token toocall Hola API Graph.
* **Software como aplicación de servicio (multiempresa)**: en este escenario, un fabricante de software independiente (ISV) desarrolla una aplicación web multiempresa hospedada que ofrece características de administración de usuarios para otras organizaciones que usan Azure AD. Estas características requieren acceso toodirectory objetos, y así aplicación hello debe toocall Hola API Graph. desarrollador de Hello registra la aplicación hello en Azure AD, configura toorequire lectura y permisos de escritura para hello API Graph y, a continuación, habilita el acceso externo para que otras organizaciones pueden permitir la aplicación de hello toouse en su directorio. Cuando un usuario de otra organización autentica la aplicación de toohello para hello primera vez, aparecerá un cuadro de diálogo de consentimiento con permisos de Hola Hola aplicación está solicitando.  Concesión de consentimiento, a continuación, proporcionará la aplicación hello solicita los permisos toohello API Graph en el directorio del usuario de Hola. Para obtener más información sobre el marco de consentimiento de hello, consulte [información general del marco de consentimiento de hello](active-directory-integrating-applications.md).

## <a name="see-also"></a>Otras referencias
[Inicio rápido para la API de Azure AD Graph](active-directory-graph-api-quickstart.md)

[Documentación de AD Graph de REST](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Guía del desarrollador de Azure Active Directory](active-directory-developers-guide.md)

