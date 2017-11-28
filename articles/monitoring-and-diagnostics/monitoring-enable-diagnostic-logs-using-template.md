---
title: "aaaAutomatically habilitar la configuración de diagnóstico mediante una plantilla de administrador de recursos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse un administrador de recursos plantilla toocreate configuración de diagnóstico que le permitirá toostream su diagnóstico registra tooEvent concentradores o almacenarlas en una cuenta de almacenamiento."
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
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="7b21c-103">Habilitación automática de Configuración de diagnóstico al crear recursos con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b21c-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="7b21c-104">En este artículo se muestra cómo se puede utilizar un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure configuración de diagnóstico en un recurso cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="7b21c-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="7b21c-105">Esto le permite iniciar tooautomatically su tooEvent registros de diagnóstico y las métricas de los concentradores, archivarlos en una cuenta de almacenamiento, o bien enviarlas tooLog análisis cuando se crea un recurso de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="7b21c-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="7b21c-106">método Hello para habilitar registros de diagnóstico mediante una plantilla de administrador de recursos depende del tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b21c-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="7b21c-107">**no de proceso** (por ejemplo, Grupos de seguridad de red, Logic Apps, Automatización) usan [Configuración de diagnóstico como se describe en este artículo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="7b21c-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="7b21c-108">**Proceso** (WAD/LAD-based) recursos usan hello [archivo de configuración de WAD/LAD descrito en este artículo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="7b21c-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="7b21c-109">En este artículo se describe cómo diagnósticos de tooconfigure mediante cualquiera de estos métodos.</span><span class="sxs-lookup"><span data-stu-id="7b21c-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="7b21c-110">pasos básicos de Hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="7b21c-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="7b21c-111">Crear una plantilla como un archivo JSON que describe cómo toocreate Hola recursos y habilitar los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="7b21c-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="7b21c-112">[Implementar la plantilla de hello mediante cualquier método de implementación](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7b21c-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="7b21c-113">A continuación le ofrecemos un ejemplo de Hola plantilla archivo JSON que necesita toogenerate para no son de cálculo y los recursos de proceso.</span><span class="sxs-lookup"><span data-stu-id="7b21c-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="7b21c-114">Plantilla para recursos no de proceso</span><span class="sxs-lookup"><span data-stu-id="7b21c-114">Non-Compute resource template</span></span>
<span data-ttu-id="7b21c-115">Para recursos de proceso distinta, deberá toodo dos cosas:</span><span class="sxs-lookup"><span data-stu-id="7b21c-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="7b21c-116">Agregue el blob de parámetros de toohello de parámetros para el nombre de cuenta de almacenamiento de hello, Id. de regla de bus de servicio o Id. de área de trabajo de análisis de registros de OMS (habilitar el archivado de registros de diagnóstico en una cuenta de almacenamiento, la transmisión por secuencias de registros tooEvent concentradores, y/o el envío de registros tooLog análisis).</span><span class="sxs-lookup"><span data-stu-id="7b21c-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="7b21c-117">En la matriz de recursos de hello del recurso de hello para el que desea que los registros de diagnóstico de tooenable, agregue un recurso de tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="7b21c-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="7b21c-118">sigue Hello blob de propiedades de configuración de diagnóstico de hello [formato de hello descrito en este artículo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b21c-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="7b21c-119">Agregar hello `metrics` propiedad le permitirá toothese de métricas de recursos tooalso envío mismo genera, siempre que [recursos hello es compatible con métricas de supervisión de Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="7b21c-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="7b21c-120">Este es un ejemplo completo que crea una aplicación de la lógica y activa la transmisión por secuencias tooEvent centros y el almacenamiento en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b21c-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="7b21c-121">Plantilla para recursos de proceso</span><span class="sxs-lookup"><span data-stu-id="7b21c-121">Compute resource template</span></span>
<span data-ttu-id="7b21c-122">tooenable diagnósticos en un recurso de proceso, por ejemplo, una máquina Virtual o clúster de Service Fabric, debe:</span><span class="sxs-lookup"><span data-stu-id="7b21c-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="7b21c-123">Agregar definición de recursos de la extensión toohello Hola diagnósticos de Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7b21c-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="7b21c-124">Especifique una cuenta de almacenamiento y/o un centro de eventos como parámetro.</span><span class="sxs-lookup"><span data-stu-id="7b21c-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="7b21c-125">Adición de contenido de hello del archivo WADCfg XML en la propiedad XMLCfg de hello, secuencias de escape correctamente todos los caracteres XML.</span><span class="sxs-lookup"><span data-stu-id="7b21c-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="7b21c-126">Este último paso puede ser difícil tooget derecha.</span><span class="sxs-lookup"><span data-stu-id="7b21c-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="7b21c-127">[Consulte este artículo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obtener un ejemplo que divisiones Hola esquema de configuración de diagnóstico en las variables que son caracteres de escape y tiene el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="7b21c-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="7b21c-128">Hello proceso completo, incluidos ejemplos, se describe [en este documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b21c-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b21c-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b21c-129">Next Steps</span></span>
* [<span data-ttu-id="7b21c-130">Más información sobre los registros de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="7b21c-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="7b21c-131">Transmitir tooEvent centros de registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="7b21c-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

