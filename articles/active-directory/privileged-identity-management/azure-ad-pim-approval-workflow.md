---
title: "los flujos de trabajo de aprobación de administración de identidad con privilegios de aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre los flujos de trabajo de aprobación de Privileged Identity Management (PIM)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="e925b-103">Aprobaciones (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="e925b-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="e925b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e925b-104">Overview</span></span>

<span data-ttu-id="e925b-105">Con aprobaciones de Privileged Identity Management, puede configurar la aprobación de toorequire de roles para la activación y elija uno o varios usuarios o grupos de aprobadores como delegados.</span><span class="sxs-lookup"><span data-stu-id="e925b-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="e925b-106">Sigan leyendo toolearn cómo tooconfigure roles y seleccione aprobadores.</span><span class="sxs-lookup"><span data-stu-id="e925b-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="e925b-107">Tenga en cuenta que esta característica está aún en desarrollo, por lo que puede encontrar errores.</span><span class="sxs-lookup"><span data-stu-id="e925b-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="e925b-108">funcionalidad de Hello, incluyendo el texto y convenciones de nomenclatura están sujetos a cambios y no deben considerarse finales.</span><span class="sxs-lookup"><span data-stu-id="e925b-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="e925b-109">Terminología clave</span><span class="sxs-lookup"><span data-stu-id="e925b-109">Key Terminology</span></span>

<span data-ttu-id="e925b-110">*Elegibles de rol de usuario* : un rol elegibles trata de un usuario dentro de su organización que se ha asignado el rol de Azure AD tooan como derecho (rol requiere activación).</span><span class="sxs-lookup"><span data-stu-id="e925b-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="e925b-111">*Aprobador delegado*: se trata de una o varias personas o grupos de Azure AD responsables de la aprobación de las solicitudes de activación de roles.</span><span class="sxs-lookup"><span data-stu-id="e925b-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="e925b-112">Escenarios</span><span class="sxs-lookup"><span data-stu-id="e925b-112">Scenarios</span></span>

<span data-ttu-id="e925b-113">vista previa privada de Hello admite Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="e925b-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="e925b-114">**Como administrador de rol con privilegios (PRA), puede:**</span><span class="sxs-lookup"><span data-stu-id="e925b-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="e925b-115">Habilitar la aprobación de roles específicos</span><span class="sxs-lookup"><span data-stu-id="e925b-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="e925b-116">Especifique solicitudes de tooapprove de usuarios o grupos de aprobador</span><span class="sxs-lookup"><span data-stu-id="e925b-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="e925b-117">Ver el historial de solicitudes y aprobaciones de todos los roles con privilegios</span><span class="sxs-lookup"><span data-stu-id="e925b-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="e925b-118">**Como un aprobador designado, puede:**</span><span class="sxs-lookup"><span data-stu-id="e925b-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="e925b-119">Ver aprobaciones o solicitudes pendientes</span><span class="sxs-lookup"><span data-stu-id="e925b-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="e925b-120">Aprobar o rechazar solicitudes de elevación de rol (de forma individual o masiva)</span><span class="sxs-lookup"><span data-stu-id="e925b-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="e925b-121">Proporcionar una justificación de la aprobación o el rechazo</span><span class="sxs-lookup"><span data-stu-id="e925b-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="e925b-122">**Como usuario de rol apto, puede:**</span><span class="sxs-lookup"><span data-stu-id="e925b-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="e925b-123">Solicitar la activación de un rol que requiere aprobación</span><span class="sxs-lookup"><span data-stu-id="e925b-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="e925b-124">ver el estado de saludo de su tooactivate de solicitud</span><span class="sxs-lookup"><span data-stu-id="e925b-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="e925b-125">Completar la tarea en Azure AD si la activación se ha aprobado</span><span class="sxs-lookup"><span data-stu-id="e925b-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="e925b-126">Navegación</span><span class="sxs-lookup"><span data-stu-id="e925b-126">Navigation</span></span>

