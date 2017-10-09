---
title: recurso de aaaDefine secundario en la plantilla de Azure | Documentos de Microsoft
description: "Muestra cómo tooset Hola tipo de recurso y el nombre de recurso secundario en una plantilla de Azure Resource Manager"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="9123c-103">Establecimiento del nombre y el tipo de recurso secundario en la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9123c-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="9123c-104">Al crear una plantilla, con frecuencia necesitan tooinclude un recurso secundario que es el recurso primario de tooa relacionados.</span><span class="sxs-lookup"><span data-stu-id="9123c-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="9123c-105">Por ejemplo, la plantilla puede incluir un servidor SQL Server y una base de datos.</span><span class="sxs-lookup"><span data-stu-id="9123c-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="9123c-106">Hola SQL server es el recurso primario de Hola, y base de datos de Hola Hola secundarios recursos.</span><span class="sxs-lookup"><span data-stu-id="9123c-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="9123c-107">formato de Hola Hola secundarios del tipo de recurso es:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="9123c-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="9123c-108">Hola formato del nombre de recurso de hello secundarios es:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="9123c-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="9123c-109">Sin embargo, especificar tipo de Hola y el nombre de una plantilla diferente en función de si está anidada dentro de recurso primario de hello, o en su propio en nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9123c-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="9123c-110">Este tema muestra cómo toohandle ambos enfoques.</span><span class="sxs-lookup"><span data-stu-id="9123c-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="9123c-111">Al construir un recurso de tooa de referencia completa, Hola orden toocombine segmentos de tipo hello y nombre no es simplemente una concatenación de hello dos.</span><span class="sxs-lookup"><span data-stu-id="9123c-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="9123c-112">En su lugar, después de espacio de nombres de hello, utilice una secuencia de */nombre de tipo* pares de toomost menos específica específico:</span><span class="sxs-lookup"><span data-stu-id="9123c-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="9123c-113">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9123c-113">For example:</span></span>

<span data-ttu-id="9123c-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` es correcto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` no es correcto</span><span class="sxs-lookup"><span data-stu-id="9123c-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="9123c-115">Recurso secundario anidado</span><span class="sxs-lookup"><span data-stu-id="9123c-115">Nested child resource</span></span>
<span data-ttu-id="9123c-116">toodefine de manera más fácil de Hello un recurso secundario es toonest dentro de recurso primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9123c-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="9123c-117">Hello en el ejemplo siguiente se muestra una base de datos SQL anidado dentro de un servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9123c-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="9123c-118">Para recursos secundarios de hello, tipo de Hola se establece demasiado`databases` , pero su tipo de recurso completo es `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="9123c-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="9123c-119">No proporciona `Microsoft.Sql/servers/` porque se da por supuesto Hola primario tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="9123c-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="9123c-120">nombre de recurso de Hello secundario está establecido demasiado`exampledatabase` pero el nombre completo de hello incluye el nombre de elemento primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9123c-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="9123c-121">No proporciona `exampleserver` porque se da por supuesto de recurso primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9123c-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="9123c-122">Recurso secundario de nivel superior</span><span class="sxs-lookup"><span data-stu-id="9123c-122">Top-level child resource</span></span>
<span data-ttu-id="9123c-123">Puede definir recursos secundarios de hello en el nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9123c-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="9123c-124">Puede usar este enfoque si no se ha implementado el recurso primario de Hola Hola misma plantilla, o si desea toouse `copy` toocreate varios recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="9123c-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="9123c-125">Con este enfoque, debe proporcionar el tipo de recurso completo de Hola e incluir nombre de recurso primario de hello en nombre de recurso de hello secundarios.</span><span class="sxs-lookup"><span data-stu-id="9123c-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="9123c-126">base de datos de Hello es un servidor de toohello de recursos secundarios aunque se definen en hello al mismo nivel en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9123c-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9123c-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9123c-127">Next steps</span></span>
* <span data-ttu-id="9123c-128">Para obtener recomendaciones sobre cómo toocreate plantillas, consulte [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="9123c-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="9123c-129">Para obtener un ejemplo de creación de varios recursos secundarios, consulte [Implementación de varias instancias de recursos en plantillas de Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="9123c-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
