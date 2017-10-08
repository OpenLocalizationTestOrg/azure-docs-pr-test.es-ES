---
title: "aaaDynamic grupos y la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "La colaboración B2B de Active Directory de Azure puede utilizarse con grupos dinámicos de Azure AD"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Grupos dinámicos y colaboración B2B de Azure Active Directory

## <a name="what-are-dynamic-groups"></a>¿Qué son los grupos dinámicos?
Configuración dinámica de pertenencia a grupos de seguridad de Azure Active Directory (Azure AD) está disponible en [Hola portal de Azure](https://portal.azure.com). Los administradores pueden configurar reglas de grupos de toopopulate que se crean en Azure Active Directory en función de atributos de usuario (por ejemplo, userType, departamento o país). Los miembros se pueden agregar automáticamente tooor quita de un grupo de seguridad en función de sus atributos. Estos grupos pueden proporcionar acceso a recursos tooapplications o en la nube (los sitios de SharePoint, documentos) y tooassign licencias toomembers. Obtenga más información sobre los grupos dinámicos en [Grupos dedicados en Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

Hola adecuado [P1 de Azure AD Premium o P2 con licencias](https://azure.microsoft.com/pricing/details/active-directory/) es grupos dinámicos necesarios toocreate y uso. Obtenga más información en el artículo de hello [crear reglas basadas en atributos de pertenencia dinámica a grupos en Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>¿Qué grupos dinámicos integrados de hello?
Hola **todos los usuarios** grupo dinámico permite toocreate de administradores de inquilinos un grupo que contiene todos los usuarios de inquilinos de hello con un solo clic. De forma predeterminada, Hola **todos los usuarios** grupo incluye a todos los usuarios de directorio de hello, incluidos los miembros y los invitados.
En el portal de administración de Azure Active Directory nuevo hello, puede elegir hello tooenable **todos los usuarios** grupo Hola ver configuración de grupo.

![Grupos integrados](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>La protección de Hola a todos los grupos de usuarios dinámica
De forma predeterminada, Hola **todos los usuarios** grupo contiene los usuarios de colaboración (invitado) de B2B. Puede proteger aún más su **todos los usuarios** grupo mediante el uso de un usuario de invitado de tooremove de regla. Hello en la ilustración siguiente se muestra hello **todos los usuarios** grupo Modificar tooexclude invitados.

![Habilitación de todos los grupos de usuarios](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Es posible que también resulte útil toocreate un nuevo grupo dinámico que contiene solo los usuarios invitados, para que pueda aplicar directivas (por ejemplo, las directivas de acceso condicional de Azure AD) toothem.
Este el aspecto que tendría ese grupo:

![Exclusión de usuarios invitados](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propiedades de usuario de la colaboración B2B](active-directory-b2b-user-properties.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegación de las invitaciones de colaboración B2B](active-directory-b2b-delegate-invitations.md)
* [Código de colaboración B2B y ejemplos de PowerShell](active-directory-b2b-code-samples.md)
* [Configuración de aplicaciones de SaaS para la colaboración B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Asignación de notificaciones de usuario de colaboración B2B](active-directory-b2b-claims-mapping.md)
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)
