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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="bae4d-103">Convertir Azure administra el almacenamiento de discos de toopremium estándar y viceversa.</span><span class="sxs-lookup"><span data-stu-id="bae4d-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="bae4d-104">Managed Disks ofrece dos opciones de almacenamiento: [Premium](../../storage/storage-premium-storage.md) (basado en SSD) y [Estándar](../../storage/storage-standard-storage.md) (basado en HDD).</span><span class="sxs-lookup"><span data-stu-id="bae4d-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="bae4d-105">Permite cambiar de tooeasily entre las opciones de hello dos con el tiempo de inactividad mínimo según sus necesidades de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="bae4d-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="bae4d-106">Esta funcionalidad no está disponible con discos no administrados.</span><span class="sxs-lookup"><span data-stu-id="bae4d-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="bae4d-107">Pero puede fácilmente [convertir discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily conmutador entre las opciones de hello dos.</span><span class="sxs-lookup"><span data-stu-id="bae4d-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="bae4d-108">Este artículo muestra cómo tooconvert administra los discos de toopremium estándar y viceversa mediante CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae4d-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="bae4d-109">Si necesita tooinstall o actualizarlo, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bae4d-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bae4d-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bae4d-110">Before you begin</span></span>

* <span data-ttu-id="bae4d-111">conversión de Hello requiere un reinicio de hello VM, por lo que programar la migración de Hola de discos del almacenamiento de datos durante un período de mantenimiento existente.</span><span class="sxs-lookup"><span data-stu-id="bae4d-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="bae4d-112">Si usas discos no administrados, en primer lugar [convertir discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse esta tooswitch artículo entre las opciones de almacenamiento de hello dos.</span><span class="sxs-lookup"><span data-stu-id="bae4d-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="bae4d-113">Convert Hola a todos los discos de una máquina virtual administrados por de toopremium estándar y viceversa.</span><span class="sxs-lookup"><span data-stu-id="bae4d-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="bae4d-114">En el siguiente ejemplo de Hola, mostramos cómo tooswitch todos los discos de una máquina virtual desde el almacenamiento de toopremium estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="bae4d-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="bae4d-115">discos administrados por toouse premium, la máquina virtual debe usar un [tamaño de máquina virtual](sizes.md) que admite el almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="bae4d-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="bae4d-116">En este ejemplo también cambia de tamaño de tooa que admite el almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="bae4d-116">This example also switches tooa size that supports premium storage.</span></span>

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="bae4d-117">Convertir un disco administrado de toopremium estándar y viceversa.</span><span class="sxs-lookup"><span data-stu-id="bae4d-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="bae4d-118">Para la carga de trabajo de desarrollo y pruebas, puede que desee toohave mezcla de discos estándar y premium tooreduce su costo.</span><span class="sxs-lookup"><span data-stu-id="bae4d-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="bae4d-119">Que puede realizar mediante la actualización de almacenamiento de toopremium, solo los discos de Hola que requieren un mejor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="bae4d-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="bae4d-120">En el siguiente ejemplo de Hola, mostramos cómo tooswitch un único disco de una máquina virtual desde el almacenamiento de toopremium estándar y viceversa.</span><span class="sxs-lookup"><span data-stu-id="bae4d-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="bae4d-121">discos administrados por toouse premium, la máquina virtual debe usar un [tamaño de máquina virtual](sizes.md) que admite el almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="bae4d-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="bae4d-122">En este ejemplo también cambia de tamaño de tooa que admite el almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="bae4d-122">This example also switches tooa size that supports premium storage.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bae4d-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bae4d-123">Next steps</span></span>

<span data-ttu-id="bae4d-124">Realice una copia de solo lectura de una máquina virtual mediante [instantáneas](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="bae4d-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

