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
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="5c346-103">Cómo toouse el escalado automático y conjuntos de escalas de máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="5c346-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5c346-104">El escalado automático de máquinas virtuales en un conjunto de escala es la creación de Hola o eliminación de máquinas de hello establecer como sea necesario toomatch los requisitos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="5c346-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="5c346-105">A medida que aumenta el volumen de Hola de trabajo, una aplicación puede requerir recursos adicionales tooenable tooeffectively realizar tareas.</span><span class="sxs-lookup"><span data-stu-id="5c346-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="5c346-106">El escalado automático es un proceso automatizado que ayuda a reducir la sobrecarga de administración.</span><span class="sxs-lookup"><span data-stu-id="5c346-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="5c346-107">Al reducir la sobrecarga, no necesita toocontinually supervisar el rendimiento del sistema o decidir cómo toomanage recursos.</span><span class="sxs-lookup"><span data-stu-id="5c346-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="5c346-108">El escalado es un proceso flexible.</span><span class="sxs-lookup"><span data-stu-id="5c346-108">Scaling is an elastic process.</span></span> <span data-ttu-id="5c346-109">Como Hola aumenta la carga, se pueden agregar más recursos.</span><span class="sxs-lookup"><span data-stu-id="5c346-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="5c346-110">Y como disminuye la demanda, los recursos pueden toominimize quitado costos y mantener los niveles de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="5c346-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="5c346-111">Configurar el escalado automático en una escala que se establece mediante el uso de una plantilla de administrador de recursos de Azure, Azure PowerShell, CLI de Azure u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c346-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="5c346-112">Configuración del escalado mediante plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5c346-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="5c346-113">En lugar de implementar y administrar cada recurso de la aplicación por separado, utilice una plantilla que implemente todos los recursos en una operación única y coordinada.</span><span class="sxs-lookup"><span data-stu-id="5c346-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="5c346-114">En la plantilla de hello, recursos de la aplicación se definen y se especifican parámetros de implementación para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="5c346-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="5c346-115">plantilla de Hello consta de JSON y expresiones que puede utilizar valores de tooconstruct para su implementación.</span><span class="sxs-lookup"><span data-stu-id="5c346-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="5c346-116">toolearn más, mire [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5c346-117">En la plantilla de hello, especifique Hola capacidad elemento:</span><span class="sxs-lookup"><span data-stu-id="5c346-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="5c346-118">Capacidad identifica número Hola de máquinas virtuales en el conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="5c346-119">Puede cambiar manualmente la capacidad de hello mediante la implementación de una plantilla con un valor diferente.</span><span class="sxs-lookup"><span data-stu-id="5c346-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="5c346-120">Si va a implementar una capacidad de Hola de cambio de plantilla tooonly, puede incluir únicamente el elemento SKU Hola con capacidad de hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="5c346-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="5c346-121">Hello capacidad de su conjunto de escala puede ajustarse automáticamente mediante una combinación de hello **autoscaleSettings** extensión de diagnósticos de hello y recursos.</span><span class="sxs-lookup"><span data-stu-id="5c346-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="5c346-122">Configurar la extensión de diagnósticos de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="5c346-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="5c346-123">El escalado automático solo es posible si la colección de métricas se realiza correctamente en cada máquina virtual en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="5c346-124">Hola extensión de diagnósticos de Azure proporciona capacidades de supervisión y diagnóstico de Hola que satisfaga las necesidades de colección de recursos de escalado automático de Hola Hola métricas.</span><span class="sxs-lookup"><span data-stu-id="5c346-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="5c346-125">Puede instalar la extensión de hello como parte de la plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="5c346-126">Este ejemplo muestra las variables de Hola que se usan en extensión de diagnósticos de hello plantilla tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="5c346-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="5c346-127">Cuando se implementa la plantilla de hello, se proporcionan parámetros.</span><span class="sxs-lookup"><span data-stu-id="5c346-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="5c346-128">En este ejemplo, nombre de Hola de cuenta de almacenamiento de hello (donde se almacenan los datos) y Hola se proporcionan el nombre del conjunto de escalas de hello (donde se recopilan los datos).</span><span class="sxs-lookup"><span data-stu-id="5c346-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="5c346-129">En este ejemplo de Windows Server, sólo el contador de rendimiento del número de subprocesos de Hola se recopila.</span><span class="sxs-lookup"><span data-stu-id="5c346-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="5c346-130">Hola a todos los contadores de rendimiento disponibles en Windows o Linux puede ser información de diagnóstico de toocollect utilizado y puede incluirse en la configuración de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="5c346-131">Este ejemplo muestra la definición de Hola de extensión de hello en plantilla hello:</span><span class="sxs-lookup"><span data-stu-id="5c346-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="5c346-132">Cuando se ejecuta la extensión de diagnósticos de hello, datos de Hola se almacenan y se recopilan en una tabla, en la cuenta de almacenamiento de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="5c346-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="5c346-133">Hola **WADPerformanceCounters** tabla, puede encontrar los datos recopilado de hello:</span><span class="sxs-lookup"><span data-stu-id="5c346-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="5c346-134">Configurar recursos de hello autoScaleSettings</span><span class="sxs-lookup"><span data-stu-id="5c346-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="5c346-135">recursos de Hello autoscaleSettings usa información de Hola de toodecide de extensión de diagnósticos de hello si ha establecido tooincrease o disminuir el número de Hola de máquinas virtuales en la escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="5c346-136">Este ejemplo muestra la configuración de hello del recurso de hello en plantilla hello:</span><span class="sxs-lookup"><span data-stu-id="5c346-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="5c346-137">En el ejemplo de Hola anterior, se crean dos reglas para definir las acciones de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="5c346-138">primera regla de Hello define la acción de escalado horizontal de Hola y segunda regla de Hola Hola escala en acción.</span><span class="sxs-lookup"><span data-stu-id="5c346-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="5c346-139">Estos valores se proporcionan en las reglas de hello:</span><span class="sxs-lookup"><span data-stu-id="5c346-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="5c346-140">Regla</span><span class="sxs-lookup"><span data-stu-id="5c346-140">Rule</span></span> | <span data-ttu-id="5c346-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="5c346-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="5c346-142">metricName</span><span class="sxs-lookup"><span data-stu-id="5c346-142">metricName</span></span>        | <span data-ttu-id="5c346-143">Este valor es Hola igual que el contador de rendimiento de Hola que definió en la variable de hello wadperfcounter para extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="5c346-144">En el ejemplo de Hola anterior, se usa el contador del número de subprocesos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="5c346-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="5c346-145">metricResourceUri</span></span> | <span data-ttu-id="5c346-146">Este valor es el identificador de recurso de hello del conjunto de escalas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="5c346-147">Este identificador contiene nombre Hola Hola del grupo de recursos, el nombre de Hola de proveedor de recursos de Hola y el nombre de Hola de tooscale de conjunto de escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="5c346-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="5c346-148">timeGrain</span></span>         | <span data-ttu-id="5c346-149">Este valor es la granularidad de Hola de métricas de Hola que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="5c346-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="5c346-150">En el anterior ejemplo de Hola, los datos se recopilan en un intervalo de un minuto.</span><span class="sxs-lookup"><span data-stu-id="5c346-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="5c346-151">Este valor se utiliza en combinación con timeWindow.</span><span class="sxs-lookup"><span data-stu-id="5c346-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="5c346-152">statistic</span><span class="sxs-lookup"><span data-stu-id="5c346-152">statistic</span></span>         | <span data-ttu-id="5c346-153">Este valor determina la forma métricas Hola Hola combinado tooaccommodate acción de escala automática.</span><span class="sxs-lookup"><span data-stu-id="5c346-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="5c346-154">Hola los valores posibles son: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="5c346-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="5c346-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="5c346-155">timeWindow</span></span>        | <span data-ttu-id="5c346-156">Este valor es Hola intervalo de tiempo en el que se recopilan datos de instancia.</span><span class="sxs-lookup"><span data-stu-id="5c346-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="5c346-157">Debe estar comprendido entre 5 minutos y 12 horas.</span><span class="sxs-lookup"><span data-stu-id="5c346-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="5c346-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="5c346-158">timeAggregation</span></span>   | <span data-ttu-id="5c346-159">Este valor determina cómo se deben combinar los datos de Hola que se recopilan con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="5c346-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="5c346-160">valor predeterminado de Hello es Media.</span><span class="sxs-lookup"><span data-stu-id="5c346-160">hello default value is Average.</span></span> <span data-ttu-id="5c346-161">Hola los valores posibles son: promedio, mínimo, máximo, último, Total, recuento.</span><span class="sxs-lookup"><span data-stu-id="5c346-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="5c346-162">operator</span><span class="sxs-lookup"><span data-stu-id="5c346-162">operator</span></span>          | <span data-ttu-id="5c346-163">Este valor es el operador de Hola que es usado toocompare Hola hello y datos de umbral de métrica.</span><span class="sxs-lookup"><span data-stu-id="5c346-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="5c346-164">Hola los valores posibles son: es igual a, valores, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="5c346-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="5c346-165">threshold</span><span class="sxs-lookup"><span data-stu-id="5c346-165">threshold</span></span>         | <span data-ttu-id="5c346-166">Este valor es el valor de Hola que desencadena la acción de escalado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="5c346-167">Ser seguro tooprovide una diferencia suficiente entre los valores de umbral de Hola para hello **escalada** y **de escala** acciones.</span><span class="sxs-lookup"><span data-stu-id="5c346-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="5c346-168">Si establece Hola mismos valores para ambas acciones, sistema de hello prevé cambio constante, lo que impide que se implementa una acción de escalado.</span><span class="sxs-lookup"><span data-stu-id="5c346-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="5c346-169">Por ejemplo, establecer ambos subprocesos too600 en el anterior ejemplo de Hola no funciona.</span><span class="sxs-lookup"><span data-stu-id="5c346-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="5c346-170">dirección</span><span class="sxs-lookup"><span data-stu-id="5c346-170">direction</span></span>         | <span data-ttu-id="5c346-171">Este valor determina la acción de Hola que se realiza cuando se obtiene el valor de umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="5c346-172">valores posibles de Hello son aumentan o disminuyen.</span><span class="sxs-lookup"><span data-stu-id="5c346-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="5c346-173">type</span><span class="sxs-lookup"><span data-stu-id="5c346-173">type</span></span>              | <span data-ttu-id="5c346-174">Este valor es el tipo de Hola de acción que se realizarán y se debe establecer tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="5c346-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="5c346-175">value</span><span class="sxs-lookup"><span data-stu-id="5c346-175">value</span></span>             | <span data-ttu-id="5c346-176">Este valor es el número de Hola de máquinas virtuales que se agregan tooor quitado del conjunto de escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="5c346-177">Este valor debe ser 1 o un valor superior.</span><span class="sxs-lookup"><span data-stu-id="5c346-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="5c346-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="5c346-178">cooldown</span></span>          | <span data-ttu-id="5c346-179">Este valor es cantidad de Hola de toowait de tiempo desde la última acción de escalado de hello antes de que se produce la acción siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="5c346-180">Debe estar comprendido entre un minuto y una semana.</span><span class="sxs-lookup"><span data-stu-id="5c346-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="5c346-181">Función de contador de rendimiento de hello, que está usando, algunos de los elementos de hello en configuración de plantilla de Hola se utilizan de manera diferente.</span><span class="sxs-lookup"><span data-stu-id="5c346-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="5c346-182">En el anterior ejemplo de Hola, contador de rendimiento de hello es el número de subprocesos, el valor del umbral de hello es 650 para una acción de escalado horizontal y el valor del umbral de hello es 550 para la acción de escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="5c346-183">Si usa un contador como porcentaje de tiempo de procesador, el valor del umbral de Hola se establece toohello porcentaje de uso de CPU que determina una acción de escalado.</span><span class="sxs-lookup"><span data-stu-id="5c346-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="5c346-184">Cuando se desencadena una acción de escalado, por ejemplo, una carga elevada, aumenta en función de valor de hello en plantilla Hola Hola capacidad de hello conjunto.</span><span class="sxs-lookup"><span data-stu-id="5c346-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="5c346-185">Por ejemplo, en una escala de establece donde capacidad Hola se establece too3 y se establece el valor de acción de escala de Hola too1:</span><span class="sxs-lookup"><span data-stu-id="5c346-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="5c346-186">Cuando Hola actual carga causas Hola subproceso promedio recuento toogo por encima del umbral de Hola de 650:</span><span class="sxs-lookup"><span data-stu-id="5c346-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="5c346-187">A **escalada** se desencadena la acción que causas Hola capacidad de hello conjunto toobe aumentado en uno:</span><span class="sxs-lookup"><span data-stu-id="5c346-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="5c346-188">resultado de Hello es que una máquina virtual se agrega el conjunto de escalas de toohello:</span><span class="sxs-lookup"><span data-stu-id="5c346-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="5c346-189">Tras un período de enfriamiento de cinco minutos, si promedio de Hola de subprocesos en máquinas de hello permanece en 600, otra máquina se agrega el conjunto toohello.</span><span class="sxs-lookup"><span data-stu-id="5c346-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="5c346-190">Si el número de subprocesos de promedio de hello permanezca por debajo de 550, capacidad de Hola de conjunto de escalas de Hola se reduce en uno y un equipo se quita del conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="5c346-191">Configuración del escalado con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c346-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="5c346-192">Mire toosee ejemplos del uso de PowerShell tooset la escala automática, [Monitor de Azure PowerShell rápido iniciar ejemplos](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="5c346-193">Configuración del escalado con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5c346-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="5c346-194">Mire toosee ejemplos del uso de CLI de Azure tooset la escala automática, [Monitor Azure multiplataforma CLI rápido iniciar ejemplos](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="5c346-195">Configurar el ajuste de escala con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5c346-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="5c346-196">Hola toosee muestra un ejemplo del uso de Azure tooset portal la escala automática, busque en [crear un conjunto de escala de máquinas virtuales mediante el portal de Azure de hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="5c346-197">Más información sobre las acciones de escalado</span><span class="sxs-lookup"><span data-stu-id="5c346-197">Investigate scaling actions</span></span>

* <span data-ttu-id="5c346-198">**Portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="5c346-198">**Azure portal**</span></span>  
<span data-ttu-id="5c346-199">Actualmente, puede obtener una cantidad limitada de información mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c346-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="5c346-200">**Explorador de recursos de Azure**</span><span class="sxs-lookup"><span data-stu-id="5c346-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="5c346-201">Esta herramienta es hello más adecuado para explorar el estado actual de Hola de su conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="5c346-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="5c346-202">Siga esta ruta de acceso y debería ver la vista de instancia de Hola de escala de hello establecido que creó:</span><span class="sxs-lookup"><span data-stu-id="5c346-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="5c346-203">**Subscriptions &gt; {su suscripción} &gt; resourceGroups &gt; {su grupo de recursos} &gt; providers &gt; Microsoft.Compute &gt; virtualMachineScaleSets &gt; {su conjunto de escalado} &gt; virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="5c346-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="5c346-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="5c346-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="5c346-205">Utilice este comando tooget cierta información:</span><span class="sxs-lookup"><span data-stu-id="5c346-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="5c346-206">Conectar máquina virtual de toohello jumpbox tal como lo haría con cualquier otro equipo y, a continuación, se pueden obtener acceso remoto a máquinas virtuales de hello en procesos individuales de hello escala conjunto toomonitor.</span><span class="sxs-lookup"><span data-stu-id="5c346-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c346-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c346-207">Next Steps</span></span>
* <span data-ttu-id="5c346-208">Mire [ajusta automáticamente las máquinas en un conjunto de escala de máquinas virtuales](virtual-machine-scale-sets-windows-autoscale.md) toosee un ejemplo de cómo toocreate una escala establece con el escalado automático configurado.</span><span class="sxs-lookup"><span data-stu-id="5c346-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="5c346-209">Encuentre ejemplos de características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de PowerShell de Azure Monitor](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="5c346-210">Obtenga información sobre las características de notificación de [usar escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="5c346-211">Obtenga información acerca de cómo demasiado[toosend webhook y correo electrónico notificaciones de alerta de registros de auditoría de uso en el Monitor de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="5c346-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="5c346-212">Más información sobre los [escenarios avanzados de escalado automático](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="5c346-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
