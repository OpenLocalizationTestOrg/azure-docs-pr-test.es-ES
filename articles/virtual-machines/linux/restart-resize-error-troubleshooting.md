---
title: "Problemas de reinicio o cambio de tamaño de las máquinas virtuales de Azure | Microsoft Docs"
description: "Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Linux existente en Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="d279e-103">Solución de problemas de implementación con el reinicio o el cambio de tamaño de una máquina virtual Linux existente en Azure</span><span class="sxs-lookup"><span data-stu-id="d279e-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="d279e-104">Al intentar iniciar una máquina virtual de Azure detenida o cambiar el tamaño de una máquina virtual de Azure existente, es común encontrarse un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="d279e-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="d279e-105">Dicho error se produce cuando el clúster o la región no tienen recursos disponibles o no admiten el tamaño de máquina virtual solicitado.</span><span class="sxs-lookup"><span data-stu-id="d279e-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="d279e-106">Recopilación de registros de actividad</span><span class="sxs-lookup"><span data-stu-id="d279e-106">Collect activity logs</span></span>
<span data-ttu-id="d279e-107">Para iniciar la solución de problemas, recopile los registros de actividad para identificar el error asociado con el problema.</span><span class="sxs-lookup"><span data-stu-id="d279e-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="d279e-108">Los vínculos siguientes contienen información detallada sobre el proceso:</span><span class="sxs-lookup"><span data-stu-id="d279e-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="d279e-109">Ver operaciones de implementación</span><span class="sxs-lookup"><span data-stu-id="d279e-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="d279e-110">Ver registros de actividad para administrar recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="d279e-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="d279e-111">Problema: Error al iniciar una máquina virtual detenida</span><span class="sxs-lookup"><span data-stu-id="d279e-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="d279e-112">Intenta iniciar una máquina virtual detenida, pero obtiene un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="d279e-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="d279e-113">Causa</span><span class="sxs-lookup"><span data-stu-id="d279e-113">Cause</span></span>
<span data-ttu-id="d279e-114">La solicitud de iniciar la máquina virtual detenida se debe intentar en el clúster original que hospeda el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="d279e-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="d279e-115">Sin embargo, el clúster no tiene espacio libre disponible para responder a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="d279e-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="d279e-116">Resolución</span><span class="sxs-lookup"><span data-stu-id="d279e-116">Resolution</span></span>
* <span data-ttu-id="d279e-117">Detenga todas las máquinas virtuales del conjunto de disponibilidad y reinicie las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d279e-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="d279e-118">Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="d279e-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="d279e-119">Después de detener todas las máquinas virtuales, selecciónelas y haga clic en Iniciar.</span><span class="sxs-lookup"><span data-stu-id="d279e-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="d279e-120">Vuelva a intentar solicitar el reinicio más tarde.</span><span class="sxs-lookup"><span data-stu-id="d279e-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="d279e-121">Problema: error al reiniciar una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="d279e-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="d279e-122">Intenta cambiar el tamaño de una máquina virtual existente, pero obtiene un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="d279e-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="d279e-123">Causa</span><span class="sxs-lookup"><span data-stu-id="d279e-123">Cause</span></span>
<span data-ttu-id="d279e-124">La solicitud de cambiar el tamaño de la máquina virtual se debe realizar en el clúster original que alberga el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="d279e-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="d279e-125">Sin embargo, el clúster no admite el tamaño de máquina virtual solicitado.</span><span class="sxs-lookup"><span data-stu-id="d279e-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="d279e-126">Resolución</span><span class="sxs-lookup"><span data-stu-id="d279e-126">Resolution</span></span>
* <span data-ttu-id="d279e-127">Vuelva a intentar la solicitud con un tamaño de máquina virtual menor.</span><span class="sxs-lookup"><span data-stu-id="d279e-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="d279e-128">Si no se puede cambiar el tamaño de la máquina virtual solicitada:</span><span class="sxs-lookup"><span data-stu-id="d279e-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="d279e-129">Detenga todas las máquinas virtuales en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="d279e-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="d279e-130">Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="d279e-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="d279e-131">Después de detener todas las máquinas virtuales, aumente el tamaño de la máquina virtual que quiera.</span><span class="sxs-lookup"><span data-stu-id="d279e-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="d279e-132">Seleccione la máquina virtual cuyo tamaño ha cambiado, haga clic en **Iniciar**e inicie las máquinas virtuales detenidas.</span><span class="sxs-lookup"><span data-stu-id="d279e-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d279e-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d279e-133">Next steps</span></span>
<span data-ttu-id="d279e-134">Si surgen problemas al crear una nueva máquina virtual Linux en Azure, consulte [Solución de problemas de la implementación de Resource Manager con la creación de una nueva máquina virtual de Linux en Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d279e-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

