---
title: "Configuración de la tunelización forzada para conexiones de sitio a sitio de Azure: Resource Manager | Microsoft Docs"
description: "Cómo tooredirect o 'force' todos los tooyour de espera de tráfico de vinculado a Internet en ubicación y local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Configurar la tunelización forzada mediante el modelo de implementación de hello Azure Resource Manager

Forzada permite redirigir o "forzar" todos los vinculado a Internet tráfico tooyour back-ubicación de local a través de un túnel VPN de sitio a sitio para inspección y auditoría de túnel. Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI. Sin la tunelización forzada, tráfico de Internet desde las máquinas virtuales en Azure siempre atraviesa de infraestructura de red de Azure directamente out toohello Internet, sin Hola opción tooallow se tooinspect o auditoría tráfico Hola. Acceso de Internet no autorizado puede provocar potencialmente la divulgación de tooinformation u otros tipos de infracciones de seguridad.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

Este artículo le guiará a través de configuración forzada de túnel para redes virtuales creadas mediante el modelo de implementación del Administrador de recursos de Hola. La tunelización forzada puede configurarse mediante el uso de PowerShell, no a través del portal de Hola. Si desea tooconfigure tunelización para el modelo de implementación clásica de hello forzada, seleccione artículo clásico de hello después de la lista desplegable:

> [!div class="op_single_selector"]
> * [PowerShell: clásico](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell: administrador de recursos](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Información acerca de la tunelización forzada

Hola siguiente diagrama ilustra forzada cómo funciona la tunelización. 

![Tunelización forzada](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

En el ejemplo de Hola anterior, Hola front-end no se fuerza la subred de túnel. las cargas de trabajo de Hello en la subred de front-end de hello pueden continuar tooaccept y responder las solicitudes de toocustomer de hello Internet directamente. Hello subredes de nivel intermedio y back-end se convierten obligatoriamente túnel. Las conexiones de salida de estos toohello dos subredes Internet será tooan forzado o redirigida volver al sitio local a través de una de hello que túneles VPN S2S.

Esto le permite toorestrict e inspeccionar el acceso a Internet desde las máquinas virtuales o servicios de nube de Azure, mientras continúa tooenable su arquitectura de servicio de varios niveles necesaria. Si no hay ningún cargas de trabajo orientado a Internet en las redes virtuales, también se pueden aplicar forzada túnel toohello todo redes virtuales.

## <a name="requirements-and-considerations"></a>Requisitos y consideraciones

La tunelización forzada en Azure se configura a través de rutas definidas por el usuario de redes virtuales. Redirigir el tráfico tooan local de sitio se expresa como una puerta de enlace de VPN de Azure de toohello de ruta predeterminada. Para obtener más información sobre las redes virtuales y las rutas definidas por el usuario, consulte [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).

* Cada subred de la red virtual tiene una tabla de enrutamiento del sistema integrada. tabla de enrutamiento de sistema de Hello tiene Hola los tres grupos de rutas siguientes:
  
  * **Las rutas de red virtual locales:** directamente toohello máquinas virtuales de destino en hello misma red virtual.
  * **Rutas locales:** toohello puerta de enlace de VPN de Azure.
  * **Ruta predeterminada:** toohello directamente Internet. Se quitan los paquetes destinados toohello las direcciones IP privadas no cubiertas por las rutas de hello dos anteriores.
* Este procedimiento utiliza rutas definidas por el usuario (UDR) toocreate una tooadd de tabla de enrutamiento una ruta predeterminada y, a continuación, asociar Hola enrutamiento tabla tooyour red virtual subredes tooenable forzado túnel en esas subredes.
* La tunelización forzada debe asociarse a una red virtual que tenga una puerta de enlace de VPN basada en rutas. Deberá tooset un sitio denominado"predeterminado" entre la red virtual de hello entre entornos sitios locales toohello conectado. Además, Hola local dispositivo VPN debe configurarse mediante 0.0.0.0/0 como selectores de tráfico. 
* La tunelización forzada de ExpressRoute no se configura mediante este mecanismo, pero en su lugar, se habilita de forma anunciando una ruta predeterminada a través de hello BGP de ExpressRoute sesiones de emparejamiento. Para obtener más información, vea hello [documentación de ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Información general sobre la configuración

Hola procedimiento le ayuda a crear un grupo de recursos y una red virtual. Después, creará una puerta de enlace de VPN y configurará la tunelización forzada. En este procedimiento, la red virtual de hello 'Red virtual de varios niveles' no tiene tres subredes: 'Front-end', 'Nivel intermedio' y 'Back-end', con cuatro entre entornos conexiones: 'DefaultSiteHQ' y tres bifurcaciones.

pasos del procedimiento Hola establecer hello 'DefaultSiteHQ' como conexión de sitio predeterminado de hello tunelización forzada y configurar hello 'Nivel intermedio' y 'Back-end' subredes toouse tunelización forzada.

## <a name="before-you-begin"></a>Antes de empezar

Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.

### <a name="toolog-in"></a>toolog en

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Configuración de la tunelización forzada

1. Cree un grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Cree una red virtual y especifique las subredes.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Crear Hola puertas de enlace de red local.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Crear regla de ruta y la tabla de ruta de Hola.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Asociar Hola ruta tabla toohello nivel intermedio y las subredes de back-end.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Crear Hola puerta de enlace con un sitio predeterminado. Este paso toma algunas toocomplete de tiempo, en ocasiones 45 minutos o más, porque para crear y configurar la puerta de enlace de Hola.<br> Hola **- GatewayDefaultSite** es Hola parámetro del cmdlet que permite Hola forzada toowork de configuración de enrutamiento, eche un vistazo tooconfigure cuidado esta opción correctamente. Este parámetro solo está disponible en PowerShell 1.0 o posterior.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Establecer las conexiones VPN de sitio a sitio Hola.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```