---
title: grupos de acciones de aaaCreate con plantillas de administrador de recursos | Documentos de Microsoft
description: "Obtenga información acerca de cómo agrupar toocreate una acción mediante una plantilla de Azure Resource Manager."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>Creación de un grupo de acciones con una plantilla de Resource Manager
Este artículo muestra cómo toouse una [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure grupos de acciones. Mediante el uso de plantillas, puede configurar automáticamente grupos de acciones que se pueden reutilizar en determinados tipos de alertas. Estos grupos de acciones de aseguran de que todos los Hola correcto partes reciben notificaciones cuando se desencadene una alerta.

pasos básicos de Hello son:

1. Crear una plantilla como un archivo JSON que describe cómo toocreate Hola grupo de acciones.

2. Implementar la plantilla de hello mediante [cualquier método de implementación](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

En primer lugar, se describe cómo toocreate una plantilla de administrador de recursos para una acción grupo donde las definiciones de acción de hello están codificados en la plantilla de Hola. En segundo lugar, se describe cómo toocreate una plantilla que toma la información de configuración de webhook de hello como parámetros de entrada cuando se implementa Hola plantilla.

## <a name="resource-manager-templates-for-an-action-group"></a>Plantillas de Resource Manager para un grupo de acciones

toocreate un grupo de acciones mediante una plantilla de administrador de recursos, se crea un recurso de tipo hello `Microsoft.Insights/actionGroups`. A continuación, rellene todas las propiedades relacionadas. Aquí hay dos plantillas de ejemplo que crean un grupo de acciones.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a>Pasos siguientes
* Más información sobre los [grupos de acciones](monitoring-action-groups.md).
* Obtenga más información sobre [alertas](monitoring-overview-alerts.md).
* Obtenga información acerca de cómo tooadd [alertas mediante una plantilla de administrador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
