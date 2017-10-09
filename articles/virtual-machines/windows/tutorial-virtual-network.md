---
title: "aaaAzure redes virtuales y máquinas virtuales de Windows | Documentos de Microsoft"
description: "Tutorial: Administración de máquinas virtuales Windows y redes virtuales de Azure con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Administración de máquinas virtuales Windows y redes virtuales de Azure con Azure PowerShell

Las máquinas virtuales de Azure utilizan las redes de Azure para la comunicación de red interna y externa. En este tutorial, creará varias máquinas virtuales (VM) en una red virtual y configurará la conectividad de red entre ellas. Aprenderá a:

> [!div class="checklist"]
> * Crear una red virtual
> * Crear subredes de redes virtuales
> * Controlar el tráfico de red con grupos de seguridad de red
> * Ver reglas de tráfico en acción

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Creación de una red virtual

Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es un aislamiento lógico de hello nube de Azure dedicada tooyour suscripción. Dentro de una red virtual, buscar subredes, las reglas para las conexiones desde toohello subredes de hello las máquinas virtuales y subredes de toothose de conectividad.

Para poder crear otros recursos de Azure, necesita toocreate un grupo de recursos con [AzureRmResourceGroup nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myRGNetwork* en hello *EastUS* ubicación:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Una subred es un recurso secundario de una red virtual que le ayudará a definir segmentos de espacios de direcciones dentro de un bloque CIDR mediante prefijos de direcciones IP. Pueden agregarse NIC toosubnets y tooVMs conectados, proporcionar conectividad para diversas cargas de trabajo.

Cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Crear una red virtual denominada *myVNet* con *myFrontendSubnet* con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Creación de una máquina virtual de "front-end"

Para la toocommunicate de una máquina virtual en una red virtual, se necesita una interfaz de red virtual (NIC). Hola *myFrontendVM* se obtiene acceso desde Hola internet, por lo que también necesita una dirección IP pública. 

Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Cree una NIC con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Establecer el nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello VM con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Crear máquinas virtuales de hello con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [AzureRmVMOperatingSystem conjunto](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), y [nueva AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Instalación del servidor web

Puede instalar IIS en *myFrontendVM* usando una sesión del Escritorio remoto. Necesitará tooget Hola pública dirección IP de hello tooaccess VM se.

Puede obtener la dirección IP pública de Hola de *myFrontendVM* con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIPAddress* creado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Tome nota de esta dirección IP para poder usarla en pasos futuros.

Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con *myFrontendVM*. Reemplace  *<publicIPAddress>*  con la dirección de Hola que haya grabado previamente. Cuando se le solicite, escriba credenciales de hello utilizadas cuando creó Hola máquina virtual.

```
mstsc /v:<publicIpAddress>
``` 

Ahora que ha iniciado sesión demasiado*myFrontendVM*, puede utilizar una sola línea de PowerShell tooinstall IIS y permitir el tráfico de web de tooallow de regla de hello firewall local. Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando de hello:

Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) extensión de script personalizado de hello toorun que instala el servidor Web IIS de hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Ahora puede usar Hola IP dirección toobrowse toohello VM toosee Hola IIS sitio público.

![Sitio predeterminado de IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Administración del tráfico interno

Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooa de tooresources conectado de tráfico de red red virtual. Los NSG pueden ser toosubnets asociado o NIC individuales adjunta tooVMs. Abrir o cerrar tooVMs de acceso a través de puertos se realiza utilizando las reglas NSG. Al crear *myFrontendVM*, el puerto de entrada 3389 se abrió automáticamente para la conectividad RDP.

La comunicación interna de las máquinas virtuales puede configurarse con un NSG. En esta sección, aprenderá cómo toocreate una subred adicional en Hola de red y asignar una tooallow de tooit NSG una conexión de *myFrontendVM* demasiado*myBackendVM* en el puerto 1433. subred de Hello, a continuación, se asigna toohello VM cuando se crea.

Puede limitar el tráfico interno demasiado*myBackendVM* de sólo *myFrontendVM* mediante la creación de un NSG de subred de back-end de Hola. Hello en el ejemplo siguiente se crea una regla NSG denominada *myBackendNSGRule* con [AzureRmNetworkSecurityRuleConfig New](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Agregue un nuevo grupo de seguridad de red denominado *myBackendNSG* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Adición de una subred de "back-end"

Agregar *myBackEndSubnet* demasiado*myVNet* con [AzureRmVirtualNetworkSubnetConfig agregar](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Creación de la máquina virtual de "back-end"

Hola Hola de manera más fácil toocreate que VM back-end es mediante una imagen de SQL Server. Este tutorial sólo crea Hola VM con el servidor de base de datos de hello, pero no proporciona información acerca del acceso a la base de datos de Hola.

Creación de *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Establecer el nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello VM con Get-Credential:

```powershell
$cred = Get-Credential
```

Creación de *myBackendVM*:

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

imagen de Hola que se utiliza tiene instalado SQL Server, pero no se utiliza en este tutorial. Es tooshow incluye también cómo puede configurar el tráfico de web toohandle de una máquina virtual y una administración de base de datos de toohandle de máquina virtual.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado y protege las redes de Azure como máquinas toovirtual relacionados. 

> [!div class="checklist"]
> * Crear una red virtual
> * Crear subredes de redes virtuales
> * Controlar el tráfico de red con grupos de seguridad de red
> * Ver reglas de tráfico en acción

Avanzar toohello toolearn de tutorial siguiente acerca de la supervisión para asegurar datos en máquinas virtuales mediante copia de seguridad de Azure. .

> [!div class="nextstepaction"]
> [Copia de seguridad de máquinas virtuales Windows en Azure](./tutorial-backup-vms.md)
