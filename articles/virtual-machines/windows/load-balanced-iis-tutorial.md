---
title: "aaaTutorial - compilación una aplicación de alta disponibilidad en máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una aplicación segura y de alta disponibilidad a través de tres máquinas virtuales de Windows con un equilibrador de carga en Azure"
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Compilación de una aplicación de alta disponibilidad y carga equilibrada en máquinas virtuales Windows en Azure

En este tutorial, creará una aplicación de alta disponibilidad que sea resistente toomaintenance eventos. aplicación Hello usa un equilibrador de carga, un conjunto de disponibilidad y tres máquinas virtuales de Windows (VM). Este tutorial instala IIS, aunque puede utilizar este tutorial toodeploy un marco de aplicación diferente usando Hola directrices y los mismos componentes de alta disponibilidad. 

## <a name="step-1---azure-prerequisites"></a>Paso 1: Requisitos previos de Azure

toocomplete este tutorial, asegúrese de que ha instalado hello más reciente [Azure PowerShell](/powershell/azure/overview) módulo.

En primer lugar, inicie sesión en tooyour suscripción de Azure con el comando de inicio de sesión AzureRmAccount hello y siga hello en pantalla instrucciones.

```powershell
Login-AzureRmAccount
```

Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. Para poder crear otros recursos de Azure, necesita toocreate un grupo de recursos con [AzureRmResourceGroup nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` región: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Paso 2: Creación de un conjunto de disponibilidad

Las máquinas virtuales se pueden crear en dominios de error lógico y actualización. Cada dominio lógico representa una parte del hardware en el centro de datos Azure Hola subyacente. Cuando crea dos o más máquinas virtuales, los recursos de proceso y almacenamiento se distribuyen en estos dominios. Esta distribución mantiene la disponibilidad de saludo de la aplicación si un componente de hardware necesita mantenimiento. Los conjuntos de disponibilidad le permiten definir estos dominios de error lógico y actualización.

Cree un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Paso 3: Creación de un equilibrador de carga

Un equilibrador de carga de Azure distribuye el tráfico a través de un conjunto de máquinas virtuales definidas usando reglas de equilibrador de carga. Un sondeo de estado supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.

### <a name="create-public-ip-address"></a>Creación de una dirección IP pública

tooaccess la aplicación en hello Internet, asignar un equilibrador de carga de toohello de dirección IP público. Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hello en el ejemplo siguiente se crea una dirección IP pública denominada `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Creación de un equilibrador de carga

Cree una dirección IP de front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hello en el ejemplo siguiente se crea una dirección IP de front-end denominada `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Cree un grupo de direcciones de back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hello en el ejemplo siguiente se crea un grupo de direcciones de back-end denominado `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

A continuación, cree el equilibrador de carga de hello con [AzureRmLoadBalancer nuevo](/powershell/module/azurerm.network/new-azurermloadbalancer). Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre `myLoadBalancer` con hello `myPublicIP` dirección:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Creación de un sondeo de estado

tooallow Hola equilibrador toomonitor Hola estado de carga de la aplicación, utilice un sondeo de estado. sondeo de estado de Hello dinámicamente agrega o quita las máquinas virtuales de rotación del equilibrador de carga de hello en función de sus comprobaciones de toohealth de respuesta. De forma predeterminada, una máquina virtual se quita de la distribución de equilibrador de carga de hello después de dos errores consecutivos en intervalos de 15 segundos.

Cree un sondeo de estado con [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hello en el ejemplo siguiente se crea un sondeo de estado denominado `myHealthProbe` que supervisa cada máquina virtual:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Creación de reglas del equilibrador de carga

Una regla de equilibrador de carga es toodefine usado cómo tráfico es distribuida toohello máquinas virtuales.

Cree una regla del equilibrador de carga con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hello en el ejemplo siguiente se crea una regla de equilibrador de carga denominada `myLoadBalancerRule` y equilibra el tráfico en el puerto `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Actualizar el equilibrador de carga de hello con [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Paso 4: Configuración de las redes

Cada máquina virtual tiene uno o más virtual tarjetas de red (NIC) que se conectan tooa de red virtual. Esta red virtual se protege el tráfico toofilter basándose en reglas de acceso definidas.

### <a name="create-virtual-network"></a>Creación de una red virtual

Primero, cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hello en el ejemplo siguiente se crea una subred denominada `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooyour de conectividad de red de tooprovide las máquinas virtuales, cree una red virtual con [AzureRmVirtualNetwork nuevo](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet` con `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Configuración de la seguridad de red

Un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) de Azure controla el tráfico entrante y saliente para una o varias máquinas virtuales. Las reglas del grupo de seguridad de red permiten o deniegan el tráfico de red en un puerto específico o en un intervalo de puertos. Estas reglas también pueden incluir un prefijo de dirección de origen para que solo el tráfico que se origine en un origen predefinido pueda comunicarse con una máquina virtual.

tooallow web tooreach de tráfico de la aplicación, cree una regla de grupo de seguridad de red con [AzureRmNetworkSecurityRuleConfig nuevo](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Hello en el ejemplo siguiente se crea una regla de grupo de seguridad de red denominada `myNetworkSecurityGroupRule`:

```powershell
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
```

Cree un grupo de seguridad de red con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Hello en el ejemplo siguiente se crea un NSG denominado `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Agregar subred toohello grupo de seguridad de red de hello con [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Red virtual de Hola de actualización con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Creación de las tarjetas de interfaz de red virtual

Cargar la función equilibradores con recursos NIC virtual hello en lugar de Hola VM real. Hello NIC virtual está conectado toohello equilibrador de carga y, a continuación, asociará tooa máquina virtual.

Cree una NIC virtual con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello en el ejemplo siguiente se crea tres NIC virtuales. (Una NIC virtual para cada máquina virtual debe crear para la aplicación Hola siguiendo los pasos):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Paso 5: Creación de máquinas virtuales

Con todos los hello subyacente componentes en su lugar, ahora puede crear toorun de máquinas virtuales de alta disponibilidad la aplicación. 

Obtener nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello la máquina virtual con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Crear máquinas virtuales de hello con [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem conjunto](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [conjunto AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface agregar](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), y [nueva AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hola siguiente ejemplo crea tres máquinas virtuales:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Toma varios toocreate minutos y configurar todas las tres máquinas virtuales. Hello sondeo de estado del equilibrador de carga detecta automáticamente cuando se ejecuta la aplicación hello en cada máquina virtual. Una vez que se ejecuta la aplicación hello, regla de equilibrador de carga de hello inicia toodistribute tráfico.

### <a name="install-hello-app"></a>Instalar la aplicación hello 

Las extensiones de máquina virtual de Azure son tareas de configuración de máquina virtual de tooautomate usado como instalar aplicaciones y configurar el sistema operativo de Hola. Hola [extensión de script personalizado para Windows](./../virtual-machines-windows-extensions-customscript.md) es toorun usa cualquier script de PowerShell en la máquina virtual de Hola. script de Hola se pueda almacenar en almacenamiento de Azure, cualquier extremo HTTP accesible, o incrustado en la configuración de la extensión de hello secuencia de comandos personalizada. Cuando se utiliza la extensión de script personalizado de hello, agente de máquina virtual de Azure de hello administra la ejecución de script de Hola.

Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) extensión de script personalizado de tooinstall Hola. Hola se ejecuta la extensión `powershell Add-WindowsFeature Web-Server` servidor Web IIS de Hola tooinstall:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Prueba de la aplicación

Obtener dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para `myPublicIP` creado anteriormente:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Escriba la dirección IP pública hello en el Explorador de web tooa. Con la regla NSG hello en su lugar, se muestra el sitio Web IIS de hello predeterminado. 

![Sitio predeterminado de IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Paso 6: Tareas de administración

Puede que necesite tooperform mantenimiento en hello máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo. toodeal con un aumento del tráfico tooyour aplicación, puede que necesite tooadd máquinas virtuales adicionales. Esta sección muestra cómo tooremove o agregar una máquina virtual desde el equilibrador de carga de Hola. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Quitar una máquina virtual de equilibrador de carga de Hola

Quitar una máquina virtual del grupo de direcciones de back-end de hello mediante el restablecimiento de la propiedad de LoadBalancerBackendAddressPools Hola de tarjeta de interfaz de red de Hola.

Obtener la tarjeta de interfaz de red de hello con [AzureRmNetworkInterface Get](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Establecer la propiedad de LoadBalancerBackendAddressPools de Hola de tarjeta de interfaz de red de hello demasiado null$:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Tarjeta de interfaz de red de Hola de actualización:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Agregar un equilibrador de carga de toohello VM

Después de realizar el mantenimiento de la máquina virtual o si necesita capacidad de tooexpand, agregar Hola NIC de un grupo de direcciones de back-end VM toohello Hola de equilibrador de carga.

Obtener el equilibrador de carga de hello:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Agregar grupo de direcciones de back-end de Hola de tarjeta de interfaz de red de toohello equilibrador de carga de hello:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Tarjeta de interfaz de red de Hola de actualización:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Pasos siguientes

Ejemplos – [Scripts de ejemplo de Azure Virtual Machine PowerShell](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
