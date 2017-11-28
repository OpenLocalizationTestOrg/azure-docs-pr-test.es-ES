---
title: "Administración de discos de Azure con Azure PowerShell | Microsoft Docs"
description: "Tutorial: Administración de discos de Azure con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="ea085-103">Administración de discos de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea085-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="ea085-104">Las máquinas virtuales de Azure usan discos para almacenar el sistema operativo, las aplicaciones y los datos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ea085-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="ea085-105">Al crear una máquina virtual es importante elegir un tamaño de disco y la configuración adecuada para la carga de trabajo esperada.</span><span class="sxs-lookup"><span data-stu-id="ea085-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="ea085-106">Este tutorial trata la implementación y administración de discos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="ea085-107">Aprenderá sobre los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="ea085-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea085-108">Discos del SO y temporales</span><span class="sxs-lookup"><span data-stu-id="ea085-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="ea085-109">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="ea085-109">Data disks</span></span>
> * <span data-ttu-id="ea085-110">Discos Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="ea085-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="ea085-111">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="ea085-111">Disk performance</span></span>
> * <span data-ttu-id="ea085-112">Conectar y preparar los discos de datos</span><span class="sxs-lookup"><span data-stu-id="ea085-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="ea085-113">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="ea085-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ea085-114">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="ea085-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="ea085-115">Si necesita actualizarla, vea [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ea085-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="ea085-116">Discos de Azure predeterminados</span><span class="sxs-lookup"><span data-stu-id="ea085-116">Default Azure disks</span></span>

<span data-ttu-id="ea085-117">Cuando se crea una máquina virtual de Azure, se conectan dos discos automáticamente a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="ea085-118">**Disco del sistema operativo**: hospedan el sistema operativo de las máquinas virtuales. Se puede cambiar su tamaño hasta 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="ea085-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="ea085-119">Al disco del sistema operativo se le asigna una letra de unidad *c:* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ea085-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="ea085-120">La configuración de almacenamiento en caché del disco del sistema operativo está optimizada para el rendimiento del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ea085-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="ea085-121">El disco del sistema operativo **no debería** hospedar aplicaciones o datos.</span><span class="sxs-lookup"><span data-stu-id="ea085-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="ea085-122">Para aplicaciones y datos, use un disco de datos. Explicamos esto más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ea085-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="ea085-123">**Disco temporal**: los discos temporales utilizan una unidad de estado sólida que se encuentra en el mismo host de Azure que la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="ea085-124">Los discos temporales son muy eficiente y se pueden usar para operaciones tales como el procesamiento temporal de los datos.</span><span class="sxs-lookup"><span data-stu-id="ea085-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="ea085-125">Sin embargo, si la máquina virtual se mueve a un nuevo host, los datos almacenados en un disco temporal se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="ea085-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="ea085-126">El tamaño del disco temporal se determina por el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="ea085-127">A los discos temporales se les asigna una letra de unidad de *d:* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ea085-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="ea085-128">Tamaños de disco temporal</span><span class="sxs-lookup"><span data-stu-id="ea085-128">Temporary disk sizes</span></span>

| <span data-ttu-id="ea085-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea085-129">Type</span></span> | <span data-ttu-id="ea085-130">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="ea085-130">VM Size</span></span> | <span data-ttu-id="ea085-131">Tamaño máximo de disco temporal (GB)</span><span class="sxs-lookup"><span data-stu-id="ea085-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="ea085-132">Uso general</span><span class="sxs-lookup"><span data-stu-id="ea085-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="ea085-133">Series A y D</span><span class="sxs-lookup"><span data-stu-id="ea085-133">A and D series</span></span> | <span data-ttu-id="ea085-134">800</span><span class="sxs-lookup"><span data-stu-id="ea085-134">800</span></span> |
| [<span data-ttu-id="ea085-135">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="ea085-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="ea085-136">Serie F</span><span class="sxs-lookup"><span data-stu-id="ea085-136">F series</span></span> | <span data-ttu-id="ea085-137">800</span><span class="sxs-lookup"><span data-stu-id="ea085-137">800</span></span> |
| [<span data-ttu-id="ea085-138">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="ea085-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="ea085-139">Series D y G</span><span class="sxs-lookup"><span data-stu-id="ea085-139">D and G series</span></span> | <span data-ttu-id="ea085-140">6144</span><span class="sxs-lookup"><span data-stu-id="ea085-140">6144</span></span> |
| [<span data-ttu-id="ea085-141">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="ea085-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="ea085-142">Serie L</span><span class="sxs-lookup"><span data-stu-id="ea085-142">L series</span></span> | <span data-ttu-id="ea085-143">5630</span><span class="sxs-lookup"><span data-stu-id="ea085-143">5630</span></span> |
| [<span data-ttu-id="ea085-144">GPU</span><span class="sxs-lookup"><span data-stu-id="ea085-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="ea085-145">Serie N</span><span class="sxs-lookup"><span data-stu-id="ea085-145">N series</span></span> | <span data-ttu-id="ea085-146">1440</span><span class="sxs-lookup"><span data-stu-id="ea085-146">1440</span></span> |
| [<span data-ttu-id="ea085-147">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="ea085-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="ea085-148">Series A y H</span><span class="sxs-lookup"><span data-stu-id="ea085-148">A and H series</span></span> | <span data-ttu-id="ea085-149">2000</span><span class="sxs-lookup"><span data-stu-id="ea085-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="ea085-150">Discos de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="ea085-150">Azure data disks</span></span>

<span data-ttu-id="ea085-151">Se pueden agregar discos de datos adicionales para instalar aplicaciones y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="ea085-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="ea085-152">Los discos de datos deben usarse en cualquier situación donde desee un almacenamiento de datos duradero y con capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ea085-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="ea085-153">Cada disco de datos tiene una capacidad máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="ea085-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="ea085-154">El tamaño de la máquina virtual determina cuántos discos de datos se pueden conectar a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="ea085-155">Para cada núcleo de la máquina virtual, se pueden conectar dos discos de datos.</span><span class="sxs-lookup"><span data-stu-id="ea085-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="ea085-156">Discos de datos máximos por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ea085-156">Max data disks per VM</span></span>

| <span data-ttu-id="ea085-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea085-157">Type</span></span> | <span data-ttu-id="ea085-158">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="ea085-158">VM Size</span></span> | <span data-ttu-id="ea085-159">Discos de datos máximos por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ea085-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="ea085-160">Uso general</span><span class="sxs-lookup"><span data-stu-id="ea085-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="ea085-161">Series A y D</span><span class="sxs-lookup"><span data-stu-id="ea085-161">A and D series</span></span> | <span data-ttu-id="ea085-162">32</span><span class="sxs-lookup"><span data-stu-id="ea085-162">32</span></span> |
| [<span data-ttu-id="ea085-163">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="ea085-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="ea085-164">Serie F</span><span class="sxs-lookup"><span data-stu-id="ea085-164">F series</span></span> | <span data-ttu-id="ea085-165">32</span><span class="sxs-lookup"><span data-stu-id="ea085-165">32</span></span> |
| [<span data-ttu-id="ea085-166">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="ea085-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="ea085-167">Series D y G</span><span class="sxs-lookup"><span data-stu-id="ea085-167">D and G series</span></span> | <span data-ttu-id="ea085-168">64</span><span class="sxs-lookup"><span data-stu-id="ea085-168">64</span></span> |
| [<span data-ttu-id="ea085-169">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="ea085-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="ea085-170">Serie L</span><span class="sxs-lookup"><span data-stu-id="ea085-170">L series</span></span> | <span data-ttu-id="ea085-171">64</span><span class="sxs-lookup"><span data-stu-id="ea085-171">64</span></span> |
| [<span data-ttu-id="ea085-172">GPU</span><span class="sxs-lookup"><span data-stu-id="ea085-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="ea085-173">Serie N</span><span class="sxs-lookup"><span data-stu-id="ea085-173">N series</span></span> | <span data-ttu-id="ea085-174">48</span><span class="sxs-lookup"><span data-stu-id="ea085-174">48</span></span> |
| [<span data-ttu-id="ea085-175">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="ea085-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="ea085-176">Series A y H</span><span class="sxs-lookup"><span data-stu-id="ea085-176">A and H series</span></span> | <span data-ttu-id="ea085-177">32</span><span class="sxs-lookup"><span data-stu-id="ea085-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="ea085-178">Tipos de disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ea085-178">VM disk types</span></span>

<span data-ttu-id="ea085-179">Azure proporciona dos tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="ea085-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="ea085-180">Disco estándar</span><span class="sxs-lookup"><span data-stu-id="ea085-180">Standard disk</span></span>

<span data-ttu-id="ea085-181">El almacenamiento estándar está respaldado por unidades de disco duro y ofrece un almacenamiento rentable al mismo tiempo que tiene un rendimiento superior.</span><span class="sxs-lookup"><span data-stu-id="ea085-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="ea085-182">Los discos estándar son ideales para cargas de trabajo de desarrollo y prueba rentables.</span><span class="sxs-lookup"><span data-stu-id="ea085-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="ea085-183">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="ea085-183">Premium disk</span></span>

<span data-ttu-id="ea085-184">Los discos Premium están respaldados por un disco de latencia reducida y alto rendimiento basado en SSD.</span><span class="sxs-lookup"><span data-stu-id="ea085-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="ea085-185">Es perfecto para máquinas virtuales que ejecutan cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="ea085-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="ea085-186">Premium Storage es compatible con las máquinas virtuales de las series DS, DSv2, GS y FS.</span><span class="sxs-lookup"><span data-stu-id="ea085-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="ea085-187">Los discos Premium incluyen 3 tipos (P10, P20 y P30); el tamaño del disco determina el tipo de disco.</span><span class="sxs-lookup"><span data-stu-id="ea085-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="ea085-188">Al seleccionar el tamaño de un disco, el valor se redondea al siguiente tipo.</span><span class="sxs-lookup"><span data-stu-id="ea085-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="ea085-189">Por ejemplo, si el tamaño es inferior a 128 GB, el tipo de disco será P10, entre 129 y 512 P20, y más de 512 P30.</span><span class="sxs-lookup"><span data-stu-id="ea085-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="ea085-190">Rendimiento de los discos Premium</span><span class="sxs-lookup"><span data-stu-id="ea085-190">Premium disk performance</span></span>

|<span data-ttu-id="ea085-191">Tipo de disco de Premium Storage</span><span class="sxs-lookup"><span data-stu-id="ea085-191">Premium storage disk type</span></span> | <span data-ttu-id="ea085-192">P10</span><span class="sxs-lookup"><span data-stu-id="ea085-192">P10</span></span> | <span data-ttu-id="ea085-193">P20</span><span class="sxs-lookup"><span data-stu-id="ea085-193">P20</span></span> | <span data-ttu-id="ea085-194">P30</span><span class="sxs-lookup"><span data-stu-id="ea085-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ea085-195">Tamaño del disco (redondeo hacia arriba)</span><span class="sxs-lookup"><span data-stu-id="ea085-195">Disk size (round up)</span></span> | <span data-ttu-id="ea085-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="ea085-196">128 GB</span></span> | <span data-ttu-id="ea085-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="ea085-197">512 GB</span></span> | <span data-ttu-id="ea085-198">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="ea085-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="ea085-199">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="ea085-199">IOPS per disk</span></span> | <span data-ttu-id="ea085-200">500</span><span class="sxs-lookup"><span data-stu-id="ea085-200">500</span></span> | <span data-ttu-id="ea085-201">2,300</span><span class="sxs-lookup"><span data-stu-id="ea085-201">2,300</span></span> | <span data-ttu-id="ea085-202">5.000</span><span class="sxs-lookup"><span data-stu-id="ea085-202">5,000</span></span> |
<span data-ttu-id="ea085-203">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="ea085-203">Throughput per disk</span></span> | <span data-ttu-id="ea085-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="ea085-204">100 MB/s</span></span> | <span data-ttu-id="ea085-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="ea085-205">150 MB/s</span></span> | <span data-ttu-id="ea085-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="ea085-206">200 MB/s</span></span> |

<span data-ttu-id="ea085-207">Aunque la tabla anterior identifica las IOPS máximas por disco, se puede obtener un mayor nivel de rendimiento dividiendo varios discos de datos.</span><span class="sxs-lookup"><span data-stu-id="ea085-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="ea085-208">Por ejemplo, 64 discos de datos pueden conectarse a la máquina virtual Standard_GS5.</span><span class="sxs-lookup"><span data-stu-id="ea085-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="ea085-209">Si cada uno de estos discos tienen un tamaño de P30, se puede lograr un máximo de 80 000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="ea085-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="ea085-210">Para obtener información detallada sobre las IOPS máximas por máquina virtual, consulte el artículo sobre [tamaños de máquinas virtuales Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ea085-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="ea085-211">Creación y conexión de discos</span><span class="sxs-lookup"><span data-stu-id="ea085-211">Create and attach disks</span></span>

<span data-ttu-id="ea085-212">Para completar el ejemplo de este tutorial, debe tener una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ea085-213">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="ea085-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="ea085-214">Al trabajar en el tutorial, reemplace los nombres de grupo de recursos y máquina virtual cuando proceda.</span><span class="sxs-lookup"><span data-stu-id="ea085-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="ea085-215">Cree la configuración inicial con [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="ea085-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="ea085-216">En el ejemplo siguiente se crea un disco denominado con un tamaño de 128 gigabytes.</span><span class="sxs-lookup"><span data-stu-id="ea085-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="ea085-217">Cree el disco de datos con el comando [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="ea085-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="ea085-218">Obtenga la máquina virtual que desea agregar al disco de datos con el comando [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="ea085-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="ea085-219">Agregue el disco de datos a la configuración de máquina virtual con el comando [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="ea085-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="ea085-220">Actualice la máquina virtual con el comando [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="ea085-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="ea085-221">Preparación de los discos de datos</span><span class="sxs-lookup"><span data-stu-id="ea085-221">Prepare data disks</span></span>

<span data-ttu-id="ea085-222">Cuando se haya conectado un disco a la máquina virtual, el sistema operativo debe configurarse para utilizar el disco.</span><span class="sxs-lookup"><span data-stu-id="ea085-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="ea085-223">En el ejemplo siguiente se muestra cómo configurar manualmente el primer disco que se agrega a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="ea085-224">Este proceso también se puede automatizar utilizando la [extensión de script personalizado](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ea085-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="ea085-225">Configuración manual</span><span class="sxs-lookup"><span data-stu-id="ea085-225">Manual configuration</span></span>

<span data-ttu-id="ea085-226">Crear una conexión RDP con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="ea085-227">Abra PowerShell y ejecute este script.</span><span class="sxs-lookup"><span data-stu-id="ea085-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="ea085-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea085-228">Next steps</span></span>

<span data-ttu-id="ea085-229">En este tutorial, ha aprendido sobre temas relacionados con los discos de máquina virtual; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ea085-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea085-230">Discos del SO y temporales</span><span class="sxs-lookup"><span data-stu-id="ea085-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="ea085-231">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="ea085-231">Data disks</span></span>
> * <span data-ttu-id="ea085-232">Discos Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="ea085-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="ea085-233">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="ea085-233">Disk performance</span></span>
> * <span data-ttu-id="ea085-234">Conectar y preparar los discos de datos</span><span class="sxs-lookup"><span data-stu-id="ea085-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="ea085-235">Siga con el siguiente tutorial para aprender sobre la automatización de la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea085-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea085-236">Automatización de la configuración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ea085-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
