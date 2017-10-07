---
title: aaaCreate una imagen no administrada de una VM generalizada en Azure | Documentos de Microsoft
description: "Crear una imagen no administrado de un generalizado toocreate toouse de máquina virtual de Windows varias copias de una máquina virtual en Azure."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Cómo toocreate una máquina virtual no administrada de la imagen de una VM de Azure

En este artículo se explica cómo usar cuentas de almacenamiento. Se recomienda utilizar Managed Disks e imágenes administradas en lugar de una cuenta de almacenamiento. Para más información, vea [Captura de una imagen administrada de una máquina virtual generalizada en Azure](capture-image-resource.md).

Este artículo muestra cómo toouse Azure PowerShell toocreate una imagen de una VM generalizada de Azure con una cuenta de almacenamiento. A continuación, puede usar Hola imagen toocreate otra máquina virtual. imagen de Hello incluye el disco del sistema operativo de Hola y discos de datos de Hola que son la máquina virtual de toohello adjunto. imagen de Hello no incluye recursos de red virtual de hello, por lo que necesita tooset los recursos cuando creas Hola nueva máquina virtual. 

## <a name="prerequisites"></a>Requisitos previos
Necesita toohave PowerShell de Azure versión 1.0. x o posterior instalado. Si aún no ha instalado PowerShell, lea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para los pasos de instalación.

## <a name="generalize-hello-vm"></a>Generalizar Hola VM 
Esta sección muestra cómo toogeneralize la máquina virtual de Windows para su uso como una imagen. Generalizar una máquina virtual quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen. Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).

Asegúrese de que los roles de servidor hello ejecutando en el equipo de hello son compatibles con Sysprep. Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si va a cargar el tooAzure de disco duro virtual para hello primera vez, asegúrese de que tiene [preparado la máquina virtual](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de ejecutar Sysprep. 
> 
> 

También puede generalizar una VM de Linux con `sudo waagent -deprovision+user` y, a continuación, use PowerShell toocapture Hola máquina virtual. Para obtener información acerca del uso de hello CLI toocapture una máquina virtual, consulte [cómo toogeneralize y la captura de una máquina virtual de Linux con hello Azure CLI ](../linux/capture-image.md).


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

## <a name="log-in-tooazure-powershell"></a>Inicie sesión en tooAzure PowerShell
1. Abra PowerShell de Azure e inicie sesión tooyour cuenta de Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Abre una ventana emergente para tooenter sus credenciales de cuenta de Azure.
2. Obtener identificadores de suscripción de Hola para las suscripciones disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Conjunto Hola suscripción correcta con el identificador de suscripción de Hola.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Cancela la asignación de hello VM y establezca Hola estado toogeneralized
1. Cancela la asignación de recursos de la máquina virtual de Hola.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Hola *estado* para hello VM en hello Azure portal cambia de **detenido** demasiado**detenido (desasignado)**.
2. Establecer el estado de saludo de la máquina virtual de hello demasiado**generalizado**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Comprobar estado de Hola de hello máquina virtual. Hola **OSState/generalizar** sección para hello VM debe tener hello **DisplayStatus** establecido demasiado**VM generalizado**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Crear imagen de Hola

Crear una imagen de máquina virtual no administrado en el contenedor de almacenamiento de destino de hello con este comando. Hello imagen se crea en Hola misma cuenta de almacenamiento como Hola máquina virtual original. Hola `-Path` parámetro guarda una copia de la plantilla JSON de Hola Hola equipo de origen VM tooyour local. Hola `-DestinationContainerName` parámetro es Hola nombre del contenedor de Hola que desea toohold las imágenes. Si no existe el contenedor de hello, se crea automáticamente.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Puede obtener dirección URL de hello de la imagen de plantilla de archivos de hello JSON. Vaya toohello **recursos** > **storageProfile** > **osDisk** > **imagen**  >  **uri** sección de ruta de acceso completa de saludo de la imagen. dirección URL de Hola de imagen de hello es similar: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
También puede comprobar Hola URI en el portal de Hola. imagen de Hello es contenedor tooa copiada denominado **system** en su cuenta de almacenamiento. 

## <a name="create-a-vm-from-hello-image"></a>Crear una máquina virtual a partir de la imagen de Hola

Ahora puede crear una o más máquinas virtuales de imagen de hello no administrado.

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
Hello PowerShell siguiente completa de configuraciones de máquina virtual de Hola y usa imagen no administrado como origen de Hola para instalación nueva de Hola.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>Compruebe que se creó la máquina virtual de Hola
Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Pasos siguientes
toomanage la nueva máquina virtual con PowerShell de Azure, consulte [administrar máquinas virtuales con el Administrador de recursos de Azure y PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


