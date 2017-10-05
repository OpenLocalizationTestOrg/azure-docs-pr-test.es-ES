---
title: "Ubicación para recursos en plantillas de Azure | Microsoft Docs"
description: "Muestra cómo establecer una ubicación para un recurso en una plantilla de Azure Resource Manager"
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
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="e2981-103">Establecimiento de la ubicación para recursos en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e2981-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="e2981-104">Al implementar una plantilla, debe proporcionar una ubicación para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="e2981-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="e2981-105">Este tema muestra cómo determinar las ubicaciones que están disponibles con su suscripción para cada tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="e2981-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="e2981-106">Determinación de las ubicaciones admitidas</span><span class="sxs-lookup"><span data-stu-id="e2981-106">Determine supported locations</span></span>

<span data-ttu-id="e2981-107">Para obtener una lista completa de las ubicaciones admitidas para cada tipo de recurso, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="e2981-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="e2981-108">No obstante, es posible que la suscripción no tenga acceso a todas las ubicaciones de esa lista.</span><span class="sxs-lookup"><span data-stu-id="e2981-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="e2981-109">Para ver una lista personalizada de las ubicaciones que están disponibles con su suscripción, utilice Azure PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2981-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="e2981-110">En el ejemplo siguiente se usa PowerShell para obtener las ubicaciones para el tipo de recurso `Microsoft.Web\sites`:</span><span class="sxs-lookup"><span data-stu-id="e2981-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="e2981-111">En el ejemplo siguiente se usa la CLI de Azure 2.0 para obtener las ubicaciones para el tipo de recurso `Microsoft.Web\sites`:</span><span class="sxs-lookup"><span data-stu-id="e2981-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="e2981-112">Establecimiento de la ubicación en la plantilla</span><span class="sxs-lookup"><span data-stu-id="e2981-112">Set location in template</span></span>

<span data-ttu-id="e2981-113">Después de determinar las ubicaciones admitidas para los recursos, debe establecer esa ubicación en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e2981-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="e2981-114">La manera más fácil de establecer este valor consiste en crear un grupo de recursos en una ubicación que admita los tipos de recursos y establecer cada ubicación en `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="e2981-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="e2981-115">Puede volver a implementar la plantilla en grupos de recursos de diferentes ubicaciones y no cambie ningún valor en la plantilla ni en los parámetros.</span><span class="sxs-lookup"><span data-stu-id="e2981-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="e2981-116">En el ejemplo siguiente se muestra una cuenta de almacenamiento que está implementada en la misma ubicación que el grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e2981-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="e2981-117">Si tiene que codificar la ubicación en la plantilla, indique el nombre de una de las regiones admitidas.</span><span class="sxs-lookup"><span data-stu-id="e2981-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="e2981-118">En el ejemplo siguiente se muestra una cuenta de almacenamiento que está siempre implementada en Centro-Norte de EE. UU:</span><span class="sxs-lookup"><span data-stu-id="e2981-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="e2981-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2981-119">Next steps</span></span>
* <span data-ttu-id="e2981-120">Para más recomendaciones sobre la creación de plantillas, consulte [Procedimientos recomendados para crear plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="e2981-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

