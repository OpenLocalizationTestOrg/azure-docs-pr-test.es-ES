---
title: Azure Portal para directivas de recursos| Microsoft Docs
description: "Describe cómo usar Azure Portal para crear y administrar directivas de Resource Manager. Las directivas pueden aplicarse a la suscripción o a los grupos de recursos."
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="ad245-104">Uso de Azure Portal para asignar y administrar directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="ad245-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="ad245-105">Azure Portal permite asignar directivas de recursos a suscripciones y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad245-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="ad245-106">La interfaz de usuario facilita la selección de la directiva que desea asignar y especificar los valores de los parámetros de dicha directiva para personalizar la configuración de directiva.</span><span class="sxs-lookup"><span data-stu-id="ad245-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="ad245-107">Para asignar una directiva a través del portal, la definición de la directiva debe existir en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ad245-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="ad245-108">La suscripción tiene varias definiciones de directivas integradas que están listas para asignarlas a grupos de recursos o suscripciones.</span><span class="sxs-lookup"><span data-stu-id="ad245-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="ad245-109">Se ven estas directivas integradas y todas las directivas personalizadas que ha definido al usar el portal para asignar directivas.</span><span class="sxs-lookup"><span data-stu-id="ad245-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="ad245-110">Para obtener una introducción a las directivas y a cómo definir una directiva personalizada, consulte [Información general sobre las directivas de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ad245-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="ad245-111">Todos los recursos secundarios heredan las directivas.</span><span class="sxs-lookup"><span data-stu-id="ad245-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="ad245-112">De este modo, si una directiva se aplica a un grupo de recursos, será aplicable a todos los recursos de dicho grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad245-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="ad245-113">En este artículo, el término **ámbito** hace referencia al grupo de recursos o a la suscripción a los que se asigna la directiva.</span><span class="sxs-lookup"><span data-stu-id="ad245-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="ad245-114">Las directivas se evalúan al crear y actualizar los recursos (operaciones PUT y PATCH).</span><span class="sxs-lookup"><span data-stu-id="ad245-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="ad245-115">Asignación de una directiva</span><span class="sxs-lookup"><span data-stu-id="ad245-115">Assign a policy</span></span>

1. <span data-ttu-id="ad245-116">Para asignar una directiva a un grupo de recursos o a una suscripción, selecciónelos.</span><span class="sxs-lookup"><span data-stu-id="ad245-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="ad245-117">En la configuración, seleccione **Directivas**.</span><span class="sxs-lookup"><span data-stu-id="ad245-117">In the settings, select **Policies**.</span></span>

   ![seleccionar directivas](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="ad245-119">Para crear una asignación de directiva para este ámbito, seleccione **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ad245-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![agregar asignación](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="ad245-121">Seleccione la directiva que desea asignar.</span><span class="sxs-lookup"><span data-stu-id="ad245-121">Select the policy you want to assign.</span></span> <span data-ttu-id="ad245-122">Aunque no haya agregado ninguna definición de directiva a su suscripción, verá las directivas integradas disponibles para su asignación.</span><span class="sxs-lookup"><span data-stu-id="ad245-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="ad245-123">Estas directivas integradas abarcan muchos escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="ad245-123">These built-in policies cover many common scenarios.</span></span>

   ![seleccionar definición](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="ad245-125">Después de seleccionar una directiva, verá su descripción y sus parámetros.</span><span class="sxs-lookup"><span data-stu-id="ad245-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="ad245-126">Por ejemplo, la siguiente imagen muestra el parámetro **Ubicaciones permitidas**, que se requiere para la directiva que restringe las ubicaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="ad245-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![mostrar parámetros](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="ad245-128">A través de la interfaz de usuario, seleccione los valores que se especifican para los parámetros de la directiva (como las ubicaciones que se pueden usar para la implementación).</span><span class="sxs-lookup"><span data-stu-id="ad245-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![seleccionar valores de parámetros](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="ad245-130">Especifique los valores de los otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="ad245-130">Provide values for the other parameters.</span></span> <span data-ttu-id="ad245-131">El ámbito se asigna automáticamente en función de la hoja que seleccionó al iniciar la asignación de la directiva.</span><span class="sxs-lookup"><span data-stu-id="ad245-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="ad245-132">Seleccione **Aceptar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="ad245-132">Select **OK** when done.</span></span>

   ![definir parámetros](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="ad245-134">Ha asignado la directiva al ámbito especificado.</span><span class="sxs-lookup"><span data-stu-id="ad245-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="ad245-135">Visualización de asignaciones de directiva</span><span class="sxs-lookup"><span data-stu-id="ad245-135">View policy assignments</span></span>

<span data-ttu-id="ad245-136">Después de asignar una directiva, la verá en la lista de directivas de dicho ámbito.</span><span class="sxs-lookup"><span data-stu-id="ad245-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="ad245-137">La pestaña **Detalles** muestra un resumen de la asignación de la directiva.</span><span class="sxs-lookup"><span data-stu-id="ad245-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![mostrar detalles](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="ad245-139">La pestaña **Regla de asignación** muestra el JSON de la definición de la directiva.</span><span class="sxs-lookup"><span data-stu-id="ad245-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![mostrar regla de asignación](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="ad245-141">Cambio de una asignación de directiva existente</span><span class="sxs-lookup"><span data-stu-id="ad245-141">Change an existing policy assignment</span></span>

<span data-ttu-id="ad245-142">Para cambiar una directiva, seleccione **Editar asignación** o **Eliminar**</span><span class="sxs-lookup"><span data-stu-id="ad245-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![editar o eliminar asignación](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="ad245-144">Asignación de directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="ad245-144">Assign custom policies</span></span>

<span data-ttu-id="ad245-145">Si ha definido directivas personalizadas en su suscripción, estarán disponibles para su asignación a través del portal.</span><span class="sxs-lookup"><span data-stu-id="ad245-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="ad245-146">Delante de dichas políticas aparece **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="ad245-146">Those policies are prefaced with **[Custom]**</span></span>

![directivas personalizadas](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="ad245-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad245-148">Next steps</span></span>
* <span data-ttu-id="ad245-149">Para obtener información acerca de la sintaxis JSON para definir directivas, consulte [Información general sobre las directivas de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ad245-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ad245-150">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ad245-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="ad245-151">El esquema de la directiva está publicado en [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="ad245-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

