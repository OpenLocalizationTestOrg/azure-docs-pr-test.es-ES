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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Establecimiento de la ubicación para recursos en plantillas de Azure Resource Manager
Al implementar una plantilla, debe proporcionar una ubicación para cada recurso. Este tema muestra cómo escriban toodetermine Hola ubicaciones de suscripción tooyour disponibles para cada recurso.

## <a name="determine-supported-locations"></a>Determinación de las ubicaciones admitidas

Para obtener una lista completa de las ubicaciones admitidas para cada tipo de recurso, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/). Sin embargo, la suscripción podría no tener acceso a ubicaciones de hello tooall en esa lista. toosee una lista personalizada de ubicaciones de suscripción tooyour disponibles, utilice Azure PowerShell o CLI de Azure. 

Hello en el ejemplo siguiente se utiliza PowerShell tooget Hola ubicaciones para hello `Microsoft.Web\sites` tipo de recurso:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Hello en el ejemplo siguiente se utiliza Azure CLI 2.0 tooget Hola ubicaciones para hello `Microsoft.Web\sites` tipo de recurso:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Establecimiento de la ubicación en la plantilla

Después de determinar las ubicaciones de hello admite para los recursos, debe tooset esa ubicación en la plantilla. Hola tooset de manera más fácil este valor es toocreate un recurso de grupo en una ubicación que es compatible con los tipos de recursos de Hola y establece cada ubicación demasiado`[resourceGroup().location]`. Puede volver a implementar grupos de tooresource de plantillas de hello en diferentes ubicaciones y no cambie los valores de parámetros o de plantilla de Hola. 

Hello en el ejemplo siguiente se muestra una cuenta de almacenamiento que está implementado toohello misma ubicación que el grupo de recursos de hello:

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

Si necesita toohardcode ubicación de hello en la plantilla, proporcione el nombre de Hola de una de las regiones de hello admitida. Hola de ejemplo siguiente se muestra una cuenta de almacenamiento que siempre esté implementado tooNorth Central US:

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

## <a name="next-steps"></a>Pasos siguientes
* Para obtener recomendaciones sobre cómo toocreate plantillas, consulte [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).

