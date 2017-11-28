---
title: "aaaPowerShell script toodeploy clúster HPC de Linux | Documentos de Microsoft"
description: "Ejecutar un toodeploy de secuencia de comandos de PowerShell en un clúster de HPC Pack 2012 R2 de Linux en máquinas virtuales de Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="a5217-103">Crear un clúster de informática de alto rendimiento (HPC) de Linux con script de implementación de IaaS de HPC Pack Hola</span><span class="sxs-lookup"><span data-stu-id="a5217-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="a5217-104">Ejecute toodeploy de secuencia de comandos de PowerShell de hello IaaS de HPC Pack implementación en un clúster de HPC Pack 2012 R2 completando para las cargas de trabajo de Linux en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5217-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="a5217-105">clúster de Hello consta de un nodo principal unido a Active Directory con Windows Server y Microsoft HPC Pack y nodos de proceso que ejecutan uno de hello las distribuciones de Linux compatibles con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a5217-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="a5217-106">Si desea toodeploy un clúster de HPC Pack en las cargas de trabajo de Azure para Windows, vea [crear un clúster de HPC de Windows con hello script de implementación de IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5217-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="a5217-107">También puede utilizar un toodeploy de plantilla un clúster de HPC Pack de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a5217-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="a5217-108">Si desea consultar un ejemplo, consulte [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)(Creación de un clúster de HPC con nodos de proceso de Linux).</span><span class="sxs-lookup"><span data-stu-id="a5217-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a5217-109">Hola script de PowerShell descrito en este artículo crea un clúster de Microsoft HPC Pack 2012 R2 en Azure con el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5217-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="a5217-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5217-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="a5217-111">Además, script de Hola descrito en este artículo no es compatible con HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="a5217-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="a5217-112">Archivos de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a5217-112">Example configuration file</span></span>
<span data-ttu-id="a5217-113">Hello siguiente archivo de configuración crea un controlador de dominio y un bosque de dominio e implementa un clúster de HPC Pack que tiene un nodo principal con bases de datos locales y 10 nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="a5217-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="a5217-114">Todos los servicios de nube de Hola se crean directamente en la ubicación de Asia oriental Hola.</span><span class="sxs-lookup"><span data-stu-id="a5217-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="a5217-115">Hello nodos de proceso de Linux en se crean dos servicios en la nube y dos cuentas de almacenamiento (es decir, *MyLnxCN-0001* a *MyLnxCN-0005* en *MyLnxCNService01* y *mylnxstorage01*, y *MyLnxCN-0006* a *MyLnxCN-0010* en *MyLnxCNService02* y *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="a5217-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="a5217-116">nodos de proceso de Hola se crean a partir de una imagen de Linux de OpenLogic CentOS versión 7.0.</span><span class="sxs-lookup"><span data-stu-id="a5217-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="a5217-117">Utilizar sus propios valores para el nombre de la suscripción y los nombres de cuenta y el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5217-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="a5217-118">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="a5217-118">Troubleshooting</span></span>
* <span data-ttu-id="a5217-119">**Error "La red virtual no existe"**.</span><span class="sxs-lookup"><span data-stu-id="a5217-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="a5217-120">Si ejecuta toodeploy de script de implementación de IaaS de HPC Pack Hola varios clústeres en Azure simultáneamente en una suscripción, pueden producir un error en una o más implementaciones con error de Hola "red virtual *VNet\_nombre* no existe".</span><span class="sxs-lookup"><span data-stu-id="a5217-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="a5217-121">Si se produce este error, vuelva a ejecutar script de Hola para la implementación de hello error.</span><span class="sxs-lookup"><span data-stu-id="a5217-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="a5217-122">**Problema de tener acceso a Hola Internet desde la red virtual de Azure de hello**.</span><span class="sxs-lookup"><span data-stu-id="a5217-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="a5217-123">Si crea un clúster de HPC Pack con un nuevo controlador de dominio mediante el uso de script de implementación de Hola o manualmente promover un controlador de toodomain de máquina virtual del nodo principal, puede experimentar problemas para conectar máquinas virtuales de hello en toohello de red virtual de Azure Hola Internet.</span><span class="sxs-lookup"><span data-stu-id="a5217-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="a5217-124">Esto puede ocurrir si un servidor reenviador DNS se configura automáticamente en el controlador de dominio de Hola y este servidor no se puede resolver correctamente.</span><span class="sxs-lookup"><span data-stu-id="a5217-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="a5217-125">toowork resolver este problema, inicie sesión en el controlador de dominio de toohello y cualquier opción de configuración de reenviador de Hola de quitar o configurar un servidor reenviador DNS válido.</span><span class="sxs-lookup"><span data-stu-id="a5217-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="a5217-126">toodo, en el administrador del servidor, haga clic en **herramientas** > **DNS** tooopen Administrador de DNS y, a continuación, haga doble clic en **reenviadores**.</span><span class="sxs-lookup"><span data-stu-id="a5217-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5217-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5217-127">Next steps</span></span>
* <span data-ttu-id="a5217-128">Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para obtener información sobre las distribuciones de Linux admitidas, mover los datos y el envío de clúster de HPC Pack tooan de trabajos con Linux nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="a5217-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="a5217-129">Para ver los tutoriales que usan Hola script toocreate un clúster y ejecutan una carga de trabajo de Linux HPC, vea:</span><span class="sxs-lookup"><span data-stu-id="a5217-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="a5217-130">Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="a5217-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="a5217-131">Ejecución de OpenFOAM con Microsoft HPC Pack en nodos de proceso de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="a5217-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="a5217-132">Ejecución de STAR-CCM+ con Microsoft HPC Pack en nodos de proceso de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="a5217-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

