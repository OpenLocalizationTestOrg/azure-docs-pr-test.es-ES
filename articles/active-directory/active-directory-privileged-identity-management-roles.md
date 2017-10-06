---
title: aaaRoles en Azure AD Privileged Identity Management | Documentos de Microsoft
description: "Obtenga información acerca de los roles se utilizan para identidades con privilegios con hello extensión de Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Rol administrativo diferente en Azure Active Directory PIM
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

Puede asignar a los usuarios de su organización roles administrativos toodifferent en Azure AD. Estas asignaciones de roles de controlar qué tareas, como agregar o quitar usuarios o cambiar la configuración de servicio, los usuarios de hello son tooperform capaz en Azure AD, Office 365 y otros servicios en línea de Microsoft y aplicaciones conectadas.  

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.

Un administrador global puede actualizar los usuarios **permanentemente** asignado tooroles en Azure AD, mediante los cmdlets de PowerShell como `Add-MsolRoleMember` y `Remove-MsolRoleMember`, o a través del portal clásico de hello tal como se describe en [ asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md).

Privileged Identity Management (PIM) de Azure AD administra las directivas de acceso con privilegios para los usuarios en Azure AD. PIM asigna usuarios tooone o más roles en Azure AD y puede asignar a alguien toobe permanente de rol de Hola o válidos para la función hello. Cuando un usuario se asigna permanentemente el rol de tooa o activa una asignación de roles pueden, a continuación, pueden administrar Active Directory de Azure, Office 365 y otras aplicaciones con permisos de hello tootheir roles asignados.

No hay ninguna diferencia en el acceso de hello dado toosomeone con permanente frente a una asignación de roles válidos. Hola única diferencia es que algunas personas, no es necesario que el acceso a todo el tiempo Hola. Se realizan aptos para su rol de Hola y pueden activar y desactivar cada vez necesitan.

## <a name="roles-managed-in-pim"></a>Roles administrados en PIM
Privileged Identity Management de le permite asignar roles de administrador de toocommon de los usuarios, incluidos:

* **Administrador global** (también conocido como administrador de la compañía) tiene características administrativas de acceso tooall. Puede tener más de un administrador global en su organización. Hola quien automáticamente se suscribe toopurchase Office 365 se convierte en un administrador global.
* **administrador de roles con privilegios** administra PIM de Azure AD y actualiza las asignaciones de roles para otros usuarios.  
* **Administrador de facturación** : hace compras, administra suscripciones, administra incidencias de soporte técnico y supervisa el estado del servicio.
* **Administrador de contraseñas** : restablece las contraseñas, administra las solicitudes de servicio y supervisa el estado del servicio. Administradores de contraseñas son contraseñas tooresetting limitado de usuarios.
* **Administrador de servicios** : administra las solicitudes de servicio y supervisa el estado del servicio.
  
  > [!NOTE]
  > Si utilizas Office 365, a continuación, antes de asignar el usuario de tooa del rol Hola de administración de servicio, en primer lugar asignar permisos administrativos del usuario de hello tooa servicio, como Exchange Online.
  > 
  > 
* **administrador de control de usuarios** restablece las contraseñas, supervisa el estado del servicio y administra cuentas de usuario, grupos de usuarios y solicitudes de servicio. Hola de administración de usuario no se puede eliminar un administrador global, crear otros roles de administrador o restablecer las contraseñas de facturación, globales y administradores de servicios.
* **Administrador de Exchange** tiene acceso administrativo tooExchange en línea a través del centro de administración de Exchange de hello (CEF) y puede realizar casi cualquier tarea en Exchange Online.
* **Administrador de SharePoint** tiene acceso administrativo tooSharePoint en línea a través del centro de administración de SharePoint Online de Hola y puede realizar casi cualquier tarea en SharePoint Online.
* **Skype para Administrador empresarial** tiene acceso administrativo tooSkype para la empresa a través de hello Skype para el centro de administración de negocios y puede realizar casi cualquier tarea de Skype empresarial Online.

Consulte estos artículos para más información sobre la [asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md) y de roles de administrador en [Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


De PIM, también puede [asignar estos usuarios de roles tooa](active-directory-privileged-identity-management-how-to-add-role-to-user.md) para que puedan hello usuario [activar Hola rol cuando sea necesario](active-directory-privileged-identity-management-how-to-activate-role.md).

Si desea toogive otro toomanage de acceso de usuario de PIM, roles de Hola que PIM requiere hello toohave de usuario se describen con mayor detalle en [cómo toogive a tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Roles no administrados en PIM
Los roles de Exchange Online o SharePoint Online, excepto los mencionados anteriormente, no están representados en Azure AD y, por lo tanto, no son visibles en PIM. Para obtener más información sobre cómo cambiar las asignaciones de roles específicas de estos servicios de Office 365, consulte [Permisos en Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Las suscripciones de Azure y los grupos de recursos tampoco están representados en Azure AD. toomanage Azure suscripciones, vea [cómo tooadd o cambiar roles de administrador de Azure](../billing/billing-add-change-azure-subscription-administrator.md) y para obtener más información sobre, consulte RBAC de Azure [Azure Role-Based el Control de acceso](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Roles de usuario e inicio de sesión
Para algunas aplicaciones y servicios de Microsoft, asignación de un rol de usuario tooa puede no ser suficiente tooenable ese toobe de usuario administrador.

Acceso toohello portal de Azure clásico requiere Hola usuario sea un administrador de servicios o Coadministrador en una suscripción de Azure, incluso si el usuario de hello no necesita toomanage Hola suscripciones de Azure.  Por ejemplo, los valores de configuración de toomanage para Azure AD en el portal clásico hello, un usuario deben ser un administrador global de Azure AD y un Coadministrador de suscripción en una suscripción de Azure.  toolearn cómo ver las suscripciones de tooadd usuarios tooAzure, [cómo tooadd o cambiar roles de administrador de Azure](../billing/billing-add-change-azure-subscription-administrator.md).

TooMicrosoft de acceso a servicios en línea pueden requerir usuario hello también se pueden asignar una licencia para poder abrir el portal del servicio de Hola o realizar tareas administrativas.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Asignar a un usuario de tooa de licencia de Azure AD
1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com) con una cuenta de administrador global o una cuenta de administrador.
2. Seleccione **todos los elementos** desde el menú principal de Hola.
3. Seleccione el directorio de hello que desea toowork con y que tiene licencias asociado.
4. Seleccione **Licencias**. Aparecerá la lista de Hola de licencias disponibles.
5. Seleccione el plan de licencia de Hola que contiene las licencias de Hola que desea toodistribute.
6. Seleccione **Asignar usuarios**.
7. Usuario seleccione Hola que desea tooassign una licencia para.
8. Haga clic en hello **asignar** botón.  usuario de Hello ahora puede iniciar sesión en tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

