---
title: "Uso del escalado automático de Azure con métricas de invitado en una plantilla de conjunto de escalado de Linux | Microsoft Docs"
description: "Obtenga información acerca de cómo tooautoscale usar las métricas de invitado en una plantilla de conjunto de escala de máquinas virtuales de Linux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Escalado automático con métricas de invitado en una plantilla de conjunto de escalado de Linux

Hay dos tipos de métricas en Azure que se obtienen de las máquinas virtuales y escalar conjuntos: otras proceden de hello hospedar la máquina virtual y otros proceden de la máquina virtual invitada de Hola. Métricas de host no requieren configuración adicional porque se recopilan por host Hola de máquina virtual, mientras que las métricas de invitado requieren nos hello tooinstall [extensión de diagnósticos de Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) o hello [diagnósticos de Azure de Linux extensión](../virtual-machines/linux/diagnostic-extension.md) Hola máquina virtual invitada. Un motivo toouse invitado métricas comunes en lugar de las métricas de host son que las métricas de invitado proporcionan una mayor variedad de métricas de las métricas de host. Un ejemplo es las métricas de consumo de memoria, que solo están disponibles mediante las métricas de invitado. se enumeran las métricas de host de Hello admitida [aquí](../monitoring-and-diagnostics/monitoring-supported-metrics.md), y se enumeran las métricas de uso frecuente invitado [aquí](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Este artículo se muestra cómo hello toomodify [plantilla de conjunto de escala viable mínima](./virtual-machine-scale-sets-mvss-start.md) toouse reglas de escalado automático basan en las métricas de invitado para conjuntos de escalas de Linux.

## <a name="change-hello-template-definition"></a>Cambiar la definición de la plantilla de Hola

Se puede ver la plantilla de conjunto de escala viable mínima [aquí](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), y se puede ver la plantilla para la implementación de escala de Linux Hola establecida con el escalado automático basadas en invitado [aquí](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Examinemos Hola diff utiliza toocreate esta plantilla (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:

Primero, vamos agregar parámetros para `storageAccountName` y `storageAccountSasToken`. agente de diagnóstico de Hello almacenará datos métricos en un [tabla](../cosmos-db/table-storage-how-to-use-dotnet.md) en esta cuenta de almacenamiento. A partir de hello agente de diagnóstico de Linux versión 3.0, ya no se admite con una clave de acceso de almacenamiento. Se debe usar un [token de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

A continuación, se modifique el conjunto de escalas de hello `extensionProfile` extensión de diagnósticos de tooinclude Hola. En esta configuración, se especifican recurso Hola establecido de Id. de escala de hello toocollect métricas de, así como Hola cuenta de almacenamiento y las métricas SAS toouse token toostore Hola. También se especifican con qué frecuencia se agregan métricas de hello (en este caso, cada minuto) y qué tootrack métricas (en este caso memoria usada por ciento). Para más información sobre esta configuración y las métricas, aparte del porcentaje de memoria usado, consulte [esta documentación](../virtual-machines/linux/diagnostic-extension.md).

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

Por último, agregamos una `autoscaleSettings` escalado automático de tooconfigure de recursos en función de estas métricas. Este recurso tiene un `dependsOn` cláusula que hace referencia a escala Hola establece tooensure que el conjunto de escalas de hello existe antes de intentar tooautoscale lo. Si se elige un tooautoscale métrica diferentes en, se utilizaría hello `counterSpecifier` de configuración de extensión de diagnósticos de hello como hello `metricName` en la configuración de escalado automático de Hola. Para obtener más información sobre la configuración de escalado automático, vea hello [prácticas recomendadas de escalado automático](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) hello y [documentación de referencia de API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
