---
title: "aaaCreating escalas de máquina Virtual establece mediante cmdlets de PowerShell | Documentos de Microsoft"
description: "Empezar a crear y administrar los primeros conjuntos de escalado de máquina virtual de Azure con cmdlets de Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>Creación de conjuntos de escalado de máquina virtual con cmdlets de PowerShell
Este artículo le guía a través de un ejemplo de cómo toocreate una escala de máquinas virtuales establece (VMSS). Crea un conjunto de escalado de tres nodos, con redes y almacenamiento asociados.

## <a name="first-steps"></a>Primeros pasos
Asegúrese de tener instalado hello más reciente Azure PowerShell módulo, toomake dispone de los cmdlets de PowerShell de hello necesario toomaintain y crear conjuntos de escalas de.
Vaya a herramientas de línea de comandos de toohello [aquí](http://aka.ms/webpi-azps) para Hola más reciente de los módulos de Azure disponibles.

toofind VMSS relacionados con los cmdlets, use la cadena de búsqueda de hello \*VMSS\*. Por ejemplo, _gcm *vmss*_.

## <a name="creating-a-vmss"></a>Creación de un VMSS
#### <a name="create-resource-group"></a>Crear grupo de recursos
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>Crear redes (VNET o subred)
#### <a name="subnet-specification"></a>Especificación de subred
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>Especificación de VNET
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>Crear el recurso de IP pública tooAllow acceso externo
Se trata de enlazado toohello equilibrador de carga.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>Cree un equilibrador de carga
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a>Configurar el equilibrador de carga
Crear configuración de grupo de direcciones de back-end, esto va a compartirse entre NIC Hola de máquinas virtuales de hello en el conjunto de escalas de Hola.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

Establece el puerto de sondeo con equilibrio de carga, cambiar la configuración de hello según corresponda para su aplicación.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

Crear un grupo NAT entrante para una conexión directa enrutada (no carga equilibrada) toohello máquinas virtuales en la escala de hello establecido por medio de hello equilibrador de carga. Esto es toodemonstrate con RDP y no puede ser necesario en la aplicación.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Crear Hola regla de equilibrio de carga, en este ejemplo se muestra en carga equilibrio puerto 80 solicitudes, usando la configuración de Hola de los pasos anteriores.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

Cree el equilibrador de carga con la configuración.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

Compruebe la configuración de carga Equilibrada, compruebe la carga equilibrada puerto configuraciones, tenga en cuenta que no verá que se crean las reglas de NAT de entrada hasta hello las máquinas virtuales en el conjunto de escalas de Hola.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>Configurar y crear Hola escala configurada
Tenga en cuenta que esta infraestructura en el ejemplo se muestra cómo distribuir tooset seguridad y tráfico de web de escala en el conjunto de escalas de hello, pero Hola imágenes de máquinas virtuales especificadas aquí no tiene ningún servicio web instalado.

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

Enlazar tooLoad NIC equilibrador y subred

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

Crear la configuración del conjunto de escalado

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

Compilar la configuración del conjunto de escalado

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

Ahora ha creado el conjunto de escalas de Hola. Puede probar conexión toohello máquinas virtuales individuales mediante RDP en este ejemplo:

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
