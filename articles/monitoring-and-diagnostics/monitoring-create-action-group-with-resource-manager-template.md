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
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="8df92-103">Creación de un grupo de acciones con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8df92-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="8df92-104">Este artículo muestra cómo toouse una [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure grupos de acciones.</span><span class="sxs-lookup"><span data-stu-id="8df92-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="8df92-105">Mediante el uso de plantillas, puede configurar automáticamente grupos de acciones que se pueden reutilizar en determinados tipos de alertas.</span><span class="sxs-lookup"><span data-stu-id="8df92-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="8df92-106">Estos grupos de acciones de aseguran de que todos los Hola correcto partes reciben notificaciones cuando se desencadene una alerta.</span><span class="sxs-lookup"><span data-stu-id="8df92-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="8df92-107">pasos básicos de Hello son:</span><span class="sxs-lookup"><span data-stu-id="8df92-107">hello basic steps are:</span></span>

1. <span data-ttu-id="8df92-108">Crear una plantilla como un archivo JSON que describe cómo toocreate Hola grupo de acciones.</span><span class="sxs-lookup"><span data-stu-id="8df92-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="8df92-109">Implementar la plantilla de hello mediante [cualquier método de implementación](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="8df92-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="8df92-110">En primer lugar, se describe cómo toocreate una plantilla de administrador de recursos para una acción grupo donde las definiciones de acción de hello están codificados en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df92-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="8df92-111">En segundo lugar, se describe cómo toocreate una plantilla que toma la información de configuración de webhook de hello como parámetros de entrada cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="8df92-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="8df92-112">Plantillas de Resource Manager para un grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="8df92-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="8df92-113">toocreate un grupo de acciones mediante una plantilla de administrador de recursos, se crea un recurso de tipo hello `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="8df92-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="8df92-114">A continuación, rellene todas las propiedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="8df92-114">Then you fill in all related properties.</span></span> <span data-ttu-id="8df92-115">Aquí hay dos plantillas de ejemplo que crean un grupo de acciones.</span><span class="sxs-lookup"><span data-stu-id="8df92-115">Here are two sample templates that create an action group.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="8df92-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8df92-116">Next steps</span></span>
* <span data-ttu-id="8df92-117">Más información sobre los [grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8df92-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="8df92-118">Obtenga más información sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8df92-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="8df92-119">Obtenga información acerca de cómo tooadd [alertas mediante una plantilla de administrador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8df92-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
