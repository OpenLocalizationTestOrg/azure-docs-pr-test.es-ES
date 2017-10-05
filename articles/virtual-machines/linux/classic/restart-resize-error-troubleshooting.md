---
title: "Problemas de reinicio o cambio de tamaño de las máquinas virtuales | Microsoft Docs"
description: "Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual con Linux existente en Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="b80d3-103">Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual con Linux existente en Azure</span><span class="sxs-lookup"><span data-stu-id="b80d3-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b80d3-104">Clásico</span><span class="sxs-lookup"><span data-stu-id="b80d3-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="b80d3-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b80d3-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="b80d3-106">Al intentar iniciar una máquina virtual de Azure detenida o cambiar el tamaño de una máquina virtual de Azure existente, es común encontrarse un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="b80d3-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="b80d3-107">Dicho error se produce cuando el clúster o la región no tienen recursos disponibles o no admiten el tamaño de máquina virtual solicitado.</span><span class="sxs-lookup"><span data-stu-id="b80d3-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b80d3-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b80d3-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b80d3-109">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="b80d3-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b80d3-110">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b80d3-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b80d3-111">Para la versión de Resource Manager, consulte [aquí](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b80d3-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="b80d3-112">Recopilación de registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="b80d3-112">Collect audit logs</span></span>
<span data-ttu-id="b80d3-113">Para iniciar la solución de problemas, recopile los registros de auditoría para identificar el error asociado con el problema.</span><span class="sxs-lookup"><span data-stu-id="b80d3-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="b80d3-114">En Azure Portal, haga clic en **Examinar** > **Máquinas virtuales** > *su máquina virtual de Linux* > **Configuración** > **Registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="b80d3-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="b80d3-115">Problema: Error al iniciar una máquina virtual detenida</span><span class="sxs-lookup"><span data-stu-id="b80d3-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="b80d3-116">Intenta iniciar una máquina virtual detenida, pero obtiene un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="b80d3-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="b80d3-117">Causa</span><span class="sxs-lookup"><span data-stu-id="b80d3-117">Cause</span></span>
<span data-ttu-id="b80d3-118">La solicitud de iniciar la máquina virtual detenida se debe intentar en el clúster original que hospeda el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="b80d3-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="b80d3-119">Sin embargo, el clúster no tiene espacio libre disponible para responder a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b80d3-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="b80d3-120">Resolución</span><span class="sxs-lookup"><span data-stu-id="b80d3-120">Resolution</span></span>
* <span data-ttu-id="b80d3-121">Cree un nuevo servicio en la nube y asócielo con una región o con una red virtual basada en regiones, pero con no un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="b80d3-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="b80d3-122">Elimine la máquina virtual detenida.</span><span class="sxs-lookup"><span data-stu-id="b80d3-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="b80d3-123">Vuelva a crear la máquina virtual en el nuevo servicio en la nube mediante los discos.</span><span class="sxs-lookup"><span data-stu-id="b80d3-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="b80d3-124">Inicie la máquina virtual recién creada.</span><span class="sxs-lookup"><span data-stu-id="b80d3-124">Start the re-created VM.</span></span>

<span data-ttu-id="b80d3-125">Si se produce un error al intentar crear un nuevo servicio en la nube, vuelva a intentarlo más tarde o cambie la región de dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="b80d3-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b80d3-126">El nuevo servicio en la nube tendrá un nuevo nombre y dirección VIP, por lo que deberá cambiar dicha información en todas las dependencias que utilicen dicha información para el servicio en la nube existente.</span><span class="sxs-lookup"><span data-stu-id="b80d3-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="b80d3-127">Problema: error al reiniciar una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="b80d3-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="b80d3-128">Intenta cambiar el tamaño de una máquina virtual existente, pero obtiene un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="b80d3-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="b80d3-129">Causa</span><span class="sxs-lookup"><span data-stu-id="b80d3-129">Cause</span></span>
<span data-ttu-id="b80d3-130">La solicitud de cambiar el tamaño de la máquina virtual se debe realizar en el clúster original que alberga el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="b80d3-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="b80d3-131">Sin embargo, el clúster no admite el tamaño de máquina virtual solicitado.</span><span class="sxs-lookup"><span data-stu-id="b80d3-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="b80d3-132">Resolución</span><span class="sxs-lookup"><span data-stu-id="b80d3-132">Resolution</span></span>
<span data-ttu-id="b80d3-133">Reduzca el tamaño de máquina virtual solicitado y vuelva a intentar la solicitud de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="b80d3-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="b80d3-134">Haga clic en **Examinar todo** > **Máquinas virtuales (clásico)** > *su máquina virtual* > **Configuración** > **Tamaño**.</span><span class="sxs-lookup"><span data-stu-id="b80d3-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="b80d3-135">Para información detallada, vea [Cambiar el tamaño de la máquina virtual](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="b80d3-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="b80d3-136">Si no es posible reducir el tamaño de la máquina virtual, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b80d3-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="b80d3-137">Cree un nuevo servicio en la nube, pero asegúrese de que no está vinculado a ningún grupo de afinidad ni asociado a ninguna red virtual vinculada a un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="b80d3-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="b80d3-138">Cree una máquina virtual nueva y de mayor tamaño en dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="b80d3-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="b80d3-139">Puede consolidar todas las máquinas virtuales en el mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="b80d3-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="b80d3-140">Si el servicio en la nube existente está asociado a una red virtual basada en regiones, puede conectar el nuevo servicio en la nube a la red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="b80d3-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="b80d3-141">Si el servicio en la nube existente no está asociado a una red virtual basada en regiones, tendrá que eliminar sus máquinas virtuales y volver a crearlas en el nuevo servicio en la nube desde los discos.</span><span class="sxs-lookup"><span data-stu-id="b80d3-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="b80d3-142">No obstante, es importante recordar que el nuevo servicio en la nube tendrá un nuevo nombre y dirección VIP, por lo que deberá actualizar esta información en todas las dependencias que utilicen esta información para el servicio en la nube existente.</span><span class="sxs-lookup"><span data-stu-id="b80d3-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b80d3-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b80d3-143">Next steps</span></span>
<span data-ttu-id="b80d3-144">Si surgen problemas al crear una nueva máquina virtual Linux en Azure, consulte [Solución de problemas de la implementación de Resource Manager con la creación de una nueva máquina virtual de Linux en Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b80d3-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

