---
title: 'Conecte los dispositivos VPN basada en directivas de VPN de Azure puertas de enlace toomultiple local: Azure Resource Manager: PowerShell | Documentos de Microsoft'
description: "Este artículo le guiará a través de configuración de Azure basadas en enrutamiento puerta de enlace toomultiple basada en directivas VPN dispositivos VPN mediante el Administrador de recursos de Azure y PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>Conectar VPN de Azure puertas de enlace toomultiple local basada en directivas VPN dispositivos con PowerShell

En este artículo le ayuda a configurar un Azure basadas en enrutamiento puerta de enlace tooconnect toomultiple local basada en directivas VPN los dispositivos VPN aprovechar las directivas de IPsec/IKE personalizadas en las conexiones VPN de S2S.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>Acerca de las puertas de enlace de VPN basadas en directivas y en rutas

Directivas: *frente a* basadas en enrutamiento de los dispositivos VPN difieren en cómo se establecen los selectores de tráfico de IPsec de hello en una conexión:

* **Basada en directivas** dispositivos VPN utilizan combinaciones de Hola de prefijos de ambos toodefine redes cómo se cifra y descifra el tráfico a través de túneles de IPsec. Normalmente se basa en dispositivos de firewall que realizan el filtrado de paquetes. Descifrado y cifrado de túnel de IPsec se agregan toohello el filtrado de paquetes y el motor de procesamiento.
* **Basadas en enrutamiento** dispositivos VPN utilizan selectores de tráfico y para cualquier (comodín) y las tablas de permiten enrutamiento/reenvío túneles de IPsec toodifferent de dirigir el tráfico. Normalmente se basa en plataformas de enrutador donde cada túnel IPsec se modela como una interfaz de red o VTI (interfaz de túnel virtual).

Hello diagramas siguientes resaltan dos modelos de hello:

