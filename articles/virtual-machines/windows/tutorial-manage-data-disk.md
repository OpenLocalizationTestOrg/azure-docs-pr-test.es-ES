---
title: aaaManage Azure discos con hello Azure PowerShell | Documentos de Microsoft
description: 'Tutorial: administrar los discos de Azure con hello Azure PowerShell'
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="6066e-103">Administración de discos de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6066e-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="6066e-104">Máquinas virtuales de Azure usa el sistema operativo de discos toostore hello las máquinas virtuales, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="6066e-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="6066e-105">Al crear una máquina virtual es importante toochoose un tamaño de disco y carga de trabajo de configuración adecuado toohello que se esperaba.</span><span class="sxs-lookup"><span data-stu-id="6066e-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="6066e-106">Este tutorial trata la implementación y administración de discos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6066e-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="6066e-107">Aprenderá sobre los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="6066e-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6066e-108">Discos del SO y temporales</span><span class="sxs-lookup"><span data-stu-id="6066e-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6066e-109">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="6066e-109">Data disks</span></span>
> * <span data-ttu-id="6066e-110">Discos Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="6066e-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="6066e-111">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="6066e-111">Disk performance</span></span>
> * <span data-ttu-id="6066e-112">Conectar y preparar los discos de datos</span><span class="sxs-lookup"><span data-stu-id="6066e-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="6066e-113">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="6066e-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="6066e-114">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="6066e-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="6066e-115">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6066e-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="6066e-116">Discos de Azure predeterminados</span><span class="sxs-lookup"><span data-stu-id="6066e-116">Default Azure disks</span></span>

<span data-ttu-id="6066e-117">Cuando se crea una máquina virtual de Azure, dos discos son máquinas virtuales de toohello unido automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6066e-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="6066e-118">**Disco del sistema operativo** : discos del sistema operativo se pueden cambiar la too1 terabytes y hosts Hola sistema operativo de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6066e-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="6066e-119">disco de SO Hola se asigna una letra de unidad de *c:* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6066e-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="6066e-120">configuración de disco del sistema operativo Hola el almacenamiento en caché de disco de Hello está optimizado para el rendimiento del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="6066e-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="6066e-121">disco de SO Hello **no debería** hospedar aplicaciones o datos.</span><span class="sxs-lookup"><span data-stu-id="6066e-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="6066e-122">Para aplicaciones y datos, use un disco de datos. Explicamos esto más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6066e-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="6066e-123">**Disco temporal** -temporales discos utilizan una unidad de estado sólida que se encuentra en hello mismo host de Azure como Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6066e-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="6066e-124">Los discos temporales son muy eficiente y se pueden usar para operaciones tales como el procesamiento temporal de los datos.</span><span class="sxs-lookup"><span data-stu-id="6066e-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="6066e-125">Sin embargo, si Hola VM es tooa movida nuevo host, se quitará cualquier dato almacenado en un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="6066e-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="6066e-126">tamaño de Hola de disco temporal de Hola se determina por hello tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6066e-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="6066e-127">A los discos temporales se les asigna una letra de unidad de *d:* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6066e-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="6066e-128">Tamaños de disco temporal</span><span class="sxs-lookup"><span data-stu-id="6066e-128">Temporary disk sizes</span></span>

