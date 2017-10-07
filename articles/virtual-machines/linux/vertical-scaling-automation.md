---
title: "escala aaaVertically máquina virtual de Azure con la automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toovertically escalar una máquina Virtual Linux en alertas de respuesta de toomonitoring con automatización de Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="870f5-103">Escalado vertical de máquinas virtuales Linux de Azure con Azure Automation</span><span class="sxs-lookup"><span data-stu-id="870f5-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="870f5-104">Escalado vertical es el proceso de Hola de aumentar o disminuir los recursos de Hola de un equipo de carga de trabajo de respuesta toohello.</span><span class="sxs-lookup"><span data-stu-id="870f5-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="870f5-105">En Azure, esto puede realizarse mediante el cambio de tamaño Hola de hello Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="870f5-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="870f5-106">Esto puede ayudar a los escenarios siguientes de Hola</span><span class="sxs-lookup"><span data-stu-id="870f5-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="870f5-107">Si no se utiliza con frecuencia Hola Máquina Virtual, éste se pueden cambiar hacia abajo tooa menor tamaño tooreduce los costos mensuales</span><span class="sxs-lookup"><span data-stu-id="870f5-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="870f5-108">Si Hola Máquina Virtual ve una carga máxima, puede ser tooincrease de tamaño mayor de tooa cuyo tamaño ha cambiado su capacidad máxima</span><span class="sxs-lookup"><span data-stu-id="870f5-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="870f5-109">esquema de Hola para hello pasos tooaccomplish se trata como a continuación</span><span class="sxs-lookup"><span data-stu-id="870f5-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="870f5-110">La instalación de las máquinas virtuales tooaccess de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="870f5-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="870f5-111">Importar runbooks de escala Vertical de automatización de Azure de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="870f5-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="870f5-112">Agregar un runbook de tooyour de webhook</span><span class="sxs-lookup"><span data-stu-id="870f5-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="870f5-113">Agregar una alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="870f5-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="870f5-114">Debido a un tamaño de Hola Hola primera máquina Virtual, se puede escalar, los tamaños de Hola puede ser limitada debido toohello disponibilidad de hello otros tamaños de clúster de hello actual Máquina Virtual está implementada en.</span><span class="sxs-lookup"><span data-stu-id="870f5-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="870f5-115">Hola publicado runbooks de automatización que se usan en este artículo se encargará de este caso y solo escalar dentro hello debajo de pares de tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="870f5-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="870f5-116">Esto significa que una máquina Virtual de Standard_D1v2 no repentinamente puede aumentarse tooStandard_G5 o reducida tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="870f5-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="870f5-117">Pares de escalado de tamaños de VM</span><span class="sxs-lookup"><span data-stu-id="870f5-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="870f5-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="870f5-118">Basic_A0</span></span> |<span data-ttu-id="870f5-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="870f5-119">Basic_A4</span></span> |
> | <span data-ttu-id="870f5-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="870f5-120">Standard_A0</span></span> |<span data-ttu-id="870f5-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="870f5-121">Standard_A4</span></span> |
> | <span data-ttu-id="870f5-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="870f5-122">Standard_A5</span></span> |<span data-ttu-id="870f5-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="870f5-123">Standard_A7</span></span> |
> | <span data-ttu-id="870f5-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="870f5-124">Standard_A8</span></span> |<span data-ttu-id="870f5-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="870f5-125">Standard_A9</span></span> |
> | <span data-ttu-id="870f5-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="870f5-126">Standard_A10</span></span> |<span data-ttu-id="870f5-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="870f5-127">Standard_A11</span></span> |
> | <span data-ttu-id="870f5-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="870f5-128">Standard_D1</span></span> |<span data-ttu-id="870f5-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="870f5-129">Standard_D4</span></span> |
> | <span data-ttu-id="870f5-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="870f5-130">Standard_D11</span></span> |<span data-ttu-id="870f5-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="870f5-131">Standard_D14</span></span> |
> | <span data-ttu-id="870f5-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="870f5-132">Standard_DS1</span></span> |<span data-ttu-id="870f5-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="870f5-133">Standard_DS4</span></span> |
> | <span data-ttu-id="870f5-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="870f5-134">Standard_DS11</span></span> |<span data-ttu-id="870f5-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="870f5-135">Standard_DS14</span></span> |
> | <span data-ttu-id="870f5-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="870f5-136">Standard_D1v2</span></span> |<span data-ttu-id="870f5-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="870f5-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="870f5-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="870f5-138">Standard_D11v2</span></span> |<span data-ttu-id="870f5-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="870f5-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="870f5-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="870f5-140">Standard_G1</span></span> |<span data-ttu-id="870f5-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="870f5-141">Standard_G5</span></span> |
> | <span data-ttu-id="870f5-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="870f5-142">Standard_GS1</span></span> |<span data-ttu-id="870f5-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="870f5-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="870f5-144">La instalación de las máquinas virtuales tooaccess de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="870f5-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="870f5-145">Hola primera cosa que necesita toodo es crear una cuenta de automatización de Azure que hospedará Hola runbooks usan tooscale Hola conjunto de escalado de VM instancias.</span><span class="sxs-lookup"><span data-stu-id="870f5-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="870f5-146">Servicio de automatización de hello había introducido recientemente característica "Ejecutar como cuenta de" hello lo que facilita configurar Hola entidad de servicio automáticamente runbooks en ejecución hello en nombre de usuario de hello muy fácil.</span><span class="sxs-lookup"><span data-stu-id="870f5-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="870f5-147">Puede leer más sobre esto en el siguiente artículo de hello:</span><span class="sxs-lookup"><span data-stu-id="870f5-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="870f5-148">Autenticación de Runbooks con una cuenta de ejecución de Azure</span><span class="sxs-lookup"><span data-stu-id="870f5-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="870f5-149">Importar runbooks de escala Vertical de automatización de Azure de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="870f5-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="870f5-150">Hola runbooks que son necesarios para escalar verticalmente la máquina Virtual ya se han publicado en hello Galería de runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="870f5-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="870f5-151">Deberá tooimport en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="870f5-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="870f5-152">Puede obtener información sobre cómo tooimport runbooks leyendo Hola artículo siguiente.</span><span class="sxs-lookup"><span data-stu-id="870f5-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="870f5-153">Galerías de runbooks y módulos para la automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="870f5-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="870f5-154">Hola runbooks que necesitan toobe importado se muestran en la imagen Hola siguiente</span><span class="sxs-lookup"><span data-stu-id="870f5-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importar runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="870f5-156">Agregar un runbook de tooyour de webhook</span><span class="sxs-lookup"><span data-stu-id="870f5-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="870f5-157">Una vez que haya importado Hola runbooks deberá tooadd un runbook de toohello webhook por lo que se puede desencadenar una alerta de una máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="870f5-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="870f5-158">detalles de Hola de cómo crear un webhook para el Runbook se pueden leer aquí</span><span class="sxs-lookup"><span data-stu-id="870f5-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="870f5-159">Webhooks de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="870f5-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="870f5-160">Asegúrese de que copiar hello webhook antes de cerrar el cuadro de diálogo de hello webhook ya que será necesario en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="870f5-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="870f5-161">Agregar una alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="870f5-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="870f5-162">Seleccione la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="870f5-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="870f5-163">Seleccione "Reglas de alerta".</span><span class="sxs-lookup"><span data-stu-id="870f5-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="870f5-164">Seleccione "Agregar alerta".</span><span class="sxs-lookup"><span data-stu-id="870f5-164">Select "Add alert"</span></span>
4. <span data-ttu-id="870f5-165">Seleccione una alerta de hello toofire métrica en</span><span class="sxs-lookup"><span data-stu-id="870f5-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="870f5-166">Seleccionar una condición que, cuando cumple will provocar Hola alerta toofire</span><span class="sxs-lookup"><span data-stu-id="870f5-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="870f5-167">Seleccione un umbral para la condición de hello en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="870f5-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="870f5-168">toobe cumplido</span><span class="sxs-lookup"><span data-stu-id="870f5-168">toobe fulfilled</span></span>
7. <span data-ttu-id="870f5-169">Seleccionar un período sobre qué Hola supervisar el servicio comprobará de condición de Hola y el umbral en los pasos 5 y 6</span><span class="sxs-lookup"><span data-stu-id="870f5-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="870f5-170">Pegue en webhook Hola que copió desde la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="870f5-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Agregar alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Agregar alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

