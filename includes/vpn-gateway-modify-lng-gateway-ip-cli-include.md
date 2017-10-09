### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>puerta de enlace de la red local de hello toomodify 'gatewayIpAddress'

Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian. dirección IP de puerta de enlace de Hello puede cambiarse sin quitar una conexión de puerta de enlace VPN existente (si tiene uno). de direcciones IP de puerta de enlace de hello toomodify, reemplazar de los valores de hello 'Sitio2' y 'TestRG1' con los suyos propios usando hello [actualizar la puerta de enlace local az red](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Compruebe que la dirección IP de hello es correcta en la salida de hello:

```
"gatewayIpAddress": "23.99.222.170",
```