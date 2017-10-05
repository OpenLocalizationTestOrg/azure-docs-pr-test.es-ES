---
title: "Habilitación automática de Configuración de diagnóstico con una plantilla de Resource Manager | Microsoft Docs"
description: "Aprenda a usar una plantilla de Resource Manager para crear una configuración de diagnóstico que le permitirá transmitir los registros de diagnóstico a centros de eventos o almacenarlos en una cuenta de almacenamiento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="b3eeb-103">Habilitación automática de Configuración de diagnóstico al crear recursos con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3eeb-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="b3eeb-104">En este artículo se muestra cómo usar una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) para establecer Configuración de diagnóstico en un recurso cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="b3eeb-105">Esto permite empezar automáticamente a transmitir las métricas y los registros de diagnóstico a Event Hubs, a archivarlos en una cuenta de almacenamiento o a enviarlos a Log Analytics cuando se crea un recurso.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="b3eeb-106">El método para habilitar registros de diagnóstico mediante una plantilla de Resource Manager depende del tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="b3eeb-107">**no de proceso** (por ejemplo, Grupos de seguridad de red, Logic Apps, Automatización) usan [Configuración de diagnóstico como se describe en este artículo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="b3eeb-108">**de proceso** (basados en WAD/LAD) usan el [archivo de configuración de WAD/LAD descrito en este artículo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="b3eeb-109">En este artículo se describe cómo configurar diagnósticos mediante cualquiera de estos métodos.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="b3eeb-110">Los pasos básicos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b3eeb-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="b3eeb-111">Cree una plantilla como archivo JSON que describa cómo crear el recurso y habilitar los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="b3eeb-112">[Implemente la plantilla mediante cualquier método de implementación](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="b3eeb-113">A continuación, se ofrece un ejemplo del archivo JSON de plantilla que debe generar para los recursos de proceso y los que no lo son.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="b3eeb-114">Plantilla para recursos no de proceso</span><span class="sxs-lookup"><span data-stu-id="b3eeb-114">Non-Compute resource template</span></span>
<span data-ttu-id="b3eeb-115">Para recursos no de proceso, debe hacer dos cosas:</span><span class="sxs-lookup"><span data-stu-id="b3eeb-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="b3eeb-116">Agregue parámetros al blob de parámetros para el nombre de cuenta de almacenamiento, el identificador de regla de Service Bus o el identificador del área de trabajo de Log Analytics de OMS (esto habilita el archivado de registros de diagnóstico en una cuenta de almacenamiento, el streaming de registros a Event Hubs o el envío de registros a Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="b3eeb-117">En la matriz de recursos del recurso para el que desea habilitar los registros de diagnóstico, agregue un recurso de tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="b3eeb-118">El blob de propiedades para la configuración de diagnóstico sigue [el formato descrito en este artículo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="b3eeb-119">Al agregar la propiedad `metrics`, también podrá enviar métricas de recursos para estos mismos resultados, siempre y cuando [los recursos admitan las métricas de Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="b3eeb-120">Este es un ejemplo completo en el que se crea una aplicación lógica y se activa la transmisión a Event Hubs y el almacenamiento en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="b3eeb-121">Plantilla para recursos de proceso</span><span class="sxs-lookup"><span data-stu-id="b3eeb-121">Compute resource template</span></span>
<span data-ttu-id="b3eeb-122">Para habilitar los diagnósticos en un recurso de proceso, por ejemplo, un clúster de Service Fabric o de máquinas virtuales, necesitará hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3eeb-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="b3eeb-123">Agregue la extensión de Diagnósticos de Azure a la definición de recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="b3eeb-124">Especifique una cuenta de almacenamiento y/o un centro de eventos como parámetro.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="b3eeb-125">Agregue el contenido del archivo XML de WADCfg a la propiedad XMLCfg y dé el formato de escape correcto a todos los caracteres XML.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="b3eeb-126">Este último paso puede ser complicado de realizar correctamente.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="b3eeb-127">[Consulte este artículo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para ver un ejemplo que divide el esquema de configuración de diagnóstico en variables con el formato y el escape correctos.</span><span class="sxs-lookup"><span data-stu-id="b3eeb-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="b3eeb-128">Se describe el proceso completo, con ejemplos, [en este documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3eeb-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3eeb-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3eeb-129">Next Steps</span></span>
* [<span data-ttu-id="b3eeb-130">Más información sobre los registros de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="b3eeb-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="b3eeb-131">Transmita registros de diagnóstico de Azure a centros de eventos</span><span class="sxs-lookup"><span data-stu-id="b3eeb-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

