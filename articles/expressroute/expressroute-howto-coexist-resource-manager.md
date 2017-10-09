---
title: "Configuración de conexiones de ExpressRoute y VPN de sitio a sitio coexistentes: Resource Manager: Azure | Microsoft Docs"
description: "Este artículo le guiará en la configuración de conexiones ExpressRoute y VPN de sitio a sitio que puedan coexistir en el modelo de implementación de Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Configuración de conexiones coexistentes de ExpressRoute de sitio a sitio
> [!div class="op_single_selector"]
> * [PowerShell: administrador de recursos](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell: clásico](expressroute-howto-coexist-classic.md)
> 
> 

La configuración de las conexiones coexistentes VPN de sitio a sitio y ExpressRoute tiene varias ventajas. Puede configurar una VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExressRoute o usar VPN de sitio a sitio tooconnect toosites que no están conectados a través de ExpressRoute. Trataremos Hola pasos tooconfigure ambos escenarios en este artículo. En este artículo se aplica el modelo de implementación del Administrador de recursos de toohello y usa PowerShell. Esta configuración no está disponible en hello portal de Azure.

> [!IMPORTANT]
> Circuitos ExpressRoute deben configurarse previamente antes de seguir estas instrucciones Hola. Asegúrese de que ha seguido las guías de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y [configurar el enrutamiento de](expressroute-howto-routing-arm.md) antes de continuar.
> 
> 

