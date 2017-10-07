---
title: aaaMigrate de AWS y otra plataformas tooManaged discos en Azure | Documentos de Microsoft
description: "Cree VM en Azure con VHD cargados desde otras nubes, como AWS u otras plataformas de virtualización, y aproveche las ventajas de Azure Managed Disks."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Migrar de Amazon Web Services (AWS) y otras plataformas tooManaged discos en Azure

Puede cargar archivos VHD desde AWS o local toocreate de tooAzure de soluciones máquinas virtuales que se benefician de discos administrados virtualización. Discos administrados Azure elimina la necesidad de hello toomanaging de cuentas de almacenamiento de máquinas virtuales de IaaS de Azure. También tiene tooonly especificar tipo de hello (Premium o estándar) y el tamaño del disco que necesita y Azure creará y administrará disco Hola automáticamente. 

Puede cargar VHD generalizados o especializados. 
- **VHD generalizado**: elimina toda la información personal de la cuenta mediante Sysprep. 
- **Especializado VHD** -mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original. 

> [!IMPORTANT]
> Antes de cargar cualquier tooAzure de disco duro virtual, debe seguir [preparar una tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Escenario                                                                                                                         | Documentación                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Tiene un instancias AWS EC2 existente que podría como toomigrate tooAzure discos administrados                                     | [Mover una máquina virtual de Amazon Web Services (AWS) tooAzure](aws-to-azure.md)                           |
| Tiene una máquina virtual desde y otra plataforma de virtualización que desearía toouse toouse como una imagen toocreate varias máquinas virtuales de Azure. | [Cargar un disco duro virtual generalizado y utilizar toocreate un nuevas máquinas virtuales de Azure](upload-generalized-managed.md) |
| Tener una máquina virtual de forma única personalizada que desearía toorecreate en Azure.                                                      | [Cargar un tooAzure especializada de VHD y crear una nueva máquina virtual](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Información general de Managed Disks

Discos administrado de Azure simplifica la administración de máquinas virtuales mediante la eliminación de cuentas de almacenamiento de hello necesidad toomanage. Managed Disks también aprovecha las ventajas de la mejor confiabilidad de las VM en un conjunto de disponibilidad. Garantiza que los discos de Hola de diferentes máquinas virtuales en un conjunto de disponibilidad estará suficientemente aislados desde cada otro tooavoid punto único de errores. Discos de diferentes máquinas virtuales coloca automáticamente en un conjunto de disponibilidad en diferentes unidades de escala de almacenamiento (sellos) que limita el impacto de Hola de errores de unidad de escala de almacenamiento únicos producidos debido a errores de software y toohardware. En virtud de sus necesidades, puede elegir entre dos tipos de opciones de almacenamiento: 
 
- [Managed Disks Premium](../../storage/common/storage-premium-storage.md) son medios de almacenamiento basados en unidades de estado sólido (SSD) que ofrecen compatibilidad con discos de alto rendimiento y latencia baja para máquinas virtuales que ejecutan cargas de trabajo intensivas de E/S. Puede aprovechar de velocidad de Hola y rendimiento de estos discos por discos administrados de migración tooPremium.  

- [Los discos estándar administrado](../../storage/common/storage-standard-storage.md) usar medios de almacenamiento de la unidad de disco duro (HDD) según y son más adecuados para desarrollo y pruebas y otras cargas de trabajo de acceso con frecuencia que son menos sensible variabilidad tooperformance.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planear la migración de Hola de discos tooManaged

Esta sección le ayudará a mejor decisión de Hola de toomake en tipos de máquina virtual y disco.


### <a name="location"></a>Ubicación

Elija una ubicación donde Azure Managed Disks esté disponible. Si va a migrar discos administrados de tooPremium, asegúrese también de que almacenamiento Premium está disponible en la región de Hola donde piensa toomigrate a. Consulte [Servicios de Azure por región](https://azure.microsoft.com/regions/#services) para obtener información actualizada sobre las ubicaciones disponibles.

### <a name="vm-sizes"></a>Tamaños de VM

Si va a migrar discos administrados de tooPremium, tiene tamaño de hello tooupdate de hello VM tooPremium tamaño con capacidad de almacenamiento disponible en región Hola donde se encuentra la máquina virtual. Revise los tamaños de máquinas virtuales de Hola que son capaces de almacenamiento Premium. se enumeran las especificaciones de tamaño de máquina virtual de Azure de Hello en [tamaños de máquinas virtuales](sizes.md).
Revise las características de rendimiento de Hola de máquinas virtuales que funcionen con el almacenamiento Premium y elija el tamaño más adecuado de hello máquina virtual que mejor se adapte a la carga de trabajo. Asegúrese de que hay suficiente ancho de banda disponible en el tráfico de disco de máquina virtual toodrive Hola.

### <a name="disk-sizes"></a>Tamaños de disco

**Managed Disks Premium**

Hay tres tipos de Managed Disks Premium que se pueden usar con la VM y cada uno de ellos tiene sus límites específicos de rendimiento y E/S por segundo. Tenga en cuenta estos límites al elegir Hola tipo de disco de Premium para la máquina virtual en función de las necesidades de saludo de la aplicación en cuanto a capacidad, rendimiento, escalabilidad, y la carga máxima.

| Tipo de discos Premium  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Tamaño del disco           | 128 GB            | 512 GB            | 1.024 GB (1 TB)    |
| IOPS por disco       | 500               | 2300              | 5000              |
| Rendimiento de disco | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo |

**Discos administrados Estándar**

Hay cinco tipos de discos administrados Estándar que se pueden usar con la VM. Cada uno de ellos tiene una capacidad distinta, pero los mismos límites de rendimiento y E/S por segundo. Elija el tipo de Hola de discos administrados estándar según las necesidades de capacidad de saludo de la aplicación.

| Tipo de disco Estándar  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Tamaño del disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1.024 GB (1 TB)   |
| IOPS por disco       | 500              | 500              | 500              | 500              | 500              |
| Rendimiento de disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo |

### <a name="disk-caching-policy"></a>Directiva de almacenamiento en caché de disco 

**Managed Disks Premium**

De forma predeterminada, es la directiva de caché de disco *de sólo lectura* de Hola a todos los discos de datos Premium, y *lectura y escritura* para el disco del sistema operativo Hola Premium asocia toohello máquina virtual. Esta opción de configuración se recomienda tooachieve Hola un rendimiento óptimo para IOs la aplicación. Para discos de datos de solo escritura o de gran cantidad de escritura (por ejemplo, archivos de registro de SQL Server), deshabilite el almacenamiento en caché de disco para lograr un mejor rendimiento de la aplicación.

### <a name="pricing"></a>Precios

Hola de revisión [precios de discos administrados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Precios de discos administrados de Premium están el mismo que Hola los discos Premium no administrado. Sin embargo, los precios de Managed Disks Estándar son distintos a los de los Unmanaged Disks Estándar.


## <a name="next-steps"></a>Pasos siguientes

- Antes de cargar cualquier tooAzure de disco duro virtual, debe seguir [preparar una tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