<span data-ttu-id="e925b-127">Hemos actualizado aprobaciones de hello navegación toosupport</span><span class="sxs-lookup"><span data-stu-id="e925b-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="e925b-128">página de aterrizaje de Hello predeterminada proporciona un acceso cómodo tooinformation sobre hello y PIM nueva documentación de aprobaciones.</span><span class="sxs-lookup"><span data-stu-id="e925b-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="e925b-129">También se ha agregado una sección nueva para todos los usuarios de PIM, "My Audit History" (Mi historial de auditoría).</span><span class="sxs-lookup"><span data-stu-id="e925b-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="e925b-130">Aquí puede encontrar todas las identidades de tooyour relevantes de información Hola.</span><span class="sxs-lookup"><span data-stu-id="e925b-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="e925b-131">Esto incluye todas las solicitudes pendientes y completadas, ninguna decisión relativa al que haya realizado sobre las solicitudes de Hola para resolver y todas sus activaciones rol pasados en una ubicación conveniente.</span><span class="sxs-lookup"><span data-stu-id="e925b-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="e925b-132">Habilitar la aprobación de roles específicos</span><span class="sxs-lookup"><span data-stu-id="e925b-132">Enable approval for specific roles</span></span>

<span data-ttu-id="e925b-133">aprobación de tooenable para un rol específico, primero seleccione Roles del directorio de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e925b-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="e925b-134">Busque y seleccione Configuración Hola de navegación izquierdo de Roles de directorio</span><span class="sxs-lookup"><span data-stu-id="e925b-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="e925b-135">Seleccione Roles con privilegios:</span><span class="sxs-lookup"><span data-stu-id="e925b-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="e925b-136">Seleccione "Activar" Hola requieren la sección de aprobación:</span><span class="sxs-lookup"><span data-stu-id="e925b-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="e925b-137">Una vez habilitada, hoja de hello expandirá hello tooshow detalles siguientes:</span><span class="sxs-lookup"><span data-stu-id="e925b-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="e925b-138">Si no especifica los aprobadores, hello PRA(s) se convierten en hello aprobadores de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e925b-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="e925b-139">PRA(s) sería necesario tooapprove activación todas las solicitudes para este rol.</span><span class="sxs-lookup"><span data-stu-id="e925b-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="e925b-140">Especifique solicitudes de tooapprove de usuarios o grupos de aprobador</span><span class="sxs-lookup"><span data-stu-id="e925b-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="e925b-141">aprobación de toodelegate, haga clic en la opción de hello demasiado "Seleccionar aprobadores":</span><span class="sxs-lookup"><span data-stu-id="e925b-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="e925b-142">Cuando se carga la hoja de aprobadores seleccione hello, puede buscar un usuario o grupo específico mediante la barra de búsqueda de hello en la parte superior de Hola o seleccionar de lista rellenada previamente hello, a continuación, haga clic en "Seleccionar" cuando finaliza:</span><span class="sxs-lookup"><span data-stu-id="e925b-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="e925b-143">Nota: puede seleccionar varios usuarios o grupos a la vez.</span><span class="sxs-lookup"><span data-stu-id="e925b-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="e925b-144">La selección aparecerá en lista de Hola de aprobadores seleccionados tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="e925b-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="e925b-145">tooremove aprobador, simplemente haga clic en siguiente tootheir nombre del botón Quitar del saludo.</span><span class="sxs-lookup"><span data-stu-id="e925b-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="e925b-146">tooadd aprobadores adicionales, el proceso de repetición Hola.</span><span class="sxs-lookup"><span data-stu-id="e925b-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="e925b-147">Ver el historial de solicitudes y aprobaciones de todos los roles con privilegios</span><span class="sxs-lookup"><span data-stu-id="e925b-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="e925b-148">historial de solicitud y aprobación de tooview para los roles con todos los privilegios, seleccione historial de auditoría desde el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="e925b-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="e925b-149">Puede ordenar los datos de Hola por acción y busque "Activación"aprobado"</span><span class="sxs-lookup"><span data-stu-id="e925b-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="e925b-150">Ver aprobaciones o solicitudes pendientes</span><span class="sxs-lookup"><span data-stu-id="e925b-150">View pending approvals (requests)</span></span>

