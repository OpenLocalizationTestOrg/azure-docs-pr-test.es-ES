---
title: "Concesión de acceso para Privileged Identity Management - Azure | Microsoft Docs"
description: "Aprenda a agregar roles a los usuarios con la extensión Privileged Identity Management de Azure Active Directory para que así puedan administrar PIM."
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
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="59b1f-103">Concesión de acceso para administrar Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="59b1f-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="59b1f-104">El administrador global que habilita Privileged Identity Management (PIM) de Azure AD para una organización, obtiene automáticamente asignaciones de roles y acceso a PIM.</span><span class="sxs-lookup"><span data-stu-id="59b1f-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="59b1f-105">Nadie más obtiene acceso de escritura de forma predeterminada, ni siquiera otros administradores globales.</span><span class="sxs-lookup"><span data-stu-id="59b1f-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="59b1f-106">Otros administradores globales, administradores de seguridad y lectores de seguridad tienen acceso de solo lectura a PIM de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59b1f-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="59b1f-107">Para proporcionar acceso a PIM, el primer usuario puede asignar a otros el rol **Administrador de rol con privilegios** .</span><span class="sxs-lookup"><span data-stu-id="59b1f-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="59b1f-108">Esta asignación se debe realizar desde dentro de PIM y no se puede cambiar mediante PowerShell u otros portales.</span><span class="sxs-lookup"><span data-stu-id="59b1f-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="59b1f-109">La administración de PIM de Azure AD requiere Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="59b1f-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="59b1f-110">Dado que las cuentas de Microsoft no se pueden registrar en Azure MFA, un usuario que inicia sesión con una cuenta de Microsoft no puede tener acceso a PIM de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59b1f-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="59b1f-111">Asegúrese de que siempre haya al menos dos usuarios en un rol de administrador de roles con privilegios, por si se diera el caso de que a un usuario se le impida el acceso o su cuenta se haya eliminado.</span><span class="sxs-lookup"><span data-stu-id="59b1f-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="59b1f-112">Concesión de acceso a otro usuario para administrar PIM</span><span class="sxs-lookup"><span data-stu-id="59b1f-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="59b1f-113">Vaya al [Portal de Azure](https://portal.azure.com/) y seleccione la aplicación **Privileged Identity Management de Azure AD** en el panel.</span><span class="sxs-lookup"><span data-stu-id="59b1f-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="59b1f-114">Seleccione **Administrar roles con privilegios** > **Administrador de rol con privilegios** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59b1f-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Agregar administradores de roles con privilegios: captura de pantalla][1]
3. <span data-ttu-id="59b1f-116">En la hoja Agregar usuarios administrados, el paso 1 ya está completo.</span><span class="sxs-lookup"><span data-stu-id="59b1f-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="59b1f-117">Seleccione el paso 2, **Seleccionar usuarios** y busque el usuario que quiere agregar.</span><span class="sxs-lookup"><span data-stu-id="59b1f-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Seleccionar usuarios: captura de pantalla][2]
4. <span data-ttu-id="59b1f-119">Seleccione el usuario en los resultados de búsqueda y haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="59b1f-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="59b1f-120">Haga clic en **Aceptar** para guardar la selección.</span><span class="sxs-lookup"><span data-stu-id="59b1f-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="59b1f-121">El usuario que ha seleccionado aparecerá en la lista de administradores de roles con privilegios.</span><span class="sxs-lookup"><span data-stu-id="59b1f-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="59b1f-122">Cuando asigne un nuevo rol a alguien, esta persona se configura automáticamente como apto para activar este rol.</span><span class="sxs-lookup"><span data-stu-id="59b1f-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="59b1f-123">Si quiere establecer el rol como permanente para este usuario, haga clic en él en la lista.</span><span class="sxs-lookup"><span data-stu-id="59b1f-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="59b1f-124">Seleccione **convertir en permanente** en el menú de información de usuario.</span><span class="sxs-lookup"><span data-stu-id="59b1f-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="59b1f-125">Envíe al usuario un vínculo a [Introducción a Privileged Identity Management de Azure AD](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="59b1f-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="59b1f-126">Eliminación de los derechos de acceso de otro usuario para administrar PIM</span><span class="sxs-lookup"><span data-stu-id="59b1f-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="59b1f-127">Antes de eliminar a alguien del rol de administrador de roles con privilegios, asegúrese siempre de que haya dos usuarios asignados a él.</span><span class="sxs-lookup"><span data-stu-id="59b1f-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="59b1f-128">En el panel de PIM, haga clic en el rol **Administrador de roles con privilegios**.</span><span class="sxs-lookup"><span data-stu-id="59b1f-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="59b1f-129">Se mostrará la lista de usuarios que tienen actualmente ese rol.</span><span class="sxs-lookup"><span data-stu-id="59b1f-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="59b1f-130">Haga clic en el usuario en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="59b1f-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="59b1f-131">Haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="59b1f-131">Click on **Remove**.</span></span>  <span data-ttu-id="59b1f-132">Aparecerá un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="59b1f-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="59b1f-133">Haga clic en **Sí** para quitar el usuario del rol.</span><span class="sxs-lookup"><span data-stu-id="59b1f-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="59b1f-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59b1f-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
