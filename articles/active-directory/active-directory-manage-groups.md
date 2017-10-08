---
title: aaaUse grupos toomanage acceso tooresources en Azure Active Directory | Documentos de Microsoft
description: "Cómo tener acceso a grupos de toouse de usuario de Azure Active Directory toomanage tooon locales y aplicaciones en la nube y recursos."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Administrar acceso tooresources con grupos de Active Directory de Azure
Azure Active Directory (Azure AD) es una solución de administración integral de identidades y acceso que ofrece un potente conjunto de capacidades toomanage acceso tooon locales y aplicaciones en la nube y recursos, incluidos los servicios en línea de Microsoft como Office 365 y una gran variedad de aplicaciones de SaaS que no sean de Microsoft. Este artículo proporciona información general, pero si desea que toostart mediante Azure AD se agrupa ahora mismo, siga las instrucciones de hello en [administrar grupos de seguridad en Azure AD](active-directory-accessmanagement-manage-groups.md). Si desea que toosee cómo puede usar PowerShell toomanage grupos en Azure Active directory puede leer más información en [cmdlets de Azure Active Directory para la administración de grupo](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse Azure Active Directory, se necesita una cuenta de Azure. Si aún no tiene ninguna, puede [registrarse para obtener una cuenta de Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).
>
>

Dentro de Azure AD, una de las características principales de hello es Hola capacidad toomanage acceso tooresources. Estos recursos pueden formar parte del directorio de hello, como en caso de hello toomanage de objetos de permisos a través de roles en el directorio de Hola o recursos de directorio de toohello externo, como las aplicaciones de SaaS, servicios de Azure y los sitios de SharePoint o local recursos. Hay cuatro maneras de que un usuario puede asignarse como recurso de tooa de derechos de acceso:

1. Asignación directa

    Los usuarios pueden asignarse directamente tooa recursos propietario de Hola de ese recurso.
2. Pertenencia a grupos

    Un grupo se puede asignar tooa recursos por el propietario del recurso de hello y, al hacerlo, conceder a los miembros de Hola de ese recurso toohello de acceso de grupo. Pertenencia a grupo de hello, a continuación, puede administrarse por propietario Hola del grupo de Hola. De hecho, los delegados de propietario de recurso de Hola Hola permiso tooassign usuarios tootheir recursos toohello propietario del grupo de Hola.
3. Basado en reglas

    propietario del recurso de Hello puede usar un tooexpress de regla que los usuarios que deben asignarse acceso tooa recursos. resultado de Hello de regla de hello depende de los atributos de hello usados en esa regla y sus valores para usuarios específicos y de esta forma, el propietario del recurso de hello delega con efectividad hello toomanage derecho acceso tootheir recursos toohello origen de autoridad de Hola atributos que se utilizan en la regla de Hola. propietario del recurso de Hello todavía administra la propia regla hello y determina qué atributos y valores de proporcionan acceso tootheir recursos.
4. Autoridad externa

    recursos de Hello acceso tooa se derivan de un origen externo; Por ejemplo, un grupo que se sincroniza desde un origen autoritativo como un directorio local o una aplicación de SaaS como jornada laboral. propietario del recurso de Hello asigna recursos de hello grupo tooprovide acceso toohello y origen externo de hello administra a los miembros de hello del grupo de Hola.

   ![Información general del diagrama de administración del acceso](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Vea un vídeo que explica la administración del acceso
Puede ver un breve vídeo que explica más detalladamente este tema:

**Azure AD: Suscripción Introducción toodynamic para grupos**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>¿Cómo funciona la administración de acceso en Azure Active Directory?
En hello center de hello solución de administración de acceso de Azure AD es grupo de seguridad de Hola. El uso de un tooresources de acceso de toomanage de grupo de seguridad es un paradigma conocido, que permite que un recurso de manera flexible y fácil de entender tooprovide acceso tooa grupo Hola diseñada de usuarios. propietario del recurso de Hello (o el Administrador de hello del directorio de hello) puede asignar a un grupo tooprovide un determinados recursos de toohello derecho de acceso que poseen. los miembros de Hello del grupo de Hola se proporcionará acceso de Hola y propietario del recurso de hello puede delegar la lista de miembros de Hola Hola toomanage derecho de una persona, por ejemplo, un administrador de departamento o un administrador del departamento de soporte técnico de toosomeone de grupo.

![Diagrama de administración de acceso de Azure Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

propietario de Hola de un grupo puede hacer que ese grupo disponibles para las solicitudes de autoservicio. Si lo hace, un usuario final puede buscar y encontrar el grupo de Hola y realizar una solicitud toojoin, búsquedas eficazmente permisos tooaccess Hola de los recursos que se administran a través del grupo de Hola. propietario de Hello del grupo de hello puede definir el grupo de Hola para que las solicitudes de combinación se aprueban automáticamente o requieren la aprobación de propietario de hello del grupo de Hola. Cuando un usuario realiza una solicitud toojoin un grupo, solicitud de incorporación de Hola se reenvía toohello propietarios del grupo de Hola. Si uno de los propietarios de hello aprueba la solicitud de hello, se notifica al usuario que lo solicita de Hola y usuario de hello es toohello Unidos a un grupo. Si uno de los propietarios de hello rechaza la solicitud de hello, usuario solicitante Hola recibe una notificación, pero no unidos a un grupo de toohello.

## <a name="getting-started-with-access-management"></a>Introducción a administración de accesos
¿Se inició tooget listo? Pruebe algunas de las tareas básicas de Hola que puede realizar con grupos de Azure AD. Utilice estos tooprovide funciones especializadas access toodifferent grupos de personas para los distintos recursos de su organización. A continuación se incluye una lista de los primeros pasos básicos.

* [Crear una regla sencilla tooconfigure pertenencia dinámica a un grupo](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Uso de un grupo toomanage acceso tooSaaS las aplicaciones](active-directory-accessmanagement-group-saasapps.md)
* [Puesta a disposición de un grupo para el autoservicio del usuario final](active-directory-accessmanagement-self-service-group-management.md)
* [Sincronizar un tooAzure de grupo local mediante Azure AD Connect](active-directory-aadconnect.md)
* [Administración de propietarios de un grupo](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha comprendido conceptos básicos de Hola de administración de acceso, presentamos algunas capacidades avanzadas adicionales disponibles en Azure Active Directory para administrar recursos y las aplicaciones de access tooyour.

* [Uso de atributos toocreate reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Administración de grupos de seguridad en Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Configuración de grupos dedicados en Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Referencia de API Graph para grupos](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
