---
title: "aaaHow toostart una revisión de acceso | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate revisar de un acceso de identidades con privilegios con hello aplicación Privileged Identity Management de Azure."
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
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="aeac4-103">¿Cómo toostart un acceso Revise en Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="aeac4-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="aeac4-104">Las asignaciones de roles se convierten en "obsoletas" cuando los usuarios tienen acceso con privilegios que ya no necesitan.</span><span class="sxs-lookup"><span data-stu-id="aeac4-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="aeac4-105">En orden tooreduce riesgo de hello asociado con estas asignaciones de funciones obsoletas, los administradores de roles con privilegios con regularidad deben revisar los roles de Hola que se les ha asignado a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="aeac4-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="aeac4-106">Este documento describen los pasos de hello para iniciar una revisión de acceso en Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="aeac4-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="aeac4-107">Inicio de una revisión de acceso</span><span class="sxs-lookup"><span data-stu-id="aeac4-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="aeac4-108">Si aún no lo ha agregado tooyour panel de hello PIM aplicación Hola portal de Azure, consulte los pasos de hello en [Getting Started with Privileged Identity Management de Azure](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="aeac4-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="aeac4-109">Desde la página principal de hello PIM aplicación, hay tres toostart formas una revisión de acceso:</span><span class="sxs-lookup"><span data-stu-id="aeac4-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="aeac4-110">**Revisiones de acceso** > **Agregar**</span><span class="sxs-lookup"><span data-stu-id="aeac4-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="aeac4-111">Botón **Roles** > **Revisar**</span><span class="sxs-lookup"><span data-stu-id="aeac4-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="aeac4-112">Hola seleccione rol específico toobe revisado de lista de roles de hello > **revisión** botón</span><span class="sxs-lookup"><span data-stu-id="aeac4-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="aeac4-113">Al hacer clic en hello **revisar** button, hello **iniciar una revisión de acceso** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="aeac4-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="aeac4-114">En esta hoja, está continuo tooconfigure Hola revisión con un nombre y límite de tiempo, elija un rol tooreview y decidir quién llevará a cabo revisión Hola.</span><span class="sxs-lookup"><span data-stu-id="aeac4-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Inicio de una revisión de acceso: captura de pantalla][1]

### <a name="configure-hello-review"></a><span data-ttu-id="aeac4-116">Configurar la revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="aeac4-116">Configure hello review</span></span>
<span data-ttu-id="aeac4-117">toocreate un acceso revisar, deberá tooname y establezca una fecha de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="aeac4-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Configuración de una revisión: captura de pantalla][2]

<span data-ttu-id="aeac4-119">Asegúrese de longitud de Hola de hello revisar tiempo suficiente para que los usuarios toocomplete.</span><span class="sxs-lookup"><span data-stu-id="aeac4-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="aeac4-120">Si finaliza antes de la fecha de finalización de hello, siempre puede detener revisión Hola al principio.</span><span class="sxs-lookup"><span data-stu-id="aeac4-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="aeac4-121">Elija un rol tooreview</span><span class="sxs-lookup"><span data-stu-id="aeac4-121">Choose a role tooreview</span></span>
<span data-ttu-id="aeac4-122">Cada revisión se centra solo en un rol.</span><span class="sxs-lookup"><span data-stu-id="aeac4-122">Each review focuses on only one role.</span></span> <span data-ttu-id="aeac4-123">A menos que iniciara Hola revisión de acceso de una hoja de rol específico, deberá toochoose un rol ahora.</span><span class="sxs-lookup"><span data-stu-id="aeac4-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="aeac4-124">Navegue demasiado**revisar la pertenencia a roles**</span><span class="sxs-lookup"><span data-stu-id="aeac4-124">Navigate too**Review role membership**</span></span>
   
    ![Revisión de pertenencia al rol: captura de pantalla][3]
2. <span data-ttu-id="aeac4-126">Elegir un rol de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="aeac4-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="aeac4-127">Decidir quién llevará a cabo revisión Hola</span><span class="sxs-lookup"><span data-stu-id="aeac4-127">Decide who will perform hello review</span></span>
<span data-ttu-id="aeac4-128">Hay tres opciones para realizar una revisión.</span><span class="sxs-lookup"><span data-stu-id="aeac4-128">There are three options for performing a review.</span></span> <span data-ttu-id="aeac4-129">Puede asignar Hola revisión toosomeone toocomplete else, puede hacerlo usted mismo, o puede hacer que cada usuario revise su propio acceso.</span><span class="sxs-lookup"><span data-stu-id="aeac4-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="aeac4-130">Navegue demasiado**seleccione revisores**</span><span class="sxs-lookup"><span data-stu-id="aeac4-130">Navigate too**Select reviewers**</span></span>
   
    ![Selección de revisores: captura de pantalla][4]
2. <span data-ttu-id="aeac4-132">Elija una de las opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="aeac4-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="aeac4-133">**Seleccionar revisor**: utilice esta opción si no sabe quién requiere acceso.</span><span class="sxs-lookup"><span data-stu-id="aeac4-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="aeac4-134">Con esta opción, puede asignar el propietario del recurso de hello revisión tooa o grupo administrador toocomplete.</span><span class="sxs-lookup"><span data-stu-id="aeac4-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="aeac4-135">**Me**: útil si desea toopreview cómo access revisa el trabajo, o quiere tooreview en nombre de personas que no se pueden.</span><span class="sxs-lookup"><span data-stu-id="aeac4-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="aeac4-136">**Revisión los miembros a sí mismos**: Utilice esta opción toohave Hola a los usuarios para revisar sus propias asignaciones de roles.</span><span class="sxs-lookup"><span data-stu-id="aeac4-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="aeac4-137">Revisión de Hola de inicio</span><span class="sxs-lookup"><span data-stu-id="aeac4-137">Start hello review</span></span>
<span data-ttu-id="aeac4-138">Por último, tener Hola opción toorequire que los usuarios proporcionen un motivo si aprueba su acceso.</span><span class="sxs-lookup"><span data-stu-id="aeac4-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="aeac4-139">Agregue una descripción de la revisión de hello si lo desea y seleccione **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="aeac4-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="aeac4-140">Asegúrese de que los usuarios saber que hay una revisión de acceso en espera para ellos y mostrarlos en [cómo tooperform un acceso revisar](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="aeac4-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="aeac4-141">Administrar la revisión de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="aeac4-141">Manage hello access review</span></span>
<span data-ttu-id="aeac4-142">Puede seguir el progreso de hello revisores Hola complete sus opiniones en hello panel PIM de Azure AD, en hello access revisa la sección.</span><span class="sxs-lookup"><span data-stu-id="aeac4-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="aeac4-143">Derechos de acceso no se cambiarán en el directorio de hello hasta que [revisión Hola completa](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="aeac4-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="aeac4-144">Hasta que se encuentra el período de revisión de hello sobre, recordar a los usuarios toocomplete su revisión o revisión de Hola de detención al principio contra el acceso de Hola revisiones sección.</span><span class="sxs-lookup"><span data-stu-id="aeac4-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="aeac4-145">Tabla de contenido de PIM</span><span class="sxs-lookup"><span data-stu-id="aeac4-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
