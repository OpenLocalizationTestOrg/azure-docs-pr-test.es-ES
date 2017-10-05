---
title: "Definición de recursos secundarios en la plantilla de Azure | Microsoft Docs"
description: "Muestra cómo se establece el tipo y el nombre de un recurso secundario en una plantilla de Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="ab5a7-103">Establecimiento del nombre y el tipo de recurso secundario en la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab5a7-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="ab5a7-104">Al crear una plantilla, con frecuencia es necesario incluir un recurso secundario relacionado con uno primario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="ab5a7-105">Por ejemplo, la plantilla puede incluir un servidor SQL Server y una base de datos.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="ab5a7-106">SQL Server es el recurso primario y la base de datos, el secundario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="ab5a7-107">El formato del tipo de recurso secundario es: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="ab5a7-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="ab5a7-108">El formato del nombre de recurso secundario es: `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="ab5a7-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="ab5a7-109">Sin embargo, el tipo y el nombre se especifican en una plantilla de manera diferente en función de si se anida dentro del recurso primario o por sí misma en el nivel superior.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="ab5a7-110">En este tema se muestra cómo aplicar ambos enfoques.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="ab5a7-111">Al construir una referencia completa a un recurso, el orden para combinar los segmentos a partir del tipo y el nombre no es simplemente una concatenación de los dos.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="ab5a7-112">En su lugar, después del espacio de nombres, use una secuencia de pares *tipo/nombre* de menos a más específico:</span><span class="sxs-lookup"><span data-stu-id="ab5a7-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="ab5a7-113">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab5a7-113">For example:</span></span>

<span data-ttu-id="ab5a7-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` es correcto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` no es correcto</span><span class="sxs-lookup"><span data-stu-id="ab5a7-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="ab5a7-115">Recurso secundario anidado</span><span class="sxs-lookup"><span data-stu-id="ab5a7-115">Nested child resource</span></span>
<span data-ttu-id="ab5a7-116">La manera más fácil de definir un recurso secundario es anidarlo en el primario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="ab5a7-117">En el ejemplo siguiente se muestra una base de datos de SQL anidada en un servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="ab5a7-118">Para el recurso secundario, el tipo se establece en `databases`, pero el tipo de recurso completo es `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="ab5a7-119">No proporciona `Microsoft.Sql/servers/`, porque lo adopta del tipo de recurso primario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="ab5a7-120">El nombre del recurso secundario se establece en `exampledatabase`, pero el nombre completo incluye el primario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="ab5a7-121">No proporciona `exampleserver`, porque lo adopta del recurso primario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="ab5a7-122">Recurso secundario de nivel superior</span><span class="sxs-lookup"><span data-stu-id="ab5a7-122">Top-level child resource</span></span>
<span data-ttu-id="ab5a7-123">Puede definir el recurso secundario en el nivel superior.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="ab5a7-124">Este enfoque puede usarse si el recurso primario no está implementado en la misma plantilla o si desea usar `copy` para crear varios recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="ab5a7-125">En este enfoque, es necesario proporcionar el tipo de recurso completo, así como incluir el nombre del recurso primario en el del secundario.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="ab5a7-126">La base de datos es un recurso secundario del servidor, aunque se definan en el mismo nivel en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ab5a7-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab5a7-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab5a7-127">Next steps</span></span>
* <span data-ttu-id="ab5a7-128">Para más recomendaciones sobre la creación de plantillas, consulte [Procedimientos recomendados para crear plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="ab5a7-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="ab5a7-129">Para obtener un ejemplo de creación de varios recursos secundarios, consulte [Implementación de varias instancias de recursos en plantillas de Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ab5a7-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
