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
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="c7021-103">Autoescala vertical con conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c7021-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="c7021-104">Este artículo describe cómo toovertically escalar Azure [conjuntos de escalas de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/) con o sin reaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="c7021-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="c7021-105">Para el escalado de máquinas virtuales que no están en conjuntos de escalado vertical, consulte demasiado[escalar verticalmente la máquina virtual de Azure con la automatización de Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7021-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c7021-106">Escalado vertical, también conocido como *escalar verticalmente* y *reducir*, significa que aumenta o disminuye el tamaño de máquina virtual (VM) de carga de trabajo de respuesta tooa.</span><span class="sxs-lookup"><span data-stu-id="c7021-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="c7021-107">Compare esto con [escalado horizontal](virtual-machine-scale-sets-autoscale-overview.md), también denominada tooas *escalar horizontalmente* y *escalar en*, donde se modifica el número de Hola de máquinas virtuales según la carga de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7021-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="c7021-108">Reaprovisionar significa quitar una máquina virtual existente y reemplazarla por una nueva.</span><span class="sxs-lookup"><span data-stu-id="c7021-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="c7021-109">Cuando aumente o disminuya el tamaño de Hola de máquinas virtuales en un conjunto de escala de máquinas virtuales, en algunos casos desee tooresize existente de las máquinas virtuales y conservar los datos, mientras que en otros casos deberá toodeploy nuevas máquinas virtuales del nuevo tamaño de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7021-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="c7021-110">Este documento describe ambos casos.</span><span class="sxs-lookup"><span data-stu-id="c7021-110">This document covers both cases.</span></span>

<span data-ttu-id="c7021-111">El escalado vertical puede resultar útil cuando:</span><span class="sxs-lookup"><span data-stu-id="c7021-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="c7021-112">Un servicio integrado en máquinas virtuales se está infrautilizando (por ejemplo, los fines de semana).</span><span class="sxs-lookup"><span data-stu-id="c7021-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="c7021-113">Reducir tamaño de máquina virtual de hello puede reducir los costos mensuales.</span><span class="sxs-lookup"><span data-stu-id="c7021-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="c7021-114">Toocope aumenta de tamaño VM con mayor demanda sin crear máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="c7021-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="c7021-115">Puede configurar vertical escalado toobe desencadenada basado en métricas alertas en función de su conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c7021-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="c7021-116">Cuando se activa la alerta de Hola que desencadene un webhook que desencadena un runbook que se puede ampliar su escala establece hacia arriba o hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="c7021-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="c7021-117">El escalado vertical puede configurarse siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c7021-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="c7021-118">Cree una cuenta de Automatización de Azure con funciones de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c7021-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="c7021-119">Importe a la suscripción los Runbooks de escalado vertical de Automatización de Azure para los conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c7021-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="c7021-120">Agregar un runbook de tooyour de webhook.</span><span class="sxs-lookup"><span data-stu-id="c7021-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="c7021-121">Agregar una alerta tooyour conjunto de escalado de máquinas virtuales mediante una notificación de webhook.</span><span class="sxs-lookup"><span data-stu-id="c7021-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="c7021-122">La autoescala vertical solo se puede realizar en determinados intervalos de tamaños de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7021-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="c7021-123">Comparar las especificaciones de Hola de cada tamaño antes de decidir tooscale desde un tooanother (número más alto no siempre indica tamaño de máquina virtual más grande).</span><span class="sxs-lookup"><span data-stu-id="c7021-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="c7021-124">Puede elegir tooscale entre Hola siguientes pares de tamaños:</span><span class="sxs-lookup"><span data-stu-id="c7021-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="c7021-125">Pares de escalado de tamaños de VM</span><span class="sxs-lookup"><span data-stu-id="c7021-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="c7021-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="c7021-126">Standard_A0</span></span> |<span data-ttu-id="c7021-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="c7021-127">Standard_A11</span></span> |
> | <span data-ttu-id="c7021-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="c7021-128">Standard_D1</span></span> |<span data-ttu-id="c7021-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="c7021-129">Standard_D14</span></span> |
> | <span data-ttu-id="c7021-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="c7021-130">Standard_DS1</span></span> |<span data-ttu-id="c7021-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="c7021-131">Standard_DS14</span></span> |
> | <span data-ttu-id="c7021-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="c7021-132">Standard_D1v2</span></span> |<span data-ttu-id="c7021-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="c7021-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="c7021-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="c7021-134">Standard_G1</span></span> |<span data-ttu-id="c7021-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="c7021-135">Standard_G5</span></span> |
> | <span data-ttu-id="c7021-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="c7021-136">Standard_GS1</span></span> |<span data-ttu-id="c7021-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="c7021-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="c7021-138">Creación de una cuenta de Automatización de Azure con funciones de ejecución</span><span class="sxs-lookup"><span data-stu-id="c7021-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="c7021-139">Hola primera cosa que necesita toodo es crear una cuenta de automatización de Azure que hospedará Hola runbooks usan tooscale Hola conjunto de escalado de VM instancias.</span><span class="sxs-lookup"><span data-stu-id="c7021-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="c7021-140">Recientemente [automatización de Azure](https://azure.microsoft.com/services/automation/) introdujo la característica "Ejecutar como cuenta de" hello lo que facilita configurar Hola entidad de servicio automáticamente runbooks en ejecución hello en nombre de usuario muy fácil.</span><span class="sxs-lookup"><span data-stu-id="c7021-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="c7021-141">Puede leer más sobre esto en el siguiente artículo de hello:</span><span class="sxs-lookup"><span data-stu-id="c7021-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="c7021-142">Autenticación de Runbooks con una cuenta de ejecución de Azure</span><span class="sxs-lookup"><span data-stu-id="c7021-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="c7021-143">Importación de Runbooks de escalado vertical de Automatización de Azure a la suscripción</span><span class="sxs-lookup"><span data-stu-id="c7021-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="c7021-144">Hola runbooks necesita escala toovertically que los conjuntos de escalas de VM ya se han publicado en hello Galería de runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7021-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="c7021-145">tooimport en su suscripción siguen Hola los pasos de este artículo:</span><span class="sxs-lookup"><span data-stu-id="c7021-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="c7021-146">Galerías de runbooks y módulos para la automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="c7021-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="c7021-147">Elija la opción de examinar la Galería de Hola del menú de Runbooks de hello:</span><span class="sxs-lookup"><span data-stu-id="c7021-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Toobe runbooks importado][runbooks]

