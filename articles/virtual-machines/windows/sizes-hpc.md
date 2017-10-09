---
title: "tamaños de máquina virtual de Windows aaaAzure - HPC | Documentos de Microsoft"
description: "Enumera los tamaños diferentes de hello disponibles para las máquinas virtuales en Azure de informática de alto rendimiento de Windows."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a>Tamaños de máquina virtual de informática de alto rendimiento

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Instancias compatibles con RDMA
Un subconjunto de instancias de proceso intensivo de hello (H16r, H16mr, A8 y A9) cuentan con una interfaz de red para la conectividad de memoria directa remota (RDMA) de acceso. Esta interfaz es además tamaños de máquina virtual de toohello red de Azure estándar interfaz tooother disponible. 
  
Esta interfaz permite hello toocommunicate de instancias compatible con RDMA a través de una red de InfiniBand, funcionan a velocidades FDR para máquinas virtuales H16r y H16mr y las tasas QDR para máquinas virtuales A8 y A9. Estas capacidades RDMA pueden mejorar la escalabilidad de Hola y el rendimiento de las aplicaciones de interfaz de paso de mensajes (MPI).

Estos son los requisitos para máquinas virtuales de Windows compatibles con RDMA tooaccess Hola red RDMA de Azure: 

* **Sistema operativos**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Actualmente, Windows Server 2016 no admite conectividad RDMA en Azure.
  >

* **Conjunto de disponibilidad o servicio en la nube** : Hola a implementar máquinas virtuales de hello compatibles con RDMA en el mismo conjunto (cuando se utiliza el modelo de implementación de Azure Resource Manager hello) de disponibilidad u Hola mismo servicio en la nube (cuando se utiliza el modelo de implementación clásica de hello). Si utiliza Azure Batch, Hola máquinas virtuales compatibles con RDMA debe estar en hello mismo grupo.

* **MPI** : Microsoft MPI (MS-MPI) 2012 R2 o versiones posteriores, MPI Intel Library 5.x.

  Implementaciones de MPI admitidas use hello toocommunicate de interfaz Microsoft Network Direct entre instancias. 

* **Espacio de direcciones de red RDMA** -Hola dirección espacio 172.16.0.0/16 de reserva de red RDMA de hello en Azure. toorun de aplicaciones de MPI en instancias implementadas en una red virtual de Azure, asegúrese de que el espacio de direcciones de red virtual de hello no se superponen red RDMA de Hola.

* **Extensión HpcVmDrivers VM** -en máquinas virtuales compatibles con RDMA, debe agregar el controladores de dispositivos de hello HpcVmDrivers extensión tooinstall Windows red para la conectividad RDMA. (En ciertas implementaciones de instancias A8 y A9, Hola extensión HpcVmDrivers se agrega automáticamente.) tooa de extensión VM de hello tooadd VM, puede usar [Azure PowerShell](/powershell/azure/overview) cmdlets. 

  
  Hola el siguiente comando instala Hola más reciente extensión HpcVMDrivers de versión 1.1 en una máquina virtual compatible con RDMA existente denominada *myVM* implementados en el grupo de recursos de hello llamado *myResourceGroup* en hello  *Oeste de Estados Unidos* región:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Para obtener más información, consulte el artículo de [características y extensiones de las máquinas virtuales](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). También puede trabajar con las extensiones de máquinas virtuales implementadas en hello [modelo de implementación clásica](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Uso de HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuito HPC clúster y el trabajo de administración de la solución de Microsoft, constituye una opción para toocreate un clúster de cálculo en las aplicaciones de MPI basados en Windows Azure toorun y otras cargas de trabajo HPC. HPC Pack 2012 R2 y versiones posteriores incluyen un entorno en tiempo de ejecución para MS-MPI que usa la red RDMA de Azure de hello cuando se implementa en máquinas virtuales compatibles con RDMA.




## <a name="other-sizes"></a>Otros tamaños
- [Uso general](sizes-general.md)
- [Proceso optimizado](sizes-compute.md)
- [Memoria optimizada](../virtual-machines-windows-sizes-memory.md)
- [Almacenamiento optimizado](../virtual-machines-windows-sizes-storage.md)
- [GPU optimizada](sizes-gpu.md)

## <a name="next-steps"></a>Pasos siguientes

- Para las instancias de proceso intensivo de las listas de comprobación toouse Hola con HPC Pack en Windows Server, vea [configurar un clúster de Windows RDMA con aplicaciones de MPI de HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- instancias de proceso intensivo toouse al ejecutar aplicaciones MPI con Azure Batch, vea [varias instancias de uso tareas toorun las aplicaciones de interfaz de paso de mensajes (MPI) en Azure Batch](../../batch/batch-mpi.md).

- Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.