<span data-ttu-id="e925b-151">Como un aprobador delegado, recibirá notificaciones por correo electrónico cuando una solicitud está pendiente de aprobación.</span><span class="sxs-lookup"><span data-stu-id="e925b-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="e925b-152">tooview estas solicitudes en el portal PIM de hello, desde la ficha Panel (en la nueva navegación hello) seleccione Hola "aprobación solicitudes pendientes" hello la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="e925b-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="e925b-153">Ahí se mostrará una lista de solicitudes pendientes de aprobación:</span><span class="sxs-lookup"><span data-stu-id="e925b-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="e925b-154">Aprobar o rechazar solicitudes de elevación de rol (de forma individual o masiva)</span><span class="sxs-lookup"><span data-stu-id="e925b-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="e925b-155">Seleccione las solicitudes de hello desea tooapprove o denegar y haga clic en botón hello en la barra de acciones que se corresponde con su decisión:</span><span class="sxs-lookup"><span data-stu-id="e925b-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="e925b-156">Proporcionar una justificación de la aprobación o el rechazo</span><span class="sxs-lookup"><span data-stu-id="e925b-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="e925b-157">Esto abre una nueva tooapprove hoja o denegar varias solicitudes a la vez.</span><span class="sxs-lookup"><span data-stu-id="e925b-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="e925b-158">Especificar una justificación para su decisión, y haga clic en Aprobar (o denegar) en parte inferior de Hola u hoja hello:</span><span class="sxs-lookup"><span data-stu-id="e925b-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="e925b-159">Cuando se completa el proceso de solicitud de hello, símbolo de estado de hello reflejará la decisión adoptada (en este ejemplo, la decisión de hello es aprobar):</span><span class="sxs-lookup"><span data-stu-id="e925b-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="e925b-160">Solicitar la activación de un rol que requiere aprobación</span><span class="sxs-lookup"><span data-stu-id="e925b-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="e925b-161">Solicitar la activación de un rol que requiere la aprobación se puede iniciar desde navegación PIM antiguo de Hola o navegación nueva hello, como proceso de Hola para sigue siendo de activación de rol Hola igual.</span><span class="sxs-lookup"><span data-stu-id="e925b-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="e925b-162">Simplemente seleccione un rol de la lista de Hola de roles para activar:</span><span class="sxs-lookup"><span data-stu-id="e925b-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="e925b-163">Si un rol con privilegios requiere Multi-Factor Authentication, se le pedirá que complete esa tarea en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="e925b-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="e925b-164">Cuando haya terminado, haga clic en Activar y proporcione una justificación (si es necesario):</span><span class="sxs-lookup"><span data-stu-id="e925b-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="e925b-165">solicitante de Hello verá una notificación que Hola solicitud está pendiente de aprobación:</span><span class="sxs-lookup"><span data-stu-id="e925b-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="e925b-166">Ver el estado de saludo de su tooactivate de solicitud</span><span class="sxs-lookup"><span data-stu-id="e925b-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="e925b-167">Ver el estado de saludo de una solicitud pendiente tooactivate debe tener acceso desde el nuevo panel de navegación.</span><span class="sxs-lookup"><span data-stu-id="e925b-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="e925b-168">Desde la barra de navegación izquierda de hello, seleccione la pestaña de "Mis solicitudes" de hello:</span><span class="sxs-lookup"><span data-stu-id="e925b-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="e925b-169">estado de la solicitud de saludo predeterminado es demasiado "Pendiente", pero puede alternar toosee todos o solicitudes denegadas.</span><span class="sxs-lookup"><span data-stu-id="e925b-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="e925b-170">Completar la tarea en Azure AD si la activación se ha aprobado</span><span class="sxs-lookup"><span data-stu-id="e925b-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="e925b-171">Una vez aprobada la solicitud de hello, rol de hello está activo y se puede continuar con cualquier trabajo que requiere este rol.</span><span class="sxs-lookup"><span data-stu-id="e925b-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="e925b-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e925b-172">Next steps</span></span>

<span data-ttu-id="e925b-173">Sus comentarios son valiosos toous.</span><span class="sxs-lookup"><span data-stu-id="e925b-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="e925b-174">Póngase tooshare libre ni comentario con nosotros aquí.</span><span class="sxs-lookup"><span data-stu-id="e925b-174">Please feel free tooshare comments or feedback with us here!</span></span>
