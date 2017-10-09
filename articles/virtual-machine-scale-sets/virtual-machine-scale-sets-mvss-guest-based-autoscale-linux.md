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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="97317-103">Escalado automático con métricas de invitado en una plantilla de conjunto de escalado de Linux</span><span class="sxs-lookup"><span data-stu-id="97317-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="97317-104">Hay dos tipos de métricas en Azure que se obtienen de las máquinas virtuales y escalar conjuntos: otras proceden de hello hospedar la máquina virtual y otros proceden de la máquina virtual invitada de Hola.</span><span class="sxs-lookup"><span data-stu-id="97317-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="97317-105">Métricas de host no requieren configuración adicional porque se recopilan por host Hola de máquina virtual, mientras que las métricas de invitado requieren nos hello tooinstall [extensión de diagnósticos de Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) o hello [diagnósticos de Azure de Linux extensión](../virtual-machines/linux/diagnostic-extension.md) Hola máquina virtual invitada.</span><span class="sxs-lookup"><span data-stu-id="97317-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="97317-106">Un motivo toouse invitado métricas comunes en lugar de las métricas de host son que las métricas de invitado proporcionan una mayor variedad de métricas de las métricas de host.</span><span class="sxs-lookup"><span data-stu-id="97317-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="97317-107">Un ejemplo es las métricas de consumo de memoria, que solo están disponibles mediante las métricas de invitado.</span><span class="sxs-lookup"><span data-stu-id="97317-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="97317-108">se enumeran las métricas de host de Hello admitida [aquí](../monitoring-and-diagnostics/monitoring-supported-metrics.md), y se enumeran las métricas de uso frecuente invitado [aquí](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="97317-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="97317-109">Este artículo se muestra cómo hello toomodify [plantilla de conjunto de escala viable mínima](./virtual-machine-scale-sets-mvss-start.md) toouse reglas de escalado automático basan en las métricas de invitado para conjuntos de escalas de Linux.</span><span class="sxs-lookup"><span data-stu-id="97317-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="97317-110">Cambiar la definición de la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="97317-110">Change hello template definition</span></span>

<span data-ttu-id="97317-111">Se puede ver la plantilla de conjunto de escala viable mínima [aquí](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), y se puede ver la plantilla para la implementación de escala de Linux Hola establecida con el escalado automático basadas en invitado [aquí](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="97317-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="97317-112">Examinemos Hola diff utiliza toocreate esta plantilla (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:</span><span class="sxs-lookup"><span data-stu-id="97317-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="97317-113">Primero, vamos agregar parámetros para `storageAccountName` y `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="97317-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="97317-114">agente de diagnóstico de Hello almacenará datos métricos en un [tabla](../cosmos-db/table-storage-how-to-use-dotnet.md) en esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97317-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="97317-115">A partir de hello agente de diagnóstico de Linux versión 3.0, ya no se admite con una clave de acceso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97317-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="97317-116">Se debe usar un [token de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="97317-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="97317-117">A continuación, se modifique el conjunto de escalas de hello `extensionProfile` extensión de diagnósticos de tooinclude Hola.</span><span class="sxs-lookup"><span data-stu-id="97317-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="97317-118">En esta configuración, se especifican recurso Hola establecido de Id. de escala de hello toocollect métricas de, así como Hola cuenta de almacenamiento y las métricas SAS toouse token toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="97317-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="97317-119">También se especifican con qué frecuencia se agregan métricas de hello (en este caso, cada minuto) y qué tootrack métricas (en este caso memoria usada por ciento).</span><span class="sxs-lookup"><span data-stu-id="97317-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="97317-120">Para más información sobre esta configuración y las métricas, aparte del porcentaje de memoria usado, consulte [esta documentación](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="97317-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="97317-121">Por último, agregamos una `autoscaleSettings` escalado automático de tooconfigure de recursos en función de estas métricas.</span><span class="sxs-lookup"><span data-stu-id="97317-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="97317-122">Este recurso tiene un `dependsOn` cláusula que hace referencia a escala Hola establece tooensure que el conjunto de escalas de hello existe antes de intentar tooautoscale lo.</span><span class="sxs-lookup"><span data-stu-id="97317-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="97317-123">Si se elige un tooautoscale métrica diferentes en, se utilizaría hello `counterSpecifier` de configuración de extensión de diagnósticos de hello como hello `metricName` en la configuración de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="97317-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="97317-124">Para obtener más información sobre la configuración de escalado automático, vea hello [prácticas recomendadas de escalado automático](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) hello y [documentación de referencia de API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="97317-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="97317-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97317-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
