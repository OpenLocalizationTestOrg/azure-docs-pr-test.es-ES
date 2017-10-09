---
title: grupos de aaaDedicated en Active Directory de Azure | Documentos de Microsoft
description: "Información general sobre cómo funcionan los grupos específicos en Azure Active Directory y cómo se crean."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Grupos dedicados en Azure Active Directory
En Azure Active Directory (Azure AD), la característica de grupos dedicados Hola crea y rellena automáticamente la pertenencia a grupos de Azure AD predefinido. No se puede agregar los miembros de grupos dedicados o quiten con hello Azure clásico portal, cmdlets de Windows PowerShell, o mediante programación.

> [!NOTE]
> Los grupos dedicados requieren que se asigne una licencia de Azure AD Premium:
>
> * Administrador de Hola que administra la regla de hello en un grupo
> * todos los usuarios que están seleccionados de forma Hola regla toobe un miembro del grupo de Hola
>
>

**grupos de tooenable dedicado**

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, abra el directorio de su organización.
2. Seleccione hello **grupos** ficha y un grupo de hello, a continuación, abra desea tooedit.
3. Seleccione hello **configurar** ficha y, a continuación, establezca **habilitar grupos dedicados** demasiado**Sí**.

Una vez Hola cambiar habilitar grupos dedicados se establece demasiado**Sí**, también puede habilitar Hola directory tooautomatically crear grupo dedicado de todos los usuarios de Hola Hola establecer **habilitar "Todos los usuarios" grupo** cambiar demasiado**Sí**. También puede, a continuación, Editar nombre de Hola de este grupo dedicado escribiendo en hello **nombre para mostrar "Todos los usuarios" grupo** campo.

puede utilizarse el grupo de todos los usuarios de Hello tooassign Hola mismo permisos tooall Hola usuarios del directorio. Por ejemplo, puede conceder todos los usuarios en su tooa de acceso de directorio aplicación SaaS mediante la asignación de acceso para todos los usuarios grupo dedicado toothis aplicación Hola.

grupo de todos los usuarios de Hello dedicado incluye todos los usuarios en el directorio de hello, incluidos invitados y usuarios externos. Si necesita un grupo que excluye los usuarios externos, puede hacerlo mediante la creación de un grupo con una regla dinámica basada en atributos como siguiente hello:

                (user.userPrincipalName -notContains "#EXT#@")

Para un grupo que excluye a todos los invitados, use una regla como siguiente hello:

                (user.userType -ne "Guest")

toolearn acerca de cómo toocreate *avanzadas* (reglas que puede contener varias comparaciones) para la pertenencia dinámica a grupos, consulte [utilizando atributos toocreate reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
