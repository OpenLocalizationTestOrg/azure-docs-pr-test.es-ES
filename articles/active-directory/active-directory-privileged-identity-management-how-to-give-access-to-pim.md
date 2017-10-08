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
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="4e1a4-103">Lo que proporciona acceso toomanage AD Privileged Identity Management de Azure</span><span class="sxs-lookup"><span data-stu-id="4e1a4-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="4e1a4-104">Administrador global de Hello, que permite a Azure AD Privileged Identity Management (PIM) de una organización automáticamente obtener las asignaciones de roles y tener acceso a tooPIM.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="4e1a4-105">Nadie más obtiene acceso de escritura de forma predeterminada, ni siquiera otros administradores globales.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="4e1a4-106">Otros administradores globales, los administradores de seguridad y los lectores de seguridad tienen acceso de solo lectura tooAzure PIM AD.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="4e1a4-107">toogive acceso tooPIM, Hola primer usuario puede asignar a otros usuarios toohello **Administrador de roles con privilegios de** rol.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="4e1a4-108">Esta asignación se debe realizar desde dentro de PIM y no se puede cambiar mediante PowerShell u otros portales.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="4e1a4-109">La administración de PIM de Azure AD requiere Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="4e1a4-110">Dado que las cuentas de Microsoft no se pueden registrar en Azure MFA, un usuario que inicia sesión con una cuenta de Microsoft no puede tener acceso a PIM de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="4e1a4-111">Asegúrese de que siempre haya al menos dos usuarios en un rol de administrador de roles con privilegios, por si se diera el caso de que a un usuario se le impida el acceso o su cuenta se haya eliminado.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="4e1a4-112">Proporcionar a otro usuario acceso toomanage PIM</span><span class="sxs-lookup"><span data-stu-id="4e1a4-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="4e1a4-113">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y seleccione hello **Azure AD Privileged Identity Management** aplicación en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="4e1a4-114">Seleccione **Administrar roles con privilegios** > **Administrador de rol con privilegios** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Agregar administradores de roles con privilegios: captura de pantalla][1]
3. <span data-ttu-id="4e1a4-116">En la hoja de hello agregar usuarios administrados, paso 1 ya está completando.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="4e1a4-117">Seleccione paso 2, **Seleccionar usuarios** y búsqueda para el usuario de hello desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Seleccionar usuarios: captura de pantalla][2]
4. <span data-ttu-id="4e1a4-119">Seleccione el usuario de hello en los resultados de búsqueda de Hola y haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="4e1a4-120">Haga clic en **Aceptar** toosave la selección.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="4e1a4-121">usuario de Hola que ha seleccionado se mostrará en lista de Hola de administradores de roles con privilegios.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="4e1a4-122">Cada vez que se asigna un nuevo toosomeone de rol, se configuran automáticamente como rol de hello tooactivate elegibles.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="4e1a4-123">Si desea que toomake permanente en función de hello, haga clic en usuario de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="4e1a4-124">Seleccione **realizar perm** en el menú de información de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="4e1a4-125">Enviar un vínculo al usuario de hello demasiado[Introducción a Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4e1a4-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="4e1a4-126">Eliminación de los derechos de acceso de otro usuario para administrar PIM</span><span class="sxs-lookup"><span data-stu-id="4e1a4-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="4e1a4-127">Antes de quitar un usuario del rol de administrador de roles con privilegios de hello, asegúrese siempre de seguirá habiendo dos usuarios asignados tooit.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="4e1a4-128">En el panel PIM de hello, haga clic en el rol de Hola **Administrador de roles con privilegios de**.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="4e1a4-129">se mostrará la lista de Hola de usuarios actualmente en ese rol.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="4e1a4-130">Haga clic en usuario de hello en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="4e1a4-131">Haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-131">Click on **Remove**.</span></span>  <span data-ttu-id="4e1a4-132">Aparecerá un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="4e1a4-133">Haga clic en **Sí** tooremove usuario Hola rol Hola.</span><span class="sxs-lookup"><span data-stu-id="4e1a4-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="4e1a4-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e1a4-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
