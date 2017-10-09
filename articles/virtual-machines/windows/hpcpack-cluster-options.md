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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Opciones de HPC Pack toocreate y administrar un clúster de Windows HPC en Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

En este artículo se centra en Opciones toocreate HPC Pack cargas de trabajo de Windows de toorun de clústeres. Existen opciones para los clústeres de HPC creando Pack toorun [las cargas de trabajo de Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Ejecución de un clúster de HPC Pack en VM de Azure
### <a name="azure-templates"></a>Plantillas de Azure
* (GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016) (Plantillas de clúster de HPC Pack 2016)
* (Marketplace) [HPC Pack cluster for Windows workloads (Clúster de HPC par cargas de trabajo de Windows)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [HPC Pack cluster for Excel workloads (Clúster de HPC par cargas de trabajo de Excel)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Inicio rápido) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Inicio rápido) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Imágenes de VM de Azure
* [Nodo principal de HPC Pack 2016 en Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Nodo de proceso de HPC Pack 2016 en Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Nodo principal de HPC Pack 2016 en Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Nodo de proceso de HPC Pack 2016 en Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Nodo principal de HPC Pack 2012 R2 en Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Nodo de proceso de 2012 R2 en Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Nodo de proceso de HPC Pack con Excel en Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>Script de implementación de PowerShell
* [Crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Tutoriales
* [Tutorial: Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Implementación de un clúster de HPC Pack 2016 en Azure)
* [Tutorial: Introducción a un clúster de HPC Pack en Azure toorun Excel y las cargas de trabajo SOA](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Implementación manual con hello portal de Azure
* [Configurar el nodo principal de Hola de un clúster de HPC Pack en una VM de Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Administración de clústeres
* [Administración de nodos de proceso en un clúster de HPC Pack en Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Aumento y reducción de los recursos de proceso de Azure en un clúster de HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Enviar el clúster de HPC Pack tooan de trabajos en Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Job management in HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)
* [Manage an HPC Pack cluster in Azure with Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Administrar un clúster de HPC Pack en Azure con Azure Active Directory)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Agregar clúster de HPC Pack de tooan de nodos de rol de trabajo
* [Irrumpir en instancias de trabajo tooAzure con HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Tutorial: Configuración de un clúster híbrido con HPC Pack en Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Agregar Azure "irrumpir" nodos tooan HPC Pack nodo principal en Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Integración con Azure Batch
* [Ráfaga tooAzure por lotes con HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Creación de clústeres RDMA para cargas de trabajo MPI
* [Configurar un clúster de Windows RDMA con aplicaciones de MPI de HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

