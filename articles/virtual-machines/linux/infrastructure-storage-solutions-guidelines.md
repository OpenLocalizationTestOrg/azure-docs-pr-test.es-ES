---
title: Soluciones de almacenamiento para VM de Linux en Azure| Microsoft Docs
description: "Obtenga información sobre las directrices clave de diseño e implementación para implementar soluciones de almacenamiento en los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7c5089b9db945b0e0f4523e53bb44c178ffd0781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a>Directrices de infraestructura de Azure Storage para máquinas virtuales Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artículo se centra en entender las necesidades de almacenamiento y las consideraciones de diseño para conseguir un rendimiento óptimo de la máquina virtual.

## <a name="implementation-guidelines-for-storage"></a>Directrices de implementación para el almacenamiento
Decisiones:

* ¿Va a usar Azure Managed Disks o discos no administrados?
* ¿Necesita usar el almacenamiento Estándar o Premium para la carga de trabajo?
* ¿Necesita crear bandas en los discos para crear discos de más de 4 TB?
* ¿Necesita crear bandas en los discos para lograr un rendimiento óptimo de E/S para la carga de trabajo?
* ¿Qué conjunto de cuentas de almacenamiento necesita para hospedar su infraestructura o carga de trabajo de TI?

Tareas:

* Revise las solicitudes de E/S de las aplicaciones que va a implementar y planee el número y el tipo adecuados de cuentas de almacenamiento.
* Cree el conjunto de cuentas de almacenamiento usando su convención de nomenclatura. Puede usar la CLI o el Portal de Azure.

## <a name="storage"></a>Almacenamiento
Almacenamiento de Azure es una parte clave del proceso de implementación y administración de aplicaciones y máquinas virtuales. Almacenamiento de Azure proporciona servicios para almacenar datos de archivos, datos sin estructura y mensajes, y también forma parte de la infraestructura que da soporte a las máquinas virtuales.

[Azure Managed Disks](../../storage/storage-managed-disks-overview.md) controla automáticamente el almacenamiento en segundo plano. Con los discos no administrados, era preciso crear cuentas de almacenamiento que contuvieran los discos (archivos VHD) de las máquinas virtuales de Azure. Al escalar verticalmente, era preciso asegurarse de que se habían creado cuentas de almacenamiento adicionales, para que no se superar el límite de IOPS de almacenamiento con cualquiera de los discos. Si Managed Disks controla el almacenamiento, desaparecen los límites de la cuenta de almacenamiento (por ejemplo, 20 000 IOPS por cuenta). Tampoco es preciso copiar las imágenes personalizadas (archivos VHD) en varias cuentas de almacenamiento. Puede administrarlas en una ubicación central (una cuenta de almacenamiento por región de Azure) y utilizarlas para crear cientos de máquinas virtuales en una suscripción. Se recomienda utilizar Managed Disks para las nuevas implementaciones.

Existen dos tipos de cuentas de almacenamiento disponibles para la compatibilidad con máquinas virtuales.

* Las cuentas de Standard Storage proporcionan acceso a Blob Storage (que se usa para almacenar discos de VM de Azure), Table Storage, Queue Storage y File Storage.
* [Premium Storage](../../storage/storage-premium-storage.md) ofrecen compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo de E/S intensivas, como el clúster MongoDB particionado. En estos momentos, Premium Storage solo admite discos de VM de Azure.

Azure crea máquinas virtuales con un disco del sistema operativo, un disco temporal y ninguno o varios discos de datos opcionales. Tanto el disco del sistema operativo como los discos de datos son blobs en páginas de Azure, mientras que el disco temporal se almacena localmente en el nodo en que reside el equipo. Tenga cuidado al diseñar aplicaciones para que solo utilice este disco temporal para datos no persistentes, ya que la máquina virtual se puede migrar entre hosts durante un evento de mantenimiento. Se podrían perder los datos almacenados en el disco temporal.

El entorno de Azure Storage subyacente proporciona alta disponibilidad y durabilidad para garantizar que los datos permanezcan protegidos frente a errores de hardware o mantenimientos no planeados. Al diseñar el entorno de Azure Storage, puede decidir replicar el almacenamiento de máquina virtual de los siguientes modos:

* Localmente dentro de un determinado centro de datos de Azure
* En centros de datos de Azure dentro de una región determinada
* En centros de datos de Azure de diferentes regiones

Puede leer [más información acerca de las opciones de replicación para una alta disponibilidad](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Los discos de datos y del sistema operativo tienen un tamaño máximo de 4 TB. Puede usar el Administrador de volúmenes lógicos (LVM) para superar este límite mediante la agrupación de discos de datos para presentar volúmenes lógicos de más de 1023 GB a la máquina virtual.

Existen algunos límites de escalabilidad que se aplican a la hora de diseñar las implementaciones de Azure Storage. Consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../../azure-subscription-service-limits.md#storage-limits) para obtener más información. Consulte también [Objetivos de escalabilidad y rendimiento del almacenamiento en Azure](../../storage/storage-scalability-targets.md).

En cuanto al almacenamiento de aplicaciones, puede guardar datos de objetos no estructurados como documentos, imágenes, copias de seguridad, datos de configuración, registros, etc. mediante Blob Storage. En lugar de que aplicación escriba en un disco virtual asociado a la máquina virtual, la aplicación puede escribir directamente en el Almacenamiento de blobs de Azure. Blob Storage también proporciona la opción de [capas de almacenamiento de acceso frecuente y acceso esporádico](../../storage/storage-blob-storage-tiers.md) según las necesidades de disponibilidad y las restricciones de costo.

## <a name="striped-disks"></a>Discos con bandas
Además de ofrecer la posibilidad de crear discos de más de 1023 GB, en muchos casos, la creación de bandas en los discos de datos mejorará el rendimiento, ya que permite que varios blobs respalden el almacenamiento de un solo volumen. Con la creación de bandas, las operaciones de E/S necesarias para escribir y leer datos de un único disco lógico se realizan en paralelo.

Azure impone límites en la cantidad de discos de datos y la cantidad de ancho de banda disponible en función del tamaño de la máquina virtual. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).

Si usa la creación de bandas en discos de datos de Azure, tenga en cuenta las siguientes directrices:

* Conecte los discos de datos máximos que se permiten para el tamaño de la VM.
* Use LVM.
* Evite el uso de opciones de almacenamiento en caché del disco de datos de Azure (directiva de almacenamiento en caché = ninguna).

Para más información, consulte [Configuración del LVM en una máquina virtual Linux en Azure](configure-lvm.md).

## <a name="multiple-storage-accounts"></a>Cuentas de almacenamiento múltiples
En esta sección no se aplica a [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ya que no creará cuentas de almacenamiento independientes. 

Al diseñar el entorno de Azure Storage para los discos no administrados, puede utilizar varias cuentas de almacenamiento a medida que el número de máquinas virtuales implementadas aumente. Este enfoque ayuda a distribuir la E/S entre la infraestructura subyacente de Azure Storage con el fin de mantener un rendimiento óptimo para las VM y aplicaciones. Al diseñar las aplicaciones que se van a implementar, tenga en cuenta los requisitos que E/S de cada VM tendrá y compense esas VM entre las cuentas de Azure Storage. Trate de evitar agrupar todas las máquinas virtuales que exigen E/S elevadas en una o dos cuentas de almacenamiento.

Para obtener más información sobre las funcionalidades de E/S de las distintas opciones de Azure Storage y algunos máximos recomendados, consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

