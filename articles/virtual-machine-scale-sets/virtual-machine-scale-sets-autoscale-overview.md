---
title: "ajuste de escala en aaaAutomatic y máquina virtual según la escala de conjuntos de | Documentos de Microsoft"
description: "Obtenga información acerca del uso de máquinas virtuales de escalado automático recursos tooautomatically escala y diagnóstico en un conjunto de escala."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Cómo toouse el escalado automático y conjuntos de escalas de máquina Virtual
El escalado automático de máquinas virtuales en un conjunto de escala es la creación de Hola o eliminación de máquinas de hello establecer como sea necesario toomatch los requisitos de rendimiento. A medida que aumenta el volumen de Hola de trabajo, una aplicación puede requerir recursos adicionales tooenable tooeffectively realizar tareas.

El escalado automático es un proceso automatizado que ayuda a reducir la sobrecarga de administración. Al reducir la sobrecarga, no necesita toocontinually supervisar el rendimiento del sistema o decidir cómo toomanage recursos. El escalado es un proceso flexible. Como Hola aumenta la carga, se pueden agregar más recursos. Y como disminuye la demanda, los recursos pueden toominimize quitado costos y mantener los niveles de rendimiento.

Configurar el escalado automático en una escala que se establece mediante el uso de una plantilla de administrador de recursos de Azure, Azure PowerShell, CLI de Azure u Hola portal de Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Configuración del escalado mediante plantillas de Resource Manager
En lugar de implementar y administrar cada recurso de la aplicación por separado, utilice una plantilla que implemente todos los recursos en una operación única y coordinada. En la plantilla de hello, recursos de la aplicación se definen y se especifican parámetros de implementación para diferentes entornos. plantilla de Hello consta de JSON y expresiones que puede utilizar valores de tooconstruct para su implementación. toolearn más, mire [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).

En la plantilla de hello, especifique Hola capacidad elemento:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Capacidad identifica número Hola de máquinas virtuales en el conjunto de Hola. Puede cambiar manualmente la capacidad de hello mediante la implementación de una plantilla con un valor diferente. Si va a implementar una capacidad de Hola de cambio de plantilla tooonly, puede incluir únicamente el elemento SKU Hola con capacidad de hello actualizado.

Hello capacidad de su conjunto de escala puede ajustarse automáticamente mediante una combinación de hello **autoscaleSettings** extensión de diagnósticos de hello y recursos.

### <a name="configure-hello-azure-diagnostics-extension"></a>Configurar la extensión de diagnósticos de Azure Hola
El escalado automático solo es posible si la colección de métricas se realiza correctamente en cada máquina virtual en el conjunto de escalas de Hola. Hola extensión de diagnósticos de Azure proporciona capacidades de supervisión y diagnóstico de Hola que satisfaga las necesidades de colección de recursos de escalado automático de Hola Hola métricas. Puede instalar la extensión de hello como parte de la plantilla de administrador de recursos de Hola.

Este ejemplo muestra las variables de Hola que se usan en extensión de diagnósticos de hello plantilla tooconfigure hello:

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Cuando se implementa la plantilla de hello, se proporcionan parámetros. En este ejemplo, nombre de Hola de cuenta de almacenamiento de hello (donde se almacenan los datos) y Hola se proporcionan el nombre del conjunto de escalas de hello (donde se recopilan los datos). En este ejemplo de Windows Server, sólo el contador de rendimiento del número de subprocesos de Hola se recopila. Hola a todos los contadores de rendimiento disponibles en Windows o Linux puede ser información de diagnóstico de toocollect utilizado y puede incluirse en la configuración de la extensión de Hola.

Este ejemplo muestra la definición de Hola de extensión de hello en plantilla hello:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Cuando se ejecuta la extensión de diagnósticos de hello, datos de Hola se almacenan y se recopilan en una tabla, en la cuenta de almacenamiento de Hola que especifique. Hola **WADPerformanceCounters** tabla, puede encontrar los datos recopilado de hello:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Configurar recursos de hello autoScaleSettings
recursos de Hello autoscaleSettings usa información de Hola de toodecide de extensión de diagnósticos de hello si ha establecido tooincrease o disminuir el número de Hola de máquinas virtuales en la escala de Hola.

Este ejemplo muestra la configuración de hello del recurso de hello en plantilla hello:

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

En el ejemplo de Hola anterior, se crean dos reglas para definir las acciones de escalado automático de Hola. primera regla de Hello define la acción de escalado horizontal de Hola y segunda regla de Hola Hola escala en acción. Estos valores se proporcionan en las reglas de hello:

