---
title: "aaaCreate VM desde una imagen de máquina virtual administrada de Azure | Documentos de Microsoft"
description: "Crear una máquina virtual de Windows desde una imagen de máquina virtual administrada generalizada con PowerShell de Azure, en el modelo de implementación del Administrador de recursos de Hola."
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Creación de una máquina virtual a partir de una imagen administrada

Puede crear varias VM a partir de una imagen de VM administrada en Azure. Una imagen de máquina virtual administrada contiene Hola información necesarios toocreate una máquina virtual, incluidos los discos de sistema operativo y datos de Hola. Hola discos duros virtuales que constituyen la imagen de hello, incluidos los discos de hello OS y los discos de datos, se almacenan como discos administrados. 


## <a name="prerequisites"></a>Requisitos previos

Necesita toohave ya [crea una imagen de máquina virtual administrada](capture-image-resource.md) Hola a toouse para crear nueva máquina virtual. 

Asegúrese de que tiene las últimas versiones de Hola de hello AzureRM.Compute y AzureRM.Network módulos de PowerShell. Abra un símbolo del sistema de PowerShell como administrador y ejecute hello después tooinstall comando ellos.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).



## <a name="collect-information-about-hello-image"></a>Recopilar información acerca de la imagen de Hola

En primer lugar se necesita toogather información básica acerca de la imagen de Hola y cree una variable para la imagen de Hola. Este ejemplo utiliza una imagen de máquina virtual administrada con el nombre **myImage** decir Hola en **myResourceGroup** grupo de recursos de hello **oeste Ee.uu. Central** ubicación. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Crear una red virtual
Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).

1. Crear una subred de Hola. Este ejemplo crea una subred denominada **mySubnet** con prefijo de dirección de hello **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crear red virtual de Hola. Este ejemplo crea una red virtual denominada **myVnet** con prefijo de dirección de hello **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Creación de una dirección IP y una interfaz de red

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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Crear grupo de seguridad de red de hello y una regla de RDP

toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad de red (NSG) que permite el acceso RDP en el puerto 3389. 

Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389. Para obtener más información acerca de los NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Cree una variable para la red virtual de Hola

Cree una variable para la red virtual de hello completado. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obtener las credenciales de Hola Hola VM

Hello siguiente cmdlet abrirá una ventana donde se incluirá un nuevo toouse de nombre y la contraseña de usuario como cuenta de administrador local de Hola de tengan acceso remoto a Hola VM. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Las variables establecidas para hello VM name, nombre de equipo y Hola tamaño de hello VM

1. Cree variables para el nombre de la máquina virtual de Hola y el nombre de equipo. Este ejemplo establece el nombre de la máquina virtual de hello como **myVM** y el nombre de equipo de hello como **MiPC**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Establecer tamaño de Hola de máquina virtual de Hola. Este ejemplo crea la VM con el tamaño **Standard_DS1_v2**. Vea hello [tamaños de máquina virtual](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentación para obtener más información.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Agregar nombre de máquina virtual de Hola y de configuración de máquina virtual de tamaño toohello.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Imagen de máquina virtual de hello conjunto como imagen de origen para hello nueva máquina virtual

Establecer la imagen de origen de hello con el Id. de Hola de imagen de VM de hello administrado.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Establecer la configuración del sistema operativo hello y agregue NIC de Hola.

Escriba el tipo de almacenamiento de hello (PremiumLRS o StandardLRS) y el tamaño de Hola de disco del sistema operativo Hola. Este ejemplo establece el tipo de cuenta de hello demasiado**PremiumLRS**, Hola demasiado de tamaño de disco**128 GB** y disco, almacenamiento en caché demasiado**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Crear hello VM

Crear nueva máquina virtual con configuración de Hola que hemos creado y almacenado en Hola de Hola **$vm** variable.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Compruebe que se creó la máquina virtual de Hola
Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Pasos siguientes
toomanage la nueva máquina virtual con PowerShell de Azure, consulte [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

