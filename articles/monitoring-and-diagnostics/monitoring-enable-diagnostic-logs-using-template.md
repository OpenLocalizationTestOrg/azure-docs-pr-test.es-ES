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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Habilitación automática de Configuración de diagnóstico al crear recursos con una plantilla de Resource Manager
En este artículo se muestra cómo se puede utilizar un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure configuración de diagnóstico en un recurso cuando se crea. Esto le permite iniciar tooautomatically su tooEvent registros de diagnóstico y las métricas de los concentradores, archivarlos en una cuenta de almacenamiento, o bien enviarlas tooLog análisis cuando se crea un recurso de transmisión por secuencias.

método Hello para habilitar registros de diagnóstico mediante una plantilla de administrador de recursos depende del tipo de recurso de Hola.

* **no de proceso** (por ejemplo, Grupos de seguridad de red, Logic Apps, Automatización) usan [Configuración de diagnóstico como se describe en este artículo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Proceso** (WAD/LAD-based) recursos usan hello [archivo de configuración de WAD/LAD descrito en este artículo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

En este artículo se describe cómo diagnósticos de tooconfigure mediante cualquiera de estos métodos.

pasos básicos de Hello son los siguientes:

1. Crear una plantilla como un archivo JSON que describe cómo toocreate Hola recursos y habilitar los diagnósticos.
2. [Implementar la plantilla de hello mediante cualquier método de implementación](../azure-resource-manager/resource-group-template-deploy.md).

A continuación le ofrecemos un ejemplo de Hola plantilla archivo JSON que necesita toogenerate para no son de cálculo y los recursos de proceso.

## <a name="non-compute-resource-template"></a>Plantilla para recursos no de proceso
Para recursos de proceso distinta, deberá toodo dos cosas:

1. Agregue el blob de parámetros de toohello de parámetros para el nombre de cuenta de almacenamiento de hello, Id. de regla de bus de servicio o Id. de área de trabajo de análisis de registros de OMS (habilitar el archivado de registros de diagnóstico en una cuenta de almacenamiento, la transmisión por secuencias de registros tooEvent concentradores, y/o el envío de registros tooLog análisis).
   
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
2. En la matriz de recursos de hello del recurso de hello para el que desea que los registros de diagnóstico de tooenable, agregue un recurso de tipo `[resource namespace]/providers/diagnosticSettings`.
   
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

sigue Hello blob de propiedades de configuración de diagnóstico de hello [formato de hello descrito en este artículo](https://msdn.microsoft.com/library/azure/dn931931.aspx). Agregar hello `metrics` propiedad le permitirá toothese de métricas de recursos tooalso envío mismo genera, siempre que [recursos hello es compatible con métricas de supervisión de Azure](monitoring-supported-metrics.md).

Este es un ejemplo completo que crea una aplicación de la lógica y activa la transmisión por secuencias tooEvent centros y el almacenamiento en una cuenta de almacenamiento.

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

## <a name="compute-resource-template"></a>Plantilla para recursos de proceso
tooenable diagnósticos en un recurso de proceso, por ejemplo, una máquina Virtual o clúster de Service Fabric, debe:

1. Agregar definición de recursos de la extensión toohello Hola diagnósticos de Azure VM.
2. Especifique una cuenta de almacenamiento y/o un centro de eventos como parámetro.
3. Adición de contenido de hello del archivo WADCfg XML en la propiedad XMLCfg de hello, secuencias de escape correctamente todos los caracteres XML.

> [!WARNING]
> Este último paso puede ser difícil tooget derecha. [Consulte este artículo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obtener un ejemplo que divisiones Hola esquema de configuración de diagnóstico en las variables que son caracteres de escape y tiene el formato correcto.
> 
> 

Hello proceso completo, incluidos ejemplos, se describe [en este documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre los registros de Diagnósticos de Azure](monitoring-overview-of-diagnostic-logs.md)
* [Transmitir tooEvent centros de registros de diagnóstico de Azure](monitoring-stream-diagnostic-logs-to-event-hubs.md)

