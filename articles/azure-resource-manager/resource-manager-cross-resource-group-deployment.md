---
title: grupos de recursos de toomultiple aaaDeploy recursos de Azure | Documentos de Microsoft
description: "Muestra cómo agrupar tootarget más de un recurso de Azure durante la implementación."
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
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="784a1-103">Implementar toomore de recursos de Azure a un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="784a1-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="784a1-104">Normalmente, implementar todos los recursos de hello en el plantilla tooa único grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="784a1-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="784a1-105">Sin embargo, hay escenarios donde desea toodeploy un conjunto de recursos entre sí pero colocarlas en distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="784a1-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="784a1-106">Por ejemplo, puede que desee máquina toodeploy Hola de copia de seguridad virtual para la ubicación y el grupo de recursos independiente de Azure Site Recovery tooa.</span><span class="sxs-lookup"><span data-stu-id="784a1-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="784a1-107">El Administrador de recursos permite toouse anidado plantillas tootarget distintos grupos de recursos de grupo de recursos de hello utilizado para la plantilla de elemento primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="784a1-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="784a1-108">grupo de recursos de Hello es el contenedor de ciclo de vida de hello para la aplicación hello y su colección de recursos.</span><span class="sxs-lookup"><span data-stu-id="784a1-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="784a1-109">Crear grupo de recursos de hello fuera de la plantilla de Hola y especificar tootarget de grupo de recursos de Hola durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="784a1-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="784a1-110">Para un grupos de tooresource introducción, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="784a1-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="784a1-111">Plantilla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="784a1-111">Example template</span></span>

<span data-ttu-id="784a1-112">tootarget un recurso diferente, debe usar una plantilla anidada o vinculada durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="784a1-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="784a1-113">Hola `Microsoft.Resources/deployments` tipo de recurso proporciona un `resourceGroup` parámetro que permite toospecify otro grupo de recursos para hello anidados implementación.</span><span class="sxs-lookup"><span data-stu-id="784a1-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="784a1-114">Todos los grupos de recursos de hello deben existir antes de ejecutar la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="784a1-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="784a1-115">Hello en el ejemplo siguiente se implementa dos cuentas de almacenamiento: uno en el grupo de recursos de hello especificado durante la implementación y uno en un grupo de recursos denominado `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="784a1-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="784a1-116">Si establece `resourceGroup` toohello el nombre de un grupo de recursos que no existe, Hola implementación produce un error.</span><span class="sxs-lookup"><span data-stu-id="784a1-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="784a1-117">Si no proporciona un valor para `resourceGroup`, Administrador de recursos usa el grupo de recursos de hello primario.</span><span class="sxs-lookup"><span data-stu-id="784a1-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="784a1-118">Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="784a1-118">Deploy hello template</span></span>

<span data-ttu-id="784a1-119">plantilla de ejemplo de Hola toodeploy, puede usar el portal hello, Azure PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="784a1-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="784a1-120">En el caso de Azure PowerShell o la CLI de Azure, debe usar una versión de mayo de 2017 o posterior.</span><span class="sxs-lookup"><span data-stu-id="784a1-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="784a1-121">Hola ejemplos se supone que ha guardado localmente plantilla Hola como un archivo denominado **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="784a1-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="784a1-122">Para PowerShell:</span><span class="sxs-lookup"><span data-stu-id="784a1-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="784a1-123">Para la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="784a1-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="784a1-124">Una vez finalizada la implementación, verá dos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="784a1-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="784a1-125">Cada uno contiene una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="784a1-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="784a1-126">Usar la función resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="784a1-126">Use resourceGroup() function</span></span>

<span data-ttu-id="784a1-127">De entre las implementaciones del grupo de recursos, hello [resouceGroup() función](resource-group-template-functions-resource.md#resourcegroup) resuelve diferente en función de cómo especificar plantilla anidada Hola.</span><span class="sxs-lookup"><span data-stu-id="784a1-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="784a1-128">Si incrusta una plantilla dentro de otra, resouceGroup() en plantillas anidadas Hola resuelve grupo de recursos de toohello primario.</span><span class="sxs-lookup"><span data-stu-id="784a1-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="784a1-129">Una plantilla de embedded utiliza Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="784a1-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="784a1-130">Si crea un vínculo tooa de plantilla independiente, resouceGroup() en la plantilla vinculada Hola resuelve toohello grupo de recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="784a1-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="784a1-131">Una plantilla vinculada usa Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="784a1-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="784a1-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="784a1-132">Next steps</span></span>

* <span data-ttu-id="784a1-133">toounderstand toodefine parámetros de la plantilla, vea [comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="784a1-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="784a1-134">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="784a1-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="784a1-135">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="784a1-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
