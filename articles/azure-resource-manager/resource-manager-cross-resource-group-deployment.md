---
title: "Implementación de recursos de Azure en varios grupos de recursos | Microsoft Docs"
description: "Muestra cómo tener como destino más de un grupo de recursos de Azure durante la implementación."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="a1270-103">Implementación de recursos de Azure en más de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a1270-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="a1270-104">Por lo general, todos los recursos de la plantilla se implementan en un único grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1270-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="a1270-105">Sin embargo, existen escenarios en los que desea implementar un conjunto de recursos juntos pero colocarlos en distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1270-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="a1270-106">Por ejemplo, puede que desee implementar la máquina virtual de copia de seguridad para Azure Site Recovery en un grupo de recursos y una ubicación independientes.</span><span class="sxs-lookup"><span data-stu-id="a1270-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="a1270-107">Resource Manager permite usar plantillas anidadas para tener como destino grupos de recursos diferentes al usado para la plantilla principal.</span><span class="sxs-lookup"><span data-stu-id="a1270-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="a1270-108">El grupo de recursos es el contenedor de ciclo de vida para la aplicación y su colección de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1270-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="a1270-109">Cree el grupo de recursos fuera de la plantilla y especifique el grupo de recursos de destino durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="a1270-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="a1270-110">Para ver una introducción a los grupos de recursos, consulte [Información general sobre Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1270-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="a1270-111">Plantilla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a1270-111">Example template</span></span>

<span data-ttu-id="a1270-112">Para usar como destino un recurso diferente, debe usar una plantilla anidada o vinculada durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="a1270-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="a1270-113">El tipo de recurso `Microsoft.Resources/deployments` proporciona un parámetro `resourceGroup`, que permite especificar un grupo de recursos distinto para la implementación anidada.</span><span class="sxs-lookup"><span data-stu-id="a1270-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="a1270-114">Todos los grupos de recursos deben existir antes de que se ejecute la implementación.</span><span class="sxs-lookup"><span data-stu-id="a1270-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="a1270-115">En el ejemplo siguiente se implementan dos cuentas de almacenamiento: una en el grupo de recursos especificado durante la implementación y otra en un grupo de recursos llamado `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="a1270-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="a1270-116">Si establece `resourceGroup` en el nombre de un grupo de recursos que no existe, la implementación generará un error.</span><span class="sxs-lookup"><span data-stu-id="a1270-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="a1270-117">Si no proporciona ningún valor para `resourceGroup`, Resource Manager usa el grupo de recursos principal.</span><span class="sxs-lookup"><span data-stu-id="a1270-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="a1270-118">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="a1270-118">Deploy the template</span></span>

<span data-ttu-id="a1270-119">Para implementar la plantilla de ejemplo, puede usar el portal, Azure PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1270-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="a1270-120">En el caso de Azure PowerShell o la CLI de Azure, debe usar una versión de mayo de 2017 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a1270-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="a1270-121">En los ejemplos se supone que ha guardado la plantilla localmente como un archivo denominado **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="a1270-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="a1270-122">Para PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a1270-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="a1270-123">Para la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="a1270-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="a1270-124">Una vez finalizada la implementación, verá dos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1270-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="a1270-125">Cada uno contiene una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a1270-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="a1270-126">Usar la función resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="a1270-126">Use resourceGroup() function</span></span>

<span data-ttu-id="a1270-127">En el caso de las implementaciones de grupos de recursos, la [función resourceGroup()](resource-group-template-functions-resource.md#resourcegroup) se resuelve de manera diferente en función de cómo se especifica la plantilla anidada.</span><span class="sxs-lookup"><span data-stu-id="a1270-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="a1270-128">Si inserta una plantilla dentro de otra, la función resourceGroup() de la plantilla anidada se resuelve en el grupo de recursos principal.</span><span class="sxs-lookup"><span data-stu-id="a1270-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="a1270-129">Una plantilla insertada usa el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="a1270-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="a1270-130">Si vincula a una plantilla independiente, la función resourceGroup() de la plantilla vinculada se resuelve en el grupo de recursos anidado.</span><span class="sxs-lookup"><span data-stu-id="a1270-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="a1270-131">Una plantilla vinculada usa el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="a1270-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a1270-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1270-132">Next steps</span></span>

* <span data-ttu-id="a1270-133">Para entender cómo definir parámetros en la plantilla, consulte [Nociones sobre la estructura y la sintaxis de las plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a1270-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a1270-134">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a1270-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="a1270-135">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a1270-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
