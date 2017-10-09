pasos de Hola para esta tarea, use una red virtual basan en valores Hola Hola después de la lista de referencias de configuración. En esta lista también se enumeran nombres y valores de configuración adicionales. No usamos esta lista directamente en cualquiera de los pasos de hello, aunque se agregue variables basadas en valores de hello en esta lista. Puede copiar hello toouse de lista como referencia, reemplazando los valores de hello con sus propios.

**Lista de referencia de configuración**

* Nombre de red virtual = "TestVNet"
* Espacio de direcciones de red virtual = 192.168.0.0/16
* Grupo de recursos: "TestRG"
* Nombre de subred 1 = "FrontEnd" 
* Espacio de direcciones de subred 1 = "192.168.1.0/24"
* Nombre de subred de puerta de enlace: "GatewaySubnet" (siempre debe asignar a las subredes de puerta de enlace el nombre *GatewaySubnet*).
* Espacio de direcciones de subred de puerta de enlace = "192.168.200.0/26"
* Región = "East US"
* Nombre de puerta de enlace = "GW"
* Nombre de IP de puerta de enlace = "GWIP"
* Nombre de configuración de IP de puerta de enlace = "gwipconf"
* Tipo = "ExpressRoute" (este tipo es obligatorio para una configuración de ExpressRoute).
* Nombre de IP pública de puerta de enlace = "gwpip"

## <a name="add-a-gateway"></a>Adición de una puerta de enlace
1. Conectar tooyour suscripción de Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Declare las variables para este ejercicio. Ser tooedit seguro de que desea toouse una Hola ejemplo tooreflect Hola configuración.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Almacenar objetos de red virtual de hello como una variable.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Agregue un tooyour de subred de puerta de enlace red Virtual. subred de puerta de enlace de Hello debe denominarse "GatewaySubnet". Se recomienda que cree una subred de puerta de enlace con un valor /27 o mayor (/26, /25, etc.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Establecer configuración de Hola.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Almacenar la subred de puerta de enlace de hello como una variable.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Pida una dirección IP pública. se requiere una dirección IP Hola antes de crear la puerta de enlace de Hola. No se puede especificar la dirección IP de Hola que desee toouse; se asigna dinámicamente. Usará esta dirección IP en la sección de configuración siguiente Hola. Hola AllocationMethod debe ser dinámicos.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Crear configuración de hello para la puerta de enlace. configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública. En este paso, está especificando la configuración de Hola que se usará al crear puerta de enlace de Hola. Este paso no crea objetos de puerta de enlace de Hola. Use la configuración de puerta de enlace de ejemplo de Hola a continuación toocreate.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Crear puerta de enlace de Hola. En este paso, Hola **- el GatewayType** es especialmente importante. Debe utilizar el valor de hello **ExpressRoute**. Después de ejecutar estos cmdlets, puerta de enlace de hello puede tardar 45 minutos o más toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Compruebe que se creó la puerta de enlace de Hola
Usar hello siga los comandos tooverify que Hola puerta de enlace se ha creado:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Cambio del tamaño de una puerta de enlace
Hay varias [SKU de puerta de enlace](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Puede usar Hola después comando toochange hello SKU de puerta de enlace en cualquier momento.

> [!IMPORTANT]
> Este comando no funciona para la puerta de enlace de UltraPerformance. toochange la puerta de enlace de puerta de enlace tooan UltraPerformance, primero quite Hola existente de la puerta de enlace ExpressRoute y, a continuación, crear una nueva puerta de enlace de UltraPerformance. toodowngrade la puerta de enlace de una puerta de enlace UltraPerformance, quite primero Hola UltraPerformance puerta de enlace y, a continuación, cree una nueva puerta de enlace.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Eliminación de una puerta de enlace
Usar hello después tooremove una puerta de enlace de comando:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```