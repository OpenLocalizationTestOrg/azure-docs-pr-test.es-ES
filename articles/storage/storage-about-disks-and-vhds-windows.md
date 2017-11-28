---
title: "Acerca de los discos y los VHD para máquinas virtuales de Windows en Microsoft Azure | Microsoft Docs"
description: "Conozca los aspectos básicos de los discos y los VHD para las máquinas virtuales Windows en Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 34a4d8fa176484fbadb1b385d794cada5be607c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="180b3-103">Acerca de los discos y los discos duros virtuales para máquinas virtuales de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="180b3-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="180b3-104">Como cualquier otro equipo, las máquinas virtuales de Azure usan discos como un lugar para almacenar un sistema operativo, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="180b3-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="180b3-105">Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="180b3-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="180b3-106">El disco de sistema operativo se crea a partir de una imagen, y tanto el disco de sistema operativo como la imagen son discos duros virtuales (VHD) almacenados en una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="180b3-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="180b3-107">Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="180b3-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="180b3-108">En este artículo, se tratan los diferentes usos de los discos y después se describen los diferentes tipos de discos que puede crear y utilizar.</span><span class="sxs-lookup"><span data-stu-id="180b3-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="180b3-109">Este artículo también está disponible para [máquinas virtuales Linux](storage-about-disks-and-vhds-linux.md).</span><span class="sxs-lookup"><span data-stu-id="180b3-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="180b3-110">Discos usados por las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="180b3-110">Disks used by VMs</span></span>

<span data-ttu-id="180b3-111">Observemos cómo las máquinas virtuales utilizan los discos.</span><span class="sxs-lookup"><span data-stu-id="180b3-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="180b3-112">Disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="180b3-112">Operating system disk</span></span>
<span data-ttu-id="180b3-113">Cada máquina virtual tiene un disco de sistema operativo acoplado.</span><span class="sxs-lookup"><span data-stu-id="180b3-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="180b3-114">Está registrado como unidad SATA y etiquetado como la unidad C: de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="180b3-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="180b3-115">Este disco tiene una capacidad máxima de 2048 gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="180b3-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="180b3-116">Disco temporal</span><span class="sxs-lookup"><span data-stu-id="180b3-116">Temporary disk</span></span>
<span data-ttu-id="180b3-117">Cada máquina contiene un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="180b3-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="180b3-118">El disco temporal proporciona almacenamiento a corto plazo para aplicaciones y procesos, y está destinado únicamente a almacenar datos como archivos de paginación o de intercambio.</span><span class="sxs-lookup"><span data-stu-id="180b3-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="180b3-119">Los datos del disco temporal pueden perderse durante un [evento de mantenimiento](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o cuando [vuelva a implementar una máquina virtual](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="180b3-119">Data on the temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="180b3-120">Durante un reinicio estándar de la máquina virtual, los datos de la unidad temporal deben conservarse.</span><span class="sxs-lookup"><span data-stu-id="180b3-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="180b3-121">El disco temporal está etiquetado de forma predeterminada como unidad D: y se usa para almacenar el archivo pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="180b3-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="180b3-122">Para reasignar este disco a una letra de unidad diferente, consulte [Cambiar la letra de unidad de disco temporal de Windows](../virtual-machines/windows/change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="180b3-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="180b3-123">El tamaño del disco temporal varía, según el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="180b3-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="180b3-124">Para más información, consulte [Tamaños de las máquinas virtuales Windows](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="180b3-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="180b3-125">Para más información sobre cómo usa Azure el disco temporal, consulte [Understanding the temporary drive on Windows Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="180b3-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="180b3-126">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="180b3-126">Data disk</span></span>
<span data-ttu-id="180b3-127">Un disco de datos es un disco duro virtual (VHD) que se adjunta a una máquina virtual para almacenar datos de aplicaciones u otros datos que necesita mantener.</span><span class="sxs-lookup"><span data-stu-id="180b3-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="180b3-128">Los discos de datos se registran como unidades SCSI y se etiquetan con una letra elegida por usted.</span><span class="sxs-lookup"><span data-stu-id="180b3-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="180b3-129">Cada disco de datos tiene una capacidad máxima de 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="180b3-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="180b3-130">El tamaño de la máquina virtual determina cuántos discos de datos puede conectar y el tipo de almacenamiento que puede usar para hospedar los discos.</span><span class="sxs-lookup"><span data-stu-id="180b3-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="180b3-131">Para más información acerca de las capacidades de las máquinas virtuales, consulte [Tamaños de las máquinas virtuales Windows](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="180b3-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="180b3-132">Azure crea un disco del sistema operativo cuando se crea una máquina virtual desde una imagen.</span><span class="sxs-lookup"><span data-stu-id="180b3-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="180b3-133">Si usa una imagen que incluye discos de datos, Azure también crea los discos de datos al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="180b3-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="180b3-134">De lo contrario, agregue discos de datos después de crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="180b3-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="180b3-135">Puede agregar discos de datos a una máquina virtual en cualquier momento **conectando** el disco a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="180b3-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="180b3-136">Puede usar un VHD cargado o copiado por usted en la cuenta de almacenamiento o uno que Azure cree para usted.</span><span class="sxs-lookup"><span data-stu-id="180b3-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="180b3-137">Al adjuntar un disco de datos, el archivo del VHD se asocia a la máquina virtual y se coloca una "concesión" en dicho VHD para que no pueda eliminarse del almacenamiento mientras esté adjunto.</span><span class="sxs-lookup"><span data-stu-id="180b3-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="180b3-138">Una última recomendación: utilice TRIM con los discos estándar no administrados</span><span class="sxs-lookup"><span data-stu-id="180b3-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="180b3-139">Si utiliza discos estándar no administrados (HDD), debería habilitar TRIM.</span><span class="sxs-lookup"><span data-stu-id="180b3-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="180b3-140">TRIM descarta los bloques sin utilizar del disco, por lo que solo se le facturará el almacenamiento que utiliza realmente.</span><span class="sxs-lookup"><span data-stu-id="180b3-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="180b3-141">Esto puede suponerle un ahorro si crea archivos grandes y, luego, los elimina.</span><span class="sxs-lookup"><span data-stu-id="180b3-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="180b3-142">Puede ejecutar este comando para comprobar la configuración de TRIM.</span><span class="sxs-lookup"><span data-stu-id="180b3-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="180b3-143">Abra un símbolo del sistema en su máquina virtual de Windows y escriba:</span><span class="sxs-lookup"><span data-stu-id="180b3-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="180b3-144">Si el comando devuelve 0, significa que TRIM está habilitada correctamente.</span><span class="sxs-lookup"><span data-stu-id="180b3-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="180b3-145">Si devuelve 1, ejecute el siguiente comando para habilitar TRIM:</span><span class="sxs-lookup"><span data-stu-id="180b3-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="180b3-146">Nota: La compatibilidad con Trim comienza con Windows Server 2012 / Windows 8 y versiones posteriores. Vea [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints) (La nueva API que permite a las aplicaciones enviar sugerencias "TRIM y Unmap" a los medios de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="180b3-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="180b3-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="180b3-147">Next steps</span></span>
* <span data-ttu-id="180b3-148">[Conecte un disco](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para agregar almacenamiento adicional para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="180b3-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="180b3-149">[Cambiar la letra de unidad de disco temporal de Windows](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) con el fin de que la aplicación pueda usar la unidad D: para los datos.</span><span class="sxs-lookup"><span data-stu-id="180b3-149">[Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

