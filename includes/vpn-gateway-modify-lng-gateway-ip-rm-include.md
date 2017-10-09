### <a name="gwipnoconnection"></a>puerta de enlace de la red local de hello toomodify 'GatewayIpAddress': no hay ninguna conexión de puerta de enlace

Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian. Utilice toomodify de ejemplo de Hola una puerta de enlace de red local que no tiene una conexión de puerta de enlace.

Cuando se modifica este valor, también puede modificar los prefijos de direcciones de hello en hello mismo tiempo. Ser seguro toouse Hola existente nombre de la puerta de enlace de red local en la configuración actual de orden toooverwrite Hola. Si utiliza un nombre diferente, puede crear una nueva puerta de enlace de red local, en lugar de sobrescribir Hola uno ya existente.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>puerta de enlace de la red local de hello toomodify 'GatewayIpAddress' - conexión de puerta de enlace existente

Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian. Si la puerta de enlace ya existe una conexión, primero debe conexión de hello tooremove. Después de quita la conexión de hello, puede modificar la dirección IP de puerta de enlace de Hola y volver a crear una nueva conexión. También puede modificar los prefijos de direcciones de hello en hello mismo tiempo. Esto tendrá como resultado un tiempo de inactividad para la conexión VPN. Cuando se modifica la dirección IP de puerta de enlace de hello, no necesita la puerta de enlace VPN toodelete Hola. Solo necesita conexión de hello tooremove.
 

1. Quitar conexión de Hola. Puede encontrar Hola nombre de la conexión mediante el cmdlet de hello 'Get-AzureRmVirtualNetworkGatewayConnection'.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Modifique el valor de 'GatewayIpAddress' hello. También puede modificar los prefijos de direcciones de hello en hello mismo tiempo. Ser seguro toouse Hola existente nombre de la configuración actual de red local puerta de enlace toooverwrite Hola. Si no lo hace, puede crear una nueva puerta de enlace de red local, en lugar de sobrescribir Hola uno ya existente.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Crear conexiones de Hola. En este ejemplo, vamos a configurar un tipo de conexión de IPsec. Cuando se vuelve a crear la conexión, use el tipo de conexión de Hola que se especifica para la configuración. Para los tipos de conexión adicionales, vea hello [cmdlet de PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.  nombre de tooobtain hello VirtualNetworkGateway, puede ejecutar hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.
   
    Establecer variables de Hola.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Crear conexiones de Hola.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```