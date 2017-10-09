---
title: plantilla de administrador de recursos de aaaExport con CLI de Azure | Documentos de Microsoft
description: Use el Administrador de recursos de Azure y Azure CLI tooexport una plantilla a partir de un grupo de recursos.
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
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="91f66-103">Exportación de plantillas de Azure Resource Manager con CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="91f66-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="91f66-104">El Administrador de recursos permite tooexport una plantilla de administrador de recursos de los recursos existentes en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="91f66-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="91f66-105">Puede usar ese toolearn plantilla generada sobre Hola plantilla sintaxis o tooautomate Hola volver a implementar la solución según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="91f66-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="91f66-106">Es importante toonote que hay dos tooexport de distintas formas una plantilla:</span><span class="sxs-lookup"><span data-stu-id="91f66-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="91f66-107">Puede exportar Hola real de la plantilla que usa para una implementación.</span><span class="sxs-lookup"><span data-stu-id="91f66-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="91f66-108">plantilla exportada Hola incluye todas las variables y parámetros de hello exactamente tal y como aparecían en la plantilla original Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="91f66-109">Este enfoque es útil cuando es necesario tooretrieve una plantilla.</span><span class="sxs-lookup"><span data-stu-id="91f66-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="91f66-110">Puede exportar una plantilla que representa el estado actual de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="91f66-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="91f66-111">plantilla exportada Hello no se basa en cualquier plantilla que utiliza para la implementación.</span><span class="sxs-lookup"><span data-stu-id="91f66-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="91f66-112">En su lugar, crea una plantilla que es una instantánea Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="91f66-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="91f66-113">plantilla exportada Hello tiene muchos valores codificados de forma rígida y probablemente no tantos parámetros como normalmente tendría que definir.</span><span class="sxs-lookup"><span data-stu-id="91f66-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="91f66-114">Este enfoque es útil cuando se ha modificado el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="91f66-115">Ahora, debe grupo de recursos de hello toocapture como una plantilla.</span><span class="sxs-lookup"><span data-stu-id="91f66-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="91f66-116">En este tema se muestran ambos métodos.</span><span class="sxs-lookup"><span data-stu-id="91f66-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="91f66-117">Implementación de una solución</span><span class="sxs-lookup"><span data-stu-id="91f66-117">Deploy a solution</span></span>

<span data-ttu-id="91f66-118">tooillustrate ambos enfoques para exportar una plantilla, puede empezar mediante la implementación de una suscripción de tooyour de solución.</span><span class="sxs-lookup"><span data-stu-id="91f66-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="91f66-119">Si ya tiene un grupo de recursos en la suscripción que desea tooexport, no es necesario toodeploy esta solución.</span><span class="sxs-lookup"><span data-stu-id="91f66-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="91f66-120">Sin embargo, Hola resto de este artículo se hace referencia toohello plantilla para esta solución.</span><span class="sxs-lookup"><span data-stu-id="91f66-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="91f66-121">script de ejemplo de Hola implementa una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91f66-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="91f66-122">Guardado de una plantilla desde el historial de implementación</span><span class="sxs-lookup"><span data-stu-id="91f66-122">Save template from deployment history</span></span>

