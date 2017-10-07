---
title: aaaManage Azure discos con hello CLI de Azure | Documentos de Microsoft
description: 'Tutorial: administrar los discos de Azure con hello CLI de Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Administrar discos de Azure con hello CLI de Azure

Máquinas virtuales de Azure usa el sistema operativo de discos toostore hello las máquinas virtuales, aplicaciones y datos. Al crear una máquina virtual es importante toochoose un tamaño de disco y carga de trabajo de configuración adecuado toohello que se esperaba. Este tutorial trata la implementación y administración de discos de máquina virtual. Aprenderá sobre los siguientes temas:

> [!div class="checklist"]
> * Discos del SO y temporales
> * Discos de datos
> * Discos Estándar y Premium
> * Rendimiento de disco
> * Conectar y preparar los discos de datos
> * Cambiar el tamaño de los discos
> * Instantáneas de disco


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Discos de Azure predeterminados

Cuando se crea una máquina virtual de Azure, dos discos son máquinas virtuales de toohello unido automáticamente. 

**Disco del sistema operativo** : discos del sistema operativo se pueden cambiar la too1 terabytes y hosts Hola sistema operativo de las máquinas virtuales. Hola SO disco se etiqueta */dev/sda* de forma predeterminada. configuración de disco del sistema operativo Hola el almacenamiento en caché de disco de Hello está optimizado para el rendimiento del sistema operativo. Debido a esta configuración, Hola disco del sistema operativo **no debería** hospedar aplicaciones o datos. Para aplicaciones y datos, use discos de datos, que se detallan más adelante en este artículo. 

**Disco temporal** -temporales discos utilizan una unidad de estado sólida que se encuentra en hello mismo host de Azure como Hola máquina virtual. Los discos temporales son muy eficiente y se pueden usar para operaciones tales como el procesamiento temporal de los datos. Sin embargo, si Hola VM es tooa movida nuevo host, se quitará cualquier dato almacenado en un disco temporal. tamaño de Hola de disco temporal de Hola se determina por hello tamaño de máquina virtual. Los discos temporales llevan la etiqueta */dev/sdb* y tienen un punto de montaje de */mnt*.

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

Los discos Premium están respaldados por un disco de latencia reducida y alto rendimiento basado en SSD. Es perfecto para máquinas virtuales que ejecutan cargas de trabajo de producción. Premium Storage es compatible con las máquinas virtuales de las series DS, DSv2, GS y FS. Los discos Premium vienen en tres tipos (P10, P20, P30), tamaño de hello del disco de hello determina el tipo de disco de Hola. Al seleccionar esta opción, un valor de Hola de tamaño de disco se redondea toohello siguiente tipo. Por ejemplo, si el tamaño del disco de hello es inferior a 128 GB, tipo de disco de hello es P10. Si el tamaño del disco de hello es entre 129 y 512 GB, tamaño de hello es un P20. Nada más de 512 GB, tamaño de hello es un P30.

### <a name="premium-disk-performance"></a>Rendimiento del disco Premium

|Tipo de disco de Premium Storage | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Tamaño del disco (redondeo hacia arriba) | 128 GB | 512 GB | 1024 GB (1 TB) |
| Máximo de IOPS por disco | 500 | 2,300 | 5.000 |
Rendimiento de disco | 100 MB/s | 150 MB/s | 200 MB/s |

Mientras Hola por encima de la tabla identifica máximo de IOPS por disco, se consigue un mayor nivel de rendimiento por varios discos de datos de creación de bandas. Por ejemplo, una máquina virtual Standard_GS5 puede conseguir 80 000 IOPS como máximo. Para más información sobre el número máximo de IOPS por máquina virtual, consulte los [tamaños de máquinas virtuales Linux](sizes.md).

## <a name="create-and-attach-disks"></a>Creación y conexión de discos

Discos de datos se pueden crear y conectados en el momento de la creación de máquinas virtuales o tooan existente de la máquina virtual.

### <a name="attach-disk-at-vm-creation"></a>Conexión del disco en el momento de creación de la máquina virtual

