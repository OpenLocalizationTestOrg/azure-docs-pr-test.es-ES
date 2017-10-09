### <a name="noconnection"></a>prefijos de direcciones en la IP de la puerta de enlace de red local toomodify - no hay ninguna conexión de puerta de enlace

prefijos de dirección adicional tooadd:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

prefijos de direcciones de tooremove:<br>
Omitir los prefijos de Hola que ya no necesite. En este ejemplo, ya no necesitamos prefijo 20.0.0.0/24 (de ejemplo de Hola anterior), por lo que se actualice la puerta de enlace de red local de hello, sin incluir ese prefijo.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify red local puerta de enlace prefijos de direcciones IP: conexión de puerta de enlace existente

Si tiene una conexión de puerta de enlace y desea tooadd o quitar prefijos de direcciones IP de hello contenidos en la puerta de enlace de red local, deberá hello toodo siguiendo los pasos en orden. Esto tendrá como resultado un tiempo de inactividad para la conexión VPN. Cuando se modifica prefijos de direcciones IP, no es necesario puerta de enlace VPN toodelete Hola. Solo necesita conexión de hello tooremove.


1. Quitar conexión de Hola.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Modifique los prefijos de direcciones de hello para la puerta de enlace de red local.
   
  Establecer variable de Hola para hello LocalNetworkGateway.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Modifique los prefijos de Hola.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Crear conexiones de Hola. En este ejemplo, vamos a configurar un tipo de conexión de IPsec. Cuando se vuelve a crear la conexión, use el tipo de conexión de Hola que se especifica para la configuración. Para los tipos de conexión adicionales, vea hello [cmdlet de PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.
   
  Establecer variable de Hola para hello VirtualNetworkGateway.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Crear conexiones de Hola. Este ejemplo utiliza la variable de hello $local que establece en el paso 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```