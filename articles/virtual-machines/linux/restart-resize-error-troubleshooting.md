---
title: "problemas de aaaVM reiniciar o cambiar el tamaño en Azure | Documentos de Microsoft"
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
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="20a1e-103">Solución de problemas de implementación con el reinicio o el cambio de tamaño de una máquina virtual Linux existente en Azure</span><span class="sxs-lookup"><span data-stu-id="20a1e-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="20a1e-104">Cuando intente toostart una máquina Virtual de Azure (VM) detenida, o cambiar el tamaño de una máquina virtual de Azure existente, se produce de error común de hello es un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="20a1e-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="20a1e-105">Este error se produce cuando el clúster de Hola o región no tenga recursos disponibles o no se solicitó que Hola de soporte técnico de tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="20a1e-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="20a1e-106">Recopilación de registros de actividad</span><span class="sxs-lookup"><span data-stu-id="20a1e-106">Collect activity logs</span></span>
<span data-ttu-id="20a1e-107">toostart solución de problemas, actividad hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="20a1e-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="20a1e-108">Hola siguientes vínculos contiene información detallada sobre el proceso de hello:</span><span class="sxs-lookup"><span data-stu-id="20a1e-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="20a1e-109">Ver operaciones de implementación</span><span class="sxs-lookup"><span data-stu-id="20a1e-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="20a1e-110">Ver registros de actividad toomanage Azure recursos</span><span class="sxs-lookup"><span data-stu-id="20a1e-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="20a1e-111">Problema: Error al iniciar una máquina virtual detenida</span><span class="sxs-lookup"><span data-stu-id="20a1e-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="20a1e-112">Intente toostart una VM detenida pero obtendrá un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="20a1e-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="20a1e-113">Causa</span><span class="sxs-lookup"><span data-stu-id="20a1e-113">Cause</span></span>
<span data-ttu-id="20a1e-114">solicitud de Hola Hola toostart detiene la máquina virtual tiene toobe vuelve a intentar cada clúster original Hola que aloja el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="20a1e-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="20a1e-115">Sin embargo, el clúster de hello no tiene solicitud de espacio libre disponible toofulfill Hola.</span><span class="sxs-lookup"><span data-stu-id="20a1e-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="20a1e-116">Resolución</span><span class="sxs-lookup"><span data-stu-id="20a1e-116">Resolution</span></span>
* <span data-ttu-id="20a1e-117">Detener Hola todas las máquinas virtuales en la disponibilidad de Hola establecerán y, a continuación, reinicie cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="20a1e-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="20a1e-118">Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="20a1e-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="20a1e-119">Después de que todos Hola detener las máquinas virtuales, seleccione cada una de las máquinas virtuales de hello detenido y haga clic en Inicio.</span><span class="sxs-lookup"><span data-stu-id="20a1e-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="20a1e-120">Vuelva a intentar la solicitud de reinicio de hello en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="20a1e-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="20a1e-121">Problema: error al reiniciar una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="20a1e-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="20a1e-122">Intente tooresize una máquina virtual existente pero obtendrá un error de asignación.</span><span class="sxs-lookup"><span data-stu-id="20a1e-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="20a1e-123">Causa</span><span class="sxs-lookup"><span data-stu-id="20a1e-123">Cause</span></span>
<span data-ttu-id="20a1e-124">solicitud de Hola Hola tooresize VM tiene toobe intentaba ejecutar en clúster original Hola ese servicio de nube de Hola de hosts.</span><span class="sxs-lookup"><span data-stu-id="20a1e-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="20a1e-125">Sin embargo, no es compatible con clúster de Hola Hola solicitado tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="20a1e-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="20a1e-126">Resolución</span><span class="sxs-lookup"><span data-stu-id="20a1e-126">Resolution</span></span>
* <span data-ttu-id="20a1e-127">Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="20a1e-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="20a1e-128">Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="20a1e-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="20a1e-129">Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="20a1e-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="20a1e-130">Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="20a1e-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="20a1e-131">Después de que todos Hola detener las máquinas virtuales, cambie el tamaño deseado de hello VM tooa mayor tamaño.</span><span class="sxs-lookup"><span data-stu-id="20a1e-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="20a1e-132">Cambiar el tamaño Hola seleccione máquina virtual y haga clic en **iniciar**, y, a continuación, inicie cada Hola detiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="20a1e-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20a1e-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20a1e-133">Next steps</span></span>
<span data-ttu-id="20a1e-134">Si surgen problemas al crear una nueva máquina virtual Linux en Azure, consulte [Solución de problemas de la implementación de Resource Manager con la creación de una nueva máquina virtual de Linux en Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20a1e-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

