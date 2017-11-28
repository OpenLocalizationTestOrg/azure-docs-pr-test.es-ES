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
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="7f4ab-103">La configuración de activación de rol toomanage en Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="7f4ab-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="7f4ab-104">Un administrador de roles con privilegios puede personalizar con privilegios de Azure AD Identity Management (PIM) en su organización, incluida la modificación de la experiencia de Hola para un usuario que se está activando una asignación de roles válidos.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="7f4ab-105">Administrar la configuración de activación de rol de Hola</span><span class="sxs-lookup"><span data-stu-id="7f4ab-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="7f4ab-106">Vaya toohello [portal de Azure](https://portal.azure.com) y seleccione hello **Azure AD Privileged Identity Management** aplicación desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="7f4ab-107">Seleccione **Administrar roles con privilegios** > **Configuración** > **Roles con privilegios**.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="7f4ab-108">Elija el rol de Hola cuya configuración desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="7f4ab-109">En la página de configuración de Hola para cada rol, hay una serie de opciones que puede configurar.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="7f4ab-110">Esta configuración solo afecta a los usuarios que son administradores aptos, no a los administradores permanentes.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="7f4ab-111">**Las activaciones**: tiempo de hello, en horas, que un rol permanece activo antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="7f4ab-112">Este valor puede estar comprendido entre 1 y 72 horas.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="7f4ab-113">**Las notificaciones**: puede elegir si o no el sistema de hello envía tooadmins de mensajes de correo electrónico confirma que ha activado un rol.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="7f4ab-114">Puede ser útil para detectar activaciones no autorizadas o ilegales.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="7f4ab-115">**Vale de incidente o solicitud**: puede elegir si se permite o no toorequire administradores elegibles tooinclude un vale de número cuando activa su rol.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="7f4ab-116">Puede ser útil al realizar auditorías de acceso a rol.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="7f4ab-117">**La autenticación multifactor**: puede elegir si toorequire usuarios tooverify su identidad con MFA para poder activar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="7f4ab-118">Solo tienen tooverify esto una vez por sesión, no cada vez que Active un rol.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="7f4ab-119">Hay dos tookeep sugerencias en cuenta al habilitar MFA:</span><span class="sxs-lookup"><span data-stu-id="7f4ab-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="7f4ab-120">Los usuarios que tienen cuentas de Microsoft para obtener sus direcciones de correo electrónico (normalmente @outlook.com, pero no siempre) no se puede registrar para Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="7f4ab-121">Si desea tooassign roles toousers con cuentas de Microsoft, debe hacerlos administradores permanentes o deshabilitar MFA para ese rol.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="7f4ab-122">No se puede deshabilitar MFA para roles con privilegios elevados en Azure AD y Office 365.</span><span class="sxs-lookup"><span data-stu-id="7f4ab-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="7f4ab-123">Esta es una característica de seguridad porque estos roles deben protegerse cuidadosamente:</span><span class="sxs-lookup"><span data-stu-id="7f4ab-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="7f4ab-124">Administrador de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7f4ab-124">Application administrator</span></span>
  * <span data-ttu-id="7f4ab-125">Administrador del servidor proxy de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7f4ab-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="7f4ab-126">Administrador de facturación</span><span class="sxs-lookup"><span data-stu-id="7f4ab-126">Billing administrator</span></span>  
  * <span data-ttu-id="7f4ab-127">Administrador de cumplimiento</span><span class="sxs-lookup"><span data-stu-id="7f4ab-127">Compliance administrator</span></span>  
  * <span data-ttu-id="7f4ab-128">Administrador de servicios de CRM</span><span class="sxs-lookup"><span data-stu-id="7f4ab-128">CRM service administrator</span></span>
  * <span data-ttu-id="7f4ab-129">Aprobador del acceso a la Caja de seguridad del cliente</span><span class="sxs-lookup"><span data-stu-id="7f4ab-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="7f4ab-130">Escritor de directorio</span><span class="sxs-lookup"><span data-stu-id="7f4ab-130">Directory writer</span></span>  
  * <span data-ttu-id="7f4ab-131">Administrador de Exchange</span><span class="sxs-lookup"><span data-stu-id="7f4ab-131">Exchange administrator</span></span>  
  * <span data-ttu-id="7f4ab-132">Administrador global</span><span class="sxs-lookup"><span data-stu-id="7f4ab-132">Global administrator</span></span>
  * <span data-ttu-id="7f4ab-133">Administrador de servicios de Intune</span><span class="sxs-lookup"><span data-stu-id="7f4ab-133">Intune service administrator</span></span>
  * <span data-ttu-id="7f4ab-134">Administrador de buzón de correo</span><span class="sxs-lookup"><span data-stu-id="7f4ab-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="7f4ab-135">Soporte para asociados de nivel 1</span><span class="sxs-lookup"><span data-stu-id="7f4ab-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="7f4ab-136">Soporte para asociados de nivel 2</span><span class="sxs-lookup"><span data-stu-id="7f4ab-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="7f4ab-137">Administrador de roles con privilegios</span><span class="sxs-lookup"><span data-stu-id="7f4ab-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="7f4ab-138">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="7f4ab-138">Security administrator</span></span>  
  * <span data-ttu-id="7f4ab-139">Administrador de SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f4ab-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="7f4ab-140">Administrador de Skype Empresarial</span><span class="sxs-lookup"><span data-stu-id="7f4ab-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="7f4ab-141">Administrador de cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="7f4ab-141">User account administrator</span></span>  

<span data-ttu-id="7f4ab-142">Para obtener más información sobre el uso de MFA con PIM vea [cómo tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="7f4ab-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="7f4ab-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f4ab-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