### <a name="policy-based-vpn-example"></a>Ejemplo de VPN basada en directivas
![basada en directivas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Ejemplo de VPN basada en rutas
![basada en rutas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Compatibilidad de Azure con VPN basada en directivas
Actualmente, Azure admite los dos modos de puertas de enlace de VPN: puertas de enlace de VPN basadas en directivas y puertas de enlace de VPN basadas en rutas. Se crean en distintas plataformas internas, lo que da lugar a diferentes especificaciones:

|                          | **Puerta de enlace de VPN PolicyBased** | **Puerta de enlace de VPN RouteBased**               |
| ---                      | ---                         | ---                                      |
| **SKU de puerta de enlace de Azure**    | Básica                       | Básica, Estándar, HighPerformance         |
| **Versión de IKE**          | IKEv1                       | IKEv2                                    |
| **Máx. de conexiones de sitio a sitio** | **1**                       | Básica o Estándar: 10<br> HighPerformance: 30 |
|                          |                             |                                          |

Con la directiva de IPsec/IKE personalizada hello, ahora puede configurar Azure basadas en enrutamiento VPN puertas de enlace toouse tráfico basado en prefijo selectores con la opción "**PolicyBasedTrafficSelectors**", tooconnect tooon local basada en directivas de los dispositivos VPN. Esta funcionalidad le permite tooconnect de red virtual de Azure y toomultiple de puerta de enlace VPN dispositivos VPN/firewall basada en directivas, quitar el límite de conexión única Hola de hello actuales Azure basada en directivas con puertas de enlace VPN local.

> [!IMPORTANT]
> 1. tooenable esta conectividad, deben admitir los dispositivos VPN basada en directivas locales **IKEv2** tooconnect toohello Azure basadas en enrutamiento puertas de enlace VPN. Compruebe las especificaciones del dispositivo VPN.
> 2. redes locales de Hello conexión a través de los dispositivos VPN basada en directivas con este mecanismo solo pueden conectar toohello red virtual de Azure; **no están en tránsito redes locales de tooother o redes virtuales a través de bienvenida la misma puerta de enlace de VPN de Azure**.
> 3. opción de configuración de Hello es parte de la directiva de conexión de IPsec/IKE personalizada hello. Si habilita la opción de selector de hello tráfico basada en directivas, debe especificar la directiva completa de hello (algoritmos de cifrado e integridad de IPsec/IKE, ventajas claves y vigencias de SA).

Hola siguiente diagrama muestra por qué el enrutamiento del tránsito a través de puerta de enlace VPN de Azure no funciona con la opción de hello basada en directivas:

![tránsito basado en directivas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Tal y como se muestra en el diagrama de hello, puerta de enlace de VPN de Azure de hello tiene selectores de tráfico de hello tooeach de red virtual de los prefijos de red local hello, pero no los prefijos de las conexiones entre Hola. Por ejemplo, el sitio local 2, sitio 3 y 4 pueden cada comunican tooVNet1 respectivamente, pero no se pueden conectar a través de hello Azure VPN gateway tooeach otros. diagrama de Hello muestra hello selectores de tráfico que no están disponibles en la puerta de enlace de VPN de Azure de hello en esta configuración de conexión cruzada.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Configuración de los selectores de tráfico basados en directivas en una conexión

Hello instrucciones de este artículo, siga Hola mismo ejemplo tal y como se describe en [directiva configurar IPsec/IKE para las conexiones de S2S o red virtual a red virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish una conexión VPN de S2S. Esto se muestra en hello siguiente diagrama:

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Hola tooenable de flujo de trabajo esta conectividad:
1. Crear red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local para la conexión entre entornos
2. Cree una directiva IPsec/IKE.
3. Aplicar la directiva de hello cuando se crea una conexión de S2S o red virtual a red virtual, y **habilitar selectores de tráfico basado en directiva de hello** en conexión Hola
4. Si ya se creó la conexión de hello, puede aplicar o actualizar la conexión existente de hello directiva tooan

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Habilitación de los selectores de tráfico basados en directivas en una conexión

Asegúrese de que ha completado [parte 3 de artículo de directiva de IPsec/IKE configurar hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) para esta sección. Hola siguiendo el ejemplo se utiliza Hola mismos parámetros y pasos:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Paso 1: crear la red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Declare las variables de & Conectar tooyour suscripción
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
Hola toouse cmdlets del Administrador de recursos, asegúrese de cambiar el modo de tooPowerShell. Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).

Abra la consola de PowerShell y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que conectarse:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Crear red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local
Hola de ejemplo siguiente crea la red virtual de hello, TestVNet1 con tres subredes y puerta de enlace VPN de Hola. Al reemplazar valores, es importante que siempre asigne el nombre "GatewaySubnet" a la subred de la puerta de enlace. Si usa otro, se produce un error al crear la puerta de enlace.

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Paso 2: Creación de una conexión VPN de sitio a sitio con una directiva IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Cree una directiva IPsec/IKE.

> [!IMPORTANT]
> Necesita una directiva de IPsec/IKE en orden tooenable "UsePolicyBasedTrafficSelectors" opción de conexión de hello toocreate.

Hello en el ejemplo siguiente se crea una directiva de IPsec/IKE con estos algoritmos y parámetros:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, vigencia de SA de 3600 segundos y 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Crear la conexión de VPN de S2S de hello en los selectores de tráfico basada en directivas y la directiva de IPsec/IKE
Crear una conexión VPN de S2S y aplicar la directiva de IPsec/IKE Hola creado en el paso anterior de Hola. Tenga en cuenta los parámetros adicionales de Hola "-UsePolicyBasedTrafficSelectors $True" lo que permite a los selectores de tráfico basada en directivas en conexión Hola.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Después de completar los pasos de hello, Hola conexión VPN S2S usará Hola directiva IPsec/IKE definida y habilitar a selectores de tráfico basada en directivas en conexión Hola. Puede repetir Hola mismo pasos tooadd más conexiones tooadditional basada en directivas VPN dispositivos locales de Hola misma puerta de enlace de VPN de Azure.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Actualización de los selectores de tráfico basados en directivas para una conexión
Hola última sección muestra cómo los selectores de tráfico basado en directiva de hello tooupdate opción para una conexión VPN de S2S existente.

### <a name="1-get-hello-connection"></a>1. Obtener la conexión de Hola
Obtener el recurso de conexión de Hola.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Hola tráfico basada en directivas selectores opción Check
Hello la línea siguiente se muestra si se utilizan los selectores de tráfico basado en directiva de Hola para conexión de hello:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Si la línea hello devuelve "**True**", a continuación, selectores de tráfico basada en directivas se configuran en la conexión de hello; en caso contrario, devuelve "**False**."

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Actualizar los selectores de tráfico basado en directiva de hello en una conexión
Una vez que obtenga el recurso de conexión de hello, puede habilitar o deshabilitar la opción de Hola.

#### <a name="disable-usepolicybasedtrafficselectors"></a>Deshabilitación de UsePolicyBasedTrafficSelectors
Hello en el ejemplo siguiente se deshabilita la opción de selectores de tráfico basada en directivas de hello, pero deja Hola sin cambios de directiva de IPsec/IKE:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>Habilitación de UsePolicyBasedTrafficSelectors
el ejemplo siguiente se Hello permite opción selectores de hello tráfico basada en directivas, pero deja Hola sin cambios de directiva de IPsec/IKE:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Pasos siguientes
Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.

Consulte también [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuración de la directiva IPsec/IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual) para obtener más información sobre las directivas IPsec/IKE personalizadas.
