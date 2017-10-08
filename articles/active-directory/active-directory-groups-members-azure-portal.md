---
title: miembros de hello aaaManage para un grupo en Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo tooadd o quitar usuarios y dispositivos de un grupo en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Administración de la pertenencia a grupos de los usuarios del inquilino de Azure Active Directory
Este artículo explica cómo toomanage Hola a los miembros de un grupo en Azure Active Directory (Azure AD).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>¿Cómo buscar a los miembros de Hola y administrarlos?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![Apertura de Administración de usuarios](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. En hello **usuarios y grupos** hoja, seleccione **todos los grupos de**.

   ![Hoja de apertura Hola grupos](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. En hello **a los usuarios y grupos: todos los grupos de** hoja, seleccione un grupo.
5. En hello **grupo - *groupname***  hoja, seleccione **miembros**.

   ![Hoja de los miembros de Hola de apertura](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. grupo de toohello miembros tooadd, en hello **grupo - miembros** hoja, seleccione **agregar miembros**.

   ![Comando Agregar miembros](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. En hello **miembros** hoja, seleccione uno o más usuarios o dispositivos grupo de toohello tooadd y seleccione hello **seleccione** situado en la parte inferior de Hola de hello hoja tooadd les toohello grupo. Hola **usuario** cuadro filtra Hola presentación de acuerdo con la parte de un nombre de usuario o dispositivo tooany de entrada de búsqueda de coincidencias. No se aceptan caracteres comodín en el cuadro.
8. tooremove miembros del grupo de hello, en hello **grupo - miembros** hoja, seleccione un miembro.
9. En hello ***membername*** hoja, seleccione hello **quitar** comando y confirme su elección en el símbolo del sistema de Hola.

   ![Comando Quitar miembros](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Cuando termine de modificar los miembros del grupo de hello, seleccione **guardar**.

## <a name="additional-information"></a>Información adicional
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Ver los grupos existentes](active-directory-groups-view-azure-portal.md)
* [Crear un nuevo grupo y agregar miembros](active-directory-groups-create-azure-portal.md)
* [Administrar la configuración de un grupo](active-directory-groups-settings-azure-portal.md)
* [Administrar la pertenencia a grupos](active-directory-groups-membership-azure-portal.md)
* [Administrar reglas dinámicas de los usuarios de un grupo](active-directory-groups-dynamic-membership-azure-portal.md)
