Debe crear una red virtual y una subred de puerta de enlace en primer lugar, antes de trabajar en hello siguiente las tareas. Vea el artículo de hello [configurar una red Virtual con el portal clásico de hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) para obtener más información.   

## <a name="add-a-gateway"></a>Adición de una puerta de enlace
Use el comando de hello debajo toocreate una puerta de enlace. Ser seguro toosubstitute todos los valores de sus propios.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Compruebe que se creó la puerta de enlace de Hola
Se ha creado el comando de Hola de uso siguiente tooverify que Hola puerta de enlace. Este comando también recupera el Id. de puerta de enlace de hello, que necesita para otras operaciones.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Cambio del tamaño de una puerta de enlace
Hay varias [SKU de puerta de enlace](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Puede usar Hola después comando toochange hello SKU de puerta de enlace en cualquier momento.

> [!IMPORTANT]
> Este comando no funciona para la puerta de enlace de UltraPerformance. toochange la puerta de enlace de puerta de enlace tooan UltraPerformance, primero quite Hola existente de la puerta de enlace ExpressRoute y, a continuación, crear una nueva puerta de enlace de UltraPerformance. toodowngrade la puerta de enlace de una puerta de enlace UltraPerformance, quite primero Hola UltraPerformance puerta de enlace y, a continuación, cree una nueva puerta de enlace. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Eliminación de una puerta de enlace
Usar comandos de hello debajo tooremove una puerta de enlace

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>