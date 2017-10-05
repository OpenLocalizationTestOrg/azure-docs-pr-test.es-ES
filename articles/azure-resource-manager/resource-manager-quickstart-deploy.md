---
title: "Implementación de recursos en Azure | Microsoft Docs"
description: Use Azure PowerShell o la CLI de Azure para implementar recursos en Azure. Los recursos se definen en una plantilla de Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 19d5ec337a18b1a159de05ed611b2ccd0c15c592
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-to-azure"></a><span data-ttu-id="f0ee5-104">Implementación de recursos en Azure</span><span class="sxs-lookup"><span data-stu-id="f0ee5-104">Deploy resources to Azure</span></span>

<span data-ttu-id="f0ee5-105">En este tema se muestra cómo implementar recursos en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-105">This topic shows how to deploy resources to your Azure subscription.</span></span> <span data-ttu-id="f0ee5-106">Puede usar Azure PowerShell o la CLI de Azure para implementar una plantilla de Resource Manager que define la infraestructura de la solución.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span></span>

<span data-ttu-id="f0ee5-107">Para ver una introducción de los conceptos de Resource Manager, consulte [Información general sobre Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="f0ee5-108">Pasos para la implementación</span><span class="sxs-lookup"><span data-stu-id="f0ee5-108">Steps for deployment</span></span>

<span data-ttu-id="f0ee5-109">En este tema se da por supuesto que implementa la [plantilla de almacenamiento de ejemplo](#example-storage-template) que aparece aquí.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="f0ee5-110">Puede usar una plantilla distinta, pero los parámetros que escriba serán diferentes a los que se muestran en este tema.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="f0ee5-111">Después de crear una plantilla, los pasos generales para implementar la plantilla son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-111">After creating a template, the general steps for deploying your template are:</span></span>

1. <span data-ttu-id="f0ee5-112">Inicie sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-112">Log in to your account</span></span>
2. <span data-ttu-id="f0ee5-113">Seleccione la suscripción que se va a usar (solo es necesario si tiene varias suscripciones y quiere usar una distinta a la suscripción predeterminada).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span></span>
3. <span data-ttu-id="f0ee5-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f0ee5-114">Create a resource group</span></span>
4. <span data-ttu-id="f0ee5-115">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="f0ee5-115">Deploy the template</span></span>
5. <span data-ttu-id="f0ee5-116">Compruebe el estado de la implementación.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-116">Check your deployment status</span></span>

<span data-ttu-id="f0ee5-117">Las secciones siguientes muestran cómo llevar a cabo esos pasos con [PowerShell](#powershell) o la [CLI de Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="f0ee5-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0ee5-118">PowerShell</span></span>

1. <span data-ttu-id="f0ee5-119">Para instalar Azure PowerShell, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="f0ee5-120">Para empezar rápidamente con la implementación, use los siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-120">To quickly get started with deployment, use the following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="f0ee5-121">El cmdlet `Set-AzureRmContext` solo se necesita si desea usar una suscripción distinta de la suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="f0ee5-122">Para ver todas las suscripciones y sus identificadores, use:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-122">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="f0ee5-123">La implementación puede demorar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-123">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="f0ee5-124">Cuando termine, verá un mensaje similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="f0ee5-125">Para ver el grupo de recursos y la cuenta de almacenamiento que se implementaron en la suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-125">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="f0ee5-126">Puede especificar parámetros de plantilla como parámetros de PowerShell cuando implemente una plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="f0ee5-127">El ejemplo anterior no incluía ningún parámetro de plantilla, por lo que se usaron los valores predeterminados en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-127">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="f0ee5-128">Para implementar otra cuenta de almacenamiento y proporcionar valores de parámetro para el prefijo de nombre del almacenamiento y la SKU de la cuenta de almacenamiento, use:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="f0ee5-129">Ahora tiene dos cuentas de almacenamiento en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="f0ee5-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f0ee5-130">Azure CLI</span></span>

1. <span data-ttu-id="f0ee5-131">Para instalar la CLI de Azure, consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="f0ee5-132">Para empezar a trabajar rápidamente con la implementación, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-132">To quickly get started with deployment, use the following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="f0ee5-133">El comando `az account set` solo se necesita si desea usar una suscripción distinta de la suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="f0ee5-134">Para ver todas las suscripciones y sus identificadores, use:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-134">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="f0ee5-135">La implementación puede demorar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="f0ee5-136">Cuando termine, verá un mensaje similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="f0ee5-137">Para ver el grupo de recursos y la cuenta de almacenamiento que se implementaron en la suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-137">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="f0ee5-138">Puede especificar parámetros de plantilla como parámetros de PowerShell cuando implemente una plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="f0ee5-139">El ejemplo anterior no incluía ningún parámetro de plantilla, por lo que se usaron los valores predeterminados en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-139">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="f0ee5-140">Para implementar otra cuenta de almacenamiento y proporcionar valores de parámetro para el prefijo de nombre del almacenamiento y la SKU de la cuenta de almacenamiento, use:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="f0ee5-141">Ahora tiene dos cuentas de almacenamiento en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f0ee5-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="f0ee5-142">Plantilla de almacenamiento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f0ee5-142">Example storage template</span></span>

<span data-ttu-id="f0ee5-143">Use la plantilla de ejemplo siguiente para implementar una cuenta de almacenamiento en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="f0ee5-143">Use the following example template to deploy a storage account to your subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="f0ee5-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0ee5-144">Next steps</span></span>

* <span data-ttu-id="f0ee5-145">Para información detallada sobre cómo usar PowerShell para implementar plantillas, consulte [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="f0ee5-146">Para información detallada sobre cómo usar la CLI de Azure para implementar plantillas, consulte [Implementación de recursos con plantillas de Resource Manager y la CLI de Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="f0ee5-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



