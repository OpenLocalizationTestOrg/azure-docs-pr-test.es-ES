---
title: "aaaAbout discos y discos duros virtuales para máquinas virtuales de Windows de Microsoft Azure | Documentos de Microsoft"
description: "Conozca los conceptos básicos de Hola de discos y máquinas virtuales de discos duros virtuales para Windows en Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Acerca de los discos y los discos duros virtuales para máquinas virtuales de Windows en Azure
Al igual que cualquier otro equipo, máquinas virtuales en Azure utilice discos según una toostore lugar un sistema operativo, aplicaciones y datos. Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal. disco del sistema operativo Hola se crea a partir de una imagen y disco del sistema operativo de Hola y de imagen de hello son discos duros virtuales (VHD) almacenados en una cuenta de almacenamiento de Azure. Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales. 

En este artículo, se le hable sobre los diferentes usos de Hola para discos de hello y, a continuación, se describen los tipos diferentes de hello de discos, puede crear y utilizar. Este artículo también está disponible para [máquinas virtuales Linux](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos usados por las máquinas virtuales

¡Eche un vistazo a cómo se utilizan discos de Hola por hello las máquinas virtuales.

### <a name="operating-system-disk"></a>Disco del sistema operativo
Cada máquina virtual tiene un disco de sistema operativo acoplado. Se ha registrado como unidad SATA y etiquetada como unidad C: de Hola de forma predeterminada. Este disco tiene una capacidad máxima de 2048 gigabytes (GB). 

### <a name="temporary-disk"></a>Disco temporal
Cada máquina contiene un disco temporal. disco temporal de Hello proporciona almacenamiento a corto plazo para aplicaciones y procesos y datos de almacén de tooonly previsto como página o archivos de intercambio. Datos en disco temporal de hello podrían perderse durante un [evento de mantenimiento](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o cuando se [volver a implementar una máquina virtual](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Durante un reinicio estándar de hello VM, deben conservar datos hello en la unidad temporal de Hola.

disco temporal de Hola se etiqueta como unidad D: Hola de forma predeterminada y se utiliza para almacenar pagefile.sys. tooremap esta letra de unidad diferente de tooa de disco, consulte [cambiar la letra de unidad Hola de disco temporal de Windows hello](../virtual-machines/windows/change-drive-letter.md). tamaño de Hello del disco temporal de hello varía según tamaño Hola de máquina virtual de Hola. Para más información, consulte [Tamaños de las máquinas virtuales Windows](../virtual-machines/windows/sizes.md).

Para obtener más información sobre cómo Azure utiliza disco temporal de hello, consulte [descripción de la unidad temporal de hello en máquinas virtuales de Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Disco de datos
Un disco de datos es un disco duro virtual que es datos de la aplicación de la máquina virtual adjunto tooa toostore y otros datos que necesita tookeep. Los discos de datos se registran como unidades SCSI y se etiquetan con una letra elegida por usted. Cada disco de datos tiene una capacidad máxima de 4095 GB. tamaño de máquina virtual de Hola Hola determina cuántos discos de datos que se puede adjuntar tooit y Hola el tipo de almacenamiento que puede utilizar discos de hello toohost.

> [!NOTE]
> Para más información acerca de las capacidades de las máquinas virtuales, consulte [Tamaños de las máquinas virtuales Windows](../virtual-machines/windows/sizes.md).
> 

Azure crea un disco del sistema operativo cuando se crea una máquina virtual desde una imagen. Si utiliza una imagen que incluye discos de datos, Azure también crea Hola discos de datos cuando crea la máquina virtual de Hola. En caso contrario, agregue discos de datos después de crear la máquina virtual de Hola.

Puede agregar datos discos tooa virtual machine en cualquier momento, por **adjuntar** Hola máquina virtual de toohello de disco. Puede usar un disco duro virtual que se ha cargado o copiado tooyour cuenta de almacenamiento, o uno que Azure crea para usted. Adjuntar un disco de datos asocia el archivo de disco duro virtual de hello con hello VM colocando una "concesión" en hello VHD, por lo que no se puede eliminar del almacenamiento mientras sigue estando asociada.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Una última recomendación: utilice TRIM con los discos estándar no administrados 

Si utiliza discos estándar no administrados (HDD), debería habilitar TRIM. TRIM descarta los bloques sin utilizar en el disco de Hola, por lo que solo se le facturará de almacenamiento que utiliza realmente. Esto puede suponerle un ahorro si crea archivos grandes y, luego, los elimina. 

Puede ejecutar esta opción de RECORTE de comando toocheck Hola. Abra un símbolo del sistema en su máquina virtual de Windows y escriba:


```
fsutil behavior query DisableDeleteNotify
```

Si el comando de hello devuelve 0, RECORTE está habilitada correctamente. Si devuelve 1, ejecute hello después tooenable comando RECORTE:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Nota: Compatibilidad para Trim comienza con Windows Server 2012 / Windows 8 y posteriores, consulte vea [nueva API permite a las aplicaciones de medios de toostorage de sugerencias "Recortar y anular la asignación de" toosend](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Pasos siguientes
* [Conectar un disco](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd almacenamiento adicional para la máquina virtual.
* [Cambiar la letra de unidad Hola de disco temporal de Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) por lo que la aplicación puede usar la unidad D: de Hola para los datos.

