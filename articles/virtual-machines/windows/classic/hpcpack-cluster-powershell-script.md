---
title: "Script de PowerShell para implementar un clúster de Windows HPC | Microsoft Docs"
description: "Ejecución de un script de PowerShell para implementar un clúster de HPC Pack 2012 R2 de Windows completo en máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 85b125ab19671b61d2541af6378c95feb88bf952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="6e7b1-103">Creación de un clúster de proceso de alto rendimiento (HPC) de Windows con el script de implementación de HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="6e7b1-103">Create a Windows high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="6e7b1-104">Ejecute el script de PowerShell de implementación de HPC Pack IaaS para implementar un clúster de HPC Pack 2012 R2 completo para cargas de trabajo Windows en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="6e7b1-105">El clúster consta de un nodo principal unido a Active Directory en el que se ejecuta Windows Server y Microsoft HPC Pack, y los recursos de cálculo de Windows adicionales que especifique.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="6e7b1-106">Si desea implementar un clúster de HPC Pack en Azure para cargas de trabajo de Linux, consulte [Creación de un clúster de informática de alto rendimiento (HPC) en máquinas virtuales de Linux con el script de implementación de HPC Pack IaaS](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="6e7b1-106">If you want to deploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with the HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="6e7b1-107">También puede usar una plantilla del Administrador de recursos de Azure para implementar un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="6e7b1-108">Para ver ejemplos, consulte [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) (Creación de un clúster de HPC) y [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/) (Creación de un clúster de HPC con una imagen de nodo de proceso personalizado).</span><span class="sxs-lookup"><span data-stu-id="6e7b1-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6e7b1-109">El script de PowerShell que se describe en este artículo crea un clúster de Microsoft HPC Pack 2012 R2 en Azure mediante el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="6e7b1-110">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="6e7b1-111">Además, el script que se describe en este artículo no es compatible con HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="6e7b1-112">Archivos de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6e7b1-112">Example configuration files</span></span>
<span data-ttu-id="6e7b1-113">En los siguientes ejemplos, sustituya por sus propios valores el nombre o la identificación de la suscripción y los nombres de cuenta y servicio.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-113">In the following examples, substitute your own values for your subscription Id or name and the account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="6e7b1-114">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="6e7b1-114">Example 1</span></span>
<span data-ttu-id="6e7b1-115">El siguiente archivo de configuración implementa un clúster de HPC Pack que tiene un nodo principal con bases de datos locales y cinco nodos de proceso que ejecutan el sistema operativo Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-115">The following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="6e7b1-116">Todos los servicios en la nube se crean directamente en la ubicación oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-116">All the cloud services are created directly in the West US location.</span></span> <span data-ttu-id="6e7b1-117">El nodo principal actúa como controlador de dominio del bosque de dominio.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-117">The head node acts as domain controller of the domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="6e7b1-118">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="6e7b1-118">Example 2</span></span>
<span data-ttu-id="6e7b1-119">El archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-119">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="6e7b1-120">El clúster tiene un nodo principal con bases de datos locales y 12 nodos de proceso con la extensión de máquina virtual BGInfo aplicada.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-120">The cluster has 1 head node with local databases and 12 compute nodes with the BGInfo VM extension applied.</span></span>
<span data-ttu-id="6e7b1-121">La instalación automática de actualizaciones de Windows está deshabilitada para todas las máquinas virtuales en el bosque de dominio.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-121">Automatic installation of Windows updates is disabled for all the VMs in the domain forest.</span></span> <span data-ttu-id="6e7b1-122">Todos los servicios en la nube se crean directamente en la ubicación de Este de Asia.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-122">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="6e7b1-123">Los nodos de proceso se crean en tres servicios en la nube y tres cuentas de almacenamiento: de *MyHPCCN-0001* a *MyHPCCN-0005* en *MyHPCCNService01* y *mycnstorage01*; de *MyHPCCN-0006* a *MyHPCCN0010* en *MyHPCCNService02* y *mycnstorage02*; y de *MyHPCCN-0011* a *MyHPCCN-0012* en *MyHPCCNService03* y *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="6e7b1-123">The compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* to *MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* to *MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* to *MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="6e7b1-124">Los nodos de proceso se crean a partir de una imagen privada existente capturada desde un nodo de proceso.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-124">The compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="6e7b1-125">El servicio de crecimiento y reducción automático está habilitado con intervalos de crecimiento y reducción predeterminados.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-125">The auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="6e7b1-126">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="6e7b1-126">Example 3</span></span>
<span data-ttu-id="6e7b1-127">El archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-127">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="6e7b1-128">El clúster contiene un nodo principal, un servidor de bases de datos con un disco de datos de 500 GB, dos nodos de agente que ejecutan el sistema operativo Windows Server 2012 R2 y cinco nodos de proceso que ejecutan el sistema operativo Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-128">The cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running the Windows Server 2012 R2 operating system, and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="6e7b1-129">El servicio en la nube MyHPCCNService se crea en el grupo de afinidad *MyIBAffinityGroup*, mientras que los restantes servicios en la nube se crean en el grupo de afinidad *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-129">The cloud service MyHPCCNService is created in the affinity group *MyIBAffinityGroup*, and the other cloud services are created in the affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="6e7b1-130">La API de REST del Programador de trabajos de HPC y el portal web de HPC están habilitados en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-130">The HPC Job Scheduler REST API and HPC web portal are enabled on the head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="6e7b1-131">Ejemplo 4</span><span class="sxs-lookup"><span data-stu-id="6e7b1-131">Example 4</span></span>
<span data-ttu-id="6e7b1-132">El archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-132">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="6e7b1-133">El clúster tiene dos nodos principales con bases de datos locales y se crean dos plantillas de nodo de Azure y tres nodos de Azure de tamaño medio para la plantilla de nodo *AzureTemplate1*de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-133">The cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="6e7b1-134">Se ejecuta un archivo de script en el nodo principal después de configurar este nodo.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-134">A script file runs on the head node after the head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="6e7b1-135">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="6e7b1-135">Troubleshooting</span></span>
* <span data-ttu-id="6e7b1-136">**Error "La red virtual no existe"**: si ejecuta el script para implementar varios clústeres en Azure simultáneamente con una única suscripción, puede producirse un error de "La red virtual *Nombre de\_red virtual* no existe" en una implementación o varias.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-136">**“VNet doesn’t exist” error** - If you run the script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="6e7b1-137">Si se produce este error, vuelva a ejecutar el script para la implementación en la que ocurrió el error.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-137">If this error occurs, run the script again for the failed deployment.</span></span>
* <span data-ttu-id="6e7b1-138">**Problemas de acceso a Internet desde la red virtual de Azure** : si crea un clúster con un nuevo controlador de dominio mediante el script de implementación o promueve manualmente una máquina virtual del nodo principal a un controlador de dominio, puede experimentar problemas al conectar las máquinas virtuales a Internet.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-138">**Problem accessing the Internet from the Azure virtual network** - If you create a cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs to the Internet.</span></span> <span data-ttu-id="6e7b1-139">Este problema puede ocurrir si se configura automáticamente un servidor de reenviador DNS en el controlador de dominio y este servidor de reenviador DNS no se resuelve correctamente.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-139">This problem can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="6e7b1-140">Para evitar este problema, inicie sesión en el controlador de dominio y, o bien, quite la configuración de reenviador, o bien, configure un servidor de reenviador DNS válida.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-140">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="6e7b1-141">Para configurar esta opción, en Administrador del servidor, haga clic **Herramientas** >
    **DNS** para abrir el Administrador de DNS y, a continuación, haga doble clic en **Reenviadores**.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-141">To configure this setting, in Server Manager click **Tools** >
    **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="6e7b1-142">**Problemas de acceso a la red RDMA desde máquinas virtuales de proceso intensivo** : si agrega máquinas virtuales de nodo de agente o de nodo de proceso de Windows Server mediante un tamaño compatible con RDMA, como A8 o A9, puede experimentar problemas para conectar estas máquinas virtuales a la red de aplicación RDMA.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs to the RDMA application network.</span></span> <span data-ttu-id="6e7b1-143">Una razón por la que puede ocurrir esto es que la extensión HpcVmDrivers no esté correctamente instalada cuando las máquinas virtuales se agregan al clúster.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-143">One reason this problem occurs is if the HpcVmDrivers extension is not properly installed when the VMs are added to the cluster.</span></span> <span data-ttu-id="6e7b1-144">Por ejemplo, la extensión puede bloquearse en el estado de instalación.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-144">For example, the extension might be stuck in the installing state.</span></span>
  
    <span data-ttu-id="6e7b1-145">Para evitar este problema, compruebe primero el estado de la extensión en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-145">To work around this problem, first check the state of the extension in the VMs.</span></span> <span data-ttu-id="6e7b1-146">Si la extensión no está instalada correctamente, intente quitar los nodos del clúster de HPC y, a continuación, vuelva a agregarlos.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-146">If the extension is not properly installed, try removing the nodes from the HPC cluster and then add the nodes again.</span></span> <span data-ttu-id="6e7b1-147">Por ejemplo, puede agregar máquinas virtuales de nodos de proceso mediante la ejecución del script Add-HpcIaaSNode.ps1 en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-147">For example, you can add compute node VMs by running the Add-HpcIaaSNode.ps1 script on the head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e7b1-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e7b1-148">Next steps</span></span>
