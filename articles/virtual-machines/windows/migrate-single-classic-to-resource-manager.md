---
title: "aaaMigrate un tooan VM clásico ARM VM de disco administrado | Documentos de Microsoft"
description: "Migrar una sola máquina virtual de Azure de implementación clásica de hello tooManaged discos en el modelo de implementación del Administrador de recursos de Hola de modelo."
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Migrar manualmente un tooa clásico VM nueva ARM VM administrados de disco de hello VHD 


En esta sección le ayuda a toomigrate las máquinas virtuales de Azure existente desde el modelo de implementación clásica de hello demasiado[discos administrados](managed-disks-overview.md) en el modelo de implementación del Administrador de recursos de Hola.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planear la migración de Hola de discos tooManaged

Esta sección le ayudará a mejor decisión de Hola de toomake en tipos de máquina virtual y disco.


### <a name="location"></a>Ubicación

Elija una ubicación donde Azure Managed Disks esté disponible. Si va a migrar discos administrados de tooPremium, asegúrese también de que almacenamiento Premium está disponible en la región de Hola donde piensa toomigrate a. Consulte [Servicios de Azure por región](https://azure.microsoft.com/regions/#services) para información actualizada sobre las ubicaciones disponibles.

### <a name="vm-sizes"></a>Tamaños de VM

Si va a migrar discos administrados de tooPremium, tiene tamaño de hello tooupdate de hello VM tooPremium tamaño con capacidad de almacenamiento disponible en región Hola donde se encuentra la máquina virtual. Revise los tamaños de máquinas virtuales de Hola que son capaces de almacenamiento Premium. se enumeran las especificaciones de tamaño de máquina virtual de Azure de Hello en [tamaños de máquinas virtuales](sizes.md).
Revise las características de rendimiento de Hola de máquinas virtuales que funcionen con el almacenamiento Premium y elija el tamaño más adecuado de hello máquina virtual que mejor se adapte a la carga de trabajo. Asegúrese de que hay suficiente ancho de banda disponible en el tráfico de disco de máquina virtual toodrive Hola.

### <a name="disk-sizes"></a>Tamaños de disco

**Managed Disks Premium**

Hay siete tipos de Managed Disks Premium que se pueden usar con la máquina virtual y cada uno de ellos tiene sus límites específicos de rendimiento y E/S por segundo. Tenga en cuenta estos límites al elegir Hola tipo de disco de Premium para la máquina virtual en función de las necesidades de saludo de la aplicación en cuanto a capacidad, rendimiento, escalabilidad, y la carga máxima.

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamaño del disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1.024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Rendimiento de disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 

**Discos administrados Estándar**

Hay siete tipos de discos administrados Estándar que se pueden usar con la máquina virtual. Cada uno de ellos tiene una capacidad distinta, pero los mismos límites de rendimiento y E/S por segundo. Elija el tipo de Hola de discos administrados estándar según las necesidades de capacidad de saludo de la aplicación.

| Tipo de disco Estándar  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Tamaño del disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1.024 GB (1 TB)   | 2048 GB (2 TB)    | 4095 GB (4 TB)   | 
| IOPS por disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Rendimiento de disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 


### <a name="disk-caching-policy"></a>Directiva de almacenamiento en caché de disco 

**Managed Disks Premium**

De forma predeterminada, es la directiva de caché de disco *de sólo lectura* de Hola a todos los discos de datos Premium, y *lectura y escritura* para el disco del sistema operativo Hola Premium asocia toohello máquina virtual. Esta opción de configuración se recomienda tooachieve Hola un rendimiento óptimo para IOs la aplicación. Para discos de datos de solo escritura o de gran cantidad de escritura (por ejemplo, archivos de registro de SQL Server), deshabilite el almacenamiento en caché de disco para lograr un mejor rendimiento de la aplicación.

### <a name="pricing"></a>Precios

Hola de revisión [precios de discos administrados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Precios de discos administrados de Premium están el mismo que Hola los discos Premium no administrado. Sin embargo, los precios de Managed Disks Estándar son distintos a los de los Unmanaged Disks Estándar.


## <a name="checklist"></a>Lista de comprobación

1.  Si va a migrar discos administrados de tooPremium, asegúrese de que está disponible en la región de Hola que se va a migrar a.

2.  Decidir la serie de hello nuevas máquinas virtuales que va a usar. Debe ser un sistema de almacenamiento Premium capaz si va a migrar discos administrados de tooPremium.

3.  Decidir Hola VM tamaño exacto que va a utilizar que están disponibles en la región de Hola que se va a migrar a. Tamaño de máquina virtual debe toobe número de hello toosupport lo suficientemente grande como de los discos de datos que tiene. Por ejemplo, si tiene cuatro discos de datos, Hola VM debe tener dos o más núcleos. Considere también las necesidades de potencia de procesamiento, memoria y ancho de banda de red.

4.  Tener detalles VM actuales de hello útiles, incluidas las listas de Hola de discos y los blobs de disco duro virtual correspondientes.

Prepare la aplicación para el tiempo de inactividad. toodo una migración limpia, que toostop todo el procesamiento de hello en hello actual sistema. Solo entonces puede obtenerlo tooconsistent estado en el que puede migrar toohello nueva plataforma. Duración del tiempo de inactividad depende de la cantidad de Hola de los datos de hello discos toomigrate.


## <a name="migrate-hello-vm"></a>Migrar Hola VM

Prepare la aplicación para el tiempo de inactividad. toodo una migración limpia, que toostop todo el procesamiento de hello en hello actual sistema. Solo entonces puede obtenerlo tooconsistent estado en el que puede migrar toohello nueva plataforma. Duración del tiempo de inactividad depende cantidad Hola de los datos de hello discos toomigrate.


1.  En primer lugar, establezca los parámetros comunes de hello:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Crear un disco de sistema operativo administrado utilizando Hola VHD de hello VM clásico.

    Asegúrese de que haya proporcionado Hola completar URI de hello parámetro toohello $osVhdUri de disco duro virtual del sistema operativo. Además, escriba **-AccountType** como **PremiumLRS** o **StandardLRS** según el tipo de discos al que migra (Premium o Estándar).

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Adjuntar Hola SO disco toohello nueva máquina virtual.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Crear un disco de datos administrados desde el archivo de disco duro virtual de datos de hello y agregar toohello nueva máquina virtual.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Crear nueva máquina virtual de Hola estableciendo pública IP, la red Virtual y la NIC.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Puede haber pasos adicionales necesarios toosupport la aplicación que no es estarán sujetos a esta guía.
>
>

## <a name="next-steps"></a>Pasos siguientes

- Conectar la máquina virtual de toohello. Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

