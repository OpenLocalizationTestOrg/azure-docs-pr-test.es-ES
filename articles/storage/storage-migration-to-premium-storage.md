---
title: "máquinas virtuales de aaaMigrating tooAzure almacenamiento Premium | Documentos de Microsoft"
description: "Migre su tooAzure de máquinas virtuales existente almacenamiento Premium. El Almacenamiento premium le ofrece compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo con un uso intensivo de E/S, que se ejecutan en máquinas virtuales de Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="9f622-104">Migrar tooAzure almacenamiento Premium (discos no administrada)</span><span class="sxs-lookup"><span data-stu-id="9f622-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="9f622-105">Este artículo describe cómo toomigrate una máquina virtual que utiliza discos estándar no administrado tooa máquina virtual que usa no administrada de discos premium.</span><span class="sxs-lookup"><span data-stu-id="9f622-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="9f622-106">Se recomienda utilizar discos de Azure administrados para nuevas máquinas virtuales y que convierta los discos de toomanaged anterior de discos no administrado.</span><span class="sxs-lookup"><span data-stu-id="9f622-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="9f622-107">Administrar cuentas de almacenamiento subyacentes de discos identificador hello por lo que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="9f622-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="9f622-108">Para obtener más información, consulte [Managed Disks Overview](storage-managed-disks-overview.md) (Información general sobre Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="9f622-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="9f622-109">El Almacenamiento premium de Azure le ofrece soporte de disco de alto rendimiento y latencia baja para máquinas virtuales con cargas de trabajo intensivas de E/S.</span><span class="sxs-lookup"><span data-stu-id="9f622-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="9f622-110">Puede sacar partido de velocidad de Hola y el rendimiento de estos discos al migrar tooAzure discos de máquina virtual de su aplicación almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="9f622-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="9f622-111">Hola de esta guía sirve toohelp nuevos usuarios de almacenamiento de Azure Premium mejor preparación toomake una transición sin problemas desde su tooPremium de sistema almacenamiento actual.</span><span class="sxs-lookup"><span data-stu-id="9f622-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="9f622-112">Guía de Hello direcciones tres componentes clave de hello en este proceso:</span><span class="sxs-lookup"><span data-stu-id="9f622-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="9f622-113">Planear la migración de hello tooPremium almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="9f622-114">Preparar y discos duros virtuales (VHD) de copia tooPremium almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="9f622-115">Creación de una máquina virtual de Azure mediante Premium Storage</span><span class="sxs-lookup"><span data-stu-id="9f622-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="9f622-116">Puede migrar las máquinas virtuales de otra tooAzure plataformas almacenamiento Premium o migrar máquinas virtuales de Azure existente de almacenamiento estándar tooPremium almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="9f622-117">En esta guía se describen los pasos para ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="9f622-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="9f622-118">Siga los pasos de hello especificados en sección relevantes de hello según el escenario.</span><span class="sxs-lookup"><span data-stu-id="9f622-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="9f622-119">Encontrará una introducción a las características y los precios de Premium Storage en [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9f622-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="9f622-120">Se recomienda migrar cualquier disco de máquina virtual que requieren alta IOPS tooAzure almacenamiento Premium para mejorar el rendimiento de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9f622-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="9f622-121">Si el disco no requiere un número elevado de operaciones de entrada/salida por segundo, puede limitar los costos mediante el mantenimiento del almacenamiento estándar, que almacena los datos de disco de máquina virtual en unidades de disco duro (HDD) en lugar de SSD.</span><span class="sxs-lookup"><span data-stu-id="9f622-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="9f622-122">Completar el proceso de migración de hello en su totalidad puede requerir alguna acción adicional antes y después de los pasos de hello proporcionados en esta guía.</span><span class="sxs-lookup"><span data-stu-id="9f622-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="9f622-123">Algunos ejemplos son la configuración de redes virtuales o los puntos de conexión o de realizar cambios de código dentro de la aplicación hello propio y lo que puede requerir algún tiempo de inactividad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f622-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="9f622-124">Estas acciones son tooeach único de la aplicación y se debe completar junto con los pasos de hello proporcionadas en este tooPremium de transición completa de hello guía toomake máxima uniformidad posible de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="9f622-125"><a name="plan-the-migration-to-premium-storage"></a>Planear la migración de hello tooPremium almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="9f622-126">En esta sección se asegura de que está listo toofollow pasos de migración de hello en este artículo y le ayuda a mejor decisión de Hola de toomake en tipos de máquina virtual y disco.</span><span class="sxs-lookup"><span data-stu-id="9f622-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9f622-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f622-127">Prerequisites</span></span>
* <span data-ttu-id="9f622-128">Necesitará una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-128">You will need an Azure subscription.</span></span> <span data-ttu-id="9f622-129">Si no tiene ninguna, puede crear una suscripción de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/) de un mes o visitar la página [Precios de Azure](https://azure.microsoft.com/pricing/) para conocer más opciones.</span><span class="sxs-lookup"><span data-stu-id="9f622-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="9f622-130">tooexecute cmdlets de PowerShell, deberá módulo de Microsoft Azure PowerShell Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="9f622-131">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para hello instalar punto e instrucciones de instalación.</span><span class="sxs-lookup"><span data-stu-id="9f622-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="9f622-132">Cuando planee toouse Azure VM que se ejecutan en almacenamiento Premium, debe toouse Hola máquinas virtuales con capacidad de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="9f622-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="9f622-133">Puede usar discos de almacenamiento Estándar y Premium Storage con las máquinas virtuales compatibles con Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="9f622-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="9f622-134">Los discos de almacenamiento Premium estarán disponibles con más tipos VM en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="9f622-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="9f622-135">Para obtener más información sobre todos los tamaños y tipos de disco de máquina virtual de Azure disponibles, consulte [Tamaños de máquinas virtuales](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [Tamaños de Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="9f622-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="9f622-136">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="9f622-136">Considerations</span></span>
<span data-ttu-id="9f622-137">Una VM de Azure admite la asociación varios discos de almacenamiento Premium para que las aplicaciones pueden tener hasta too256 TB de almacenamiento por máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="9f622-138">Con el Almacenamiento premium, las aplicaciones pueden tener hasta 80.000 E/S por segundo (operaciones de entrada/salida por segundo) por máquina virtual, así como un rendimiento del disco de 2.000 MB por segundo por máquina virtual, con latencias extremadamente bajas para operaciones de lectura.</span><span class="sxs-lookup"><span data-stu-id="9f622-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="9f622-139">Dispone de opciones en varias máquinas virtuales y discos.</span><span class="sxs-lookup"><span data-stu-id="9f622-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="9f622-140">Esta sección es toohelp toofind una opción que mejor se adapte a la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9f622-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="9f622-141">Tamaños de VM</span><span class="sxs-lookup"><span data-stu-id="9f622-141">VM sizes</span></span>
<span data-ttu-id="9f622-142">se enumeran las especificaciones de tamaño de máquina virtual de Azure de Hello en [tamaños de máquinas virtuales](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f622-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9f622-143">Revise las características de rendimiento de Hola de máquinas virtuales que funcionen con el almacenamiento Premium y elija el tamaño más adecuado de hello máquina virtual que mejor se adapte a la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9f622-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="9f622-144">Asegúrese de que hay suficiente ancho de banda disponible en el tráfico de disco de máquina virtual toodrive Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="9f622-145">Tamaños de disco</span><span class="sxs-lookup"><span data-stu-id="9f622-145">Disk sizes</span></span>
<span data-ttu-id="9f622-146">Hay tres tipos de discos que se pueden usar con las máquinas virtuales y cada uno de ellos tiene sus límites específicos de rendimiento y E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="9f622-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="9f622-147">Tenga en cuenta estos límites al elegir tipo de disco de hello para la máquina virtual en función de necesidades de saludo de la aplicación en cuanto a capacidad, rendimiento, escalabilidad, y la carga máxima.</span><span class="sxs-lookup"><span data-stu-id="9f622-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="9f622-148">Tipo de discos Premium</span><span class="sxs-lookup"><span data-stu-id="9f622-148">Premium Disks Type</span></span>  | <span data-ttu-id="9f622-149">P10</span><span class="sxs-lookup"><span data-stu-id="9f622-149">P10</span></span>   | <span data-ttu-id="9f622-150">P20</span><span class="sxs-lookup"><span data-stu-id="9f622-150">P20</span></span>   | <span data-ttu-id="9f622-151">P30</span><span class="sxs-lookup"><span data-stu-id="9f622-151">P30</span></span>            | <span data-ttu-id="9f622-152">P40</span><span class="sxs-lookup"><span data-stu-id="9f622-152">P40</span></span>            | <span data-ttu-id="9f622-153">P50</span><span class="sxs-lookup"><span data-stu-id="9f622-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="9f622-154">Tamaño del disco</span><span class="sxs-lookup"><span data-stu-id="9f622-154">Disk size</span></span>           | <span data-ttu-id="9f622-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="9f622-155">128 GB</span></span>| <span data-ttu-id="9f622-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="9f622-156">512 GB</span></span>| <span data-ttu-id="9f622-157">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="9f622-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="9f622-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="9f622-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="9f622-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="9f622-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="9f622-160">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="9f622-160">IOPS per disk</span></span>       | <span data-ttu-id="9f622-161">500</span><span class="sxs-lookup"><span data-stu-id="9f622-161">500</span></span>   | <span data-ttu-id="9f622-162">2300</span><span class="sxs-lookup"><span data-stu-id="9f622-162">2300</span></span>  | <span data-ttu-id="9f622-163">5000</span><span class="sxs-lookup"><span data-stu-id="9f622-163">5000</span></span>           | <span data-ttu-id="9f622-164">7500</span><span class="sxs-lookup"><span data-stu-id="9f622-164">7500</span></span>           | <span data-ttu-id="9f622-165">7500</span><span class="sxs-lookup"><span data-stu-id="9f622-165">7500</span></span>           | 
| <span data-ttu-id="9f622-166">Rendimiento de disco</span><span class="sxs-lookup"><span data-stu-id="9f622-166">Throughput per disk</span></span> | <span data-ttu-id="9f622-167">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="9f622-167">100 MB per second</span></span> | <span data-ttu-id="9f622-168">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="9f622-168">150 MB per second</span></span> | <span data-ttu-id="9f622-169">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="9f622-169">200 MB per second</span></span> | <span data-ttu-id="9f622-170">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="9f622-170">250 MB per second</span></span> | <span data-ttu-id="9f622-171">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="9f622-171">250 MB per second</span></span> |

<span data-ttu-id="9f622-172">Dependiendo de la carga de trabajo, decida si son necesarios más discos de datos para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="9f622-173">Puede adjuntar varios datos persistentes discos tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="9f622-174">Si es necesario, puede crear bandas en capacidad de hello discos tooincrease Hola y el rendimiento de volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="9f622-175">(Consulte qué es el seccionamiento de discos [aquí](storage-premium-storage-performance.md#disk-striping)). Si secciona discos de datos de Premium Storage mediante [Espacios de almacenamiento][4], tendrá que configurarlos con una columna por cada disco que use.</span><span class="sxs-lookup"><span data-stu-id="9f622-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="9f622-176">En caso contrario, hello general rendimiento del volumen de hello particionado puede ser menor del esperado debido toouneven distribución del tráfico en varios discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="9f622-177">Para máquinas virtuales Linux pueden usar hello *mdadm* tooachieve utilidad Hola igual.</span><span class="sxs-lookup"><span data-stu-id="9f622-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="9f622-178">Vea el artículo [Configuración del software RAID en Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información.</span><span class="sxs-lookup"><span data-stu-id="9f622-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="9f622-179">Objetivos de escalabilidad de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-179">Storage account scalability targets</span></span>
<span data-ttu-id="9f622-180">Cuentas de almacenamiento Premium tienen Hola siguientes destinos de escalabilidad en suma toohello [objetivos de rendimiento y escalabilidad de almacenamiento de Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="9f622-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="9f622-181">Si los requisitos de su aplicación superan los objetivos de escalabilidad de Hola de una única cuenta de almacenamiento, compilar su aplicación toouse varias cuentas de almacenamiento y dividir los datos en esas cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="9f622-182">Capacidad total de la cuenta</span><span class="sxs-lookup"><span data-stu-id="9f622-182">Total Account Capacity</span></span> | <span data-ttu-id="9f622-183">Ancho de banda total de una cuenta de almacenamiento con redundancia local</span><span class="sxs-lookup"><span data-stu-id="9f622-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f622-184">Capacidad de disco: 35 TB</span><span class="sxs-lookup"><span data-stu-id="9f622-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="9f622-185">Capacidad de instantánea: 10 TB</span><span class="sxs-lookup"><span data-stu-id="9f622-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="9f622-186">Seguridad too50 gigabits por segundo entrante + saliente</span><span class="sxs-lookup"><span data-stu-id="9f622-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="9f622-187">Hola a para obtener más información acerca de las especificaciones de almacenamiento Premium, visite [objetivos de escalabilidad y rendimiento al usar almacenamiento Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="9f622-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="9f622-188">Directiva de almacenamiento en caché de disco</span><span class="sxs-lookup"><span data-stu-id="9f622-188">Disk caching policy</span></span>
<span data-ttu-id="9f622-189">De forma predeterminada, es la directiva de caché de disco *de sólo lectura* de Hola a todos los discos de datos Premium, y *lectura y escritura* para el disco del sistema operativo Hola Premium asocia toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="9f622-190">Esta opción de configuración se recomienda tooachieve Hola un rendimiento óptimo para IOs la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f622-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="9f622-191">Para discos de datos de solo escritura o de gran cantidad de escritura (por ejemplo, archivos de registro de SQL Server), deshabilite el almacenamiento en caché de disco para lograr un mejor rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f622-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="9f622-192">configuración de la caché de Hola para discos de datos existentes se puede actualizar con [Portal de Azure](https://portal.azure.com) o hello *- HostCaching* parámetro de hello *Set-AzureDataDisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f622-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="9f622-193">Ubicación</span><span class="sxs-lookup"><span data-stu-id="9f622-193">Location</span></span>
<span data-ttu-id="9f622-194">Elija una ubicación donde el Almacenamiento premium de Azure esté disponible.</span><span class="sxs-lookup"><span data-stu-id="9f622-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="9f622-195">Consulte [Servicios de Azure por región](https://azure.microsoft.com/regions/#services) para obtener información actualizada sobre las ubicaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9f622-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="9f622-196">Máquinas virtuales ubicadas en hello misma región como lo Hola cuenta de almacenamiento que almacenes Hola discos para hello VM le proporcionará un rendimiento mucho mejor que si están en regiones independientes.</span><span class="sxs-lookup"><span data-stu-id="9f622-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="9f622-197">Otras opciones de configuración de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="9f622-198">Al crear una máquina virtual de Azure, estará más frecuentes tooconfigure ciertas opciones de configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="9f622-199">Recuerde que algunos valores son fijos para duración de Hola de Hola de máquina virtual, mientras que puede modificar o agregar otros.</span><span class="sxs-lookup"><span data-stu-id="9f622-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="9f622-200">Revise estos valores de configuración de máquina virtual de Azure y asegúrese de que se trata configurado adecuadamente toomatch sus requisitos de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9f622-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="9f622-201">Optimización</span><span class="sxs-lookup"><span data-stu-id="9f622-201">Optimization</span></span>
<span data-ttu-id="9f622-202">En [Azure Premium Storage: diseño de alto rendimiento](storage-premium-storage-performance.md) se proporcionan instrucciones para crear aplicaciones de alto rendimiento con Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="9f622-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="9f622-203">Puede seguir directrices de hello combinadas con mejor tootechnologies de aplicable de prácticas rendimiento que usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f622-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="9f622-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparar y copie tooPremium almacenamiento de discos duros virtuales (VHD)</span><span class="sxs-lookup"><span data-stu-id="9f622-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="9f622-205">Hola pasos de la sección proporciona instrucciones para preparar los discos duros virtuales de la máquina virtual y copiar discos duros virtuales tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="9f622-206">Escenario 1: "Estoy migrando tooAzure de máquinas virtuales de Azure existente almacenamiento Premium."</span><span class="sxs-lookup"><span data-stu-id="9f622-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="9f622-207">Escenario 2: "Estoy migrar varias VM desde otro tooAzure plataformas almacenamiento Premium."</span><span class="sxs-lookup"><span data-stu-id="9f622-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="9f622-208">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f622-208">Prerequisites</span></span>
<span data-ttu-id="9f622-209">Hola tooprepare discos duros virtuales para la migración, necesitará:</span><span class="sxs-lookup"><span data-stu-id="9f622-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="9f622-210">Una suscripción de Azure, una cuenta de almacenamiento y un contenedor en el que el almacenamiento de la cuenta toowhich puede copiar el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="9f622-211">Tenga en cuenta que cuenta de almacenamiento de destino de hello puede ser una cuenta estándar o Premium almacenamiento según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="9f622-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="9f622-212">Hola de toogeneralize de herramienta VHD si tiene previsto toocreate varias instancias VM del mismo.</span><span class="sxs-lookup"><span data-stu-id="9f622-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="9f622-213">Por ejemplo, sysprep para Windows o virt sysprep para Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9f622-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="9f622-214">Una herramienta tooupload Hola VHD archivo toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="9f622-215">Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md) o usar un [el Explorador de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f622-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="9f622-216">Esta guía describe copiar el disco duro virtual mediante la herramienta de AzCopy Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="9f622-217">Si elige la opción de copia sincrónica con AzCopy, para un rendimiento óptimo, copie el disco duro virtual mediante la ejecución de una de estas herramientas desde una máquina virtual de Azure que se encuentra en hello misma región que la cuenta de almacenamiento de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="9f622-218">Si está copiando un VHD de una máquina virtual de Azure en una región distinta, el rendimiento puede ser más lento.</span><span class="sxs-lookup"><span data-stu-id="9f622-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="9f622-219">Para copiar una gran cantidad de datos a través de ancho de banda limitado, considere la posibilidad de [con hello importación/exportación de Azure servicio tootransfer datos tooBlob almacenamiento](storage-import-export-service.md); Esto le permite tootransfer tooan Azure las unidades de los datos por disco duro de envío Centro de datos.</span><span class="sxs-lookup"><span data-stu-id="9f622-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="9f622-220">Puede usar Hola importación/exportación de Azure servicio toocopy datos tooa cuenta de almacenamiento estándar solo.</span><span class="sxs-lookup"><span data-stu-id="9f622-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="9f622-221">Una vez que los datos de hello están en su cuenta de almacenamiento estándar, puede usar cualquier hello [API de copia de Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) o cuenta de almacenamiento premium de AzCopy tootransfer Hola datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="9f622-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="9f622-222">Tenga en cuenta que Microsoft Azure solo admite archivos VHD de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="9f622-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="9f622-223">No se admiten archivos VHDX ni discos duros virtuales dinámicos.</span><span class="sxs-lookup"><span data-stu-id="9f622-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="9f622-224">Si tiene un disco duro virtual dinámico, se puede convertir mediante Hola de tamaño de toofixed [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f622-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="9f622-225"><a name="scenario1"></a>Escenario 1: "Estoy migrando tooAzure de máquinas virtuales de Azure existente almacenamiento Premium."</span><span class="sxs-lookup"><span data-stu-id="9f622-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="9f622-226">Si va a migrar existente máquinas virtuales de Azure, Hola de detención de máquina virtual, preparar los discos duros virtuales por tipo de Hola de disco duro virtual que desee y, a continuación, copie Hola VHD con AzCopy o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f622-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="9f622-227">Hola VM debe toobe completamente hacia abajo toomigrate un estado limpio.</span><span class="sxs-lookup"><span data-stu-id="9f622-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="9f622-228">Habrá un tiempo de inactividad hasta que se complete la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="9f622-229">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="9f622-229">Step 1.</span></span> <span data-ttu-id="9f622-230">Preparar los VHD para la migración</span><span class="sxs-lookup"><span data-stu-id="9f622-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="9f622-231">Si va a migrar tooPremium de máquinas virtuales de Azure existente almacenamiento, puede ser el disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="9f622-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="9f622-232">Una imagen del sistema operativo generalizado</span><span class="sxs-lookup"><span data-stu-id="9f622-232">A generalized operating system image</span></span>
* <span data-ttu-id="9f622-233">Un disco del sistema operativo exclusivo</span><span class="sxs-lookup"><span data-stu-id="9f622-233">A unique operating system disk</span></span>
* <span data-ttu-id="9f622-234">Un disco de datos</span><span class="sxs-lookup"><span data-stu-id="9f622-234">A data disk</span></span>

<span data-ttu-id="9f622-235">A continuación se describen estos tres escenarios para preparar un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="9f622-236">Usar un toocreate de disco duro virtual de sistema operativo generalizado varias instancias de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9f622-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="9f622-237">Si va a cargar un disco duro virtual que será usado toocreate varias instancias de máquina virtual de Azure genéricas, en primer lugar debe generalizar VHD con una utilidad de sysprep.</span><span class="sxs-lookup"><span data-stu-id="9f622-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="9f622-238">Esto aplica tooa disco duro virtual que es local o en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="9f622-239">Sysprep quita cualquier información específica de la máquina de hello VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f622-240">Realice una instantánea o copia de seguridad de la máquina virtual antes de generalizarla.</span><span class="sxs-lookup"><span data-stu-id="9f622-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="9f622-241">Ejecutar sysprep se detenga y se cancela la asignación de instancia de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="9f622-242">Siga estos pasos toosysprep un VHD de sistema operativo de Windows.</span><span class="sxs-lookup"><span data-stu-id="9f622-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="9f622-243">Tenga en cuenta que ejecuta el comando Sysprep de hello, deberá tooshut hacia abajo de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="9f622-244">Para obtener más información sobre Sysprep, consulte [Introducción a Sysprep](http://technet.microsoft.com/library/hh825209.aspx) o [Referencia técnica de Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f622-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="9f622-245">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="9f622-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="9f622-246">Escriba Hola después tooopen comando Sysprep:</span><span class="sxs-lookup"><span data-stu-id="9f622-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="9f622-247">Hola herramienta de preparación del sistema, seleccione sistema Out-of-Box experiencia configuración rápida (OOBE), seleccione Hola generalizar casilla, seleccione **apagado**y, a continuación, haga clic en **Aceptar**, tal y como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="9f622-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="9f622-248">Sysprep se generalizar el sistema operativo de Hola y apagar el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="9f622-249">Para una VM Ubuntu, use sysprep virt tooachieve Hola igual.</span><span class="sxs-lookup"><span data-stu-id="9f622-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="9f622-250">Vea [sysprep virt](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) para más información.</span><span class="sxs-lookup"><span data-stu-id="9f622-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="9f622-251">Vea también algunos de código abierto de hello [software de aprovisionamiento del servidor Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) para otros sistemas operativos Linux.</span><span class="sxs-lookup"><span data-stu-id="9f622-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="9f622-252">Usar un único toocreate de sistema operativo VHD una única instancia de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9f622-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="9f622-253">Si tiene una aplicación que se ejecuta en hello VM que requiere datos específicos de la máquina de hello, no generalice Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="9f622-254">Un disco duro virtual generalizado no puede ser toocreate usa una única instancia de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="9f622-255">Por ejemplo, si tiene el controlador de dominio en el disco duro virtual, ejecutar sysprep lo anulará como controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="9f622-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="9f622-256">Revisar aplicaciones Hola que se ejecutan en la máquina virtual y Hola el impacto de ejecutar sysprep en ellos antes de generalizar Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="9f622-257">Registro de VHD de disco de datos</span><span class="sxs-lookup"><span data-stu-id="9f622-257">Register data disk VHD</span></span>
<span data-ttu-id="9f622-258">Si tiene discos de datos en Azure toobe migrar, debe procurar seguro de máquinas virtuales de Hola que utilizan estos datos se apagan discos.</span><span class="sxs-lookup"><span data-stu-id="9f622-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="9f622-259">Siga los pasos de Hola se describe a continuación toocopy VHD tooAzure almacenamiento Premium y registrarlo como un disco de datos aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="9f622-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="9f622-260">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="9f622-260">Step 2.</span></span> <span data-ttu-id="9f622-261">Crear destino de hello para el disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="9f622-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="9f622-262">Cree una cuenta de almacenamiento para mantener los discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f622-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="9f622-263">Considere la posibilidad de hello siguientes puntos cuando planee dónde toostore los discos duros virtuales:</span><span class="sxs-lookup"><span data-stu-id="9f622-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="9f622-264">destino de Hello cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="9f622-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="9f622-265">ubicación Hello de la cuenta de almacenamiento debe ser igual que el almacenamiento Premium compatible con máquinas virtuales de Azure que creará en la fase final de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="9f622-266">Podría copiar tooa nueva cuenta de almacenamiento u Hola de toouse plan misma cuenta de almacenamiento según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="9f622-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="9f622-267">Copie y guarde la clave de cuenta de almacenamiento de Hola de cuenta de almacenamiento de destino de hello para la fase siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="9f622-268">En los discos de datos, puede elegir tookeep algunos discos de datos en una cuenta de almacenamiento estándar (por ejemplo, los discos que tienen almacenamiento mejor refrigeración), pero se recomienda encarecidamente que mover todos los datos de almacenamiento de información premium toouse de carga de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="9f622-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="9f622-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Paso 3.</span><span class="sxs-lookup"><span data-stu-id="9f622-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="9f622-270">Copiar un VHD con AzCopy o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f622-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="9f622-271">Necesitará toofind la ruta de acceso del contenedor y la cuenta tooprocess clave cualquiera de estas dos opciones de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="9f622-272">Tanto una como otra pueden encontrarse en **Azure Portal** > **Storage**.</span><span class="sxs-lookup"><span data-stu-id="9f622-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="9f622-273">dirección URL del contenedor Hola será como "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="9f622-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="9f622-274">Opción 1: Copiar un VHD con AzCopy (copia asincrónica)</span><span class="sxs-lookup"><span data-stu-id="9f622-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="9f622-275">AzCopy puede cargar fácilmente Hola VHD a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="9f622-276">Función tamaño Hola de hello discos duros virtuales, esto puede tardar tiempo.</span><span class="sxs-lookup"><span data-stu-id="9f622-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="9f622-277">Recuerde límites de entrada/salida de la cuenta de almacenamiento de toocheck hello cuando utilice esta opción.</span><span class="sxs-lookup"><span data-stu-id="9f622-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="9f622-278">Vea [Objetivos de escalabilidad y rendimiento del almacenamiento en Azure](storage-scalability-targets.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="9f622-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="9f622-279">Descargue e instale AzCopy desde aquí: [versión más reciente de AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="9f622-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="9f622-280">Abra PowerShell de Azure y carpeta toohello vaya donde está instalado AzCopy.</span><span class="sxs-lookup"><span data-stu-id="9f622-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="9f622-281">Archivo de disco duro virtual de hello toocopy de "Origen" de comando siguiente de Hola de uso demasiado "Destino".</span><span class="sxs-lookup"><span data-stu-id="9f622-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="9f622-282">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f622-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="9f622-283">Estas son las descripciones de parámetros de hello utilizados en hello AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="9f622-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="9f622-284">**El código fuente:  *&lt;origen&gt;:***  ubicación de carpeta de Hola o dirección URL del contenedor de almacenamiento que contiene Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="9f622-285">**/ SourceKey:  *&lt;clave de la cuenta de origen&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="9f622-286">**/ Dest:  *&lt;destino&gt;:***  toocopy de dirección URL del contenedor de almacenamiento Hola disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="9f622-287">**/ DestKey:  *&lt;clave de cuenta dest&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="9f622-288">**/ Patrón:  *&lt;nombre de archivo&gt;:***  especificar el nombre de archivo de Hola de hello toocopy de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="9f622-289">Para obtener más información sobre el uso de AzCopy herramienta, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="9f622-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="9f622-290">Opción 2: Copiar un VHD con PowerShell (copia sincronizada)</span><span class="sxs-lookup"><span data-stu-id="9f622-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="9f622-291">También puede copiar el archivo VHD de hello mediante el cmdlet de PowerShell de hello AzureStorageBlobCopy de inicio.</span><span class="sxs-lookup"><span data-stu-id="9f622-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="9f622-292">Usar hello siguiente comando de PowerShell de Azure toocopy disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="9f622-293">Reemplazar valores de hello en <> con los valores correspondientes de la cuenta de almacenamiento de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="9f622-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="9f622-294">toouse este comando, debe tener un contenedor denominado discos duros virtuales en la cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="9f622-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="9f622-295">Si no existe el contenedor de hello, crear uno antes de ejecutar el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="9f622-296">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f622-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="9f622-297"><a name="scenario2"></a>Escenario 2: "Estoy migrar varias VM desde otro tooAzure plataformas almacenamiento Premium."</span><span class="sxs-lookup"><span data-stu-id="9f622-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="9f622-298">Si va a migrar el disco duro virtual de almacenamiento en nube que no Azure tooAzure, primero debe exportar el directorio local de hello VHD tooa.</span><span class="sxs-lookup"><span data-stu-id="9f622-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="9f622-299">Tiene la ruta de acceso de origen completa de hello del directorio local Hola donde se almacena los VHD práctica y, a continuación, utilizando tooupload AzCopy se tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="9f622-300">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="9f622-300">Step 1.</span></span> <span data-ttu-id="9f622-301">Exportar el directorio local de disco duro virtual tooa</span><span class="sxs-lookup"><span data-stu-id="9f622-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="9f622-302">Copia de un VHD desde AWS</span><span class="sxs-lookup"><span data-stu-id="9f622-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="9f622-303">Si usas AWS, exportar Hola EC2 instancia tooa disco duro virtual en un depósito de S3 de Amazon.</span><span class="sxs-lookup"><span data-stu-id="9f622-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="9f622-304">Siga los pasos de hello descritos en la documentación de Amazon de herramienta de interfaz de línea de comandos (CLI) de exportación de Amazon EC2 instancias tooinstall Hola Amazon EC2 hello y ejecutar archivo VHD de hello comando Crear-instancia-export-tarea tooexport Hola EC2 instancia tooa.</span><span class="sxs-lookup"><span data-stu-id="9f622-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="9f622-305">Ser seguro toouse **VHD** para hello disco &#95; imagen &#95; Variable de formato cuando se ejecuta hello **crear instancia-export-tareas** comando.</span><span class="sxs-lookup"><span data-stu-id="9f622-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="9f622-306">Hello VHD archivo exportado se guarda en el cubo de hello Amazon S3 que designar durante ese proceso.</span><span class="sxs-lookup"><span data-stu-id="9f622-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="9f622-307">Descargar archivo de disco duro virtual de hello de depósito de S3 Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="9f622-308">Archivo VHD Hola seleccione, a continuación, **acciones** > **descargar**.</span><span class="sxs-lookup"><span data-stu-id="9f622-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="9f622-309">Copia un VHD de una nube que no es de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="9f622-310">Si va a migrar el disco duro virtual de almacenamiento en nube que no Azure tooAzure, primero debe exportar el directorio local de hello VHD tooa.</span><span class="sxs-lookup"><span data-stu-id="9f622-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="9f622-311">Copiar ruta de acceso de origen completa de hello del directorio local Hola donde se almacena los VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="9f622-312">Copia de un VHD desde un entorno local</span><span class="sxs-lookup"><span data-stu-id="9f622-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="9f622-313">Si está migrando VHD desde un entorno local, necesitará la ruta de acceso de origen completa de Hola donde se almacena los VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="9f622-314">ruta de acceso de origen de Hello podría ser un recurso compartido de archivo o ubicación de servidor.</span><span class="sxs-lookup"><span data-stu-id="9f622-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="9f622-315">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="9f622-315">Step 2.</span></span> <span data-ttu-id="9f622-316">Crear destino de hello para el disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="9f622-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="9f622-317">Cree una cuenta de almacenamiento para mantener los discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f622-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="9f622-318">Considere la posibilidad de hello siguientes puntos cuando planee dónde toostore los discos duros virtuales:</span><span class="sxs-lookup"><span data-stu-id="9f622-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="9f622-319">cuenta de almacenamiento de destino de Hello podría ser almacenamiento standard o premium según sus necesidades de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f622-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="9f622-320">región Hello de la cuenta de almacenamiento debe ser igual que el almacenamiento Premium compatible con máquinas virtuales de Azure que creará en la fase final de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="9f622-321">Podría copiar tooa nueva cuenta de almacenamiento u Hola de toouse plan misma cuenta de almacenamiento según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="9f622-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="9f622-322">Copie y guarde la clave de cuenta de almacenamiento de Hola de cuenta de almacenamiento de destino de hello para la fase siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="9f622-323">Se recomienda encarecidamente que mover todos los datos de almacenamiento de información premium toouse de carga de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="9f622-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="9f622-324">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="9f622-324">Step 3.</span></span> <span data-ttu-id="9f622-325">Cargar Hola VHD tooAzure almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="9f622-326">Ahora que tiene el disco duro virtual en el directorio local de hello, puede utilizar AzCopy o AzurePowerShell tooupload Hola .vhd archivo tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f622-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="9f622-327">A continuación se explican ambas opciones:</span><span class="sxs-lookup"><span data-stu-id="9f622-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="9f622-328">Opción 1: Usar el archivo .vhd de Azure PowerShell Add-AzureVhd tooupload Hola</span><span class="sxs-lookup"><span data-stu-id="9f622-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="9f622-329">Un ejemplo <Uri> podría ser ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="9f622-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="9f622-330">Un ejemplo <FileInfo> podría ser ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="9f622-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="9f622-331">Opción 2: Usar el archivo .vhd de AzCopy tooupload Hola</span><span class="sxs-lookup"><span data-stu-id="9f622-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="9f622-332">AzCopy puede cargar fácilmente Hola VHD a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="9f622-333">Función tamaño Hola de hello discos duros virtuales, esto puede tardar tiempo.</span><span class="sxs-lookup"><span data-stu-id="9f622-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="9f622-334">Recuerde límites de entrada/salida de la cuenta de almacenamiento de toocheck hello cuando utilice esta opción.</span><span class="sxs-lookup"><span data-stu-id="9f622-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="9f622-335">Vea [Objetivos de escalabilidad y rendimiento del almacenamiento en Azure](storage-scalability-targets.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="9f622-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="9f622-336">Descargue e instale AzCopy desde aquí: [versión más reciente de AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="9f622-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="9f622-337">Abra PowerShell de Azure y carpeta toohello vaya donde está instalado AzCopy.</span><span class="sxs-lookup"><span data-stu-id="9f622-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="9f622-338">Archivo de disco duro virtual de hello toocopy de "Origen" de comando siguiente de Hola de uso demasiado "Destino".</span><span class="sxs-lookup"><span data-stu-id="9f622-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="9f622-339">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f622-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="9f622-340">Estas son las descripciones de parámetros de hello utilizados en hello AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="9f622-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="9f622-341">**El código fuente:  *&lt;origen&gt;:***  ubicación de carpeta de Hola o dirección URL del contenedor de almacenamiento que contiene Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="9f622-342">**/ SourceKey:  *&lt;clave de la cuenta de origen&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="9f622-343">**/ Dest:  *&lt;destino&gt;:***  toocopy de dirección URL del contenedor de almacenamiento Hola disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="9f622-344">**/ DestKey:  *&lt;clave de cuenta dest&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="9f622-345">**/ BlobType: página:** especifica ese destino hello es un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="9f622-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="9f622-346">**/ Patrón:  *&lt;nombre de archivo&gt;:***  especificar el nombre de archivo de Hola de hello toocopy de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="9f622-347">Para obtener más información sobre el uso de AzCopy herramienta, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="9f622-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="9f622-348">Otras opciones para cargar un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="9f622-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="9f622-349">También puede cargar una cuenta de almacenamiento de disco duro virtual tooyour utilizando uno de hello siguiente significa:</span><span class="sxs-lookup"><span data-stu-id="9f622-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="9f622-350">API de tipo Copy Blob de Almacenamiento Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="9f622-351">Blobs de carga de Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="9f622-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="9f622-352">Referencia de la API de REST de servicios de importación y exportación de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="9f622-353">Se recomienda utilizar el servicio Import/Export si se calcula que el tiempo de carga va a ser superior a siete días.</span><span class="sxs-lookup"><span data-stu-id="9f622-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="9f622-354">Puede usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tiempo de Hola de unidad de tamaño y la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="9f622-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="9f622-355">Importación/exportación puede ser usar cuenta de almacenamiento estándar tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="9f622-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="9f622-356">Necesitará toocopy de cuenta de almacenamiento de almacenamiento estándar toopremium mediante una herramienta como AzCopy.</span><span class="sxs-lookup"><span data-stu-id="9f622-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="9f622-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Creación de máquinas virtuales de Azure mediante Premium Storage</span><span class="sxs-lookup"><span data-stu-id="9f622-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="9f622-358">Una vez Hola VHD cargado o copiado toohello deseado cuenta de almacenamiento, siga las instrucciones de hello en este Hola de tooregister sección VHD como una imagen del sistema operativo o disco del sistema operativo según el escenario y, a continuación, crear una instancia de la máquina virtual del mismo.</span><span class="sxs-lookup"><span data-stu-id="9f622-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="9f622-359">disco de datos de Hello VHD puede ser toohello adjunto VM una vez que se crea.</span><span class="sxs-lookup"><span data-stu-id="9f622-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="9f622-360">Final de Hola de esta sección se incluye un script de migración de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9f622-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="9f622-361">Dicho script no se ajusta a todos los escenarios.</span><span class="sxs-lookup"><span data-stu-id="9f622-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="9f622-362">Puede que tenga tooupdate Hola script toomatch con su escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="9f622-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="9f622-363">Consulte más adelante, toosee si esta secuencia de comandos aplica el escenario de tooyour, [un Script de migración de ejemplo](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="9f622-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="9f622-364">Lista de comprobación</span><span class="sxs-lookup"><span data-stu-id="9f622-364">Checklist</span></span>
1. <span data-ttu-id="9f622-365">Espere a que todos los discos VHD de hello copia está completa.</span><span class="sxs-lookup"><span data-stu-id="9f622-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="9f622-366">Asegúrese de que el almacenamiento Premium está disponible en la región de Hola que se va a migrar a.</span><span class="sxs-lookup"><span data-stu-id="9f622-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="9f622-367">Decidir la serie de hello nuevas máquinas virtuales que va a usar.</span><span class="sxs-lookup"><span data-stu-id="9f622-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="9f622-368">Debe ser un sistema de almacenamiento Premium capaz y Hola debe ser dependiendo de la disponibilidad de hello en la región de Hola y en función de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="9f622-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="9f622-369">Decida el tamaño VM exacto de Hola que va a usar.</span><span class="sxs-lookup"><span data-stu-id="9f622-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="9f622-370">Tamaño de máquina virtual debe toobe número de hello toosupport lo suficientemente grande como de los discos de datos que tiene.</span><span class="sxs-lookup"><span data-stu-id="9f622-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="9f622-371">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="9f622-371">E.g.</span></span> <span data-ttu-id="9f622-372">Si tiene 4 discos de datos, Hola VM debe tener 2 o más núcleos.</span><span class="sxs-lookup"><span data-stu-id="9f622-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="9f622-373">Considere también las necesidades de potencia de procesamiento, memoria y ancho de banda de red.</span><span class="sxs-lookup"><span data-stu-id="9f622-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="9f622-374">Crear una cuenta de almacenamiento Premium en la región de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="9f622-375">Se trata de cuenta de hello que se empleará para hello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="9f622-376">Tener detalles VM actuales de hello útiles, incluidas las listas de Hola de discos y los blobs de disco duro virtual correspondientes.</span><span class="sxs-lookup"><span data-stu-id="9f622-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="9f622-377">Prepare la aplicación para el tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="9f622-377">Prepare your application for downtime.</span></span> <span data-ttu-id="9f622-378">toodo una migración limpia, que toostop todo el procesamiento de hello en hello actual sistema.</span><span class="sxs-lookup"><span data-stu-id="9f622-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="9f622-379">Solo entonces puede obtenerlo tooconsistent estado en el que puede migrar toohello nueva plataforma.</span><span class="sxs-lookup"><span data-stu-id="9f622-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="9f622-380">Duración del tiempo de inactividad dependerá de la cantidad de Hola de datos en hello discos toomigrate.</span><span class="sxs-lookup"><span data-stu-id="9f622-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="9f622-381">Si va a crear una VM de administrador de recursos de Azure desde un disco especializado de disco duro virtual, consulte demasiado[esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) para la implementación de administrador de recursos de VM con disco existente.</span><span class="sxs-lookup"><span data-stu-id="9f622-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="9f622-382">Registrar el disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="9f622-382">Register your VHD</span></span>
<span data-ttu-id="9f622-383">toocreate una máquina virtual desde el disco duro virtual del sistema operativo o tooattach un tooa de disco de datos nueva máquina virtual, primero debe registrarse ellos.</span><span class="sxs-lookup"><span data-stu-id="9f622-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="9f622-384">Siga los pasos especificados a continuación en función del escenario de su VHD.</span><span class="sxs-lookup"><span data-stu-id="9f622-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="9f622-385">Generalizado toocreate de sistema operativo VHD varias instancias de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="9f622-386">Después de imagen del sistema operativo generalizado es el disco duro virtual cargado toohello cuenta de almacenamiento, regístrelo como un **imagen de máquina virtual de Azure** para que pueda crear una o varias instancias VM del mismo.</span><span class="sxs-lookup"><span data-stu-id="9f622-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="9f622-387">Usar un VHD de hello después tooregister de cmdlets de PowerShell como una imagen de sistema operativo de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="9f622-388">Proporcione la dirección URL de contenedor completa de Hola donde se ha copiado el disco duro virtual a.</span><span class="sxs-lookup"><span data-stu-id="9f622-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="9f622-389">Copie y guarde el nombre de Hola de esta nueva imagen de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="9f622-390">En el ejemplo de Hola anterior, es *NombreImagenSO*.</span><span class="sxs-lookup"><span data-stu-id="9f622-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="9f622-391">Único sistema operativo VHD toocreate una sola instancia de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="9f622-392">Después de hello único VHD de SO es almacenamiento toohello cargado account, registrarlo como un **el disco del sistema operativo de Azure** para que pueda crear una instancia de la máquina virtual del mismo.</span><span class="sxs-lookup"><span data-stu-id="9f622-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="9f622-393">Usar estas tooregister de cmdlets de PowerShell en un VHD como un disco de sistema operativo de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="9f622-394">Proporcione la dirección URL de contenedor completa de Hola donde se ha copiado el disco duro virtual a.</span><span class="sxs-lookup"><span data-stu-id="9f622-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="9f622-395">Copie y guarde el nombre de Hola de este nuevo disco de SO de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="9f622-396">En el ejemplo de Hola anterior, es *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="9f622-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="9f622-397">Toobe de disco duro virtual del disco de datos adjunta toonew instancias de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="9f622-398">Después de hello VHD es el disco de datos cargado toostorage cuenta, registrarlo como un disco de datos de Azure para que pueda tooyour adjunto nueva serie DS, DSv2 serie o instancia de máquina virtual de la serie GS Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="9f622-399">Use estos tooregister de cmdlets de PowerShell en el disco duro virtual como un disco de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="9f622-400">Proporcione la dirección URL de contenedor completa de Hola donde se ha copiado el disco duro virtual a.</span><span class="sxs-lookup"><span data-stu-id="9f622-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="9f622-401">Copie y guarde el nombre de Hola de este nuevo disco de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f622-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="9f622-402">En el ejemplo de Hola anterior, es *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="9f622-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="9f622-403">Creación de una máquina virtual compatible con Premium Storage</span><span class="sxs-lookup"><span data-stu-id="9f622-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="9f622-404">Una vez Hola imagen del sistema operativo o disco del sistema operativo se registran, cree un nuevo DS-series, DSv2-series o GS-series VM.</span><span class="sxs-lookup"><span data-stu-id="9f622-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="9f622-405">Va a utilizar imagen de sistema operativo de Hola o nombre de disco de sistema operativo que haya registrado.</span><span class="sxs-lookup"><span data-stu-id="9f622-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="9f622-406">Seleccione el tipo de máquina virtual de Hola de capa de almacenamiento Premium de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="9f622-407">En el ejemplo siguiente, estamos utilizando hello *Standard_DS2* tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="9f622-408">Actualizar hello toomake de tamaño de disco que se corresponde con la capacidad y los requisitos de rendimiento y tamaños de disco de Azure disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="9f622-409">Cmdlets de PowerShell de seguimiento Hola paso a paso por debajo de toocreate Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="9f622-410">En primer lugar, establezca los parámetros comunes de hello:</span><span class="sxs-lookup"><span data-stu-id="9f622-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="9f622-411">En primer lugar, cree un servicio en la nube en el que hospedar las máquinas virtuales nuevas.</span><span class="sxs-lookup"><span data-stu-id="9f622-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="9f622-412">A continuación, según el escenario, crear instancia de máquina virtual de Azure de Hola de hello imagen del sistema operativo o disco del sistema operativo que haya registrado.</span><span class="sxs-lookup"><span data-stu-id="9f622-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="9f622-413">Generalizado toocreate de sistema operativo VHD varias instancias de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="9f622-414">Crear Hola uno o más instancias de máquina virtual de la serie DS Azure nuevo mediante hello **imagen del sistema operativo Azure** que haya registrado.</span><span class="sxs-lookup"><span data-stu-id="9f622-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="9f622-415">Especifique este nombre de imagen del sistema operativo en configuración de máquina virtual de hello al crear la nueva máquina virtual tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f622-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="9f622-416">Único sistema operativo VHD toocreate una sola instancia de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="9f622-417">Crear una nueva instancia de máquina virtual de Azure de serie de DS utilizando hello **disco del sistema operativo Azure** que haya registrado.</span><span class="sxs-lookup"><span data-stu-id="9f622-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="9f622-418">Especifique este nombre de disco del sistema operativo en configuración de máquina virtual de hello al crear Hola nueva máquina virtual tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f622-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="9f622-419">Especifique más datos sobre la máquina virtual de Azure, como un servicio en la nube, la región, la cuenta de almacenamiento, el conjunto de disponibilidad y la directiva de almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="9f622-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="9f622-420">Observe que la instancia de la máquina virtual de hello debe compartir ubicación con el sistema operativo asociado o discos de datos, por lo que la cuenta de almacenamiento, la región y el servicio de nube Hola seleccionado debe estar en Hola la misma ubicación que Hola subyacente discos duros virtuales de esos discos.</span><span class="sxs-lookup"><span data-stu-id="9f622-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="9f622-421">Acoplar disco de datos</span><span class="sxs-lookup"><span data-stu-id="9f622-421">Attach data disk</span></span>
<span data-ttu-id="9f622-422">Por último, si se ha registrado datos disco discos duros virtuales, deberá asociarlas toohello nueva VM de Azure con capacidad de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="9f622-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="9f622-423">Usar los siguientes datos disco toohello de PowerShell cmdlet tooattach nueva máquina virtual y especifique Hola directiva de caché.</span><span class="sxs-lookup"><span data-stu-id="9f622-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="9f622-424">En el ejemplo siguiente Hola directiva de caché se establece demasiado*ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="9f622-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="9f622-425">Puede haber pasos adicionales necesarios toosupport la aplicación que no es estarán sujetos a esta guía.</span><span class="sxs-lookup"><span data-stu-id="9f622-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="9f622-426">Comprobación y planeamiento de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9f622-426">Checking and plan backup</span></span>
<span data-ttu-id="9f622-427">Una vez Hola nueva máquina virtual está activo y en ejecución, acceso mediante Hola mismo identificador de inicio de sesión y la contraseña es que la VM original de Hola y comprobar que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="9f622-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="9f622-428">Todas las configuraciones de hello, incluidos volúmenes de hello particionado, estará presentes en Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="9f622-429">Hola último paso es tooplan programación de copia de seguridad y mantenimiento de hello que nueva máquina virtual en función de las necesidades de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9f622-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="9f622-430"><a name="a-sample-migration-script"></a>Un script de migración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9f622-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="9f622-431">Si tiene varios toomigrate de máquinas virtuales, automatización mediante scripts de PowerShell le resultarán útil.</span><span class="sxs-lookup"><span data-stu-id="9f622-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="9f622-432">Aquí te mostramos una secuencia de comandos de ejemplo que automatiza la migración de Hola de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f622-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="9f622-433">Tenga en cuenta que el siguiente script es sólo un ejemplo y no hay algunos supuestos sobre discos de máquina virtual actuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="9f622-434">Puede que tenga tooupdate Hola script toomatch con su escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="9f622-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="9f622-435">suposiciones de Hello son:</span><span class="sxs-lookup"><span data-stu-id="9f622-435">hello assumptions are:</span></span>

* <span data-ttu-id="9f622-436">Va a crear máquinas virtuales de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="9f622-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="9f622-437">Los discos de SO de origen y los discos de datos de origen están en la misma cuenta de almacenamiento y en el mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="9f622-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="9f622-438">Si los discos de sistema operativo y los discos de datos no están en Hola mismo colocar, puede utilizar AzCopy o Azure PowerShell toocopy discos duros virtuales a través de las cuentas de almacenamiento y los contenedores.</span><span class="sxs-lookup"><span data-stu-id="9f622-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="9f622-439">Consulte el paso anterior toohello: [VHD de copia con AzCopy o PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="9f622-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="9f622-440">Editar esta secuencia de comandos toomeet el escenario que es otra opción, pero se recomienda utilizar AzCopy o PowerShell, ya que es más rápido y sencillo.</span><span class="sxs-lookup"><span data-stu-id="9f622-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="9f622-441">a continuación se proporciona el script de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-441">hello automation script is provided below.</span></span> <span data-ttu-id="9f622-442">Reemplace el texto por la información y actualizar Hola script toomatch con su escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="9f622-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="9f622-443">Utilizando un script existente hello no conserva la configuración de red de hello del máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="9f622-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="9f622-444">Se necesita una configuración de red hello toore-config en las máquinas virtuales migradas.</span><span class="sxs-lookup"><span data-stu-id="9f622-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="9f622-445"><a name="optimization"></a>Optimización</span><span class="sxs-lookup"><span data-stu-id="9f622-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="9f622-446">La configuración actual de la máquina virtual se puede personalizar específicamente toowork bien con los discos estándar.</span><span class="sxs-lookup"><span data-stu-id="9f622-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="9f622-447">Por ejemplo, tooincrease Hola rendimiento mediante el uso de muchos discos en un volumen seccionado.</span><span class="sxs-lookup"><span data-stu-id="9f622-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="9f622-448">Por ejemplo, en lugar de utilizar discos de 4 por separado en almacenamiento Premium, es posible que costo de hello toooptimize puede tener un único disco.</span><span class="sxs-lookup"><span data-stu-id="9f622-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="9f622-449">Las optimizaciones como este toobe necesidad maneja un caso por caso y requieren pasos personalizados después de la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="9f622-450">Además, tenga en cuenta que este proceso no puede funcionar bien para bases de datos y las aplicaciones que dependen de diseño del disco Hola definido en el programa de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="9f622-451">Preparación</span><span class="sxs-lookup"><span data-stu-id="9f622-451">Preparation</span></span>
1. <span data-ttu-id="9f622-452">Hola completa migración Simple, como se describe en hello en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="9f622-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="9f622-453">Las optimizaciones se realizará en hello nueva máquina virtual después de la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="9f622-454">Definir nuevos tamaños de disco Hola necesarios para la configuración de hello optimizado.</span><span class="sxs-lookup"><span data-stu-id="9f622-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="9f622-455">Determinar la asignación de hello actual discos o volúmenes toohello nuevo disco especificaciones.</span><span class="sxs-lookup"><span data-stu-id="9f622-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="9f622-456">Pasos de ejecución</span><span class="sxs-lookup"><span data-stu-id="9f622-456">Execution steps</span></span>
1. <span data-ttu-id="9f622-457">Crear nuevos discos de hello con los tamaños adecuados de hello en hello VM de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="9f622-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="9f622-458">Inicio de sesión toohello VM y copia Hola datos de hello volumen toohello nuevo disco actual que asigna toothat volumen.</span><span class="sxs-lookup"><span data-stu-id="9f622-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="9f622-459">Haga esto para todos los volúmenes actual Hola que necesitan toomap tooa nuevo disco.</span><span class="sxs-lookup"><span data-stu-id="9f622-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="9f622-460">A continuación, cambiar discos nuevos de hello aplicación configuración tooswitch toohello y separar los anteriores volúmenes Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="9f622-461">Para ajustar la aplicación hello para mejorar el rendimiento de disco, consulte demasiado[optimizar el rendimiento de la aplicación](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="9f622-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="9f622-462">Migraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9f622-462">Application migrations</span></span>
<span data-ttu-id="9f622-463">Las bases de datos y otras aplicaciones complejas pueden requerir pasos especiales definidos por el proveedor de la aplicación hello para la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f622-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="9f622-464">Consulte la documentación de la aplicación toorespective.</span><span class="sxs-lookup"><span data-stu-id="9f622-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="9f622-465">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="9f622-465">E.g.</span></span> <span data-ttu-id="9f622-466">las bases de datos normalmente se pueden migrar mediante copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="9f622-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f622-467">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f622-467">Next steps</span></span>
<span data-ttu-id="9f622-468">Vea Hola recursos para escenarios específicos para migrar máquinas virtuales siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f622-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="9f622-469">Migrar máquinas virtuales de Azure entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9f622-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="9f622-470">Crear y cargar un VHD de Windows Server tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9f622-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="9f622-471">Crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="9f622-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="9f622-472">Migración de máquinas virtuales de Amazon AWS tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="9f622-473">Además, vea Hola después recursos toolearn más información sobre el almacenamiento de Azure y máquinas virtuales de Azure:</span><span class="sxs-lookup"><span data-stu-id="9f622-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="9f622-474">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9f622-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="9f622-475">Máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="9f622-476">Almacenamiento premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f622-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
