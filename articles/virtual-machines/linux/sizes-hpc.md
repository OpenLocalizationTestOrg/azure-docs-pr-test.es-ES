---
title: "tamaños de VM de Linux aaaAzure - HPC | Documentos de Microsoft"
description: "Enumera los tamaños diferentes de hello disponibles para las máquinas virtuales en Azure de informática de alto rendimiento de Linux."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a>Tamaños de máquina virtual Linux de informática de alto rendimiento

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Instancias compatibles con RDMA
Un subconjunto de instancias de proceso intensivo de hello (H16r, H16mr, A8 y A9) cuentan con una interfaz de red para la conectividad de memoria directa remota (RDMA) de acceso. Esta interfaz es además tamaños de máquina virtual de toohello red de Azure estándar interfaz tooother disponible. 
  
Esta interfaz permite hello toocommunicate de instancias compatible con RDMA a través de una red de InfiniBand, funcionan a velocidades FDR para máquinas virtuales H16r y H16mr y las tasas QDR para máquinas virtuales A8 y A9. Estas capacidades RDMA pueden mejorar la escalabilidad de Hola y el rendimiento de las aplicaciones de interfaz de paso de mensajes (MPI).

Estos son los requisitos para máquinas virtuales de Linux compatibles con RDMA tooaccess Hola red RDMA de Azure:
 
* **Distribuciones** : debe implementar las máquinas virtuales de compatible con RDMA SUSE Linux Enterprise Server (SLES) u Hola de imágenes de Software de Wave no autorizado (anteriormente OpenLogic) basado en CentOS HPC en Azure Marketplace. Hello imágenes Marketplace siguientes admiten conectividad RDMA:
  
    * SLES 12 SP1 para HPC, o SLES 12 SP1 para HPC (premium)
    
    * HPC 7.3 basadas en CentOS, HPC 7.1 basadas en CentOS, HPC 6.8 basadas en CentOS o HPC 6.5 basadas en CentOS  
 
        > [!NOTE]
        > Para las máquinas virtuales de la serie H, se recomienda SLES 12 SP1 para la imagen de HPC o la imagen de HPC 7.1 o posterior basada en CentOS.
        >
        > En las imágenes HPC basado en CentOS hello, actualizaciones del núcleo están deshabilitadas en hello **yum** archivo de configuración. Esto es porque hello controladores Linux RDMA distribuidos como un paquete RPM y actualizaciones de controladores podrían no funcionar si se actualiza el kernel Hola.
        > 
        > 
* **MPI** : Biblioteca MPI Intel 5.x
  
    Dependiendo de la imagen de Marketplace de Hola que elija, instalación de licencia, independiente, o puede ser necesaria la configuración de MPI de Intel, como se indica a continuación: 
  
  * **SLES 12 SP1 para la imagen HPC** -se distribuyen los paquetes de MPI de Intel en hello máquina virtual. Instale con hello siguiente comando:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Imágenes de HPC basadas en CentOS**: Intel MPI 5.1 ya está instalado.  
    
    Configuración adicional del sistema es necesario toorun trabajos MPI en máquinas virtuales en clúster. Por ejemplo, en un clúster de máquinas virtuales, necesitará tooestablish nodos de proceso de confianza entre Hola. Para la configuración típica, vea [configurar una aplicación de MPI Linux RDMA toorun de clúster](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Consideraciones sobre la topología de red
* En las máquinas virtuales con Linux compatibles con RDMA de Azure, Eth1 se reserva para el tráfico de red RDMA. No cambie los valores de configuración de Eth1 o toda la información de archivo de configuración de Hola que hace referencia toothis red. Eth0 se reserva para el tráfico de red regular de Azure.

* En Azure, no se admite IP sobre InfiniBand (IB). Solo se admite RDMA sobre IB.

## <a name="using-hpc-pack"></a>Uso de HPC Pack
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuito HPC clúster y el trabajo de administración de la solución de Microsoft, constituye una opción automáticamente instancias de proceso intensivo de hello toouse con Linux. versiones más recientes de Hola de HPC Pack admiten varias distribuciones de Linux toorun en proceso nodos implementados en máquinas virtuales de Azure, administrados por un nodo principal de Windows Server. Con los nodos de proceso de Linux compatibles con RDMA ejecutando MPI de Intel, HPC Pack puede programar y ejecutar aplicaciones MPI Linux esa red RDMA de Hola de acceso. Consulte [Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Otros tamaños
- [Uso general](sizes-general.md)
- [Proceso optimizado](sizes-compute.md)
- [Memoria optimizada](sizes-memory.md)
- [Almacenamiento optimizado](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Pasos siguientes

- tooget inició implementar y usar tamaños de proceso intensivo con RDMA en Linux, consulte [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.




