---
title: "tamaños de máquina virtual de Windows aaaAzure - HPC | Documentos de Microsoft"
description: "Enumera los tamaños diferentes de hello disponibles para las máquinas virtuales en Azure de informática de alto rendimiento de Windows."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="3acf3-103">Tamaños de máquina virtual de informática de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="3acf3-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="3acf3-104">Instancias compatibles con RDMA</span><span class="sxs-lookup"><span data-stu-id="3acf3-104">RDMA-capable instances</span></span>
<span data-ttu-id="3acf3-105">Un subconjunto de instancias de proceso intensivo de hello (H16r, H16mr, A8 y A9) cuentan con una interfaz de red para la conectividad de memoria directa remota (RDMA) de acceso.</span><span class="sxs-lookup"><span data-stu-id="3acf3-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="3acf3-106">Esta interfaz es además tamaños de máquina virtual de toohello red de Azure estándar interfaz tooother disponible.</span><span class="sxs-lookup"><span data-stu-id="3acf3-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="3acf3-107">Esta interfaz permite hello toocommunicate de instancias compatible con RDMA a través de una red de InfiniBand, funcionan a velocidades FDR para máquinas virtuales H16r y H16mr y las tasas QDR para máquinas virtuales A8 y A9.</span><span class="sxs-lookup"><span data-stu-id="3acf3-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="3acf3-108">Estas capacidades RDMA pueden mejorar la escalabilidad de Hola y el rendimiento de las aplicaciones de interfaz de paso de mensajes (MPI).</span><span class="sxs-lookup"><span data-stu-id="3acf3-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="3acf3-109">Estos son los requisitos para máquinas virtuales de Windows compatibles con RDMA tooaccess Hola red RDMA de Azure:</span><span class="sxs-lookup"><span data-stu-id="3acf3-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="3acf3-110">**Sistema operativos**</span><span class="sxs-lookup"><span data-stu-id="3acf3-110">**Operating system**</span></span>
  
  <span data-ttu-id="3acf3-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3acf3-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3acf3-112">Actualmente, Windows Server 2016 no admite conectividad RDMA en Azure.</span><span class="sxs-lookup"><span data-stu-id="3acf3-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="3acf3-113">**Conjunto de disponibilidad o servicio en la nube** : Hola a implementar máquinas virtuales de hello compatibles con RDMA en el mismo conjunto (cuando se utiliza el modelo de implementación de Azure Resource Manager hello) de disponibilidad u Hola mismo servicio en la nube (cuando se utiliza el modelo de implementación clásica de hello).</span><span class="sxs-lookup"><span data-stu-id="3acf3-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="3acf3-114">Si utiliza Azure Batch, Hola máquinas virtuales compatibles con RDMA debe estar en hello mismo grupo.</span><span class="sxs-lookup"><span data-stu-id="3acf3-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="3acf3-115">**MPI** : Microsoft MPI (MS-MPI) 2012 R2 o versiones posteriores, MPI Intel Library 5.x.</span><span class="sxs-lookup"><span data-stu-id="3acf3-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="3acf3-116">Implementaciones de MPI admitidas use hello toocommunicate de interfaz Microsoft Network Direct entre instancias.</span><span class="sxs-lookup"><span data-stu-id="3acf3-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="3acf3-117">**Espacio de direcciones de red RDMA** -Hola dirección espacio 172.16.0.0/16 de reserva de red RDMA de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="3acf3-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="3acf3-118">toorun de aplicaciones de MPI en instancias implementadas en una red virtual de Azure, asegúrese de que el espacio de direcciones de red virtual de hello no se superponen red RDMA de Hola.</span><span class="sxs-lookup"><span data-stu-id="3acf3-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="3acf3-119">**Extensión HpcVmDrivers VM** -en máquinas virtuales compatibles con RDMA, debe agregar el controladores de dispositivos de hello HpcVmDrivers extensión tooinstall Windows red para la conectividad RDMA.</span><span class="sxs-lookup"><span data-stu-id="3acf3-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="3acf3-120">(En ciertas implementaciones de instancias A8 y A9, Hola extensión HpcVmDrivers se agrega automáticamente.) tooa de extensión VM de hello tooadd VM, puede usar [Azure PowerShell](/powershell/azure/overview) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3acf3-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="3acf3-121">Hola el siguiente comando instala Hola más reciente extensión HpcVMDrivers de versión 1.1 en una máquina virtual compatible con RDMA existente denominada *myVM* implementados en el grupo de recursos de hello llamado *myResourceGroup* en hello  *Oeste de Estados Unidos* región:</span><span class="sxs-lookup"><span data-stu-id="3acf3-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="3acf3-122">Para obtener más información, consulte el artículo de [características y extensiones de las máquinas virtuales](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3acf3-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3acf3-123">También puede trabajar con las extensiones de máquinas virtuales implementadas en hello [modelo de implementación clásica](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="3acf3-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="3acf3-124">Uso de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3acf3-124">Using HPC Pack</span></span>

<span data-ttu-id="3acf3-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuito HPC clúster y el trabajo de administración de la solución de Microsoft, constituye una opción para toocreate un clúster de cálculo en las aplicaciones de MPI basados en Windows Azure toorun y otras cargas de trabajo HPC.</span><span class="sxs-lookup"><span data-stu-id="3acf3-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="3acf3-126">HPC Pack 2012 R2 y versiones posteriores incluyen un entorno en tiempo de ejecución para MS-MPI que usa la red RDMA de Azure de hello cuando se implementa en máquinas virtuales compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="3acf3-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="3acf3-127">Otros tamaños</span><span class="sxs-lookup"><span data-stu-id="3acf3-127">Other sizes</span></span>
- [<span data-ttu-id="3acf3-128">Uso general</span><span class="sxs-lookup"><span data-stu-id="3acf3-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="3acf3-129">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="3acf3-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="3acf3-130">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="3acf3-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="3acf3-131">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="3acf3-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="3acf3-132">GPU optimizada</span><span class="sxs-lookup"><span data-stu-id="3acf3-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="3acf3-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3acf3-133">Next steps</span></span>

- <span data-ttu-id="3acf3-134">Para las instancias de proceso intensivo de las listas de comprobación toouse Hola con HPC Pack en Windows Server, vea [configurar un clúster de Windows RDMA con aplicaciones de MPI de HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3acf3-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="3acf3-135">instancias de proceso intensivo toouse al ejecutar aplicaciones MPI con Azure Batch, vea [varias instancias de uso tareas toorun las aplicaciones de interfaz de paso de mensajes (MPI) en Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="3acf3-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="3acf3-136">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="3acf3-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




