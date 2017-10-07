---
title: "proceso intensivo aaaAbout las máquinas virtuales con Linux | Documentos de Microsoft"
description: "Obtener información general y consideraciones para el uso de tamaños de proceso intensivo de hello H-series y A8, A9, A10 y A11 para máquinas virtuales de Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Acerca de las máquinas virtuales de la serie H y A de procesos intensivos para Linux
Aquí es información general y algunas consideraciones para el uso de Hola H-series de Azure más recientes y Hola tamaños A8, A9, A10 y A11 anteriores, también conocido como *infromáticos* instancias. Este artículo se centra en el uso de estos tamaños con las máquinas virtuales con Linux. También puede utilizarlos para [máquinas virtuales Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para conocer las especificaciones básicas, las capacidades de almacenamiento y los detalles del disco, consulte [Tamaños de las máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Red de acceso toohello RDMA
Puede crear clústeres de máquinas virtuales de Linux compatibles con RDMA que ejecute uno de hello siguientes distribuciones de Linux HPC admitidas y una ventaja de tootake de implementación de MPI admitida de red RDMA de Azure de Hola. Vea [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para opciones de implementación y los pasos de configuración de ejemplo.

* **Distribuciones** : debe implementar las máquinas virtuales de compatible con RDMA SUSE Linux Enterprise Server (SLES) u Hola de imágenes de Software de Wave no autorizado (anteriormente OpenLogic) basado en CentOS HPC en Azure Marketplace. Hello imágenes Marketplace siguientes admiten conectividad RDMA:
  
    * SLES 12 SP1 para HPC, SLES 12 SP1 para HPC (Premium)
    
    * HPC 7.1 basada en CentOS y HPC 6.5 basada en CentOS  
 
        > [!NOTE]
        > Para las máquinas virtuales de la serie H, se recomienda un SLES 12 SP1 para la imagen de HPC o la imagen de HPC 7.1 basada en CentOS.
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
    
    Configuración adicional del sistema es necesario toorun trabajos MPI en máquinas virtuales en clúster. Por ejemplo, en un clúster de máquinas virtuales, necesitará tooestablish nodos de proceso de confianza entre Hola. Para la configuración típica, vea [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Consideraciones sobre el HPC Pack y Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuito HPC clúster y el trabajo de administración de la solución de Microsoft, proporciona una opción de instancias de proceso intensivo de hello toouse con Linux. versiones más recientes de Hola de HPC Pack admiten varias distribuciones de Linux toorun en proceso nodos implementados en máquinas virtuales de Azure, administrados por un nodo principal de Windows Server. Con los nodos de proceso de Linux compatibles con RDMA ejecutando MPI de Intel, HPC Pack puede programar y ejecutar aplicaciones MPI Linux esa red RDMA de Hola de acceso. tooget iniciado, consulte [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Consideraciones sobre la topología de red
* En las máquinas virtuales con Linux compatibles con RDMA de Azure, Eth1 se reserva para el tráfico de red RDMA. No cambie los valores de configuración de Eth1 o toda la información de archivo de configuración de Hola que hace referencia toothis red. Eth0 se reserva para el tráfico de red regular de Azure.
* En Azure, no se admite IP sobre InfiniBand (IB). Solo se admite RDMA sobre IB.



## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información sobre la disponibilidad y precios de los tamaños de proceso intensivo de hello, consulte [precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Para más información sobre las capacidades de almacenamiento y los detalles del disco, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* tooget inició implementar y usar tamaños de proceso intensivo con RDMA en Linux, consulte [configurar una aplicación de MPI de Linux RDMA clúster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

