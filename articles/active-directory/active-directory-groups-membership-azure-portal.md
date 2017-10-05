---
title: "Administración de los grupos a los que pertenece un grupo en Azure Active Directory | Microsoft Docs"
description: "Los grupos pueden contener otros grupos en Azure Active Directory. Aquí se muestra cómo administrar las pertenencias a grupos."
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Administración de los grupos a los que pertenece un grupo en el inquilino de Azure Active Directory
Los grupos pueden contener otros grupos en Azure Active Directory. Aquí se muestra cómo administrar las pertenencias a grupos.

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a>¿Cómo puedo encontrar los grupos de los que es miembro mi grupo?
1. Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.
2. Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.

   ![Apertura de Administración de usuarios](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. En la hoja **Usuarios y grupos**, seleccione **Todos los grupos**.

   ![Apertura de la hoja Grupos](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. En la hoja **Usuarios y grupos - Todos los grupos** seleccione un grupo.
5. En la hoja **Grupo - *nombre del grupo*** seleccione **Pertenencia a grupos**.

   ![Apertura de la hoja Pertenencia a grupos](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. Para agregar un grupo como miembro de otro grupo, en la hoja **Grupo - Pertenencia a grupos** seleccione el comando **Agregar** comando.
7. Seleccione un grupo de la hoja **Seleccionar grupo** y, después, haga clic en el botón **Seleccionar** situado en la parte inferior de dicha hoja. Solo se pueden agregar grupos a otros grupos de uno en uno. El cuadro **Usuario** filtra la visualización en función de si coincide lo que ha escrito con cualquier parte del nombre de un usuario o dispositivo. No se aceptan caracteres comodín en el cuadro.

   ![Adición de una pertenencia a grupos](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. Para quitar un grupo como miembro de otro grupo, en la hoja **Grupo - Pertenencia a grupos** , seleccione uno.
9. En la hoja ***nombreDelGrupo***, seleccione el comando **Quitar** y confirme la elección en el símbolo del sistema.

   ![Comando de eliminación de pertenencia a grupo](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Cuando termine de cambiar las pertenencias a grupos de su grupo, seleccione **Guardar**.

## <a name="additional-information"></a>Información adicional
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Ver los grupos existentes](active-directory-groups-view-azure-portal.md)
* [Crear un nuevo grupo y agregar miembros](active-directory-groups-create-azure-portal.md)
* [Administrar la configuración de un grupo](active-directory-groups-settings-azure-portal.md)
* [Administrar miembros de un grupo](active-directory-groups-members-azure-portal.md)
* [Administrar reglas dinámicas de los usuarios de un grupo](active-directory-groups-dynamic-membership-azure-portal.md)
