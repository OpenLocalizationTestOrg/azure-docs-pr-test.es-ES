---
title: "Flujos de trabajo de aprobación de Azure Privileged Identity Management | Microsoft Docs"
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
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="a34ea-103">Aprobaciones (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a34ea-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="a34ea-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a34ea-104">Overview</span></span>

<span data-ttu-id="a34ea-105">Con las aprobaciones de Privileged Identity Management, puede configurar roles para requerir la aprobación para la activación y elegir uno o varios usuarios o grupos como aprobadores delegados.</span><span class="sxs-lookup"><span data-stu-id="a34ea-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="a34ea-106">Siga leyendo para obtener información sobre cómo configurar roles y seleccionar aprobadores.</span><span class="sxs-lookup"><span data-stu-id="a34ea-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="a34ea-107">Tenga en cuenta que esta característica está aún en desarrollo, por lo que puede encontrar errores.</span><span class="sxs-lookup"><span data-stu-id="a34ea-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="a34ea-108">La funcionalidad, incluidas las convenciones de nomenclatura y de texto, está sujeta a modificaciones, por lo que no se puede considerar como definitiva.</span><span class="sxs-lookup"><span data-stu-id="a34ea-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="a34ea-109">Terminología clave</span><span class="sxs-lookup"><span data-stu-id="a34ea-109">Key Terminology</span></span>

<span data-ttu-id="a34ea-110">*Usuario de rol apto*: se trata de un usuario de la organización asignado a un rol de Azure AD como apto (el rol requiere activación).</span><span class="sxs-lookup"><span data-stu-id="a34ea-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="a34ea-111">*Aprobador delegado*: se trata de una o varias personas o grupos de Azure AD responsables de la aprobación de las solicitudes de activación de roles.</span><span class="sxs-lookup"><span data-stu-id="a34ea-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="a34ea-112">Escenarios</span><span class="sxs-lookup"><span data-stu-id="a34ea-112">Scenarios</span></span>

<span data-ttu-id="a34ea-113">La versión preliminar privada admite los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="a34ea-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="a34ea-114">**Como administrador de rol con privilegios (PRA), puede:**</span><span class="sxs-lookup"><span data-stu-id="a34ea-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="a34ea-115">Habilitar la aprobación de roles específicos</span><span class="sxs-lookup"><span data-stu-id="a34ea-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="a34ea-116">Especificar usuarios y grupos de aprobadores para la aprobación de solicitudes</span><span class="sxs-lookup"><span data-stu-id="a34ea-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="a34ea-117">Ver el historial de solicitudes y aprobaciones de todos los roles con privilegios</span><span class="sxs-lookup"><span data-stu-id="a34ea-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="a34ea-118">**Como un aprobador designado, puede:**</span><span class="sxs-lookup"><span data-stu-id="a34ea-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="a34ea-119">Ver aprobaciones o solicitudes pendientes</span><span class="sxs-lookup"><span data-stu-id="a34ea-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="a34ea-120">Aprobar o rechazar solicitudes de elevación de rol (de forma individual o masiva)</span><span class="sxs-lookup"><span data-stu-id="a34ea-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="a34ea-121">Proporcionar una justificación de la aprobación o el rechazo</span><span class="sxs-lookup"><span data-stu-id="a34ea-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="a34ea-122">**Como usuario de rol apto, puede:**</span><span class="sxs-lookup"><span data-stu-id="a34ea-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="a34ea-123">Solicitar la activación de un rol que requiere aprobación</span><span class="sxs-lookup"><span data-stu-id="a34ea-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="a34ea-124">Ver el estado de la solicitud de activación</span><span class="sxs-lookup"><span data-stu-id="a34ea-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="a34ea-125">Completar la tarea en Azure AD si la activación se ha aprobado</span><span class="sxs-lookup"><span data-stu-id="a34ea-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="a34ea-126">Navegación</span><span class="sxs-lookup"><span data-stu-id="a34ea-126">Navigation</span></span>

<span data-ttu-id="a34ea-127">Se ha actualizado la navegación para admitir las aprobaciones</span><span class="sxs-lookup"><span data-stu-id="a34ea-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="a34ea-128">En la página de aterrizaje predeterminada se ofrece un acceso conveniente a información sobre PIM y a la documentación nueva sobre aprobaciones.</span><span class="sxs-lookup"><span data-stu-id="a34ea-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="a34ea-129">También se ha agregado una sección nueva para todos los usuarios de PIM, "My Audit History" (Mi historial de auditoría).</span><span class="sxs-lookup"><span data-stu-id="a34ea-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="a34ea-130">Aquí puede encontrar toda la información relevante para su identidad.</span><span class="sxs-lookup"><span data-stu-id="a34ea-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="a34ea-131">Se incluyen todas las solicitudes pendientes y completadas, todas las decisiones tomadas en relación con las solicitudes resueltas y todas las activaciones de roles anteriores en una misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="a34ea-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="a34ea-132">Habilitar la aprobación de roles específicos</span><span class="sxs-lookup"><span data-stu-id="a34ea-132">Enable approval for specific roles</span></span>

<span data-ttu-id="a34ea-133">Para habilitar la aprobación de un rol específico, primero seleccione Directory Roles (Roles del directorio) en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="a34ea-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="a34ea-134">Busque y seleccione la configuración en Directory Roles (Roles del directorio) en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="a34ea-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="a34ea-135">Seleccione Roles con privilegios:</span><span class="sxs-lookup"><span data-stu-id="a34ea-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="a34ea-136">Seleccione "Activado" en la sección Requerir aprobación:</span><span class="sxs-lookup"><span data-stu-id="a34ea-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="a34ea-137">Una vez habilitada esta opción, la hoja se expandirá para mostrar los detalles siguientes:</span><span class="sxs-lookup"><span data-stu-id="a34ea-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="a34ea-138">Si NO especifica ningún aprobador, el PRA será el aprobador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a34ea-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="a34ea-139">PRA deberá aprobar TODAS las solicitudes de activación de este rol.</span><span class="sxs-lookup"><span data-stu-id="a34ea-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="a34ea-140">Especificar usuarios y grupos de aprobadores para la aprobación de solicitudes</span><span class="sxs-lookup"><span data-stu-id="a34ea-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="a34ea-141">Para delegar la aprobación, haga clic en la opción "Seleccionar aprobadores":</span><span class="sxs-lookup"><span data-stu-id="a34ea-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="a34ea-142">Cuando se carga la hoja Seleccionar aprobadores, debe buscar un usuario o grupo específico con la barra de búsqueda que se encuentra en la parte superior o seleccionarlo en la lista rellenada previamente y, después, hacer clic en "Seleccionar" cuando haya terminado:</span><span class="sxs-lookup"><span data-stu-id="a34ea-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="a34ea-143">Nota: puede seleccionar varios usuarios o grupos a la vez.</span><span class="sxs-lookup"><span data-stu-id="a34ea-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="a34ea-144">La selección aparecerá en la lista de los aprobadores seleccionados tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a34ea-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="a34ea-145">Para quitar un aprobador, simplemente haga clic en el botón Remove (Quitar) junto al nombre.</span><span class="sxs-lookup"><span data-stu-id="a34ea-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="a34ea-146">Para agregar aprobadores adicionales, repita el proceso.</span><span class="sxs-lookup"><span data-stu-id="a34ea-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="a34ea-147">Ver el historial de solicitudes y aprobaciones de todos los roles con privilegios</span><span class="sxs-lookup"><span data-stu-id="a34ea-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="a34ea-148">Para ver el historial de solicitudes y aprobaciones de todos los roles con privilegios, seleccione Historial de auditoría en el panel:</span><span class="sxs-lookup"><span data-stu-id="a34ea-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="a34ea-149">Puede ordenar los datos por acción y buscar el texto "Activación aprobada".</span><span class="sxs-lookup"><span data-stu-id="a34ea-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="a34ea-150">Ver aprobaciones o solicitudes pendientes</span><span class="sxs-lookup"><span data-stu-id="a34ea-150">View pending approvals (requests)</span></span>

<span data-ttu-id="a34ea-151">Como un aprobador delegado, recibirá notificaciones por correo electrónico cuando una solicitud está pendiente de aprobación.</span><span class="sxs-lookup"><span data-stu-id="a34ea-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="a34ea-152">Para ver estas solicitudes en el portal de PIM, en el nuevo panel de navegación, seleccione la pestaña "Solicitudes de aprobación pendientes" en la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="a34ea-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="a34ea-153">Ahí se mostrará una lista de solicitudes pendientes de aprobación:</span><span class="sxs-lookup"><span data-stu-id="a34ea-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="a34ea-154">Aprobar o rechazar solicitudes de elevación de rol (de forma individual o masiva)</span><span class="sxs-lookup"><span data-stu-id="a34ea-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="a34ea-155">Seleccione las solicitudes que desea aprobar o rechazar y haga clic en el botón de la barra de acciones correspondiente a su decisión:</span><span class="sxs-lookup"><span data-stu-id="a34ea-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="a34ea-156">Proporcionar una justificación de la aprobación o el rechazo</span><span class="sxs-lookup"><span data-stu-id="a34ea-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="a34ea-157">Se abrirá una nueva hoja para aprobar o rechazar varias solicitudes a la vez.</span><span class="sxs-lookup"><span data-stu-id="a34ea-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="a34ea-158">Escriba una justificación de la decisión que ha tomado y haga clic en los botones para aprobar o rechazar en la parte inferior de la hoja:</span><span class="sxs-lookup"><span data-stu-id="a34ea-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="a34ea-159">Una vez completado el proceso de solicitud, el símbolo de estado reflejará la decisión adoptada (en este ejemplo, la decisión es aprobar):</span><span class="sxs-lookup"><span data-stu-id="a34ea-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="a34ea-160">Solicitar la activación de un rol que requiere aprobación</span><span class="sxs-lookup"><span data-stu-id="a34ea-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="a34ea-161">La solicitud de activación de un rol que requiere aprobación puede iniciarse desde el panel de navegación de PIM antiguo o desde el nuevo panel de navegación, ya que el proceso de activación de roles sigue siendo el mismo.</span><span class="sxs-lookup"><span data-stu-id="a34ea-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="a34ea-162">Solo tiene que seleccionar un rol en la lista de roles para activarlo:</span><span class="sxs-lookup"><span data-stu-id="a34ea-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="a34ea-163">Si un rol con privilegios requiere Multi-Factor Authentication, se le pedirá que complete esa tarea en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="a34ea-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="a34ea-164">Cuando haya terminado, haga clic en Activar y proporcione una justificación (si es necesario):</span><span class="sxs-lookup"><span data-stu-id="a34ea-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="a34ea-165">El solicitante verá una notificación que indica que la solicitud está pendiente de aprobación:</span><span class="sxs-lookup"><span data-stu-id="a34ea-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="a34ea-166">Ver el estado de la solicitud de activación</span><span class="sxs-lookup"><span data-stu-id="a34ea-166">View the status of your request to activate</span></span>

<span data-ttu-id="a34ea-167">Para ver el estado de una solicitud pendiente de activación, es necesario acceder desde el nuevo panel de navegación.</span><span class="sxs-lookup"><span data-stu-id="a34ea-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="a34ea-168">En la barra de navegación de la izquierda, seleccione la pestaña "My Requests" (Mis solicitudes):</span><span class="sxs-lookup"><span data-stu-id="a34ea-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="a34ea-169">El estado de solicitud predeterminado es "Pendiente", pero puede alternar para ver todas las solicitudes o solo las solicitudes rechazadas.</span><span class="sxs-lookup"><span data-stu-id="a34ea-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="a34ea-170">Completar la tarea en Azure AD si la activación se ha aprobado</span><span class="sxs-lookup"><span data-stu-id="a34ea-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="a34ea-171">Una vez aprobada la solicitud, el rol se activa y puede continuar con cualquier tarea que requiere este rol.</span><span class="sxs-lookup"><span data-stu-id="a34ea-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="a34ea-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a34ea-172">Next steps</span></span>

<span data-ttu-id="a34ea-173">Sus comentarios son muy importantes,</span><span class="sxs-lookup"><span data-stu-id="a34ea-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="a34ea-174">así que no dude en compartirlos con nosotros aquí.</span><span class="sxs-lookup"><span data-stu-id="a34ea-174">Please feel free to share comments or feedback with us here!</span></span>
