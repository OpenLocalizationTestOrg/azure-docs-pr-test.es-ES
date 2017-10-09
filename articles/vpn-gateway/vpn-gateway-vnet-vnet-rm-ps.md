---
title: 'Conectar una red virtual de red virtual de Azure tooanother: PowerShell | Documentos de Microsoft'
description: "Este artículo le guiará para conectar redes virtuales entre sí por medio de PowerShell y el Administrador de recursos de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Configuración de una conexión de VPN Gateway de red virtual a red virtual mediante PowerShell

Este artículo muestra cómo toocreate una conexión de puerta de enlace VPN entre redes virtuales. Hello redes virtuales pueden estar en Hola mismo o en distintas regiones y de Hola iguales o distintas suscripciones. Al conectar redes virtuales de distintas suscripciones, las suscripciones de hello no es necesario toobe asociada Hola a mismo inquilino de Active Directory. 

pasos de Hello en este artículo aplican el modelo de implementación del Administrador de recursos de toohello y usan PowerShell. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI de Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conexión de diferentes modelos de implementación - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conexión de diferentes modelos de implementación - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE. Si sus redes virtuales están en hello misma región, puede que desee tooconsider conectándolos mediante el intercambio de tráfico de red virtual. El emparejamiento de VNET no usa VPN Gateway. Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).

Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios. Esto le permite establecer topologías de red que combinen la conectividad entre entornos con conectividad entre redes virtuales, como se muestra en hello siguiente diagrama:

