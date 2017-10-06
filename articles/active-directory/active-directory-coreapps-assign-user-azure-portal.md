---
title: "una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory aaaAssign | Documentos de Microsoft"
description: "¿Cómo tooselect una tooassign de aplicación de empresa una tooit de usuario o grupo en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory
Es fácil tooassign un usuario o un grupo tooyour las aplicaciones empresariales en Azure Active Directory (Azure AD). Debe tener la aplicación empresarial de hello permisos adecuados toomanage hello y debe ser administrador global para el directorio de Hola.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>¿Cómo se puede asignar acceso de usuario tooan aplicación de empresa?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba Azure Active Directory en el cuadro de texto de hello y, a continuación, seleccione **ENTRAR**.
3. En hello **Azure Active Directory - *directoryname***  hoja (es decir, hello Azure AD hoja para el directorio de hello administra), seleccione **aplicaciones empresariales**.

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. En hello **aplicaciones empresariales** hoja, seleccione **todas las aplicaciones**. Verá una lista de aplicaciones de hello que puede administrar.
5. En hello **aplicaciones empresariales - todas las aplicaciones** hoja, seleccione una aplicación.
6. En hello ***appname*** hoja (es decir, Hola hoja con nombre Hola de aplicación seleccionada de hello en el título de hello), seleccione **usuarios y grupos**.

    ![Selección de Hola a todos los comandos de las aplicaciones](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. En hello ***appname*** **-asignación de grupo de & usuario** hoja, seleccione hello **agregar** comando.
8. En hello **Agregar asignación** hoja, seleccione **usuarios y grupos**.

    ![Asignar una aplicación de usuario o grupo toohello](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. En hello **usuarios y grupos** hoja, seleccione uno o más usuarios o grupos de hello lista y, a continuación, seleccione hello **seleccione** situado en parte inferior de Hola de hoja de Hola.
10. En hello **Agregar asignación** hoja, seleccione **rol**. A continuación, en hello **Seleccionar rol** hoja, seleccione un toohello de tooapply rol seleccionado usuarios o grupos y, a continuación, seleccione hello **Aceptar** situado en parte inferior de Hola de hoja de Hola.
11. En hello **Agregar asignación** hoja, seleccione hello **asignar** situado en parte inferior de Hola de hoja de Hola. Hola asignados a los usuarios o grupos tendrán permisos de hello definidos por el rol seleccionado de Hola para esta aplicación de empresa.

## <a name="next-steps"></a>Pasos siguientes
* [Ver todos mis grupos](active-directory-groups-view-azure-portal.md)
* [Eliminación de asignaciones de usuario o grupo de una aplicación empresarial](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial](active-directory-coreapps-disable-app-azure-portal.md)
* [Cambiar el nombre de Hola o el logotipo de una aplicación de empresa](active-directory-coreapps-change-app-logo-user-azure-portal.md)
