---
title: "Administración de la configuración de activación del rol | Microsoft Docs"
description: "Obtenga información sobre cómo cambiar la configuración predeterminada de identidades con privilegios con la extensión de Privileged Identity Management de Azure Active Directory."
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="78d8a-103">Administración de la configuración de activación de rol en Privileged Identity Management de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d8a-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="78d8a-104">Un administrador de roles con privilegios puede personalizar Privileged Identity Management (PIM) de Azure AD en su organización, como cambiar la experiencia de un usuario que va a activar una asignación de rol apto.</span><span class="sxs-lookup"><span data-stu-id="78d8a-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="78d8a-105">Administración de la configuración de activación del rol</span><span class="sxs-lookup"><span data-stu-id="78d8a-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="78d8a-106">Vaya al [Portal de Azure](https://portal.azure.com) y seleccione la aplicación **Azure AD Privileged Identity Management** en el panel.</span><span class="sxs-lookup"><span data-stu-id="78d8a-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="78d8a-107">Seleccione **Administrar roles con privilegios** > **Configuración** > **Roles con privilegios**.</span><span class="sxs-lookup"><span data-stu-id="78d8a-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="78d8a-108">Seleccione el rol cuya configuración desea administrar.</span><span class="sxs-lookup"><span data-stu-id="78d8a-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="78d8a-109">En la página de configuración de cada rol, hay una serie de valores que puede configurar.</span><span class="sxs-lookup"><span data-stu-id="78d8a-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="78d8a-110">Esta configuración solo afecta a los usuarios que son administradores aptos, no a los administradores permanentes.</span><span class="sxs-lookup"><span data-stu-id="78d8a-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="78d8a-111">**Activaciones**: el tiempo, en horas, que un rol permanece activo antes de que caduque.</span><span class="sxs-lookup"><span data-stu-id="78d8a-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="78d8a-112">Este valor puede estar comprendido entre 1 y 72 horas.</span><span class="sxs-lookup"><span data-stu-id="78d8a-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="78d8a-113">**Notificaciones**: puede elegir si el sistema enviará o no correos electrónicos a los administradores para confirmar que han activado un rol.</span><span class="sxs-lookup"><span data-stu-id="78d8a-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="78d8a-114">Puede ser útil para detectar activaciones no autorizadas o ilegales.</span><span class="sxs-lookup"><span data-stu-id="78d8a-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="78d8a-115">**Vale de incidente o solicitud**: puede elegir que los administradores incluyan o no un número de vale cuando activen su rol.</span><span class="sxs-lookup"><span data-stu-id="78d8a-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="78d8a-116">Puede ser útil al realizar auditorías de acceso a rol.</span><span class="sxs-lookup"><span data-stu-id="78d8a-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="78d8a-117">**Multi-Factor Authentication**: puede elegir que los usuarios comprueben o no su identidad con MFA para poder activar sus roles.</span><span class="sxs-lookup"><span data-stu-id="78d8a-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="78d8a-118">Solo tiene que realizar esta acción una vez por sesión, no cada vez que activen un rol.</span><span class="sxs-lookup"><span data-stu-id="78d8a-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="78d8a-119">Al habilitar MFA, es conveniente tener en cuenta dos sugerencias:</span><span class="sxs-lookup"><span data-stu-id="78d8a-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="78d8a-120">Los usuarios que tienen cuentas de Microsoft para obtener sus direcciones de correo electrónico (normalmente @outlook.com, pero no siempre) no se puede registrar para Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="78d8a-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="78d8a-121">Si quiere asignar roles a los usuarios con cuentas de Microsoft, debe establecerlos en administradores permanentes o deshabilitar MFA para ese rol.</span><span class="sxs-lookup"><span data-stu-id="78d8a-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="78d8a-122">No se puede deshabilitar MFA para roles con privilegios elevados en Azure AD y Office 365.</span><span class="sxs-lookup"><span data-stu-id="78d8a-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="78d8a-123">Esta es una característica de seguridad porque estos roles deben protegerse cuidadosamente:</span><span class="sxs-lookup"><span data-stu-id="78d8a-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="78d8a-124">Administrador de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="78d8a-124">Application administrator</span></span>
  * <span data-ttu-id="78d8a-125">Administrador del servidor proxy de la aplicación</span><span class="sxs-lookup"><span data-stu-id="78d8a-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="78d8a-126">Administrador de facturación</span><span class="sxs-lookup"><span data-stu-id="78d8a-126">Billing administrator</span></span>  
  * <span data-ttu-id="78d8a-127">Administrador de cumplimiento</span><span class="sxs-lookup"><span data-stu-id="78d8a-127">Compliance administrator</span></span>  
  * <span data-ttu-id="78d8a-128">Administrador de servicios de CRM</span><span class="sxs-lookup"><span data-stu-id="78d8a-128">CRM service administrator</span></span>
  * <span data-ttu-id="78d8a-129">Aprobador del acceso a la Caja de seguridad del cliente</span><span class="sxs-lookup"><span data-stu-id="78d8a-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="78d8a-130">Escritor de directorio</span><span class="sxs-lookup"><span data-stu-id="78d8a-130">Directory writer</span></span>  
  * <span data-ttu-id="78d8a-131">Administrador de Exchange</span><span class="sxs-lookup"><span data-stu-id="78d8a-131">Exchange administrator</span></span>  
  * <span data-ttu-id="78d8a-132">Administrador global</span><span class="sxs-lookup"><span data-stu-id="78d8a-132">Global administrator</span></span>
  * <span data-ttu-id="78d8a-133">Administrador de servicios de Intune</span><span class="sxs-lookup"><span data-stu-id="78d8a-133">Intune service administrator</span></span>
  * <span data-ttu-id="78d8a-134">Administrador de buzón de correo</span><span class="sxs-lookup"><span data-stu-id="78d8a-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="78d8a-135">Soporte para asociados de nivel 1</span><span class="sxs-lookup"><span data-stu-id="78d8a-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="78d8a-136">Soporte para asociados de nivel 2</span><span class="sxs-lookup"><span data-stu-id="78d8a-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="78d8a-137">Administrador de roles con privilegios</span><span class="sxs-lookup"><span data-stu-id="78d8a-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="78d8a-138">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="78d8a-138">Security administrator</span></span>  
  * <span data-ttu-id="78d8a-139">Administrador de SharePoint</span><span class="sxs-lookup"><span data-stu-id="78d8a-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="78d8a-140">Administrador de Skype Empresarial</span><span class="sxs-lookup"><span data-stu-id="78d8a-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="78d8a-141">Administrador de cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="78d8a-141">User account administrator</span></span>  

<span data-ttu-id="78d8a-142">Para obtener más información sobre cómo usar MFA con PIM, vea [Exigencia de MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="78d8a-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="78d8a-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78d8a-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

