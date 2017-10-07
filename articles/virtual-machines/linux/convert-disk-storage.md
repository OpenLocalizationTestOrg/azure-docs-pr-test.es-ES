---
title: "aaaConvert Azure administra el almacenamiento de discos de toopremium estándar y viceversa. | Documentos de Microsoft"
description: "Cómo tooconvert Azure administra el almacenamiento de discos de toopremium estándar y viceversa, mediante el uso de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Convertir Azure administra el almacenamiento de discos de toopremium estándar y viceversa.

Managed Disks ofrece dos opciones de almacenamiento: [Premium](../../storage/storage-premium-storage.md) (basado en SSD) y [Estándar](../../storage/storage-standard-storage.md) (basado en HDD). Permite cambiar de tooeasily entre las opciones de hello dos con el tiempo de inactividad mínimo según sus necesidades de rendimiento. Esta funcionalidad no está disponible con discos no administrados. Pero puede fácilmente [convertir discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily conmutador entre las opciones de hello dos.

Este artículo muestra cómo tooconvert administra los discos de toopremium estándar y viceversa mediante CLI de Azure. Si necesita tooinstall o actualizarlo, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Antes de empezar

* conversión de Hello requiere un reinicio de hello VM, por lo que programar la migración de Hola de discos del almacenamiento de datos durante un período de mantenimiento existente. 
* Si usas discos no administrados, en primer lugar [convertir discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse esta tooswitch artículo entre las opciones de almacenamiento de hello dos. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Convert Hola a todos los discos de una máquina virtual administrados por de toopremium estándar y viceversa.

En el siguiente ejemplo de Hola, mostramos cómo tooswitch todos los discos de una máquina virtual desde el almacenamiento de toopremium estándar de Hola. discos administrados por toouse premium, la máquina virtual debe usar un [tamaño de máquina virtual](sizes.md) que admite el almacenamiento premium. En este ejemplo también cambia de tamaño de tooa que admite el almacenamiento premium.

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Convertir un disco administrado de toopremium estándar y viceversa.

Para la carga de trabajo de desarrollo y pruebas, puede que desee toohave mezcla de discos estándar y premium tooreduce su costo. Que puede realizar mediante la actualización de almacenamiento de toopremium, solo los discos de Hola que requieren un mejor rendimiento. En el siguiente ejemplo de Hola, mostramos cómo tooswitch un único disco de una máquina virtual desde el almacenamiento de toopremium estándar y viceversa. discos administrados por toouse premium, la máquina virtual debe usar un [tamaño de máquina virtual](sizes.md) que admite el almacenamiento premium. En este ejemplo también cambia de tamaño de tooa que admite el almacenamiento premium.

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a>Pasos siguientes

Realice una copia de solo lectura de una máquina virtual mediante [instantáneas](snapshot-copy-managed-disk.md).

