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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="adc3a-103">Habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="adc3a-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="adc3a-104">En las tareas anteriores, habilitó Azure Active Directory Domain Services para su inquilino de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="adc3a-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="adc3a-105">tarea siguiente de Hello es tooenable sincronización de hashes de credenciales que requiere para tooAzure de autenticación de NT LAN Manager (NTLM) y Kerberos servicios de dominio de AD.</span><span class="sxs-lookup"><span data-stu-id="adc3a-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="adc3a-106">Una vez haya configurado la sincronización de credenciales, los usuarios pueden iniciar sesión toohello dominio administrado con sus credenciales corporativas.</span><span class="sxs-lookup"><span data-stu-id="adc3a-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="adc3a-107">Hola pasos implicados son diferentes para cuentas de usuario de vs de cuentas de usuario solo en la nube que se sincronizan desde su directorio local mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="adc3a-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="adc3a-108">Si su inquilino de Azure AD tiene una combinación de la nube solo los usuarios y los usuarios de sus instalaciones en AD, necesita tooperform ambos pasos.</span><span class="sxs-lookup"><span data-stu-id="adc3a-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="adc3a-109">**Las cuentas de usuario solo en la nube**: [sincronizar contraseñas para cuentas de usuario solo en la nube dominio administrado tooyour](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="adc3a-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="adc3a-110">**Las cuentas de usuario local**: [sincronizar contraseñas para cuentas de usuario que se ha sincronizado desde local AD tooyour administrado dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="adc3a-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="adc3a-111">Tarea 5: habilitar la sincronización de contraseña tooyour dominio administrado para las cuentas de usuario solo en la nube</span><span class="sxs-lookup"><span data-stu-id="adc3a-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="adc3a-112">usuarios tooauthenticate Hola administran dominio, servicios de dominio de Active Directory de Azure necesita credenciales hash en un formato que es adecuado para la autenticación NTLM y Kerberos.</span><span class="sxs-lookup"><span data-stu-id="adc3a-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="adc3a-113">Azure AD no generar o almacenar los hashes de credenciales en formato de Hola que se necesita para la autenticación NTLM o Kerberos, hasta que se habilite Azure Servicios de dominio de Active Directory para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="adc3a-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="adc3a-114">Por motivos de seguridad obvios, Azure AD tampoco almacena las credenciales de contraseñas en forma de texto sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="adc3a-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="adc3a-115">Por lo tanto, Azure AD no tiene una forma tooautomatically generar estos hashes de credenciales de Kerberos o NTLM en función de las credenciales de los usuarios existentes.</span><span class="sxs-lookup"><span data-stu-id="adc3a-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="adc3a-116">Si su organización tiene cuentas de usuario solo en la nube, los usuarios que necesitan los servicios de dominio de Active Directory de toouse Azure deben cambiar sus contraseñas.</span><span class="sxs-lookup"><span data-stu-id="adc3a-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="adc3a-117">Una cuenta de usuario solo en la nube es una cuenta creada en su directorio de Azure AD con hello portal de Azure o cmdlets de PowerShell de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="adc3a-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="adc3a-118">Estas cuentas de usuario no se sincronizan desde un directorio local.</span><span class="sxs-lookup"><span data-stu-id="adc3a-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="adc3a-119">Este proceso de cambio de contraseña hace credencial Hola hashes requeridos por Azure Servicios de dominio de Active Directory para la autenticación Kerberos y NTLM toobe de autenticación generado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="adc3a-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="adc3a-120">O bien puede expirar contraseñas Hola para todos los usuarios de Hola que necesitan los servicios de dominio de Active Directory de toouse Azure de inquilinos o indíqueles toochange sus contraseñas.</span><span class="sxs-lookup"><span data-stu-id="adc3a-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="adc3a-121">Habilitación de la generación de hash de credenciales de NTLM y Kerberos para una cuenta de usuario solo de nube</span><span class="sxs-lookup"><span data-stu-id="adc3a-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="adc3a-122">Aquí indicamos Hola que necesita tooprovide los usuarios, por lo que se pueden cambiar sus contraseñas:</span><span class="sxs-lookup"><span data-stu-id="adc3a-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="adc3a-123">Vaya toohello [Panel de acceso de Azure AD](http://myapps.microsoft.com) página para su organización.</span><span class="sxs-lookup"><span data-stu-id="adc3a-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Iniciar el panel de acceso de Azure AD Hola](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="adc3a-125">En hello esquina superior derecha, haga clic en su nombre y seleccione **perfil** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="adc3a-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Seleccionar perfil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="adc3a-127">En hello **perfil** página, haga clic en **cambiar contraseña**.</span><span class="sxs-lookup"><span data-stu-id="adc3a-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Hacer clic en "Cambiar contraseña"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="adc3a-129">Si hello **cambiar contraseña** opción no se muestra en la ventana de Panel de acceso de hello, asegúrese de que su organización ha configurado [administración de contraseñas en Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="adc3a-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="adc3a-130">En hello **cambiar contraseña** página, escriba la contraseña existente (antigua), escriba una contraseña nueva y, a continuación, confírmela.</span><span class="sxs-lookup"><span data-stu-id="adc3a-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Creación de una red virtual para los Servicios de dominio de Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="adc3a-132">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="adc3a-132">Click **submit**.</span></span>

<span data-ttu-id="adc3a-133">Unos minutos después de haber cambiado la contraseña, la nueva contraseña de hello es utilizable en servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="adc3a-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="adc3a-134">Después de unos minutos más (normalmente, minutos aproximadamente 20), puede iniciar sesión en toocomputers que afectan al dominio administrado toohello combinadas mediante Hola recién cambiado contraseña.</span><span class="sxs-lookup"><span data-stu-id="adc3a-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="adc3a-135">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="adc3a-135">Related Content</span></span>
* [<span data-ttu-id="adc3a-136">Cómo tooupdate su propia contraseña</span><span class="sxs-lookup"><span data-stu-id="adc3a-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="adc3a-137">Introducción a la administración de contraseñas en Azure AD</span><span class="sxs-lookup"><span data-stu-id="adc3a-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="adc3a-138">Habilitar la sincronización de contraseña tooAzure servicios de dominio de Active Directory para un anuncio de Azure sincronizado de inquilinos</span><span class="sxs-lookup"><span data-stu-id="adc3a-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="adc3a-139">Administración de un dominio administrado con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="adc3a-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="adc3a-140">Unirse a un dominio de servicios de dominio de Active Directory de Azure administrados de tooan máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="adc3a-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="adc3a-141">Unirse a un dominio de servicios de dominio de Active Directory de Azure administrados de tooan máquina virtual de Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="adc3a-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
