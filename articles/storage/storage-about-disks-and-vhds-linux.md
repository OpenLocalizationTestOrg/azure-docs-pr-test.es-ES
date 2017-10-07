---
title: "aaaAbout discos y discos duros virtuales para máquinas virtuales de Linux de Microsoft Azure | Documentos de Microsoft"
description: "Conozca los conceptos básicos de Hola de discos y discos duros virtuales de máquinas virtuales de Linux en Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Acerca de los discos y los discos duros virtuales para máquinas virtuales de Linux en Azure
Al igual que cualquier otro equipo, máquinas virtuales en Azure utilice discos según una toostore lugar un sistema operativo, aplicaciones y datos. Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco del sistema operativo Linux y un disco temporal. disco del sistema operativo Hola se crea a partir de una imagen y disco del sistema operativo de Hola y de imagen de hello son discos duros virtuales (VHD) almacenados en una cuenta de almacenamiento de Azure. Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales. 

En este artículo, se le hable sobre los diferentes usos de Hola para discos de hello y, a continuación, se describen los tipos diferentes de hello de discos, puede crear y utilizar. Este artículo también está disponible para [máquinas virtuales Windows](storage-about-disks-and-vhds-windows.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos usados por las máquinas virtuales

¡Eche un vistazo a cómo se utilizan discos de Hola por hello las máquinas virtuales.

## <a name="operating-system-disk"></a>Disco del sistema operativo
Cada máquina virtual tiene un disco de sistema operativo acoplado. Está registrado como unidad SATA y etiquetado de forma predeterminada como /dev/sda. Este disco tiene una capacidad máxima de 2048 gigabytes (GB). 

## <a name="temporary-disk"></a>Disco temporal
Cada máquina contiene un disco temporal. disco temporal de Hello proporciona almacenamiento a corto plazo para aplicaciones y procesos y datos de almacén de tooonly previsto como página o archivos de intercambio. Datos en disco temporal de hello podrían perderse durante un [evento de mantenimiento](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o cuando se [volver a implementar una máquina virtual](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante un reinicio estándar de hello VM, deben conservar datos hello en la unidad temporal de Hola.

En máquinas virtuales Linux, disco de hello suele **/dev/sdb** y formatea y monta demasiado**/mnt** por hello agente Linux de Azure. tamaño de Hello del disco temporal de hello varía según tamaño Hola de máquina virtual de Hola. Para más información, consulte [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md).

Para obtener más información sobre cómo Azure utiliza disco temporal de hello, consulte [descripción de la unidad temporal de hello en máquinas virtuales de Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Disco de datos
Un disco de datos es un disco duro virtual que es datos de la aplicación de la máquina virtual adjunto tooa toostore y otros datos que necesita tookeep. Los discos de datos se registran como unidades SCSI y se etiquetan con una letra elegida por usted. Cada disco de datos tiene una capacidad máxima de 4095 GB. tamaño de máquina virtual de Hola Hola determina cuántos discos de datos que se puede adjuntar tooit y Hola el tipo de almacenamiento que puede utilizar discos de hello toohost.

> [!NOTE]
> Para ver más detalles acerca de las capacidades de las máquinas virtuales, consulte [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md).
> 

Azure crea un disco del sistema operativo cuando se crea una máquina virtual desde una imagen. Si utiliza una imagen que incluye discos de datos, Azure también crea Hola discos de datos cuando crea la máquina virtual de Hola. En caso contrario, agregue discos de datos después de crear la máquina virtual de Hola.

Puede agregar datos discos tooa virtual machine en cualquier momento, por **adjuntar** Hola máquina virtual de toohello de disco. Puede usar un disco duro virtual que se ha cargado o copiado tooyour cuenta de almacenamiento, o uno que Azure crea para usted. Adjuntar un disco de datos asocia el archivo de disco duro virtual de hello con Hola VM, colocando una "concesión" en hello VHD, por lo que no se puede eliminar del almacenamiento mientras sigue estando asociada.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Pasos siguientes
* [Conectar un disco](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd almacenamiento adicional para la máquina virtual.
* [Configure el RAID de software](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para la redundancia.
* [Capture una máquina virtual Linux](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para poder implementar rápidamente máquinas virtuales adicionales.

