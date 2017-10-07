---
title: "aaaMigrate discos de máquinas virtuales de Azure tooManaged | Documentos de Microsoft"
description: "Migrar máquinas virtuales de Azure creadas con discos no administrados en toouse de cuentas de almacenamiento administrado discos."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Migrar máquinas virtuales de Azure tooManaged discos en Azure

Discos administrados Azure simplifica la administración de almacenamiento mediante la eliminación de la necesidad de hello tooseparately administrar cuentas de almacenamiento.  También puede migrar los discos toobenefit existente de máquinas virtuales de Azure tooManaged de confiabilidad de las máquinas virtuales en un conjunto de disponibilidad. Garantiza que los discos de Hola de diferentes máquinas virtuales en un conjunto de disponibilidad estará suficientemente aislados desde cada otro tooavoid punto único de errores. Discos de diferentes máquinas virtuales coloca automáticamente en un conjunto de disponibilidad en diferentes unidades de escala de almacenamiento (sellos) que limita el impacto de Hola de errores de unidad de escala de almacenamiento únicos producidos debido a errores de software y toohardware.
En virtud de sus necesidades, puede elegir entre dos tipos de opciones de almacenamiento:

- [Managed Disks Premium](../../storage/common/storage-premium-storage.md) son medios de almacenamiento basados en unidades de estado sólido (SSD) que ofrecen compatibilidad con discos de alto rendimiento y latencia baja para máquinas virtuales que ejecutan cargas de trabajo intensivas de E/S. Puede aprovechar de velocidad de Hola y rendimiento de estos discos por discos administrados de migración tooPremium.

- [Los discos estándar administrado](../../storage/common/storage-standard-storage.md) usar medios de almacenamiento de la unidad de disco duro (HDD) según y son más adecuados para desarrollo y pruebas y otras cargas de trabajo de acceso con frecuencia que son menos sensible variabilidad tooperformance.

Puede migrar tooManaged discos en los escenarios siguientes:

| Migrar...                                            | Vínculo de documentación                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Convertir máquinas virtuales de forma independiente y las máquinas virtuales en un conjunto de disponibilidad toomanaged discos   | [Convierta los discos de toouse administra las máquinas virtuales](convert-unmanaged-to-managed-disks.md) |
| Una sola máquina virtual desde clásico tooResource Manager en discos administrados     | [Migración de una VM única](migrate-single-classic-to-resource-manager.md)  | 
| Todas las máquinas virtuales de hello en una red virtual de clásico tooResource Manager en discos administrados     | [Migrar recursos de IaaS de clásico tooResource Manager](migration-classic-resource-manager-ps.md) y, a continuación, [convertir una máquina virtual a partir de discos de toomanaged de discos no administrado](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Plan para la conversión de hello tooManaged discos

Esta sección le ayudará a mejor decisión de Hola de toomake en tipos de máquina virtual y disco.


## <a name="location"></a>Ubicación

Elija una ubicación donde Azure Managed Disks esté disponible. Si va a mover discos de tooPremium administrados, asegúrese también de que almacenamiento Premium está disponible en la región de Hola donde piensa toomove a. Consulte [Servicios de Azure por región](https://azure.microsoft.com/regions/#services) para obtener información actualizada sobre las ubicaciones disponibles.

## <a name="vm-sizes"></a>Tamaños de VM

Si va a migrar discos administrados de tooPremium, tiene tamaño de hello tooupdate de hello VM tooPremium tamaño con capacidad de almacenamiento disponible en región Hola donde se encuentra la máquina virtual. Revise los tamaños de máquinas virtuales de Hola que son capaces de almacenamiento Premium. se enumeran las especificaciones de tamaño de máquina virtual de Azure de Hello en [tamaños de máquinas virtuales](sizes.md).
Revise las características de rendimiento de Hola de máquinas virtuales que funcionen con el almacenamiento Premium y elija el tamaño más adecuado de hello máquina virtual que mejor se adapte a la carga de trabajo. Asegúrese de que hay suficiente ancho de banda disponible en el tráfico de disco de máquina virtual toodrive Hola.

## <a name="disk-sizes"></a>Tamaños de disco

**Managed Disks Premium**

Hay siete tipos de Managed Disks premium que se pueden usar con la máquina virtual y cada uno de ellos tiene sus límites específicos de rendimiento y E/S por segundo. Tenga en cuenta estos límites al elegir Hola tipo de disco de Premium para la máquina virtual en función de las necesidades de saludo de la aplicación en cuanto a capacidad, rendimiento, escalabilidad, y la carga máxima.

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamaño del disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1.024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Rendimiento de disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo |

**Discos administrados Estándar**

Hay siete tipos de Managed Disks estándar que se pueden usar con la máquina virtual. Cada uno de ellos tiene una capacidad distinta, pero los mismos límites de rendimiento y E/S por segundo. Elija el tipo de Hola de discos administrados estándar según las necesidades de capacidad de saludo de la aplicación.

| Tipo de disco Estándar  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Tamaño del disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1.024 GB (1 TB)   | 2048 GB (2 TB)    | 4095 GB (4 TB)   | 
| IOPS por disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Rendimiento de disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 

## <a name="disk-caching-policy"></a>Directiva de almacenamiento en caché de disco

**Managed Disks Premium**

De forma predeterminada, es la directiva de caché de disco *de sólo lectura* de Hola a todos los discos de datos Premium, y *lectura y escritura* para el disco del sistema operativo Hola Premium asocia toohello máquina virtual. Esta opción de configuración se recomienda tooachieve Hola un rendimiento óptimo para IOs la aplicación. Para discos de datos de solo escritura o de gran cantidad de escritura (por ejemplo, archivos de registro de SQL Server), deshabilite el almacenamiento en caché de disco para lograr un mejor rendimiento de la aplicación.

## <a name="pricing"></a>Precios

Hola de revisión [precios de discos administrados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Precios de discos administrados de Premium están el mismo que Hola los discos Premium no administrado. Sin embargo, los precios de Managed Disks Estándar son distintos a los de los Unmanaged Disks Estándar.



## <a name="next-steps"></a>Pasos siguientes

- Más información sobre [Managed Disks](managed-disks-overview.md)
