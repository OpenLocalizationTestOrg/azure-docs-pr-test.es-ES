### <a name="noconnection"></a>prefijos de direcciones en la IP de la puerta de enlace de red local toomodify - no hay ninguna conexión de puerta de enlace

Si no dispone de una conexión de puerta de enlace y desea tooadd o quitar los prefijos de direcciones IP, puede seguir Hola mismo comando que usar puerta de enlace de red local de hello toocreate, [crear az red local puerta de enlace](https://docs.microsoft.com/cli/azure/network/local-gateway#create). También puede usar esta dirección IP de puerta de enlace de comando tooupdate hello de dispositivo VPN de Hola. configuración actual de toooverwrite hello, use nombre existente de hello de la puerta de enlace de red local. Si utiliza un nombre diferente, puede crear una nueva puerta de enlace de red local, en lugar de sobrescribir Hola uno ya existente.

Se debe especificar cada vez que realice un cambio, una lista completa de Hola de prefijos, hello no solo agrega el prefijo que desea toochange. Especifique solo los prefijos de Hola que desea tookeep. En este caso, 10.0.0.0/24 y 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify red local puerta de enlace prefijos de direcciones IP: conexión de puerta de enlace existente

Si tiene una conexión de puerta de enlace y desea tooadd o quita los prefijos de direcciones IP, puede actualizar los prefijos de hello mediante [actualizar la puerta de enlace local az red](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Esto tendrá como resultado un tiempo de inactividad para la conexión VPN. Al modificar la dirección IP de hello prefijos, no es necesario puerta de enlace VPN toodelete Hola.

Se debe especificar cada vez que realice un cambio, una lista completa de Hola de prefijos, hello no solo agrega el prefijo que desea toochange. En este ejemplo, 10.0.0.0/24 y 20.0.0.0/24 ya están presentes. Se agregue Hola prefijos 30.0.0.0/24 y 40.0.0.0/24 y especifique todos los 4 de prefijos de hello al actualizar.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```