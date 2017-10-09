---
title: aaaCreate un grupo de usuarios de Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo toocreate un grupo en Azure Active Directory y agregue el grupo de miembros toohello"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Creación de un grupo y adición de miembros en Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Portal de Azure clásico](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Este artículo se explica cómo toocreate y rellenar un nuevo grupo en Azure Active Directory. Utilice una tarea de administración de grupo tooperform como la asignación de licencias o permisos tooa número de usuarios o dispositivos a la vez.

## <a name="how-do-i-create-a-group"></a>¿Cómo se crea un grupo?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![Apertura de Administración de usuarios](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. En hello **usuarios y grupos** hoja, seleccione **todos los grupos de**.

   ![Hoja de apertura Hola grupos](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. En hello **a los usuarios y grupos: todos los grupos de** hoja, seleccione hello **agregar** comando.

   ![Al seleccionar el comando Add Hola](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. En hello **grupo** hoja, agregue un nombre y una descripción para el grupo de Hola.
6. tooselect tooadd toohello grupo de miembros, seleccione **asignado** en hello **tipo de pertenencia** cuadro y, a continuación, seleccione **miembros**. Para obtener más información acerca de cómo toomanage Hola pertenencia de un grupo de forma dinámica, consulte [utilizando atributos toocreate reglas de pertenencia a grupos avanzadas](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Seleccionar miembros tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. En hello **miembros** hoja, seleccione uno o más usuarios o dispositivos grupo de toohello tooadd y seleccione hello **seleccione** situado en la parte inferior de Hola de hello hoja tooadd les toohello grupo. Hola **usuario** cuadro filtra Hola presentación de acuerdo con la parte de un nombre de usuario o dispositivo tooany de entrada de búsqueda de coincidencias. No se aceptan caracteres comodín en el cuadro.
8. Cuando termine de agregar el grupo de miembros toohello, seleccione **crear** en hello **grupo** hoja.    

   ![Creación de la confirmación de grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Consulta de los grupos existentes](active-directory-groups-view-azure-portal.md)
* [Administración de la configuración de un grupo](active-directory-groups-settings-azure-portal.md)
* [Administrar miembros de un grupo](active-directory-groups-members-azure-portal.md)
* [Administrar la pertenencia a grupos](active-directory-groups-membership-azure-portal.md)
* [Administrar reglas dinámicas de los usuarios de un grupo](active-directory-groups-dynamic-membership-azure-portal.md)
