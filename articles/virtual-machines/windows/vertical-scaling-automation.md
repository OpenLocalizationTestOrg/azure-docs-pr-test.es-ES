---
title: "aaaUse toovertically de automatización de Azure escale máquinas virtuales de Windows | Documentos de Microsoft"
description: "Escalar verticalmente una máquina Virtual de Windows en las alertas de toomonitoring de respuesta con la automatización de Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="2bd65-103">Escalado vertical de máquinas virtuales de Windows con Azure Automation</span><span class="sxs-lookup"><span data-stu-id="2bd65-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="2bd65-104">Escalado vertical es el proceso de Hola de aumentar o disminuir los recursos de Hola de un equipo de carga de trabajo de respuesta toohello.</span><span class="sxs-lookup"><span data-stu-id="2bd65-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="2bd65-105">En Azure, esto puede realizarse mediante el cambio de tamaño Hola de hello Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="2bd65-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="2bd65-106">Esto puede ayudar a los escenarios siguientes de Hola</span><span class="sxs-lookup"><span data-stu-id="2bd65-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="2bd65-107">Si no se utiliza con frecuencia Hola Máquina Virtual, éste se pueden cambiar hacia abajo tooa menor tamaño tooreduce los costos mensuales</span><span class="sxs-lookup"><span data-stu-id="2bd65-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="2bd65-108">Si Hola Máquina Virtual ve una carga máxima, puede ser tooincrease de tamaño mayor de tooa cuyo tamaño ha cambiado su capacidad máxima</span><span class="sxs-lookup"><span data-stu-id="2bd65-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="2bd65-109">esquema de Hola para hello pasos tooaccomplish se trata como a continuación</span><span class="sxs-lookup"><span data-stu-id="2bd65-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="2bd65-110">La instalación de las máquinas virtuales tooaccess de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="2bd65-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="2bd65-111">Importar runbooks de escala Vertical de automatización de Azure de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="2bd65-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="2bd65-112">Agregar un runbook de tooyour de webhook</span><span class="sxs-lookup"><span data-stu-id="2bd65-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="2bd65-113">Agregar una alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="2bd65-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="2bd65-114">Debido a un tamaño de Hola Hola primera máquina Virtual, se puede escalar, los tamaños de Hola puede ser limitada debido toohello disponibilidad de hello otros tamaños de clúster de hello actual Máquina Virtual está implementada en.</span><span class="sxs-lookup"><span data-stu-id="2bd65-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="2bd65-115">Hola publicado runbooks de automatización que se usan en este artículo se encargará de este caso y solo escalar dentro hello debajo de pares de tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2bd65-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="2bd65-116">Esto significa que una máquina Virtual de Standard_D1v2 no repentinamente puede aumentarse tooStandard_G5 o reducida tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="2bd65-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="2bd65-117">Pares de escalado de tamaños de VM</span><span class="sxs-lookup"><span data-stu-id="2bd65-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="2bd65-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="2bd65-118">Basic_A0</span></span> |<span data-ttu-id="2bd65-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="2bd65-119">Basic_A4</span></span> |
> | <span data-ttu-id="2bd65-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="2bd65-120">Standard_A0</span></span> |<span data-ttu-id="2bd65-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="2bd65-121">Standard_A4</span></span> |
> | <span data-ttu-id="2bd65-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="2bd65-122">Standard_A5</span></span> |<span data-ttu-id="2bd65-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="2bd65-123">Standard_A7</span></span> |
> | <span data-ttu-id="2bd65-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="2bd65-124">Standard_A8</span></span> |<span data-ttu-id="2bd65-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="2bd65-125">Standard_A9</span></span> |
> | <span data-ttu-id="2bd65-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="2bd65-126">Standard_A10</span></span> |<span data-ttu-id="2bd65-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="2bd65-127">Standard_A11</span></span> |
> | <span data-ttu-id="2bd65-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="2bd65-128">Standard_D1</span></span> |<span data-ttu-id="2bd65-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="2bd65-129">Standard_D4</span></span> |
> | <span data-ttu-id="2bd65-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="2bd65-130">Standard_D11</span></span> |<span data-ttu-id="2bd65-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="2bd65-131">Standard_D14</span></span> |
> | <span data-ttu-id="2bd65-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="2bd65-132">Standard_DS1</span></span> |<span data-ttu-id="2bd65-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="2bd65-133">Standard_DS4</span></span> |
> | <span data-ttu-id="2bd65-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="2bd65-134">Standard_DS11</span></span> |<span data-ttu-id="2bd65-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="2bd65-135">Standard_DS14</span></span> |
> | <span data-ttu-id="2bd65-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="2bd65-136">Standard_D1v2</span></span> |<span data-ttu-id="2bd65-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="2bd65-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="2bd65-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="2bd65-138">Standard_D11v2</span></span> |<span data-ttu-id="2bd65-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="2bd65-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="2bd65-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="2bd65-140">Standard_G1</span></span> |<span data-ttu-id="2bd65-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="2bd65-141">Standard_G5</span></span> |
> | <span data-ttu-id="2bd65-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="2bd65-142">Standard_GS1</span></span> |<span data-ttu-id="2bd65-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="2bd65-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="2bd65-144">La instalación de las máquinas virtuales tooaccess de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="2bd65-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="2bd65-145">Hola primera cosa que necesita toodo es crear una cuenta de automatización de Azure que hospedará Hola runbooks usan tooscale una máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="2bd65-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale a Virtual Machine.</span></span> <span data-ttu-id="2bd65-146">Servicio de automatización de hello había introducido recientemente característica "Ejecutar como cuenta de" hello lo que facilita configurar Hola entidad de servicio automáticamente runbooks en ejecución hello en nombre de usuario de hello muy fácil.</span><span class="sxs-lookup"><span data-stu-id="2bd65-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="2bd65-147">Puede leer más sobre esto en el siguiente artículo de hello:</span><span class="sxs-lookup"><span data-stu-id="2bd65-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="2bd65-148">Autenticación de Runbooks con una cuenta de ejecución de Azure</span><span class="sxs-lookup"><span data-stu-id="2bd65-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="2bd65-149">Importar runbooks de escala Vertical de automatización de Azure de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="2bd65-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="2bd65-150">Hola runbooks que son necesarios para escalar verticalmente la máquina Virtual ya se han publicado en hello Galería de runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="2bd65-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="2bd65-151">Deberá tooimport en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="2bd65-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="2bd65-152">Puede obtener información sobre cómo tooimport runbooks leyendo Hola artículo siguiente.</span><span class="sxs-lookup"><span data-stu-id="2bd65-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="2bd65-153">Galerías de runbooks y módulos para la automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="2bd65-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="2bd65-154">Hola runbooks que necesitan toobe importado se muestran en la imagen Hola siguiente</span><span class="sxs-lookup"><span data-stu-id="2bd65-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importar runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="2bd65-156">Agregar un runbook de tooyour de webhook</span><span class="sxs-lookup"><span data-stu-id="2bd65-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="2bd65-157">Una vez que haya importado Hola runbooks deberá tooadd un runbook de toohello webhook por lo que se puede desencadenar una alerta de una máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="2bd65-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="2bd65-158">detalles de Hola de cómo crear un webhook para el Runbook se pueden leer aquí</span><span class="sxs-lookup"><span data-stu-id="2bd65-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="2bd65-159">Webhooks de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="2bd65-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="2bd65-160">Asegúrese de que copiar hello webhook antes de cerrar el cuadro de diálogo de hello webhook ya que será necesario en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="2bd65-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="2bd65-161">Agregar una alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="2bd65-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="2bd65-162">Seleccione la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2bd65-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="2bd65-163">Seleccione "Reglas de alerta".</span><span class="sxs-lookup"><span data-stu-id="2bd65-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="2bd65-164">Seleccione "Agregar alerta".</span><span class="sxs-lookup"><span data-stu-id="2bd65-164">Select "Add alert"</span></span>
4. <span data-ttu-id="2bd65-165">Seleccione una alerta de hello toofire métrica en</span><span class="sxs-lookup"><span data-stu-id="2bd65-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="2bd65-166">Seleccionar una condición que, cuando cumple will provocar Hola alerta toofire</span><span class="sxs-lookup"><span data-stu-id="2bd65-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="2bd65-167">Seleccione un umbral para la condición de hello en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="2bd65-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="2bd65-168">toobe cumplido</span><span class="sxs-lookup"><span data-stu-id="2bd65-168">toobe fulfilled</span></span>
7. <span data-ttu-id="2bd65-169">Seleccionar un período sobre qué Hola supervisar el servicio comprobará de condición de Hola y el umbral en los pasos 5 y 6</span><span class="sxs-lookup"><span data-stu-id="2bd65-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="2bd65-170">Pegue en webhook Hola que copió desde la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bd65-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Agregar alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Agregar alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

