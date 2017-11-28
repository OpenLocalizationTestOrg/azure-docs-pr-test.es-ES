---
title: aaaManage Azure discos con hello CLI de Azure | Documentos de Microsoft
description: 'Tutorial: administrar los discos de Azure con hello CLI de Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="26013-103">Administrar discos de Azure con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="26013-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="26013-104">Máquinas virtuales de Azure usa el sistema operativo de discos toostore hello las máquinas virtuales, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="26013-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="26013-105">Al crear una máquina virtual es importante toochoose un tamaño de disco y carga de trabajo de configuración adecuado toohello que se esperaba.</span><span class="sxs-lookup"><span data-stu-id="26013-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="26013-106">Este tutorial trata la implementación y administración de discos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="26013-107">Aprenderá sobre los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="26013-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26013-108">Discos del SO y temporales</span><span class="sxs-lookup"><span data-stu-id="26013-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="26013-109">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="26013-109">Data disks</span></span>
> * <span data-ttu-id="26013-110">Discos Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="26013-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="26013-111">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="26013-111">Disk performance</span></span>
> * <span data-ttu-id="26013-112">Conectar y preparar los discos de datos</span><span class="sxs-lookup"><span data-stu-id="26013-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="26013-113">Cambiar el tamaño de los discos</span><span class="sxs-lookup"><span data-stu-id="26013-113">Resizing disks</span></span>
> * <span data-ttu-id="26013-114">Instantáneas de disco</span><span class="sxs-lookup"><span data-stu-id="26013-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="26013-115">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="26013-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="26013-116">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="26013-117">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="26013-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="26013-118">Discos de Azure predeterminados</span><span class="sxs-lookup"><span data-stu-id="26013-118">Default Azure disks</span></span>

<span data-ttu-id="26013-119">Cuando se crea una máquina virtual de Azure, dos discos son máquinas virtuales de toohello unido automáticamente.</span><span class="sxs-lookup"><span data-stu-id="26013-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="26013-120">**Disco del sistema operativo** : discos del sistema operativo se pueden cambiar la too1 terabytes y hosts Hola sistema operativo de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="26013-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="26013-121">Hola SO disco se etiqueta */dev/sda* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="26013-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="26013-122">configuración de disco del sistema operativo Hola el almacenamiento en caché de disco de Hello está optimizado para el rendimiento del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="26013-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="26013-123">Debido a esta configuración, Hola disco del sistema operativo **no debería** hospedar aplicaciones o datos.</span><span class="sxs-lookup"><span data-stu-id="26013-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="26013-124">Para aplicaciones y datos, use discos de datos, que se detallan más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="26013-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="26013-125">**Disco temporal** -temporales discos utilizan una unidad de estado sólida que se encuentra en hello mismo host de Azure como Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="26013-126">Los discos temporales son muy eficiente y se pueden usar para operaciones tales como el procesamiento temporal de los datos.</span><span class="sxs-lookup"><span data-stu-id="26013-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="26013-127">Sin embargo, si Hola VM es tooa movida nuevo host, se quitará cualquier dato almacenado en un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="26013-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="26013-128">tamaño de Hola de disco temporal de Hola se determina por hello tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="26013-129">Los discos temporales llevan la etiqueta */dev/sdb* y tienen un punto de montaje de */mnt*.</span><span class="sxs-lookup"><span data-stu-id="26013-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="26013-130">Tamaños de disco temporal</span><span class="sxs-lookup"><span data-stu-id="26013-130">Temporary disk sizes</span></span>

