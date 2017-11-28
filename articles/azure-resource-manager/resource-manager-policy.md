---
title: Directivas de recursos de Azure | Microsoft Docs
description: "Describe cómo usar las directivas de Azure Resource Manager para asegurarse de que se establecen propiedades de recursos coherentes durante la implementación. Las directivas pueden aplicarse a la suscripción o a los grupos de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="084db-104">Información general sobre las directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="084db-104">Resource policy overview</span></span>
<span data-ttu-id="084db-105">Las directivas de recursos permiten establecer convenciones para los recursos de una organización.</span><span class="sxs-lookup"><span data-stu-id="084db-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="084db-106">La definición de convenciones permite controlar los costes y administrar los recursos más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="084db-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="084db-107">Por ejemplo, puede especificar que se permitan solo determinados tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="084db-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="084db-108">O puede obligar a que todos los recursos tengan una etiqueta concreta.</span><span class="sxs-lookup"><span data-stu-id="084db-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="084db-109">Todos los recursos secundarios heredan las directivas.</span><span class="sxs-lookup"><span data-stu-id="084db-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="084db-110">De este modo, si una directiva se aplica a un grupo de recursos, será aplicable a todos los recursos de dicho grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="084db-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="084db-111">Hay que comprender dos conceptos acerca de las directivas:</span><span class="sxs-lookup"><span data-stu-id="084db-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="084db-112">definición de la directiva: describe cuándo se aplica la directiva y qué acción realizar</span><span class="sxs-lookup"><span data-stu-id="084db-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="084db-113">asignación de la directiva: la definición de la directiva se aplica a un ámbito (suscripción o grupo de recursos)</span><span class="sxs-lookup"><span data-stu-id="084db-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="084db-114">Este tema se centra en la definición de la directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="084db-115">Para obtener información acerca de la asignación de directivas, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos) o [Assign and manage policies through script](resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="084db-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="084db-116">Las directivas se evalúan al crear y actualizar los recursos (operaciones PUT y PATCH).</span><span class="sxs-lookup"><span data-stu-id="084db-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="084db-117">Actualmente, la directiva no evalúa los tipos de recursos que no se admiten etiquetas, variante y ubicación, como el tipo de recurso Microsoft.Resources/deployments.</span><span class="sxs-lookup"><span data-stu-id="084db-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="084db-118">Esta compatibilidad se agregará en el futuro.</span><span class="sxs-lookup"><span data-stu-id="084db-118">This support will be added at a future time.</span></span> <span data-ttu-id="084db-119">Para evitar problemas de compatibilidad con versiones anteriores, debe especificar explícitamente el tipo al crear directivas.</span><span class="sxs-lookup"><span data-stu-id="084db-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="084db-120">Por ejemplo, una directiva de etiqueta que no especifique tipos se aplicará a todos los tipos.</span><span class="sxs-lookup"><span data-stu-id="084db-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="084db-121">En ese caso, una implementación de plantilla puede dar error si hay un recurso anidado que no admite etiquetas y el tipo de recurso de implementación se ha agregado a la evaluación de directivas.</span><span class="sxs-lookup"><span data-stu-id="084db-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="084db-122">¿En qué se diferencia de RBAC?</span><span class="sxs-lookup"><span data-stu-id="084db-122">How is it different from RBAC?</span></span>
<span data-ttu-id="084db-123">Hay algunas diferencias importantes entre directiva y control de acceso basado en roles (RBAC).</span><span class="sxs-lookup"><span data-stu-id="084db-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="084db-124">RBAC se centra en las acciones del **usuario** en ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="084db-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="084db-125">Por ejemplo, se agrega un usuario al rol de colaborador para un grupo de recursos en el ámbito deseado, para que pueda realizar cambios en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="084db-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="084db-126">La directiva se centra en las propiedades de los **recursos** durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="084db-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="084db-127">Por ejemplo, a través de directivas, puede controlar los tipos de recursos que se pueden aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="084db-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="084db-128">O puede restringir las ubicaciones en las que se pueden aprovisionar los recursos.</span><span class="sxs-lookup"><span data-stu-id="084db-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="084db-129">A diferencia de RBAC, la directiva es un sistema que permite de manera predeterminada y niega explícitamente.</span><span class="sxs-lookup"><span data-stu-id="084db-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="084db-130">Para usar las directivas, debe autenticarse a través de RBAC.</span><span class="sxs-lookup"><span data-stu-id="084db-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="084db-131">En concreto, la cuenta necesita:</span><span class="sxs-lookup"><span data-stu-id="084db-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="084db-132">El permiso `Microsoft.Authorization/policydefinitions/write` para definir una directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="084db-133">El permiso `Microsoft.Authorization/policyassignments/write` para asignar una directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="084db-134">Estos permisos no se incluyen en el rol **Colaborador**.</span><span class="sxs-lookup"><span data-stu-id="084db-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="084db-135">Directivas integradas</span><span class="sxs-lookup"><span data-stu-id="084db-135">Built-in policies</span></span>

