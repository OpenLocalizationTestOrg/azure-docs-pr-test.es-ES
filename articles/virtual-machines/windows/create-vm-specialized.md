---
title: aaaCreate una VM de Windows desde un disco duro virtual especializado en Azure | Documentos de Microsoft
description: "Crear una nueva máquina virtual de Windows si se adjunta un disco especializado administrado como disco del sistema operativo hello en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Creación de una máquina virtual Windows a partir de un disco especializado

Crear una nueva máquina virtual si se adjunta un disco especializado administrado como disco del sistema operativo hello mediante Powershell. Un disco especializado es una copia del disco duro virtual (VHD) de una máquina virtual existente que mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original. 

Cuando se usa un toocreate VHD especializada una nueva máquina virtual, Hola nueva máquina virtual conserva el nombre de equipo de Hola Hola VM original. También se conserva otra información específica del equipo y, en algunos casos, esta información duplicada podría ocasionar problemas. Tenga en cuenta en qué tipo de información específica del equipo se basan las aplicaciones al copiar una máquina virtual.

Tiene dos opciones:
* [Carga de un disco duro virtual](#option-1-upload-a-specialized-vhd)
* [Copia de una máquina virtual de Azure existente](#option-2-copy-an-existing-azure-vm)

Este tema muestra cómo toouse administra los discos. Si tiene una implementación heredada que requiere el uso de una cuenta de Storage, vea [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md) (Creación de una máquina virtual a partir de un VHD especializado en una cuenta de Storage).

## <a name="before-you-begin"></a>Antes de empezar
Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).


## <a name="option-1-upload-a-specialized-vhd"></a>Opción 1: Cargar un VHD especializado

Puede cargar Hola que VHD de una máquina virtual especializada creado con una herramienta de virtualización local, como Hyper-V o una máquina virtual exportado desde otra nube.

### <a name="prepare-hello-vm"></a>Preparar Hola VM
Si piensa toouse Hola VHD como-es toocreate una nueva máquina virtual, asegúrese de que se completa Hola pasos. 
  
  * [Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **No** generalizar Hola VM con Sysprep.
  * Quite todas las herramientas de virtualización de invitado y los agentes instalados en hello VM (por ejemplo, las herramientas de VMware).
  * Asegúrese de hello VM es toopull configurado su dirección IP y la configuración de DNS a través de DHCP. Esto garantiza que el servidor hello Obtiene una dirección IP dentro de la red virtual de hello cuando se inicia. 


### <a name="get-hello-storage-account"></a>Obtener la cuenta de almacenamiento de Hola
Se necesita un almacenamiento cuenta en Azure toostore Hola carga VHD. Puede usar una cuenta de almacenamiento existente o crear una nueva. 

cuentas de almacenamiento disponibles de hello tooshow, escriba:

```powershell
Get-AzureRmStorageAccount
```

Si desea que toouse una cuenta de almacenamiento existente, continúe toohello [carga Hola VHD](#upload-the-vhd-to-your-storage-account) sección.

Si necesita toocreate una cuenta de almacenamiento, siga estos pasos:

1. Se necesita el nombre de Hola Hola del grupo de recursos donde se debe crear la cuenta de almacenamiento de Hola. toofind todos los grupos de recursos de Hola que se encuentran en su suscripción, tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate un grupo de recursos denominado *myResourceGroup* Hola *West US* región, escriba:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Crear una cuenta de almacenamiento denominada *mystorageaccount* en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Cargar la cuenta de almacenamiento de hello VHD tooyour 
Hola de uso [AzureRmVhd agregar](/powershell/module/azurerm.compute/add-azurermvhd) contenedor cmdlet tooupload Hola VHD tooa en su cuenta de almacenamiento. En este ejemplo Hola a cargas de archivo *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa cuenta de almacenamiento denominada *mystorageaccount* en hello *myResourceGroup* grupo de recursos. archivo de Hola se almacena en el contenedor de hello denominado *mycontainer* y nombre de archivo nuevo de hello será *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Si se realiza correctamente, obtendrá una respuesta que busca toothis similar:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Crear un disco administrado desde Hola VHD

Crear un disco administrado desde Hola especializado de disco duro virtual en su cuenta de almacenamiento mediante [AzureRMDisk nuevo](/powershell/module/azurerm.compute/new-azurermdisk). Este ejemplo se utiliza **myOSDisk1** para el nombre del disco hello, coloca Hola disco en *StandardLRS* almacenamiento y usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como Hola URI para el origen de hello VHD.

Crear un nuevo grupo de recursos para hello nueva máquina virtual.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Crear nuevo disco de SO Hola de hello carga VHD. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Opción 2: Copiar una máquina virtual de Azure existente

Puede crear una copia de una máquina virtual que utiliza discos administrados tomando una instantánea de máquina virtual de hello, a continuación, mediante ese toocreate instantánea un nuevo administrado disco y una nueva máquina virtual.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Tomar una instantánea del disco del sistema operativo Hola

Puede realizar una instantánea de una máquina virtual completa (incluidos todos los discos) o solo de un disco. Hello pasos siguientes muestran cómo Hola tootake una instantánea de solo Hola SO disco de la VM con [AzureRmSnapshot New](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet. 

Configure algunos parámetros. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Obtenga el objeto de VM de Hola.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Obtener nombre de disco de SO Hola.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Crear configuración de instantáneas de Hola. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Tomar instantánea de Hola.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Si tiene previsto toouse Hola instantánea toocreate una máquina virtual que necesita toobe alto rendimiento, use el parámetro hello `-AccountType Premium_LRS` con el comando hello AzureRmSnapshot de nuevo. parámetro Hello crea instantáneas de Hola para que se almacena como un disco de Premium administrados. Managed Disks Premium son más costosos que los Estándar. Por tanto, asegúrese de que realmente necesita Premium antes de usar el parámetro hello.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Crear un nuevo disco de instantánea de Hola

Crear un disco administrado desde Hola instantánea mediante [AzureRMDisk nuevo](/powershell/module/azurerm.compute/new-azurermdisk). Este ejemplo se utiliza *myOSDisk* para el nombre del disco Hola.

Crear un nuevo grupo de recursos para hello nueva máquina virtual.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Establecer el nombre de disco de SO Hola. 

```powershell
$osDiskName = 'myOsDisk'
```

Crear disco administrado Hola.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Crear nueva máquina virtual de Hola 

Crear funciones de red y otro toobe de recursos de máquina virtual usa Hola nueva máquina virtual.

### <a name="create-hello-subnet-and-vnet"></a>Crear red virtual y subred de Hola

Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).

Crear una subred de Hola. Este ejemplo crea una subred denominada **mySubNet**, en el grupo de recursos de hello **myDestinationResourceGroup**, y conjuntos de Hola prefijo de dirección de subred demasiado**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Crear red virtual de Hola. Este ejemplo establece Hola toobe de nombre de red virtual **myVnetName**, Hola ubicación demasiado**oeste de Estados Unidos**, y Hola prefijo de dirección de red virtual de hello demasiado**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Crear grupo de seguridad de red de hello y una regla de RDP
toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que permite el acceso RDP en el puerto 3389. Dado que Hola VHD para hello nueva máquina virtual creada a partir de una máquina virtual especializada existente, puede usar una cuenta de máquina virtual de origen de Hola para RDP.

Este ejemplo establece Hola nombre NSG demasiado**myNsg** y nombre de regla Hola RDP demasiado**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Para obtener más información acerca de los puntos de conexión y las reglas NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Creación de una dirección IP pública y una NIC
tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.

Crear dirección IP pública de Hola. En este ejemplo, nombre de dirección IP pública de Hola se establece demasiado**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Crear NIC de Hola. En este ejemplo, nombre de la NIC de Hola se establece demasiado**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Establecer nombre de máquina virtual de Hola y el tamaño

Este ejemplo establece Hola nombre de máquina virtual demasiado*myVM* y Hola VM tamaño demasiado*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Agregar Hola NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Agregar disco Hola SO 

Agregar using de hello SO disco toohello configuración [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk). Este ejemplo establece el tamaño de hello del disco de Hola de demasiado*128 GB* y adjuntará Hola disco administrado como un *Windows* disco del sistema operativo.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Completar Hola VM 

Crear Hola VM con [AzureRMVM New](/powershell/module/azurerm.compute/new-azurermvm)Hola configuraciones que se acaba de crear.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Si este comando es correcto, verá un resultado similar al siguiente:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Compruebe que se creó la máquina virtual de Hola
Debería ver Hola recién creado máquina virtual en hello [portal de Azure](https://portal.azure.com), en **examinar** > **máquinas virtuales**, o mediante el uso de hello después de PowerShell comandos:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Pasos siguientes
toosign en tooyour nueva máquina virtual, examinar toohello VM en hello [portal](https://portal.azure.com), haga clic en **conectar**y el archivo de escritorio remoto RDP Hola abierto. Usar credenciales de cuenta de hello de su toosign de máquina virtual original en la nueva máquina virtual de tooyour. Para obtener más información, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md).

