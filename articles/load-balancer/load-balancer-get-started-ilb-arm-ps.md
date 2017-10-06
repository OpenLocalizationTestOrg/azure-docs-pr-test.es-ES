---
title: aaaCreate un interno de Azure carga equilibrador - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador mediante PowerShell en el Administrador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Creación del equilibrador de carga interno con PowerShell

> [!div class="op_single_selector"]
> * [Portal de Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Hola pasos explica cómo toocreate un interno cargar equilibrador con el Administrador de recursos de Azure PowerShell. Con el Administrador de recursos de Azure, Hola elementos toocreate un equilibrador de carga interno se configuran individualmente y, a continuación, se combinan toocreate un equilibrador de carga.

Necesita toocreate y configurar Hola después objetos toodeploy un equilibrador de carga:

* Delante de la configuración de IP final: configurar la dirección IP privada de hello para el tráfico de red entrante
* Grupo de direcciones de back-end - configurará las interfaces de red de Hola que recibirán tráfico con equilibrio de carga de hello procedentes de grupo de direcciones IP de front-end
* Reglas de equilibrio de carga: equilibrador de carga de origen y configuración del puerto local para saludo.
* Sondea - configura el sondeo de estado de mantenimiento de Hola para instancias de máquina Virtual de Hola.
* Reglas NAT de entrada: se configura el acceso de toodirectly de reglas de puerto de hello entre instancias de máquina Virtual de Hola.

Para obtener más información acerca de los componentes del equilibrador de carga con el Administrador de recursos de Azure en [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](load-balancer-arm.md).

Hello pasos siguientes se explica cómo tooconfigure un equilibrador de carga entre dos máquinas virtuales.

## <a name="setup-powershell-toouse-resource-manager"></a>El programa de instalación PowerShell toouse el Administrador de recursos

Asegúrese de que tiene Hola última versión de producción de hello Azure módulo de PowerShell y tengan PowerShell configurar correctamente tooaccess su suscripción de Azure.

### <a name="step-1"></a>Paso 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Paso 2

Compruebe las suscripciones de hello para la cuenta de hello

```powershell
Get-AzureRmSubscription
```

Es posible que tooAuthenticate solicitada con sus credenciales.

### <a name="step-3"></a>Paso 3

Elija qué su toouse de las suscripciones de Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Creación de un grupo de recursos para el equilibrador de carga

Creación de un grupo de recursos (omitir este paso si se usa un grupo de recursos existente)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los comandos toocreate que se va a usar un equilibrador de carga Hola mismo grupo de recursos.

Hola ejemplo anterior crea un grupo de recursos denominado "NRP-RG" y la ubicación "West US".

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Creación de una red virtual y una dirección IP privada para el grupo de IP front-end

Crea una subred de red virtual de Hola y asigna toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Cree una red virtual:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Crea la red virtual de Hola y agrega la red virtual de hello subred toohello lb subred ser NRPVNet y asigna toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Creación de un grupo de direcciones IP front-end y un grupo de direcciones back-end

Cómo configurar un grupo IP de front-end para Hola entrante cargar tráfico de red de equilibrador y tráfico de equilibrio de carga de back-end dirección grupo tooreceive Hola.

### <a name="step-1"></a>Paso 1

Cree un grupo IP de front-end con la dirección IP privada de hello 10.0.2.5 para hello subred 10.0.2.0/24 que será el extremo del tráfico de red entrante de Hola.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Paso 2

Configurar un grupo de direcciones de back-end utiliza tooreceive el tráfico entrante de grupo de direcciones IP de front-end:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Creación de reglas de equilibrio de carga, reglas NAT, sondeos y el equilibrador de carga

Después de crear el grupo de direcciones IP de front-end de Hola y el grupo de direcciones de back-end de hello, necesitará las reglas de hello toocreate que pertenecerán el recurso de equilibrador de carga de toohello:

### <a name="step-1"></a>Paso 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

ejemplo de Hola anterior está creando Hola siguientes elementos:

* Regla NAT que todos los entrantes tráfico tooport 3441 irá tooport 3389.
* una segunda regla NAT que todos los entrantes tráfico tooport 3442 irá tooport 3389.
* una regla de equilibrador de carga que se cargará equilibrar todo el tráfico entrante en el puerto de puerto público 80 toolocal 80 en el grupo de direcciones de back-end de Hola.
* una regla de sondeo que comprobará el estado de mantenimiento de Hola de ruta de acceso "HealthProbe.aspx"

### <a name="step-2"></a>Paso 2

Crear el equilibrador de carga de hello sumar todos los objetos (reglas NAT, reglas de equilibrador de carga, las configuraciones de sondeo):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Creación de interfaces de red

Después de crear el equilibrador de carga interno de hello, debe definir qué interfaces de red va a recibir Hola entrante con equilibrio de carga tráfico de red, las reglas de NAT y sondeo. interfaz de red de Hello en este caso se configura individualmente y se puede asignar máquinas virtuales de tooa más adelante.

### <a name="step-1"></a>Paso 1

Obtener recursos de hello virtuales interfaces de red de toocreate de red y la subred:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Este paso crea una interfaz de red que pertenecerán toohello grupo de back-end de equilibradores de carga y asociar la primera regla NAT de Hola para RDP para esta interfaz de red:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Paso 2

Cree una segunda interfaz de red llamada LB-Nic2-BE:

Este paso crea una segunda interfaz de red, asignar toohello mismo equilibrador de carga volver Finalizar grupo y asociar la segunda regla NAT Hola creado para RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

resultado final de Hello mostrará siguiente hello:

    $backendnic1

Resultado esperado:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Paso 3

Usar comandos hello AzureRmVMNetworkInterface agregar hello tooassign NIC virtual tooa máquina.

Puede encontrar Hola toocreate instrucciones paso a paso una máquina virtual y asigne tooa NIC siguiendo Hola documentación: [crear una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Agregar la interfaz de red de Hola

Si ya tiene una máquina virtual creada, puede agregar la interfaz de red de Hola con hello siguiendo los pasos:

### <a name="step-1"></a>Paso 1

Cargar recursos de equilibrador de carga de hello en una variable (si aún no lo ha hecho todavía). variable de saludo que se utiliza es $lb llamado y Hola uso mismos nombres de recurso de equilibrador de carga de hello creados anteriormente.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Paso 2

Variable de tooa de configuración de carga Hola back-end.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Paso 3

Cargar la interfaz de red de hello ya creado en una variable. nombre de variable de Hello utilizado es $ tarjeta NIC. nombre de la interfaz de red Hello usa es Hola igual de ejemplo de Hola anterior.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Paso 4

Cambiar configuración de back-end de hello en la interfaz de red de Hola.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Paso 5

Guardar el objeto de interfaz de red de Hola.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Después de una interfaz de red se agrega el grupo de back-end de equilibradores de carga de toohello, comienza a recibir tráfico de red en función de las reglas para ese recurso de equilibrador de carga de equilibrio de carga de Hola.

## <a name="update-an-existing-load-balancer"></a>Actualización de un equilibrador de carga existente

### <a name="step-1"></a>Paso 1
Con el equilibrador de carga de Hola de ejemplo de Hola anterior, asignar $slb mediante Get-AzureRmLoadBalancer de toovariable de objeto de equilibrador de carga

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Paso 2

En el siguiente ejemplo de Hola, agregará una nueva regla de NAT de entrada mediante el puerto 81 de front-end de Hola y puerto 8181 para la copia de hello finalizar equilibrador de carga existente de grupo tooan

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Paso 3

Guardar configuración nueva de hello mediante Set-AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Elimine un equilibrador de carga

Usar Hola comando Remove-AzureRmLoadBalancer toodelete un equilibrador de carga creada anteriormente con el nombre "NRP-LB" en un grupo de recursos denominado "NRP-RG"

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Puede usar Hola opcional cambiar - Force tooavoid Hola para su eliminación.

## <a name="next-steps"></a>Pasos siguientes

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
