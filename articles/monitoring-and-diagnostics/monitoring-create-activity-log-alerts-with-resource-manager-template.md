---
title: una alerta de registro de actividad con una plantilla de administrador de recursos aaaCreate | Documentos de Microsoft
description: Reciba notificaciones cuando se creen recursos de Azure.
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
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Creación de una alerta del registro de actividad con una plantilla de Resource Manager
Este artículo muestra cómo toouse una [plantilla de Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) alertas de registro de actividad de tooconfigure. Mediante el uso de plantillas, puede configurar fácilmente muchas alertas que se activarán según condiciones de eventos del registro de actividad específicas como parte del proceso de implementación automatizada.

pasos básicos de Hello son:

1. Crear una plantilla como un archivo JSON que describe cómo la actividad de hello toocreate registro alerta.

2. Implementar la plantilla de hello mediante [cualquier método de implementación](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Plantilla de Resource Manager para una alerta del registro de actividad
toocreate una alerta de registro de actividad mediante una plantilla de administrador de recursos, se crea un recurso de tipo hello `microsoft.insights/activityLogAlerts`. A continuación, rellene todas las propiedades relacionadas. A continuación, se muestra una plantilla que crea una alerta del registro de actividad.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

Visite nuestra [Galería de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para encontrar algunos ejemplos de plantillas de alertas del registro de actividad.

## <a name="next-steps"></a>Pasos siguientes
- Obtenga más información sobre [alertas](monitoring-overview-alerts.md).
- Obtenga información acerca de cómo tooadd [grupos de acciones mediante una plantilla de administrador de recursos](monitoring-create-action-group-with-resource-manager-template.md).
- Obtenga información acerca de cómo demasiado[crear un toomonitor de alerta de registro de actividad en todas las operaciones de motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Obtenga información acerca de cómo demasiado[crear un toomonitor de alerta de registro de actividad en todas las operaciones de escala-escalabilidad de escalado automático errores en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