<span data-ttu-id="c7021-149">se muestran runbooks Hola que necesitan toobe importado.</span><span class="sxs-lookup"><span data-stu-id="c7021-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="c7021-150">Seleccione el runbook de hello en función de si desea escalar con o sin reaprovisionamiento vertical:</span><span class="sxs-lookup"><span data-stu-id="c7021-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galería de Runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="c7021-152">Agregar un runbook de tooyour de webhook</span><span class="sxs-lookup"><span data-stu-id="c7021-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="c7021-153">Una vez que haya importado Hola runbooks deberá tooadd un runbook de toohello webhook por lo que se puede desencadenar una alerta de un conjunto de escala de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7021-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="c7021-154">detalles de Hola de crear un webhook para el Runbook se describen en este artículo:</span><span class="sxs-lookup"><span data-stu-id="c7021-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="c7021-155">Webhooks de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="c7021-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="c7021-156">Asegúrese de que copiar hello webhook URI antes de cerrar el cuadro de diálogo de hello webhook ya que será necesario en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="c7021-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="c7021-157">Agregar una alerta tooyour conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="c7021-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="c7021-158">A continuación se muestra un PowerShell script que muestra cómo tooadd una alerta tooa conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c7021-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="c7021-159">Consulte toohello siguiendo el nombre del artículo tooget Hola de alerta de hello toofire métrica hello: [métricas comunes de escalado automático de Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c7021-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="c7021-160">Es recomienda tooconfigure un período de tiempo razonable de alerta de hello en tooavoid orden desencadenar escalado vertical, y a cualquier asociado interrupción del servicio, con demasiada frecuencia.</span><span class="sxs-lookup"><span data-stu-id="c7021-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="c7021-161">Considere un intervalo mínimo de 20 a 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="c7021-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="c7021-162">Tenga en cuenta si necesita tooavoid ninguna interrupción de ajuste de escala horizontal.</span><span class="sxs-lookup"><span data-stu-id="c7021-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="c7021-163">Para obtener más información sobre cómo toocreate alertas consulte toohello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c7021-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="c7021-164">Ejemplos de inicio rápido de PowerShell de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="c7021-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="c7021-165">Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="c7021-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="c7021-166">Resumen</span><span class="sxs-lookup"><span data-stu-id="c7021-166">Summary</span></span>
<span data-ttu-id="c7021-167">En este artículo se mostraron ejemplos sencillos de escalado vertical.</span><span class="sxs-lookup"><span data-stu-id="c7021-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="c7021-168">Con estos bloques de creación (cuenta de automatización, Runbooks, webhooks, alertas) puede conectar una gran variedad de eventos con un conjunto personalizado de acciones.</span><span class="sxs-lookup"><span data-stu-id="c7021-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
