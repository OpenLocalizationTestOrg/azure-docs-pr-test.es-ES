---
title: aaaHow tooAssign usuarios tooapplications | Documentos de Microsoft
description: "Comprender cómo los usuarios se asignen tooan aplicación en su inquilino"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>¿Cómo tooassign usuarios tooapplications

En este artículo le ayudarán a toounderstand cómo los usuarios se asignen tooan aplicación en su inquilino.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>¿Cómo los usuarios se asignen tooan aplicación en Azure AD?

Para un usuario se tooaccess una aplicación, debe estar asignados tooit de alguna manera. Asignación puede realizarla un administrador, un delegado de negocio o a veces, Hola usuario por sí mismos. A continuación describe las formas de hello los usuarios pueden obtener asignar tooapplications:

1.  Un administrador [asigna un usuario](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello aplicación directamente

2.  Un administrador [asigna un grupo de](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) ese usuario hello es un miembro de la aplicación toohello, incluidos:

  * Un grupo que se ha sincronizado de forma local

  * Un grupo de seguridad estático creado en la nube de Hola

  * A [grupo de seguridad dinámica](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) creado en la nube de Hola

  * Un grupo de Office 365 creado en la nube de Hola

  * Hola [todos los usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupo

3.  Un administrador habilita [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd de usuario una aplicación usando Hola [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Agregar aplicación** característica **sin la aprobación de negocios**

4.  Un administrador habilita [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd de usuario una aplicación usando Hola [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Agregar aplicación** característica, pero solo w **i-ésimo autorización previa de un conjunto seleccionado de aprobadores de negocios**

5.  Un administrador habilita [administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin un grupo que se asigna demasiado una aplicación de usuario**sin la aprobación de negocios**

6.  Un administrador habilita [administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin de usuario un grupo que se asigna una aplicación a, pero solo **con la aprobación previa de un conjunto seleccionado de aprobadores de negocios**

7.  Un administrador asigna un usuario de tooa de licencia directamente para una primera aplicación de usuario, como [Microsoft Office 365](http://products.office.com/)

8.  Un administrador asigna un grupo de tooa de licencias que Hola usuario es miembro de tooa primera aplicación de usuario, como [Microsoft Office 365](http://products.office.com/)

9.  Un [administrador consiente aplicación tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe utilizado por todos los usuarios y, a continuación, un usuario inicia sesión en la aplicación de toohello

10. Un usuario [da su consentimiento tooan aplicación](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) por sí mismos, debe iniciar sesión en la aplicación de toohello

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)