* <span data-ttu-id="6e7b1-149">Pruebe a ejecutar una carga de trabajo de prueba en el clúster.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-149">Try running a test workload on the cluster.</span></span> <span data-ttu-id="6e7b1-150">Para obtener un ejemplo, consulte la [guía de introducción](https://technet.microsoft.com/library/jj884144)de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-150">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="6e7b1-151">Para ver un tutorial sobre cómo crear un script de implementación del clúster y ejecutar una carga de trabajo de HPC, consulte [Introducción a un clúster de HPC Pack en Azure para ejecutar cargas de trabajo de Excel y SOA](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e7b1-151">For a tutorial to script the cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="6e7b1-152">Pruebe las herramientas de HPC Pack para iniciar, detener, agregar y quitar nodos de proceso de un clúster creado.</span><span class="sxs-lookup"><span data-stu-id="6e7b1-152">Try HPC Pack's tools to start, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="6e7b1-153">Consulte [Administración de nodos de proceso en un clúster de HPC Pack en Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="6e7b1-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="6e7b1-154">Para configurar el envío de trabajos al clúster desde un equipo local, consulte [Envío de trabajos HPC desde un equipo local a un clúster de HPC Pack implementado en Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e7b1-154">To get set up to submit jobs to the cluster from a local computer, see [Submit HPC jobs from an on-premises computer to an HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

