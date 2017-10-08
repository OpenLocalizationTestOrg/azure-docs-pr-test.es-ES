---
title: aaaHow tooactivate o desactivar un rol | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooactivate roles para privileged identidades con aplicaciones de Azure Privileged Identity Management de Hola."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>¿Cómo tooactivate o desactivar los roles en Azure AD Privileged Identity Management
Active Directory (AD) Privileged Identity Management de Azure simplifica cómo las empresas administran tooresources de acceso con privilegios en Azure AD y otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.  

Si realizaron aptas para un rol administrativo, que significa que puede activar ese rol cuando necesite acciones tooperform con privilegios. Por ejemplo, si administra de vez en cuando características de Office 365, los administradores de roles con privilegios de su organización puede que no le hayan asignado el rol de administrador global permanente, ya que ese rol afecta también a otros servicios. En su lugar, pueden asignarle roles de Azure AD como administrador de Exchange Online. Puede solicitar tooactivate ese rol cuando necesite sus privilegios y, a continuación, tendrá el control de administración para un período de tiempo predeterminado.

Este artículo es para que los administradores que necesitan tooactivate su rol en Azure AD Privileged Identity Management (PIM). Le guiará por hello pasos tooactivate un rol cuando se necesitan permisos de Hola y desactiva la función hello cuando haya terminado. Además, los administradores de roles con privilegios pueden solicitar aprobación tooactivate un rol (versión preliminar). Obtenga más información sobre [flujos de trabajo de aprobación de PIM](./privileged-identity-management/azure-ad-pim-approval-workflow.md) aquí.

## <a name="add-hello-privileged-identity-management-application"></a>Agregar aplicación de hello Privileged Identity Management
Usar la aplicación de Privileged Identity Management de hello Azure AD en hello [portal de Azure](https://portal.azure.com/) toorequest activación de un rol, incluso si se va a toooperate en otro portal o PowerShell. Si no tiene la aplicación de Azure AD Privileged Identity Management de hello en el portal de Azure, siga estas tooget pasos que se inició.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione el nombre de usuario en hello superior derecho de hello portal de Azure y directorio Hola seleccione donde tendrá estar en funcionamiento.
3. Seleccione **más servicios** y usar hello toosearch de cuadro de texto de filtro para **Azure AD Privileged Identity Management**.
4. Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**. Hola aplicación Privileged Identity Management se abre.

## <a name="activate-a-role"></a>Activación de un rol
Cuando necesite tootake en un rol, puede solicitar la activación seleccionando hello **Roles Mis** opción de navegación en la aplicación de Privileged Identity Management de hello Azure AD de la columna de navegación izquierda.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y el icono de Privileged Identity Management seleccione hello Azure AD.
2. Seleccione **My Roles** (Mis roles). Aparecerá una lista de sus roles válidos asignados en hello agrupación al principio de Hola de página de Hola.
3. Seleccione un rol tooactivate.
4. Seleccione **Activar**. Hola **solicitar la activación de rol** aparece hoja.
5. Algunos roles requieren la autenticación multifactor (MFA) para poder activar el rol de Hola. Solo tiene tooauthenticate una vez por sesión.
   
    ![Comprobación con MFA antes de la activación del rol: captura de pantalla][2]
6. Escriba el motivo de hello para la solicitud de activación de hello en el campo de texto hello.  Algunos roles requieren toosupply un número de vales de problemas.
7. Seleccione **Aceptar**.  Si el rol de hello no requiere aprobación, ahora se activa y rol de hello aparece en la lista Hola de roles activos (directamente debajo de hello las asignaciones de roles válidos). Si hello [rol requiere aprobación](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, aparecerá una notificación del sistema brevemente en hello superior derecha del explorador que le informa de solicitud de hello está pendiente de aprobación.

    ![Notificación de solicitud pendiente: captura de pantalla][3]

## <a name="deactivate-a-role"></a>Desactivación de un rol
Cuando se ha activado un rol, si alcanza su límite de tiempo (de duración elegible), se desactiva automáticamente.

Si completar tareas de administración al principio, también puede desactivar un rol manualmente en hello aplicación de Azure AD Privileged Identity Management.  Seleccione **Roles Mis**, elija rol Hola haya terminado con desde hello **las asignaciones de roles de Active** agrupación y, a continuación, seleccione **desactivar**.  

## <a name="cancel-a-pending-request"></a>Cancelación de una solicitud pendiente
En caso de hello no requieren activación de un rol que requiere aprobación, puede cancelar una solicitud pendiente en cualquier momento. Simplemente seleccione hello **Roles Mis** opción de navegación en la aplicación de Privileged Identity Management de hello Azure AD de la columna de navegación izquierda.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y el icono de Privileged Identity Management seleccione hello Azure AD.
2. Seleccione **My Roles** (Mis roles). Aparecerá una lista de sus roles válidos asignados en hello agrupación al principio de Hola de página de Hola.
3. Seleccione un rol.
4. Seleccione hello **activación está pendiente de aprobación** banner en la hoja de detalles de activación de rol de Hola.
5. Seleccione **cancelar** en parte superior de Hola de hello **pendiente de aprobación** hoja.

   ![Captura de pantalla de la solicitud de cancelación pendiente][4]

## <a name="next-steps"></a>Pasos siguientes
Si está interesado en aprender más sobre Azure AD Privileged Identity Management, hello vínculos siguientes tienen más información.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
