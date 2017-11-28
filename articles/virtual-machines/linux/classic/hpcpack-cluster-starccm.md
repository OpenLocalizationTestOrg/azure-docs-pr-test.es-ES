---
title: "aaaRun estrella-CCM + con HPC Pack en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Implemente un clúster de Microsoft HPC Pack en Azure y ejecute un trabajo STAR-CCM+ en varios nodos de proceso Linux en una red RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="05078-103">Ejecución de STAR-CCM+ con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="05078-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="05078-104">Este artículo muestra cómo agrupar toodeploy un Microsoft HPC Pack en Azure y se ejecuta un [CD-adapco estrella-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) trabajo en varios nodos de ejecución de Linux que se interconectan con InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="05078-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="05078-105">Microsoft HPC Pack proporciona características toorun una variedad de HPC a gran escala y aplicaciones en paralelo, incluidas las aplicaciones de MPI, acerca de los clústeres de máquinas virtuales de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="05078-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="05078-106">HPC Pack también admite la ejecución de aplicaciones Linux HPC en máquinas virtuales de nodos de proceso Linux implementadas en un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="05078-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="05078-107">Para nodos con HPC Pack de ejecución de un toousing Introducción Linux, consulte [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="05078-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="05078-108">Configuración de un clúster de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="05078-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="05078-109">Descargar scripts de implementación de IaaS de HPC Pack Hola de hello [centro de descarga de](https://www.microsoft.com/en-us/download/details.aspx?id=44949) y extráigalos localmente.</span><span class="sxs-lookup"><span data-stu-id="05078-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="05078-110">Azure PowerShell es un requisito previo.</span><span class="sxs-lookup"><span data-stu-id="05078-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="05078-111">Si PowerShell no está configurado en el equipo local, lea el artículo de hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="05078-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="05078-112">En tiempo de Hola de redactar este artículo, las imágenes de Linux de Hola de hello Azure Marketplace (que contiene controladores de InfiniBand Hola de Azure) son para SLES 12, CentOS 6.5 y CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="05078-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="05078-113">En este artículo se basa en el uso de Hola de SLES 12.</span><span class="sxs-lookup"><span data-stu-id="05078-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="05078-114">nombre de hello tooretrieve de todas las imágenes de Linux compatibles con HPC en hello Marketplace, puede ejecutar Hola siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="05078-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="05078-115">la salida de Hello muestra la ubicación de hello en el que están disponibles estas imágenes y Hola nombre de imagen (**ImageName**) toobe utilizado en la plantilla de implementación de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="05078-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="05078-116">Antes de implementar el clúster de hello, tendrá toobuild un archivo de plantilla de implementación de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="05078-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="05078-117">Dado que estamos usando como objetivo un clúster pequeño, nodo principal de Hola se controlador de dominio de Hola y hospedar una base de datos local de SQL.</span><span class="sxs-lookup"><span data-stu-id="05078-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="05078-118">Hello plantilla siguiente se implementa este tipo de nodo principal, cree un archivo XML denominado **MyCluster.xml**y reemplace los valores de hello de **SubscriptionId**, **StorageAccount**,  **Ubicación**, **VMName**, y **ServiceName** con la suya.</span><span class="sxs-lookup"><span data-stu-id="05078-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="05078-119">Iniciar la creación del nodo principal de hello mediante la ejecución de comandos de PowerShell de hello en un símbolo del sistema con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="05078-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="05078-120">Después de 20 minutos de too30, nodo principal de hello debería estar listo.</span><span class="sxs-lookup"><span data-stu-id="05078-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="05078-121">Puede conectarse tooit desde Hola portal de Azure, haga clic en hello **conectar** icono de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="05078-122">Finalmente, es posible que tenga el reenviador de DNS de toofix Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="05078-123">toodo por lo tanto, inicie el Administrador de DNS.</span><span class="sxs-lookup"><span data-stu-id="05078-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="05078-124">Nombre del servidor secundario hello en el Administrador de DNS, seleccione **propiedades**y, a continuación, haga clic en hello **reenviadores** ficha.</span><span class="sxs-lookup"><span data-stu-id="05078-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="05078-125">Haga clic en hello **editar** tooremove los reenviadores y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="05078-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="05078-126">Asegúrese de que ese hello **usar sugerencias de raíz si los reenviadores no están disponibles** casilla de verificación está seleccionada y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="05078-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="05078-127">Configuración de nodos de proceso Linux</span><span class="sxs-lookup"><span data-stu-id="05078-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="05078-128">Implementar nodos de proceso de hello Linux mediante Hola misma plantilla de implementación que ha usado el nodo principal de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="05078-129">Archivo de copia hello **MyCluster.xml** desde el nodo principal de equipo local toohello y actualización hello **NodeCount** etiquetar con número de Hola de nodos que desea toodeploy (< = 20).</span><span class="sxs-lookup"><span data-stu-id="05078-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="05078-130">Ser toohave cuidado suficientes núcleos disponibles en su cuota de Azure, ya que cada instancia A9 consumirá 16 núcleos en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="05078-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="05078-131">Puede usar instancias de A8 (8 núcleos) en lugar de A9 si desea toouse más máquinas virtuales en hello mismo presupuesto.</span><span class="sxs-lookup"><span data-stu-id="05078-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="05078-132">En el nodo principal de hello, copie los scripts de implementación de IaaS de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="05078-133">Ejecute hello siga los comandos de PowerShell de Azure en un símbolo del sistema con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="05078-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="05078-134">Ejecutar **Add-AzureAccount** tooconnect tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="05078-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="05078-135">Si tiene varias suscripciones, ejecute **Get-AzureSubscription** toolist ellos.</span><span class="sxs-lookup"><span data-stu-id="05078-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="05078-136">Establezca una suscripción de manera predeterminada, ejecute hello **Select-AzureSubscription - SubscriptionName xxxx-predeterminado** comando.</span><span class="sxs-lookup"><span data-stu-id="05078-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="05078-137">Ejecutar **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart implementar nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="05078-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Implementación del nodo principal en acción][hndeploy]

