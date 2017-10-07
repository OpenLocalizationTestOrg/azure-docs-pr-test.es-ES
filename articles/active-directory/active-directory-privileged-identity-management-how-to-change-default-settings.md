---
title: "configuración de activación de rol aaaHow toomanage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toochange Hola configuración predeterminada para las identidades con privilegios con hello extensión de Active Directory Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>La configuración de activación de rol toomanage en Azure AD Privileged Identity Management
Un administrador de roles con privilegios puede personalizar con privilegios de Azure AD Identity Management (PIM) en su organización, incluida la modificación de la experiencia de Hola para un usuario que se está activando una asignación de roles válidos.

## <a name="manage-hello-role-activation-settings"></a>Administrar la configuración de activación de rol de Hola
1. Vaya toohello [portal de Azure](https://portal.azure.com) y seleccione hello **Azure AD Privileged Identity Management** aplicación desde el panel de Hola.
2. Seleccione **Administrar roles con privilegios** > **Configuración** > **Roles con privilegios**.
3. Elija el rol de Hola cuya configuración desea toomanage.

En la página de configuración de Hola para cada rol, hay una serie de opciones que puede configurar. Esta configuración solo afecta a los usuarios que son administradores aptos, no a los administradores permanentes.

**Las activaciones**: tiempo de hello, en horas, que un rol permanece activo antes de que expire. Este valor puede estar comprendido entre 1 y 72 horas.

**Las notificaciones**: puede elegir si o no el sistema de hello envía tooadmins de mensajes de correo electrónico confirma que ha activado un rol. Puede ser útil para detectar activaciones no autorizadas o ilegales.

**Vale de incidente o solicitud**: puede elegir si se permite o no toorequire administradores elegibles tooinclude un vale de número cuando activa su rol. Puede ser útil al realizar auditorías de acceso a rol.

**La autenticación multifactor**: puede elegir si toorequire usuarios tooverify su identidad con MFA para poder activar sus funciones. Solo tienen tooverify esto una vez por sesión, no cada vez que Active un rol. Hay dos tookeep sugerencias en cuenta al habilitar MFA:

* Los usuarios que tienen cuentas de Microsoft para obtener sus direcciones de correo electrónico (normalmente @outlook.com, pero no siempre) no se puede registrar para Azure MFA. Si desea tooassign roles toousers con cuentas de Microsoft, debe hacerlos administradores permanentes o deshabilitar MFA para ese rol.
* No se puede deshabilitar MFA para roles con privilegios elevados en Azure AD y Office 365. Esta es una característica de seguridad porque estos roles deben protegerse cuidadosamente:  
  
  * Administrador de aplicaciones
  * Administrador del servidor proxy de la aplicación
  * Administrador de facturación  
  * Administrador de cumplimiento  
  * Administrador de servicios de CRM
  * Aprobador del acceso a la Caja de seguridad del cliente
  * Escritor de directorio  
  * Administrador de Exchange  
  * Administrador global
  * Administrador de servicios de Intune
  * Administrador de buzón de correo  
  * Soporte para asociados de nivel 1  
  * Soporte para asociados de nivel 2  
  * Administrador de roles con privilegios   
  * Administrador de seguridad  
  * Administrador de SharePoint  
  * Administrador de Skype Empresarial  
  * Administrador de cuenta de usuario  

Para obtener más información sobre el uso de MFA con PIM vea [cómo tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

