---
title: "clúster de Windows HPC aaaPowerShell script toodeploy | Documentos de Microsoft"
description: "Ejecutar un toodeploy de secuencia de comandos de PowerShell en un clúster de Windows HPC Pack 2012 R2 en máquinas virtuales de Azure"
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
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="275d0-103">Crear un clúster de informática de alto rendimiento (HPC) de Windows con script de implementación de IaaS de HPC Pack Hola</span><span class="sxs-lookup"><span data-stu-id="275d0-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="275d0-104">Ejecute toodeploy de secuencia de comandos de PowerShell de hello IaaS de HPC Pack implementación en un clúster de HPC Pack 2012 R2 completando para las cargas de trabajo de Windows en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="275d0-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="275d0-105">Hola clúster está formado por un nodo principal unido a Active Directory con Windows Server y Microsoft HPC Pack y especifica los recursos de cálculo de Windows adicionales.</span><span class="sxs-lookup"><span data-stu-id="275d0-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="275d0-106">Si desea toodeploy un clúster de HPC Pack en Azure para las cargas de trabajo de Linux, consulte [crear un clúster de HPC de Linux con hello script de implementación de IaaS de HPC Pack](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="275d0-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="275d0-107">También puede utilizar un toodeploy de plantilla un clúster de HPC Pack de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="275d0-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="275d0-108">Para ver ejemplos, consulte [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) (Creación de un clúster de HPC) y [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/) (Creación de un clúster de HPC con una imagen de nodo de proceso personalizado).</span><span class="sxs-lookup"><span data-stu-id="275d0-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="275d0-109">Hola script de PowerShell descrito en este artículo crea un clúster de Microsoft HPC Pack 2012 R2 en Azure con el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="275d0-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="275d0-111">Además, script de Hola descrito en este artículo no es compatible con HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="275d0-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="275d0-112">Archivos de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="275d0-112">Example configuration files</span></span>
<span data-ttu-id="275d0-113">En hello en los ejemplos siguientes, sustitúyalo por sus propios valores para el Id. de suscripción o nombre y los nombres de cuenta y el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="275d0-114">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="275d0-114">Example 1</span></span>
<span data-ttu-id="275d0-115">Hello archivo de configuración siguiente implementa un clúster de HPC Pack que tiene cinco nodos de proceso que ejecutan el sistema operativo de Windows Server 2012 R2 de Hola y de un nodo principal con bases de datos locales.</span><span class="sxs-lookup"><span data-stu-id="275d0-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="275d0-116">Todos los servicios de nube de Hola se crean directamente en hello ubicación oeste de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="275d0-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="275d0-117">nodo principal de Hello actúa como controlador de dominio del bosque de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-117">hello head node acts as domain controller of hello domain forest.</span></span>

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

### <a name="example-2"></a><span data-ttu-id="275d0-118">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="275d0-118">Example 2</span></span>
<span data-ttu-id="275d0-119">Hola, el archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente.</span><span class="sxs-lookup"><span data-stu-id="275d0-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="275d0-120">clúster de Hello tiene 1 nodo principal con bases de datos locales y 12 nodos con hello extensión BGInfo VM aplicada de ejecución.</span><span class="sxs-lookup"><span data-stu-id="275d0-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="275d0-121">Instalación automática de actualizaciones de Windows está deshabilitada para hello todas las máquinas virtuales en el bosque de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="275d0-122">Todos los servicios de nube de Hola se crean directamente en la ubicación de Asia oriental.</span><span class="sxs-lookup"><span data-stu-id="275d0-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="275d0-123">se crean nodos de proceso de Hello en tres servicios en la nube y tres cuentas de almacenamiento: *MyHPCCN-0001* demasiado*MyHPCCN-0005* en *MyHPCCNService01* y  *mycnstorage01*; *MyHPCCN-0006* demasiado*MyHPCCN0010* en *MyHPCCNService02* y *mycnstorage02*; y  *MyHPCCN-0011* demasiado*MyHPCCN-0012* en *MyHPCCNService03* y *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="275d0-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="275d0-124">nodos de proceso de Hola se crean a partir de una imagen privada existente que se capturó de un nodo de proceso.</span><span class="sxs-lookup"><span data-stu-id="275d0-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="275d0-125">aumentar Hello automático y reducir está habilitado el servicio no tiene valor predeterminado aumentar y reducir los intervalos.</span><span class="sxs-lookup"><span data-stu-id="275d0-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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

### <a name="example-3"></a><span data-ttu-id="275d0-126">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="275d0-126">Example 3</span></span>
<span data-ttu-id="275d0-127">Hola, el archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente.</span><span class="sxs-lookup"><span data-stu-id="275d0-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="275d0-128">clúster de Hello contiene un nodo principal, un servidor de base de datos con un disco de datos de 500 GB, dos nodos de agente que ejecutan el sistema operativo de Windows Server 2012 R2 de Hola y cinco nodos de proceso que ejecutan el sistema operativo de Windows Server 2012 R2 de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="275d0-129">Hola servicio en la nube MyHPCCNService se crea en el grupo de afinidad de hello *MyIBAffinityGroup*, y otros servicios de nube hello se crean una en el grupo de afinidad de hello *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="275d0-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="275d0-130">Hola API de REST de programador de trabajos de HPC y el portal web de HPC están habilitadas en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

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



