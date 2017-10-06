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
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Crear un clúster de informática de alto rendimiento (HPC) de Linux con script de implementación de IaaS de HPC Pack Hola
Ejecute toodeploy de secuencia de comandos de PowerShell de hello IaaS de HPC Pack implementación en un clúster de HPC Pack 2012 R2 completando para las cargas de trabajo de Linux en máquinas virtuales de Azure. clúster de Hello consta de un nodo principal unido a Active Directory con Windows Server y Microsoft HPC Pack y nodos de proceso que ejecutan uno de hello las distribuciones de Linux compatibles con HPC Pack. Si desea toodeploy un clúster de HPC Pack en las cargas de trabajo de Azure para Windows, vea [crear un clúster de HPC de Windows con hello script de implementación de IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). También puede utilizar un toodeploy de plantilla un clúster de HPC Pack de Azure Resource Manager. Si desea consultar un ejemplo, consulte [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)(Creación de un clúster de HPC con nodos de proceso de Linux).

> [!IMPORTANT] 
> Hola script de PowerShell descrito en este artículo crea un clúster de Microsoft HPC Pack 2012 R2 en Azure con el modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.
> Además, script de Hola descrito en este artículo no es compatible con HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Archivos de configuración de ejemplo
Hello siguiente archivo de configuración crea un controlador de dominio y un bosque de dominio e implementa un clúster de HPC Pack que tiene un nodo principal con bases de datos locales y 10 nodos de proceso de Linux. Todos los servicios de nube de Hola se crean directamente en la ubicación de Asia oriental Hola. Hello nodos de proceso de Linux en se crean dos servicios en la nube y dos cuentas de almacenamiento (es decir, *MyLnxCN-0001* a *MyLnxCN-0005* en *MyLnxCNService01* y *mylnxstorage01*, y *MyLnxCN-0006* a *MyLnxCN-0010* en *MyLnxCNService02* y *mylnxstorage02* ). nodos de proceso de Hola se crean a partir de una imagen de Linux de OpenLogic CentOS versión 7.0. 

Utilizar sus propios valores para el nombre de la suscripción y los nombres de cuenta y el servicio de Hola.

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
## <a name="troubleshooting"></a>Solución de problemas
* **Error "La red virtual no existe"**. Si ejecuta toodeploy de script de implementación de IaaS de HPC Pack Hola varios clústeres en Azure simultáneamente en una suscripción, pueden producir un error en una o más implementaciones con error de Hola "red virtual *VNet\_nombre* no existe".
  Si se produce este error, vuelva a ejecutar script de Hola para la implementación de hello error.
* **Problema de tener acceso a Hola Internet desde la red virtual de Azure de hello**. Si crea un clúster de HPC Pack con un nuevo controlador de dominio mediante el uso de script de implementación de Hola o manualmente promover un controlador de toodomain de máquina virtual del nodo principal, puede experimentar problemas para conectar máquinas virtuales de hello en toohello de red virtual de Azure Hola Internet. Esto puede ocurrir si un servidor reenviador DNS se configura automáticamente en el controlador de dominio de Hola y este servidor no se puede resolver correctamente.
  
    toowork resolver este problema, inicie sesión en el controlador de dominio de toohello y cualquier opción de configuración de reenviador de Hola de quitar o configurar un servidor reenviador DNS válido. toodo, en el administrador del servidor, haga clic en **herramientas** > **DNS** tooopen Administrador de DNS y, a continuación, haga doble clic en **reenviadores**.

## <a name="next-steps"></a>Pasos siguientes
* Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para obtener información sobre las distribuciones de Linux admitidas, mover los datos y el envío de clúster de HPC Pack tooan de trabajos con Linux nodos de proceso.
* Para ver los tutoriales que usan Hola script toocreate un clúster y ejecutan una carga de trabajo de Linux HPC, vea:
  * [Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure](hpcpack-cluster-namd.md)
  * [Ejecución de OpenFOAM con Microsoft HPC Pack en nodos de proceso de Linux en Azure](hpcpack-cluster-openfoam.md)
  * [Ejecución de STAR-CCM+ con Microsoft HPC Pack en nodos de proceso de Linux en Azure](hpcpack-cluster-starccm.md)

