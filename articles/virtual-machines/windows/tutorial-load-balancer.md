---
title: "aaaHow tooload equilibrar máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure carga equilibrador toocreate una aplicación segura y de alta disponibilidad a través de tres máquinas virtuales de Windows"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>¿Cómo tooload equilibrar máquinas virtuales de Windows en Azure toocreate una aplicación de alta disponibilidad
El equilibrio de carga proporciona un mayor nivel de disponibilidad al distribuir las solicitudes entrantes entre varias máquinas virtuales. En este tutorial, aprenderá acerca de los componentes diferentes Hola Hola Azure del equilibrador de carga que distribución el tráfico y proporcionan una alta disponibilidad. Aprenderá a:

> [!div class="checklist"]
> * Creación de un equilibrador de carga de Azure
> * Creación del sondeo de estado de un equilibrador de carga
> * Crear reglas de tráfico del equilibrador de carga
> * Usar la extensión de Script personalizado de hello toocreate un sitio IIS básico
> * Crear máquinas virtuales y adjuntar tooa equilibrador de carga
> * Ver un equilibrador de carga en acción
> * Agregar y quitar las máquinas virtuales de un equilibrador de carga

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Información general sobre Azure Load Balancer
Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto. Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.

Se define una configuración de IP de front-end que contiene una o varias direcciones IP públicas. Esta configuración de IP de front-end permite que su toobe de aplicaciones y el equilibrador de carga puede tener acceso a través de Internet de Hola. 

Máquinas virtuales se conectarán tooa equilibrador de carga con la tarjeta de interfaz de red virtual (NIC). toodistribute tráfico toohello máquinas virtuales, un grupo de direcciones de back-end contiene direcciones IP de Hola Hola virtual (NIC) toohello conectados del equilibrador de carga.

flujo de hello toocontrol de tráfico, defina reglas de equilibrador de carga para determinados puertos y protocolos que se asignan tooyour las máquinas virtuales.


## <a name="create-azure-load-balancer"></a>Creación del equilibrador de carga de Azure
Esta sección detalla cómo puede crear y configurar cada componente Hola de equilibrador de carga. Antes de poder crear el equilibrador de carga, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupLoadBalancer* en hello *EastUS* ubicación:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Crear una dirección IP pública
tooaccess Hola de la aplicación en Internet, necesita una dirección IP pública para el equilibrador de carga de Hola. Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hello en el ejemplo siguiente se crea una dirección IP pública denominada *myPublicIP* en hello *myResourceGroupLoadBalancer* grupo de recursos:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Crear un equilibrador de carga
Cree una dirección IP de front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hello en el ejemplo siguiente se crea una dirección IP de front-end denominada *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Cree un grupo de direcciones de back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hello en el ejemplo siguiente se crea un grupo de direcciones de back-end denominado *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

A continuación, cree el equilibrador de carga de hello con [AzureRmLoadBalancer nuevo](/powershell/module/azurerm.network/new-azurermloadbalancer). Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre *myLoadBalancer* con hello *myPublicIP* dirección:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Creación de un sondeo de estado
tooallow Hola equilibrador toomonitor Hola estado de carga de la aplicación, utilice un sondeo de estado. sondeo de estado de Hello dinámicamente agrega o quita las máquinas virtuales de rotación del equilibrador de carga de hello en función de sus comprobaciones de toohealth de respuesta. De forma predeterminada, una máquina virtual se quita de la distribución de equilibrador de carga de hello después de dos errores consecutivos en intervalos de 15 segundos. Cree un sondeo de estado en función de un protocolo o una página de comprobación de mantenimiento específica para la aplicación. 

Hola siguiente ejemplo crea un sondeo TCP. También se pueden crear sondeos HTTP personalizados para comprobaciones de estado más específicas. Al utilizar un sondeo HTTP personalizado, debe crear página de comprobación de mantenimiento de hello, como *healthcheck.aspx*. sondeo de Hello debe devolver un **HTTP 200 OK** respuesta para host Hola carga equilibrador tookeep Hola de rotación.