Crear un grupo de recursos con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Crear una máquina virtual mediante hello [crear vm az]( /cli/azure/vm#create) comando. Hola `--datadisk-sizes-gb` argumento es usado toospecify que un disco adicional debe crearse y adjunta la máquina virtual de toohello. toocreate y adjuntar más de un disco, use una lista delimitada por espacios de los valores de tamaño de disco. En el siguiente ejemplo de Hola, se crea una máquina virtual con discos de datos de dos, ambos 128 GB. Dado que los tamaños de disco Hola son 128 GB, estos discos se configuran como P10s, que proporcionan el máximo de 500 IOPS por disco.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Adjuntar disco tooexisting VM

toocreate y conectar una máquina virtual existente de disco tooan nuevo, use hello [adjuntar el disco de vm az](/cli/azure/vm/disk#attach) comando. Hello en el ejemplo siguiente se crea un disco de premium, 128 gigabytes de tamaño y lo adjunta toohello que crea la VM en el último paso de Hola.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Preparación de los discos de datos

Una vez instalado un disco de máquina virtual de toohello adjunto, sistema operativo de hello debe toobe configurado toouse Hola disco. Hola de ejemplo siguiente muestra cómo configurar toomanually en un disco. Este proceso también se puede automatizar mediante cloud-init, que se trata en un [tutorial posterior](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuración manual

Crear una conexión SSH con la máquina virtual de Hola. Reemplace la dirección IP de ejemplo de Hola con la dirección IP pública de Hola de máquina virtual de Hola.

```azurecli-interactive 
ssh 52.174.34.95
```

Disco de partición Hola con `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Escribir una partición de toohello de sistema de archivos mediante el uso de hello `mkfs` comando.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Montar el disco nuevo de Hola para que sea accesible en el sistema operativo de Hola.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

disco de Hello ahora puede obtenerse a través de hello *datadrive* punto de montaje, que se puede comprobar mediante la ejecución de hello `df -h` comando. 

```bash
df -h
```

salida de Hello muestra una nueva unidad de hello montado en */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure que Hola unidad se vuelve a montar tras un reinicio, debe agregarse toohello */etcetera/fstab* archivo. toodo por lo tanto, obtener Hola UUID del disco de hello con hello `blkid` utilidad.

```bash
sudo -i blkid
```

salida de Hello muestra hello UUID de la unidad de hello, `/dev/sdc1` en este caso.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Agregar un toohello similar de línea después de toohello */etcetera/fstab* archivo. Tenga en cuenta también que las barreras de escritura puede deshabilitarse mediante *barrier=0*; esta configuración puede mejorar el rendimiento del disco. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Ahora que hello disco se ha configurado, cierre la sesión de SSH de Hola.

```bash
exit
```

## <a name="resize-vm-disk"></a>Cambio del tamaño de disco de una máquina virtual

Una vez que se ha implementado una máquina virtual, el disco del sistema operativo de Hola o los discos de datos adjunto se pueden aumentar de tamaño. Aumentar tamaño de Hola de un disco resulta beneficioso cuando se necesita más espacio de almacenamiento o un mayor nivel de rendimiento (P10, P20, P30). Cabe mencionar que no se puede reducir el tamaño de los discos.

Antes de aumentar el tamaño del disco, Hola Id. o nombre de disco de hello es necesario. Hola de uso [lista de discos az](/cli/azure/vm/disk#list) tooreturn comando todos los discos en un grupo de recursos. Tome nota del nombre de disco de Hola que desearía tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Hola VM también debe ser desasignado. Hola de uso [cancelar la asignación de máquina virtual az]( /cli/azure/vm#deallocate) comando toostop y cancelar la asignación Hola máquina virtual.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Hola de uso [actualización de disco az](/cli/azure/vm/disk#update) disco de comando tooresize Hola. Este ejemplo cambia el tamaño de un disco llamado *myDataDisk* too1 terabyte.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Una vez completada la operación de cambio de tamaño de hello, inicie Hola máquina virtual.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Si ha cambiado el tamaño Hola operativo disco del sistema, se expande automáticamente partición Hola. Si ha cambiado el tamaño de un disco de datos, cualquier partición actual necesita toobe expandir en el sistema operativo de las máquinas virtuales de Hola.

## <a name="snapshot-azure-disks"></a>Captura de instantáneas de discos de Azure

Tomar una instantánea de disco, crea una copia de únicamente, en un momento lectura del disco de Hola. Instantáneas de máquina virtual de Azure son útiles para guardar rápidamente el estado de Hola de una máquina virtual antes de realizar cambios de configuración. En caso de hello cambios de configuración hello demostrar toobe no deseada, estado de VM puede restaurarse con instantáneas de Hola. Cuando una máquina virtual tiene más de un disco, se toma una instantánea de cada disco independientemente de hello otros usuarios. Para realizar copias de seguridad coherente de aplicación, considere la posibilidad de detener Hola VM antes de tomar instantáneas de disco. O bien, usar hello [servicio de copia de seguridad de Azure](/azure/backup/), lo que permite tooperform automatizada copias de seguridad mientras Hola VM se esté ejecutando.

### <a name="create-snapshot"></a>Creación de una instantánea

Antes de crear una instantánea de disco de máquina virtual, hello identificador o nombre de disco de hello es necesario. Hola de uso [mostrar de la máquina virtual de az](https://docs.microsoft.com/en-us/cli/azure/vm#show) Id. de comando tooreturn Hola disco. En este ejemplo, Id. de disco de Hola se almacena en una variable para que se puede utilizar en un paso posterior.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Ahora que tiene el Id. de hello del disco de máquina virtual de hello, hello siguiente comando crea una instantánea del disco de Hola.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Creación del disco a partir de la instantánea

Esta instantánea, a continuación, se puede convertir en un disco, que puede ser la máquina virtual de toorecreate usado Hola.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Restauración de la máquina virtual a partir de la instantánea

recuperación de máquina virtual toodemonstrate, máquina de virtual existente de eliminación Hola. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Crear una nueva máquina virtual desde el disco de la instantánea de Hola.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Reconexión de un disco de datos

Todos los discos de datos necesitan máquina virtual de toohello de toobe volver a adjuntar.

Encontrar primero un nombre de disco de datos hello mediante hello [lista de discos az](https://docs.microsoft.com/cli/azure/disk#list) comando. En este ejemplo lugares Hola nombre del disco de hello en una variable denominada *datadisk*, que se usa en el paso siguiente de saludo.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Hola de uso [adjuntar el disco de vm az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco de comando tooattach Hola.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido sobre temas relacionados con los discos de máquina virtual; por ejemplo:

> [!div class="checklist"]
> * Discos del SO y temporales
> * Discos de datos
> * Discos Estándar y Premium
> * Rendimiento de disco
> * Conectar y preparar los discos de datos
> * Cambiar el tamaño de los discos
> * Instantáneas de disco

Avanzar toohello toolearn de tutorial siguiente acerca de cómo automatizar la configuración de máquina virtual.

> [!div class="nextstepaction"]
> [Automatización de la configuración de máquinas virtuales](./tutorial-automate-vm-deployment.md)
