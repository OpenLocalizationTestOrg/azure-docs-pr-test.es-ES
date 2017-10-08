---
title: aaaHow toogive acceso tooPrivileged Identity Management - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd roles toousers con Hola extensión de Azure Active Directory Privileged Identity Management para que puedan administrar PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Lo que proporciona acceso toomanage AD Privileged Identity Management de Azure
Administrador global de Hello, que permite a Azure AD Privileged Identity Management (PIM) de una organización automáticamente obtener las asignaciones de roles y tener acceso a tooPIM. Nadie más obtiene acceso de escritura de forma predeterminada, ni siquiera otros administradores globales. Otros administradores globales, los administradores de seguridad y los lectores de seguridad tienen acceso de solo lectura tooAzure PIM AD. toogive acceso tooPIM, Hola primer usuario puede asignar a otros usuarios toohello **Administrador de roles con privilegios de** rol. Esta asignación se debe realizar desde dentro de PIM y no se puede cambiar mediante PowerShell u otros portales.

> [!NOTE]
> La administración de PIM de Azure AD requiere Azure MFA. Dado que las cuentas de Microsoft no se pueden registrar en Azure MFA, un usuario que inicia sesión con una cuenta de Microsoft no puede tener acceso a PIM de Azure AD.
> 
> 

Asegúrese de que siempre haya al menos dos usuarios en un rol de administrador de roles con privilegios, por si se diera el caso de que a un usuario se le impida el acceso o su cuenta se haya eliminado.

## <a name="give-another-user-access-toomanage-pim"></a>Proporcionar a otro usuario acceso toomanage PIM
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y seleccione hello **Azure AD Privileged Identity Management** aplicación en el panel de Hola.
2. Seleccione **Administrar roles con privilegios** > **Administrador de rol con privilegios** > **Agregar**.
   
    ![Agregar administradores de roles con privilegios: captura de pantalla][1]
3. En la hoja de hello agregar usuarios administrados, paso 1 ya está completando. Seleccione paso 2, **Seleccionar usuarios** y búsqueda para el usuario de hello desea tooadd.
   
    ![Seleccionar usuarios: captura de pantalla][2]
4. Seleccione el usuario de hello en los resultados de búsqueda de Hola y haga clic en **realiza**.
5. Haga clic en **Aceptar** toosave la selección. usuario de Hola que ha seleccionado se mostrará en lista de Hola de administradores de roles con privilegios.
   
   * Cada vez que se asigna un nuevo toosomeone de rol, se configuran automáticamente como rol de hello tooactivate elegibles. Si desea que toomake permanente en función de hello, haga clic en usuario de hello en lista de Hola. Seleccione **realizar perm** en el menú de información de usuario de Hola.
6. Enviar un vínculo al usuario de hello demasiado[Introducción a Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Eliminación de los derechos de acceso de otro usuario para administrar PIM
Antes de quitar un usuario del rol de administrador de roles con privilegios de hello, asegúrese siempre de seguirá habiendo dos usuarios asignados tooit.

1. En el panel PIM de hello, haga clic en el rol de Hola **Administrador de roles con privilegios de**.  se mostrará la lista de Hola de usuarios actualmente en ese rol.
2. Haga clic en usuario de hello en la lista de usuarios de Hola.
3. Haga clic en **Quitar**.  Aparecerá un mensaje de confirmación.
4. Haga clic en **Sí** tooremove usuario Hola rol Hola.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
