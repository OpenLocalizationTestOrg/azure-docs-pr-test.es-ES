---
title: "Exportación de plantillas de Resource Manager con CLI de Azure | Microsoft Docs"
description: Use Azure Resource Manager y CLI de Azure para exportar una plantilla desde un grupo de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="fdbc6-103">Exportación de plantillas de Azure Resource Manager con CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fdbc6-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="fdbc6-104">Resource Manager permite exportar una plantilla de Resource Manager a partir de los recursos existentes en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="fdbc6-105">Puede usar esa plantilla generada para aprender sobre la sintaxis de plantillas o para automatizar la nueva implementación de su solución según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="fdbc6-106">Es importante tener en cuenta que hay dos formas diferentes de exportar una plantilla:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="fdbc6-107">Puede exportar la plantilla que utilizó para una implementación.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="fdbc6-108">La plantilla exportada incluye todos los parámetros y variables exactamente como aparecían en la plantilla original.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="fdbc6-109">Este enfoque es útil cuando se necesita recuperar una plantilla.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="fdbc6-110">Puede exportar una plantilla que representa el estado actual del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="fdbc6-111">La plantilla exportada no se basa en ninguna plantilla que usara para la implementación.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="fdbc6-112">Al contrario, crea una plantilla que es una instantánea del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="fdbc6-113">La plantilla exportada tiene muchos valores codificados de forma rígida y es probable que no tenga tantos parámetros como normalmente se definirían.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="fdbc6-114">Este enfoque resulta útil cuando se ha modificado el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="fdbc6-115">Ahora, debe capturar el grupo de recursos como plantilla.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="fdbc6-116">En este tema se muestran ambos métodos.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="fdbc6-117">Implementación de una solución</span><span class="sxs-lookup"><span data-stu-id="fdbc6-117">Deploy a solution</span></span>

<span data-ttu-id="fdbc6-118">Para ilustrar ambos enfoques para exportar una plantilla, empecemos por la implementación de una solución en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="fdbc6-119">Si ya tiene un grupo de recursos en la suscripción que desee exportar, no es necesario implementar esta solución.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="fdbc6-120">Sin embargo, el resto de este artículo hace referencia a la plantilla para esta solución.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="fdbc6-121">El script de ejemplo implementa una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="fdbc6-122">Guardado de una plantilla desde el historial de implementación</span><span class="sxs-lookup"><span data-stu-id="fdbc6-122">Save template from deployment history</span></span>

<span data-ttu-id="fdbc6-123">Puede recuperar una plantilla desde el historial de implementación mediante el comando [z group deployment export](/cli/azure/group/deployment#export).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="fdbc6-124">En el ejemplo siguiente se guarda la plantilla implementada previamente:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="fdbc6-125">Devuelve la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-125">It returns the template.</span></span> <span data-ttu-id="fdbc6-126">Copie el JSON y guárdelo como un archivo.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="fdbc6-127">Tenga en cuenta que es la misma plantilla que usó para la implementación.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="fdbc6-128">Los parámetros y variables coinciden con la plantilla de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="fdbc6-129">Puede volver a implementar esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="fdbc6-130">Exportación de un grupo de recursos como una plantilla</span><span class="sxs-lookup"><span data-stu-id="fdbc6-130">Export resource group as template</span></span>

<span data-ttu-id="fdbc6-131">En lugar de recuperar una plantilla del historial de implementación, puede recuperar una plantilla que represente el estado actual de un grupo de recursos mediante el uso del comando [az group export](/cli/azure/group#export).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="fdbc6-132">Utilice este comando si ha realizado muchos cambios en el grupo de recursos y ninguna plantilla existente representa todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="fdbc6-133">Devuelve la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-133">It returns the template.</span></span> <span data-ttu-id="fdbc6-134">Copie el JSON y guárdelo como un archivo.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="fdbc6-135">Tenga en cuenta que es diferente de la plantilla en GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="fdbc6-136">Tiene parámetros diferentes y no hay ninguna variable.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-136">It has different parameters and no variables.</span></span> <span data-ttu-id="fdbc6-137">La ubicación y las SKU de almacenamiento tienen una codificación de forma rígida en los valores.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="fdbc6-138">En el ejemplo siguiente se muestra la plantilla exportada, pero la plantilla tiene un nombre de parámetro ligeramente diferente:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="fdbc6-139">Puede volver a implementar esta plantilla, pero tendrá que adivinar el nombre único para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="fdbc6-140">El nombre del parámetro es ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="fdbc6-141">Personalización de la plantilla exportada</span><span class="sxs-lookup"><span data-stu-id="fdbc6-141">Customize exported template</span></span>

<span data-ttu-id="fdbc6-142">Puede modificar esta plantilla para que sea más flexible y fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="fdbc6-143">Para permitir más ubicaciones, cambie la propiedad de ubicación para utilizar la misma ubicación que el grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="fdbc6-144">Para evitar tener que adivinar un nombre único para la cuenta de almacenamiento, quite el parámetro para el nombre de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="fdbc6-145">Agregue un parámetro para un sufijo de nombre de almacenamiento y una SKU de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="fdbc6-146">Agregue una variable que construya el nombre de cuenta de almacenamiento con la función uniqueString:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="fdbc6-147">Establezca el nombre de la cuenta de almacenamiento en la variable:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="fdbc6-148">Establezca la SKU en el parámetro:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="fdbc6-149">La plantilla ahora tiene el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-149">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="fdbc6-150">Vuelva a implementar la plantilla modificada.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdbc6-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fdbc6-151">Next steps</span></span>
* <span data-ttu-id="fdbc6-152">Para más información sobre el uso del portal para exportar una plantilla, vea [Exportación de plantillas de Azure Resource Manager desde recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="fdbc6-153">Para definir parámetros de plantilla, consulte [Creación de plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="fdbc6-154">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>