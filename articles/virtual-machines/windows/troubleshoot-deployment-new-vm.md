---
title: "Solución de problemas de implementación de máquinas virtuales Windows en Azure | Microsoft Docs"
description: "Solución de problemas de implementación de Resource Manager cuando crea una nueva máquina virtual de Windows en Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 86795ba6eab3505a3d539e4fc4e032bdeecc2e78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="63372-103">Solución de problemas de implementación al crear una nueva máquina virtual Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="63372-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="63372-104">Principales problemas</span><span class="sxs-lookup"><span data-stu-id="63372-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="63372-105">Para consultar otros problemas de implementación de máquinas virtuales y preguntas, vea [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Solución de problemas de implementación de máquinas virtuales de Windows en Azure).</span><span class="sxs-lookup"><span data-stu-id="63372-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="63372-106">Recopilación de registros de actividad</span><span class="sxs-lookup"><span data-stu-id="63372-106">Collect activity logs</span></span>
<span data-ttu-id="63372-107">Para iniciar la solución de problemas, recopile los registros de actividad para identificar el error asociado con el problema.</span><span class="sxs-lookup"><span data-stu-id="63372-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="63372-108">Los vínculos siguientes contienen información detallada sobre el proceso que se debe seguir.</span><span class="sxs-lookup"><span data-stu-id="63372-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="63372-109">Ver operaciones de implementación</span><span class="sxs-lookup"><span data-stu-id="63372-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="63372-110">Ver registros de actividad para administrar recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="63372-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="63372-111">**Y:** si el sistema operativo es Windows generalizado y se carga o captura con la configuración generalizada, no habrá errores.</span><span class="sxs-lookup"><span data-stu-id="63372-111">**Y:** If the OS is Windows generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="63372-112">De forma similar, si el sistema operativo es Windows especializado y se carga o captura con la configuración especializada, no habrá errores.</span><span class="sxs-lookup"><span data-stu-id="63372-112">Similarly, if the OS is Windows specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="63372-113">**Errores de carga:**</span><span class="sxs-lookup"><span data-stu-id="63372-113">**Upload Errors:**</span></span>

<span data-ttu-id="63372-114">**N<sup>1</sup>:** si el sistema operativo es Windows generalizado y se carga como especializado, aparecerá un error de tiempo de espera de aprovisionamiento con la máquina virtual bloqueada en la pantalla de OOBE.</span><span class="sxs-lookup"><span data-stu-id="63372-114">**N<sup>1</sup>:** If the OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with the VM stuck at the OOBE screen.</span></span>

<span data-ttu-id="63372-115">**N<sup>2</sup>:** si el sistema operativo es Windows especializado y se carga como generalizado, recibirá un error de aprovisionamiento con la máquina virtual bloqueada en la pantalla de OOBE porque la nueva máquina virtual se ejecuta con el nombre del equipo, el nombre de usuario y la contraseña originales.</span><span class="sxs-lookup"><span data-stu-id="63372-115">**N<sup>2</sup>:** If the OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with the VM stuck at the OOBE screen because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="63372-116">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="63372-116">**Resolution**</span></span>

