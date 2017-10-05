---
title: "Usar Azure Automation para escalar verticalmente máquinas virtuales Windows | Microsoft Docs"
description: "Escalado vertical de una máquina virtual de Windows en respuesta a las alertas de supervisión con Azure Automation"
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
ms.openlocfilehash: ea5169c1a95f00e78ae3f5f177812466eb7a0deb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="9febd-103">Escalado vertical de máquinas virtuales de Windows con Azure Automation</span><span class="sxs-lookup"><span data-stu-id="9febd-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="9febd-104">El escalado vertical es el proceso de aumentar o disminuir los recursos de una máquina como respuesta a la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9febd-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="9febd-105">Para lograrlo en Azure, cambie el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="9febd-106">Esto puede ser útil en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="9febd-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="9febd-107">Si la máquina virtual no se utiliza con frecuencia, puede disminuir su tamaño para reducir los costos mensuales.</span><span class="sxs-lookup"><span data-stu-id="9febd-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="9febd-108">Si la máquina virtual experimenta una carga máxima, es posible ajustarla en un mayor tamaño para aumentar su capacidad.</span><span class="sxs-lookup"><span data-stu-id="9febd-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="9febd-109">Los pasos para lograr esto se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="9febd-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="9febd-110">Configurar la Automatización de Azure para tener acceso a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9febd-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="9febd-111">Importar los runbooks de escalado vertical de Automatización de Azure a la suscripción</span><span class="sxs-lookup"><span data-stu-id="9febd-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="9febd-112">Agregar un webhook al runbook.</span><span class="sxs-lookup"><span data-stu-id="9febd-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="9febd-113">Agregar una alerta a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="9febd-114">Debido al tamaño de la primera máquina virtual, los tamaños a los que se puede escalar pueden estar limitados en virtud de la disponibilidad de los demás tamaños en el clúster donde actualmente está implementada la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="9febd-115">En los runbooks de automatización publicados que se usan en este artículo nos hacemos cargo de esta situación y solo escalamos dentro de los siguientes pares de tamaños de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="9febd-116">Esto significa que una máquina virtual Standard_D1v2 no se aumentará de manera repentina a Standard_G5 ni se reducirá a Basic_A0.</span><span class="sxs-lookup"><span data-stu-id="9febd-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="9febd-117">Pares de escalado de tamaños de VM</span><span class="sxs-lookup"><span data-stu-id="9febd-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="9febd-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="9febd-118">Basic_A0</span></span> |<span data-ttu-id="9febd-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="9febd-119">Basic_A4</span></span> |
> | <span data-ttu-id="9febd-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="9febd-120">Standard_A0</span></span> |<span data-ttu-id="9febd-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="9febd-121">Standard_A4</span></span> |
> | <span data-ttu-id="9febd-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="9febd-122">Standard_A5</span></span> |<span data-ttu-id="9febd-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="9febd-123">Standard_A7</span></span> |
> | <span data-ttu-id="9febd-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="9febd-124">Standard_A8</span></span> |<span data-ttu-id="9febd-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="9febd-125">Standard_A9</span></span> |
> | <span data-ttu-id="9febd-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="9febd-126">Standard_A10</span></span> |<span data-ttu-id="9febd-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="9febd-127">Standard_A11</span></span> |
> | <span data-ttu-id="9febd-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="9febd-128">Standard_D1</span></span> |<span data-ttu-id="9febd-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="9febd-129">Standard_D4</span></span> |
> | <span data-ttu-id="9febd-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="9febd-130">Standard_D11</span></span> |<span data-ttu-id="9febd-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="9febd-131">Standard_D14</span></span> |
> | <span data-ttu-id="9febd-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="9febd-132">Standard_DS1</span></span> |<span data-ttu-id="9febd-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="9febd-133">Standard_DS4</span></span> |
> | <span data-ttu-id="9febd-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="9febd-134">Standard_DS11</span></span> |<span data-ttu-id="9febd-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="9febd-135">Standard_DS14</span></span> |
> | <span data-ttu-id="9febd-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="9febd-136">Standard_D1v2</span></span> |<span data-ttu-id="9febd-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="9febd-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="9febd-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="9febd-138">Standard_D11v2</span></span> |<span data-ttu-id="9febd-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="9febd-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="9febd-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="9febd-140">Standard_G1</span></span> |<span data-ttu-id="9febd-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="9febd-141">Standard_G5</span></span> |
> | <span data-ttu-id="9febd-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="9febd-142">Standard_GS1</span></span> |<span data-ttu-id="9febd-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="9febd-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="9febd-144">Configurar la Automatización de Azure para tener acceso a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9febd-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="9febd-145">Lo primero que debe hacer es crear una cuenta de Automatización de Azure que hospedará los runbooks que se usan para escalar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale a Virtual Machine.</span></span> <span data-ttu-id="9febd-146">Recientemente, el servicio de automatización presentó la característica "Cuenta de ejecución", que facilita la configuración de la entidad de servicio para ejecutar los Runbooks automáticamente en nombre de un usuario.</span><span class="sxs-lookup"><span data-stu-id="9febd-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="9febd-147">Encontrará más información al respecto en el siguiente artículo:</span><span class="sxs-lookup"><span data-stu-id="9febd-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="9febd-148">Autenticación de Runbooks con una cuenta de ejecución de Azure</span><span class="sxs-lookup"><span data-stu-id="9febd-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="9febd-149">Importar los runbooks de escalado vertical de Automatización de Azure a la suscripción</span><span class="sxs-lookup"><span data-stu-id="9febd-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="9febd-150">Los runbooks necesarios para el escalado vertical de la máquina virtual están publicados actualmente en la galería de runbooks de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="9febd-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="9febd-151">Deberá importarlos a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="9febd-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="9febd-152">En el siguiente artículo, puede obtener información sobre cómo importar runbooks:</span><span class="sxs-lookup"><span data-stu-id="9febd-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="9febd-153">Galerías de runbooks y módulos para la automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="9febd-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="9febd-154">En la imagen que aparece a continuación, se muestran los runbooks que es necesario importar:</span><span class="sxs-lookup"><span data-stu-id="9febd-154">The runbooks that need to be imported are shown in the image below</span></span>