<span data-ttu-id="084db-136">Azure proporciona algunas definiciones de directiva predefinidas que pueden reducir el número de directivas que tiene que definir.</span><span class="sxs-lookup"><span data-stu-id="084db-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="084db-137">Para continuar con las definiciones de la directiva, debe tener en cuenta si una directiva integrada ya proporciona la definición que necesita.</span><span class="sxs-lookup"><span data-stu-id="084db-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="084db-138">Las definiciones de directiva integrada son:</span><span class="sxs-lookup"><span data-stu-id="084db-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="084db-139">Ubicaciones permitidas</span><span class="sxs-lookup"><span data-stu-id="084db-139">Allowed locations</span></span>
* <span data-ttu-id="084db-140">Tipos de recursos permitidos</span><span class="sxs-lookup"><span data-stu-id="084db-140">Allowed resource types</span></span>
* <span data-ttu-id="084db-141">SKU de cuenta de almacenamiento permitida</span><span class="sxs-lookup"><span data-stu-id="084db-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="084db-142">SKU de máquina virtual permitida</span><span class="sxs-lookup"><span data-stu-id="084db-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="084db-143">Aplicación de etiqueta y valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="084db-143">Apply tag and default value</span></span>
* <span data-ttu-id="084db-144">Aplicación de etiqueta y valor</span><span class="sxs-lookup"><span data-stu-id="084db-144">Enforce tag and value</span></span>
* <span data-ttu-id="084db-145">Tipos de recursos no permitidos</span><span class="sxs-lookup"><span data-stu-id="084db-145">Not allowed resource types</span></span>
* <span data-ttu-id="084db-146">Requisito de la versión 12.0 de SQL Server</span><span class="sxs-lookup"><span data-stu-id="084db-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="084db-147">Requisito de cifrado de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="084db-147">Require storage account encryption</span></span>

