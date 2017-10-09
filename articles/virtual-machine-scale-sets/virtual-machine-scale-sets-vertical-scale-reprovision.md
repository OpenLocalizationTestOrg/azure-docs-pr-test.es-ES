---
title: "conjuntos de escalas de máquina virtual de Azure de escala aaaVertically | Documentos de Microsoft"
description: "¿Cómo toovertically escalar una máquina Virtual en las alertas de toomonitoring de respuesta con la automatización de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Autoescala vertical con conjuntos de escalado de máquinas virtuales
Este artículo describe cómo toovertically escalar Azure [conjuntos de escalas de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/) con o sin reaprovisionamiento. Para el escalado de máquinas virtuales que no están en conjuntos de escalado vertical, consulte demasiado[escalar verticalmente la máquina virtual de Azure con la automatización de Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Escalado vertical, también conocido como *escalar verticalmente* y *reducir*, significa que aumenta o disminuye el tamaño de máquina virtual (VM) de carga de trabajo de respuesta tooa. Compare esto con [escalado horizontal](virtual-machine-scale-sets-autoscale-overview.md), también denominada tooas *escalar horizontalmente* y *escalar en*, donde se modifica el número de Hola de máquinas virtuales según la carga de trabajo de Hola.

Reaprovisionar significa quitar una máquina virtual existente y reemplazarla por una nueva. Cuando aumente o disminuya el tamaño de Hola de máquinas virtuales en un conjunto de escala de máquinas virtuales, en algunos casos desee tooresize existente de las máquinas virtuales y conservar los datos, mientras que en otros casos deberá toodeploy nuevas máquinas virtuales del nuevo tamaño de Hola. Este documento describe ambos casos.

El escalado vertical puede resultar útil cuando:

* Un servicio integrado en máquinas virtuales se está infrautilizando (por ejemplo, los fines de semana). Reducir tamaño de máquina virtual de hello puede reducir los costos mensuales.
* Toocope aumenta de tamaño VM con mayor demanda sin crear máquinas virtuales adicionales.

Puede configurar vertical escalado toobe desencadenada basado en métricas alertas en función de su conjunto de escalado de máquinas virtuales. Cuando se activa la alerta de Hola que desencadene un webhook que desencadena un runbook que se puede ampliar su escala establece hacia arriba o hacia abajo. El escalado vertical puede configurarse siguiendo estos pasos:

1. Cree una cuenta de Automatización de Azure con funciones de ejecución.
2. Importe a la suscripción los Runbooks de escalado vertical de Automatización de Azure para los conjuntos de escalado de máquinas virtuales.
3. Agregar un runbook de tooyour de webhook.
4. Agregar una alerta tooyour conjunto de escalado de máquinas virtuales mediante una notificación de webhook.

> [!NOTE]
> La autoescala vertical solo se puede realizar en determinados intervalos de tamaños de máquina virtual. Comparar las especificaciones de Hola de cada tamaño antes de decidir tooscale desde un tooanother (número más alto no siempre indica tamaño de máquina virtual más grande). Puede elegir tooscale entre Hola siguientes pares de tamaños:
> 
> | Pares de escalado de tamaños de VM |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Creación de una cuenta de Automatización de Azure con funciones de ejecución
Hola primera cosa que necesita toodo es crear una cuenta de automatización de Azure que hospedará Hola runbooks usan tooscale Hola conjunto de escalado de VM instancias. Recientemente [automatización de Azure](https://azure.microsoft.com/services/automation/) introdujo la característica "Ejecutar como cuenta de" hello lo que facilita configurar Hola entidad de servicio automáticamente runbooks en ejecución hello en nombre de usuario muy fácil. Puede leer más sobre esto en el siguiente artículo de hello:

* [Autenticación de Runbooks con una cuenta de ejecución de Azure](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importación de Runbooks de escalado vertical de Automatización de Azure a la suscripción
Hola runbooks necesita escala toovertically que los conjuntos de escalas de VM ya se han publicado en hello Galería de runbooks de automatización de Azure. tooimport en su suscripción siguen Hola los pasos de este artículo:

* [Galerías de runbooks y módulos para la automatización de Azure](../automation/automation-runbook-gallery.md)

Elija la opción de examinar la Galería de Hola del menú de Runbooks de hello:

![Toobe runbooks importado][runbooks]

se muestran runbooks Hola que necesitan toobe importado. Seleccione el runbook de hello en función de si desea escalar con o sin reaprovisionamiento vertical:

![Galería de Runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Agregar un runbook de tooyour de webhook
Una vez que haya importado Hola runbooks deberá tooadd un runbook de toohello webhook por lo que se puede desencadenar una alerta de un conjunto de escala de la máquina virtual. detalles de Hola de crear un webhook para el Runbook se describen en este artículo:

* [Webhooks de Automatización de Azure](../automation/automation-webhooks.md)

> [!NOTE]
> Asegúrese de que copiar hello webhook URI antes de cerrar el cuadro de diálogo de hello webhook ya que será necesario en la sección siguiente Hola.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Agregar una alerta tooyour conjunto de escala de VM.
A continuación se muestra un PowerShell script que muestra cómo tooadd una alerta tooa conjunto de escalado de máquinas virtuales. Consulte toohello siguiendo el nombre del artículo tooget Hola de alerta de hello toofire métrica hello: [métricas comunes de escalado automático de Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> Es recomienda tooconfigure un período de tiempo razonable de alerta de hello en tooavoid orden desencadenar escalado vertical, y a cualquier asociado interrupción del servicio, con demasiada frecuencia. Considere un intervalo mínimo de 20 a 30 minutos. Tenga en cuenta si necesita tooavoid ninguna interrupción de ajuste de escala horizontal.
> 
> 

Para obtener más información sobre cómo toocreate alertas consulte toohello siguientes artículos:

* [Ejemplos de inicio rápido de PowerShell de Azure Monitor](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Resumen
En este artículo se mostraron ejemplos sencillos de escalado vertical. Con estos bloques de creación (cuenta de automatización, Runbooks, webhooks, alertas) puede conectar una gran variedad de eventos con un conjunto personalizado de acciones.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
