---
title: "aaaMigrate un tooan VM clásico ARM VM de disco administrado | Documentos de Microsoft"
description: "Migrar una sola máquina virtual de Azure de implementación clásica de hello tooManaged discos en el modelo de implementación del Administrador de recursos de Hola de modelo."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="bbe36-103">Migrar manualmente un tooa clásico VM nueva ARM VM administrados de disco de hello VHD</span><span class="sxs-lookup"><span data-stu-id="bbe36-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="bbe36-104">En esta sección le ayuda a toomigrate las máquinas virtuales de Azure existente desde el modelo de implementación clásica de hello demasiado[discos administrados](managed-disks-overview.md) en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbe36-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="bbe36-105">Planear la migración de Hola de discos tooManaged</span><span class="sxs-lookup"><span data-stu-id="bbe36-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="bbe36-106">Esta sección le ayudará a mejor decisión de Hola de toomake en tipos de máquina virtual y disco.</span><span class="sxs-lookup"><span data-stu-id="bbe36-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="bbe36-107">Ubicación</span><span class="sxs-lookup"><span data-stu-id="bbe36-107">Location</span></span>

<span data-ttu-id="bbe36-108">Elija una ubicación donde Azure Managed Disks esté disponible.</span><span class="sxs-lookup"><span data-stu-id="bbe36-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="bbe36-109">Si va a migrar discos administrados de tooPremium, asegúrese también de que almacenamiento Premium está disponible en la región de Hola donde piensa toomigrate a.</span><span class="sxs-lookup"><span data-stu-id="bbe36-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="bbe36-110">Consulte [Servicios de Azure por región](https://azure.microsoft.com/regions/#services) para información actualizada sobre las ubicaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="bbe36-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="bbe36-111">Tamaños de VM</span><span class="sxs-lookup"><span data-stu-id="bbe36-111">VM sizes</span></span>

<span data-ttu-id="bbe36-112">Si va a migrar discos administrados de tooPremium, tiene tamaño de hello tooupdate de hello VM tooPremium tamaño con capacidad de almacenamiento disponible en región Hola donde se encuentra la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bbe36-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="bbe36-113">Revise los tamaños de máquinas virtuales de Hola que son capaces de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bbe36-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="bbe36-114">se enumeran las especificaciones de tamaño de máquina virtual de Azure de Hello en [tamaños de máquinas virtuales](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="bbe36-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="bbe36-115">Revise las características de rendimiento de Hola de máquinas virtuales que funcionen con el almacenamiento Premium y elija el tamaño más adecuado de hello máquina virtual que mejor se adapte a la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bbe36-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="bbe36-116">Asegúrese de que hay suficiente ancho de banda disponible en el tráfico de disco de máquina virtual toodrive Hola.</span><span class="sxs-lookup"><span data-stu-id="bbe36-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="bbe36-117">Tamaños de disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-117">Disk sizes</span></span>

<span data-ttu-id="bbe36-118">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="bbe36-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="bbe36-119">Hay siete tipos de Managed Disks Premium que se pueden usar con la máquina virtual y cada uno de ellos tiene sus límites específicos de rendimiento y E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="bbe36-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="bbe36-120">Tenga en cuenta estos límites al elegir Hola tipo de disco de Premium para la máquina virtual en función de las necesidades de saludo de la aplicación en cuanto a capacidad, rendimiento, escalabilidad, y la carga máxima.</span><span class="sxs-lookup"><span data-stu-id="bbe36-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="bbe36-121">Tipo de discos Premium</span><span class="sxs-lookup"><span data-stu-id="bbe36-121">Premium Disks Type</span></span>  | <span data-ttu-id="bbe36-122">P4</span><span class="sxs-lookup"><span data-stu-id="bbe36-122">P4</span></span>    | <span data-ttu-id="bbe36-123">P6</span><span class="sxs-lookup"><span data-stu-id="bbe36-123">P6</span></span>    | <span data-ttu-id="bbe36-124">P10</span><span class="sxs-lookup"><span data-stu-id="bbe36-124">P10</span></span>   | <span data-ttu-id="bbe36-125">P20</span><span class="sxs-lookup"><span data-stu-id="bbe36-125">P20</span></span>   | <span data-ttu-id="bbe36-126">P30</span><span class="sxs-lookup"><span data-stu-id="bbe36-126">P30</span></span>   | <span data-ttu-id="bbe36-127">P40</span><span class="sxs-lookup"><span data-stu-id="bbe36-127">P40</span></span>   | <span data-ttu-id="bbe36-128">P50</span><span class="sxs-lookup"><span data-stu-id="bbe36-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="bbe36-129">Tamaño del disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-129">Disk size</span></span>           | <span data-ttu-id="bbe36-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-130">128 GB</span></span>| <span data-ttu-id="bbe36-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-131">512 GB</span></span>| <span data-ttu-id="bbe36-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-132">128 GB</span></span>| <span data-ttu-id="bbe36-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-133">512 GB</span></span>            | <span data-ttu-id="bbe36-134">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="bbe36-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="bbe36-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="bbe36-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="bbe36-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="bbe36-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="bbe36-137">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-137">IOPS per disk</span></span>       | <span data-ttu-id="bbe36-138">120</span><span class="sxs-lookup"><span data-stu-id="bbe36-138">120</span></span>   | <span data-ttu-id="bbe36-139">240</span><span class="sxs-lookup"><span data-stu-id="bbe36-139">240</span></span>   | <span data-ttu-id="bbe36-140">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-140">500</span></span>   | <span data-ttu-id="bbe36-141">2300</span><span class="sxs-lookup"><span data-stu-id="bbe36-141">2300</span></span>              | <span data-ttu-id="bbe36-142">5000</span><span class="sxs-lookup"><span data-stu-id="bbe36-142">5000</span></span>              | <span data-ttu-id="bbe36-143">7500</span><span class="sxs-lookup"><span data-stu-id="bbe36-143">7500</span></span>              | <span data-ttu-id="bbe36-144">7500</span><span class="sxs-lookup"><span data-stu-id="bbe36-144">7500</span></span>              | 
| <span data-ttu-id="bbe36-145">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-145">Throughput per disk</span></span> | <span data-ttu-id="bbe36-146">25 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-146">25 MB per second</span></span>  | <span data-ttu-id="bbe36-147">50 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-147">50 MB per second</span></span>  | <span data-ttu-id="bbe36-148">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-148">100 MB per second</span></span> | <span data-ttu-id="bbe36-149">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-149">150 MB per second</span></span> | <span data-ttu-id="bbe36-150">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-150">200 MB per second</span></span> | <span data-ttu-id="bbe36-151">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-151">250 MB per second</span></span> | <span data-ttu-id="bbe36-152">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-152">250 MB per second</span></span> | 

<span data-ttu-id="bbe36-153">**Discos administrados Estándar**</span><span class="sxs-lookup"><span data-stu-id="bbe36-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="bbe36-154">Hay siete tipos de discos administrados Estándar que se pueden usar con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bbe36-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="bbe36-155">Cada uno de ellos tiene una capacidad distinta, pero los mismos límites de rendimiento y E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="bbe36-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="bbe36-156">Elija el tipo de Hola de discos administrados estándar según las necesidades de capacidad de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbe36-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="bbe36-157">Tipo de disco Estándar</span><span class="sxs-lookup"><span data-stu-id="bbe36-157">Standard Disk Type</span></span>  | <span data-ttu-id="bbe36-158">S4</span><span class="sxs-lookup"><span data-stu-id="bbe36-158">S4</span></span>               | <span data-ttu-id="bbe36-159">S6</span><span class="sxs-lookup"><span data-stu-id="bbe36-159">S6</span></span>               | <span data-ttu-id="bbe36-160">S10</span><span class="sxs-lookup"><span data-stu-id="bbe36-160">S10</span></span>              | <span data-ttu-id="bbe36-161">S20</span><span class="sxs-lookup"><span data-stu-id="bbe36-161">S20</span></span>              | <span data-ttu-id="bbe36-162">S30</span><span class="sxs-lookup"><span data-stu-id="bbe36-162">S30</span></span>              | <span data-ttu-id="bbe36-163">S40</span><span class="sxs-lookup"><span data-stu-id="bbe36-163">S40</span></span>              | <span data-ttu-id="bbe36-164">S50</span><span class="sxs-lookup"><span data-stu-id="bbe36-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="bbe36-165">Tamaño del disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-165">Disk size</span></span>           | <span data-ttu-id="bbe36-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-166">30 GB</span></span>            | <span data-ttu-id="bbe36-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-167">64 GB</span></span>            | <span data-ttu-id="bbe36-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-168">128 GB</span></span>           | <span data-ttu-id="bbe36-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="bbe36-169">512 GB</span></span>           | <span data-ttu-id="bbe36-170">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="bbe36-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="bbe36-171">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="bbe36-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="bbe36-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="bbe36-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="bbe36-173">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-173">IOPS per disk</span></span>       | <span data-ttu-id="bbe36-174">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-174">500</span></span>              | <span data-ttu-id="bbe36-175">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-175">500</span></span>              | <span data-ttu-id="bbe36-176">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-176">500</span></span>              | <span data-ttu-id="bbe36-177">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-177">500</span></span>              | <span data-ttu-id="bbe36-178">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-178">500</span></span>              | <span data-ttu-id="bbe36-179">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-179">500</span></span>             | <span data-ttu-id="bbe36-180">500</span><span class="sxs-lookup"><span data-stu-id="bbe36-180">500</span></span>              | 
| <span data-ttu-id="bbe36-181">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-181">Throughput per disk</span></span> | <span data-ttu-id="bbe36-182">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-182">60 MB per second</span></span> | <span data-ttu-id="bbe36-183">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-183">60 MB per second</span></span> | <span data-ttu-id="bbe36-184">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-184">60 MB per second</span></span> | <span data-ttu-id="bbe36-185">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-185">60 MB per second</span></span> | <span data-ttu-id="bbe36-186">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-186">60 MB per second</span></span> | <span data-ttu-id="bbe36-187">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-187">60 MB per second</span></span> | <span data-ttu-id="bbe36-188">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="bbe36-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="bbe36-189">Directiva de almacenamiento en caché de disco</span><span class="sxs-lookup"><span data-stu-id="bbe36-189">Disk caching policy</span></span> 

<span data-ttu-id="bbe36-190">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="bbe36-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="bbe36-191">De forma predeterminada, es la directiva de caché de disco *de sólo lectura* de Hola a todos los discos de datos Premium, y *lectura y escritura* para el disco del sistema operativo Hola Premium asocia toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bbe36-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="bbe36-192">Esta opción de configuración se recomienda tooachieve Hola un rendimiento óptimo para IOs la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbe36-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="bbe36-193">Para discos de datos de solo escritura o de gran cantidad de escritura (por ejemplo, archivos de registro de SQL Server), deshabilite el almacenamiento en caché de disco para lograr un mejor rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbe36-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="bbe36-194">Precios</span><span class="sxs-lookup"><span data-stu-id="bbe36-194">Pricing</span></span>

<span data-ttu-id="bbe36-195">Hola de revisión [precios de discos administrados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="bbe36-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="bbe36-196">Precios de discos administrados de Premium están el mismo que Hola los discos Premium no administrado.</span><span class="sxs-lookup"><span data-stu-id="bbe36-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="bbe36-197">Sin embargo, los precios de Managed Disks Estándar son distintos a los de los Unmanaged Disks Estándar.</span><span class="sxs-lookup"><span data-stu-id="bbe36-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="bbe36-198">Lista de comprobación</span><span class="sxs-lookup"><span data-stu-id="bbe36-198">Checklist</span></span>

1.  <span data-ttu-id="bbe36-199">Si va a migrar discos administrados de tooPremium, asegúrese de que está disponible en la región de Hola que se va a migrar a.</span><span class="sxs-lookup"><span data-stu-id="bbe36-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="bbe36-200">Decidir la serie de hello nuevas máquinas virtuales que va a usar.</span><span class="sxs-lookup"><span data-stu-id="bbe36-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="bbe36-201">Debe ser un sistema de almacenamiento Premium capaz si va a migrar discos administrados de tooPremium.</span><span class="sxs-lookup"><span data-stu-id="bbe36-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="bbe36-202">Decidir Hola VM tamaño exacto que va a utilizar que están disponibles en la región de Hola que se va a migrar a.</span><span class="sxs-lookup"><span data-stu-id="bbe36-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="bbe36-203">Tamaño de máquina virtual debe toobe número de hello toosupport lo suficientemente grande como de los discos de datos que tiene.</span><span class="sxs-lookup"><span data-stu-id="bbe36-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="bbe36-204">Por ejemplo, si tiene cuatro discos de datos, Hola VM debe tener dos o más núcleos.</span><span class="sxs-lookup"><span data-stu-id="bbe36-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="bbe36-205">Considere también las necesidades de potencia de procesamiento, memoria y ancho de banda de red.</span><span class="sxs-lookup"><span data-stu-id="bbe36-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="bbe36-206">Tener detalles VM actuales de hello útiles, incluidas las listas de Hola de discos y los blobs de disco duro virtual correspondientes.</span><span class="sxs-lookup"><span data-stu-id="bbe36-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="bbe36-207">Prepare la aplicación para el tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="bbe36-207">Prepare your application for downtime.</span></span> <span data-ttu-id="bbe36-208">toodo una migración limpia, que toostop todo el procesamiento de hello en hello actual sistema.</span><span class="sxs-lookup"><span data-stu-id="bbe36-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="bbe36-209">Solo entonces puede obtenerlo tooconsistent estado en el que puede migrar toohello nueva plataforma.</span><span class="sxs-lookup"><span data-stu-id="bbe36-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="bbe36-210">Duración del tiempo de inactividad depende de la cantidad de Hola de los datos de hello discos toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bbe36-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="bbe36-211">Migrar Hola VM</span><span class="sxs-lookup"><span data-stu-id="bbe36-211">Migrate hello VM</span></span>

<span data-ttu-id="bbe36-212">Prepare la aplicación para el tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="bbe36-212">Prepare your application for downtime.</span></span> <span data-ttu-id="bbe36-213">toodo una migración limpia, que toostop todo el procesamiento de hello en hello actual sistema.</span><span class="sxs-lookup"><span data-stu-id="bbe36-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="bbe36-214">Solo entonces puede obtenerlo tooconsistent estado en el que puede migrar toohello nueva plataforma.</span><span class="sxs-lookup"><span data-stu-id="bbe36-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="bbe36-215">Duración del tiempo de inactividad depende cantidad Hola de los datos de hello discos toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bbe36-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="bbe36-216">En primer lugar, establezca los parámetros comunes de hello:</span><span class="sxs-lookup"><span data-stu-id="bbe36-216">First, set hello common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="bbe36-217">Crear un disco de sistema operativo administrado utilizando Hola VHD de hello VM clásico.</span><span class="sxs-lookup"><span data-stu-id="bbe36-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="bbe36-218">Asegúrese de que haya proporcionado Hola completar URI de hello parámetro toohello $osVhdUri de disco duro virtual del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bbe36-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="bbe36-219">Además, escriba **-AccountType** como **PremiumLRS** o **StandardLRS** según el tipo de discos al que migra (Premium o Estándar).</span><span class="sxs-lookup"><span data-stu-id="bbe36-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="bbe36-220">Adjuntar Hola SO disco toohello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bbe36-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="bbe36-221">Crear un disco de datos administrados desde el archivo de disco duro virtual de datos de hello y agregar toohello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bbe36-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="bbe36-222">Crear nueva máquina virtual de Hola estableciendo pública IP, la red Virtual y la NIC.</span><span class="sxs-lookup"><span data-stu-id="bbe36-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="bbe36-223">Puede haber pasos adicionales necesarios toosupport la aplicación que no es estarán sujetos a esta guía.</span><span class="sxs-lookup"><span data-stu-id="bbe36-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bbe36-224">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbe36-224">Next steps</span></span>

- <span data-ttu-id="bbe36-225">Conectar la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="bbe36-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="bbe36-226">Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bbe36-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

