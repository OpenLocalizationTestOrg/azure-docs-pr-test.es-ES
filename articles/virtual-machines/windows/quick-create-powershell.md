---
title: "aaaAzure inicio rápido: crear VM de Windows PowerShell | Documentos de Microsoft"
description: "Aprender rápidamente toocreate una máquina virtual de Windows con PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Creación de una máquina virtual Windows con PowerShell

módulo de PowerShell de Azure de Hello es toocreate usado y administrar recursos de Azure desde la línea de comandos de PowerShell de Hola o en scripts. Esta guía se detalla mediante toocreate de PowerShell y ejecute Windows Server 2016 con máquina virtual de Azure. Una vez completada la implementación, se conecte toohello servidor e instale IIS.  

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

Este inicio rápido requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en la suscripción de Azure con hello tooyour `Login-AzureRmAccount` comando y siga hello en pantalla instrucciones.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Creación de un grupo de recursos

Cree un grupo de recursos de Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Creación de los recursos de red principales

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Cree una red virtual, una subred, una dirección IP pública. 
Estos recursos son la máquina virtual de tooprovide usado red conectividad toohello y conéctelo toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Cree un grupo de seguridad de red y una regla de grupo de seguridad de red. 
grupo de seguridad de red de Hello protege la máquina virtual de hello mediante reglas entrantes y salientes. En este caso, se crea una regla de entrada para el puerto 3389, que permite las conexiones entrantes al Escritorio remoto. También queremos toocreate una regla de entrada para el puerto 80, lo que permite el tráfico web entrante.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Crear una tarjeta de red de máquina virtual de Hola. 
Crear una tarjeta de red con [AzureRmNetworkInterface New](/powershell/module/azurerm.network/new-azurermnetworkinterface) para la máquina virtual de Hola. tarjeta de red de Hello conecta subred de tooa de máquina virtual de hello, grupo de seguridad de red y dirección IP pública.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Create virtual machine

Cree una configuración de máquina virtual. Esta configuración incluye valores de hello que se usan al implementar la máquina virtual de hello como una configuración de imagen, el tamaño y la autenticación de la máquina virtual. Cuando se realiza este paso, se le solicitará las credenciales. los valores de Hello que especifique se configuran como nombre de usuario de hello y una contraseña para la máquina virtual de Hola.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Crear la máquina virtual Hola con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

Una vez finalizada la implementación de hello, cree una conexión a escritorio remota con la máquina virtual de Hola.

Hola de uso [AzureRmPublicIpAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress) dirección tooreturn Hola IP pública de la máquina virtual de Hola de comandos. Tome nota de esta dirección IP para que pueda conectarse tooit con la conectividad de web tootest de explorador en un paso posterior.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola. Reemplace la dirección IP de hello con hello *publicIPAddress* de la máquina virtual. Cuando se le solicite, escriba credenciales de hello usadas al crear la máquina virtual de Hola.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Instalación de IIS mediante PowerShell

Ahora que ha iniciado en toohello máquina virtual de Azure, puede usar una sola línea de PowerShell tooinstall IIS y permitir el tráfico de web de tooallow de regla de hello firewall local. Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando de hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Hola de vista Página de bienvenida de IIS

Con IIS instalado y el puerto 80 ahora abierta en la máquina virtual de hello Internet, puede usar un explorador web de la página de bienvenida de IIS de elección tooview Hola predeterminado. Estar seguro de hello toouse *publicIpAddress* documentó anteriormente página predeterminada de toovisit Hola. 

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no necesite, puede usar hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web. toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Windows.

> [!div class="nextstepaction"]
> [Tutoriales de máquinas virtuales Windows de Azure](./tutorial-manage-vm.md)
