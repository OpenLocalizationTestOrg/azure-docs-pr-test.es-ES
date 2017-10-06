---
title: "Almacenamiento estándar rentable basado en aaaHD y discos de máquina virtual de Azure | Documentos de Microsoft"
description: "Examine el almacenamiento Estándar rentable y los discos de máquina virtual administrados y no administrados."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Almacenamiento Estándar rentable y discos de máquina virtual de Azure administrados y no administrados

El almacenamiento estándar de Azure ofrece compatibilidad de discos confiable y de bajo coste para las máquinas virtuales que ejecutan cargas de trabajo que no tienen en cuenta la latencia. También admite blobs, tablas, colas y archivos. Con el almacenamiento estándar, los datos de Hola se almacenan en unidades de disco duro (HDD). Cuando se trabaja con máquinas virtuales, se pueden usar discos de almacenamiento estándar para escenarios de desarrollo/pruebas y para cargas de trabajo menos críticas, y discos de Premium Storage para aplicaciones de producción de misión crítica. El almacenamiento estándar está disponible en todas las regiones de Azure. 

En este artículo se centrará en el uso de Hola de almacenamiento estándar para discos de máquina virtual. Para obtener más información sobre el uso de Hola de almacenamiento de blobs, tablas, colas y archivos, consulte toohello [tooStorage Introducción](storage-introduction.md).

## <a name="disk-types"></a>Tipos de disco

Hay dos maneras de toocreate discos estándar para las máquinas virtuales de Azure:

**Sin administrar discos**: trata de método original de hello en los que administrará Hola almacenamiento cuentas utilizadas toostore Hola archivos VHD que corresponden toohello discos de máquina virtual. Los archivos VHD se almacenan como blobs en páginas en las cuentas de almacenamiento. Los discos no administrados pueden ser adjunto tooany tamaño de VM de Azure, incluidas las máquinas virtuales de Hola que usan almacenamiento Premium, principalmente como hello DSv2 y serie GS. Máquinas virtuales de Azure admiten la conexión de varios discos estándares, lo que permite una too256 TB de almacenamiento por máquina virtual.

[**Azure discos administrados**](storage-managed-disks-overview.md): esta característica administra las cuentas de almacenamiento de Hola que usó para discos de máquina virtual de Hola para usted. Especificar tipo de hello (Premium o estándar) y el tamaño del disco necesita y Azure crea y administra el disco de hello en su nombre. No tienes tooworry acerca de cómo colocar discos Hola entre varias cuentas de almacenamiento en orden tooensure que permanezca dentro de los límites de escalabilidad de Hola Hola las cuentas de almacenamiento: Azure controla automáticamente.

Aunque ambos tipos de discos están disponibles, se recomienda utilizar discos administrados tootake aprovechar sus muchas características.

