---
title: "Opciones de clúster de HPC Pack de Linux en la nube | Microsoft Docs"
description: "Obtenga información sobre opciones con Microsoft HPC Pack para crear y administrar un clúster de informática de alto rendimiento (HPC) de Linux en la nube de Azure."
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
ms.openlocfilehash: 616006d29149f7f47b03bd127cf3c83ad63a5c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>Opciones con HPC Pack para crear y administrar un clúster de HPC en Azure para cargas de trabajo de Linux
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Este artículo se centra en las opciones para usar HPC Pack para ejecutar cargas de trabajo de Linux. También hay opciones para ejecutar [cargas de trabajo de Windows HPC con HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Ejecución de un clúster de HPC Pack en VM de Azure
### <a name="azure-templates"></a>Plantillas de Azure
* (GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Plantillas de clúster de HPC Pack 2016)
* (Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (Inicio rápido) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>Script de implementación de PowerShell
* [Creación de un clúster HPC con el script de implementación de IaaS de HPC Pack](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Tutoriales
* [Tutorial: Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Ejecución de STAR-CCM+ con Microsoft HPC Pack en un clúster de Linux RDMA en Azure](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>Administración de clústeres
* [Envío de trabajos a un clúster de HPC Pack en Azure](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Job management in HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Creación de clústeres RDMA para cargas de trabajo MPI
* [Tutorial: Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configuración de un clúster de Linux RDMA para ejecutar aplicaciones MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