![Importar runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="9febd-156">Agregar un webhook al runbook.</span><span class="sxs-lookup"><span data-stu-id="9febd-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="9febd-157">Una vez que importe los runbooks, deberá agregar un webhook al runbook para que, de este modo, una alerta proveniente de una máquina virtual pueda desencadenarlo.</span><span class="sxs-lookup"><span data-stu-id="9febd-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="9febd-158">A continuación, puede leer los detalles sobre cómo crear un webhook para el runbook:</span><span class="sxs-lookup"><span data-stu-id="9febd-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="9febd-159">Webhooks de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="9febd-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="9febd-160">Asegúrese de copiar el webhook antes de cerrar el cuadro de diálogo de webhook, porque lo necesitará en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="9febd-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="9febd-161">Agregar una alerta a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="9febd-162">Seleccione la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9febd-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="9febd-163">Seleccione "Reglas de alerta".</span><span class="sxs-lookup"><span data-stu-id="9febd-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="9febd-164">Seleccione "Agregar alerta".</span><span class="sxs-lookup"><span data-stu-id="9febd-164">Select "Add alert"</span></span>
4. <span data-ttu-id="9febd-165">Seleccione una métrica según la cual activar la alerta.</span><span class="sxs-lookup"><span data-stu-id="9febd-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="9febd-166">Seleccione una condición que, cuando se cumpla, hará que se active la alerta.</span><span class="sxs-lookup"><span data-stu-id="9febd-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="9febd-167">Seleccione un umbral para la condición establecida en el paso 5</span><span class="sxs-lookup"><span data-stu-id="9febd-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="9febd-168">que se satisfaga.</span><span class="sxs-lookup"><span data-stu-id="9febd-168">to be fulfilled</span></span>
7. <span data-ttu-id="9febd-169">Seleccione un período durante el cual el servicio de supervisión comprobará la condición y el umbral que se establecieron en los pasos 5 y 6.</span><span class="sxs-lookup"><span data-stu-id="9febd-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="9febd-170">Péguelo en el webhook que copió desde la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="9febd-170">Paste in the webhook you copied from the previous section.</span></span>

![Agregar alerta a máquina virtual 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Agregar alerta a máquina virtual 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

