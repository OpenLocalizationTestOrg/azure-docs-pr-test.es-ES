---
title: las directivas de recursos aaaAzure | Documentos de Microsoft
description: "Describe cómo se establecen las propiedades de recurso coherente de toouse Azure Resource Manager directivas tooensure durante la implementación. Se pueden aplicar directivas en grupos de suscripción o el recurso de Hola."
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="6acbc-104">Información general sobre las directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="6acbc-104">Resource policy overview</span></span>
<span data-ttu-id="6acbc-105">Las directivas de recursos permiten tooestablish convenciones para los recursos de su organización.</span><span class="sxs-lookup"><span data-stu-id="6acbc-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="6acbc-106">La definición de convenciones permite controlar los costes y administrar los recursos más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="6acbc-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="6acbc-107">Por ejemplo, puede especificar que se permitan solo determinados tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6acbc-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="6acbc-108">O puede obligar a que todos los recursos tengan una etiqueta concreta.</span><span class="sxs-lookup"><span data-stu-id="6acbc-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="6acbc-109">Todos los recursos secundarios heredan las directivas.</span><span class="sxs-lookup"><span data-stu-id="6acbc-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="6acbc-110">Por lo tanto, si una directiva aplicada tooa grupo de recursos, es aplicable tooall recursos de hello en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6acbc-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="6acbc-111">Hay dos toounderstand conceptos acerca de las directivas:</span><span class="sxs-lookup"><span data-stu-id="6acbc-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="6acbc-112">definición de directiva - describen cuando se aplica la directiva de Hola y qué acción tootake</span><span class="sxs-lookup"><span data-stu-id="6acbc-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="6acbc-113">asignación de directiva, aplica ámbito tooa de la definición de la directiva Hola (suscripción o grupo de recursos)</span><span class="sxs-lookup"><span data-stu-id="6acbc-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="6acbc-114">Este tema se centra en la definición de la directiva.</span><span class="sxs-lookup"><span data-stu-id="6acbc-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="6acbc-115">Para obtener información acerca de la asignación de directiva, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md) o [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="6acbc-116">Las directivas se evalúan al crear y actualizar los recursos (operaciones PUT y PATCH).</span><span class="sxs-lookup"><span data-stu-id="6acbc-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="6acbc-117">Actualmente, directiva no evalúa los tipos de recursos que no son compatibles con etiquetas, tipo y ubicación, como el tipo de recurso de hello Microsoft.Resources/deployments.</span><span class="sxs-lookup"><span data-stu-id="6acbc-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="6acbc-118">Esta compatibilidad se agregará en el futuro.</span><span class="sxs-lookup"><span data-stu-id="6acbc-118">This support will be added at a future time.</span></span> <span data-ttu-id="6acbc-119">tooavoid problemas de compatibilidad con versiones anteriores, se debe especificar explícitamente tipo al crear directivas.</span><span class="sxs-lookup"><span data-stu-id="6acbc-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="6acbc-120">Por ejemplo, una directiva de etiqueta que no especifique tipos se aplicará a todos los tipos.</span><span class="sxs-lookup"><span data-stu-id="6acbc-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="6acbc-121">En ese caso, una implementación de plantilla puede producir un error si hay un recurso anidado que no es compatible con etiquetas y tipo de recurso de implementación de Hola se ha agregado toopolicy evaluación.</span><span class="sxs-lookup"><span data-stu-id="6acbc-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="6acbc-122">¿En qué se diferencia de RBAC?</span><span class="sxs-lookup"><span data-stu-id="6acbc-122">How is it different from RBAC?</span></span>
<span data-ttu-id="6acbc-123">Hay algunas diferencias importantes entre directiva y control de acceso basado en roles (RBAC).</span><span class="sxs-lookup"><span data-stu-id="6acbc-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="6acbc-124">RBAC se centra en las acciones del **usuario** en ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="6acbc-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="6acbc-125">Por ejemplo, se agregan toohello rol de colaborador para un grupo de recursos en el ámbito de hello deseado, por lo que puede hacer el grupo de recursos de toothat de cambios.</span><span class="sxs-lookup"><span data-stu-id="6acbc-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="6acbc-126">La directiva se centra en las propiedades de los **recursos** durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="6acbc-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="6acbc-127">Por ejemplo, a través de directivas, puede controlar tipos de Hola de recursos que se pueden aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="6acbc-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="6acbc-128">O bien, puede restringir las ubicaciones de hello en el que se pueden aprovisionar recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="6acbc-129">A diferencia de RBAC, la directiva es un sistema que permite de manera predeterminada y niega explícitamente.</span><span class="sxs-lookup"><span data-stu-id="6acbc-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="6acbc-130">las directivas de toouse, se debe autenticar a través de RBAC.</span><span class="sxs-lookup"><span data-stu-id="6acbc-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="6acbc-131">En concreto, la cuenta necesita:</span><span class="sxs-lookup"><span data-stu-id="6acbc-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="6acbc-132">`Microsoft.Authorization/policydefinitions/write`toodefine una directiva de permisos</span><span class="sxs-lookup"><span data-stu-id="6acbc-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="6acbc-133">`Microsoft.Authorization/policyassignments/write`tooassign una directiva de permisos</span><span class="sxs-lookup"><span data-stu-id="6acbc-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="6acbc-134">Estos permisos no se incluyen en hello **colaborador** rol.</span><span class="sxs-lookup"><span data-stu-id="6acbc-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="6acbc-135">Directivas integradas</span><span class="sxs-lookup"><span data-stu-id="6acbc-135">Built-in policies</span></span>

<span data-ttu-id="6acbc-136">Azure proporciona algunas definiciones de directivas integradas que pueden reducir el número de Hola de directivas tiene toodefine.</span><span class="sxs-lookup"><span data-stu-id="6acbc-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="6acbc-137">Antes de continuar con las definiciones de directiva, debe considerar si una directiva integrada ya proporciona la definición de hello que necesaria.</span><span class="sxs-lookup"><span data-stu-id="6acbc-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="6acbc-138">Hola definiciones de directivas integradas son:</span><span class="sxs-lookup"><span data-stu-id="6acbc-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="6acbc-139">Ubicaciones permitidas</span><span class="sxs-lookup"><span data-stu-id="6acbc-139">Allowed locations</span></span>
* <span data-ttu-id="6acbc-140">Tipos de recursos permitidos</span><span class="sxs-lookup"><span data-stu-id="6acbc-140">Allowed resource types</span></span>
* <span data-ttu-id="6acbc-141">SKU de cuenta de almacenamiento permitida</span><span class="sxs-lookup"><span data-stu-id="6acbc-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="6acbc-142">SKU de máquina virtual permitida</span><span class="sxs-lookup"><span data-stu-id="6acbc-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="6acbc-143">Aplicación de etiqueta y valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="6acbc-143">Apply tag and default value</span></span>
* <span data-ttu-id="6acbc-144">Aplicación de etiqueta y valor</span><span class="sxs-lookup"><span data-stu-id="6acbc-144">Enforce tag and value</span></span>
* <span data-ttu-id="6acbc-145">Tipos de recursos no permitidos</span><span class="sxs-lookup"><span data-stu-id="6acbc-145">Not allowed resource types</span></span>
* <span data-ttu-id="6acbc-146">Requisito de la versión 12.0 de SQL Server</span><span class="sxs-lookup"><span data-stu-id="6acbc-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="6acbc-147">Requisito de cifrado de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6acbc-147">Require storage account encryption</span></span>

<span data-ttu-id="6acbc-148">Puede asignar cualquiera de estas directivas a través de hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), o [CLI de Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6acbc-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="6acbc-149">Estructura de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="6acbc-149">Policy definition structure</span></span>
<span data-ttu-id="6acbc-150">Usar JSON toocreate una definición de directiva.</span><span class="sxs-lookup"><span data-stu-id="6acbc-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="6acbc-151">definición de la directiva de Hello contiene elementos para:</span><span class="sxs-lookup"><span data-stu-id="6acbc-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="6acbc-152">parameters</span><span class="sxs-lookup"><span data-stu-id="6acbc-152">parameters</span></span>
* <span data-ttu-id="6acbc-153">nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="6acbc-153">display name</span></span>
* <span data-ttu-id="6acbc-154">description</span><span class="sxs-lookup"><span data-stu-id="6acbc-154">description</span></span>
* <span data-ttu-id="6acbc-155">regla de directiva</span><span class="sxs-lookup"><span data-stu-id="6acbc-155">policy rule</span></span>
  * <span data-ttu-id="6acbc-156">evaluación lógica</span><span class="sxs-lookup"><span data-stu-id="6acbc-156">logical evaluation</span></span>
  * <span data-ttu-id="6acbc-157">efecto</span><span class="sxs-lookup"><span data-stu-id="6acbc-157">effect</span></span>

<span data-ttu-id="6acbc-158">Hola de ejemplo siguiente muestra una directiva que limita donde se implementan los recursos:</span><span class="sxs-lookup"><span data-stu-id="6acbc-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="6acbc-159">parameters</span><span class="sxs-lookup"><span data-stu-id="6acbc-159">Parameters</span></span>
<span data-ttu-id="6acbc-160">Usar parámetros ayuda a simplificar la administración de directivas reduciendo el número de Hola de definiciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="6acbc-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="6acbc-161">Definir una directiva para una propiedad de recurso (por ejemplo, para limitar las ubicaciones de Hola donde se pueden implementar los recursos) e incluir parámetros en la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="6acbc-162">A continuación, reutilizar esa definición de directiva para diferentes escenarios pasando valores diferentes (por ejemplo, para especificar un conjunto de ubicaciones para una suscripción) al asignar la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="6acbc-163">Declarará parámetros al crear las definiciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="6acbc-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="6acbc-164">puede ser tipo Hello de un parámetro de cadena o matriz.</span><span class="sxs-lookup"><span data-stu-id="6acbc-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="6acbc-165">propiedad de metadatos de Hola se utiliza para herramientas como toodisplay portal Azure simplifica la información.</span><span class="sxs-lookup"><span data-stu-id="6acbc-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="6acbc-166">En la regla de directiva de hello, hace referencia a parámetros con hello según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="6acbc-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="6acbc-167">Nombre para mostrar y descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-167">Display name and description</span></span>

<span data-ttu-id="6acbc-168">Usar hello **displayName** y **descripción** tooidentify Hola definición de directiva y proporcionar un contexto para cuando se utiliza.</span><span class="sxs-lookup"><span data-stu-id="6acbc-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="6acbc-169">Regla de directiva</span><span class="sxs-lookup"><span data-stu-id="6acbc-169">Policy rule</span></span>

<span data-ttu-id="6acbc-170">regla de directivas de Hello consta de **si** y **, a continuación,** bloques.</span><span class="sxs-lookup"><span data-stu-id="6acbc-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="6acbc-171">Hola **si** bloque, definir una o varias condiciones que especifican cuando se aplica la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="6acbc-172">Puede aplicar las condiciones de operadores lógicos toothese tooprecisely definir escenario de Hola para una directiva.</span><span class="sxs-lookup"><span data-stu-id="6acbc-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="6acbc-173">Hola **, a continuación,** bloque, definir el efecto de Hola que tiene lugar cuando hello **si** se cumplen estas condiciones.</span><span class="sxs-lookup"><span data-stu-id="6acbc-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="6acbc-174">Operadores lógicos</span><span class="sxs-lookup"><span data-stu-id="6acbc-174">Logical operators</span></span>
<span data-ttu-id="6acbc-175">operadores lógicos de Hello admitido son:</span><span class="sxs-lookup"><span data-stu-id="6acbc-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="6acbc-176">Hola **no** sintaxis invierte el resultado de hello de condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="6acbc-177">Hola **todo** sintaxis (toohello similar lógico **y** operación) requiere true de toobe de todas las condiciones.</span><span class="sxs-lookup"><span data-stu-id="6acbc-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="6acbc-178">Hola **anyOf** sintaxis (toohello similar lógico **o** operación) requiere true de toobe uno o más condiciones.</span><span class="sxs-lookup"><span data-stu-id="6acbc-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="6acbc-179">Puede anidar los operadores lógicos.</span><span class="sxs-lookup"><span data-stu-id="6acbc-179">You can nest logical operators.</span></span> <span data-ttu-id="6acbc-180">Hola siguiente ejemplo se muestra un **no** operación que está anidada dentro de un **todo** operación.</span><span class="sxs-lookup"><span data-stu-id="6acbc-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="6acbc-181">Condiciones</span><span class="sxs-lookup"><span data-stu-id="6acbc-181">Conditions</span></span>
<span data-ttu-id="6acbc-182">Hola condición se evalúa como si una **campo** cumple determinados criterios.</span><span class="sxs-lookup"><span data-stu-id="6acbc-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="6acbc-183">las condiciones de Hello admitido son:</span><span class="sxs-lookup"><span data-stu-id="6acbc-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="6acbc-184">Cuando se usa hello **como** condición, puede proporcionar un carácter comodín (*) en el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="6acbc-185">Cuando se usa hello **coincide con** condición, proporcione `#` toorepresent un dígito, `?` por una letra y cualquier otro carácter toorepresent ese carácter real.</span><span class="sxs-lookup"><span data-stu-id="6acbc-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="6acbc-186">Para obtener ejemplos, vea [Aplicación de directivas de recursos para nombres y texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="6acbc-187">Fields</span><span class="sxs-lookup"><span data-stu-id="6acbc-187">Fields</span></span>
<span data-ttu-id="6acbc-188">Para crear condiciones se usan campos.</span><span class="sxs-lookup"><span data-stu-id="6acbc-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="6acbc-189">Un campo representa las propiedades de carga de solicitud de recursos de Hola que es usado toodescribe Hola estado del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="6acbc-190">se admite Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="6acbc-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="6acbc-191">alias de propiedad: para obtener una lista, vea [Alias](#aliases).</span><span class="sxs-lookup"><span data-stu-id="6acbc-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="6acbc-192">Efecto</span><span class="sxs-lookup"><span data-stu-id="6acbc-192">Effect</span></span>
<span data-ttu-id="6acbc-193">La directiva admite tres tipos de efectos: `deny`, `audit` y `append`.</span><span class="sxs-lookup"><span data-stu-id="6acbc-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="6acbc-194">**Denegar** genera un evento en el registro de auditoría de Hola y se produce un error de solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="6acbc-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="6acbc-195">**Auditoría** genera un evento de advertencia en el registro de auditoría, pero no se producen errores solicitud Hola</span><span class="sxs-lookup"><span data-stu-id="6acbc-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="6acbc-196">**Anexar** agrega Hola definido por conjunto de campos toohello solicitud</span><span class="sxs-lookup"><span data-stu-id="6acbc-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="6acbc-197">Para **anexar**, debe proporcionar Hola detalles siguientes:</span><span class="sxs-lookup"><span data-stu-id="6acbc-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="6acbc-198">Hola valor puede ser una cadena o un objeto con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="6acbc-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="6acbc-199">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-199">Aliases</span></span>

<span data-ttu-id="6acbc-200">Use alias tooaccess específico de propiedades para un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="6acbc-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="6acbc-201">Los alias permiten toorestrict qué valores o condiciones que se permiten para una propiedad en un recurso.</span><span class="sxs-lookup"><span data-stu-id="6acbc-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="6acbc-202">Todos los alias asigna toopaths en las diferentes versiones de API para un tipo de recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="6acbc-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="6acbc-203">Durante la evaluación de directivas, motor de directiva de hello Obtiene la ruta de acceso de propiedad de Hola para esa versión de API.</span><span class="sxs-lookup"><span data-stu-id="6acbc-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="6acbc-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="6acbc-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="6acbc-205">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-205">Alias</span></span> | <span data-ttu-id="6acbc-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="6acbc-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="6acbc-208">Establecer si (6379) de puerto del servidor de Redis de hello ssl no está habilitado.</span><span class="sxs-lookup"><span data-stu-id="6acbc-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="6acbc-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="6acbc-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="6acbc-210">Establecer número de Hola de toobe de particiones que se creó en una caché de clúster Premium.</span><span class="sxs-lookup"><span data-stu-id="6acbc-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="6acbc-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="6acbc-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="6acbc-212">Establecer tamaño de Hola de toodeploy de caché de Redis Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="6acbc-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="6acbc-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="6acbc-214">Establecer toouse familia de SKU de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="6acbc-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="6acbc-216">Establecer tipo de Hola de caché en Redis toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6acbc-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="6acbc-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="6acbc-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="6acbc-218">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-218">Alias</span></span> | <span data-ttu-id="6acbc-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="6acbc-221">Nombre del conjunto de hello del programa Hola a nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="6acbc-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="6acbc-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="6acbc-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="6acbc-223">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-223">Alias</span></span> | <span data-ttu-id="6acbc-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6acbc-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="6acbc-226">Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6acbc-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="6acbc-228">Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="6acbc-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="6acbc-230">Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6acbc-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="6acbc-232">Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6acbc-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="6acbc-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="6acbc-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="6acbc-234">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-234">Alias</span></span> | <span data-ttu-id="6acbc-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="6acbc-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="6acbc-237">Identificador de Hola de máquina virtual de hello imagen utilizada toocreate Hola del conjunto.</span><span class="sxs-lookup"><span data-stu-id="6acbc-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6acbc-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="6acbc-239">Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6acbc-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="6acbc-241">Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="6acbc-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="6acbc-243">Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6acbc-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="6acbc-245">Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6acbc-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="6acbc-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="6acbc-247">Establecer esa imagen Hola o disco local con licencia.</span><span class="sxs-lookup"><span data-stu-id="6acbc-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="6acbc-248">Este valor solo se usa para imágenes que contienen el sistema operativo de Windows Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="6acbc-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6acbc-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="6acbc-250">Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6acbc-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="6acbc-252">Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="6acbc-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="6acbc-254">Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6acbc-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="6acbc-256">Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6acbc-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="6acbc-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="6acbc-258">Establecer Hola vhd URI.</span><span class="sxs-lookup"><span data-stu-id="6acbc-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="6acbc-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="6acbc-260">Establecer tamaño de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="6acbc-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="6acbc-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="6acbc-262">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-262">Alias</span></span> | <span data-ttu-id="6acbc-263">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="6acbc-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="6acbc-265">Nombre del conjunto de hello del publicador de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="6acbc-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="6acbc-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="6acbc-267">Establecer tipo de Hola de extensión.</span><span class="sxs-lookup"><span data-stu-id="6acbc-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="6acbc-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="6acbc-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="6acbc-269">Establezca la versión de Hola de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="6acbc-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="6acbc-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="6acbc-271">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-271">Alias</span></span> | <span data-ttu-id="6acbc-272">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="6acbc-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="6acbc-274">Identificador de Hola de máquina virtual de hello imagen utilizada toocreate Hola del conjunto.</span><span class="sxs-lookup"><span data-stu-id="6acbc-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6acbc-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="6acbc-276">Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6acbc-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="6acbc-278">Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="6acbc-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="6acbc-280">Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6acbc-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="6acbc-282">Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6acbc-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="6acbc-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="6acbc-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="6acbc-284">Establecer esa imagen Hola o disco local con licencia.</span><span class="sxs-lookup"><span data-stu-id="6acbc-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="6acbc-285">Este valor solo se usa para imágenes que contienen el sistema operativo de Windows Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="6acbc-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="6acbc-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="6acbc-287">Establezca el prefijo del nombre de equipo de Hola para todas las máquinas virtuales de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="6acbc-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="6acbc-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="6acbc-289">Conjunto Hola URI del blob de imagen de usuario.</span><span class="sxs-lookup"><span data-stu-id="6acbc-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="6acbc-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="6acbc-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="6acbc-291">Conjunto de direcciones URL de contenedor de Hola que son discos del sistema operativo toostore usado para el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="6acbc-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="6acbc-293">Establecer tamaño de Hola de máquinas virtuales en un conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="6acbc-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="6acbc-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="6acbc-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="6acbc-295">Establecer nivel de Hola de máquinas virtuales en un conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="6acbc-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="6acbc-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="6acbc-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="6acbc-297">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-297">Alias</span></span> | <span data-ttu-id="6acbc-298">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="6acbc-300">Establecer tamaño de Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="6acbc-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="6acbc-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="6acbc-302">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-302">Alias</span></span> | <span data-ttu-id="6acbc-303">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="6acbc-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="6acbc-305">Establecer tipo de Hola de esta puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6acbc-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="6acbc-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="6acbc-307">Establecer nombre SKU de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="6acbc-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="6acbc-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="6acbc-309">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-309">Alias</span></span> | <span data-ttu-id="6acbc-310">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="6acbc-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="6acbc-312">Establezca la versión de Hola de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="6acbc-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="6acbc-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="6acbc-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="6acbc-314">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-314">Alias</span></span> | <span data-ttu-id="6acbc-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="6acbc-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="6acbc-317">Establecer la edición de Hola de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="6acbc-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="6acbc-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="6acbc-319">Nombre del conjunto de Hola de base de datos de hello grupo elástico hello es en.</span><span class="sxs-lookup"><span data-stu-id="6acbc-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="6acbc-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="6acbc-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="6acbc-321">Establecer Hola configurado servicio objetivo Id. de nivel de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="6acbc-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="6acbc-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="6acbc-323">Nombre del conjunto de Hola de hello configurado objetivo de nivel de servicio de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="6acbc-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="6acbc-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="6acbc-325">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-325">Alias</span></span> | <span data-ttu-id="6acbc-326">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="6acbc-327">servers/elasticpools</span></span> | <span data-ttu-id="6acbc-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="6acbc-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="6acbc-329">Conjunto Hola total había compartido DTU de grupo elástico de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="6acbc-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="6acbc-330">servers/elasticpools</span></span> | <span data-ttu-id="6acbc-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="6acbc-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="6acbc-332">Establecer la edición de Hola de grupo elástico Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="6acbc-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="6acbc-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="6acbc-334">Alias</span><span class="sxs-lookup"><span data-stu-id="6acbc-334">Alias</span></span> | <span data-ttu-id="6acbc-335">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acbc-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6acbc-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="6acbc-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="6acbc-337">Nivel de acceso de hello del conjunto utilizado para la facturación.</span><span class="sxs-lookup"><span data-stu-id="6acbc-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="6acbc-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="6acbc-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="6acbc-339">Establecer el nombre SKU de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="6acbc-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="6acbc-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="6acbc-341">Establecer si el servicio de hello cifra los datos de hello tal y como se almacena en el servicio de almacenamiento de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="6acbc-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="6acbc-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="6acbc-343">Establecer si el servicio de hello cifra los datos de hello tal y como se almacena en el servicio de almacenamiento de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="6acbc-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="6acbc-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="6acbc-345">Establecer el nombre SKU de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acbc-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="6acbc-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="6acbc-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="6acbc-347">Establecer https solo tooallow servicio toostorage de tráfico.</span><span class="sxs-lookup"><span data-stu-id="6acbc-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="6acbc-348">Ejemplos de directivas</span><span class="sxs-lookup"><span data-stu-id="6acbc-348">Policy examples</span></span>

<span data-ttu-id="6acbc-349">Hola temas siguientes contiene ejemplos de directivas:</span><span class="sxs-lookup"><span data-stu-id="6acbc-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="6acbc-350">Para ver ejemplos de directivas de etiqueta, consulte [Apply resource policies for tags](resource-manager-policy-tags.md) (Aplicación de directivas de recursos para etiquetas).</span><span class="sxs-lookup"><span data-stu-id="6acbc-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="6acbc-351">Para obtener ejemplos de patrones de texto y nomenclatura, vea [Aplicación de directivas de recursos para nombres y texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="6acbc-352">Para obtener ejemplos de las directivas de almacenamiento, consulte [aplicar las cuentas de recursos directivas toostorage](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="6acbc-353">Para obtener ejemplos de directivas de la máquina virtual, consulte [aplicar directivas de recursos tooLinux máquinas virtuales](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) y [aplicar directivas de recursos tooWindows máquinas virtuales](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6acbc-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="6acbc-354">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6acbc-354">Next steps</span></span>
* <span data-ttu-id="6acbc-355">Después de definir una regla de directiva, debe asignarlo tooa ámbito.</span><span class="sxs-lookup"><span data-stu-id="6acbc-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="6acbc-356">directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="6acbc-357">directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="6acbc-358">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6acbc-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="6acbc-359">esquema de la directiva de Hola se publica en [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="6acbc-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

