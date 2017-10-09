---
title: aaaCreate un orientado a Internet de Azure carga equilibrador - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una conexión a Internet equilibrador de carga en el Administrador de recursos mediante el uso de PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Creación de un equilibrador de carga orientado a Internet en Resource Manager mediante PowerShell

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [Obtenga información acerca de cómo toocreate una conexión a Internet el equilibrador de carga utilizando el modelo de implementación clásica de hello](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Implementar soluciones de hello mediante Azure PowerShell

Hola procedimientos siguientes explica cómo toocreate una conexión a Internet el equilibrador de carga mediante el Administrador de recursos de Azure con PowerShell. Con el Administrador de recursos de Azure, cada recurso se crea y configura individualmente y, a continuación, reunir toocreate un equilibrador de carga.

Debe crear y configurar Hola después objetos toodeploy un equilibrador de carga:

* Configuración de direcciones IP front-end: contiene direcciones IP públicas (PIP) para el tráfico de red entrante.
* Grupo de direcciones de back-end: contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.
* Las reglas de equilibrio de carga: contiene reglas que se asignan a un puerto público en el puerto de tooa de equilibrador de carga de hello en grupo de direcciones de back-end de Hola.
* Reglas NAT de entrada: contiene reglas que se asignan a un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.
* Sondeos: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquina virtual en el grupo de direcciones de back-end de Hola.

Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Configurar PowerShell toouse el Administrador de recursos

Asegúrese de que dispone de hello última versión de producción del módulo de Azure Resource Manager Hola de PowerShell:

1. Inicie sesión en tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    Escriba sus credenciales cuando se le solicite.

2. Compruebe las suscripciones de hello para la cuenta de hello.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Elija qué su toouse de las suscripciones de Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Cree un grupo de recursos. (Si utiliza un grupo de recursos existente, puede omitir este paso).

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Crear una red virtual y una dirección IP pública para el grupo de direcciones IP de front-end de Hola

1. Cree una subred y una red virtual.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Crear un Azure público recurso de dirección IP, denominado **PublicIP**, toobe utilizado por un grupo IP front-end con el nombre DNS de hello **loadbalancernrp.westus.cloudapp.azure.com**. Hola siguiente comando usa Hola tipo de asignación estático.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > equilibrador de carga de Hello usa la etiqueta de Hola de dominio de la dirección IP pública de hello como prefijo para su FQDN. Esto es diferente del modelo de implementación clásica de hello, que utiliza el servicio de nube de hello como Hola FQDN del equilibrador de carga.
   > En este ejemplo, hello FQDN es **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Creación de un grupo de direcciones IP front-end y un grupo de direcciones back-end

1. Cree un grupo IP front-end denominado **front-end de LB** que usa hello **PublicIp** recursos.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Cree un grupo de direcciones de back-end llamado **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>Creación de reglas NAT, una regla de equilibrador de carga, un sondeo y un equilibrador de carga

Este ejemplo crea Hola siguientes elementos:

* Un tootranslate de regla NAT entrante todos tráfico en puerto 3441 tooport 3389
* Un tootranslate de regla NAT entrante todos tráfico en puerto 3442 tooport 3389
* Un estado de mantenimiento de sondeo regla toocheck hello en una página denominada **HealthProbe.aspx**
* Un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola
* Un equilibrador de carga que usa todos estos objetos.

Siga estos pasos:

1. Crear hello las reglas NAT.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Cree un sondeo de estado. Hay dos tooconfigure formas un sondeo:

    Sondeo HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Sondeo TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Cree una regla de equilibrador de carga.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Crea el equilibrador de carga de hello mediante objetos de Hola que creó anteriormente.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>Cree tarjetas NIC

Crear interfaces de red (o modificar los existentes) y después asociar reglas de tooNAT, reglas de equilibrador de carga y sondeos:

1. Obtener la red virtual de hello y una subred de red virtual, donde hello NIC necesitan toobe creado.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Cree una NIC denominada **nic1 de carga equilibrada puede**y lo asocia a la primera regla NAT de Hola y el grupo de direcciones de back-end de primer (y único) de Hola.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Cree una NIC denominada **nic2 de carga equilibrada puede**y lo asocia a la segunda regla NAT de Hola y el grupo de direcciones de back-end de primer (y único) de Hola.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Compruebe Hola NIC.

        $backendnic1

    Resultado esperado:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
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
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Hola de uso `Add-AzureRmVMNetworkInterface` cmdlet tooassign Hola NIC toodifferent máquinas virtuales.

## <a name="create-a-virtual-machine"></a>de una máquina virtual

Para instrucciones sobre cómo crear una máquina virtual y asignar una NIC, consulte el artículo sobre cómo [crear una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Agregar equilibrador de carga de toohello de interfaz de red de Hola

1. Recuperar el equilibrador de carga de Hola de Azure.

    Cargar recursos de equilibrador de carga de hello en una variable (si aún no lo ha hecho todavía). Hola variable se denomina **$lb**. Usar hello mismos nombres de recurso de equilibrador de carga de Hola que creó anteriormente.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Variable de tooa de configuración de back-end de Hola de carga.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Cargar la interfaz de red de hello ya creado en una variable. nombre de variable de Hello es **$nic**. Hello nombre de la interfaz de red es Hola misma de hello ejemplo anterior.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Cambiar configuración de back-end de hello en la interfaz de red de Hola.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Guardar el objeto de interfaz de red de Hola.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Después de una interfaz de red se agrega el grupo de back-end de equilibradores de carga de toohello, comienza a recibir tráfico de red en función de reglas de equilibrio de carga de Hola para ese recurso de equilibrador de carga.

## <a name="update-an-existing-load-balancer"></a>Actualización de un equilibrador de carga existente

1. Equilibrador de carga mediante el uso de Hola Hola ejemplo anterior, asigne una variable de toohello del objeto de equilibrador de carga **$slb** utilizando `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. En el siguiente ejemplo de Hola, agregará una regla NAT de entrada--mediante el puerto 81 en grupo de servidores front-end de Hola y puerto 8181 para grupo de back-end de hello--tooan equilibrador de carga existente.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Guardar la nueva configuración de hello mediante `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Elimine un equilibrador de carga

Use el comando de hello `Remove-AzureLoadBalancer` toodelete un equilibrador de carga previamente creada denominado **NRP LB** en un grupo de recursos denominado **NRP RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Puede usar el modificador opcional hello **-Force** tooavoid mensaje de Hola para su eliminación.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
