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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="f25f1-103">Creación de una alerta del registro de actividad con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f25f1-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="f25f1-104">Este artículo muestra cómo toouse una [plantilla de Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) alertas de registro de actividad de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f25f1-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="f25f1-105">Mediante el uso de plantillas, puede configurar fácilmente muchas alertas que se activarán según condiciones de eventos del registro de actividad específicas como parte del proceso de implementación automatizada.</span><span class="sxs-lookup"><span data-stu-id="f25f1-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="f25f1-106">pasos básicos de Hello son:</span><span class="sxs-lookup"><span data-stu-id="f25f1-106">hello basic steps are:</span></span>

1. <span data-ttu-id="f25f1-107">Crear una plantilla como un archivo JSON que describe cómo la actividad de hello toocreate registro alerta.</span><span class="sxs-lookup"><span data-stu-id="f25f1-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="f25f1-108">Implementar la plantilla de hello mediante [cualquier método de implementación](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="f25f1-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="f25f1-109">Plantilla de Resource Manager para una alerta del registro de actividad</span><span class="sxs-lookup"><span data-stu-id="f25f1-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="f25f1-110">toocreate una alerta de registro de actividad mediante una plantilla de administrador de recursos, se crea un recurso de tipo hello `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="f25f1-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="f25f1-111">A continuación, rellene todas las propiedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="f25f1-111">Then you fill in all related properties.</span></span> <span data-ttu-id="f25f1-112">A continuación, se muestra una plantilla que crea una alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="f25f1-112">Here's a template that creates an activity log alert.</span></span>

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

<span data-ttu-id="f25f1-113">Visite nuestra [Galería de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para encontrar algunos ejemplos de plantillas de alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="f25f1-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f25f1-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f25f1-114">Next steps</span></span>
- <span data-ttu-id="f25f1-115">Obtenga más información sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f25f1-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="f25f1-116">Obtenga información acerca de cómo tooadd [grupos de acciones mediante una plantilla de administrador de recursos](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="f25f1-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="f25f1-117">Obtenga información acerca de cómo demasiado[crear un toomonitor de alerta de registro de actividad en todas las operaciones de motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="f25f1-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="f25f1-118">Obtenga información acerca de cómo demasiado[crear un toomonitor de alerta de registro de actividad en todas las operaciones de escala-escalabilidad de escalado automático errores en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="f25f1-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
