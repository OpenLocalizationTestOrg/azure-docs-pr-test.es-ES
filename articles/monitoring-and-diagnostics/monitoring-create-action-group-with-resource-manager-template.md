---
title: "Creación de grupos de acciones con plantillas de Resource Manager | Microsoft Docs"
description: Aprenda a crear un grupo de acciones mediante una plantilla de Azure Resource Manager.
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
ms.openlocfilehash: 76bf353cac13f1c2169380f8dd3c1e163d4f3f41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="dee40-103">Creación de un grupo de acciones con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dee40-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="dee40-104">En este artículo se muestra cómo utilizar una [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) para configurar grupos de acciones.</span><span class="sxs-lookup"><span data-stu-id="dee40-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="dee40-105">Mediante el uso de plantillas, puede configurar automáticamente grupos de acciones que se pueden reutilizar en determinados tipos de alertas.</span><span class="sxs-lookup"><span data-stu-id="dee40-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="dee40-106">Estos grupos de acciones garantizan que se notifique a todas las entidades correctas cuando se desencadene una alerta.</span><span class="sxs-lookup"><span data-stu-id="dee40-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="dee40-107">Los pasos básicos son:</span><span class="sxs-lookup"><span data-stu-id="dee40-107">The basic steps are:</span></span>

1. <span data-ttu-id="dee40-108">Crear una plantilla en forma de archivo JSON que describa cómo crear la alerta del grupo de acciones.</span><span class="sxs-lookup"><span data-stu-id="dee40-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="dee40-109">Implemente la plantilla mediante [cualquier método de implementación](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="dee40-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="dee40-110">En primer lugar, se describe cómo crear una plantilla de Resource Manager para un grupo de acciones donde las definiciones de acción están codificadas en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="dee40-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="dee40-111">En segundo lugar, se describe cómo crear una plantilla que toma la información de configuración de webhook como parámetros de entrada cuando se implementa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="dee40-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="dee40-112">Plantillas de Resource Manager para un grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="dee40-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="dee40-113">Para crear un grupo de acciones mediante una plantilla de Resource Manager, cree un recurso del tipo `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="dee40-113">To create an action group by using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="dee40-114">A continuación, rellene todas las propiedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="dee40-114">Then you fill in all related properties.</span></span> <span data-ttu-id="dee40-115">Aquí hay dos plantillas de ejemplo que crean un grupo de acciones.</span><span class="sxs-lookup"><span data-stu-id="dee40-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
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
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
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


## <a name="next-steps"></a><span data-ttu-id="dee40-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dee40-116">Next steps</span></span>
* <span data-ttu-id="dee40-117">Más información sobre los [grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="dee40-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="dee40-118">Obtenga más información sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="dee40-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="dee40-119">Aprenda a agregar [alertas mediante una plantilla de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="dee40-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
