---
title: "implementación de VM de Linux-RM aaaTroubleshoot | Documentos de Microsoft"
description: "Solución de problemas de implementación de Resource Manager cuando crea una nueva máquina virtual de Linux en Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="24419-103">Solución de problemas de la implementación de Resource Manager con la creación de una nueva máquina virtual de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="24419-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="24419-104">Principales problemas</span><span class="sxs-lookup"><span data-stu-id="24419-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="24419-105">Para consultar otros problemas de implementación de máquinas virtuales y preguntas, vea [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Solución de problemas de implementación de máquinas virtuales de Linux en Azure).</span><span class="sxs-lookup"><span data-stu-id="24419-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="24419-106">Recopilación de registros de actividad</span><span class="sxs-lookup"><span data-stu-id="24419-106">Collect activity logs</span></span>
<span data-ttu-id="24419-107">toostart solución de problemas, actividad hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="24419-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="24419-108">Hello vínculos siguientes contienen información detallada sobre Hola proceso toofollow.</span><span class="sxs-lookup"><span data-stu-id="24419-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="24419-109">Ver operaciones de implementación</span><span class="sxs-lookup"><span data-stu-id="24419-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="24419-110">Ver registros de actividad toomanage Azure recursos</span><span class="sxs-lookup"><span data-stu-id="24419-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="24419-111">**Y:** si Hola SO es Linux generalizado y se ha cargado ni capturado con hello generalizado configuración, no habrá errores.</span><span class="sxs-lookup"><span data-stu-id="24419-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="24419-112">De forma similar, si Hola SO está especializado de Linux, y se ha cargado ni capturado con hello especializados configuración, a continuación, no habrá los errores.</span><span class="sxs-lookup"><span data-stu-id="24419-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="24419-113">**Errores de carga:**</span><span class="sxs-lookup"><span data-stu-id="24419-113">**Upload Errors:**</span></span>

<span data-ttu-id="24419-114">**N<sup>1</sup>:** si Hola SO es Linux generalizado, y se carga como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola VM está atascada en hello fase de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="24419-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="24419-115">**N<sup>2</sup>:** si hello SO es especializado de Linux y cargarlo como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password.</span><span class="sxs-lookup"><span data-stu-id="24419-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="24419-116">**Resolución:**</span><span class="sxs-lookup"><span data-stu-id="24419-116">**Resolution:**</span></span>

<span data-ttu-id="24419-117">tooresolve ambos estos errores, cargar Hola VHD original, disponible en local, con Hola misma configuración que para hello OS (generalizado/especializado).</span><span class="sxs-lookup"><span data-stu-id="24419-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="24419-118">tooupload como generalizado, recuerde toorun-desaprovisionar primero.</span><span class="sxs-lookup"><span data-stu-id="24419-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="24419-119">**Errores de captura:**</span><span class="sxs-lookup"><span data-stu-id="24419-119">**Capture Errors:**</span></span>

<span data-ttu-id="24419-120">**N<sup>3</sup>:** si Hola SO es Linux generalizado, y se capturan como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola original máquina virtual no se puede usar tal y como está marcado como generalizado.</span><span class="sxs-lookup"><span data-stu-id="24419-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="24419-121">**N<sup>4</sup>:** si hello SO es especializado de Linux, y se capturan como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password.</span><span class="sxs-lookup"><span data-stu-id="24419-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="24419-122">Además, Hola original VM no es puede usar porque está marcado como especializadas.</span><span class="sxs-lookup"><span data-stu-id="24419-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="24419-123">**Resolución:**</span><span class="sxs-lookup"><span data-stu-id="24419-123">**Resolution:**</span></span>

<span data-ttu-id="24419-124">tooresolve ambos estos errores, eliminar la imagen actual de Hola desde el portal de hello, y [capturar de hello VHD actual](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) con Hola la misma configuración que para hello OS (generalizado/especializado).</span><span class="sxs-lookup"><span data-stu-id="24419-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="24419-125">Problema: Imagen de galería/marketplace/personalizada; error de asignación</span><span class="sxs-lookup"><span data-stu-id="24419-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="24419-126">Este error se produce en situaciones cuando la solicitud de máquina virtual nueva de hello es clúster tooa anclados que no es compatible con el tamaño de la máquina virtual de Hola que se solicita o no tiene espacio libre disponible tooaccommodate Hola solicitud.</span><span class="sxs-lookup"><span data-stu-id="24419-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="24419-127">**Causa 1:** no admiten clústeres de Hola Hola solicitado tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24419-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="24419-128">**Resolución 1:**</span><span class="sxs-lookup"><span data-stu-id="24419-128">**Resolution 1:**</span></span>

* <span data-ttu-id="24419-129">Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24419-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="24419-130">Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="24419-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="24419-131">Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="24419-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="24419-132">Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="24419-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="24419-133">Después de que todos los hello detener las máquinas virtuales, crear Hola nueva máquina virtual en hello tamaño deseado.</span><span class="sxs-lookup"><span data-stu-id="24419-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="24419-134">Iniciar Hola nueva máquina virtual en primer lugar y, a continuación, seleccione cada uno de hello detiene las máquinas virtuales y haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="24419-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="24419-135">**Causa 2:** Hola clúster no tiene recursos libres.</span><span class="sxs-lookup"><span data-stu-id="24419-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="24419-136">**Resolución 2:**</span><span class="sxs-lookup"><span data-stu-id="24419-136">**Resolution 2:**</span></span>

* <span data-ttu-id="24419-137">Vuelva a intentar la solicitud de hello en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="24419-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="24419-138">Si puede hello nueva máquina virtual se establecer parte de una disponibilidad diferentes</span><span class="sxs-lookup"><span data-stu-id="24419-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="24419-139">Crear una nueva máquina virtual en un conjunto de disponibilidad diferentes (Hola misma región).</span><span class="sxs-lookup"><span data-stu-id="24419-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="24419-140">Agregar Hola nueva VM toohello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="24419-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24419-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24419-141">Next steps</span></span>
<span data-ttu-id="24419-142">Si tiene problemas al iniciar una máquina virtual Linux detenida o al cambiar el tamaño de una máquina virtual Linux existente en Azure, consulte [Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Linux existente en Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24419-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

