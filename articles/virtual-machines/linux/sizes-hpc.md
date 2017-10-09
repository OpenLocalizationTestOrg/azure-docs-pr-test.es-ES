---
title: "tamaños de VM de Linux aaaAzure - HPC | Documentos de Microsoft"
description: "Enumera los tamaños diferentes de hello disponibles para las máquinas virtuales en Azure de informática de alto rendimiento de Linux."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="c87d0-103">Tamaños de máquina virtual Linux de informática de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="c87d0-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="c87d0-104">Instancias compatibles con RDMA</span><span class="sxs-lookup"><span data-stu-id="c87d0-104">RDMA-capable instances</span></span>
<span data-ttu-id="c87d0-105">Un subconjunto de instancias de proceso intensivo de hello (H16r, H16mr, A8 y A9) cuentan con una interfaz de red para la conectividad de memoria directa remota (RDMA) de acceso.</span><span class="sxs-lookup"><span data-stu-id="c87d0-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="c87d0-106">Esta interfaz es además tamaños de máquina virtual de toohello red de Azure estándar interfaz tooother disponible.</span><span class="sxs-lookup"><span data-stu-id="c87d0-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="c87d0-107">Esta interfaz permite hello toocommunicate de instancias compatible con RDMA a través de una red de InfiniBand, funcionan a velocidades FDR para máquinas virtuales H16r y H16mr y las tasas QDR para máquinas virtuales A8 y A9.</span><span class="sxs-lookup"><span data-stu-id="c87d0-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="c87d0-108">Estas capacidades RDMA pueden mejorar la escalabilidad de Hola y el rendimiento de las aplicaciones de interfaz de paso de mensajes (MPI).</span><span class="sxs-lookup"><span data-stu-id="c87d0-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="c87d0-109">Estos son los requisitos para máquinas virtuales de Linux compatibles con RDMA tooaccess Hola red RDMA de Azure:</span><span class="sxs-lookup"><span data-stu-id="c87d0-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="c87d0-110">**Distribuciones** : debe implementar las máquinas virtuales de compatible con RDMA SUSE Linux Enterprise Server (SLES) u Hola de imágenes de Software de Wave no autorizado (anteriormente OpenLogic) basado en CentOS HPC en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c87d0-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="c87d0-111">Hello imágenes Marketplace siguientes admiten conectividad RDMA:</span><span class="sxs-lookup"><span data-stu-id="c87d0-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="c87d0-112">SLES 12 SP1 para HPC, o SLES 12 SP1 para HPC (premium)</span><span class="sxs-lookup"><span data-stu-id="c87d0-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="c87d0-113">HPC 7.3 basadas en CentOS, HPC 7.1 basadas en CentOS, HPC 6.8 basadas en CentOS o HPC 6.5 basadas en CentOS</span><span class="sxs-lookup"><span data-stu-id="c87d0-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="c87d0-114">Para las máquinas virtuales de la serie H, se recomienda SLES 12 SP1 para la imagen de HPC o la imagen de HPC 7.1 o posterior basada en CentOS.</span><span class="sxs-lookup"><span data-stu-id="c87d0-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="c87d0-115">En las imágenes HPC basado en CentOS hello, actualizaciones del núcleo están deshabilitadas en hello **yum** archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c87d0-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="c87d0-116">Esto es porque hello controladores Linux RDMA distribuidos como un paquete RPM y actualizaciones de controladores podrían no funcionar si se actualiza el kernel Hola.</span><span class="sxs-lookup"><span data-stu-id="c87d0-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="c87d0-117">**MPI** : Biblioteca MPI Intel 5.x</span><span class="sxs-lookup"><span data-stu-id="c87d0-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="c87d0-118">Dependiendo de la imagen de Marketplace de Hola que elija, instalación de licencia, independiente, o puede ser necesaria la configuración de MPI de Intel, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c87d0-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="c87d0-119">**SLES 12 SP1 para la imagen HPC** -se distribuyen los paquetes de MPI de Intel en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c87d0-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="c87d0-120">Instale con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c87d0-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="c87d0-121">**Imágenes de HPC basadas en CentOS**: Intel MPI 5.1 ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="c87d0-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="c87d0-122">Configuración adicional del sistema es necesario toorun trabajos MPI en máquinas virtuales en clúster.</span><span class="sxs-lookup"><span data-stu-id="c87d0-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="c87d0-123">Por ejemplo, en un clúster de máquinas virtuales, necesitará tooestablish nodos de proceso de confianza entre Hola.</span><span class="sxs-lookup"><span data-stu-id="c87d0-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="c87d0-124">Para la configuración típica, vea [configurar una aplicación de MPI Linux RDMA toorun de clúster](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c87d0-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="c87d0-125">Consideraciones sobre la topología de red</span><span class="sxs-lookup"><span data-stu-id="c87d0-125">Network topology considerations</span></span>
* <span data-ttu-id="c87d0-126">En las máquinas virtuales con Linux compatibles con RDMA de Azure, Eth1 se reserva para el tráfico de red RDMA.</span><span class="sxs-lookup"><span data-stu-id="c87d0-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="c87d0-127">No cambie los valores de configuración de Eth1 o toda la información de archivo de configuración de Hola que hace referencia toothis red.</span><span class="sxs-lookup"><span data-stu-id="c87d0-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="c87d0-128">Eth0 se reserva para el tráfico de red regular de Azure.</span><span class="sxs-lookup"><span data-stu-id="c87d0-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="c87d0-129">En Azure, no se admite IP sobre InfiniBand (IB).</span><span class="sxs-lookup"><span data-stu-id="c87d0-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="c87d0-130">Solo se admite RDMA sobre IB.</span><span class="sxs-lookup"><span data-stu-id="c87d0-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="c87d0-131">Uso de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="c87d0-131">Using HPC Pack</span></span>
<span data-ttu-id="c87d0-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuito HPC clúster y el trabajo de administración de la solución de Microsoft, constituye una opción automáticamente instancias de proceso intensivo de hello toouse con Linux.</span><span class="sxs-lookup"><span data-stu-id="c87d0-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="c87d0-133">versiones más recientes de Hola de HPC Pack admiten varias distribuciones de Linux toorun en proceso nodos implementados en máquinas virtuales de Azure, administrados por un nodo principal de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c87d0-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="c87d0-134">Con los nodos de proceso de Linux compatibles con RDMA ejecutando MPI de Intel, HPC Pack puede programar y ejecutar aplicaciones MPI Linux esa red RDMA de Hola de acceso.</span><span class="sxs-lookup"><span data-stu-id="c87d0-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="c87d0-135">Consulte [Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c87d0-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="c87d0-136">Otros tamaños</span><span class="sxs-lookup"><span data-stu-id="c87d0-136">Other sizes</span></span>
- [<span data-ttu-id="c87d0-137">Uso general</span><span class="sxs-lookup"><span data-stu-id="c87d0-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="c87d0-138">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="c87d0-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="c87d0-139">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="c87d0-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="c87d0-140">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="c87d0-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="c87d0-141">GPU</span><span class="sxs-lookup"><span data-stu-id="c87d0-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="c87d0-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c87d0-142">Next steps</span></span>

- <span data-ttu-id="c87d0-143">tooget inició implementar y usar tamaños de proceso intensivo con RDMA en Linux, consulte [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c87d0-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="c87d0-144">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="c87d0-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