<span data-ttu-id="05078-139">Abra la herramienta de administrador de clústeres de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="05078-140">Después de algunos minutos, normalmente los nodos de proceso Linux aparecerán en la lista de nodos de proceso del clúster.</span><span class="sxs-lookup"><span data-stu-id="05078-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="05078-141">Con el modo de implementación clásica de hello, las máquinas virtuales IaaS se crean secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="05078-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="05078-142">Por lo que si el número de Hola de nodos es importante, obtenerlas todos implementado pueden tardar una cantidad considerable de tiempo.</span><span class="sxs-lookup"><span data-stu-id="05078-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nodos Linux en el administrador de clústeres de HPC Pack][clustermanager]

<span data-ttu-id="05078-144">Ahora que todos los nodos están activados y ejecutándose en el clúster de hello, hay toomake de configuración de infraestructura adicionales.</span><span class="sxs-lookup"><span data-stu-id="05078-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="05078-145">Configuración de un recurso compartido de archivos de Azure para nodos Linux y Windows</span><span class="sxs-lookup"><span data-stu-id="05078-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="05078-146">Puede utilizar secuencias de comandos de toostore de servicios de archivos de Azure de hello, paquetes de aplicaciones y archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="05078-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="05078-147">El servicio de archivos de Azure proporciona funcionalidades CIFS en el almacenamiento de blobs de Azure como un almacén persistente.</span><span class="sxs-lookup"><span data-stu-id="05078-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="05078-148">Tenga en cuenta que esto no es la solución más escalable de hello, pero es hello uno más simple y no requiere máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="05078-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="05078-149">Crear un recurso compartido de archivos de Azure siguiendo las instrucciones de hello en el artículo hello [Introducción al almacenamiento de archivos de Azure en Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="05078-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="05078-150">Mantenga Hola nombre de la cuenta de almacenamiento como **saname**, nombre de recurso compartido de archivo hello como **sharename**y la clave de cuenta de almacenamiento de hello como **sakey**.</span><span class="sxs-lookup"><span data-stu-id="05078-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="05078-151">Montar el recurso compartido de archivos de Azure de hello en el nodo principal de Hola</span><span class="sxs-lookup"><span data-stu-id="05078-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="05078-152">Abra un símbolo del sistema con privilegios elevados y ejecute hello siguiendo las credenciales de comando toostore hello en el almacén del equipo local de hello:</span><span class="sxs-lookup"><span data-stu-id="05078-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="05078-153">A continuación, toomount hello Azure recurso compartido de archivos, ejecute:</span><span class="sxs-lookup"><span data-stu-id="05078-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="05078-154">Montar el recurso compartido de archivos de Azure de hello en nodos de proceso de Linux</span><span class="sxs-lookup"><span data-stu-id="05078-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="05078-155">Una útil herramienta que se incluye con HPC Pack es Hola clusrun.</span><span class="sxs-lookup"><span data-stu-id="05078-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="05078-156">Puede usar este Hola de toorun de herramienta de línea de comandos mismo comando simultáneamente en un conjunto de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="05078-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="05078-157">En nuestro caso, se ha utilizado el recurso compartido de archivos de Azure de Hola de toomount y enviarlo toosurvive reinicios.</span><span class="sxs-lookup"><span data-stu-id="05078-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="05078-158">En un símbolo con privilegios elevados en el nodo principal de hello, ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="05078-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="05078-159">directorio de montaje de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="05078-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="05078-160">Hola toomount recurso compartido de archivos de Azure:</span><span class="sxs-lookup"><span data-stu-id="05078-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="05078-161">recurso compartido de toopersist Hola montaje:</span><span class="sxs-lookup"><span data-stu-id="05078-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="05078-162">Instalación de STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="05078-162">Install STAR-CCM+</span></span>
<span data-ttu-id="05078-163">Las instancias A8 y A9 de máquina virtual de Azure proporcionan compatibilidad con InfiniBand y funcionalidad de RDMA.</span><span class="sxs-lookup"><span data-stu-id="05078-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="05078-164">controladores de kernel de Hola que permiten estas capacidades están disponibles para Windows Server 2012 R2, SUSE 12, CentOS 6.5 e imágenes de CentOS 7.1 en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="05078-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="05078-165">Microsoft MPI y MPI Intel (versión 5.x) son dos bibliotecas de MPI de Hola que admiten estos controladores en Azure.</span><span class="sxs-lookup"><span data-stu-id="05078-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="05078-166">Se incluyen CD-Adapco StarCCM+ versión 11.x y posteriores con la versión 5.x de Intel MPI, por lo que se proporciona compatibilidad con InfiniBand para Azure.</span><span class="sxs-lookup"><span data-stu-id="05078-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="05078-167">Obtener hello Linux64 estrella-CCM + paquete de hello [CD-adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="05078-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="05078-168">En nuestro caso, se usa la versión 11.02.010 en precisión mixta.</span><span class="sxs-lookup"><span data-stu-id="05078-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="05078-169">En el nodo principal de hello, Hola **/hpcdata** archivos de Azure compartir, cree un script de shell denominado **setupstarccm.sh** con hello siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="05078-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="05078-170">Este script se ejecutará en cada tooset de nodo de proceso una estrella-CCM + localmente.</span><span class="sxs-lookup"><span data-stu-id="05078-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="05078-171">Script setupstarcm.sh de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05078-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="05078-172">Ahora, tooset una estrella-CCM + en todos los Linux nodos de proceso, abra un símbolo del sistema con privilegios elevados y ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="05078-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="05078-173">Mientras se ejecuta el comando de hello, puede supervisar el uso de CPU de hello mediante mapa térmico de hello del Administrador de clústeres.</span><span class="sxs-lookup"><span data-stu-id="05078-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="05078-174">Tras unos minutos todos los nodos deberían estar correctamente configurados.</span><span class="sxs-lookup"><span data-stu-id="05078-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="05078-175">Ejecución de trabajos de STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="05078-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="05078-176">HPC Pack se utiliza para sus capacidades de programador de trabajo en orden toorun estrella-CCM + trabajos.</span><span class="sxs-lookup"><span data-stu-id="05078-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="05078-177">toodo por lo tanto, se necesitamos Hola soporte técnico de algunos scripts que son utilizados toostart trabajo de Hola y ejecute estrella-CCM +.</span><span class="sxs-lookup"><span data-stu-id="05078-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="05078-178">datos de entrada de Hola se mantienen en el recurso compartido de archivos de Azure de hello primeros por simplicidad.</span><span class="sxs-lookup"><span data-stu-id="05078-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="05078-179">Hola siguiente script de PowerShell es tooqueue usa una estrella-CCM + trabajo.</span><span class="sxs-lookup"><span data-stu-id="05078-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="05078-180">Toma tres argumentos:</span><span class="sxs-lookup"><span data-stu-id="05078-180">It takes three arguments:</span></span>

* <span data-ttu-id="05078-181">nombre del modelo Hola</span><span class="sxs-lookup"><span data-stu-id="05078-181">hello model name</span></span>
* <span data-ttu-id="05078-182">número de Hola de toobe de nodos que se usa</span><span class="sxs-lookup"><span data-stu-id="05078-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="05078-183">número de Hola de núcleos en cada toobe de nodo que se usa</span><span class="sxs-lookup"><span data-stu-id="05078-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="05078-184">Dado que estrella-CCM + puede rellenar ancho de banda de memoria de hello, es mejor toouse menos núcleos por nodos de proceso y agregar nuevos nodos.</span><span class="sxs-lookup"><span data-stu-id="05078-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="05078-185">Hola número exacto de núcleos por nodo dependerá de familia del procesador hello y velocidad de interconexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="05078-186">nodos de Hola se asignan exclusivamente para el trabajo de hello y no puede compartirse con otros trabajos.</span><span class="sxs-lookup"><span data-stu-id="05078-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="05078-187">trabajo de Hello no se inicia como un trabajo de MPI directamente.</span><span class="sxs-lookup"><span data-stu-id="05078-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="05078-188">Hola **runstarccm.sh** secuencia de comandos de shell iniciará el selector MPI Hola.</span><span class="sxs-lookup"><span data-stu-id="05078-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="05078-189">Hola entrada hello y modelo **runstarccm.sh** script se almacenan en hello **/hpcdata** recurso compartido al que previamente se ha montado.</span><span class="sxs-lookup"><span data-stu-id="05078-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="05078-190">Archivos de registro se denominan con el Id. de trabajo de Hola y se almacenan en hello **/hpcdata share**, junto con hello estrella-CCM + archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="05078-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="05078-191">Script SubmitStarccmJob.ps1 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05078-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="05078-192">Reemplace **runner.java** por el iniciador de modelo Java de STAR-CCM+ y el código de registro que prefiera.</span><span class="sxs-lookup"><span data-stu-id="05078-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="05078-193">Script runstarccm.sh de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05078-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="05078-194">En nuestra prueba, se ha utilizado un token de licencia Power-On-Demand.</span><span class="sxs-lookup"><span data-stu-id="05078-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="05078-195">Para ese token, deberá hello tooset **$CDLMD_LICENSE_FILE** variable de entorno demasiado **1999@flex.cd-adapco.com**  y la clave de Hola Hola **- podkey** opción de línea de comandos de Hola .</span><span class="sxs-lookup"><span data-stu-id="05078-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="05078-196">Después de algunas operaciones de inicialización, el script de Hola extrae--hello **CCP_NODES_CORES $** variables de entorno que establezca HPC Pack: Hola lista de toobuild de nodos que se usa un archivo de host que Hola selector MPI.</span><span class="sxs-lookup"><span data-stu-id="05078-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="05078-197">Este archivo de host contendrá la lista de Hola de nombres del nodo de proceso que se usan para el trabajo de hello, un nombre por línea.</span><span class="sxs-lookup"><span data-stu-id="05078-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="05078-198">formato de Hola de **CCP_NODES_CORES $** sigue este patrón:</span><span class="sxs-lookup"><span data-stu-id="05078-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="05078-199">Donde:</span><span class="sxs-lookup"><span data-stu-id="05078-199">Where:</span></span>

* <span data-ttu-id="05078-200">`<Number of nodes>`es el número de Hola de nodos asignados toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="05078-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="05078-201">`<Name of node_n_...>`es el nombre de Hola de cada nodo asignada toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="05078-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="05078-202">`<Cores of node_n_...>`es el número de Hola de núcleos en el nodo de hello asignada toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="05078-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="05078-203">número de núcleos de Hola (**$NBCORES**) también es calculada hello en función de número de nodos (**$NBNODES**) y Hola número de núcleos por nodo (proporcionado como parámetro **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="05078-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="05078-204">Para ver opciones de MPI hello, hello las que se utilizan con Intel MPI en Azure son:</span><span class="sxs-lookup"><span data-stu-id="05078-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="05078-205">`-mpi intel`toospecify MPI de Intel.</span><span class="sxs-lookup"><span data-stu-id="05078-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="05078-206">`-fabric UDAPL`toouse Azure InfiniBand verbos.</span><span class="sxs-lookup"><span data-stu-id="05078-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="05078-207">`-cpubind bandwidth,v`ancho de banda de toooptimize de MPI con estrella-CCM +.</span><span class="sxs-lookup"><span data-stu-id="05078-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="05078-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI trabajar con Azure InfiniBand y tooset Hola requiere el número de núcleos por nodo.</span><span class="sxs-lookup"><span data-stu-id="05078-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="05078-209">`-batch`toostart estrella-CCM + en modo por lotes con ninguna interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="05078-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="05078-210">Por último, toostart un trabajo, asegúrese de que los nodos estén en ejecución y que están en línea en el Administrador de clústeres.</span><span class="sxs-lookup"><span data-stu-id="05078-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="05078-211">Después, desde un símbolo del sistema de PowerShell, ejecute esto:</span><span class="sxs-lookup"><span data-stu-id="05078-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="05078-212">Detención de nodos</span><span class="sxs-lookup"><span data-stu-id="05078-212">Stop nodes</span></span>
<span data-ttu-id="05078-213">Más adelante cuando haya terminado con las pruebas, puede usar hello después toostop de comandos de PowerShell de HPC Pack e iniciar nodos:</span><span class="sxs-lookup"><span data-stu-id="05078-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="05078-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05078-214">Next steps</span></span>
<span data-ttu-id="05078-215">Pruebe a ejecutar otras cargas de trabajo Linux.</span><span class="sxs-lookup"><span data-stu-id="05078-215">Try running other Linux workloads.</span></span> <span data-ttu-id="05078-216">Por ejemplo, consulte:</span><span class="sxs-lookup"><span data-stu-id="05078-216">For example, see:</span></span>

* [<span data-ttu-id="05078-217">Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="05078-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="05078-218">Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="05078-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
