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
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Crear un clúster de informática de alto rendimiento (HPC) de Windows con script de implementación de IaaS de HPC Pack Hola
Ejecute toodeploy de secuencia de comandos de PowerShell de hello IaaS de HPC Pack implementación en un clúster de HPC Pack 2012 R2 completando para las cargas de trabajo de Windows en máquinas virtuales de Azure. Hola clúster está formado por un nodo principal unido a Active Directory con Windows Server y Microsoft HPC Pack y especifica los recursos de cálculo de Windows adicionales. Si desea toodeploy un clúster de HPC Pack en Azure para las cargas de trabajo de Linux, consulte [crear un clúster de HPC de Linux con hello script de implementación de IaaS de HPC Pack](../../linux/classic/hpcpack-cluster-powershell-script.md). También puede utilizar un toodeploy de plantilla un clúster de HPC Pack de Azure Resource Manager. Para ver ejemplos, consulte [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) (Creación de un clúster de HPC) y [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/) (Creación de un clúster de HPC con una imagen de nodo de proceso personalizado).

> [!IMPORTANT] 
> Hola script de PowerShell descrito en este artículo crea un clúster de Microsoft HPC Pack 2012 R2 en Azure con el modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.
> Además, script de Hola descrito en este artículo no es compatible con HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Archivos de configuración de ejemplo
En hello en los ejemplos siguientes, sustitúyalo por sus propios valores para el Id. de suscripción o nombre y los nombres de cuenta y el servicio de Hola.

### <a name="example-1"></a>Ejemplo 1
Hello archivo de configuración siguiente implementa un clúster de HPC Pack que tiene cinco nodos de proceso que ejecutan el sistema operativo de Windows Server 2012 R2 de Hola y de un nodo principal con bases de datos locales. Todos los servicios de nube de Hola se crean directamente en hello ubicación oeste de Estados Unidos. nodo principal de Hello actúa como controlador de dominio del bosque de dominio de Hola.

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

### <a name="example-2"></a>Ejemplo 2
Hola, el archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente. clúster de Hello tiene 1 nodo principal con bases de datos locales y 12 nodos con hello extensión BGInfo VM aplicada de ejecución.
Instalación automática de actualizaciones de Windows está deshabilitada para hello todas las máquinas virtuales en el bosque de dominio de Hola. Todos los servicios de nube de Hola se crean directamente en la ubicación de Asia oriental. se crean nodos de proceso de Hello en tres servicios en la nube y tres cuentas de almacenamiento: *MyHPCCN-0001* demasiado*MyHPCCN-0005* en *MyHPCCNService01* y  *mycnstorage01*; *MyHPCCN-0006* demasiado*MyHPCCN0010* en *MyHPCCNService02* y *mycnstorage02*; y  *MyHPCCN-0011* demasiado*MyHPCCN-0012* en *MyHPCCNService03* y *mycnstorage03*). nodos de proceso de Hola se crean a partir de una imagen privada existente que se capturó de un nodo de proceso. aumentar Hello automático y reducir está habilitado el servicio no tiene valor predeterminado aumentar y reducir los intervalos.

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

### <a name="example-3"></a>Ejemplo 3
Hola, el archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente. clúster de Hello contiene un nodo principal, un servidor de base de datos con un disco de datos de 500 GB, dos nodos de agente que ejecutan el sistema operativo de Windows Server 2012 R2 de Hola y cinco nodos de proceso que ejecutan el sistema operativo de Windows Server 2012 R2 de Hola. Hola servicio en la nube MyHPCCNService se crea en el grupo de afinidad de hello *MyIBAffinityGroup*, y otros servicios de nube hello se crean una en el grupo de afinidad de hello *MyAffinityGroup*. Hola API de REST de programador de trabajos de HPC y el portal web de HPC están habilitadas en el nodo principal de Hola.

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



### <a name="example-4"></a>Ejemplo 4
Hola, el archivo de configuración siguiente implementa un clúster de HPC Pack en un bosque de dominio existente. clúster de Hello tiene dos nodos principal con bases de datos locales, se crean dos plantillas de nodo de Azure y se crean tres nodos de Azure Media de tamaño para la plantilla de nodo de Azure *AzureTemplate1*. Un archivo de script se ejecuta en el nodo principal de hello después de configura el nodo principal de Hola.

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

## <a name="troubleshooting"></a>Solución de problemas
* **Error "No existe la red virtual"** -si ejecuta Hola script toodeploy varios clústeres en Azure simultáneamente en una suscripción, pueden producir un error en una o más implementaciones con error de Hola "red virtual *VNet\_nombre* no existe".
  Si se produce este error, ejecute el script de Hola nuevo para la implementación de hello error.
* **Problema de tener acceso a Hola Internet desde la red virtual de Azure de Hola** : si crear un clúster con un nuevo controlador de dominio mediante el uso de script de implementación de hello, o promover manualmente un controlador de toodomain de máquina virtual de nodo principal, puede experimentar problemas conectar máquinas virtuales de hello toohello Internet. Este problema puede producirse si un servidor reenviador DNS se configura automáticamente en el controlador de dominio de Hola y este servidor no se puede resolver correctamente.
  
    toowork resolver este problema, inicie sesión en el controlador de dominio de toohello y cualquier opción de configuración de reenviador de Hola de quitar o configurar un servidor reenviador DNS válido. tooconfigure esta configuración, en el administrador del servidor, haga clic en **herramientas** >
    **DNS** tooopen Administrador de DNS y, a continuación, haga doble clic en **reenviadores**.
* **Problema de acceso a la red RDMA desde máquinas virtuales de proceso intensivo** : Si Agregar proceso de Windows Server o nodo de broker de máquinas virtuales con un compatibles con RDMA tamaño como A8 o A9, puede experimentar problemas al conectar esas máquinas virtuales de red toohello RDMA aplicación. Este problema se produce uno de los motivos es si Hola extensión HpcVmDrivers no está instalada correctamente cuando hello las máquinas virtuales se agregan toohello clúster. Por ejemplo, la extensión podría bloquearse en hello estado de instalación.
  
    toowork resolver este problema, el primer estado de Hola de comprobación de extensión de hello en máquinas virtuales de Hola. Si la extensión de hello no está instalada correctamente, intente eliminar nodos de Hola de clúster de HPC de hello y, a continuación, agregar nodos de Hola de nuevo. Por ejemplo, puede agregar máquinas virtuales de nodos de proceso mediante la ejecución de secuencias de comandos de Add-HpcIaaSNode.ps1 hello en el nodo principal de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Intentar ejecutar una carga de trabajo de prueba en clúster de Hola. Para obtener un ejemplo, vea Hola HPC Pack [Guía de introducción](https://technet.microsoft.com/library/jj884144).
* Para un tutorial tooscript Hola la implementación de clúster y ejecutar una carga de trabajo HPC, vea [empezar a trabajar con un clúster de HPC Pack en cargas de trabajo de Excel y SOA de Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Intente toostart de herramientas de HPC Pack, detener, agregar y quitar nodos de proceso de un clúster que cree. Consulte [Administración de nodos de proceso en un clúster de HPC Pack en Azure](hpcpack-cluster-node-manage.md).
* tooget configurar el clúster de toosubmit trabajos toohello desde un equipo local, vea [clúster de trabajos de HPC enviar desde un tooan de equipo local HPC Pack en Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

