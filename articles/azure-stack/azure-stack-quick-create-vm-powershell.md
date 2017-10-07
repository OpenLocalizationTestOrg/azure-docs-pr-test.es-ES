---
title: "aaaCreate una máquina virtual de Windows mediante el uso de PowerShell en la pila de Azure | Documentos de Microsoft"
description: "Cree una máquina virtual Windows con PowerShell en Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>Creación de una máquina virtual Windows con PowerShell en Azure Stack

Máquinas virtuales en asigne de pila de Azure Hola flexibilidad de virtualización sin necesidad de toobuy y mantener Hola hardware físico que lo ejecuta. Cuando se usa máquinas virtuales, saber que hay algunas diferencias entre las características de Hola que están disponibles en Azure y pila de Azure, consulte toohello [consideraciones para las máquinas virtuales en Azure pila](azure-stack-vm-considerations.md) toolearn tema sobre Estas diferencias. 

Esta guía de detalles mediante PowerShell toocreate una máquina virtual de Windows Server 2016 en pila de Azure. Puede ejecutar pasos de hello descritos en este artículo desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo basado en Windows, si está conectado a través de VPN. 

## <a name="prerequisites"></a>Requisitos previos

1. marketplace de pila de Azure de Hello no contiene imágenes de Windows Server 2016 Hola de forma predeterminada. Por lo tanto, para poder crear una máquina virtual, asegúrese de que el operador de pila de Azure hello [agrega marketplace de pila de Azure de hello Windows Server 2016 imagen toohello](azure-stack-add-default-image.md). 
2. Pila de Azure requiere una versión específica de toocreate de módulo de PowerShell de Azure y administre recursos de Hola. Siga los pasos de hello descritos en [instale PowerShell para Azure pila](azure-stack-powershell-install.md) versión requerida de tema tooinstall Hola.
3. [Configurar el entorno de PowerShell del usuario de hello pila de Azure](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure Stack. Usar hello siguiente bloque de código toocreate un grupo de recursos. Hemos asignado los valores para todas las variables en este documento, puede usarlas tal cual o asignar un valor diferente.  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>Creación de recursos de almacenamiento 

Crear una cuenta de almacenamiento y una imagen de Windows Server 2016 hello toostore del contenedor de almacenamiento.

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>Creación de los recursos de red principales

Cree una red virtual, una subred, una dirección IP pública. Estos recursos son utilizados tooprovide red conectividad toohello virtual machine.  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Creación de un grupo de seguridad de red y una regla de grupo de seguridad de red

grupo de seguridad de red de Hola protege máquinas virtuales de hello mediante reglas entrantes y salientes. Permite crear una regla de entrada para el puerto 3389 tooallow entrantes conexiones de escritorio remoto y una regla de entrada para el tráfico web tooallow entrante el puerto 80.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a>Crear una tarjeta de red de máquina virtual de Hola

tarjeta de red de Hello conecta subred de tooa de máquina virtual de hello, grupo de seguridad de red y dirección IP pública.

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a>de una máquina virtual

Cree una configuración de máquina virtual. Hola incluye configuración de Hola que se usa al implementar la máquina virtual de hello como una imagen de máquina virtual, el tamaño, las credenciales.

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a>Conectar máquina virtual de toohello

Después de que se crea correctamente la máquina virtual de hello, abra una máquina virtual de escritorio remoto conexión toohello desde el kit de desarrollo de hello, o desde un cliente externo basado en Windows si está conectado a través de VPN. tooremote en la máquina virtual de Hola que creó en el paso anterior de hello, necesita su dirección IP pública. Ejecute hello después comando tooget Hola dirección IP pública de la máquina virtual de hello: 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola. Reemplace la dirección IP de Hola por hello publicIPAddress de la máquina virtual. Cuando se le solicite, escriba Hola nombre de usuario y contraseña que utilizó al crear la máquina virtual de Hola.

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a>Eliminar la máquina virtual de Hola

Cuando ya no necesite usar hello después el grupo de recursos de Hola de tooremove de comando que contiene la máquina virtual de Hola y sus recursos relacionados:

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>Pasos siguientes

toolearn acerca del almacenamiento en la pila de Azure, consulte toohello [Introducción al almacenamiento](azure-stack-storage-overview.md) tema.

