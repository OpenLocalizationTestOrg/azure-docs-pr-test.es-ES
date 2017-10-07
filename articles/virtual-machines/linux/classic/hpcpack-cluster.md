---
title: "aaaLinux compute máquinas virtuales en un clúster de HPC Pack | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y use un módulo de HPC cluster en Azure para las cargas de trabajo (HPC) de informática de alto rendimiento de Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="a5ebc-103">Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="a5ebc-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="a5ebc-104">Configure un clúster de [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) en Azure que contenga un nodo principal en el que se ejecute Windows Server y varios nodos de proceso en los que se ejecute una distribución de Linux compatible.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="a5ebc-105">Explorar opciones toomove datos entre nodos de Linux de Hola y el nodo principal de Windows hello de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="a5ebc-106">Obtenga información acerca de cómo toosubmit Linux HPC trabajos toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a5ebc-107">En un nivel alto, hello siguiente diagrama muestra clúster de HPC Pack Hola crear y trabajar con.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Clúster de HPC con nodos de Linux][scenario]

<span data-ttu-id="a5ebc-109">Para otro toorun opciones Linux HPC cargas de trabajo en Azure, consulte [recursos técnicos para el lote e informática de alto rendimiento](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="a5ebc-110">Implementación de un clúster de HPC Pack con nodos de proceso de Linux</span><span class="sxs-lookup"><span data-stu-id="a5ebc-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="a5ebc-111">Este artículo muestra dos opciones toodeploy un clúster de HPC Pack en Azure con nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="a5ebc-112">Los dos métodos utilizan una imagen de Marketplace de Windows Server con el nodo principal de HPC Pack toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="a5ebc-113">**Plantilla de administrador de recursos de Azure** -utilizar una plantilla de hello Azure Marketplace o una plantilla de inicio rápido de comunidad de hello, creación de tooautomate de clúster de hello en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="a5ebc-114">Por ejemplo, hello [clúster de HPC Pack para cargas de trabajo de Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) plantilla en hello Azure Marketplace crea una infraestructura de clúster de HPC Pack completa para Linux HPC las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="a5ebc-115">**Script de PowerShell** -Hola de uso [script de implementación de Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate una implementación de clúster completa en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="a5ebc-116">Este script de PowerShell de Azure usa una imagen de máquina virtual de HPC Pack en hello Azure Marketplace para la implementación rápida y proporciona un conjunto completo de toodeploy de parámetros de configuración de nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="a5ebc-117">Para obtener más información acerca de las opciones de implementación de clúster de HPC Pack en Azure, consulte [opciones toocreate y administrar clústeres de informática de alto rendimiento (HPC) en Azure con Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a5ebc-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a5ebc-118">Prerequisites</span></span>
* <span data-ttu-id="a5ebc-119">**Suscripción de Azure** -puede usar una suscripción en cualquier servicio Global de Azure o Azure China Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="a5ebc-120">En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="a5ebc-121">**Cuota de núcleos** -podría necesita tooincrease Hola cuota de núcleos, especialmente si elige toodeploy varios nodos de clúster con tamaños de máquinas virtuales con varios núcleos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="a5ebc-122">tooincrease una cuota, abra una solicitud de soporte técnico al cliente en línea sin coste adicional.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="a5ebc-123">**Las distribuciones de Linux** -actualmente HPC Pack admite Hola siguiendo las distribuciones de Linux para nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="a5ebc-124">Puede usar versiones de Marketplace de estas distribuciones cuando estén disponibles o proporcionar las suyas.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="a5ebc-125">**Basado en CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC y 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="a5ebc-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="a5ebc-126">**Red Hat Enterprise Linux**: 6.7, 6.8 y 7.2</span><span class="sxs-lookup"><span data-stu-id="a5ebc-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="a5ebc-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC y SLES 12 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="a5ebc-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="a5ebc-128">**Ubuntu Server**: 14.04 LTS y 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a5ebc-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="a5ebc-129">red de toouse Hola RDMA de Azure con uno de los tamaños de VM Hola compatibles con RDMA, especifique una imagen de SUSE Linux Enterprise Server 12 HPC o basado en CentOS HPC de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="a5ebc-130">Para más información, consulte [Tamaños de máquina virtual de procesos de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="a5ebc-131">Clúster de Hola de toodeploy de requisitos previos adicionales mediante el uso de script de implementación de IaaS de HPC Pack hello:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="a5ebc-132">**Equipo cliente** -necesita un script de implementación de cliente basada en Windows equipo toorun Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="a5ebc-133">**Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="a5ebc-134">**Script de implementación de IaaS de HPC Pack** : Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="a5ebc-135">Puede comprobar Hola versión del script de Hola ejecutando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="a5ebc-136">En este artículo se basa en la versión 4.4.1 o posterior del script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="a5ebc-137">Opción de implementación 1.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-137">Deployment option 1.</span></span> <span data-ttu-id="a5ebc-138">Usar una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a5ebc-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="a5ebc-139">Vaya toohello [clúster de HPC Pack para cargas de trabajo de Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) plantilla en hello Azure Marketplace y haga clic en **implementar**.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="a5ebc-140">Hola portal de Azure, revise la información de hello y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Creación del portal][portal]
3. <span data-ttu-id="a5ebc-142">En hello **Fundamentos** hoja, escriba un nombre para el clúster de hello, que también nombres de máquina virtual del nodo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="a5ebc-143">Puede elegir un grupo de recursos existente o crear un grupo para la implementación de hello en una ubicación que sea tooyou disponible.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="a5ebc-144">Hello ubicación afecta a la disponibilidad de Hola de determinados tamaños de máquina virtual y otros servicios de Azure (consulte [productos disponibles por región](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="a5ebc-145">En hello **principal de la configuración del nodo** hoja, para una implementación de la primera, por lo general puede aceptar valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="a5ebc-146">Hola **URL de script posterior a la configuración de** es opcional establecer toospecify una secuencia de comandos de Windows PowerShell disponible públicamente que desea toorun en la máquina virtual del nodo principal Hola después de que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="a5ebc-147">En hello **configuración de nodo de proceso** hoja, seleccione un modelo de nomenclatura para los nodos de hello, número de Hola y tamaño de los nodos de Hola y Hola toodeploy de distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="a5ebc-148">En hello **configuración de infraestructura** hoja, escribe los nombres de red virtual de Hola y Active Directory dominio, dominio y las credenciales de administrador de máquina virtual y un patrón de nomenclatura para las cuentas de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a5ebc-149">HPC Pack utiliza usuarios de clústeres de tooauthenticate de dominio de Active Directory de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="a5ebc-150">Después de ejecutarán pruebas de validación de Hola y revise los términos de Hola de uso, haga clic en **compra**.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="a5ebc-151">Opción de implementación 2.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-151">Deployment option 2.</span></span> <span data-ttu-id="a5ebc-152">Usar script de implementación de IaaS de Hola</span><span class="sxs-lookup"><span data-stu-id="a5ebc-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="a5ebc-153">Siguientes son requisitos previos adicionales con toodeploy Hola clústeres mediante el uso de script de implementación de IaaS de HPC Pack hello:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="a5ebc-154">**Equipo cliente** -necesita un script de implementación de cliente basada en Windows equipo toorun Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="a5ebc-155">**Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="a5ebc-156">**Script de implementación de IaaS de HPC Pack** : Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="a5ebc-157">Puede comprobar Hola versión del script de Hola ejecutando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="a5ebc-158">En este artículo se basa en la versión 4.4.1 o posterior del script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="a5ebc-159">**Archivo de configuración XML**</span><span class="sxs-lookup"><span data-stu-id="a5ebc-159">**XML configuration file**</span></span>

<span data-ttu-id="a5ebc-160">Hola script de implementación de IaaS de HPC Pack utiliza un archivo de configuración XML como clúster de HPC de entrada toodescribe Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="a5ebc-161">Hello siguiente archivo de configuración de ejemplo especifica un clúster pequeño que consta de un nodo principal de HPC Pack y dos nodos de cálculo de tamaño A7 CentOS 7.0 Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="a5ebc-162">Modifique el archivo hello según sea necesario para su entorno y la configuración de clúster deseado y guárdelo con un nombre como HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="a5ebc-163">Por ejemplo, debe toosupply el nombre de la suscripción y un nombre de la cuenta de almacenamiento único y el nombre del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="a5ebc-164">Además, es recomendable toochoose otro admite la imagen de Linux para nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="a5ebc-165">Para obtener más información acerca de los elementos de hello en el archivo de configuración de hello, consulte el archivo Manual.rtf de hello en la carpeta de script de Hola y [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="a5ebc-166">**Hola toorun script de implementación de IaaS de HPC Pack**</span><span class="sxs-lookup"><span data-stu-id="a5ebc-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="a5ebc-167">Abra Windows PowerShell en el equipo de cliente hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="a5ebc-168">Cambiar carpeta toohello del directorio donde es el script de Hola instalado (E:\IaaSClusterScript en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="a5ebc-169">Ejecute hello después de clúster de HPC Pack de comando toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="a5ebc-170">En este ejemplo se da por supuesto que se encuentra ese archivo de configuración de hello en E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="a5ebc-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="a5ebc-171">a.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-171">a.</span></span> <span data-ttu-id="a5ebc-172">Dado que hello **AdminPassword** no se especifica en Hola anterior comando esté tooenter solicitadas contraseña Hola usuario *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="a5ebc-173">b.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-173">b.</span></span> <span data-ttu-id="a5ebc-174">script de Hola, a continuación, inicia el archivo de configuración de toovalidate Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="a5ebc-175">Esta operación puede tardar tooseveral minutos depende de la conexión de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Validación][validate]
   
    <span data-ttu-id="a5ebc-177">c.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-177">c.</span></span> <span data-ttu-id="a5ebc-178">Una vez que pasen las validaciones, script de Hola presenta toocreate de recursos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="a5ebc-179">Escriba *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-179">Enter *Y* toocontinue.</span></span>
   
    ![Recursos][resources]
   
    <span data-ttu-id="a5ebc-181">d.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-181">d.</span></span> <span data-ttu-id="a5ebc-182">script de Hola inicia el clúster de HPC Pack toodeploy hello y completa Hola configuración sin más pasos manuales.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="a5ebc-183">puede ejecutar el script de Hola durante varios minutos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-183">hello script can run for several minutes.</span></span>
   
    ![Implementación][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="a5ebc-185">En este ejemplo, hello script genera un archivo de registro automáticamente desde hello **- LogFile** parámetro no se especifica.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="a5ebc-186">Hola registros no se escriben en tiempo real, pero se recopilan final Hola de validación de Hola y la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="a5ebc-187">Si Hola proceso de PowerShell se detiene mientras se ejecuta el script de Hola, algunos archivos de registro se pierden.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="a5ebc-188">Conectar el nodo principal de toohello</span><span class="sxs-lookup"><span data-stu-id="a5ebc-188">Connect toohello head node</span></span>
<span data-ttu-id="a5ebc-189">Después de implementar el clúster de HPC Pack hello en Azure, [conectarse mediante Escritorio remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo principal VM con Hola credenciales de dominio que ha proporcionado al implementar el clúster de hello (por ejemplo, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="a5ebc-190">Administrar clústeres de Hola desde el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="a5ebc-191">En el nodo principal de hello, inicie estado de hello toocheck de administrador de clústeres de HPC de clúster de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="a5ebc-192">Puede administrar y supervisar los nodos de proceso de Linux hello igual que funcionan con Windows nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="a5ebc-193">Por ejemplo, verá nodos de Linux de hello enumerados en **administración de recursos** (estos nodos se implementan con hello **LinuxNode** plantilla).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Administración de nodos][management]

<span data-ttu-id="a5ebc-195">También verá los nodos de Linux Hola Hola **mapa térmico** vista.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Mapa térmico][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="a5ebc-197">¿Cómo toomove datos en un clúster con nodos de Linux</span><span class="sxs-lookup"><span data-stu-id="a5ebc-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="a5ebc-198">Tiene varias opciones toomove datos entre nodos de Linux y el nodo principal de Windows hello de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="a5ebc-199">Estos son tres métodos comunes, que se describe con más detalle en hello las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="a5ebc-200">**Archivos de Azure** -expone un administrado datos toostore del recurso compartido de archivos SMB de archivos en almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="a5ebc-201">Nodos de Windows y Linux puede montar un recurso compartido de archivos de Azure como una unidad o carpeta en hello mismo tiempo, incluso si se implementen en diferentes redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="a5ebc-202">**Nodo principal SMB compartir** -monta una carpeta compartida de Windows estándar del nodo principal de hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="a5ebc-203">**Servidor NFS del nodo principal**: proporciona una solución de uso compartido de archivos para un entorno mixto de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="a5ebc-204">Almacenamiento de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="a5ebc-204">Azure File storage</span></span>
<span data-ttu-id="a5ebc-205">Hola [archivos de Azure](https://azure.microsoft.com/services/storage/files/) servicio expone recursos compartidos de archivos mediante el protocolo de SMB 2.1 estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="a5ebc-206">Máquinas virtuales de Azure y servicios en la nube pueden compartir datos de archivos a través de los componentes de la aplicación a través de recursos compartidos montados y aplicaciones locales pueden tener acceso a datos de archivos en un recurso compartido a través de la API de almacenamiento de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="a5ebc-207">Para obtener pasos detallados toocreate un archivo de Azure comparten y montar en el nodo principal de hello, consulte [Introducción al almacenamiento de archivos de Azure en Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="a5ebc-208">recurso compartido de archivos de Azure de toomount Hola Hola en nodos de Linux, consulte [cómo toouse almacenamiento de archivos de Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="a5ebc-209">tooset las conexiones persistentes, consulte [Persisting conexiones tooMicrosoft archivos de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="a5ebc-210">En el siguiente ejemplo de Hola, cree un recurso compartido de archivos de Azure en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="a5ebc-211">Hola toomount compartir en el nodo principal de hello, abra un símbolo del sistema y escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="a5ebc-212">En este ejemplo, allvhdsje es el nombre de cuenta de almacenamiento, storageaccountkey es la clave de cuenta de almacenamiento y rdma es el nombre del recurso compartido de archivos de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="a5ebc-213">recurso compartido de archivos de Azure de Hola se monta como Z: en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="a5ebc-214">recurso compartido de archivos de Azure de toomount hello en los nodos de Linux, ejecute un **clusrun** comando en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="a5ebc-215">**[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  es una útil toocarry de herramienta de HPC Pack tareas administrativas en varios nodos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="a5ebc-216">(consulte también [ClusRun para nodos de Linux](#Clusrun-for-Linux-nodes) en este artículo).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="a5ebc-217">Abra una ventana de Windows PowerShell y escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="a5ebc-218">Hola primer comando crea una carpeta denominada /rdma en todos los nodos de grupo de LinuxNodes Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="a5ebc-219">segundo comando de Hello monta hello Azure archivo recurso compartido allvhdsjw.file.core.windows.net/rdma en la carpeta de /rdma Hola con dir y el archivo too777 de conjunto de bits de modo.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="a5ebc-220">En el segundo comando hello, allvhdsje es el nombre de cuenta de almacenamiento y storageaccountkey es la clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="a5ebc-221">Hola "\\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="a5ebc-222">"\\`,"significa que Hola"," (coma) forma parte del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="a5ebc-223">Recurso compartido del nodo principal</span><span class="sxs-lookup"><span data-stu-id="a5ebc-223">Head node share</span></span>
<span data-ttu-id="a5ebc-224">Como alternativa, puede montar una carpeta compartida de nodo principal de hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="a5ebc-225">Proporciona de un recurso compartido de archivos de tooshare de manera más sencillos de hello, pero el nodo principal de Hola y todos los nodos de Linux deben implementarse en hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="a5ebc-226">Estos son los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-226">Here are hello steps.</span></span>

1. <span data-ttu-id="a5ebc-227">Cree una carpeta en el nodo principal de Hola y compartirlo tooEveryone con permisos de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="a5ebc-228">Por ejemplo, compartir D:\OpenFOAM en el nodo principal de hello como \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="a5ebc-229">Aquí CentOS7RDMA HN es nombre de host de hello del nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Permisos del recurso compartido de archivos][fileshareperms]
   
    ![Uso compartido de archivos][filesharing]
2. <span data-ttu-id="a5ebc-232">Abra una ventana de Windows PowerShell y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="a5ebc-233">Hola primer comando crea una carpeta denominada /openfoam en todos los nodos de grupo de LinuxNodes Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="a5ebc-234">segundo comando de Hello monta Hola compartido carpeta //CentOS7RDMA-HN/OpenFOAM en la carpeta de hello con dir y el archivo too777 de conjunto de bits de modo.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="a5ebc-235">Hello username y password de comando hello deben ser Hola nombre de usuario y la contraseña de un usuario del clúster en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="a5ebc-236">Consulte [Adición o eliminación de usuarios de clúster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="a5ebc-237">Hola "\\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="a5ebc-238">"\\`,"significa que Hola"," (coma) forma parte del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="a5ebc-239">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="a5ebc-239">NFS server</span></span>
<span data-ttu-id="a5ebc-240">Hola servicio NFS permite tooshare y migra archivos entre equipos que ejecutan el sistema operativo de hello Windows Server 2012 mediante el protocolo SMB de Hola y equipos basados en Linux mediante el protocolo NFS de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="a5ebc-241">Hello servidor NFS y todos los demás nodos tienen toobe implementado en hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="a5ebc-242">Proporciona mayor compatibilidad con los nodos de Linux en comparación con un recurso compartido de SMB.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="a5ebc-243">Por ejemplo, admite vínculos de archivo.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="a5ebc-244">tooinstall y configurar un servidor NFS, siga los pasos de hello en [servidor de sistema primer recurso compartido de red End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="a5ebc-245">Por ejemplo, cree un recurso compartido NFS con el nombre de nfs con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Autorización de NFS][nfsauth]
   
    ![Permisos del recurso compartido de NFS][nfsshare]
   
    ![Permisos de NTFS de NFS][nfsperm]
   
    ![Propiedades de administración de NFS][nfsmanage]
2. <span data-ttu-id="a5ebc-250">Abra una ventana de Windows PowerShell y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="a5ebc-251">Hola primer comando crea una carpeta denominada /nfsshared en todos los nodos de grupo de LinuxNodes Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="a5ebc-252">segundo comando montajes hello NFS Hello compartir HN CentOS7RDMA: / nfs en Hola carpeta.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="a5ebc-253">Aquí CentOS7RDMA HN: / nfs es la ruta de acceso remoto de Hola de su recurso compartido de NFS.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="a5ebc-254">¿Cómo toosubmit trabajos</span><span class="sxs-lookup"><span data-stu-id="a5ebc-254">How toosubmit jobs</span></span>
<span data-ttu-id="a5ebc-255">Hay clúster HPC Pack toosubmit trabajos toohello de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="a5ebc-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="a5ebc-256">Administrador de clústeres HPC o GUI del Administrador de trabajos de HPC</span><span class="sxs-lookup"><span data-stu-id="a5ebc-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="a5ebc-257">Portal web de HPC</span><span class="sxs-lookup"><span data-stu-id="a5ebc-257">HPC web portal</span></span>
* <span data-ttu-id="a5ebc-258">API de REST</span><span class="sxs-lookup"><span data-stu-id="a5ebc-258">REST API</span></span>

<span data-ttu-id="a5ebc-259">Envío de trabajos con clúster toohello en Azure a través de herramientas de interfaz gráfica de usuario de HPC Pack y el portal web de HPC Hola se Hola igual que para los nodos de proceso de Windows.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="a5ebc-260">Vea [Administrador de trabajos de HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) y [cómo toosubmit trabajos desde un equipo de cliente local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a5ebc-261">trabajos de toosubmit a través de hello API de REST, consulte demasiado[crear y enviar trabajos usando Hola API de REST en Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="a5ebc-262">toosubmit trabajos desde un cliente de Linux, consulte también toohello ejemplo de Python en hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="a5ebc-263">ClusRun para nodos de Linux</span><span class="sxs-lookup"><span data-stu-id="a5ebc-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="a5ebc-264">Hola HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) herramienta puede ser comandos tooexecute usado en nodos de Linux a través de un símbolo del sistema o administrador de clústeres HPC.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="a5ebc-265">A continuación se muestran algunos ejemplos básicos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-265">Following are some basic examples.</span></span>

* <span data-ttu-id="a5ebc-266">Mostrar nombres de usuario actuales en todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="a5ebc-267">Instalar hello **gdb** herramienta del depurador con **yum** en todos los nodos hello linuxnodes de grupo y, a continuación, reiniciar los nodos de hello después de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="a5ebc-268">Crear una secuencia de comandos de shell que mostrar cada número del 1 al 10 de un segundo en cada nodo de Linux en clúster de hello, ejecutarlo y mostrar resultados desde nodos Hola inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="a5ebc-269">Es posible que tenga toouse determinados caracteres de escape **clusrun** comandos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="a5ebc-270">Como se muestra en este ejemplo, utilice ^ en un hello tooescape de símbolo del sistema ">" símbolos.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a5ebc-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5ebc-271">Next steps</span></span>
* <span data-ttu-id="a5ebc-272">Pruebe escalado Hola clúster tooa mayor número de nodos, o ejecutar una carga de trabajo de Linux en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="a5ebc-273">Para ver un ejemplo, consulte [Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="a5ebc-274">Intente un clúster con [máquinas virtuales compatibles con RDMA, proceso intensivo](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun cargas de trabajo MPI.</span><span class="sxs-lookup"><span data-stu-id="a5ebc-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="a5ebc-275">Para ver un ejemplo, consulte [Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="a5ebc-276">Si está interesado en trabajar con nodos de Linux en un clúster de HPC Pack local, vea hello [guía TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5ebc-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png