---
title: portal de aaaAzure para las directivas de recursos | Documentos de Microsoft
description: "Describe cómo toouse toocreate de portal de Azure y administrar las directivas del Administrador de recursos. Se pueden aplicar directivas en grupos de suscripción o el recurso de Hola."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="aa5b2-104">Usar tooassign de portal de Azure y administrar las directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="aa5b2-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="aa5b2-105">Hola portal de Azure permite las suscripciones y se tooassign directivas tooresource grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="aa5b2-106">interfaz de usuario de Hello resulta fácil tooselect directiva de Hola que desee tooassign y especificar valores de parámetro para esa configuración de directiva de directiva toocustomize Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="aa5b2-107">tooassign una directiva mediante el portal de hello, definición de directiva de hello ya debe existir en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="aa5b2-108">La suscripción tiene varias definiciones de directivas integradas que están listas para que los grupos de tooresource tooassign o suscripciones.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="aa5b2-109">Verá estas directivas integradas y directivas personalizadas que ha definido cuando mediante directivas de hello tooassign portal.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="aa5b2-110">Para una introducción toopolicies y cómo personalizar la directiva toodefine, consulte [información general de directivas de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="aa5b2-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="aa5b2-111">Todos los recursos secundarios heredan las directivas.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="aa5b2-112">Por lo tanto, si una directiva aplicada tooa grupo de recursos, es aplicable tooall recursos de hello en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="aa5b2-113">En este artículo, el término de hello **ámbito** hace referencia toohello grupo de recursos o suscripción que se asigna la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="aa5b2-114">Las directivas se evalúan al crear y actualizar los recursos (operaciones PUT y PATCH).</span><span class="sxs-lookup"><span data-stu-id="aa5b2-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="aa5b2-115">Asignación de una directiva</span><span class="sxs-lookup"><span data-stu-id="aa5b2-115">Assign a policy</span></span>

1. <span data-ttu-id="aa5b2-116">tooassign un tooeither directiva un grupo de recursos o suscripción, seleccione ese grupo de recursos o suscripción.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="aa5b2-117">En configuración de hello, seleccione **directivas**.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-117">In hello settings, select **Policies**.</span></span>

   ![seleccionar directivas](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="aa5b2-119">Seleccione una asignación de directiva para este ámbito, toocreate **Agregar asignación de**.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![agregar asignación](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="aa5b2-121">Seleccione la directiva de hello desea tooassign.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="aa5b2-122">Incluso si no ha agregado ninguna suscripción de tooyour de definiciones de directivas, consulte directivas integradas de Hola que están disponibles para la asignación.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="aa5b2-123">Estas directivas integradas abarcan muchos escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-123">These built-in policies cover many common scenarios.</span></span>

   ![seleccionar definición](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="aa5b2-125">Después de seleccionar una directiva, verá una descripción de la directiva de Hola y los parámetros de la directiva.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="aa5b2-126">Por ejemplo, hello siguiente imagen muestra hello **permitido ubicaciones** parámetro, que es necesario para la directiva de Hola que restringe las ubicaciones disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![mostrar parámetros](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="aa5b2-128">A través de la interfaz de usuario de hello, seleccione hello toospecify de valores para parámetros de la directiva de hello (por ejemplo, ubicaciones de Hola que pueden usarse para la implementación).</span><span class="sxs-lookup"><span data-stu-id="aa5b2-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![seleccionar valores de parámetros](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="aa5b2-130">Proporcione valores de hello otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="aa5b2-131">ámbito de Hola se asigna automáticamente en función de hoja de Hola que seleccionó al iniciar la asignación de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="aa5b2-132">Seleccione **Aceptar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-132">Select **OK** when done.</span></span>

   ![definir parámetros](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="aa5b2-134">Se ha asignado la directiva de hello toohello especifica el ámbito.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="aa5b2-135">Visualización de asignaciones de directiva</span><span class="sxs-lookup"><span data-stu-id="aa5b2-135">View policy assignments</span></span>

<span data-ttu-id="aa5b2-136">Después de asignar una directiva, se observa en la lista de Hola de directivas para ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="aa5b2-137">Hola **detalles** ficha muestra un resumen de la asignación de directivas Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![mostrar detalles](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="aa5b2-139">Hola **regla de asignación** ficha muestra hello JSON para la definición de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![mostrar regla de asignación](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="aa5b2-141">Cambio de una asignación de directiva existente</span><span class="sxs-lookup"><span data-stu-id="aa5b2-141">Change an existing policy assignment</span></span>

<span data-ttu-id="aa5b2-142">toochange una directiva, seleccione **Editar asignación de** o **eliminar**</span><span class="sxs-lookup"><span data-stu-id="aa5b2-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![editar o eliminar asignación](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="aa5b2-144">Asignación de directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="aa5b2-144">Assign custom policies</span></span>

<span data-ttu-id="aa5b2-145">Si ha definido las directivas personalizadas en su suscripción, esas directivas están disponibles para la asignación mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa5b2-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="aa5b2-146">Delante de dichas políticas aparece **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="aa5b2-146">Those policies are prefaced with **[Custom]**</span></span>

![directivas personalizadas](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="aa5b2-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa5b2-148">Next steps</span></span>
* <span data-ttu-id="aa5b2-149">toolearn acerca de la sintaxis JSON de Hola para definir las directivas, consulte [información general de directivas de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="aa5b2-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="aa5b2-150">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="aa5b2-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="aa5b2-151">esquema de la directiva de Hola se publica en [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="aa5b2-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

