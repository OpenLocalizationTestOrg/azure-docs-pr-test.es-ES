---
title: aaaManage Azure discos con hello Azure PowerShell | Documentos de Microsoft
description: 'Tutorial: administrar los discos de Azure con hello Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Administración de discos de Azure con PowerShell

Máquinas virtuales de Azure usa el sistema operativo de discos toostore hello las máquinas virtuales, aplicaciones y datos. Al crear una máquina virtual es importante toochoose un tamaño de disco y carga de trabajo de configuración adecuado toohello que se esperaba. Este tutorial trata la implementación y administración de discos de máquina virtual. Aprenderá sobre los siguientes temas:

> [!div class="checklist"]
> * Discos del SO y temporales
> * Discos de datos
> * Discos Estándar y Premium
> * Rendimiento de disco
> * Conectar y preparar los discos de datos

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Discos de Azure predeterminados

Cuando se crea una máquina virtual de Azure, dos discos son máquinas virtuales de toohello unido automáticamente. 

**Disco del sistema operativo** : discos del sistema operativo se pueden cambiar la too1 terabytes y hosts Hola sistema operativo de las máquinas virtuales.  disco de SO Hola se asigna una letra de unidad de *c:* de forma predeterminada. configuración de disco del sistema operativo Hola el almacenamiento en caché de disco de Hello está optimizado para el rendimiento del sistema operativo. disco de SO Hello **no debería** hospedar aplicaciones o datos. Para aplicaciones y datos, use un disco de datos. Explicamos esto más adelante en este artículo.

**Disco temporal** -temporales discos utilizan una unidad de estado sólida que se encuentra en hello mismo host de Azure como Hola máquina virtual. Los discos temporales son muy eficiente y se pueden usar para operaciones tales como el procesamiento temporal de los datos. Sin embargo, si Hola VM es tooa movida nuevo host, se quitará cualquier dato almacenado en un disco temporal. tamaño de Hola de disco temporal de Hola se determina por hello tamaño de máquina virtual. A los discos temporales se les asigna una letra de unidad de *d:* de forma predeterminada.

### <a name="temporary-disk-sizes"></a>Tamaños de disco temporal

| Tipo | Tamaño de VM | Tamaño máximo de disco temporal (GB) |
|----|----|----|
| [Uso general](sizes-general.md) | Series A y D | 800 |
| [Proceso optimizado](sizes-compute.md) | Serie F | 800 |
| [Memoria optimizada](../virtual-machines-windows-sizes-memory.md) | Series D y G | 6144 |
| [Almacenamiento optimizado](../virtual-machines-windows-sizes-storage.md) | Serie L | 5630 |
| [GPU](sizes-gpu.md) | Serie N | 1440 |
| [Alto rendimiento](sizes-hpc.md) | Series A y H | 2000 |

## <a name="azure-data-disks"></a>Discos de datos de Azure

Se pueden agregar discos de datos adicionales para instalar aplicaciones y almacenar datos. Los discos de datos deben usarse en cualquier situación donde desee un almacenamiento de datos duradero y con capacidad de respuesta. Cada disco de datos tiene una capacidad máxima de 1 terabyte. tamaño de Hola de máquina virtual de Hola determina cuántos discos de datos pueden estar adjunto tooa máquina virtual. Para cada núcleo de la máquina virtual, se pueden conectar dos discos de datos. 

### <a name="max-data-disks-per-vm"></a>Discos de datos máximos por máquina virtual

| Tipo | Tamaño de VM | Discos de datos máximos por máquina virtual |
|----|----|----|
| [Uso general](sizes-general.md) | Series A y D | 32 |
| [Proceso optimizado](sizes-compute.md) | Serie F | 32 |
| [Memoria optimizada](../virtual-machines-windows-sizes-memory.md) | Series D y G | 64 |
| [Almacenamiento optimizado](../virtual-machines-windows-sizes-storage.md) | Serie L | 64 |
| [GPU](sizes-gpu.md) | Serie N | 48 |
| [Alto rendimiento](sizes-hpc.md) | Series A y H | 32 |