toocreate un sondeo de estado TCP, use [AzureRmLoadBalancerProbeConfig agregar](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hello en el ejemplo siguiente se crea un sondeo de estado denominado *myHealthProbe* que supervisa cada máquina virtual:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Actualizar el equilibrador de carga de hello con [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Creación de una regla de equilibrador de carga
Una regla de equilibrador de carga es toodefine usado cómo tráfico es distribuida toohello máquinas virtuales. Definir configuración de IP front-end de hello para el tráfico entrante de Hola y Hola back-end grupo tooreceive Hola tráfico IP, junto con el origen de hello necesarios y el puerto de destino. toomake seguro que solo las máquinas virtuales correcto reciban tráfico, también definir toouse de sondeo de estado de Hola.

Cree una regla del equilibrador de carga con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hello en el ejemplo siguiente se crea una regla de equilibrador de carga denominada *myLoadBalancerRule* y equilibra el tráfico en el puerto *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Actualizar el equilibrador de carga de hello con [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Configuración de una red virtual
Antes de implementar algunas máquinas virtuales y puede probar su equilibrador, crear Hola compatibilidad con recursos de red virtual. Para obtener más información sobre las redes virtuales, vea hello [administrar redes virtuales de Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Crear recursos de red
Cree una red virtual con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Cree una regla de grupo de seguridad de red con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) y después cree un grupo de seguridad de red con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Agregar subred toohello grupo de seguridad de red de hello con [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) y, a continuación, actualizar la red virtual de hello con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Hello en el ejemplo siguiente se crea una regla de grupo de seguridad de red denominada *myNetworkSecurityGroup* y lo aplica demasiado*mySubnet*:

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Las NIC virtuales se crean con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello en el ejemplo siguiente se crea tres NIC virtuales. (Una NIC virtual para cada máquina virtual crea para la aplicación Hola siguiendo los pasos). Puede crear NIC virtuales adicionales y las máquinas virtuales en cualquier momento y agregarlos toohello equilibrador de carga:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Creación de máquinas virtuales
alta disponibilidad de Hola de tooimprove de la aplicación, coloque las máquinas virtuales en un conjunto de disponibilidad.

Cree un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Establecer un administrador username y password para máquinas virtuales de hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Ahora puede crear máquinas virtuales de hello con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm). Hola siguiente ejemplo crea tres máquinas virtuales:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Toma toocreate unos minutos y configurar todas las tres máquinas virtuales.

### <a name="install-iis-with-custom-script-extension"></a>Instalar IIS con la extensión de script personalizado
En un tutorial anterior en [cómo toocustomize una máquina virtual Windows](tutorial-automate-vm-deployment.md), ha aprendido cómo tooautomate personalización de máquina virtual con Hola extensión para ventanas de Script personalizado. Puede usar hello mismo enfoque tooinstall y configure IIS en las máquinas virtuales.

Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hola extensión de Script personalizado. Hola se ejecuta la extensión `powershell Add-WindowsFeature Web-Server` tooinstall Hola actualizaciones hello servidor Web IIS y, a continuación, *Default.htm* página tooshow Hola hostname de hello VM:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Prueba del equilibrador de carga
Obtener dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa. se muestra el sitio Web de Hello, incluyendo hostname Hola de hello VM ese equilibrador de carga de hello distribuye tooas de tráfico en el siguiente ejemplo de Hola:

![Ejecución del sitio web de IIS](./media/tutorial-load-balancer/running-iis-website.png)

equilibrador de carga de hello toosee distribuir el tráfico entre todas las tres VM que se ejecuta la aplicación, se puede forzar actualización el explorador web.


## <a name="add-and-remove-vms"></a>Agregar y quitar máquinas virtuales
Puede que necesite tooperform mantenimiento en hello máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo. toodeal con un aumento del tráfico tooyour aplicación, puede que necesite tooadd máquinas virtuales adicionales. Esta sección muestra cómo tooremove o agregar una máquina virtual desde el equilibrador de carga de Hola.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Quitar una máquina virtual de equilibrador de carga de Hola
Obtener la tarjeta de interfaz de red de hello con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), a continuación, el conjunto de hello *LoadBalancerBackendAddressPools* propiedad de Hola NIC virtual demasiado*$null*. Por último, actualice NIC virtual. Hola:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

equilibrador de carga de hello toosee distribuir el tráfico entre Hola otras dos máquinas virtuales que ejecutan la aplicación puede forzar actualización el explorador web. Ahora puede realizar el mantenimiento en Hola de máquina virtual, como instalar actualizaciones del sistema operativo o realizar un reinicio de máquina virtual.

### <a name="add-a-vm-toohello-load-balancer"></a>Agregar un equilibrador de carga de toohello VM
Después de realizar el mantenimiento de la máquina virtual, o si necesita capacidad de tooexpand, establezca hello *LoadBalancerBackendAddressPools* propiedad de hello virtual NIC toohello *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Obtener el equilibrador de carga de hello:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado un equilibrador de carga y adjunta tooit de máquinas virtuales. Ha aprendido a:

> [!div class="checklist"]
> * Creación de un equilibrador de carga de Azure
> * Creación del sondeo de estado de un equilibrador de carga
> * Crear reglas de tráfico del equilibrador de carga
> * Usar la extensión de Script personalizado de hello toocreate un sitio IIS básico
> * Crear máquinas virtuales y adjuntar tooa equilibrador de carga
> * Ver un equilibrador de carga en acción
> * Agregar y quitar las máquinas virtuales de un equilibrador de carga

Avanzar toohello siguiente tutorial toolearn cómo toomanage redes de máquina virtual.

> [!div class="nextstepaction"]
> [Administración de máquinas y redes virtuales](./tutorial-virtual-network.md)
