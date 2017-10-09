---
title: comandos aaaCommon PowerShell para redes virtuales de Azure | Documentos de Microsoft
description: "Los comandos de PowerShell comunes tooget que inició la creación de una red virtual y sus recursos asociados para las máquinas virtuales."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Comandos comunes de PowerShell para redes virtuales de Azure

Si desea toocreate una máquina virtual, debe toocreate una [red virtual](../../virtual-network/virtual-networks-overview.md) o saber acerca de una red virtual existente en qué Hola se puede agregar la máquina virtual. Normalmente, cuando se crea una máquina virtual, también necesita tooconsider crear recursos de hello descritos en este artículo.

Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.

Algunas de las variables podrían ser útiles para si ejecuta más de uno de los comandos de hello en este artículo:

- $location - ubicación de Hola Hola de recursos de red. Puede usar [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind una [región geográfica](https://azure.microsoft.com/regions/) que se adapte a sus necesidades.
- $myResourceGroup - nombre de Hola Hola del grupo de recursos donde se encuentran los recursos de red de Hola.

## <a name="create-network-resources"></a>Crear recursos de red

| Tarea | Comando |
| ---- | ------- |
| Crear configuraciones de subred |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>Una red típica podría tener una subred para un [equilibrador de carga accesible desde Internet](../../load-balancer/load-balancer-internet-overview.md) y una subred independiente para un [equilibrador de carga interno](../../load-balancer/load-balancer-internal-overview.md). |
| Crear una red virtual |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| Prueba para un nombre de dominio único |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>Puede especificar un nombre de dominio DNS para un [recurso IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), que crea una asignación para la dirección IP pública de domainname.location.cloudapp.azure.com toohello en hello servidores DNS administrados de Azure. Hola nombre puede contener solo letras, números y guiones. Hello primero y último carácter debe ser una letra o un número y nombre de dominio de hello debe ser único dentro de su ubicación de Azure. Si se devuelve **True** , significa que el nombre propuesto es único globalmente. |
| Crear una dirección IP pública |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>dirección IP pública de Hello usa nombre de dominio de Hola que previamente probado y que sirve a la configuración de front-end de Hola Hola de equilibrador de carga. |
| Crear una configuración de direcciones IP de front-end |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>configuración de front-end de Hello incluye la dirección IP pública Hola que creó anteriormente para el tráfico de red entrante. |
| Crear un grupo de direcciones de back-end |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Proporciona direcciones internas para hello back-end de hello cargar equilibrador que se tiene acceso a través de una interfaz de red. |
| Elaboración de un sondeo |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>Contiene la disponibilidad de toocheck de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola. |
| Crear una regla de equilibrio de carga |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>Contiene reglas que asignar un puerto público en el equilibrador de carga de hello tooa puerto en el grupo de direcciones de back-end de Hola. |
| Crear una regla NAT entrante |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>Contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola. |
| Crear un equilibrador de carga |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| Crear una interfaz de red |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Crear una interfaz de red con dirección IP pública de Hola y subred de red virtual que creó anteriormente. |

## <a name="get-information-about-network-resources"></a>Obtención de información sobre recursos de red

| Tarea | Comando |
| ---- | ------- |
| Enumerar redes virtuales |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>Enumera todas las redes virtuales hello en el grupo de recursos de Hola. |
| Obtener información sobre una red virtual |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| Enumerar subredes de una red virtual |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| Obtener información sobre una subred |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Obtiene información sobre la subred de hello en red virtual especificada de Hola. valor de Hello $vnet representa objeto Hola devuelto por Get-AzureRmVirtualNetwork. |
| Enumerar direcciones IP |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>Enumera las direcciones IP públicas de hello en el grupo de recursos de Hola. |
| Enumerar equilibradores de carga |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>Enumera todos los equilibradores de carga de hello en el grupo de recursos de Hola. |
| Enumerar interfaces de red |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>Enumera todas las interfaces de red de hello en el grupo de recursos de Hola. |
| Obtener información sobre una interfaz de red |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Obtiene información sobre una interfaz de red específica. |
| Obtener configuración de IP de Hola de una interfaz de red |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>Obtiene información sobre la configuración de IP de Hola de interfaz de red especificado de Hola. valor de Hello $nic representa objeto Hola devuelto por Get-AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Administración de recursos de red

| Tarea | Comando |
| ---- | ------- |
| Agregar una red virtual de tooa de subred |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Agrega una subred tooan red virtual. valor de Hello $vnet representa objeto Hola devuelto por Get-AzureRmVirtualNetwork. |
| Eliminar una red virtual |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>Red virtual especificado de Hola se quita del grupo de recursos de Hola. |
| Eliminar una interfaz de red |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Quita la interfaz de red especificado de hello del grupo de recursos de Hola. |
| Eliminar un equilibrador de carga |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" - ResourceGroupName $myResourceGroup<BR><BR>Hola quita especificado equilibrador de carga del grupo de recursos de Hola. |
| Eliminar una dirección IP pública |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>Hola quita especifica la dirección IP pública del grupo de recursos de Hola. |

## <a name="next-steps"></a>Pasos siguientes
* Interfaz de red de uso Hola recién creado cuando se [crear una máquina virtual](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Obtenga información sobre cómo puede [crear una máquina virtual con varias interfaces de red](../../virtual-network/virtual-networks-multiple-nics.md).

