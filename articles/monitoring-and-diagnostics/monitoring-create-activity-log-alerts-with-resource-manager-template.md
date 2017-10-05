---
title: "Creación de una alerta del registro de actividad con una plantilla de Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: 92076c7fe1f867919b7e02abf79cf0fb74fb7eb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="b1a8a-103">Creación de una alerta del registro de actividad con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1a8a-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="b1a8a-104">En este artículo se muestra cómo utilizar una [plantilla de Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) para configurar alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="b1a8a-105">Mediante el uso de plantillas, puede configurar fácilmente muchas alertas que se activarán según condiciones de eventos del registro de actividad específicas como parte del proceso de implementación automatizada.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="b1a8a-106">Los pasos básicos son:</span><span class="sxs-lookup"><span data-stu-id="b1a8a-106">The basic steps are:</span></span>

1. <span data-ttu-id="b1a8a-107">Crear una plantilla en forma de archivo JSON que describa cómo crear la alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="b1a8a-108">Implemente la plantilla mediante [cualquier método de implementación](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="b1a8a-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="b1a8a-109">Plantilla de Resource Manager para una alerta del registro de actividad</span><span class="sxs-lookup"><span data-stu-id="b1a8a-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="b1a8a-110">Para crear una alerta del registro de actividad mediante una plantilla de Resource Manager, cree un recurso del tipo `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="b1a8a-111">A continuación, rellene todas las propiedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-111">Then you fill in all related properties.</span></span> <span data-ttu-id="b1a8a-112">A continuación, se muestra una plantilla que crea una alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
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

<span data-ttu-id="b1a8a-113">Visite nuestra [Galería de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para encontrar algunos ejemplos de plantillas de alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b1a8a-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1a8a-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1a8a-114">Next steps</span></span>
- <span data-ttu-id="b1a8a-115">Obtenga más información sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b1a8a-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="b1a8a-116">Aprenda a agregar [grupos de acciones mediante una plantilla de Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="b1a8a-116">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="b1a8a-117">Aprenda a [crear una alerta del registro de actividad para supervisar todas las operaciones del motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="b1a8a-117">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="b1a8a-118">Aprenda a [crear una alerta del registro de actividad para supervisar todas las operaciones con errores de escalado automático y reducción horizontal en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="b1a8a-118">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