| Regla | Descripción |
| ---- | ----------- |
| metricName        | Este valor es Hola igual que el contador de rendimiento de Hola que definió en la variable de hello wadperfcounter para extensión de diagnósticos de Hola. En el ejemplo de Hola anterior, se usa el contador del número de subprocesos de Hola.    |
| metricResourceUri | Este valor es el identificador de recurso de hello del conjunto de escalas de máquina virtual de Hola. Este identificador contiene nombre Hola Hola del grupo de recursos, el nombre de Hola de proveedor de recursos de Hola y el nombre de Hola de tooscale de conjunto de escala de Hola. |
| timeGrain         | Este valor es la granularidad de Hola de métricas de Hola que se recopilan. En el anterior ejemplo de Hola, los datos se recopilan en un intervalo de un minuto. Este valor se utiliza en combinación con timeWindow. |
| statistic         | Este valor determina la forma métricas Hola Hola combinado tooaccommodate acción de escala automática. Hola los valores posibles son: Average, Min, Max. |
| timeWindow        | Este valor es Hola intervalo de tiempo en el que se recopilan datos de instancia. Debe estar comprendido entre 5 minutos y 12 horas. |
| timeAggregation   | Este valor determina cómo se deben combinar los datos de Hola que se recopilan con el tiempo. valor predeterminado de Hello es Media. Hola los valores posibles son: promedio, mínimo, máximo, último, Total, recuento. |
| operator          | Este valor es el operador de Hola que es usado toocompare Hola hello y datos de umbral de métrica. Hola los valores posibles son: es igual a, valores, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| threshold         | Este valor es el valor de Hola que desencadena la acción de escalado de Hola. Ser seguro tooprovide una diferencia suficiente entre los valores de umbral de Hola para hello **escalada** y **de escala** acciones. Si establece Hola mismos valores para ambas acciones, sistema de hello prevé cambio constante, lo que impide que se implementa una acción de escalado. Por ejemplo, establecer ambos subprocesos too600 en el anterior ejemplo de Hola no funciona. |
| dirección         | Este valor determina la acción de Hola que se realiza cuando se obtiene el valor de umbral de Hola. valores posibles de Hello son aumentan o disminuyen. |
| type              | Este valor es el tipo de Hola de acción que se realizarán y se debe establecer tooChangeCount. |
| value             | Este valor es el número de Hola de máquinas virtuales que se agregan tooor quitado del conjunto de escala de Hola. Este valor debe ser 1 o un valor superior. |
| cooldown          | Este valor es cantidad de Hola de toowait de tiempo desde la última acción de escalado de hello antes de que se produce la acción siguiente Hola. Debe estar comprendido entre un minuto y una semana. |

Función de contador de rendimiento de hello, que está usando, algunos de los elementos de hello en configuración de plantilla de Hola se utilizan de manera diferente. En el anterior ejemplo de Hola, contador de rendimiento de hello es el número de subprocesos, el valor del umbral de hello es 650 para una acción de escalado horizontal y el valor del umbral de hello es 550 para la acción de escala de Hola. Si usa un contador como porcentaje de tiempo de procesador, el valor del umbral de Hola se establece toohello porcentaje de uso de CPU que determina una acción de escalado.

Cuando se desencadena una acción de escalado, por ejemplo, una carga elevada, aumenta en función de valor de hello en plantilla Hola Hola capacidad de hello conjunto. Por ejemplo, en una escala de establece donde capacidad Hola se establece too3 y se establece el valor de acción de escala de Hola too1:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Cuando Hola actual carga causas Hola subproceso promedio recuento toogo por encima del umbral de Hola de 650:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

A **escalada** se desencadena la acción que causas Hola capacidad de hello conjunto toobe aumentado en uno:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

resultado de Hello es que una máquina virtual se agrega el conjunto de escalas de toohello:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Tras un período de enfriamiento de cinco minutos, si promedio de Hola de subprocesos en máquinas de hello permanece en 600, otra máquina se agrega el conjunto toohello. Si el número de subprocesos de promedio de hello permanezca por debajo de 550, capacidad de Hola de conjunto de escalas de Hola se reduce en uno y un equipo se quita del conjunto de Hola.

## <a name="set-up-scaling-using-azure-powershell"></a>Configuración del escalado con Azure PowerShell

Mire toosee ejemplos del uso de PowerShell tooset la escala automática, [Monitor de Azure PowerShell rápido iniciar ejemplos](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Configuración del escalado con la CLI de Azure

Mire toosee ejemplos del uso de CLI de Azure tooset la escala automática, [Monitor Azure multiplataforma CLI rápido iniciar ejemplos](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Configurar el ajuste de escala con hello portal de Azure

Hola toosee muestra un ejemplo del uso de Azure tooset portal la escala automática, busque en [crear un conjunto de escala de máquinas virtuales mediante el portal de Azure de hello](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Más información sobre las acciones de escalado

* **Portal de Azure**  
Actualmente, puede obtener una cantidad limitada de información mediante el portal de Hola.

* **Explorador de recursos de Azure**  
Esta herramienta es hello más adecuado para explorar el estado actual de Hola de su conjunto de escala. Siga esta ruta de acceso y debería ver la vista de instancia de Hola de escala de hello establecido que creó:  
**Subscriptions &gt; {su suscripción} &gt; resourceGroups &gt; {su grupo de recursos} &gt; providers &gt; Microsoft.Compute &gt; virtualMachineScaleSets &gt; {su conjunto de escalado} &gt; virtualMachines**

* **Azure PowerShell**  
Utilice este comando tooget cierta información:

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Conectar máquina virtual de toohello jumpbox tal como lo haría con cualquier otro equipo y, a continuación, se pueden obtener acceso remoto a máquinas virtuales de hello en procesos individuales de hello escala conjunto toomonitor.

## <a name="next-steps"></a>Pasos siguientes
* Mire [ajusta automáticamente las máquinas en un conjunto de escala de máquinas virtuales](virtual-machine-scale-sets-windows-autoscale.md) toosee un ejemplo de cómo toocreate una escala establece con el escalado automático configurado.

* Encuentre ejemplos de características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de PowerShell de Azure Monitor](../monitoring-and-diagnostics/insights-powershell-samples.md).

* Obtenga información sobre las características de notificación de [usar escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Obtenga información acerca de cómo demasiado[toosend webhook y correo electrónico notificaciones de alerta de registros de auditoría de uso en el Monitor de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Más información sobre los [escenarios avanzados de escalado automático](virtual-machine-scale-sets-advanced-autoscale.md).
