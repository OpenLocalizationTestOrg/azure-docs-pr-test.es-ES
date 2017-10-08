---
title: "Azure Active Directory Domain Services: habilitación de la sincronización de contraseñas | Microsoft Docs"
description: "Introducción a los Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory
En las tareas anteriores, habilitó Azure Active Directory Domain Services para su inquilino de Azure Active Directory (Azure AD). tarea siguiente de Hello es tooenable sincronización de hashes de credenciales que requiere para tooAzure de autenticación de NT LAN Manager (NTLM) y Kerberos servicios de dominio de AD. Una vez haya configurado la sincronización de credenciales, los usuarios pueden iniciar sesión toohello dominio administrado con sus credenciales corporativas.

Hola pasos implicados son diferentes para cuentas de usuario de vs de cuentas de usuario solo en la nube que se sincronizan desde su directorio local mediante Azure AD Connect.  Si su inquilino de Azure AD tiene una combinación de la nube solo los usuarios y los usuarios de sus instalaciones en AD, necesita tooperform ambos pasos.

<br>

> [!div class="op_single_selector"]
> * **Las cuentas de usuario solo en la nube**: [sincronizar contraseñas para cuentas de usuario solo en la nube dominio administrado tooyour](active-directory-ds-getting-started-password-sync.md)
> * **Las cuentas de usuario local**: [sincronizar contraseñas para cuentas de usuario que se ha sincronizado desde local AD tooyour administrado dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Tarea 5: habilitar la sincronización de contraseña tooyour dominio administrado para las cuentas de usuario solo en la nube
usuarios tooauthenticate Hola administran dominio, servicios de dominio de Active Directory de Azure necesita credenciales hash en un formato que es adecuado para la autenticación NTLM y Kerberos. Azure AD no generar o almacenar los hashes de credenciales en formato de Hola que se necesita para la autenticación NTLM o Kerberos, hasta que se habilite Azure Servicios de dominio de Active Directory para el inquilino. Por motivos de seguridad obvios, Azure AD tampoco almacena las credenciales de contraseñas en forma de texto sin cifrar. Por lo tanto, Azure AD no tiene una forma tooautomatically generar estos hashes de credenciales de Kerberos o NTLM en función de las credenciales de los usuarios existentes.

> [!NOTE]
> Si su organización tiene cuentas de usuario solo en la nube, los usuarios que necesitan los servicios de dominio de Active Directory de toouse Azure deben cambiar sus contraseñas. Una cuenta de usuario solo en la nube es una cuenta creada en su directorio de Azure AD con hello portal de Azure o cmdlets de PowerShell de Azure AD. Estas cuentas de usuario no se sincronizan desde un directorio local.
>
>

Este proceso de cambio de contraseña hace credencial Hola hashes requeridos por Azure Servicios de dominio de Active Directory para la autenticación Kerberos y NTLM toobe de autenticación generado en Azure AD. O bien puede expirar contraseñas Hola para todos los usuarios de Hola que necesitan los servicios de dominio de Active Directory de toouse Azure de inquilinos o indíqueles toochange sus contraseñas.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Habilitación de la generación de hash de credenciales de NTLM y Kerberos para una cuenta de usuario solo de nube
Aquí indicamos Hola que necesita tooprovide los usuarios, por lo que se pueden cambiar sus contraseñas:

1. Vaya toohello [Panel de acceso de Azure AD](http://myapps.microsoft.com) página para su organización.

    ![Iniciar el panel de acceso de Azure AD Hola](./media/active-directory-domain-services-getting-started/access-panel.png)

2. En hello esquina superior derecha, haga clic en su nombre y seleccione **perfil** en el menú de Hola.

    ![Seleccionar perfil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. En hello **perfil** página, haga clic en **cambiar contraseña**.

    ![Hacer clic en "Cambiar contraseña"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Si hello **cambiar contraseña** opción no se muestra en la ventana de Panel de acceso de hello, asegúrese de que su organización ha configurado [administración de contraseñas en Azure AD](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. En hello **cambiar contraseña** página, escriba la contraseña existente (antigua), escriba una contraseña nueva y, a continuación, confírmela.

    ![Creación de una red virtual para los Servicios de dominio de Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Haga clic en **Enviar**.

Unos minutos después de haber cambiado la contraseña, la nueva contraseña de hello es utilizable en servicios de dominio de Active Directory de Azure. Después de unos minutos más (normalmente, minutos aproximadamente 20), puede iniciar sesión en toocomputers que afectan al dominio administrado toohello combinadas mediante Hola recién cambiado contraseña.

## <a name="related-content"></a>Contenido relacionado
* [Cómo tooupdate su propia contraseña](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Introducción a la administración de contraseñas en Azure AD](../active-directory/active-directory-passwords-getting-started.md)
* [Habilitar la sincronización de contraseña tooAzure servicios de dominio de Active Directory para un anuncio de Azure sincronizado de inquilinos](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Administración de un dominio administrado con Azure Active Directory Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Unirse a un dominio de servicios de dominio de Active Directory de Azure administrados de tooan máquina virtual de Windows](active-directory-ds-admin-guide-join-windows-vm.md)
* [Unirse a un dominio de servicios de dominio de Active Directory de Azure administrados de tooan máquina virtual de Red Hat Enterprise Linux](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
