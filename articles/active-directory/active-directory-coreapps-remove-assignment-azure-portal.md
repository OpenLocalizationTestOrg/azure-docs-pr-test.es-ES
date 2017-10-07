---
title: "aaaRemove una asignación de usuario o grupo de una aplicación de empresa en Azure Active Directory | Documentos de Microsoft"
description: "Cómo tooremove Hola tener acceso a la asignación de un usuario o grupo de una aplicación de empresa en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Eliminación de asignaciones de usuario o grupo de una aplicación empresarial en Azure Active Directory
Es fácil tooremove un usuario o un grupo se asignen tooone de acceso de las aplicaciones empresariales en Azure Active Directory (Azure AD). Debe tener la aplicación empresarial de hello permisos adecuados toomanage hello y debe ser administrador global para el directorio de Hola.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>¿Cómo se puede eliminar una asignación de grupo o usuario?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.
3. En hello **Azure Active Directory - *directoryname***  hoja (es decir, hello Azure AD hoja para el directorio de hello administra), seleccione **aplicaciones empresariales**.

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. En hello **aplicaciones empresariales** hoja, seleccione **todas las aplicaciones**. Verá una lista de aplicaciones de hello que puede administrar.
5. En hello **aplicaciones empresariales - todas las aplicaciones** hoja, seleccione una aplicación.
6. En hello ***appname*** hoja (es decir, Hola hoja con nombre Hola de aplicación seleccionada de hello en el título de hello), seleccione **usuarios y grupos**.

    ![Selección de usuarios o grupos](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. En hello ***appname*** **-asignación de grupo de & usuario** hoja, seleccione uno de varios usuarios o grupos y, a continuación, seleccione hello **quitar** comando. Confirme su decisión en el símbolo del sistema de Hola.

    ![Al seleccionar el comando Remove de Hola](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Pasos siguientes
* [Ver todos mis grupos](active-directory-groups-view-azure-portal.md)
* [Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)
* [Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial](active-directory-coreapps-disable-app-azure-portal.md)
* [Cambiar el nombre de Hola o el logotipo de una aplicación de empresa](active-directory-coreapps-change-app-logo-user-azure-portal.md)
