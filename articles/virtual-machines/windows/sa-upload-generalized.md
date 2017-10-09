---
title: "aaaUpload un toocreate de disco duro virtual de generalizar varias máquinas virtuales en Azure | Documentos de Microsoft"
description: "Cargar un toocreate de cuenta de almacenamiento de Azure de tooan de disco duro virtual generalizado un toouse de máquina virtual de Windows con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Cargar un toocreate tooAzure de disco duro virtual generalizado una nueva máquina virtual

Este tema tratan cargando una cuenta de almacenamiento de disco no administrado generalizado tooa y, a continuación, crear una nueva máquina virtual con el disco de hello cargado. Con Sysprep se elimina toda la información personal de la cuenta de una imagen de un VHD generalizado. 

Si desea toocreate una máquina virtual desde un disco duro virtual especializada en una cuenta de almacenamiento, consulte [crear una máquina virtual desde un disco duro virtual especializado](sa-create-vm-specialized.md).

Este tema incluye el uso de las cuentas de almacenamiento, pero se recomienda a los clientes mover discos administrados de toousing en su lugar. Para ver un tutorial completo de cómo tooprepare, cargar y crear una nueva máquina virtual mediante discos administrados, vea [crear una nueva máquina virtual desde un tooAzure de disco duro virtual cargado generalizado con discos administrados](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Preparar Hola VM

La información personal de la cuenta se elimina de un VHD generalizado mediante Sysprep. Si piensa toouse Hola VHD como una imagen toocreate nuevas máquinas virtuales desde, debe:
  
  * [Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md). 
  * Generalice la máquina virtual de hello mediante Sysprep

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Generalización de una máquina virtual Windows con Sysprep
Esta sección muestra cómo toogeneralize la máquina virtual de Windows para su uso como una imagen. Sysprep quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen. Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).

Asegúrese de que los roles de servidor hello ejecutando en el equipo de hello son compatibles con Sysprep. Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si está ejecutando Sysprep antes de cargar su tooAzure de disco duro virtual para hello primera vez, asegúrese de que tiene [preparado la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep. 
> 
> 

1. Inicie sesión en toohello máquina virtual de Windows.
2. Abra la ventana de símbolo del sistema de hello como administrador. Cambie el directorio de hello demasiado**%windir%\system32\sysprep**y, a continuación, ejecute `sysprep.exe`.
3. Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que ese hello **generalizar** casilla está activada.
4. En **Opciones de apagado**, seleccione **Apagar**.
5. Haga clic en **Aceptar**.
   
    ![Iniciar Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Cuando Sysprep finalice, se apaga máquina virtual de Hola. 

> [!IMPORTANT]
> No se reinician Hola VM hasta que esté listo cargando tooAzure de disco duro virtual de Hola o crear una imagen de VM de Hola. Si obtiene reinicia Hola VM accidentalmente, ejecute Sysprep toogeneralize vuelva a.
> 
> 


## <a name="upload-hello-vhd"></a>Cargar Hola VHD

Cargar la cuenta de almacenamiento de Azure de hello VHD tooan.

### <a name="log-in-tooazure"></a>Inicie sesión en tooAzure
Si aún no tiene PowerShell versión 1.4 o posterior instalado, leer [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

1. Abra PowerShell de Azure e inicie sesión tooyour cuenta de Azure. Abre una ventana emergente para tooenter sus credenciales de cuenta de Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Obtener identificadores de suscripción de Hola para las suscripciones disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Conjunto Hola suscripción correcta con el identificador de suscripción de Hola. Reemplace `<subscriptionID>` con el Id. de Hola de hello corregir la suscripción.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Obtener la cuenta de almacenamiento de Hola
Necesita una cuenta de almacenamiento en la imagen de máquina virtual de Azure toostore Hola cargado. Puede usar una cuenta de almacenamiento existente o crear una nueva. 

cuentas de almacenamiento disponibles de hello tooshow, escriba:

```powershell
Get-AzureRmStorageAccount
```

Si desea que toouse una cuenta de almacenamiento existente, continúe toohello [imagen de máquina virtual de carga hello](#upload-the-vm-vhd-to-your-storage-account) sección.

Si necesita toocreate una cuenta de almacenamiento, siga estos pasos:

1. Se necesita el nombre de Hola Hola del grupo de recursos donde se debe crear la cuenta de almacenamiento de Hola. toofind todos los grupos de recursos de Hola que se encuentran en su suscripción, tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate un grupo de recursos denominado **myResourceGroup** Hola **West US** región, escriba:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Crear una cuenta de almacenamiento denominada **mystorageaccount** en este grupo de recursos mediante el uso de hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Iniciar Hola carga 

Hola de uso [AzureRmVhd agregar](/powershell/module/azurerm.compute/add-azurermvhd) contenedor cmdlet tooupload Hola imagen tooa en su cuenta de almacenamiento. En este ejemplo Hola a cargas de archivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa cuenta de almacenamiento denominada **mystorageaccount** en hello **myResourceGroup** grupo de recursos. archivo Hello se colocarán en el contenedor de hello denominado **mycontainer** y nombre de archivo nuevo de hello será **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

Dependiendo de la conexión de red y el tamaño de hello del archivo VHD, este comando puede tardar un rato toocomplete.


## <a name="create-a-new-vm"></a>Creación de una máquina virtual nueva 

Ahora puede usar Hola carga VHD toocreate una nueva máquina virtual. 

### <a name="set-hello-uri-of-hello-vhd"></a>Hola de conjunto de URI de hello VHD

Hola URI para hello toouse de disco duro virtual está en formato de hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd. En este ejemplo Hola VHD denominada **myVHD** está en la cuenta de almacenamiento de hello **mystorageaccount** en el contenedor de hello **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Crear una red virtual
Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).

1. Crear una subred de Hola. Hello en el ejemplo siguiente crea una subred denominada **mySubnet** en grupo de recursos de hello **myResourceGroup** con prefijo de dirección de hello **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crear red virtual de Hola. Hello en el ejemplo siguiente crea una red virtual con el nombre **myVnet** Hola **West US** ubicación con el prefijo de dirección de hello **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Creación de una dirección IP y una interfaz de red
tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.

1. Cree una dirección IP pública. Este ejemplo crea una dirección IP pública denominada "**myPip**". 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Crear NIC de Hola. Este ejemplo crea una NIC denominada "**myNic**". 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Crear grupo de seguridad de red de hello y una regla de RDP
toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad que permite el acceso RDP en el puerto 3389. 

Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389. Para obtener más información acerca de los NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Cree una variable para la red virtual de Hola
Cree una variable para la red virtual de hello completado. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Crear hello VM
Hello siguiente script de PowerShell muestra cómo tooset configuraciones de máquina virtual de Hola y Hola uso carga imagen de máquina virtual como origen de Hola para instalación nueva de Hola.



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>Compruebe que se creó la máquina virtual de Hola
Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Pasos siguientes
toomanage la nueva máquina virtual con PowerShell de Azure, consulte [administrar máquinas virtuales con el Administrador de recursos de Azure y PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


