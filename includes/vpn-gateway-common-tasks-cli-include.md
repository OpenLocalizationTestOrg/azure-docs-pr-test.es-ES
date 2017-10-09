### <a name="tooview-local-network-gateways"></a>puertas de enlace de red local de tooview

tooview una lista de puertas de enlace de la red local de hello, use hello [lista de puerta de enlace local de red az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>Hola tooverify comparten valores de clave

Compruebe que el valor de clave de hello compartido es Hola mismo valor que utilizó para la configuración del dispositivo VPN. Si no es así, ejecute conexión Hola utilizando de nuevo valor de hello de dispositivo de Hola o actualizar dispositivo Hola con el valor de Hola de hello devuelto. Hola valores deben coincidir. Hola tooview compartido clave, use hello [lista de conexiones vpn de red az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>puerta de enlace VPN de hello tooview dirección IP pública

dirección IP toofind Hola pública de la puerta de enlace de red virtual, use hello [lista de ip pública de red az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando. Para facilitar la lectura, la salida de hello en este ejemplo es la lista de Hola de toodisplay con formato de direcciones IP públicas en formato de tabla.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
