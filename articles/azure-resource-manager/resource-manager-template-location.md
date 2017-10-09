---
title: "aaaAzure ubicación del recurso de plantilla | Documentos de Microsoft"
description: "Muestra cómo tooset una ubicación para un recurso en una plantilla de Azure Resource Manager"
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
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="5e717-103">Establecimiento de la ubicación para recursos en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5e717-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="5e717-104">Al implementar una plantilla, debe proporcionar una ubicación para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="5e717-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="5e717-105">Este tema muestra cómo escriban toodetermine Hola ubicaciones de suscripción tooyour disponibles para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="5e717-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="5e717-106">Determinación de las ubicaciones admitidas</span><span class="sxs-lookup"><span data-stu-id="5e717-106">Determine supported locations</span></span>

<span data-ttu-id="5e717-107">Para obtener una lista completa de las ubicaciones admitidas para cada tipo de recurso, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="5e717-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="5e717-108">Sin embargo, la suscripción podría no tener acceso a ubicaciones de hello tooall en esa lista.</span><span class="sxs-lookup"><span data-stu-id="5e717-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="5e717-109">toosee una lista personalizada de ubicaciones de suscripción tooyour disponibles, utilice Azure PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e717-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="5e717-110">Hello en el ejemplo siguiente se utiliza PowerShell tooget Hola ubicaciones para hello `Microsoft.Web\sites` tipo de recurso:</span><span class="sxs-lookup"><span data-stu-id="5e717-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="5e717-111">Hello en el ejemplo siguiente se utiliza Azure CLI 2.0 tooget Hola ubicaciones para hello `Microsoft.Web\sites` tipo de recurso:</span><span class="sxs-lookup"><span data-stu-id="5e717-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="5e717-112">Establecimiento de la ubicación en la plantilla</span><span class="sxs-lookup"><span data-stu-id="5e717-112">Set location in template</span></span>

<span data-ttu-id="5e717-113">Después de determinar las ubicaciones de hello admite para los recursos, debe tooset esa ubicación en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="5e717-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="5e717-114">Hola tooset de manera más fácil este valor es toocreate un recurso de grupo en una ubicación que es compatible con los tipos de recursos de Hola y establece cada ubicación demasiado`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="5e717-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="5e717-115">Puede volver a implementar grupos de tooresource de plantillas de hello en diferentes ubicaciones y no cambie los valores de parámetros o de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e717-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="5e717-116">Hello en el ejemplo siguiente se muestra una cuenta de almacenamiento que está implementado toohello misma ubicación que el grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="5e717-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

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

<span data-ttu-id="5e717-117">Si necesita toohardcode ubicación de hello en la plantilla, proporcione el nombre de Hola de una de las regiones de hello admitida.</span><span class="sxs-lookup"><span data-stu-id="5e717-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="5e717-118">Hola de ejemplo siguiente se muestra una cuenta de almacenamiento que siempre esté implementado tooNorth Central US:</span><span class="sxs-lookup"><span data-stu-id="5e717-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5e717-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e717-119">Next steps</span></span>
* <span data-ttu-id="5e717-120">Para obtener recomendaciones sobre cómo toocreate plantillas, consulte [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="5e717-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