### <a name="example-4"></a><span data-ttu-id="275d0-131">Ejemplo 4</span><span class="sxs-lookup"><span data-stu-id="275d0-131">Example 4</span></span>
<span data-ttu-id="275d0-132">Hola, el archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente.</span><span class="sxs-lookup"><span data-stu-id="275d0-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="275d0-133">clúster de Hello tiene dos nodos principal con bases de datos locales, se crean dos plantillas de nodo de Azure y se crean tres nodos de Azure Media de tamaño para la plantilla de nodo de Azure *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="275d0-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="275d0-134">Un archivo de script se ejecuta en el nodo principal de hello después de configura el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-134">A script file runs on hello head node after hello head node is configured.</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="275d0-135">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="275d0-135">Troubleshooting</span></span>
* <span data-ttu-id="275d0-136">**Error "No existe la red virtual"** -si ejecuta Hola script toodeploy varios clústeres en Azure simultáneamente en una suscripción, pueden producir un error en una o más implementaciones con error de Hola "red virtual *VNet\_nombre* no existe".</span><span class="sxs-lookup"><span data-stu-id="275d0-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="275d0-137">Si se produce este error, ejecute el script de Hola nuevo para la implementación de hello error.</span><span class="sxs-lookup"><span data-stu-id="275d0-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="275d0-138">**Problema de tener acceso a Hola Internet desde la red virtual de Azure de Hola** : si crear un clúster con un nuevo controlador de dominio mediante el uso de script de implementación de hello, o promover manualmente un controlador de toodomain de máquina virtual de nodo principal, puede experimentar problemas conectar máquinas virtuales de hello toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="275d0-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="275d0-139">Este problema puede producirse si un servidor reenviador DNS se configura automáticamente en el controlador de dominio de Hola y este servidor no se puede resolver correctamente.</span><span class="sxs-lookup"><span data-stu-id="275d0-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="275d0-140">toowork resolver este problema, inicie sesión en el controlador de dominio de toohello y cualquier opción de configuración de reenviador de Hola de quitar o configurar un servidor reenviador DNS válido.</span><span class="sxs-lookup"><span data-stu-id="275d0-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="275d0-141">tooconfigure esta configuración, en el administrador del servidor, haga clic en **herramientas** >
    **DNS** tooopen Administrador de DNS y, a continuación, haga doble clic en **reenviadores**.</span><span class="sxs-lookup"><span data-stu-id="275d0-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="275d0-142">**Problema de acceso a la red RDMA desde máquinas virtuales de proceso intensivo** : Si Agregar proceso de Windows Server o nodo de broker de máquinas virtuales con un compatibles con RDMA tamaño como A8 o A9, puede experimentar problemas al conectar esas máquinas virtuales de red toohello RDMA aplicación.</span><span class="sxs-lookup"><span data-stu-id="275d0-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="275d0-143">Este problema se produce uno de los motivos es si Hola extensión HpcVmDrivers no está instalada correctamente cuando hello las máquinas virtuales se agregan toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="275d0-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="275d0-144">Por ejemplo, la extensión podría bloquearse en hello estado de instalación.</span><span class="sxs-lookup"><span data-stu-id="275d0-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="275d0-145">toowork resolver este problema, el primer estado de Hola de comprobación de extensión de hello en máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="275d0-146">Si la extensión de hello no está instalada correctamente, intente eliminar nodos de Hola de clúster de HPC de hello y, a continuación, agregar nodos de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="275d0-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="275d0-147">Por ejemplo, puede agregar máquinas virtuales de nodos de proceso mediante la ejecución de secuencias de comandos de Add-HpcIaaSNode.ps1 hello en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="275d0-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="275d0-148">Next steps</span></span>
* <span data-ttu-id="275d0-149">Intentar ejecutar una carga de trabajo de prueba en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="275d0-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="275d0-150">Para obtener un ejemplo, vea Hola HPC Pack [Guía de introducción](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="275d0-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="275d0-151">Para un tutorial tooscript Hola la implementación de clúster y ejecutar una carga de trabajo HPC, vea [empezar a trabajar con un clúster de HPC Pack en cargas de trabajo de Excel y SOA de Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="275d0-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="275d0-152">Intente toostart de herramientas de HPC Pack, detener, agregar y quitar nodos de proceso de un clúster que cree.</span><span class="sxs-lookup"><span data-stu-id="275d0-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="275d0-153">Consulte [Administración de nodos de proceso en un clúster de HPC Pack en Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="275d0-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="275d0-154">tooget configurar el clúster de toosubmit trabajos toohello desde un equipo local, vea [clúster de trabajos de HPC enviar desde un tooan de equipo local HPC Pack en Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="275d0-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

