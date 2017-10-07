---
title: "proceso intensivo aaaAbout las máquinas virtuales con Linux | Documentos de Microsoft"
description: "Obtener información general y consideraciones para el uso de tamaños de proceso intensivo de hello H-series y A8, A9, A10 y A11 para máquinas virtuales de Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="2c538-103">Acerca de las máquinas virtuales de la serie H y A de procesos intensivos para Linux</span><span class="sxs-lookup"><span data-stu-id="2c538-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="2c538-104">Aquí es información general y algunas consideraciones para el uso de Hola H-series de Azure más recientes y Hola tamaños A8, A9, A10 y A11 anteriores, también conocido como *infromáticos* instancias.</span><span class="sxs-lookup"><span data-stu-id="2c538-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="2c538-105">Este artículo se centra en el uso de estos tamaños con las máquinas virtuales con Linux.</span><span class="sxs-lookup"><span data-stu-id="2c538-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="2c538-106">También puede utilizarlos para [máquinas virtuales Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c538-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="2c538-107">Para conocer las especificaciones básicas, las capacidades de almacenamiento y los detalles del disco, consulte [Tamaños de las máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c538-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="2c538-108">Red de acceso toohello RDMA</span><span class="sxs-lookup"><span data-stu-id="2c538-108">Access toohello RDMA network</span></span>
<span data-ttu-id="2c538-109">Puede crear clústeres de máquinas virtuales de Linux compatibles con RDMA que ejecute uno de hello siguientes distribuciones de Linux HPC admitidas y una ventaja de tootake de implementación de MPI admitida de red RDMA de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c538-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="2c538-110">Vea [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para opciones de implementación y los pasos de configuración de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2c538-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="2c538-111">**Distribuciones** : debe implementar las máquinas virtuales de compatible con RDMA SUSE Linux Enterprise Server (SLES) u Hola de imágenes de Software de Wave no autorizado (anteriormente OpenLogic) basado en CentOS HPC en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2c538-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="2c538-112">Hello imágenes Marketplace siguientes admiten conectividad RDMA:</span><span class="sxs-lookup"><span data-stu-id="2c538-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="2c538-113">SLES 12 SP1 para HPC, SLES 12 SP1 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="2c538-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="2c538-114">HPC 7.1 basada en CentOS y HPC 6.5 basada en CentOS</span><span class="sxs-lookup"><span data-stu-id="2c538-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="2c538-115">Para las máquinas virtuales de la serie H, se recomienda un SLES 12 SP1 para la imagen de HPC o la imagen de HPC 7.1 basada en CentOS.</span><span class="sxs-lookup"><span data-stu-id="2c538-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="2c538-116">En las imágenes HPC basado en CentOS hello, actualizaciones del núcleo están deshabilitadas en hello **yum** archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2c538-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="2c538-117">Esto es porque hello controladores Linux RDMA distribuidos como un paquete RPM y actualizaciones de controladores podrían no funcionar si se actualiza el kernel Hola.</span><span class="sxs-lookup"><span data-stu-id="2c538-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="2c538-118">**MPI** : Biblioteca MPI Intel 5.x</span><span class="sxs-lookup"><span data-stu-id="2c538-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="2c538-119">Dependiendo de la imagen de Marketplace de Hola que elija, instalación de licencia, independiente, o puede ser necesaria la configuración de MPI de Intel, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2c538-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="2c538-120">**SLES 12 SP1 para la imagen HPC** -se distribuyen los paquetes de MPI de Intel en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c538-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="2c538-121">Instale con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c538-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="2c538-122">**Imágenes de HPC basadas en CentOS**: Intel MPI 5.1 ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="2c538-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="2c538-123">Configuración adicional del sistema es necesario toorun trabajos MPI en máquinas virtuales en clúster.</span><span class="sxs-lookup"><span data-stu-id="2c538-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="2c538-124">Por ejemplo, en un clúster de máquinas virtuales, necesitará tooestablish nodos de proceso de confianza entre Hola.</span><span class="sxs-lookup"><span data-stu-id="2c538-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="2c538-125">Para la configuración típica, vea [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c538-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="2c538-126">Consideraciones sobre el HPC Pack y Linux</span><span class="sxs-lookup"><span data-stu-id="2c538-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="2c538-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuito HPC clúster y el trabajo de administración de la solución de Microsoft, proporciona una opción de instancias de proceso intensivo de hello toouse con Linux.</span><span class="sxs-lookup"><span data-stu-id="2c538-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="2c538-128">versiones más recientes de Hola de HPC Pack admiten varias distribuciones de Linux toorun en proceso nodos implementados en máquinas virtuales de Azure, administrados por un nodo principal de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2c538-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="2c538-129">Con los nodos de proceso de Linux compatibles con RDMA ejecutando MPI de Intel, HPC Pack puede programar y ejecutar aplicaciones MPI Linux esa red RDMA de Hola de acceso.</span><span class="sxs-lookup"><span data-stu-id="2c538-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="2c538-130">tooget iniciado, consulte [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c538-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="2c538-131">Consideraciones sobre la topología de red</span><span class="sxs-lookup"><span data-stu-id="2c538-131">Network topology considerations</span></span>
* <span data-ttu-id="2c538-132">En las máquinas virtuales con Linux compatibles con RDMA de Azure, Eth1 se reserva para el tráfico de red RDMA.</span><span class="sxs-lookup"><span data-stu-id="2c538-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="2c538-133">No cambie los valores de configuración de Eth1 o toda la información de archivo de configuración de Hola que hace referencia toothis red.</span><span class="sxs-lookup"><span data-stu-id="2c538-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="2c538-134">Eth0 se reserva para el tráfico de red regular de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c538-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="2c538-135">En Azure, no se admite IP sobre InfiniBand (IB).</span><span class="sxs-lookup"><span data-stu-id="2c538-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="2c538-136">Solo se admite RDMA sobre IB.</span><span class="sxs-lookup"><span data-stu-id="2c538-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="2c538-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c538-137">Next steps</span></span>
* <span data-ttu-id="2c538-138">Para obtener más información sobre la disponibilidad y precios de los tamaños de proceso intensivo de hello, consulte [precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="2c538-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="2c538-139">Para más información sobre las capacidades de almacenamiento y los detalles del disco, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c538-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="2c538-140">tooget inició implementar y usar tamaños de proceso intensivo con RDMA en Linux, consulte [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c538-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

