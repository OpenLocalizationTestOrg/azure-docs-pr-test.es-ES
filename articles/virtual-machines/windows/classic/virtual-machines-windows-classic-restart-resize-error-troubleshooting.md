---
title: "aaaVM reiniciar o cambiar el tamaño de problemas | Documentos de Microsoft"
description: "Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="15b7c-103">Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure</span><span class="sxs-lookup"><span data-stu-id="15b7c-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15b7c-104">Clásico</span><span class="sxs-lookup"><span data-stu-id="15b7c-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="15b7c-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="15b7c-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="15b7c-106">Cuando intente toostart una máquina Virtual de Azure (VM) detenida, o cambiar el tamaño de una máquina virtual de Azure existente, se produce de error común de hello es un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="15b7c-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="15b7c-107">Este error se produce cuando el clúster de Hola o región no tenga recursos disponibles o no se solicitó que Hola de soporte técnico de tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="15b7c-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15b7c-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="15b7c-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="15b7c-109">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="15b7c-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="15b7c-111">Recopilación de registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="15b7c-111">Collect audit logs</span></span>
<span data-ttu-id="15b7c-112">toostart solución de problemas, auditoría de hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="15b7c-113">Hola portal de Azure, haga clic en **examinar** > **máquinas virtuales** > *la máquina virtual de Windows*  >   **Configuración de** > **registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="15b7c-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="15b7c-114">Problema: Error al iniciar una máquina virtual detenida</span><span class="sxs-lookup"><span data-stu-id="15b7c-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="15b7c-115">Intente toostart una VM detenida pero obtendrá un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="15b7c-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="15b7c-116">Causa</span><span class="sxs-lookup"><span data-stu-id="15b7c-116">Cause</span></span>
<span data-ttu-id="15b7c-117">solicitud de Hola Hola toostart detiene la máquina virtual tiene toobe vuelve a intentar cada clúster original Hola que aloja el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="15b7c-118">Sin embargo, el clúster de hello no tiene solicitud de espacio libre disponible toofulfill Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="15b7c-119">Resolución</span><span class="sxs-lookup"><span data-stu-id="15b7c-119">Resolution</span></span>
* <span data-ttu-id="15b7c-120">Cree un nuevo servicio en la nube y asócielo con una región o con una red virtual basada en regiones, pero con no un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="15b7c-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="15b7c-121">Eliminar Hola detiene la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="15b7c-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="15b7c-122">Vuelva a crear Hola VM Hola nuevo servicio en nube mediante el uso de discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="15b7c-123">Iniciar Hola vuelve a crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="15b7c-123">Start hello re-created VM.</span></span>

<span data-ttu-id="15b7c-124">Si se produce un error al tratar de toocreate un nuevo servicio de nube, ya sea a intentarlo más tarde o cambiar región Hola Hola servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="15b7c-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15b7c-125">servicio de nube nuevo Hola tendrá un nuevo nombre y la dirección VIP, por lo que deberá toochange esa información para todas las dependencias de Hola que usan esa información de servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="15b7c-126">Problema: error al reiniciar una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="15b7c-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="15b7c-127">Intente tooresize una máquina virtual existente pero obtendrá un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="15b7c-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="15b7c-128">Causa</span><span class="sxs-lookup"><span data-stu-id="15b7c-128">Cause</span></span>
<span data-ttu-id="15b7c-129">solicitud de Hola Hola tooresize VM tiene toobe intentaba ejecutar en clúster original Hola ese servicio de nube de Hola de hosts.</span><span class="sxs-lookup"><span data-stu-id="15b7c-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="15b7c-130">Sin embargo, no es compatible con clúster de Hola Hola solicitado tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="15b7c-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="15b7c-131">Resolución</span><span class="sxs-lookup"><span data-stu-id="15b7c-131">Resolution</span></span>
<span data-ttu-id="15b7c-132">Reducir tamaño de máquina virtual solicita el Hola y Hola vuelva a intentar cambiar el tamaño de solicitud.</span><span class="sxs-lookup"><span data-stu-id="15b7c-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="15b7c-133">Haga clic en **Examinar todo** > **Máquinas virtuales (clásico)** > *su máquina virtual* > **Configuración** > **Tamaño**.</span><span class="sxs-lookup"><span data-stu-id="15b7c-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="15b7c-134">Para obtener instrucciones detalladas, consulte [cambiar el tamaño de máquina virtual de hello](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="15b7c-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="15b7c-135">Si no es posible tooreduce Hola tamaño de máquina virtual, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="15b7c-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="15b7c-136">Crear un nuevo servicio de nube, asegurando que se no trata vinculado tooan grupo de afinidad y no asociada a una red virtual que está vinculado tooan grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="15b7c-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="15b7c-137">Cree una máquina virtual nueva y de mayor tamaño en dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="15b7c-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="15b7c-138">Es posible consolidar todas las máquinas virtuales en hello mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="15b7c-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="15b7c-139">Si su servicio en la nube está asociado a una red virtual basada en la región, puede conectarse Hola nueva nube servicio toohello red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="15b7c-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="15b7c-140">Si Hola existente en la nube servicio no está asociado a ninguna red virtual basadas en regiones, a continuación, tiene toodelete hello las máquinas virtuales en el servicio de nube existente de hello y volver a crearlos en hello nuevo servicio en la nube desde sus discos.</span><span class="sxs-lookup"><span data-stu-id="15b7c-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="15b7c-141">Sin embargo, es importante tooremember que el servicio de nube nuevo de Hola tendrá un nuevo nombre y la dirección VIP, por lo que deberá tooupdate para todas las dependencias de Hola que actualmente utilizan esta información para servicio de nube existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="15b7c-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15b7c-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15b7c-142">Next steps</span></span>
<span data-ttu-id="15b7c-143">Si se producen problemas al crear una máquina virtual con Windows en Azure, vea [Solución de problemas de implementación con la creación de una máquina virtual con Windows en Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15b7c-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