<span data-ttu-id="63372-117">Para resolver estos errores, use [Add-AzureRmVhd para cargar el disco duro virtual original](https://msdn.microsoft.com/library/mt603554.aspx), disponible en el entorno local, con la misma configuración que para el sistema operativo (generalizada o especializada).</span><span class="sxs-lookup"><span data-stu-id="63372-117">To resolve both these errors, use [Add-AzureRmVhd to upload the original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="63372-118">Para cargar como generalizado, no olvide ejecutar sysprep antes.</span><span class="sxs-lookup"><span data-stu-id="63372-118">To upload as generalized, remember to run sysprep first.</span></span>

<span data-ttu-id="63372-119">**Errores de captura:**</span><span class="sxs-lookup"><span data-stu-id="63372-119">**Capture Errors:**</span></span>

<span data-ttu-id="63372-120">**N<sup>3</sup>:** si el sistema operativo es Windows generalizado y se captura como especializado, recibirá un error de tiempo de espera de aprovisionamiento porque la máquina virtual original no se puede utilizar, ya que está marcada como generalizada.</span><span class="sxs-lookup"><span data-stu-id="63372-120">**N<sup>3</sup>:** If the OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="63372-121">**N<sup>4</sup>:** si el sistema operativo es Windows especializado y se captura como generalizado, recibirá un error de aprovisionamiento porque la nueva máquina virtual se está ejecutando con el nombre del equipo, el nombre de usuario y la contraseña originales.</span><span class="sxs-lookup"><span data-stu-id="63372-121">**N<sup>4</sup>:** If the OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username, and password.</span></span> <span data-ttu-id="63372-122">Además, no se puede utilizar la máquina virtual original ya que está marcada como especializada.</span><span class="sxs-lookup"><span data-stu-id="63372-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="63372-123">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="63372-123">**Resolution**</span></span>

<span data-ttu-id="63372-124">Para resolver estos errores, elimine la imagen actual del portal y [vuelva a capturarla desde los discos duros virtuales actuales](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con la misma configuración que para el sistema operativo (generalizada o especializada).</span><span class="sxs-lookup"><span data-stu-id="63372-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="63372-125">Problema: Imagen de galería/marketplace/personalizada; error de asignación</span><span class="sxs-lookup"><span data-stu-id="63372-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="63372-126">Este error se produce en situaciones en las que la nueva solicitud de máquina virtual está anclada en un clúster que no admite el tamaño de la máquina virtual que se solicita o no tiene espacio libre disponible para alojar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="63372-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="63372-127">**Causa 1:** el clúster no admite el tamaño de la máquina virtual solicitada.</span><span class="sxs-lookup"><span data-stu-id="63372-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="63372-128">**Resolución 1:**</span><span class="sxs-lookup"><span data-stu-id="63372-128">**Resolution 1:**</span></span>

* <span data-ttu-id="63372-129">Vuelva a intentar la solicitud con un tamaño de máquina virtual menor.</span><span class="sxs-lookup"><span data-stu-id="63372-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="63372-130">Si no se puede cambiar el tamaño de la máquina virtual solicitada:</span><span class="sxs-lookup"><span data-stu-id="63372-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="63372-131">Detenga todas las máquinas virtuales en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="63372-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="63372-132">Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="63372-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="63372-133">Después de detener todas las máquinas virtuales, cree la nueva máquina virtual con el tamaño deseado.</span><span class="sxs-lookup"><span data-stu-id="63372-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="63372-134">Inicie la nueva máquina virtual en primer lugar y luego seleccione cada una de las máquinas virtuales detenidas y haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="63372-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="63372-135">**Causa 2:** el clúster no tiene recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="63372-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="63372-136">**Resolución 2:**</span><span class="sxs-lookup"><span data-stu-id="63372-136">**Resolution 2:**</span></span>

* <span data-ttu-id="63372-137">Vuelva a intentar la solicitud más tarde.</span><span class="sxs-lookup"><span data-stu-id="63372-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="63372-138">Si la nueva máquina virtual puede formar parte de un conjunto de disponibilidad diferente</span><span class="sxs-lookup"><span data-stu-id="63372-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="63372-139">Cree una nueva máquina virtual en un conjunto de disponibilidad diferente (en la misma región).</span><span class="sxs-lookup"><span data-stu-id="63372-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="63372-140">Agregue la nueva máquina virtual a la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="63372-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63372-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63372-141">Next steps</span></span>
<span data-ttu-id="63372-142">Si tiene problemas al iniciar una máquina virtual Windows detenida o al cambiar el tamaño de una máquina virtual Windows existente en Azure, consulte [Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63372-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

