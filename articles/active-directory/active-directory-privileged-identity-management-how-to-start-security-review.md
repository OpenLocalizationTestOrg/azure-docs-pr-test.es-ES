---
title: "Inicio de una revisión del acceso | Microsoft Docs"
description: "Aprenda a crear una revisión de acceso para identidades con privilegios con la aplicación Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="25dc0-103">Inicio de una revisión de acceso en Privileged Identity Management de Azure AD</span><span class="sxs-lookup"><span data-stu-id="25dc0-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="25dc0-104">Las asignaciones de roles se convierten en "obsoletas" cuando los usuarios tienen acceso con privilegios que ya no necesitan.</span><span class="sxs-lookup"><span data-stu-id="25dc0-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="25dc0-105">Con el fin de reducir el riesgo asociado a estas asignaciones de roles obsoletos, los administradores de roles con privilegios deben revisar regularmente los roles que se han concedido a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="25dc0-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="25dc0-106">En este documento se describen los pasos para iniciar una revisión de acceso en Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="25dc0-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="25dc0-107">Inicio de una revisión de acceso</span><span class="sxs-lookup"><span data-stu-id="25dc0-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="25dc0-108">Si no ha agregado la aplicación PIM al panel de Azure Portal, consulte los pasos que se indican en [Introducción a Privileged Identity Management de Azure AD](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="25dc0-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="25dc0-109">En la página principal de la aplicación PIM, hay tres formas de comenzar una revisión de acceso:</span><span class="sxs-lookup"><span data-stu-id="25dc0-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="25dc0-110">**Revisiones de acceso** > **Agregar**</span><span class="sxs-lookup"><span data-stu-id="25dc0-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="25dc0-111">Botón **Roles** > **Revisar**</span><span class="sxs-lookup"><span data-stu-id="25dc0-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="25dc0-112">Seleccionar el rol específico que se va a revisar en la lista de roles > Botón **Revisar**</span><span class="sxs-lookup"><span data-stu-id="25dc0-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="25dc0-113">Al hacer clic en el botón **Revisar**, aparece la hoja **Iniciar revisión de acceso**.</span><span class="sxs-lookup"><span data-stu-id="25dc0-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="25dc0-114">En esta hoja, va a configurar la revisión con un nombre y un límite de tiempo, elija un rol para revisar y decida quién llevará a cabo la revisión.</span><span class="sxs-lookup"><span data-stu-id="25dc0-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Inicio de una revisión de acceso: captura de pantalla][1]

### <a name="configure-the-review"></a><span data-ttu-id="25dc0-116">Configuración de la revisión</span><span class="sxs-lookup"><span data-stu-id="25dc0-116">Configure the review</span></span>
<span data-ttu-id="25dc0-117">Para crear una revisión de acceso, necesitará nombrarla y establecer una fecha de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="25dc0-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Configuración de una revisión: captura de pantalla][2]

<span data-ttu-id="25dc0-119">Asegúrese de que la longitud de la revisión sea lo suficientemente larga para que los usuarios la completen.</span><span class="sxs-lookup"><span data-stu-id="25dc0-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="25dc0-120">Si finaliza antes de la fecha de finalización, siempre puede detener pronto la revisión.</span><span class="sxs-lookup"><span data-stu-id="25dc0-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="25dc0-121">Elija un rol para su revisión</span><span class="sxs-lookup"><span data-stu-id="25dc0-121">Choose a role to review</span></span>
<span data-ttu-id="25dc0-122">Cada revisión se centra solo en un rol.</span><span class="sxs-lookup"><span data-stu-id="25dc0-122">Each review focuses on only one role.</span></span> <span data-ttu-id="25dc0-123">A menos que iniciara la revisión de acceso desde una hoja de rol específica, deberá elegir un rol ahora.</span><span class="sxs-lookup"><span data-stu-id="25dc0-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="25dc0-124">Vaya a **Revisar la pertenencia al rol**</span><span class="sxs-lookup"><span data-stu-id="25dc0-124">Navigate to **Review role membership**</span></span>
   
    ![Revisión de pertenencia al rol: captura de pantalla][3]
2. <span data-ttu-id="25dc0-126">Elija un rol de la lista.</span><span class="sxs-lookup"><span data-stu-id="25dc0-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="25dc0-127">Decida quién llevará a cabo la revisión</span><span class="sxs-lookup"><span data-stu-id="25dc0-127">Decide who will perform the review</span></span>
<span data-ttu-id="25dc0-128">Hay tres opciones para realizar una revisión.</span><span class="sxs-lookup"><span data-stu-id="25dc0-128">There are three options for performing a review.</span></span> <span data-ttu-id="25dc0-129">Puede asignar la revisión a otra persona para que la complete, puede hacerlo usted mismo o hacer que cada usuario revise su propio acceso.</span><span class="sxs-lookup"><span data-stu-id="25dc0-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="25dc0-130">Vaya a **Seleccionar revisores**</span><span class="sxs-lookup"><span data-stu-id="25dc0-130">Navigate to **Select reviewers**</span></span>
   
    ![Selección de revisores: captura de pantalla][4]
2. <span data-ttu-id="25dc0-132">Elija una de las opciones:</span><span class="sxs-lookup"><span data-stu-id="25dc0-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="25dc0-133">**Seleccionar revisor**: utilice esta opción si no sabe quién requiere acceso.</span><span class="sxs-lookup"><span data-stu-id="25dc0-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="25dc0-134">Con esta opción, puede asignar la revisión a un propietario de recursos o al administrador de grupos.</span><span class="sxs-lookup"><span data-stu-id="25dc0-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="25dc0-135">**Yo**: resulta útil si desea obtener una vista previa de cómo funcionan las revisiones de acceso o desea revisar en nombre de personas que no pueden hacerlo.</span><span class="sxs-lookup"><span data-stu-id="25dc0-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="25dc0-136">**Revisión de los propios miembros**: utilice esta opción para que los usuarios revisen ellos mismos sus propias asignaciones de roles.</span><span class="sxs-lookup"><span data-stu-id="25dc0-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="25dc0-137">Inicio de la revisión</span><span class="sxs-lookup"><span data-stu-id="25dc0-137">Start the review</span></span>
<span data-ttu-id="25dc0-138">Por último, tiene la opción de requerir que los usuarios proporcionen un motivo si aprueban su acceso.</span><span class="sxs-lookup"><span data-stu-id="25dc0-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="25dc0-139">Agregue una descripción de la revisión si lo desea y seleccione **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="25dc0-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="25dc0-140">Asegúrese de que permiten a los usuarios saber que hay una revisión de acceso esperando para ellos y [cómo realizar una revisión de acceso](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="25dc0-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="25dc0-141">Administración de la revisión de acceso</span><span class="sxs-lookup"><span data-stu-id="25dc0-141">Manage the access review</span></span>
<span data-ttu-id="25dc0-142">Puede seguir el progreso de las revisiones a medida que los revisores las realizan en el panel de PIM de Azure AD, en la sección de revisiones de acceso.</span><span class="sxs-lookup"><span data-stu-id="25dc0-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="25dc0-143">Los derechos de acceso no se cambian en el directorio hasta que [la revisión finaliza](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="25dc0-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="25dc0-144">Hasta que termine el período de revisión, puede recordar a los usuarios completar su revisión o detener la revisión antes desde la sección de revisiones de acceso.</span><span class="sxs-lookup"><span data-stu-id="25dc0-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="25dc0-145">Tabla de contenido de PIM</span><span class="sxs-lookup"><span data-stu-id="25dc0-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