<span data-ttu-id="91f66-123">Puede recuperar una plantilla desde el historial de implementación mediante hello [exportación de implementación de grupo az](/cli/azure/group/deployment#export) comando.</span><span class="sxs-lookup"><span data-stu-id="91f66-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="91f66-124">Hola siguiendo el ejemplo de plantilla de hello guarda antes de implementar:</span><span class="sxs-lookup"><span data-stu-id="91f66-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="91f66-125">Devuelve la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-125">It returns hello template.</span></span> <span data-ttu-id="91f66-126">Copie Hola JSON y guárdelo como un archivo.</span><span class="sxs-lookup"><span data-stu-id="91f66-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="91f66-127">Tenga en cuenta que es Hola plantilla exacto utilizado para la implementación.</span><span class="sxs-lookup"><span data-stu-id="91f66-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="91f66-128">variables y parámetros de hello coinciden con plantilla de Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="91f66-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="91f66-129">Puede volver a implementar esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="91f66-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="91f66-130">Exportación de un grupo de recursos como una plantilla</span><span class="sxs-lookup"><span data-stu-id="91f66-130">Export resource group as template</span></span>

<span data-ttu-id="91f66-131">En lugar de recuperar una plantilla de historial de implementación de hello, puede recuperar una plantilla que representa el estado actual de Hola de un grupo de recursos mediante el uso de hello [exportación de grupo az](/cli/azure/group#export) comando.</span><span class="sxs-lookup"><span data-stu-id="91f66-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="91f66-132">Utilice este comando cuando haya realizado muchos cambios tooyour grupo de recursos y ninguna plantilla existente representa todos los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="91f66-133">Devuelve la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-133">It returns hello template.</span></span> <span data-ttu-id="91f66-134">Copie Hola JSON y guárdelo como un archivo.</span><span class="sxs-lookup"><span data-stu-id="91f66-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="91f66-135">Tenga en cuenta que es diferente de la plantilla de hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="91f66-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="91f66-136">Tiene parámetros diferentes y no hay ninguna variable.</span><span class="sxs-lookup"><span data-stu-id="91f66-136">It has different parameters and no variables.</span></span> <span data-ttu-id="91f66-137">almacenamiento de Hello SKU y la ubicación son toovalues codificado de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="91f66-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="91f66-138">Hello en el ejemplo siguiente se muestra plantilla exportada hello, pero la plantilla tiene un nombre de parámetro ligeramente diferente:</span><span class="sxs-lookup"><span data-stu-id="91f66-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="91f66-139">Puede volver a esta plantilla, pero requiere adivinar un nombre único para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="91f66-140">nombre de Hola de su parámetro es ligeramente diferente.</span><span class="sxs-lookup"><span data-stu-id="91f66-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="91f66-141">Personalización de la plantilla exportada</span><span class="sxs-lookup"><span data-stu-id="91f66-141">Customize exported template</span></span>

<span data-ttu-id="91f66-142">Puede modificar esta plantilla toomake se toouse más fácil y más flexibles.</span><span class="sxs-lookup"><span data-stu-id="91f66-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="91f66-143">tooallow para obtener más ubicaciones, toouse de propiedad de ubicación de cambio Hola Hola misma ubicación que el grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="91f66-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="91f66-144">tooavoid tener tooguess un nombre de UNIQUE para la cuenta de almacenamiento, remove Hola parámetro de nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="91f66-145">Agregue un parámetro para un sufijo de nombre de almacenamiento y una SKU de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="91f66-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="91f66-146">Agregue una variable que se construye el nombre de cuenta de almacenamiento de hello con función de hello uniqueString:</span><span class="sxs-lookup"><span data-stu-id="91f66-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="91f66-147">Hola nombre de variable de toohello de cuenta de almacenamiento de hello del conjunto:</span><span class="sxs-lookup"><span data-stu-id="91f66-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="91f66-148">Establecer Hola SKU toohello parámetro:</span><span class="sxs-lookup"><span data-stu-id="91f66-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="91f66-149">La plantilla ahora tiene el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="91f66-149">Your template now looks like:</span></span>

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

<span data-ttu-id="91f66-150">Volver a implementar la plantilla modificada Hola.</span><span class="sxs-lookup"><span data-stu-id="91f66-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91f66-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91f66-151">Next steps</span></span>
* <span data-ttu-id="91f66-152">Para obtener información acerca del uso de hello portal tooexport una plantilla, consulte [exportar una plantilla de Azure Resource Manager de los recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="91f66-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="91f66-153">toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="91f66-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="91f66-154">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="91f66-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>