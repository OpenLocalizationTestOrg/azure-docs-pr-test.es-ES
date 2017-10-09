---
title: "Opciones de clúster de HPC Pack aaaLinux en la nube de hello | Documentos de Microsoft"
description: "Obtenga información acerca de las opciones con Microsoft HPC Pack toocreate y administrar un clúster (HPC) en la nube de Azure Hola de informática de Linux alto rendimiento"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="d3bb9-103">Opciones de HPC Pack toocreate y administrar un clúster de HPC en Azure para las cargas de trabajo de Linux</span><span class="sxs-lookup"><span data-stu-id="d3bb9-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="d3bb9-104">En este artículo se centra en Opciones toouse HPC Pack toorun Linux las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d3bb9-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="d3bb9-105">También hay opciones para ejecutar [cargas de trabajo de Windows HPC con HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3bb9-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="d3bb9-106">Ejecución de un clúster de HPC Pack en VM de Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="d3bb9-107">Plantillas de Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-107">Azure templates</span></span>
* <span data-ttu-id="d3bb9-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Plantillas de clúster de HPC Pack 2016)</span><span class="sxs-lookup"><span data-stu-id="d3bb9-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="d3bb9-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="d3bb9-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="d3bb9-110">(Inicio rápido) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="d3bb9-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="d3bb9-111">Script de implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3bb9-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="d3bb9-112">Crear un clúster de HPC de Linux con hello script de implementación de IaaS de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d3bb9-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="d3bb9-113">Tutoriales</span><span class="sxs-lookup"><span data-stu-id="d3bb9-113">Tutorials</span></span>
* [<span data-ttu-id="d3bb9-114">Tutorial: Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="d3bb9-115">Tutorial: Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="d3bb9-116">Tutorial: Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="d3bb9-117">Tutorial: Ejecución de STAR-CCM+ con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="d3bb9-118">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="d3bb9-118">Cluster management</span></span>
* [<span data-ttu-id="d3bb9-119">Enviar el clúster de HPC Pack tooan de trabajos en Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d3bb9-120">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d3bb9-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="d3bb9-121">Creación de clústeres RDMA para cargas de trabajo MPI</span><span class="sxs-lookup"><span data-stu-id="d3bb9-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="d3bb9-122">Tutorial: Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="d3bb9-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="d3bb9-123">Configurar una aplicación de MPI Linux RDMA toorun de clúster</span><span class="sxs-lookup"><span data-stu-id="d3bb9-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

