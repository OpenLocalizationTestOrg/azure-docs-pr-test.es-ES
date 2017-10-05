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
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="b45a2-103">Habilitación de la sincronización de contraseñas con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b45a2-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="b45a2-104">En las tareas anteriores, habilitó Azure Active Directory Domain Services para su inquilino de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b45a2-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="b45a2-105">La siguiente tarea consiste en habilitar la sincronización de los hashes de credenciales necesarios para que la autenticación NT LAN Manager (NTLM) y Kerberos se sincronice con Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="b45a2-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="b45a2-106">Una vez configurada la sincronización de credenciales, los usuarios pueden iniciar sesión en el dominio administrado mediante sus credenciales corporativas.</span><span class="sxs-lookup"><span data-stu-id="b45a2-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="b45a2-107">Los pasos necesarios son diferentes según se trate de cuentas de usuario solo de nube o de las cuentas de usuarios que se sincronizan desde el directorio local mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b45a2-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="b45a2-108">Si el inquilino de Azure AD tiene una combinación entre usuarios solo de nube y usuarios de la instalación local de AD, deberá realizar ambos pasos.</span><span class="sxs-lookup"><span data-stu-id="b45a2-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="b45a2-109">**Cuentas de usuario solo de nube**: [Sincronización de contraseñas de cuentas de usuario solo de nube con el dominio administrado](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="b45a2-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="b45a2-110">**Cuentas de usuario locales**: [Sincronización de contraseñas de cuentas de usuario sincronizadas desde la instancia local de AD con el dominio administrado](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="b45a2-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="b45a2-111">Tarea 5: habilitar la sincronización de contraseñas con el dominio administrado para las cuentas de usuario solo de nube</span><span class="sxs-lookup"><span data-stu-id="b45a2-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="b45a2-112">Azure Active Directory Domain Services necesita hashes de credenciales en un formato adecuado para la autenticación de NTLM y Kerberos para poder autenticar a los usuarios en el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="b45a2-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="b45a2-113">A menos que habilite Azure Active Directory Domain Services para el inquilino, Azure AD no genera ni almacena hashes de credenciales en el formato necesario para la autenticación NTLM o Kerberos.</span><span class="sxs-lookup"><span data-stu-id="b45a2-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="b45a2-114">Por motivos de seguridad obvios, Azure AD tampoco almacena las credenciales de contraseñas en forma de texto sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="b45a2-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="b45a2-115">Por lo tanto, Azure AD no tiene forma de generar automáticamente estos hashes de credenciales de NTLM o Kerberos basados en las credenciales de los usuarios existentes.</span><span class="sxs-lookup"><span data-stu-id="b45a2-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="b45a2-116">Si su organización tiene una cuenta de usuario solo de nube, los usuarios que tengan que usar Azure Active Directory Domain Services deberán cambiar sus contraseñas.</span><span class="sxs-lookup"><span data-stu-id="b45a2-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="b45a2-117">Una cuenta de usuario solo de nube es una cuenta creada en su directorio de Azure AD mediante Azure Portal, o bien mediante cmdlets de PowerShell de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b45a2-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="b45a2-118">Estas cuentas de usuario no se sincronizan desde un directorio local.</span><span class="sxs-lookup"><span data-stu-id="b45a2-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="b45a2-119">Este proceso de cambio de contraseña hace que los valores de hash de credenciales que necesita Azure Active Directory Domain Services para la autenticación Kerberos y NTLM se generen en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b45a2-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="b45a2-120">Puede caducar las contraseñas de todos los usuarios en el inquilino que tiene que usar Azure Active Directory Domain Services o indicar a estos usuarios que cambien sus contraseñas.</span><span class="sxs-lookup"><span data-stu-id="b45a2-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="b45a2-121">Habilitación de la generación de hash de credenciales de NTLM y Kerberos para una cuenta de usuario solo de nube</span><span class="sxs-lookup"><span data-stu-id="b45a2-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="b45a2-122">Estas son las instrucciones que tiene que proporcionar a los usuarios finales para que puedan cambiar sus contraseñas:</span><span class="sxs-lookup"><span data-stu-id="b45a2-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="b45a2-123">Vaya a la página [Panel de acceso de Azure AD](http://myapps.microsoft.com) para su organización.</span><span class="sxs-lookup"><span data-stu-id="b45a2-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Inicio del panel de acceso de Azure AD](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="b45a2-125">En la esquina superior derecha, haga clic en su nombre y seleccione **Perfil** en el menú.</span><span class="sxs-lookup"><span data-stu-id="b45a2-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Seleccionar perfil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="b45a2-127">En la página **Perfil**, haga clic en **Cambiar contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b45a2-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Hacer clic en "Cambiar contraseña"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="b45a2-129">Si no aparece la opción **Cambiar contraseña** en la ventana Panel de acceso, asegúrese de que su organización ha configurado la [administración de contraseñas en Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b45a2-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="b45a2-130">En la página **cambiar contraseña**, escriba la contraseña existente (anterior) y luego escriba una nueva contraseña y confírmela.</span><span class="sxs-lookup"><span data-stu-id="b45a2-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Creación de una red virtual para los Servicios de dominio de Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="b45a2-132">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="b45a2-132">Click **submit**.</span></span>

<span data-ttu-id="b45a2-133">Unos minutos después de haber cambiado su contraseña, la nueva contraseña se podrá usar en Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="b45a2-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b45a2-134">Después de unos minutos (por lo general, unos 20 minutos), los usuarios pueden iniciar sesión en equipos unidos al dominio administrado con su contraseña recién cambiada.</span><span class="sxs-lookup"><span data-stu-id="b45a2-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="b45a2-135">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="b45a2-135">Related Content</span></span>
* [<span data-ttu-id="b45a2-136">Actualización de la propia contraseña</span><span class="sxs-lookup"><span data-stu-id="b45a2-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="b45a2-137">Introducción a la administración de contraseñas en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b45a2-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="b45a2-138">Habilitación de la sincronización de contraseñas con Azure Active Directory Domain Services para un inquilino de Azure AD sincronizado</span><span class="sxs-lookup"><span data-stu-id="b45a2-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="b45a2-139">Administración de un dominio administrado con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b45a2-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="b45a2-140">Join a Windows virtual machine to an Azure AD Domain Services managed domain (Unión de una máquina virtual Windows a un dominio administrado de Azure Active Directory Domain Services)</span><span class="sxs-lookup"><span data-stu-id="b45a2-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="b45a2-141">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain (Unión de una máquina virtual con Red Hat Enterprise Linux a un dominio administrado de Azure Active Directory Domain Services)</span><span class="sxs-lookup"><span data-stu-id="b45a2-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
