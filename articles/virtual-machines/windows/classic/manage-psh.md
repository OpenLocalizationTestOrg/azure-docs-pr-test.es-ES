---
title: "aaaManage las máquinas virtuales mediante el uso de PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los comandos que puede usar tareas de tooautomate en la administración de las máquinas virtuales."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="58fa2-103">Administración de las máquinas virtuales con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58fa2-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="58fa2-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="58fa2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="58fa2-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="58fa2-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="58fa2-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="58fa2-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="58fa2-107">Para los comandos de PowerShell utilizando el modelo de administrador de recursos de hello comunes, consulte [aquí](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58fa2-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="58fa2-108">Muchas tareas que hacer cada día toomanage las máquinas virtuales pueden automatizarse mediante el uso de cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="58fa2-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="58fa2-109">Este artículo proporciona comandos de ejemplo para las tareas más sencillas y tooarticles de vínculos que mostrar los comandos de Hola para tareas más complejas.</span><span class="sxs-lookup"><span data-stu-id="58fa2-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="58fa2-110">Si no ha instalado y configurado Azure PowerShell aún, si desea obtener instrucciones en el artículo hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58fa2-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="58fa2-111">¿Cómo toouse Hola comandos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="58fa2-111">How toouse hello example commands</span></span>
<span data-ttu-id="58fa2-112">Necesitará tooreplace parte del texto de Hola Hola comandos con texto que sea adecuada para su entorno.</span><span class="sxs-lookup"><span data-stu-id="58fa2-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="58fa2-113">Hola < y > símbolos indican texto necesita tooreplace.</span><span class="sxs-lookup"><span data-stu-id="58fa2-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="58fa2-114">Al reemplazar texto hello, quitar símbolos de hello pero deje las comillas de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="58fa2-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="58fa2-115">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="58fa2-115">Get a VM</span></span>
<span data-ttu-id="58fa2-116">Es una tarea básica que utilizará a menudo.</span><span class="sxs-lookup"><span data-stu-id="58fa2-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="58fa2-117">Usar tooget información acerca de una máquina virtual, realizar tareas en una máquina virtual u obtener toostore de salida en una variable.</span><span class="sxs-lookup"><span data-stu-id="58fa2-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="58fa2-118">tooget información acerca de Hola de máquina virtual, ejecute este comando, reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >:</span><span class="sxs-lookup"><span data-stu-id="58fa2-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="58fa2-119">Hola toostore de salida en una variable $vm, ejecute:</span><span class="sxs-lookup"><span data-stu-id="58fa2-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="58fa2-120">Inicie sesión en tooa VM basadas en Windows</span><span class="sxs-lookup"><span data-stu-id="58fa2-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="58fa2-121">Ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="58fa2-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="58fa2-122">Puede obtener la máquina virtual de Hola y el nombre del servicio de nube de pantalla de Hola de hello **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="58fa2-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="58fa2-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unidad y la carpeta ubicación toostore Hola Descargar archivo RDP, ejemplo: c:\temp >" $localFile = $localPath + "\" + $vmname +".rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-nombre $vmName - LocalPath $localFile-iniciar</span><span class="sxs-lookup"><span data-stu-id="58fa2-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="58fa2-124">Detención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="58fa2-124">Stop a VM</span></span>
<span data-ttu-id="58fa2-125">Ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="58fa2-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="58fa2-126">Usar este hello tookeep de parámetro en caso de que sea de servicio de IP virtual (VIP) de la nube de Hola Hola última VM en ese servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="58fa2-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="58fa2-127">Si usas hello StayProvisioned parámetro, se le facturará por hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="58fa2-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="58fa2-128">Inicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="58fa2-128">Start a VM</span></span>
<span data-ttu-id="58fa2-129">Ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="58fa2-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="58fa2-130">Acoplamiento de un disco de datos</span><span class="sxs-lookup"><span data-stu-id="58fa2-130">Attach a data disk</span></span>
<span data-ttu-id="58fa2-131">Esta tarea requiere unos pocos pasos.</span><span class="sxs-lookup"><span data-stu-id="58fa2-131">This task requires a few steps.</span></span> <span data-ttu-id="58fa2-132">En primer lugar, use Hola *** Add-AzureDataDisk *** cmdlet tooadd hello toohello $vm objeto de disco.</span><span class="sxs-lookup"><span data-stu-id="58fa2-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="58fa2-133">A continuación, utilice **Update-AzureVM** configuración de cmdlet tooupdate Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="58fa2-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="58fa2-134">También necesitará toodecide si tooattach un disco nuevo o uno que contiene datos.</span><span class="sxs-lookup"><span data-stu-id="58fa2-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="58fa2-135">Para un disco nuevo, el comando hello crea el archivo .vhd de hello y lo adjunta.</span><span class="sxs-lookup"><span data-stu-id="58fa2-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="58fa2-136">tooattach un disco nuevo, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="58fa2-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="58fa2-137">tooattach un disco de datos existente, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="58fa2-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="58fa2-138">tooattach los discos de datos de un archivo .vhd existente en el almacenamiento de blobs, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="58fa2-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="58fa2-139">Creación de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="58fa2-139">Create a Windows-based VM</span></span>
<span data-ttu-id="58fa2-140">una nueva máquina virtual basada en Windows en Azure, use las instrucciones de hello en toocreate [toocreate de usar PowerShell de Azure y preconfigurar máquinas virtuales basadas en Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="58fa2-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="58fa2-141">Pasos de este tema le guían a través de la creación de hello de un conjunto de comandos que de Azure PowerShell crea una máquina virtual basada en Windows que puede configurar previamente:</span><span class="sxs-lookup"><span data-stu-id="58fa2-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="58fa2-142">Con pertenencia al dominio de Active Directory;</span><span class="sxs-lookup"><span data-stu-id="58fa2-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="58fa2-143">Con discos adicionales;</span><span class="sxs-lookup"><span data-stu-id="58fa2-143">With additional disks.</span></span>
* <span data-ttu-id="58fa2-144">Como miembro de un conjunto de carga equilibrada;</span><span class="sxs-lookup"><span data-stu-id="58fa2-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="58fa2-145">Con una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="58fa2-145">With a static IP address.</span></span>

