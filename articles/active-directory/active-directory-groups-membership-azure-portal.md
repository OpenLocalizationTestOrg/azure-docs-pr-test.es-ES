---
title: grupos de hello aaaManage su grupo pertenece tooin Azure Active Directory | Documentos de Microsoft
description: "Los grupos pueden contener otros grupos en Azure Active Directory. Le mostramos cómo toomanage esas pertenencias."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Administrar grupos de toowhich que pertenece un grupo en el inquilino de Azure Active Directory
Los grupos pueden contener otros grupos en Azure Active Directory. Le mostramos cómo toomanage esas pertenencias.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>¿Cómo se puede encontrar grupos de hello de que mi grupo es un miembro?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![Apertura de Administración de usuarios](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. En hello **usuarios y grupos** hoja, seleccione **todos los grupos de**.

   ![Hoja de apertura Hola grupos](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. En hello **a los usuarios y grupos: todos los grupos de** hoja, seleccione un grupo.
5. En hello **grupo - *groupname***  hoja, seleccione **las pertenencias a grupos**.

   ![Hoja de pertenencia a grupo de apertura Hola](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd el grupo como miembro de otro grupo, en hello **de grupo: las pertenencias a grupos** hoja, seleccione hello **agregar** comando.
7. Seleccione un grupo de hello **Seleccionar grupo** hoja y, a continuación, seleccione hello **seleccione** situado en parte inferior de Hola de hoja de Hola. Puede agregar el grupo de una tooonly a la vez. Hola **usuario** cuadro filtra Hola presentación de acuerdo con la parte de un nombre de usuario o dispositivo tooany de entrada de búsqueda de coincidencias. No se aceptan caracteres comodín en el cuadro.

   ![Adición de una pertenencia a grupos](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove el grupo como miembro de otro grupo, en hello **de grupo: las pertenencias a grupos** hoja, seleccione un grupo.
9. En hello ***groupname*** hoja, seleccione hello **quitar** comando y confirme su elección en el símbolo del sistema de Hola.

   ![Comando de eliminación de pertenencia a grupo](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Cuando termine de cambiar las pertenencias a grupos de su grupo, seleccione **Guardar**.

## <a name="additional-information"></a>Información adicional
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Ver los grupos existentes](active-directory-groups-view-azure-portal.md)
* [Crear un nuevo grupo y agregar miembros](active-directory-groups-create-azure-portal.md)
* [Administrar la configuración de un grupo](active-directory-groups-settings-azure-portal.md)
* [Administrar miembros de un grupo](active-directory-groups-members-azure-portal.md)
* [Administrar reglas dinámicas de los usuarios de un grupo](active-directory-groups-dynamic-membership-azure-portal.md)
