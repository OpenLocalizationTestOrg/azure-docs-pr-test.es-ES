---
title: aaaCustomize una VM de Windows en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola extensión de script personalizado y el almacén de claves toocustomize máquinas virtuales de Windows en Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>¿Cómo toocustomize una máquina virtual de Windows en Azure
Normalmente se desea tooconfigure máquinas virtuales (VMs) de una manera rápida y coherente, alguna forma de automatización. Un toocustomize enfoque común una VM de Windows es toouse [extensión para ventanas de Script personalizado](extensions-customscript.md). En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Usar la extensión de Script personalizado de hello tooinstall IIS
> * Crear una máquina virtual que usa Hola extensión de Script personalizado
> * Ver un sitio IIS en ejecución después de que se aplica la extensión de Hola

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="custom-script-extension-overview"></a>Información general de la extensión de script personalizado
Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure. Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración. Las secuencias de comandos pueden descargarse desde el almacenamiento de Azure o GitHub, o proporcionarse toohello portal de Azure en tiempo de ejecución de extensión.

Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.

Puede usar Hola extensión de Script personalizado con máquinas virtuales de Linux y Windows.


## <a name="create-virtual-machine"></a>Create virtual machine
Antes de poder crear una máquina virtual, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAutomate* en hello *EastUS* ubicación:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

Establecer un administrador username y password para máquinas virtuales de hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Ahora puede crear Hola VM con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm). Hello ejemplo siguiente crea componentes de red virtual Hola necesario, configuración de hello SO y, a continuación, crea una máquina virtual denominada *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
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
    -Name myNetworkSecurityGroupRuleWWW  `
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
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

Tarda unos minutos para los recursos de Hola y toobe de máquina virtual que creó.


## <a name="automate-iis-install"></a>Automatizar la instalación de IIS
Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hola extensión de Script personalizado. Hola se ejecuta la extensión `powershell Add-WindowsFeature Web-Server` tooinstall Hola actualizaciones hello servidor Web IIS y, a continuación, *Default.htm* página tooshow Hola hostname de hello VM:

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a>Sitio web de prueba
Obtener dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa. se muestra el sitio Web de Hello, incluyendo hostname Hola de hello VM ese equilibrador de carga de hello distribuye tooas de tráfico en el siguiente ejemplo de Hola:

![Ejecución del sitio web de IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se automatizó Hola IIS se instala en una máquina virtual. Ha aprendido a:

> [!div class="checklist"]
> * Usar la extensión de Script personalizado de hello tooinstall IIS
> * Crear una máquina virtual que usa Hola extensión de Script personalizado
> * Ver un sitio IIS en ejecución después de que se aplica la extensión de Hola

Avanzar toohello siguiente tutorial toolearn cómo toocreate imágenes de máquina virtual personalizadas.

> [!div class="nextstepaction"]
> [Creación de imágenes personalizadas de máquinas virtuales](./tutorial-custom-images.md)