visite tooget a trabajar con el almacenamiento de Azure estándar [empiece de forma gratuita](https://azure.microsoft.com/pricing/free-trial/). 

Para obtener información sobre cómo toocreate una máquina virtual con discos administrados, vea uno de hello después de artículos.

* [Creación de una máquina virtual con Resource Manager y PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)
* [Crear una VM de Linux con hello 2.0 de CLI de Azure](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>Características del almacenamiento estándar 

¡Eche un vistazo a algunas de las características de Hola de almacenamiento estándar. Para obtener más información, vea [Introducción tooAzure almacenamiento](storage-introduction.md).

**Almacenamiento estándar**: el almacenamiento estándar de Azure admite discos de Azure, blobs de Azure, Azure File Storage, tablas de Azure y colas de Azure. los servicios de almacenamiento estándar toouse, inician con [crear una cuenta de almacenamiento de Azure](storage-create-storage-account.md#create-a-storage-account).

**Discos de almacenamiento estándar:** almacenamiento estándar pueden ser discos conectados máquinas virtuales de Azure tooall incluidas utilizadas con el almacenamiento Premium como serie de hello DSv2 y GS de las máquinas virtuales de serie de tamaño. Un disco de almacenamiento estándar sólo puede ser tooone adjunto máquina virtual. Sin embargo, puede asociar uno o varios de estos tooa de discos de máquina virtual, recuento de disco máximo toohello definidas para ese tamaño de máquina virtual. Hola pasos de la sección en objetivos de rendimiento y la escalabilidad de almacenamiento estándar, vamos a describir las especificaciones de hello con más detalle. 

**Blob en páginas estándar**: blobs en páginas estándar son toohold usa discos persistentes para las máquinas virtuales y también puede obtenerse acceso directamente a través de REST al igual que otros tipos de Blobs de Azure. Los [blob en páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) son una colección de páginas de 512 bytes optimizadas para operaciones de lectura y escritura aleatorias. 

**Replicación del almacenamiento:** en la mayoría de las regiones, los datos de una cuenta de almacenamiento estándar se pueden replicar localmente o replicar geográficamente en varios centros de datos. Hola cuatro tipos de replicación disponible son almacenamiento localmente redundante (LRS), almacenamiento con redundancia de zona (ZRS), almacenamiento con redundancia geográfica (GRS) y almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS). Actualmente, en el almacenamiento estándar Managed Disks solo admiten el almacenamiento con redundancia local (LRS). Para más información, consulte [Replicación de Azure Storage](storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Objetivos de escalabilidad y rendimiento

En esta sección, vamos a describir los destinos de escalabilidad y rendimiento de hello necesita tooconsider al usar almacenamiento estándar.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Límites de cuenta: no hay ningún toomanaged discos

| **Recurso** | **Límite predeterminado** |
|--------------|-------------------|
| TB por cuenta de almacenamiento  | 500 TB |
| Entrada máxima<sup>1</sup> por cuenta de almacenamiento (regiones de EE. UU.) | 10 Gbps si GRS/ZRS están habilitados, 20 Gbps en el caso de LRS |
| Salida máxima<sup>1</sup> por cuenta de almacenamiento (regiones de EE. UU.) | 20 Gbps si RA-GRS/GRS/ZRS están habilitados, 30 Gbps en el caso de LRS |
| Entrada máxima<sup>1</sup> por cuenta de almacenamiento (regiones de Europa y Asia) | 5 Gbps si GRS/ZRS están habilitados, 10 Gbps en el caso de LRS |
| Salida máxima<sup>1</sup> por cuenta de almacenamiento (regiones de Europa y Asia) | 10 Gbps si RA-GRS/GRS/ZRS están habilitados, 15 Gbps en el caso de LRS |
| Tasa total de solicitudes (suponiendo un tamaño de objeto de 1 KB) por cuenta de almacenamiento | Too20, IOPS 000, entidades por segundo o mensajes por segundo |

<sup>1</sup> entrada hace referencia a datos de tooall (solicitudes) enviados tooa cuenta de almacenamiento. Salida hace referencia a datos de tooall (respuestas) recibidos de una cuenta de almacenamiento.

Para más información, consulte [Objetivos de escalabilidad y rendimiento de Almacenamiento de Azure](storage-scalability-targets.md).

Si de la aplicación hello debe superar los objetivos de escalabilidad de Hola de una única cuenta de almacenamiento, compile su aplicación toouse varias cuentas de almacenamiento y dividir los datos en esas cuentas de almacenamiento. Como alternativa, puede administrar discos de Azure y Azure administrará Hola de partición y la colocación de los datos por usted.

### <a name="standard-disks-limits"></a>Límites de los discos estándar

A diferencia de los discos Premium, no se aprovisionan las operaciones de entrada/salida de hello por segundo (IOPS) y el rendimiento (ancho de banda) de los discos estándar. Hola de discos estándares varía el rendimiento con hello VM tamaño toowhich Hola disco está conectado, no toohello tamaño del disco de Hola. Podría esperar tooachieve seguridad toohello límite de rendimiento aparecen en hello tabla siguiente.

**Límites de los discos estándar (administrados y no administrados)**

| **Nivel de máquina virtual**            | **Máquina virtual de nivel Básico** | **Máquina virtual de nivel Estándar** |
|------------------------|-------------------|----------------------|
| Tamaño máx. de disco          | 4095 GB           | 4095 GB              |
| Máximo de 8 KB de IOPS por disco | Seguridad too300         | Seguridad too500            |
| Ancho de banda máx. por disco | Seguridad too60 MB/s     | Seguridad too60 MB/s        |

Si la carga de trabajo requiere compatibilidad con discos de gran rendimiento y baja latencia, considere la posibilidad de usar Premium Storage. tooknow más ventajas de almacenamiento Premium, visite [almacenamiento Premium de alto rendimiento y discos de máquina virtual de Azure](storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Instantáneas y copia de blob

servicio de almacenamiento de archivo de disco duro virtual de hello toohello es un blob en páginas. Puede tomar instantáneas de blobs de página y cópielos tooanother ubicación, como una cuenta de almacenamiento diferente.

### <a name="unmanaged-disks"></a>Discos no administrados

Puede crear [instantáneas incrementales](storage-incremental-snapshots.md) para discos estándar no administrado en hello mismo forma de usar instantáneas con almacenamiento estándar. Se recomienda que cree instantáneas y, a continuación, copia de esas cuentas de almacenamiento estándar con redundancia geográfica de tooa de instantáneas si el disco de origen está en una cuenta de almacenamiento con redundancia local. Para obtener más información, consulte [Opciones de redundancia de Almacenamiento de Azure](storage-redundancy.md).

Si un disco está conectado tooa VM, no se permiten ciertas operaciones de API en discos de Hola. Por ejemplo, no se puede realizar un [Copy Blob](/rest/api/storageservices/Copy-Blob) operación en ese blob siempre que sea el disco de hello vinculada tooa máquina virtual. En su lugar, cree primero una instantánea del blob utilizando hello [Blob de instantánea](/rest/api/storageservices/Snapshot-Blob) el método API de REST y, a continuación, realizar hello [Copy Blob](/rest/api/storageservices/Copy-Blob) de Hola Hola de toocopy de instantánea se adjuntó el disco. Como alternativa, puede desconectar el disco de hello y, a continuación, realizar las operaciones necesarias.

toomaintain copias con redundancia geográfica de las instantáneas, puede copiar las instantáneas de una cuenta de almacenamiento estándar con redundancia geográfica de almacenamiento con redundancia local cuenta tooa mediante AzCopy o copia de Blob. Para obtener más información, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md) y [Copy Blob](/rest/api/storageservices/Copy-Blob).

Para más información acerca de cómo realizar operaciones de REST en blobs en páginas en cuentas de almacenamiento estándar, consulte [Azure Storage Services REST API Reference](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (Referencia de API de RES de los servicios de Azure Storage).

### <a name="managed-disks"></a>Discos administrados

Una instantánea de un disco administrado es una copia de solo lectura de disco administrado de hello, que se almacena como un disco administrado estándar. Instantáneas incrementales no se admiten actualmente para administrar discos pero se admitirán en futuras Hola.

Si un disco administrado está conectado tooa VM, no se permiten ciertas operaciones de API en discos de Hola. Por ejemplo, no se puede generar un tooperform de firma (SAS) de acceso compartido a una operación de copia mientras disco Hola está adjunto tooa máquina virtual. En su lugar, cree primero una instantánea del disco de hello y, a continuación, realizar copia de Hola de instantánea de Hola. Como alternativa, puede desconectar el disco de hello y, a continuación, generar una operación de copia de acceso compartido (SAS) de la firma tooperform Hola.

## <a name="pricing-and-billing"></a>Precios y facturación

Al usar almacenamiento estándar hello facturación consideraciones siguientes se aplican:

* Tamaño de datos o datos no administrados del almacenamiento estándar 
* Discos administrados estándar
* Instantáneas del almacenamiento estándar
* Transferencias de datos de salida
* Transacciones

**No administrada de tamaño de datos y el disco de almacenamiento:** para discos no administrados y otros datos (blobs, tablas, colas y archivos), se le cobra solo por cantidad de Hola de espacio que está usando. Por ejemplo, si tiene una máquina virtual cuyo blob en páginas se aprovisiona como 127 GB, pero hello VM está realmente solamente con 10 GB de espacio, se le facturará de 10 GB de espacio. Se admiten almacenamiento estándar backup too8191 GB y los discos estándar no administrados backup too4095 GB. 

**Discos administrados:** administrado discos se facturan por tamaño de hello aprovisionado. Si el disco se aprovisiona como un disco de 10 GB y se usa solo 5 GB, le cobrará para tamaño de aprovisionamiento de Hola de 10 GB.

**Las instantáneas**: las instantáneas de discos estándares se facturan por capacidad adicional de hello utilizada por las instantáneas de Hola. Para obtener información sobre las instantáneas, consulte [Crear una instantánea de un blob](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Transferencias de datos de salida**: las [transferencias de datos de salida](https://azure.microsoft.com/pricing/details/data-transfers/) (datos que salen de los centros de datos de Azure) se facturan en función del uso de ancho de banda.

**Transacción**: Azure cobra 0,0036 $ por 100 000 transacciones de almacenamiento estándar. Las transacciones incluyen tanto de lectura y toostorage de las operaciones de escritura.

Para más información acerca de los precios del almacenamiento estándar, Virtual Machines y Managed Disks, consulte:

* [Precios de Almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Precios de Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Soporte técnico del servicio Azure Backup 

Se pueden realizar copias de seguridad de máquinas virtuales con discos no administrados mediante Azure Backup. [Más detalles](../backup/backup-azure-vms-first-look-arm.md).

También puede utilizar Hola servicio copia de seguridad de Azure con discos administrados toocreate un trabajo de copia de seguridad con copias de seguridad basadas en tiempo, su fácil restauración de máquinas virtuales y las directivas de retención de copia de seguridad. En [Uso de máquinas virtuales de disco administrado con Azure Backup](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup) puede encontrar más información al respecto.

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooAzure almacenamiento](storage-introduction.md)

* [crear una cuenta de almacenamiento](storage-create-storage-account.md)

* [Introducción a Managed Disks](storage-managed-disks-overview.md)

* [Creación de una máquina virtual con Resource Manager y PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Crear una VM de Linux con hello 2.0 de CLI de Azure](../virtual-machines/linux/quick-create-cli.md)