## <a name="vm-disk-types"></a>Tipos de disco de máquina virtual

Azure proporciona dos tipos de disco.

### <a name="standard-disk"></a>Disco estándar

El almacenamiento estándar está respaldado por unidades de disco duro y ofrece un almacenamiento rentable al mismo tiempo que tiene un rendimiento superior. Los discos estándar son ideales para cargas de trabajo de desarrollo y prueba rentables.

### <a name="premium-disk"></a>Disco Premium

Los discos Premium están respaldados por un disco de latencia reducida y alto rendimiento basado en SSD. Es perfecto para máquinas virtuales que ejecutan cargas de trabajo de producción. Premium Storage es compatible con las máquinas virtuales de las series DS, DSv2, GS y FS. Los discos Premium vienen en tres tipos (P10, P20, P30), tamaño de hello del disco de hello determina el tipo de disco de Hola. Al seleccionar esta opción, un valor de Hola de tamaño de disco se redondea toohello siguiente tipo. Por ejemplo, si el tamaño de hello está por debajo de tipo de disco de 128 GB Hola será P10, entre 129 y 512 P20 y más de 512 P30. 

### <a name="premium-disk-performance"></a>Rendimiento del disco Premium

|Tipo de disco de Premium Storage | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Tamaño del disco (redondeo hacia arriba) | 128 GB | 512 GB | 1024 GB (1 TB) |
| IOPS por disco | 500 | 2,300 | 5.000 |
Rendimiento de disco | 100 MB/s | 150 MB/s | 200 MB/s |

Mientras Hola por encima de la tabla identifica máximo de IOPS por disco, se consigue un mayor nivel de rendimiento por varios discos de datos de creación de bandas. Por ejemplo, 64 datos discos pueden estar conectado tooStandard_GS5 VM. Si cada uno de estos discos tienen un tamaño de P30, se puede lograr un máximo de 80 000 IOPS. Para obtener información detallada sobre las IOPS máximas por máquina virtual, consulte el artículo sobre [tamaños de máquinas virtuales Linux](./sizes.md).

## <a name="create-and-attach-disks"></a>Creación y conexión de discos

ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente. Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una. Cuando reemplace trabajar a través de tutorial de hello, grupo de recursos de Hola y VM nombres cuando sea necesario.

Crear la configuración inicial de hello con [AzureRmDiskConfig nuevo](/powershell/module/azurerm.compute/new-azurermdiskconfig). Hola de ejemplo siguiente configura un disco que es de 128 gigabytes de tamaño.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Crear disco de datos de hello con hello [AzureRmDisk New](/powershell/module/azurerm.compute/new-azurermdisk) comando.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Get hello máquina virtual que tooadd Hola Hola de toowith de disco de datos [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Agregar configuración de máquina virtual de toohello Hola datos disco con hello [AzureRmVMDataDisk agregar](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Actualizar la máquina virtual de hello con hello [AzureRmVM actualización](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Preparación de los discos de datos

Una vez instalado un disco de máquina virtual de toohello adjunto, sistema operativo de hello debe toobe configurado toouse Hola disco. Hello en el ejemplo siguiente se muestra cómo configurar el primer disco Hola de agrega toomanually toohello máquina virtual. También se puede automatizar este proceso con hello [extensión de script personalizado](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuración manual

Crear una conexión RDP con la máquina virtual de Hola. Abra PowerShell y ejecute este script.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido sobre temas relacionados con los discos de máquina virtual; por ejemplo:

> [!div class="checklist"]
> * Discos del SO y temporales
> * Discos de datos
> * Discos Estándar y Premium
> * Rendimiento de disco
> * Conectar y preparar los discos de datos

Avanzar toohello toolearn de tutorial siguiente acerca de cómo automatizar la configuración de máquina virtual.

> [!div class="nextstepaction"]
> [Automatización de la configuración de máquinas virtuales](./tutorial-automate-vm-deployment.md)
