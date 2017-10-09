---
title: "opciones en la nube de Hola de clúster de HPC Pack aaaWindows | Documentos de Microsoft"
description: "Obtenga información acerca de las opciones con Microsoft HPC Pack toocreate y administrar un Windows informática de alto rendimiento clúster (HPC) en hello nube de Azure"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="d5f69-103">Opciones de HPC Pack toocreate y administrar un clúster de Windows HPC en Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="d5f69-104">En este artículo se centra en Opciones toocreate HPC Pack cargas de trabajo de Windows de toorun de clústeres.</span><span class="sxs-lookup"><span data-stu-id="d5f69-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="d5f69-105">Existen opciones para los clústeres de HPC creando Pack toorun [las cargas de trabajo de Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5f69-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="d5f69-106">Ejecución de un clúster de HPC Pack en VM de Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="d5f69-107">Plantillas de Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-107">Azure templates</span></span>
* <span data-ttu-id="d5f69-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Plantillas de clúster de HPC Pack 2016)</span><span class="sxs-lookup"><span data-stu-id="d5f69-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="d5f69-109">(Marketplace) [HPC Pack cluster for Windows workloads (Clúster de HPC par cargas de trabajo de Windows)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="d5f69-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="d5f69-110">(Marketplace) [HPC Pack cluster for Excel workloads (Clúster de HPC par cargas de trabajo de Excel)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="d5f69-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="d5f69-111">(Inicio rápido) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="d5f69-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="d5f69-112">(Inicio rápido) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="d5f69-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="d5f69-113">Imágenes de VM de Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-113">Azure VM images</span></span>
* [<span data-ttu-id="d5f69-114">Nodo principal de HPC Pack 2016 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d5f69-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="d5f69-115">Nodo de proceso de HPC Pack 2016 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d5f69-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="d5f69-116">Nodo principal de HPC Pack 2016 en Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d5f69-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="d5f69-117">Nodo de proceso de HPC Pack 2016 en Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d5f69-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="d5f69-118">Nodo principal de HPC Pack 2012 R2 en Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d5f69-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="d5f69-119">Nodo de proceso de 2012 R2 en Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d5f69-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="d5f69-120">Nodo de proceso de HPC Pack con Excel en Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d5f69-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="d5f69-121">Script de implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5f69-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="d5f69-122">Crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d5f69-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="d5f69-123">Tutoriales</span><span class="sxs-lookup"><span data-stu-id="d5f69-123">Tutorials</span></span>
* <span data-ttu-id="d5f69-124">[Tutorial: Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Implementación de un clúster de HPC Pack 2016 en Azure)</span><span class="sxs-lookup"><span data-stu-id="d5f69-124">[Tutorial: Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="d5f69-125">Tutorial: Introducción a un clúster de HPC Pack en Azure toorun Excel y las cargas de trabajo SOA</span><span class="sxs-lookup"><span data-stu-id="d5f69-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="d5f69-126">Implementación manual con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="d5f69-127">Configurar el nodo principal de Hola de un clúster de HPC Pack en una VM de Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="d5f69-128">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="d5f69-128">Cluster management</span></span>
* [<span data-ttu-id="d5f69-129">Administración de nodos de proceso en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="d5f69-130">Aumento y reducción de los recursos de proceso de Azure en un clúster de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d5f69-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="d5f69-131">Enviar el clúster de HPC Pack tooan de trabajos en Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f69-132">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d5f69-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* <span data-ttu-id="d5f69-133">[Manage an HPC Pack cluster in Azure with Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Administrar un clúster de HPC Pack en Azure con Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="d5f69-133">[Manage an HPC Pack cluster in Azure with Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="d5f69-134">Agregar clúster de HPC Pack de tooan de nodos de rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="d5f69-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="d5f69-135">Irrumpir en instancias de trabajo tooAzure con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d5f69-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="d5f69-136">Tutorial: Configuración de un clúster híbrido con HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="d5f69-137">Agregar Azure "irrumpir" nodos tooan HPC Pack nodo principal en Azure</span><span class="sxs-lookup"><span data-stu-id="d5f69-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="d5f69-138">Integración con Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d5f69-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="d5f69-139">Ráfaga tooAzure por lotes con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d5f69-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="d5f69-140">Creación de clústeres RDMA para cargas de trabajo MPI</span><span class="sxs-lookup"><span data-stu-id="d5f69-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="d5f69-141">Configurar un clúster de Windows RDMA con aplicaciones de MPI de HPC Pack toorun</span><span class="sxs-lookup"><span data-stu-id="d5f69-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