| <span data-ttu-id="26013-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="26013-131">Type</span></span> | <span data-ttu-id="26013-132">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="26013-132">VM Size</span></span> | <span data-ttu-id="26013-133">Tamaño máximo de disco temporal (GB)</span><span class="sxs-lookup"><span data-stu-id="26013-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="26013-134">Uso general</span><span class="sxs-lookup"><span data-stu-id="26013-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="26013-135">Series A y D</span><span class="sxs-lookup"><span data-stu-id="26013-135">A and D series</span></span> | <span data-ttu-id="26013-136">800</span><span class="sxs-lookup"><span data-stu-id="26013-136">800</span></span> |
| [<span data-ttu-id="26013-137">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="26013-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="26013-138">Serie F</span><span class="sxs-lookup"><span data-stu-id="26013-138">F series</span></span> | <span data-ttu-id="26013-139">800</span><span class="sxs-lookup"><span data-stu-id="26013-139">800</span></span> |
| [<span data-ttu-id="26013-140">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="26013-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="26013-141">Series D y G</span><span class="sxs-lookup"><span data-stu-id="26013-141">D and G series</span></span> | <span data-ttu-id="26013-142">6144</span><span class="sxs-lookup"><span data-stu-id="26013-142">6144</span></span> |
| [<span data-ttu-id="26013-143">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="26013-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="26013-144">Serie L</span><span class="sxs-lookup"><span data-stu-id="26013-144">L series</span></span> | <span data-ttu-id="26013-145">5630</span><span class="sxs-lookup"><span data-stu-id="26013-145">5630</span></span> |
| [<span data-ttu-id="26013-146">GPU</span><span class="sxs-lookup"><span data-stu-id="26013-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="26013-147">Serie N</span><span class="sxs-lookup"><span data-stu-id="26013-147">N series</span></span> | <span data-ttu-id="26013-148">1440</span><span class="sxs-lookup"><span data-stu-id="26013-148">1440</span></span> |
| [<span data-ttu-id="26013-149">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="26013-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="26013-150">Series A y H</span><span class="sxs-lookup"><span data-stu-id="26013-150">A and H series</span></span> | <span data-ttu-id="26013-151">2000</span><span class="sxs-lookup"><span data-stu-id="26013-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="26013-152">Discos de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="26013-152">Azure data disks</span></span>

<span data-ttu-id="26013-153">Se pueden agregar discos de datos adicionales para instalar aplicaciones y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="26013-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="26013-154">Los discos de datos deben usarse en cualquier situación donde desee un almacenamiento de datos duradero y con capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="26013-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="26013-155">Cada disco de datos tiene una capacidad máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="26013-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="26013-156">tamaño de Hola de máquina virtual de Hola determina cuántos discos de datos pueden estar adjunto tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="26013-157">Para cada núcleo de la máquina virtual, se pueden conectar dos discos de datos.</span><span class="sxs-lookup"><span data-stu-id="26013-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="26013-158">Discos de datos máximos por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="26013-158">Max data disks per VM</span></span>

| <span data-ttu-id="26013-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="26013-159">Type</span></span> | <span data-ttu-id="26013-160">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="26013-160">VM Size</span></span> | <span data-ttu-id="26013-161">Discos de datos máximos por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="26013-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="26013-162">Uso general</span><span class="sxs-lookup"><span data-stu-id="26013-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="26013-163">Series A y D</span><span class="sxs-lookup"><span data-stu-id="26013-163">A and D series</span></span> | <span data-ttu-id="26013-164">32</span><span class="sxs-lookup"><span data-stu-id="26013-164">32</span></span> |
| [<span data-ttu-id="26013-165">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="26013-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="26013-166">Serie F</span><span class="sxs-lookup"><span data-stu-id="26013-166">F series</span></span> | <span data-ttu-id="26013-167">32</span><span class="sxs-lookup"><span data-stu-id="26013-167">32</span></span> |
| [<span data-ttu-id="26013-168">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="26013-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="26013-169">Series D y G</span><span class="sxs-lookup"><span data-stu-id="26013-169">D and G series</span></span> | <span data-ttu-id="26013-170">64</span><span class="sxs-lookup"><span data-stu-id="26013-170">64</span></span> |
| [<span data-ttu-id="26013-171">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="26013-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="26013-172">Serie L</span><span class="sxs-lookup"><span data-stu-id="26013-172">L series</span></span> | <span data-ttu-id="26013-173">64</span><span class="sxs-lookup"><span data-stu-id="26013-173">64</span></span> |
| [<span data-ttu-id="26013-174">GPU</span><span class="sxs-lookup"><span data-stu-id="26013-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="26013-175">Serie N</span><span class="sxs-lookup"><span data-stu-id="26013-175">N series</span></span> | <span data-ttu-id="26013-176">48</span><span class="sxs-lookup"><span data-stu-id="26013-176">48</span></span> |
| [<span data-ttu-id="26013-177">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="26013-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="26013-178">Series A y H</span><span class="sxs-lookup"><span data-stu-id="26013-178">A and H series</span></span> | <span data-ttu-id="26013-179">32</span><span class="sxs-lookup"><span data-stu-id="26013-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="26013-180">Tipos de disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="26013-180">VM disk types</span></span>

<span data-ttu-id="26013-181">Azure proporciona dos tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="26013-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="26013-182">Disco estándar</span><span class="sxs-lookup"><span data-stu-id="26013-182">Standard disk</span></span>

<span data-ttu-id="26013-183">El almacenamiento estándar está respaldado por unidades de disco duro y ofrece un almacenamiento rentable al mismo tiempo que tiene un rendimiento superior.</span><span class="sxs-lookup"><span data-stu-id="26013-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="26013-184">Los discos estándar son ideales para cargas de trabajo de desarrollo y prueba rentables.</span><span class="sxs-lookup"><span data-stu-id="26013-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="26013-185">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="26013-185">Premium disk</span></span>

<span data-ttu-id="26013-186">Los discos Premium están respaldados por un disco de latencia reducida y alto rendimiento basado en SSD.</span><span class="sxs-lookup"><span data-stu-id="26013-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="26013-187">Es perfecto para máquinas virtuales que ejecutan cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="26013-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="26013-188">Premium Storage es compatible con las máquinas virtuales de las series DS, DSv2, GS y FS.</span><span class="sxs-lookup"><span data-stu-id="26013-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="26013-189">Los discos Premium vienen en tres tipos (P10, P20, P30), tamaño de hello del disco de hello determina el tipo de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="26013-190">Al seleccionar esta opción, un valor de Hola de tamaño de disco se redondea toohello siguiente tipo.</span><span class="sxs-lookup"><span data-stu-id="26013-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="26013-191">Por ejemplo, si el tamaño del disco de hello es inferior a 128 GB, tipo de disco de hello es P10.</span><span class="sxs-lookup"><span data-stu-id="26013-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="26013-192">Si el tamaño del disco de hello es entre 129 y 512 GB, tamaño de hello es un P20.</span><span class="sxs-lookup"><span data-stu-id="26013-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="26013-193">Nada más de 512 GB, tamaño de hello es un P30.</span><span class="sxs-lookup"><span data-stu-id="26013-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="26013-194">Rendimiento del disco Premium</span><span class="sxs-lookup"><span data-stu-id="26013-194">Premium disk performance</span></span>

|<span data-ttu-id="26013-195">Tipo de disco de Premium Storage</span><span class="sxs-lookup"><span data-stu-id="26013-195">Premium storage disk type</span></span> | <span data-ttu-id="26013-196">P10</span><span class="sxs-lookup"><span data-stu-id="26013-196">P10</span></span> | <span data-ttu-id="26013-197">P20</span><span class="sxs-lookup"><span data-stu-id="26013-197">P20</span></span> | <span data-ttu-id="26013-198">P30</span><span class="sxs-lookup"><span data-stu-id="26013-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26013-199">Tamaño del disco (redondeo hacia arriba)</span><span class="sxs-lookup"><span data-stu-id="26013-199">Disk size (round up)</span></span> | <span data-ttu-id="26013-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="26013-200">128 GB</span></span> | <span data-ttu-id="26013-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="26013-201">512 GB</span></span> | <span data-ttu-id="26013-202">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="26013-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="26013-203">Máximo de IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="26013-203">Max IOPS per disk</span></span> | <span data-ttu-id="26013-204">500</span><span class="sxs-lookup"><span data-stu-id="26013-204">500</span></span> | <span data-ttu-id="26013-205">2,300</span><span class="sxs-lookup"><span data-stu-id="26013-205">2,300</span></span> | <span data-ttu-id="26013-206">5.000</span><span class="sxs-lookup"><span data-stu-id="26013-206">5,000</span></span> |
<span data-ttu-id="26013-207">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="26013-207">Throughput per disk</span></span> | <span data-ttu-id="26013-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="26013-208">100 MB/s</span></span> | <span data-ttu-id="26013-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="26013-209">150 MB/s</span></span> | <span data-ttu-id="26013-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="26013-210">200 MB/s</span></span> |

<span data-ttu-id="26013-211">Mientras Hola por encima de la tabla identifica máximo de IOPS por disco, se consigue un mayor nivel de rendimiento por varios discos de datos de creación de bandas.</span><span class="sxs-lookup"><span data-stu-id="26013-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="26013-212">Por ejemplo, una máquina virtual Standard_GS5 puede conseguir 80 000 IOPS como máximo.</span><span class="sxs-lookup"><span data-stu-id="26013-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="26013-213">Para más información sobre el número máximo de IOPS por máquina virtual, consulte los [tamaños de máquinas virtuales Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="26013-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="26013-214">Creación y conexión de discos</span><span class="sxs-lookup"><span data-stu-id="26013-214">Create and attach disks</span></span>

<span data-ttu-id="26013-215">Discos de datos se pueden crear y conectados en el momento de la creación de máquinas virtuales o tooan existente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="26013-216">Conexión del disco en el momento de creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="26013-216">Attach disk at VM creation</span></span>

<span data-ttu-id="26013-217">Crear un grupo de recursos con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="26013-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="26013-218">Crear una máquina virtual mediante hello [crear vm az]( /cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="26013-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="26013-219">Hola `--datadisk-sizes-gb` argumento es usado toospecify que un disco adicional debe crearse y adjunta la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="26013-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="26013-220">toocreate y adjuntar más de un disco, use una lista delimitada por espacios de los valores de tamaño de disco.</span><span class="sxs-lookup"><span data-stu-id="26013-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="26013-221">En el siguiente ejemplo de Hola, se crea una máquina virtual con discos de datos de dos, ambos 128 GB.</span><span class="sxs-lookup"><span data-stu-id="26013-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="26013-222">Dado que los tamaños de disco Hola son 128 GB, estos discos se configuran como P10s, que proporcionan el máximo de 500 IOPS por disco.</span><span class="sxs-lookup"><span data-stu-id="26013-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="26013-223">Adjuntar disco tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="26013-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="26013-224">toocreate y conectar una máquina virtual existente de disco tooan nuevo, use hello [adjuntar el disco de vm az](/cli/azure/vm/disk#attach) comando.</span><span class="sxs-lookup"><span data-stu-id="26013-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="26013-225">Hello en el ejemplo siguiente se crea un disco de premium, 128 gigabytes de tamaño y lo adjunta toohello que crea la VM en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="26013-226">Preparación de los discos de datos</span><span class="sxs-lookup"><span data-stu-id="26013-226">Prepare data disks</span></span>

<span data-ttu-id="26013-227">Una vez instalado un disco de máquina virtual de toohello adjunto, sistema operativo de hello debe toobe configurado toouse Hola disco.</span><span class="sxs-lookup"><span data-stu-id="26013-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="26013-228">Hola de ejemplo siguiente muestra cómo configurar toomanually en un disco.</span><span class="sxs-lookup"><span data-stu-id="26013-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="26013-229">Este proceso también se puede automatizar mediante cloud-init, que se trata en un [tutorial posterior](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="26013-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="26013-230">Configuración manual</span><span class="sxs-lookup"><span data-stu-id="26013-230">Manual configuration</span></span>

<span data-ttu-id="26013-231">Crear una conexión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="26013-232">Reemplace la dirección IP de ejemplo de Hola con la dirección IP pública de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="26013-233">Disco de partición Hola con `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="26013-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="26013-234">Escribir una partición de toohello de sistema de archivos mediante el uso de hello `mkfs` comando.</span><span class="sxs-lookup"><span data-stu-id="26013-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="26013-235">Montar el disco nuevo de Hola para que sea accesible en el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="26013-236">disco de Hello ahora puede obtenerse a través de hello *datadrive* punto de montaje, que se puede comprobar mediante la ejecución de hello `df -h` comando.</span><span class="sxs-lookup"><span data-stu-id="26013-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="26013-237">salida de Hello muestra una nueva unidad de hello montado en */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="26013-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="26013-238">tooensure que Hola unidad se vuelve a montar tras un reinicio, debe agregarse toohello */etcetera/fstab* archivo.</span><span class="sxs-lookup"><span data-stu-id="26013-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="26013-239">toodo por lo tanto, obtener Hola UUID del disco de hello con hello `blkid` utilidad.</span><span class="sxs-lookup"><span data-stu-id="26013-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="26013-240">salida de Hello muestra hello UUID de la unidad de hello, `/dev/sdc1` en este caso.</span><span class="sxs-lookup"><span data-stu-id="26013-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="26013-241">Agregar un toohello similar de línea después de toohello */etcetera/fstab* archivo.</span><span class="sxs-lookup"><span data-stu-id="26013-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="26013-242">Tenga en cuenta también que las barreras de escritura puede deshabilitarse mediante *barrier=0*; esta configuración puede mejorar el rendimiento del disco.</span><span class="sxs-lookup"><span data-stu-id="26013-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="26013-243">Ahora que hello disco se ha configurado, cierre la sesión de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="26013-244">Cambio del tamaño de disco de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="26013-244">Resize VM disk</span></span>

<span data-ttu-id="26013-245">Una vez que se ha implementado una máquina virtual, el disco del sistema operativo de Hola o los discos de datos adjunto se pueden aumentar de tamaño.</span><span class="sxs-lookup"><span data-stu-id="26013-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="26013-246">Aumentar tamaño de Hola de un disco resulta beneficioso cuando se necesita más espacio de almacenamiento o un mayor nivel de rendimiento (P10, P20, P30).</span><span class="sxs-lookup"><span data-stu-id="26013-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="26013-247">Cabe mencionar que no se puede reducir el tamaño de los discos.</span><span class="sxs-lookup"><span data-stu-id="26013-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="26013-248">Antes de aumentar el tamaño del disco, Hola Id. o nombre de disco de hello es necesario.</span><span class="sxs-lookup"><span data-stu-id="26013-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="26013-249">Hola de uso [lista de discos az](/cli/azure/vm/disk#list) tooreturn comando todos los discos en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="26013-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="26013-250">Tome nota del nombre de disco de Hola que desearía tooresize.</span><span class="sxs-lookup"><span data-stu-id="26013-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="26013-251">Hola VM también debe ser desasignado.</span><span class="sxs-lookup"><span data-stu-id="26013-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="26013-252">Hola de uso [cancelar la asignación de máquina virtual az]( /cli/azure/vm#deallocate) comando toostop y cancelar la asignación Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="26013-253">Hola de uso [actualización de disco az](/cli/azure/vm/disk#update) disco de comando tooresize Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="26013-254">Este ejemplo cambia el tamaño de un disco llamado *myDataDisk* too1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="26013-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="26013-255">Una vez completada la operación de cambio de tamaño de hello, inicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="26013-256">Si ha cambiado el tamaño Hola operativo disco del sistema, se expande automáticamente partición Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="26013-257">Si ha cambiado el tamaño de un disco de datos, cualquier partición actual necesita toobe expandir en el sistema operativo de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="26013-258">Captura de instantáneas de discos de Azure</span><span class="sxs-lookup"><span data-stu-id="26013-258">Snapshot Azure disks</span></span>

<span data-ttu-id="26013-259">Tomar una instantánea de disco, crea una copia de únicamente, en un momento lectura del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="26013-260">Instantáneas de máquina virtual de Azure son útiles para guardar rápidamente el estado de Hola de una máquina virtual antes de realizar cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="26013-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="26013-261">En caso de hello cambios de configuración hello demostrar toobe no deseada, estado de VM puede restaurarse con instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="26013-262">Cuando una máquina virtual tiene más de un disco, se toma una instantánea de cada disco independientemente de hello otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="26013-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="26013-263">Para realizar copias de seguridad coherente de aplicación, considere la posibilidad de detener Hola VM antes de tomar instantáneas de disco.</span><span class="sxs-lookup"><span data-stu-id="26013-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="26013-264">O bien, usar hello [servicio de copia de seguridad de Azure](/azure/backup/), lo que permite tooperform automatizada copias de seguridad mientras Hola VM se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="26013-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="26013-265">Creación de una instantánea</span><span class="sxs-lookup"><span data-stu-id="26013-265">Create snapshot</span></span>

<span data-ttu-id="26013-266">Antes de crear una instantánea de disco de máquina virtual, hello identificador o nombre de disco de hello es necesario.</span><span class="sxs-lookup"><span data-stu-id="26013-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="26013-267">Hola de uso [mostrar de la máquina virtual de az](https://docs.microsoft.com/en-us/cli/azure/vm#show) Id. de comando tooreturn Hola disco. En este ejemplo, Id. de disco de Hola se almacena en una variable para que se puede utilizar en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="26013-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="26013-268">Ahora que tiene el Id. de hello del disco de máquina virtual de hello, hello siguiente comando crea una instantánea del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="26013-269">Creación del disco a partir de la instantánea</span><span class="sxs-lookup"><span data-stu-id="26013-269">Create disk from snapshot</span></span>

<span data-ttu-id="26013-270">Esta instantánea, a continuación, se puede convertir en un disco, que puede ser la máquina virtual de toorecreate usado Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="26013-271">Restauración de la máquina virtual a partir de la instantánea</span><span class="sxs-lookup"><span data-stu-id="26013-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="26013-272">recuperación de máquina virtual toodemonstrate, máquina de virtual existente de eliminación Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="26013-273">Crear una nueva máquina virtual desde el disco de la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="26013-274">Reconexión de un disco de datos</span><span class="sxs-lookup"><span data-stu-id="26013-274">Reattach data disk</span></span>

<span data-ttu-id="26013-275">Todos los discos de datos necesitan máquina virtual de toohello de toobe volver a adjuntar.</span><span class="sxs-lookup"><span data-stu-id="26013-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="26013-276">Encontrar primero un nombre de disco de datos hello mediante hello [lista de discos az](https://docs.microsoft.com/cli/azure/disk#list) comando.</span><span class="sxs-lookup"><span data-stu-id="26013-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="26013-277">En este ejemplo lugares Hola nombre del disco de hello en una variable denominada *datadisk*, que se usa en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="26013-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="26013-278">Hola de uso [adjuntar el disco de vm az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco de comando tooattach Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="26013-279">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26013-279">Next steps</span></span>

<span data-ttu-id="26013-280">En este tutorial, ha aprendido sobre temas relacionados con los discos de máquina virtual; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="26013-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26013-281">Discos del SO y temporales</span><span class="sxs-lookup"><span data-stu-id="26013-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="26013-282">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="26013-282">Data disks</span></span>
> * <span data-ttu-id="26013-283">Discos Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="26013-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="26013-284">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="26013-284">Disk performance</span></span>
> * <span data-ttu-id="26013-285">Conectar y preparar los discos de datos</span><span class="sxs-lookup"><span data-stu-id="26013-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="26013-286">Cambiar el tamaño de los discos</span><span class="sxs-lookup"><span data-stu-id="26013-286">Resizing disks</span></span>
> * <span data-ttu-id="26013-287">Instantáneas de disco</span><span class="sxs-lookup"><span data-stu-id="26013-287">Disk snapshots</span></span>

<span data-ttu-id="26013-288">Avanzar toohello toolearn de tutorial siguiente acerca de cómo automatizar la configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26013-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26013-289">Automatización de la configuración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="26013-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
