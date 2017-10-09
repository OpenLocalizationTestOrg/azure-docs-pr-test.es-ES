---
title: "aaaAzure Premium y Standard discos información general sobre Managed | Documentos de Microsoft"
description: "Información general de discos administrado de Azure, que administra las cuentas de almacenamiento de hello automáticamente cuando se usa máquinas virtuales de Azure"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 70d45226e531b43f2142f2798bdaf40f77f057f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-disks-overview"></a>Introducción a Azure Managed Disks

Discos administrados Azure simplifica la administración de disco para máquinas virtuales de IaaS de Azure mediante la administración hello [cuentas de almacenamiento](storage-introduction.md) asociados con discos de máquina virtual de Hola. Solo tiene tipo de hello toospecify ([Premium](storage-premium-storage.md) o [estándar](storage-standard-storage.md)) y el tamaño de hello del disco necesita y Azure crea y administra el disco de hello en su nombre.

## <a name="benefits-of-managed-disks"></a>Ventajas de los discos administrados

¡Eche un vistazo a algunas de las ventajas de hello obtendrá al usar discos administrados, a partir de este vídeo de Channel 9, [mejor resistencia de VM de Azure con discos administrados](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>La implementación de las máquina virtuales es simple y escalable

Administrar almacenamiento de identificadores de los discos automáticamente entre bastidores de Hola. Anteriormente, era toocreate almacenamiento cuentas toohold Hola los discos (archivos VHD) para las máquinas virtuales de Azure. Cuando se escala ascendentemente, había toomake seguro de que crea cuentas de almacenamiento adicionales, por lo que no superan el límite IOPS de hello para el almacenamiento con cualquiera de los discos. Con discos administrados controlar el almacenamiento, ya no está limitado por hello límites de la cuenta de almacenamiento (por ejemplo, 20.000 IOPS / cuenta). También ya no tiene toocopy sus cuentas de almacenamiento de toomultiple imágenes personalizadas (archivos VHD). También puede administrarlos en una ubicación central: una cuenta de almacenamiento por cada región de Azure – y usarlos toocreate cientos de máquinas virtuales en una suscripción.

Discos administrados le permitirá toocreate seguridad too10, VM 000 **discos** en una suscripción, que le permitirá toocreate miles de **máquinas virtuales** en una sola suscripción. Esta característica también aumenta la escalabilidad de Hola de [conjuntos de escala de máquina Virtual (VMSS)](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) permitiéndole toocreate tooa mil las máquinas virtuales en un VMSS con una imagen de Marketplace.

### <a name="better-reliability-for-availability-sets"></a>Mayor confiabilidad para los conjuntos de disponibilidad

Discos administrados ofrece una mayor confiabilidad para conjuntos de disponibilidad al garantizar que Hola discos de [máquinas virtuales en un conjunto de disponibilidad](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) están suficientemente aisladas entre sí tooavoid puntos únicos de error. Para ello y discos de Hola se coloca automáticamente en unidades de escala de almacenamiento diferente (sellos). Si se produce un error en una marca debido un error toohardware o software, solo instancias de máquina virtual de hello con discos de esas marcas producirá un error. Por ejemplo, supongamos que tiene una aplicación que se ejecuta en máquinas virtuales de cinco y hello las máquinas virtuales están en un conjunto de disponibilidad. Hello discos para esas máquinas virtuales no todos almacenarse en hello de la misma marca, para permitir si una marca deja de funcionar, hello otras instancias de la aplicación hello toorun.

### <a name="highly-durable-and-available"></a>Mayor durabilidad y disponibilidad

Los discos de Azure están diseñados para ofrecer una disponibilidad del 99,999 %. Descanse tranquilo sabiendo que tiene tres réplicas de sus datos que aportan alta durabilidad. Si las réplicas de uno o dos incluso teniendo problemas, réplicas restantes Hola ayudan a garantizar la persistencia de los datos y la tolerancia alta frente a errores. Esta arquitectura ha contribuido a que Azure destaque en el sector por ofrecer, de manera constante, durabilidad de nivel empresarial para discos IaaS, con una tasa de error anualizada del 0 %. 

### <a name="granular-access-control"></a>Control de acceso pormenorizado

Puede usar [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md) tooassign permisos específicos para un disco administrado tooone o más usuarios. Administrar discos expone una gran variedad de operaciones, incluidas la lectura, escritura (crear/actualizar), eliminar y recuperar un [firma de acceso compartido (SAS) URI](storage-dotnet-shared-access-signature-part-1.md) disco Hola. Puede conceder acceso tooonly Hola operaciones que una persona debe tooperform su trabajo. Por ejemplo, si no desea un toocopy persona una cuenta de almacenamiento de disco administrado tooa, puede elegir no toogrant acceso toohello acción de exportación de ese disco administrado. De forma similar, si no desea un toouse persona una toocopy de URI de SAS un disco administrado, puede elegir no toogrant ese permiso toohello disco administrado.

### <a name="azure-backup-service-support"></a>Soporte técnico del servicio Azure Backup
Usar servicio de copia de seguridad de Azure con discos administrados toocreate un trabajo de copia de seguridad con copias de seguridad basadas en tiempo, su fácil restauración de máquinas virtuales y las directivas de retención de copia de seguridad. Discos administrados sólo admiten almacenamiento redundante local (LRS) como opción de replicación de hello; Esto significa que mantiene tres copias de datos de hello en una única región. Para recuperación ante desastres regionales, debe realizar una copia de los discos de máquina virtual en una región distinta con el [servicio Azure Backup](../backup/backup-introduction-to-azure-backup.md) y una cuenta de almacenamiento GRS como almacén de copia de seguridad. Copia de seguridad de Azure admite actualmente los tamaños de disco de datos de too1TB para copia de seguridad. En [Uso del servicio de Azure Backup para máquinas virtuales con Managed Disks](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup) puede encontrar más información al respecto.

## <a name="pricing-and-billing"></a>Precios y facturación

Al usar discos administrados, se aplica Hola después de facturación consideraciones:
* Tipo de almacenamiento

* Tamaño del disco

* Número de transacciones

* Transferencias de datos de salida

* Instantáneas de disco administradas (copia de disco completo)

Veámoslas más detalladamente.

**Tipo de almacenamiento:** Managed Disks ofrece 2 niveles de rendimiento: [premium](storage-premium-storage.md) (basado en SSD) y [estándar](storage-standard-storage.md) (basado en HDD). facturación Hola de un disco administrado depende de qué tipo de almacenamiento que seleccionó para el disco de Hola.


**El tamaño de disco**: la facturación de discos administrados depende de tamaño de hello aprovisionado de disco Hola. Mapas de Azure Hola toohello tamaño aprovisionado (redondeado al alza) más cercano de la opción de discos administrados como se especifica en tablas de hello siguientes. Cada tooone de asignaciones de disco administrado de hello admite tamaños de aprovisionamiento y se factura según corresponda. Por ejemplo, si crea un disco administrado estándar y especificar un tamaño aprovisionado de 200 GB, se le facturará según Hola precios del tipo de disco S20 Hola.

Aquí están disponibles para un disco administrado premium tamaños de disco de hello:

| **Tipo de disco <br>administrado premium** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Tamaño del disco        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1.024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Aquí están disponibles para un disco administrado estándar tamaños de disco de hello:

| **Tipo de disco <br>administrado estándar** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Tamaño del disco        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1.024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**Número de transacciones**: se le cobra según número Hola de transacciones que se realizan en un disco administrado estándar. Las transacciones de un disco administrado premium no tienen coste.

**Transferencias de datos de salida**: las [transferencias de datos de salida](https://azure.microsoft.com/pricing/details/data-transfers/) (datos que salen de los centros de datos de Azure) se facturan en función del uso de ancho de banda.

Para obtener información detallada acerca de los precios de Managed Disks, consulte [Precios de Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Instantáneas de disco administradas

Una instantánea administrada es una copia completa de solo lectura de un disco administrado que se almacena como disco administrado estándar de forma predeterminada. Con las instantáneas, puede realizar una copia de seguridad de sus discos administrados en cualquier momento. Estas instantáneas son independientes del disco de origen de Hola y pueden ser usado toocreate nuevos discos administrado. Se facturan según el tamaño de hello usa. Por ejemplo, si crea una instantánea de un disco administrado con capacidad aprovisionada de 64 GB y el tamaño de los datos de uso real de 10 GB, se cobrará instantánea solo Hola usar tamaño de datos de 10 GB.  

[Instantáneas incrementales](storage-incremental-snapshots.md) no se admite actualmente para administrar discos, pero se admitirán en futuras Hola.

toolearn Obtenga más información sobre cómo las instantáneas de toocreate con discos administrados, consulte estos recursos:

* [Creación de una copia del disco duro virtual que se almacene como un disco administrado mediante instantáneas en Windows](../virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Creación de una copia del disco duro virtual que se almacene como un disco administrado mediante instantáneas en Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md)


## <a name="images"></a>Imágenes

Managed Disks también admite la creación de una imagen personalizada administrada. Puede crear una imagen desde un disco duro virtual personalizado en una cuenta de almacenamiento, o bien directamente desde una máquina virtual generalizada (con Sysprep). Captura de una imagen única de todos los discos asociados a una máquina virtual, incluidos Hola OS y discos de datos administrados por. Esto permite crear cientos de máquinas virtuales con la imagen personalizada sin Hola necesita toocopy o administrar las cuentas de almacenamiento.

Para obtener información sobre la creación de imágenes, consulte Hola siguientes artículos:
* [¿Cómo toocapture una imagen administrada de una VM generalizada en Azure](../virtual-machines/windows/capture-image-resource.md)
* [¿Cómo toogeneralize y la captura de una máquina virtual de Linux con Hola 2.0 de CLI de Azure](../virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Imágenes frente a instantáneas

A menudo verá palabra Hola "imagen" utilizada con máquinas virtuales y ahora vea "instantáneas" así. Es importante toounderstand Hola diferencia entre estas. Con Managed Disks, es posible tomar una imagen de una máquina virtual generalizada que se ha desasignado. Esta imagen incluirá todos Hola discos conectados toohello máquina virtual. Puede usar este toocreate imagen una nueva máquina virtual y se incluyen todos los discos de Hola.

Una instantánea es una copia de un disco en el momento de hello en el tiempo que se realiza. Solo se aplica tooone disco. Si tiene una máquina virtual que tiene solo un disco (Hola OS), puede tomar una instantánea o una imagen del mismo y crear una máquina virtual desde la instantánea de Hola o imagen de Hola.

¿Qué sucede si una máquina virtual tiene cinco discos y se seccionan? Puede tomar una instantánea de cada uno de los discos de hello, pero no hay ningún reconocimiento en hello VM del estado de Hola de discos de hello: instantáneas de hello solo saber que hay un disco. En este caso, las instantáneas de hello necesitaría toobe coordinada entre sí y que no se admite actualmente.

## <a name="managed-disks-and-encryption"></a>Managed Disks y cifrado

Hay dos tipos de cifrado toodiscuss en discos de toomanaged de referencia. Hello en primer lugar una es cifrado de servicio de almacenamiento (SSE), que se realiza mediante el servicio de almacenamiento de Hola. Hello segunda es cifrado de disco de Azure, que se puede habilitar en hello OS y discos de datos para las máquinas virtuales.

### <a name="storage-service-encryption-sse"></a>cifrado del servicio de almacenamiento (SSE)

[Cifrado del servicio de almacenamiento de Azure](storage-service-encryption.md) proporciona cifrado en reposo y proteger los datos toomeet los compromisos de seguridad y cumplimiento organizativos. SSE está habilitada de forma predeterminada para todos los discos administrados, las instantáneas y las imágenes en todas las regiones de Hola donde hay discos administrados. A partir del 10 de junio de 2017, todos los nuevos administrados instantáneas de discos o imágenes y escritos tooexisting administrar discos nuevos datos son automáticamente cifrada en reposo con claves administradas por Microsoft.  Visite hello [página de P+F de discos administrados](storage-faq-for-disks.md#managed-disks-and-storage-service-encryption) para obtener más detalles.


### <a name="azure-disk-encryption-ade"></a>Azure Disk Encryption (ADE)

Cifrado de disco de Azure le permite tooencrypt Hola OS y discos de datos usados por una máquina Virtual de IaaS. Esto incluye Managed Disks. Para Windows, las unidades de Hola se cifran mediante tecnología de cifrado de BitLocker de estándar del sector. Para Linux, discos de Hola se cifran mediante la tecnología de hello DM Crypt. Esto está integrado con el almacén de claves de Azure tooallow se toocontrol y administrar claves de cifrado de disco de Hola. Para más información, vea [Azure Disk Encryption para máquinas virtuales IaaS de Windows y Linux](../security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los discos administrados, consulte toohello siguientes artículos.

### <a name="get-started-with-managed-disks"></a>Introducción a Managed Disks

* [Creación de una máquina virtual con Resource Manager y PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Crear una VM de Linux con hello 2.0 de CLI de Azure](../virtual-machines/linux/quick-create-cli.md)

* [Adjuntar un tooa de disco de datos administrados VM de Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md)

* [Agregar una VM de Linux de disco administrado tooa](../virtual-machines/linux/add-disk.md)

* [Scripts d ejemplo de PowerShell de Managed Disks](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Usar Managed Disks en plantillas de Azure Resource Manager](storage-using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Comparación de las opciones de almacenamiento de Managed Disks

* [Discos y Premium Storage](storage-premium-storage.md)

* [Discos y almacenamiento estándar](storage-standard-storage.md)

### <a name="operational-guidance"></a>Guía de operaciones

* [Migrar desde otras plataformas y AWS tooManaged discos en Azure](../virtual-machines/windows/on-prem-to-azure.md)

* [Convertir máquinas virtuales de Azure toomanaged discos en Azure](../virtual-machines/windows/migrate-to-managed-disks.md)
