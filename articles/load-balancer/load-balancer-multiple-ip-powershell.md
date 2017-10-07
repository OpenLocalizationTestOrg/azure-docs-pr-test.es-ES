---
title: aaaLoad equilibrio en varias configuraciones de IP en Azure | Documentos de Microsoft
description: Equilibrio de carga entre las configuraciones de IP principales y secundarias.
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>Equilibrio de carga en varias configuraciones de IP mediante PowerShell

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Este artículo describe cómo aborda toouse equilibrador de carga de Azure con varias IP en una interfaz de red secundaria (NIC). En este escenario, tenemos dos máquinas virtuales que ejecutan Windows. Cada una de ellas cuenta con una NIC principal y otra secundaria. Cada uno de hello secundaria NIC tienen dos configuraciones de IP. Cada máquina virtual hospeda dos sitios web: contoso.com y fabrikam.com. Cada sitio Web está enlazado tooone Hola de configuraciones de IP en la NIC de hello secundaria. Utilizamos el equilibrador de carga Azure tooexpose dos front-end direcciones IP, una para cada sitio Web, toodistribute tráfico toohello respectivo configuración IP para el sitio Web de Hola. Este escenario utiliza Hola el mismo número de puerto a través de front-ends, así como las direcciones IP de back-end del grupo.

![Imagen del escenario de equilibrio de carga](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo de tooload de pasos en varias configuraciones de IP

Siga los pasos de hello debajo de escenario de hello tooachieve descrito en este artículo:

1. Instale Azure PowerShell. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.
2. Crear un grupo de recursos mediante Hola después de configuración:

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Para más información, consulte el [Paso 2: Creación de un grupo de recursos](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Crear un conjunto de disponibilidad](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain las máquinas virtuales. En este escenario, utilice Hola siguiente comando:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. Siga las instrucciones pasos 3 a 5 [crear una VM de Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artículo creación de hello tooprepare de una máquina virtual con una NIC único. Ejecute paso 6.1 y utilice el siguiente hello en lugar del paso 6.2:

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    Después, complete los pasos 6.3 a 6.8 de [Creación de una máquina virtual Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

5. Agregue un segundo tooeach de configuración de IP de hello las máquinas virtuales. Siga las instrucciones de hello en [asignar varias direcciones IP toovirtual máquinas](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artículo. Usar hello siguientes opciones de configuración:

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    No es necesario tooassociate Hola secundaria las configuraciones IP con direcciones IP públicas para la finalidad de Hola de este tutorial. Editar parte de asociación de hello comando tooremove Hola pública IP.

6. Complete de nuevo los pasos 4 a 6 de este artículo para VM2. Ser seguro tooreplace Hola VM nombre tooVM2 cuando haga esto. Tenga en cuenta que no es necesario toocreate una red virtual para hello segunda máquina virtual. Según sus necesidades de uso, puede crear o no una nueva subred.

7. Crear dos direcciones IP públicas y almacenarlos en variables apropiadas Hola tal como se muestra:

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. Cree dos configuraciones de IP de front-end:

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Cree los grupos de direcciones de back-end, un sondeo y las reglas de equilibrio de carga:

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. Una vez que tenga estos recursos creados, cree el equilibrador de carga:

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Agregar Hola segundo back-end dirección front-end y grupo de IP configuration tooyour recién creado equilibrador de carga:

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. comandos de Hello siguiente obtener NIC de hello y, a continuación, agregar que ambas configuraciones IP de cada grupo de direcciones secundaria de back-end toohello NIC de hello equilibrador de carga:

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. Por último, debe configurar el dirección IP de DNS recursos registros toopoint toohello respectivos front-end de hello equilibrador de carga. Puede hospedar los dominios en Azure DNS. Para más información sobre el uso de Azure DNS con Load Balancer, consulte [Uso de Azure DNS con otros servicios de Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Pasos siguientes
- Obtener más información acerca de cómo Equilibrio de carga de toocombine services en Azure en [con servicios de equilibrio de carga en Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Obtenga información acerca de cómo puede usar varios tipos de registros de Azure toomanage y solucionar problemas de equilibrador de carga en [análisis de registros para el equilibrador de carga de Azure](../load-balancer/load-balancer-monitor-log.md).
