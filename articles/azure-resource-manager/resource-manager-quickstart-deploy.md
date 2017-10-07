---
title: aaaDeploy recursos tooAzure | Documentos de Microsoft
description: Utilice tooAzure de recursos toodeploy de Azure PowerShell o CLI de Azure. recursos de Hola se definen en una plantilla de administrador de recursos.
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
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>Implementar tooAzure de recursos

Este tema se muestra cómo toodeploy recursos tooyour suscripción de Azure. Puede usar Azure PowerShell o CLI de Azure toodeploy una plantilla de administrador de recursos que define la infraestructura de Hola para su solución.

Para una tooconcepts de introducción del Administrador de recursos, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Pasos para la implementación

En este tema se da por supuesto que se va a implementar hello [plantilla de almacenamiento de ejemplo](#example-storage-template) en este tema. Puede usar una plantilla diferente, pero los parámetros de Hola que se pasan son diferentes que se muestra en este tema.

Después de crear una plantilla, los pasos generales para implementar la plantilla de hello son:

1. Inicie sesión en la cuenta de tooyour
2. Seleccione Hola suscripción toouse (sólo es necesario si tiene varias suscripciones, y desea toouse uno que no sea suscripción predeterminada de hello)
3. Crear un grupo de recursos
4. Implementar la plantilla de Hola
5. Compruebe el estado de la implementación.

Hello secciones siguientes muestran cómo tooperform los pasos con [PowerShell](#powershell) o [CLI de Azure](#azure-cli).

## <a name="powershell"></a>PowerShell

1. tooinstall PowerShell de Azure, consulte [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/overview).

2. tooquickly Introducción a la implementación, use Hola siguientes cmdlets:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Hola `Set-AzureRmContext` cmdlet solo es necesario si desea toouse una suscripción que no sea de su suscripción de manera predeterminada. toosee todas sus suscripciones y sus identificadores, use:

  ```powershell
  Get-AzureRmSubscription
  ```

3. implementación de Hello puede tardar unos toocomplete minutos. Cuando termine, verá un mensaje similar al siguiente:

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee creados por su cuenta de almacenamiento y el grupo de recursos implementa tooyour suscripción, utilice lo siguiente:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Puede especificar parámetros de plantilla como parámetros de PowerShell cuando implemente una plantilla. Hello ejemplo anterior no incluía los parámetros de plantilla, por lo que se usaron los valores predeterminados de hello en plantilla Hola. toodeploy otro almacenamiento de la cuenta y proporcionar los valores de parámetro de prefijo de nombre de almacenamiento de Hola y cuenta de almacenamiento de hello SKU, utilice:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Ahora tiene dos cuentas de almacenamiento en el grupo de recursos. 

## <a name="azure-cli"></a>CLI de Azure

1. tooinstall CLI de Azure, consulte [instalar Azure CLI 2.0](/cli/azure/install-az-cli2).

2. tooquickly Introducción a la implementación, usar hello siguientes comandos:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Hola `az account set` comando sólo es necesario si desea toouse una suscripción que no sea de su suscripción de manera predeterminada. toosee todas sus suscripciones y sus identificadores, use:

  ```azurecli
  az account list
  ```

3. implementación de Hello puede tardar unos toocomplete minutos. Cuando termine, verá un mensaje similar al siguiente:

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee creados por su cuenta de almacenamiento y el grupo de recursos implementa tooyour suscripción, utilice lo siguiente:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Puede especificar parámetros de plantilla como parámetros de PowerShell cuando implemente una plantilla. Hello ejemplo anterior no incluía los parámetros de plantilla, por lo que se usaron los valores predeterminados de hello en plantilla Hola. toodeploy otro almacenamiento de la cuenta y proporcionar los valores de parámetro de prefijo de nombre de almacenamiento de Hola y cuenta de almacenamiento de hello SKU, utilice:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Ahora tiene dos cuentas de almacenamiento en el grupo de recursos. 

## <a name="example-storage-template"></a>Plantilla de almacenamiento de ejemplo

Usar hello después toodeploy de plantilla de ejemplo tooyour suscripción a una cuenta de almacenamiento:

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
        "description": "hello value toouse for starting hello storage account name."
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
        "description": "hello type of replication toouse for hello storage account."
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

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información detallada sobre el uso de plantillas de toodeploy de PowerShell, consulte [implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Para obtener información detallada sobre el uso de plantillas de toodeploy de CLI de Azure, consulte [implementar los recursos con plantillas de administrador de recursos y la CLI de Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).