![Acerca de las conexiones](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>¿Por qué debería conectarse a redes virtuales?

Puede que desee tooconnect las redes virtuales para hello siguientes motivos:

* **Presencia geográfica y redundancia geográfica entre regiones**

  * Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.
  * Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure. Por ejemplo, puede tooset seguridad SQL Always On con grupos de disponibilidad a través de varias regiones de Azure.
* **Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**

  * Hola dentro mismo región, puede configurar aplicaciones de varios niveles con varias redes virtuales conectadas entre sí debido tooisolation o requisitos administrativos.

Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo.

## <a name="which-set-of-steps-should-i-use"></a>¿Qué serie de pasos debo seguir?

En este artículo, verá dos conjuntos de pasos diferentes. Un conjunto de pasos para [redes virtuales que residen en Hola misma suscripción](#samesub)y otro para [redes virtuales que residen en distintas suscripciones](#difsub). Hello diferencia clave entre conjuntos de hello es si puede crear y configurar todos los recursos de red y puerta de enlace virtuales dentro de hello misma sesión de PowerShell.

Hello pasos de este artículo utilizan variables que se declaran en principio Hola de cada sección. Si ya está trabajando con redes virtuales existentes, modificar la configuración de Hola de hello variables tooreflect en su propio entorno. Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>¿Cómo tooconnect redes virtuales que están en hello misma suscripción

![diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Antes de empezar

Antes de comenzar, necesita la versión más reciente de tooinstall Hola Hola Azure Resource Manager de cmdlets de PowerShell, por lo menos 4.0 o posteriores. Para obtener más información acerca de cómo instalar los cmdlets de PowerShell de hello, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Paso 1: Planeamiento de los intervalos de direcciones IP

Hola pasos, se crea dos redes virtuales junto con sus subredes correspondientes de la puerta de enlace y las configuraciones. Creamos, a continuación, una conexión VPN entre Hola dos redes virtuales. Es importante tooplan intervalos de direcciones IP de hello para la configuración de red. Tenga en cuenta que hay que asegurarse de que ninguno de los intervalos de VNet o intervalos de red local se solapen. En estos ejemplos, no se incluye ningún servidor DNS. Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Utilizamos Hola después los valores en los ejemplos de hello:

**Valores para TestVNet1:**

* Nombre de red virtual: TestVNet1
* Grupo de recursos: TestRG1
* Ubicación: Este de EE. UU.
* TestVNet1: 10.11.0.0/16 y 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* Backend: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Dirección IP pública: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valores para TestVNet4:**

* Nombre de red virtual: TestVNet4
* TestVNet2: 10.41.0.0/16 y 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* Backend: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupo de recursos: TestRG4
* Ubicación: Oeste de EE. UU.
* GatewayName: VNet4GW
* Dirección IP pública: VNet4GWIP
* VPNType: RouteBased
* Conexión: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Paso 2: Creación y configuración de TestVNet1

1. Declare las variables. Este ejemplo declara las variables de hello con valores de hello para este ejercicio. En la mayoría de los casos, debe reemplazar los valores de hello por los suyos propios. Sin embargo, puede utilizar estas variables si está ejecutando a través de hello pasos toobecome familiarizado con este tipo de configuración. Modificar variables de hello si es necesario, a continuación, copie y péguelos en la consola de PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Conectarse a tooyour cuenta. Usar hello después toohelp de ejemplo que se conecta:

  ```powershell
  Login-AzureRmAccount
  ```

  Compruebe las suscripciones de hello para la cuenta de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Especifique que desea toouse de suscripción de Hola.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Cree un nuevo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Crear configuraciones de subred para TestVNet1 de Hola. En este ejemplo se crea una red virtual denominada TestVNet1 y tres subredes llamadas: GatewaySubnet, FrontEnd y Backend. Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace. Si usa otro, se produce un error al crear la puerta de enlace.

  Hello en el ejemplo siguiente se usa variables de hello establecidas anteriormente. En este ejemplo, la subred de puerta de enlace de hello está usando un /27. Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluye direcciones más si se selecciona al menos /28 o /27. Esto le permitirá suficientes direcciones tooaccommodate posibles configuraciones adicionales que puede querer en hello futuras.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Cree TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Solicitar una pública dirección toobe toohello asignado puerta de enlace IP que creará para la red virtual. Tenga en cuenta que hello AllocationMethod es dinámico. No se puede especificar la dirección IP de Hola que desee toouse. Es puerta de enlace de tooyour asignada dinámicamente. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Crear configuración de puerta de enlace de Hola. configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública. Use la configuración de puerta de enlace de toocreate de ejemplo de Hola.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Crear puerta de enlace de Hola para TestVNet1. En este paso, creará la puerta de enlace de red virtual de Hola para su TestVNet1. Las configuraciones VNet a VNet requieren un VpnType RouteBased. Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello seleccionado SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Paso 3: Creación y configuración de TestVNet4

Una vez que haya configurado TestVNet1, cree TestVNet4. Siga los pasos de hello siguiente, reemplazando los valores de hello con su propio cuando sea necesario. Este paso puede realizarse en hello misma sesión de PowerShell porque está en Hola misma suscripción.

1. Declare las variables. Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Cree un nuevo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Crear configuraciones de subred para TestVNet4 de Hola.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Cree TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Pida una dirección IP pública.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Crear configuración de puerta de enlace de Hola.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Crear puerta de enlace de hello TestVNet4. Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello seleccionado SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Paso 4: crear conexiones de Hola

1. Obtenga ambas puertas de enlace de red virtual. Si ambos de puertas de enlace de hello están en hello misma suscripción, tal como están en el ejemplo de Hola, puede completar este paso en hello misma sesión de PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Crear hello TestVNet1 tooTestVNet4 conexión. En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet4. Verá una clave compartida que se hace referencia en los ejemplos de hello. Puede utilizar sus propios valores de clave compartida de Hola. Hola importante que es esa clave compartida de hello debe coincidir en las dos conexiones. Crear una conexión puede tardar un poco al toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Crear hello TestVNet4 tooTestVNet1 conexión. Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet4 tooTestVNet1. Asegúrese de que coincide con las claves de hello compartido. se establecerá la conexión de Hello después de unos minutos.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Compruebe la conexión. Consulte la sección de hello [cómo tooverify la conexión](#verify).

## <a name="difsub"></a>¿Cómo tooconnect redes virtuales que se encuentran en distintas suscripciones

![diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

En este escenario, conectaremos TestVNet1 y TestVNet5. TestVNet1 y TestVNet5 residen en suscripciones diferentes. las suscripciones de Hello no es necesario toobe asociado con hello mismo inquilino de Active Directory. diferencia de Hello entre estos pasos y el conjunto anterior de hello es que algunos de los pasos de configuración de Hola necesitan toobe realizada en una sesión de PowerShell independiente en el contexto de Hola de suscripción segundo Hola. Sobre todo cuando las suscripciones de hello dos pertenecen toodifferent organizaciones.

### <a name="step-5---create-and-configure-testvnet1"></a>Paso 5: Creación y configuración de TestVNet1

Debe completar [paso 1](#Step1) y [paso 2](#Step2) de hello anterior sección toocreate y configurar TestVNet1 Hola puerta de enlace VPN para TestVNet1. Para esta configuración, no es necesario toocreate TestVNet4 desde la sección anterior de hello, aunque si lo creó, no estará en conflicto con estos pasos. Cuando haya completado los pasos 1 y 2 de paso, continúe con el paso 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Paso 6: comprobar los intervalos de direcciones IP de Hola

Es importante toomake seguro de que el espacio de direcciones IP de Hola de hello nueva red virtual, TestVNet5, no se superponen con ninguno de los intervalos de VNet o intervalos de puerta de enlace de red local. En este ejemplo, las redes virtuales Hola pueden pertenecer toodifferent organizaciones. Para este ejercicio, puede usar Hola después de valores de hello TestVNet5:

**Valores para TestVNet5:**

* Nombre de red virtual: TestVNet5
* Grupo de recursos: TestRG5
* Ubicación: Japón Oriental
* TestVNet5: 10.51.0.0/16 y 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* Backend: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Dirección IP pública: VNet5GWIP
* VPNType: RouteBased
* Conexión: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Paso 7: Creación y configuración de TestVNet5

Este paso debe realizarse en el contexto de Hola de suscripción nueva Hola. Administrador de hello en otra organización que posee la suscripción de hello puede realizar esta parte.

1. Declare las variables. Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Conectar toosubscription 5. Abra la consola de PowerShell y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que conectarse:

  ```powershell
  Login-AzureRmAccount
  ```

  Compruebe las suscripciones de hello para la cuenta de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Especifique que desea toouse de suscripción de Hola.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Cree un nuevo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Crear configuraciones de subred para TestVNet5 de Hola.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Cree TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Pida una dirección IP pública.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Crear configuración de puerta de enlace de Hola.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Crear puerta de enlace de hello TestVNet5.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Paso 8: crear conexiones de Hola

En este ejemplo, dado que las puertas de enlace de hello están en distintas suscripciones hello, hemos dividiremos este paso en dos sesiones de PowerShell marcadas como [suscripción 1] y [suscripción 5].

1. **[Suscripción 1]**  Obtener puerta de enlace de red virtual de hello para la suscripción: 1. Inicie sesión y conectar tooSubscription 1 antes de ejecutar el siguiente ejemplo de Hola:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Copiar el resultado de hello de hello siguientes elementos y enviar estos administrador toohello de 5 de la suscripción a través de correo electrónico u otro método.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Estos dos elementos tendrán valores toohello similar después de la salida de ejemplo:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Suscripción 5]**  Obtener puerta de enlace de red virtual de Hola para 5 de suscripción. Inicie sesión y conectar tooSubscription 5 antes de ejecutar el siguiente ejemplo de Hola:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Copiar el resultado de hello de hello siguientes elementos y enviar estos administrador toohello de suscripción: 1 a través de correo electrónico u otro método.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Estos dos elementos tendrán valores toohello similar después de la salida de ejemplo:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Suscripción 1]**  Crear conexión hello TestVNet1 tooTestVNet5. En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet5. Hola diferencia es que vnet5gw $ no se puede obtener directamente porque está en una suscripción diferente. Deberá toocreate un nuevo objeto de PowerShell con valores de hello comunicado entre el 1 de suscripción en hello los pasos descritos anteriormente. Utilice el siguiente ejemplo de Hola. Reemplace Hola nombre, identificador y una clave compartida con sus propios valores. Hola importante que es esa clave compartida de hello debe coincidir en las dos conexiones. Crear una conexión puede tardar un poco al toocomplete.

  Conectar tooSubscription 1 antes de ejecutar el siguiente ejemplo de Hola:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Suscripción 5]**  Crear conexión hello TestVNet5 tooTestVNet1. Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet5 tooTestVNet1. Hola mismo proceso de creación de un objeto de PowerShell basado en valores de hello obtenidos en el 1 de la suscripción es válida aquí también. En este paso, asegúrese de que coinciden con las claves de hello compartido.

  Conectar tooSubscription 5 antes de ejecutar el siguiente ejemplo de Hola:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>¿Cómo tooverify una conexión

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>P+F sobre conexiones de red virtual a red virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes

* Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Vea hello [documentación de máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obtener más información.
* Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