| <span data-ttu-id="6066e-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="6066e-129">Type</span></span> | <span data-ttu-id="6066e-130">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="6066e-130">VM Size</span></span> | <span data-ttu-id="6066e-131">Tamaño máximo de disco temporal (GB)</span><span class="sxs-lookup"><span data-stu-id="6066e-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="6066e-132">Uso general</span><span class="sxs-lookup"><span data-stu-id="6066e-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6066e-133">Series A y D</span><span class="sxs-lookup"><span data-stu-id="6066e-133">A and D series</span></span> | <span data-ttu-id="6066e-134">800</span><span class="sxs-lookup"><span data-stu-id="6066e-134">800</span></span> |
| [<span data-ttu-id="6066e-135">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="6066e-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6066e-136">Serie F</span><span class="sxs-lookup"><span data-stu-id="6066e-136">F series</span></span> | <span data-ttu-id="6066e-137">800</span><span class="sxs-lookup"><span data-stu-id="6066e-137">800</span></span> |
| [<span data-ttu-id="6066e-138">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="6066e-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6066e-139">Series D y G</span><span class="sxs-lookup"><span data-stu-id="6066e-139">D and G series</span></span> | <span data-ttu-id="6066e-140">6144</span><span class="sxs-lookup"><span data-stu-id="6066e-140">6144</span></span> |
| [<span data-ttu-id="6066e-141">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="6066e-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6066e-142">Serie L</span><span class="sxs-lookup"><span data-stu-id="6066e-142">L series</span></span> | <span data-ttu-id="6066e-143">5630</span><span class="sxs-lookup"><span data-stu-id="6066e-143">5630</span></span> |
| [<span data-ttu-id="6066e-144">GPU</span><span class="sxs-lookup"><span data-stu-id="6066e-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6066e-145">Serie N</span><span class="sxs-lookup"><span data-stu-id="6066e-145">N series</span></span> | <span data-ttu-id="6066e-146">1440</span><span class="sxs-lookup"><span data-stu-id="6066e-146">1440</span></span> |
| [<span data-ttu-id="6066e-147">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="6066e-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6066e-148">Series A y H</span><span class="sxs-lookup"><span data-stu-id="6066e-148">A and H series</span></span> | <span data-ttu-id="6066e-149">2000</span><span class="sxs-lookup"><span data-stu-id="6066e-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="6066e-150">Discos de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="6066e-150">Azure data disks</span></span>

<span data-ttu-id="6066e-151">Se pueden agregar discos de datos adicionales para instalar aplicaciones y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="6066e-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="6066e-152">Los discos de datos deben usarse en cualquier situación donde desee un almacenamiento de datos duradero y con capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="6066e-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="6066e-153">Cada disco de datos tiene una capacidad máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="6066e-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="6066e-154">tamaño de Hola de máquina virtual de Hola determina cuántos discos de datos pueden estar adjunto tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6066e-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="6066e-155">Para cada núcleo de la máquina virtual, se pueden conectar dos discos de datos.</span><span class="sxs-lookup"><span data-stu-id="6066e-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="6066e-156">Discos de datos máximos por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6066e-156">Max data disks per VM</span></span>

| <span data-ttu-id="6066e-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="6066e-157">Type</span></span> | <span data-ttu-id="6066e-158">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="6066e-158">VM Size</span></span> | <span data-ttu-id="6066e-159">Discos de datos máximos por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6066e-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="6066e-160">Uso general</span><span class="sxs-lookup"><span data-stu-id="6066e-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6066e-161">Series A y D</span><span class="sxs-lookup"><span data-stu-id="6066e-161">A and D series</span></span> | <span data-ttu-id="6066e-162">32</span><span class="sxs-lookup"><span data-stu-id="6066e-162">32</span></span> |
| [<span data-ttu-id="6066e-163">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="6066e-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6066e-164">Serie F</span><span class="sxs-lookup"><span data-stu-id="6066e-164">F series</span></span> | <span data-ttu-id="6066e-165">32</span><span class="sxs-lookup"><span data-stu-id="6066e-165">32</span></span> |
| [<span data-ttu-id="6066e-166">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="6066e-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6066e-167">Series D y G</span><span class="sxs-lookup"><span data-stu-id="6066e-167">D and G series</span></span> | <span data-ttu-id="6066e-168">64</span><span class="sxs-lookup"><span data-stu-id="6066e-168">64</span></span> |
| [<span data-ttu-id="6066e-169">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="6066e-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6066e-170">Serie L</span><span class="sxs-lookup"><span data-stu-id="6066e-170">L series</span></span> | <span data-ttu-id="6066e-171">64</span><span class="sxs-lookup"><span data-stu-id="6066e-171">64</span></span> |
| [<span data-ttu-id="6066e-172">GPU</span><span class="sxs-lookup"><span data-stu-id="6066e-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6066e-173">Serie N</span><span class="sxs-lookup"><span data-stu-id="6066e-173">N series</span></span> | <span data-ttu-id="6066e-174">48</span><span class="sxs-lookup"><span data-stu-id="6066e-174">48</span></span> |
| [<span data-ttu-id="6066e-175">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="6066e-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6066e-176">Series A y H</span><span class="sxs-lookup"><span data-stu-id="6066e-176">A and H series</span></span> | <span data-ttu-id="6066e-177">32</span><span class="sxs-lookup"><span data-stu-id="6066e-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="6066e-178">Tipos de disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6066e-178">VM disk types</span></span>

<span data-ttu-id="6066e-179">Azure proporciona dos tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="6066e-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="6066e-180">Disco estándar</span><span class="sxs-lookup"><span data-stu-id="6066e-180">Standard disk</span></span>

<span data-ttu-id="6066e-181">El almacenamiento estándar está respaldado por unidades de disco duro y ofrece un almacenamiento rentable al mismo tiempo que tiene un rendimiento superior.</span><span class="sxs-lookup"><span data-stu-id="6066e-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="6066e-182">Los discos estándar son ideales para cargas de trabajo de desarrollo y prueba rentables.</span><span class="sxs-lookup"><span data-stu-id="6066e-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="6066e-183">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="6066e-183">Premium disk</span></span>

<span data-ttu-id="6066e-184">Los discos Premium están respaldados por un disco de latencia reducida y alto rendimiento basado en SSD.</span><span class="sxs-lookup"><span data-stu-id="6066e-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="6066e-185">Es perfecto para máquinas virtuales que ejecutan cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="6066e-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="6066e-186">Premium Storage es compatible con las máquinas virtuales de las series DS, DSv2, GS y FS.</span><span class="sxs-lookup"><span data-stu-id="6066e-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="6066e-187">Los discos Premium vienen en tres tipos (P10, P20, P30), tamaño de hello del disco de hello determina el tipo de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="6066e-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="6066e-188">Al seleccionar esta opción, un valor de Hola de tamaño de disco se redondea toohello siguiente tipo.</span><span class="sxs-lookup"><span data-stu-id="6066e-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="6066e-189">Por ejemplo, si el tamaño de hello está por debajo de tipo de disco de 128 GB Hola será P10, entre 129 y 512 P20 y más de 512 P30.</span><span class="sxs-lookup"><span data-stu-id="6066e-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="6066e-190">Rendimiento del disco Premium</span><span class="sxs-lookup"><span data-stu-id="6066e-190">Premium disk performance</span></span>

|<span data-ttu-id="6066e-191">Tipo de disco de Premium Storage</span><span class="sxs-lookup"><span data-stu-id="6066e-191">Premium storage disk type</span></span> | <span data-ttu-id="6066e-192">P10</span><span class="sxs-lookup"><span data-stu-id="6066e-192">P10</span></span> | <span data-ttu-id="6066e-193">P20</span><span class="sxs-lookup"><span data-stu-id="6066e-193">P20</span></span> | <span data-ttu-id="6066e-194">P30</span><span class="sxs-lookup"><span data-stu-id="6066e-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6066e-195">Tamaño del disco (redondeo hacia arriba)</span><span class="sxs-lookup"><span data-stu-id="6066e-195">Disk size (round up)</span></span> | <span data-ttu-id="6066e-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="6066e-196">128 GB</span></span> | <span data-ttu-id="6066e-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="6066e-197">512 GB</span></span> | <span data-ttu-id="6066e-198">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="6066e-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="6066e-199">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="6066e-199">IOPS per disk</span></span> | <span data-ttu-id="6066e-200">500</span><span class="sxs-lookup"><span data-stu-id="6066e-200">500</span></span> | <span data-ttu-id="6066e-201">2,300</span><span class="sxs-lookup"><span data-stu-id="6066e-201">2,300</span></span> | <span data-ttu-id="6066e-202">5.000</span><span class="sxs-lookup"><span data-stu-id="6066e-202">5,000</span></span> |
<span data-ttu-id="6066e-203">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="6066e-203">Throughput per disk</span></span> | <span data-ttu-id="6066e-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="6066e-204">100 MB/s</span></span> | <span data-ttu-id="6066e-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="6066e-205">150 MB/s</span></span> | <span data-ttu-id="6066e-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="6066e-206">200 MB/s</span></span> |

<span data-ttu-id="6066e-207">Mientras Hola por encima de la tabla identifica máximo de IOPS por disco, se consigue un mayor nivel de rendimiento por varios discos de datos de creación de bandas.</span><span class="sxs-lookup"><span data-stu-id="6066e-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="6066e-208">Por ejemplo, 64 datos discos pueden estar conectado tooStandard_GS5 VM.</span><span class="sxs-lookup"><span data-stu-id="6066e-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="6066e-209">Si cada uno de estos discos tienen un tamaño de P30, se puede lograr un máximo de 80 000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="6066e-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="6066e-210">Para obtener información detallada sobre las IOPS máximas por máquina virtual, consulte el artículo sobre [tamaños de máquinas virtuales Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="6066e-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="6066e-211">Creación y conexión de discos</span><span class="sxs-lookup"><span data-stu-id="6066e-211">Create and attach disks</span></span>

<span data-ttu-id="6066e-212">ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="6066e-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="6066e-213">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="6066e-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="6066e-214">Cuando reemplace trabajar a través de tutorial de hello, grupo de recursos de Hola y VM nombres cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6066e-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="6066e-215">Crear la configuración inicial de hello con [AzureRmDiskConfig nuevo](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="6066e-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="6066e-216">Hola de ejemplo siguiente configura un disco que es de 128 gigabytes de tamaño.</span><span class="sxs-lookup"><span data-stu-id="6066e-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="6066e-217">Crear disco de datos de hello con hello [AzureRmDisk New](/powershell/module/azurerm.compute/new-azurermdisk) comando.</span><span class="sxs-lookup"><span data-stu-id="6066e-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="6066e-218">Get hello máquina virtual que tooadd Hola Hola de toowith de disco de datos [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando.</span><span class="sxs-lookup"><span data-stu-id="6066e-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="6066e-219">Agregar configuración de máquina virtual de toohello Hola datos disco con hello [AzureRmVMDataDisk agregar](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.</span><span class="sxs-lookup"><span data-stu-id="6066e-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="6066e-220">Actualizar la máquina virtual de hello con hello [AzureRmVM actualización](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.</span><span class="sxs-lookup"><span data-stu-id="6066e-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="6066e-221">Preparación de los discos de datos</span><span class="sxs-lookup"><span data-stu-id="6066e-221">Prepare data disks</span></span>

<span data-ttu-id="6066e-222">Una vez instalado un disco de máquina virtual de toohello adjunto, sistema operativo de hello debe toobe configurado toouse Hola disco.</span><span class="sxs-lookup"><span data-stu-id="6066e-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="6066e-223">Hello en el ejemplo siguiente se muestra cómo configurar el primer disco Hola de agrega toomanually toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6066e-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="6066e-224">También se puede automatizar este proceso con hello [extensión de script personalizado](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6066e-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="6066e-225">Configuración manual</span><span class="sxs-lookup"><span data-stu-id="6066e-225">Manual configuration</span></span>

<span data-ttu-id="6066e-226">Crear una conexión RDP con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6066e-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="6066e-227">Abra PowerShell y ejecute este script.</span><span class="sxs-lookup"><span data-stu-id="6066e-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="6066e-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6066e-228">Next steps</span></span>

<span data-ttu-id="6066e-229">En este tutorial, ha aprendido sobre temas relacionados con los discos de máquina virtual; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6066e-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6066e-230">Discos del SO y temporales</span><span class="sxs-lookup"><span data-stu-id="6066e-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6066e-231">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="6066e-231">Data disks</span></span>
> * <span data-ttu-id="6066e-232">Discos Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="6066e-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="6066e-233">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="6066e-233">Disk performance</span></span>
> * <span data-ttu-id="6066e-234">Conectar y preparar los discos de datos</span><span class="sxs-lookup"><span data-stu-id="6066e-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="6066e-235">Avanzar toohello toolearn de tutorial siguiente acerca de cómo automatizar la configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6066e-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6066e-236">Automatización de la configuración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6066e-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
