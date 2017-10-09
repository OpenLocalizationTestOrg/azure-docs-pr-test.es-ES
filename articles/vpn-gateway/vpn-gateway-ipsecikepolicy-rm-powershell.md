---
title: 'Configurar una directiva de IPsec o IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual: Azure Resource Manager: PowerShell | Microsoft Docs'
description: "Este artículo le guiará a la hora de configurar una directiva de IPsec o IKE para conexiones de sitio a sitio o de red virtual a red virtual con puertas de enlace de VPN de Azure mediante Azure Resource Manager y PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>Configurar una directiva de IPsec o IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual

Este artículo le guiará a través de hello pasos tooconfigure directiva IPsec/IKE para las conexiones VPN de sitio a sitio o red virtual a red virtual con el modelo de implementación del Administrador de recursos de Hola y PowerShell.

## <a name="about"></a>Acerca de los parámetros de la directiva de IPsec e IKE para Azure VPN gateway
El protocolo IPsec e IKE estándar admite una gran variedad de algoritmos criptográficos en diversas combinaciones. Consulte demasiado[sobre los requisitos cifrados y las puertas de enlace de VPN de Azure](vpn-gateway-about-compliance-crypto.md) toosee cómo esto puede ayudar a garantizar la conectividad de red virtual a red virtual y entre entornos satisface sus requisitos de cumplimiento o seguridad.

Este artículo proporciona instrucciones toocreate y configurar una directiva de IPsec/IKE y aplicar la conexión nueva o existente de tooa:

* [Parte 1 - toocreate de flujo de trabajo y establecer una directiva de IPsec/IKE](#workflow)
* [Parte 2: algoritmos criptográficos y niveles de clave admitidos](#params)
* [Parte 3: crear una conexión VPN de sitio a sitio con una directiva de IPsec o IKE](#crossprem)
* [Parte 4: crear una conexión de red virtual a red virtual con una directiva de IPsec o IKE](#vnet2vnet)
* [Parte 5: administrar (crear, agregar, quitar) una directiva de IPsec o IKE para una conexión](#managepolicy)

> [!IMPORTANT]
> 1. Tenga en cuenta que la directiva IPsec/IKE solo funciona en hello siguiendo las SKU de puerta de enlace:
>    * ***VpnGw1, VpnGw2, VpnGw3*** (basadas en enrutamiento)
>    * ***Standard*** y ***HighPerformance*** (basadas en enrutamiento)
> 2. Solo se puede especificar ***una*** combinación de directivas para una conexión dada.
> 3. Es preciso especificar todos los algoritmos y parámetros de IKE (modo principal) e IPsec (modo rápido). No se permite la especificación de una directiva parcial.
> 4. Consulte las especificaciones de proveedor de dispositivo VPN directiva de Hola de tooensure es compatible con los dispositivos VPN local. S2S o las conexiones de red virtual a red virtual no se pueden establecer si las directivas de hello son incompatibles.

## <a name ="workflow"></a>Parte 1 - toocreate de flujo de trabajo y establecer una directiva de IPsec/IKE
En esta sección describe el flujo de trabajo de Hola a toocreate y actualización de la directiva de IPsec/IKE con el en una conexión VPN S2S o red virtual a red virtual:
1. Crear una red virtual y una puerta de enlace de VPN
2. Crear una puerta de enlace de red local para la conexión entre locales, u otra red virtual y puerta de enlace para la conexión de red virtual a red virtual
3. Crear una directiva de IPsec o IKE con los algoritmos y parámetros seleccionados
4. Crear una conexión (VNet2VNet o IPsec) con la directiva de IPsec/IKE Hola
5. Agregar, actualizar o quitar una directiva de IPsec o IKE para una conexión existente

instrucciones de Hello en este artículo le ayuda a instalar y configurar las directivas de IPsec/IKE tal y como se muestra en el diagrama de hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Parte 2: algoritmos criptográficos y niveles de clave admitidos

Hello tabla siguiente enumeran Hola admitido los algoritmos criptográficos y ventajas claves configurables por los clientes de hello:

| **IPsec o IKEv2**  | **Opciones**    |
| ---  | --- 
| Cifrado IKEv2 | AES256, AES192, AES128, DES3, DES  
| Integridad de IKEv2  | SHA384, SHA256, SHA1, MD5  |
| Grupo DH         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, No |
| Cifrado IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, No    |
| Integridad de IPsec  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| Grupo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, No 
| Vigencia de SA QM   | (**Opcional**: Se usan los valores predeterminados si no se especifica ningún valor)<br>Segundos (entero; **mín. 300**/predeterminado 27000 segundos)<br>KBytes (entero; **mín. 1024**/predeterminado 102400000 KBytes)   |
| Selector de tráfico | UsePolicyBasedTrafficSelectors** ($True/$False; **Opcional**, valor predeterminado $False si no se especifica)    |
|  |  |

> [!IMPORTANT]
> 1. **Si GCMAES se utiliza para el algoritmo de cifrado de IPsec, debe seleccionar Hola mismo algoritmo GCMAES y longitud de clave para la integridad de IPsec; Por ejemplo, si se usa GCMAES128 para ambos**
> 2. Duración de la SA de modo principal IKEv2 se fija en 28.800 segundos en puertas de enlace de VPN de Azure Hola
> 3. Establecer "UsePolicyBasedTrafficSelectors" demasiado$ True en una conexión se configurará Hola VPN de Azure puerta de enlace tooconnect toopolicy firewall basado en VPN local. Si habilita PolicyBasedTrafficSelectors, deberá tooensure que el dispositivo VPN tiene los selectores de tráfico coincidente Hola definidos con todas las combinaciones de los prefijos de (puerta de enlace de red local) de la red local de prefijos de red virtual de Azure de hello, en lugar de-hacia cualquier. Por ejemplo, si los prefijos de red local son 10.1.0.0/16 y 10.2.0.0/16 y los prefijos de red virtual son 192.168.0.0/16 y 172.16.0.0/16, necesita hello toospecify siguiendo los selectores de tráfico:
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

Para obtener más información sobre los selectores de tráfico basados en directivas, consulte [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) (Conectar varios dispositivos VPN basados en directivas locales).

Hola tabla siguiente se muestran Hola correspondientes grupos Diffie-Hellman admitidos por la directiva personalizada de hello:

| **Grupo Diffie-Hellman**  | **Grupo DH**              | **Grupo PFS** | **Longitud de clave** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | MODP de 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP de 1024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP de 2048 bits  |
| 19                        | ECP256                   | ECP256       | ECP de 256 bits    |
| 20 |                        | ECP384                   | ECP284       | ECP de 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP de 2048 bits  |

Consulte demasiado[RFC3526](https://tools.ietf.org/html/rfc3526) y [RFC5114](https://tools.ietf.org/html/rfc5114) para obtener más detalles.

## <a name ="crossprem"></a>Parte 3: crear una conexión VPN de sitio a sitio con una directiva de IPsec o IKE

En esta sección le guiará por los pasos de Hola de creación de una conexión VPN de S2S con una directiva de IPsec/IKE. Hello pasos siguientes crean Hola conexión tal y como se muestra en el diagrama de hello:

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Consulte [Creación de una conexión VPN de sitio a sitio](vpn-gateway-create-site-to-site-rm-powershell.md) para obtener instrucciones detalladas sobre cómo crear una conexión VPN de sitio a sitio.

### <a name="before"></a>Antes de empezar

* Compruebe que tiene una suscripción a Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instalar cmdlets de PowerShell del Administrador de recursos de Azure de Hola. Vea [información general de Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.

### <a name="createvnet1"></a>Paso 1: crear la red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local

#### <a name="1-declare-your-variables"></a>1. Declaración de las variables

Para este ejercicio, se empieza por declarar las variables. Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción.

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Conectar tooyour suscripción y crear un nuevo grupo de recursos

Asegúrese de que cambie hello toouse de modo tooPowerShell cmdlets del Administrador de recursos. Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).

Abra la consola de PowerShell y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que conectarse:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Crear red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local

Hola según muestra crea la red virtual de hello, TestVNet1, con tres subredes y puerta de enlace VPN de Hola. Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace. Si usa otro, se produce un error al crear la puerta de enlace.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="s2sconnection"></a>Paso 2: Creación de una conexión VPN de sitio a sitio con una directiva IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Cree una directiva IPsec/IKE.

Hola siguiente secuencia de comandos de ejemplo crea una directiva de IPsec/IKE con hello siguientes algoritmos y parámetros:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, vigencia de SA de 7200 segundos y 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

Si usas GCMAES para IPsec, debe utilizar Hola mismo algoritmo GCMAES y longitud de clave para el cifrado de IPsec y la integridad, por ejemplo:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, vigencia de SA de 7200 segundos y 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. Crear la conexión de VPN de S2S de hello con hello directiva IPsec/IKE

Crear una conexión VPN de S2S y aplicar la directiva de IPsec/IKE Hola creado anteriormente.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Opcionalmente, puede agregar "-UsePolicyBasedTrafficSelectors $True" toohello crear conexión cmdlet tooenable VPN de Azure puerta de enlace tooconnect toopolicy dispositivos basados en VPN local, como se describió anteriormente.

> [!IMPORTANT]
> Una vez que una directiva de IPsec/IKE se especifica en una conexión, puerta de enlace de VPN de Azure de hello sólo enviará o Aceptar la propuesta de IPsec/IKE Hola con algoritmos criptográficos especificados y ventajas claves de esa conexión en particular. Asegúrese de que el dispositivo VPN local para la conexión de hello usa o acepta la combinación de la directiva exacta de hello, en caso contrario, no se establecerá el túnel de VPN de S2S de Hola.


## <a name ="vnet2vnet"></a>Parte 4: crear una conexión de red virtual a red virtual con una directiva de IPsec o IKE

pasos de Hola de creación de una conexión de red virtual a red virtual con una directiva de IPsec/IKE son similar toothat de una conexión VPN de S2S. Hello secuencias de comandos de ejemplo siguientes crean Hola conexión tal y como se muestra en el diagrama de hello:

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Consulte [Creación de una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md) para conocer los pasos detallados para crear una conexión de red virtual a red virtual. Debe completar [parte 3](#crossprem) toocreate TestVNet1 y configurar Hola puerta de enlace VPN.

### <a name="createvnet2"></a>Paso 1: crear la segunda red virtual de Hola y puerta de enlace VPN

#### <a name="1-declare-your-variables"></a>1. Declaración de las variables

Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Crear la segunda red virtual de Hola y puerta de enlace VPN en el nuevo grupo de recursos Hola

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>Paso 2: crear una conexión de red virtual toVNet con hello directiva IPsec/IKE

Toohello similar conexión VPN S2S, cree una directiva de IPsec/IKE, a continuación, se aplican toopolicy toohello nueva conexión.

#### <a name="1-create-an-ipsecike-policy"></a>1. Cree una directiva IPsec/IKE.

Hola siguiente secuencia de comandos de ejemplo crea una directiva de IPsec/IKE diferente con hello siguientes algoritmos y parámetros:
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, vigencia de SA de 7200 segundos y 4096 KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. Crear conexiones de red virtual a red virtual con hello directiva IPsec/IKE

Crear una conexión de red virtual a red virtual y aplicar directivas de IPsec/IKE de Hola que ha creado. En este ejemplo, las puertas de enlace se encuentran en hello misma suscripción. Por lo que es posible toocreate y configurar las conexiones con Hola misma directiva de IPsec/IKE Hola misma sesión de PowerShell.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> Una vez que una directiva de IPsec/IKE se especifica en una conexión, puerta de enlace de VPN de Azure de hello sólo enviará o Aceptar la propuesta de IPsec/IKE Hola con algoritmos criptográficos especificados y ventajas claves de esa conexión en particular. Asegúrese de hello seguro de las directivas IPsec para las conexiones son Hola mismo, en caso contrario, no se establecerá la conexión de red virtual a red virtual.

Después de completar estos pasos, se establece la conexión de hello en unos minutos y, tendrá Hola siguiendo la topología de red tal y como se muestra en el principio de hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Parte 5: actualizar una directiva de IPsec o IKE para una conexión

Hola última sección muestra cómo toomanage directiva IPsec/IKE para una conexión de S2S o red virtual a red virtual existente. ejercicio Hola siguiente le guiará por las siguientes operaciones en una conexión de Hola:

1. Mostrar directiva de IPsec/IKE Hola de una conexión
2. Agregar o actualizar la conexión de tooa de directiva de IPsec/IKE Hola
3. Quitar la directiva de IPsec/IKE de Hola de una conexión

Hello mismos pasos aplican tooboth S2S y conexiones de red virtual a red virtual.

> [!IMPORTANT]
> La directiva de IPsec o IKE solo se admite en las puertas de enlace de VPN basadas en rutas *Standard* y *HighPerformance*. No funciona en la puerta de enlace de hello básico SKU o puerta de enlace VPN basada en directivas de Hola.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Mostrar directiva de IPsec/IKE Hola de una conexión

Hola de ejemplo siguiente muestra cómo tooget Hola configurado en una conexión de directiva de IPsec/IKE. las secuencias de comandos de Hello seguir de ejercicios de hello anteriores.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

último comando de Hello enumera directiva IPsec/IKE actual Hola configurado en conexión hello, si hay alguno. Después de la salida de ejemplo de Hola es por conexión hello:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

Si no hay ninguna directiva de IPsec/IKE configurada, Hola comando (PS > $connection6.policy) obtiene vacío devuelto. No significa IPsec/IKE no está configurado en la conexión de hello, pero que no hay ninguna directiva de IPsec/IKE personalizada. conexión real de Hello usa directiva predeterminada de hello negociado entre el dispositivo VPN en local y Hola puerta de enlace VPN de Azure.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Agregar o actualizar una directiva de IPsec o IKE para una conexión

Hola pasos tooadd una nueva directiva o actualización de una directiva existente en una conexión son Hola mismo: crear una nueva directiva, a continuación, aplicar la nueva conexión de toohello directiva Hola.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable "UsePolicyBasedTrafficSelectors" al conectar tooan locales dispositivo VPN basada en directivas, agregar Hola "-UsePolicyBaseTrafficSelectors" parámetro toohello cmdlet, o establézcala demasiado opción Hola de $ toodisable False:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

Puede obtener la conexión de hello nuevo toocheck si se actualiza la directiva de Hola.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Debería ver resultados de Hola desde la última línea hello, como se muestra en el siguiente ejemplo de Hola:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Eliminar una directiva de IPsec o IKE de una conexión

Una vez que quita la directiva personalizada de Hola desde una conexión, puerta de enlace de VPN de Azure de hello vuelve atrás toohello [lista predeterminada de las propuestas de IPsec/IKE](vpn-gateway-about-vpn-devices.md) y vuelve a negociar nuevo con el dispositivo VPN local.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

Puede usar Hola mismo toocheck de secuencia de comandos si se ha quitado la directiva de Hola de conexión de Hola.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre los selectores de tráfico basados en directivas, vea [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) (Conectar varios dispositivos VPN basados en directivas locales).

Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.