## <a name="limits-and-limitations"></a>Límites y limitaciones
* **No se admite el enrutamiento transitorio.** No se puede realizar un enrutamiento (a través de Azure) entre una red local conectada a través de una VPN sitio a sitio y una red local conectada a través de ExpressRoute.
* **No se admite la puerta de enlace de la SKU de nivel Básico.** Debe usar una puerta de enlace básico SKU que no sea para ambos hello [puerta de enlace ExpressRoute](expressroute-about-virtual-network-gateways.md) hello y [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Solo se admite la VPN Gateway basada en rutas.** Debe usar una [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) basada en rutas.
* **Se debe configurar una ruta estática para VPN Gateway.** Si la red local está conectado tooboth ExpressRoute y un sitio a sitio VPN, debe tener una ruta estática configurada en su toohello de conexión de red local tooroute Hola sitio a sitio VPN Internet pública.
* **Puerta de enlace de ExpressRoute debe configurarse en primer lugar y vinculado tooa circuito.** Debe crear la puerta de enlace de ExpressRoute de hello en primer lugar y vincularla tooa circuito antes de agregar la puerta de enlace VPN de sitio a sitio Hola.

## <a name="configuration-designs"></a>Diseños de configuración
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configuración de una VPN de sitio a sitio como una ruta de acceso de conmutación por error para ExpressRoute
Puede configurar una conexión VPN de sitio a sitio como una copia de seguridad para ExpressRoute. Esto aplica solo toovirtual redes vinculado toohello Azure ruta privada de intercambio de tráfico. No hay ninguna solución de conmutación por error basada en VPN para servicios accesibles a través de emparejamientos de Microsoft y públicos de Azure. Hola circuito de ExpressRoute no distingue vínculo principal Hola. Los datos fluyen a través de la ruta de acceso VPN de sitio a sitio Hola solo si se produce un error en hello circuito de ExpressRoute.

> [!NOTE]
> Mientras se prefiere circuito de ExpressRoute a través de VPN de sitio a sitio cuando ambas rutas se Hola igual, Azure utilizará ruta de hello más larga prefijo coincidencia toochoose Hola hacia el destino del paquete de saludo.
> 
> 

![Coexistencia](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurar una toosites de tooconnect VPN de sitio a sitio no está conectado a través de ExpressRoute
Puede configurar la red donde algunos sitios conectan directamente tooAzure a través de VPN de sitio a sitio y algunos de los sitios a través de ExpressRoute. 

![Coexistencia](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> No se puede configurar una red virtual como un enrutador de tránsito.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Seleccionar Hola pasos toouse
Hay dos conjuntos diferentes de los procedimientos toochoose de. procedimiento de configuración de Hola que seleccione depende de si tiene una red virtual existente que desea tooconnect a, o desea toocreate una nueva red virtual.

* No tiene una red virtual y necesita toocreate uno.
  
    Si aún no tiene una red virtual, este procedimiento le guía en la creación de una nueva red virtual mediante el modelo de implementación de Resource Manager y la creación de nuevas conexiones VPN de sitio a sitio y ExpressRoute. tooconfigure una red virtual, siga los pasos de hello en [toocreate una nueva red virtual y las conexiones coexistentes](#new).
* Ya tengo una red virtual del modelo de implementación de Resource Manager.
  
    Puede que ya tenga una red virtual con una conexión VPN de sitio a sitio o una conexión ExpressRoute existentes. Hola [tooconfigure coexistentes conexiones para una red virtual existente ya](#add) sección le guía a través de la eliminación de puerta de enlace de hello y, a continuación, crear nuevas conexiones de VPN de sitio a sitio y de ExpressRoute. Al crear nuevas conexiones de hello, pasos de hello deben realizarse en un orden específico. No utilice instrucciones de hello en otro artículos toocreate sus conexiones y las puertas de enlace.
  
    En este procedimiento, crear conexiones que pueden coexistir requiere toodelete la puerta de enlace y, a continuación, configure nuevas puertas de enlace. Tendrá tiempo de inactividad para las conexiones entre entornos al eliminar y volver a crear la puerta de enlace y las conexiones, pero no tendrá que toomigrate cualquiera de su máquinas virtuales o servicios tooa nueva red virtual. Las máquinas virtuales y servicios se seguirán toocommunicate capaz de salida a través del equilibrador de carga de hello al configurar la puerta de enlace si están toodo configurado así.

## <a name="new"></a>toocreate una nueva red virtual y las conexiones coexistentes
Este procedimiento le guía en la creación de una red virtual y conexiones de sitio a sitio y ExpressRoute que coexisten.

1. Instalar versión más reciente de Hola de hello cmdlets de PowerShell de Azure. Para obtener información acerca de cómo instalar los cmdlets de hello, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). cmdlets de Hola que se usan para esta configuración puede ser ligeramente diferente de lo que es posible que esté familiarizado con. Cmdlets de hello toouse seguro especificar en estas instrucciones.
2. Inicie sesión en tooyour cuenta y configurar el entorno de Hola.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Cree una red virtual, incluida la subred de la puerta de enlace. Para obtener más información acerca de la configuración de red virtual de hello, consulte [configuración de red Virtual de Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Hola subred de puerta de enlace debe ser /27 o un prefijo más corto (por ejemplo, /26 o /25).
   > 
   > 
   
    Cree una nueva red virtual.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Agregue subredes.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Guardar configuración de redes virtuales de Hola.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Cree una puerta de enlace de ExpressRoute. Para obtener más información acerca de la configuración de puerta de enlace de ExpressRoute de hello, consulte [configuración de puerta de enlace de ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Hello GatewaySKU debe ser *estándar*, *HighPerformance*, o *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Vínculo de circuito de ExpressRoute de toohello de puerta de enlace de ExpressRoute de Hola. Una vez completado este paso, se establece la conexión de hello entre la red local y Azure, a través de ExpressRoute. Para obtener más información acerca de la operación de enlace de hello, consulte [tooExpressRoute de redes virtuales de vínculo](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>A continuación, cree la puerta de enlace de la VPN de sitio a sitio. Para obtener más información acerca de la configuración de puerta de enlace VPN de hello, consulte [configurar una red virtual con una conexión de sitio a sitio](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Hello GatewaySKU debe ser *estándar*, *HighPerformance*, o *UltraPerformance*. debe Hello VpnType *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Azure VPN Gateway admite el protocolo de enrutamiento de BGP. Puede especificar ASN (número de AS) para esa red Virtual mediante la adición de conmutador de Asn - Hola Hola siguiente comando. No se especifica ese parámetro se 65515 número tooAS de forma predeterminada.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    Puede encontrar Hola emparejamiento IP BGP y Hola como número que utiliza Azure para puerta de enlace VPN de hello en $azureVpn.BgpSettings.BgpPeeringAddress y $azureVpn.BgpSettings.Asn. Para más información, consulte [Configuración de BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) para Azure VPN Gateway.
7. Cree una entidad de puerta de enlace de VPN de sitio local. Este comando no configura la puerta de enlace de VPN local. En su lugar, permite a tooprovide la configuración de puerta de enlace local hello, como la dirección IP pública de Hola y Hola local espacio de direcciones, por lo que hello puerta de enlace VPN de Azure puede conectarse tooit.
   
    Si su dispositivo VPN local solo admite enrutamiento estático, puede configurar rutas estáticas Hola Hola siguiente forma:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Si su dispositivo VPN local admite Hola BGP y desea tooenable de enrutamiento dinámico, debe tooknow Hola BGP emparejamiento hello como número de que la VPN local y la IP de dispositivo usa.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Configure su local VPN dispositivo tooconnect toohello nueva puerta de enlace VPN. Para obtener más información sobre la configuración del dispositivo VPN, vea [Configuración de dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Vínculo Hola VPN de sitio a sitio puerta de enlace en Azure toohello puerta de enlace local.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>tooconfigure coexistentes conexiones para una red virtual existente
Si tiene una red virtual existente, compruebe el tamaño de subred de puerta de enlace de Hola. Si está en la subred de puerta de enlace de hello /28 o /29, primero debe eliminar la puerta de enlace de red virtual de Hola y aumentar el tamaño de subred de puerta de enlace de Hola. Hello pasos de esta sección muestran cómo toodo que.

Si está de subred de puerta de enlace de hello /27 o superior y red virtual de hello está conectado a través de ExpressRoute, puede omitir estos pasos hello y continuar demasiado["Paso 6: crear una puerta de enlace VPN de sitio a sitio"](#vpngw) en la sección anterior de Hola. 

> [!NOTE]
> Cuando se elimina la puerta de enlace existente hello, sus instalaciones locales perderá red virtual de hello conexión tooyour mientras se trabaja con esta configuración. 
> 
> 

1. Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell de Azure. Para obtener más información acerca de cómo instalar los cmdlets, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). cmdlets de Hola que se usan para esta configuración puede ser ligeramente diferente de lo que es posible que esté familiarizado con. Cmdlets de hello toouse seguro especificar en estas instrucciones. 
2. Eliminar Hola VPN de sitio a sitio o ExpressRoute puerta de enlace existente.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Elimine la subred de puerta de enlace.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Agregue una subred de puerta de enlace que sea /27 o superior.
   
   > [!NOTE]
   > Si no tiene suficientes direcciones IP que se mantienen en el tamaño de subred de puerta de enlace de red virtual tooincrease hello, deberá tooadd más espacio de direcciones IP.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Guardar configuración de redes virtuales de Hola.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. Ya tiene una red virtual sin puertas de enlace. toocreate nuevas puertas de enlace y completar las conexiones, puede continuar con la [paso 4: crear una puerta de enlace de ExpressRoute](#gw), que se encuentra en hello anterior conjunto de pasos.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>puerta de enlace VPN de tooadd point-to-site configuration toohello
Puede seguir pasos de Hola por debajo de la puerta de enlace VPN de tooyour de tooadd Point-to-Site configuración en una configuración de coexistencia.

1. Agregue el grupo de direcciones de clientes de VPN.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Cargar certificado de raíz de hello VPN tooAzure para la puerta de enlace VPN. En este ejemplo, se supone que ese certificado de raíz de Hola se almacena en el equipo local Hola donde se ejecuta los siguientes cmdlets de PowerShell de Hola.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Para más información sobre la VPN de punto a sitio, consulte [Configuración de una conexión punto a sitio a una red virtual mediante PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