<span data-ttu-id="084db-148">Puede asignar cualquier de estas directivas a través del [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell) o la [CLI de Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="084db-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="084db-149">Estructura de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="084db-149">Policy definition structure</span></span>
<span data-ttu-id="084db-150">Para crear una definición de directiva se utiliza JSON.</span><span class="sxs-lookup"><span data-stu-id="084db-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="084db-151">La definición de directiva contiene elementos para:</span><span class="sxs-lookup"><span data-stu-id="084db-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="084db-152">parameters</span><span class="sxs-lookup"><span data-stu-id="084db-152">parameters</span></span>
* <span data-ttu-id="084db-153">nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="084db-153">display name</span></span>
* <span data-ttu-id="084db-154">description</span><span class="sxs-lookup"><span data-stu-id="084db-154">description</span></span>
* <span data-ttu-id="084db-155">regla de directiva</span><span class="sxs-lookup"><span data-stu-id="084db-155">policy rule</span></span>
  * <span data-ttu-id="084db-156">evaluación lógica</span><span class="sxs-lookup"><span data-stu-id="084db-156">logical evaluation</span></span>
  * <span data-ttu-id="084db-157">efecto</span><span class="sxs-lookup"><span data-stu-id="084db-157">effect</span></span>

<span data-ttu-id="084db-158">En el ejemplo siguiente se muestra una directiva que limita las ubicaciones donde se implementan los recursos:</span><span class="sxs-lookup"><span data-stu-id="084db-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="084db-159">Parámetros</span><span class="sxs-lookup"><span data-stu-id="084db-159">Parameters</span></span>
<span data-ttu-id="084db-160">Al usar parámetros, podrá simplificar la administración de directivas reduciendo el número de definiciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="084db-161">Definimos una directiva para una propiedad de recurso (por ejemplo, para limitar las ubicaciones donde se pueden implementar los recursos) e incluimos parámetros en la definición.</span><span class="sxs-lookup"><span data-stu-id="084db-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="084db-162">A continuación, reutilizamos esa definición de directiva en diferentes escenarios y establecemos valores diferentes (por ejemplo, especificamos un conjunto de ubicaciones para una suscripción) al asignar la directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="084db-163">Declarará parámetros al crear las definiciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="084db-164">El tipo de un parámetro puede ser cadena o matriz.</span><span class="sxs-lookup"><span data-stu-id="084db-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="084db-165">La propiedad de metadatos se utiliza para herramientas como Azure Portal para mostrar información intuitiva.</span><span class="sxs-lookup"><span data-stu-id="084db-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="084db-166">En la regla de directiva, se hace referencia a los parámetros con la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="084db-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="084db-167">Nombre para mostrar y descripción</span><span class="sxs-lookup"><span data-stu-id="084db-167">Display name and description</span></span>

<span data-ttu-id="084db-168">Use los valores de **displayName** y **description** para identificar la definición de directiva y proporcionar el contexto para su uso.</span><span class="sxs-lookup"><span data-stu-id="084db-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="084db-169">Regla de directiva</span><span class="sxs-lookup"><span data-stu-id="084db-169">Policy rule</span></span>

<span data-ttu-id="084db-170">La regla de directiva se compone de los bloques **If** y **Then**.</span><span class="sxs-lookup"><span data-stu-id="084db-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="084db-171">En el bloque **If**, defina una o varias condiciones que especifican cuándo se aplica la directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="084db-172">Puede aplicar operadores lógicos a estas condiciones para definir con precisión el escenario de una directiva.</span><span class="sxs-lookup"><span data-stu-id="084db-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="084db-173">En el bloque **Then**, defina el efecto que se produce cuando se cumplen las condiciones de **If**.</span><span class="sxs-lookup"><span data-stu-id="084db-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="084db-174">Operadores lógicos</span><span class="sxs-lookup"><span data-stu-id="084db-174">Logical operators</span></span>
<span data-ttu-id="084db-175">Los operadores lógicos admitidos son:</span><span class="sxs-lookup"><span data-stu-id="084db-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="084db-176">La sintaxis **not** invierte el resultado de la condición.</span><span class="sxs-lookup"><span data-stu-id="084db-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="084db-177">La sintaxis **allOf** (similar a la operación lógica **And**) requiere que se cumplan todas las condiciones.</span><span class="sxs-lookup"><span data-stu-id="084db-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="084db-178">La sintaxis **anyOf** (similar a la operación lógica **Or**) requiere que se cumplan una o varias condiciones.</span><span class="sxs-lookup"><span data-stu-id="084db-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="084db-179">Puede anidar los operadores lógicos.</span><span class="sxs-lookup"><span data-stu-id="084db-179">You can nest logical operators.</span></span> <span data-ttu-id="084db-180">El ejemplo siguiente muestra una operación **not** que está anidada dentro de una operación **allOf**.</span><span class="sxs-lookup"><span data-stu-id="084db-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a><span data-ttu-id="084db-181">Condiciones</span><span class="sxs-lookup"><span data-stu-id="084db-181">Conditions</span></span>
<span data-ttu-id="084db-182">Una condición evalúa si un **campo** cumple determinados criterios.</span><span class="sxs-lookup"><span data-stu-id="084db-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="084db-183">Estas son las condiciones que se admiten:</span><span class="sxs-lookup"><span data-stu-id="084db-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="084db-184">Cuando se usa la condición **like**, puede incluir un carácter comodín (*) en el valor.</span><span class="sxs-lookup"><span data-stu-id="084db-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="084db-185">Cuando se usa la condición **match**, proporcione `#` para representar un dígito, `?` para una letra y cualquier otro carácter para representar ese carácter en sí.</span><span class="sxs-lookup"><span data-stu-id="084db-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="084db-186">Para obtener ejemplos, vea [Aplicación de directivas de recursos para nombres y texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="084db-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="084db-187">Fields</span><span class="sxs-lookup"><span data-stu-id="084db-187">Fields</span></span>
<span data-ttu-id="084db-188">Para crear condiciones se usan campos.</span><span class="sxs-lookup"><span data-stu-id="084db-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="084db-189">Un campo representa las propiedades de la carga de solicitud de recursos que se usa para describir el estado del recurso.</span><span class="sxs-lookup"><span data-stu-id="084db-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="084db-190">Se admiten los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="084db-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="084db-191">alias de propiedad: para obtener una lista, vea [Alias](#aliases).</span><span class="sxs-lookup"><span data-stu-id="084db-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="084db-192">Efecto</span><span class="sxs-lookup"><span data-stu-id="084db-192">Effect</span></span>
<span data-ttu-id="084db-193">La directiva admite tres tipos de efectos: `deny`, `audit` y `append`.</span><span class="sxs-lookup"><span data-stu-id="084db-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="084db-194">**Deny** genera un evento en el registro de auditoría y se produce un error en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="084db-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="084db-195">**Audit** genera un evento de advertencia en el registro de auditoría pero no producirá un error en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="084db-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="084db-196">**Append** agrega el conjunto de campos definido a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="084db-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="084db-197">En el caso de **append**, debe proporcionar los detalles tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="084db-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="084db-198">El valor puede ser una cadena o un objeto con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="084db-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="084db-199">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-199">Aliases</span></span>

<span data-ttu-id="084db-200">Los alias de propiedad se usan para tener acceso a propiedades específicas de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="084db-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="084db-201">Los alias le permiten restringir los valores o condiciones que se permiten para una propiedad en un recurso.</span><span class="sxs-lookup"><span data-stu-id="084db-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="084db-202">Cada alias se asigna a las rutas de acceso en las diferentes versiones de la API para un tipo de recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="084db-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="084db-203">Durante la evaluación de directivas, el motor de directiva obtiene la ruta de acceso de propiedad para esa versión de la API.</span><span class="sxs-lookup"><span data-stu-id="084db-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="084db-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="084db-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="084db-205">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-205">Alias</span></span> | <span data-ttu-id="084db-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="084db-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="084db-208">Establece si el puerto de servidor Redis que no es SSL (6379) está habilitado.</span><span class="sxs-lookup"><span data-stu-id="084db-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="084db-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="084db-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="084db-210">Establezca el número de particiones que se va a crear en una caché de clúster premium.</span><span class="sxs-lookup"><span data-stu-id="084db-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="084db-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="084db-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="084db-212">Establezca el tamaño de la caché de Redis que implementar.</span><span class="sxs-lookup"><span data-stu-id="084db-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="084db-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="084db-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="084db-214">Establezca la familia de SKU que utilizar.</span><span class="sxs-lookup"><span data-stu-id="084db-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="084db-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="084db-216">Establezca el tipo de Redis Cache que implementar.</span><span class="sxs-lookup"><span data-stu-id="084db-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="084db-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="084db-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="084db-218">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-218">Alias</span></span> | <span data-ttu-id="084db-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="084db-221">Establezca el nombre del plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="084db-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="084db-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="084db-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="084db-223">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-223">Alias</span></span> | <span data-ttu-id="084db-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="084db-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="084db-226">Establezca la oferta de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="084db-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="084db-228">Establezca el publicador de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="084db-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="084db-230">Establezca la SKU de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="084db-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="084db-232">Establezca la versión de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="084db-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="084db-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="084db-234">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-234">Alias</span></span> | <span data-ttu-id="084db-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="084db-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="084db-237">Establezca el identificador de la imagen utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="084db-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="084db-239">Establezca la oferta de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="084db-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="084db-241">Establezca el publicador de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="084db-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="084db-243">Establezca la SKU de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="084db-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="084db-245">Establezca la versión de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="084db-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="084db-247">Establezca que la imagen o el disco cuenten con una licencia local.</span><span class="sxs-lookup"><span data-stu-id="084db-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="084db-248">Este valor solo se usa para imágenes que contienen el sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="084db-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="084db-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="084db-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="084db-250">Establezca la oferta de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="084db-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="084db-252">Establezca el publicador de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="084db-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="084db-254">Establezca la SKU de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="084db-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="084db-256">Establezca la versión de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="084db-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="084db-258">Establezca el URI de VHD.</span><span class="sxs-lookup"><span data-stu-id="084db-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="084db-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="084db-260">Establezca el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="084db-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="084db-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="084db-262">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-262">Alias</span></span> | <span data-ttu-id="084db-263">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="084db-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="084db-265">Establezca el nombre del publicador de la extensión.</span><span class="sxs-lookup"><span data-stu-id="084db-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="084db-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="084db-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="084db-267">Establezca el tipo de extensión.</span><span class="sxs-lookup"><span data-stu-id="084db-267">Set the type of extension.</span></span> |
| <span data-ttu-id="084db-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="084db-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="084db-269">Establezca la versión de la extensión.</span><span class="sxs-lookup"><span data-stu-id="084db-269">Set the version of the extension.</span></span> |

<span data-ttu-id="084db-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="084db-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="084db-271">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-271">Alias</span></span> | <span data-ttu-id="084db-272">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="084db-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="084db-274">Establezca el identificador de la imagen utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="084db-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="084db-276">Establezca la oferta de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="084db-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="084db-278">Establezca el publicador de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="084db-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="084db-280">Establezca la SKU de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="084db-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="084db-282">Establezca la versión de la imagen de plataforma o la imagen de marketplace utilizada para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="084db-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="084db-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="084db-284">Establezca que la imagen o el disco cuenten con una licencia local.</span><span class="sxs-lookup"><span data-stu-id="084db-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="084db-285">Este valor solo se usa para imágenes que contienen el sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="084db-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="084db-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="084db-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="084db-287">Establezca el prefijo del nombre de equipo para todas las máquinas virtuales en el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="084db-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="084db-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="084db-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="084db-289">Establece el URI del blob para la imagen de usuario.</span><span class="sxs-lookup"><span data-stu-id="084db-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="084db-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="084db-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="084db-291">Establezca las direcciones URL de contenedor que se utilizan para almacenar los discos del sistema operativo para el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="084db-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="084db-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="084db-293">Establezca el tamaño de las máquinas virtuales en un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="084db-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="084db-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="084db-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="084db-295">Establezca el nivel las máquinas virtuales en un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="084db-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="084db-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="084db-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="084db-297">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-297">Alias</span></span> | <span data-ttu-id="084db-298">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="084db-300">Establezca el tamaño de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="084db-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="084db-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="084db-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="084db-302">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-302">Alias</span></span> | <span data-ttu-id="084db-303">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="084db-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="084db-305">Establezca el tipo de esta puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="084db-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="084db-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="084db-307">Establezca el nombre de SKU de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="084db-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="084db-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="084db-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="084db-309">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-309">Alias</span></span> | <span data-ttu-id="084db-310">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="084db-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="084db-312">Establezca la versión del servidor.</span><span class="sxs-lookup"><span data-stu-id="084db-312">Set the version of the server.</span></span> |

<span data-ttu-id="084db-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="084db-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="084db-314">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-314">Alias</span></span> | <span data-ttu-id="084db-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="084db-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="084db-317">Establezca la edición de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="084db-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="084db-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="084db-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="084db-319">Establezca el nombre del grupo elástico en el que está la base de datos.</span><span class="sxs-lookup"><span data-stu-id="084db-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="084db-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="084db-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="084db-321">Establezca el Id. de objetivo de nivel de servicio configurado de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="084db-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="084db-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="084db-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="084db-323">Establezca el nombre del objetivo de nivel de servicio configurado de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="084db-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="084db-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="084db-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="084db-325">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-325">Alias</span></span> | <span data-ttu-id="084db-326">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="084db-327">servers/elasticpools</span></span> | <span data-ttu-id="084db-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="084db-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="084db-329">Establezca la DTU compartida total para el grupo elástico de base de datos.</span><span class="sxs-lookup"><span data-stu-id="084db-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="084db-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="084db-330">servers/elasticpools</span></span> | <span data-ttu-id="084db-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="084db-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="084db-332">Establezca la edición del grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="084db-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="084db-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="084db-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="084db-334">Alias</span><span class="sxs-lookup"><span data-stu-id="084db-334">Alias</span></span> | <span data-ttu-id="084db-335">Descripción</span><span class="sxs-lookup"><span data-stu-id="084db-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="084db-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="084db-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="084db-337">Establezca el nivel de acceso usado para la facturación.</span><span class="sxs-lookup"><span data-stu-id="084db-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="084db-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="084db-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="084db-339">Establezca el nombre de SKU.</span><span class="sxs-lookup"><span data-stu-id="084db-339">Set the SKU name.</span></span> |
| <span data-ttu-id="084db-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="084db-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="084db-341">Establezca si el servicio cifra los datos como si estuvieran almacenados en el servicio Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="084db-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="084db-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="084db-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="084db-343">Establezca si el servicio cifra los datos como si estuvieran almacenados en el servicio File Storage.</span><span class="sxs-lookup"><span data-stu-id="084db-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="084db-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="084db-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="084db-345">Establezca el nombre de SKU.</span><span class="sxs-lookup"><span data-stu-id="084db-345">Set the SKU name.</span></span> |
| <span data-ttu-id="084db-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="084db-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="084db-347">Establezca permitir solo el tráfico https en el servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="084db-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="084db-348">Ejemplos de directivas</span><span class="sxs-lookup"><span data-stu-id="084db-348">Policy examples</span></span>

<span data-ttu-id="084db-349">Los siguientes temas contienen ejemplos de directivas:</span><span class="sxs-lookup"><span data-stu-id="084db-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="084db-350">Para ver ejemplos de directivas de etiqueta, consulte [Apply resource policies for tags](resource-manager-policy-tags.md) (Aplicación de directivas de recursos para etiquetas).</span><span class="sxs-lookup"><span data-stu-id="084db-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="084db-351">Para obtener ejemplos de patrones de texto y nomenclatura, vea [Aplicación de directivas de recursos para nombres y texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="084db-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="084db-352">Para ver ejemplos de directivas de almacenamiento, consulte [Aplicación de directivas de recursos a cuentas de almacenamiento](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="084db-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="084db-353">Para ver ejemplos de directivas de máquina virtual, consulte [Aplicación de directivas de recursos a máquinas virtuales Linux](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) y [Aplicación de directivas de recursos a máquinas virtuales Windows](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="084db-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="084db-354">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="084db-354">Next steps</span></span>
* <span data-ttu-id="084db-355">Después de definir una regla de directiva, asígnela a un ámbito.</span><span class="sxs-lookup"><span data-stu-id="084db-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="084db-356">Para asignar directivas a través del portal, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="084db-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="084db-357">Para asignar directivas a través de la API de REST, PowerShell o la CLI de Azure, consulte [Assign and manage policies through script](resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="084db-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="084db-358">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="084db-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="084db-359">El esquema de la directiva está publicado en [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="084db-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

