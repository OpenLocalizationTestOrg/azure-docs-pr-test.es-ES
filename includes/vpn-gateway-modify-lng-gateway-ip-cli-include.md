### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="3cb9c-101">puerta de enlace de la red local de hello toomodify 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="3cb9c-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="3cb9c-102">Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="3cb9c-103">dirección IP de puerta de enlace de Hello puede cambiarse sin quitar una conexión de puerta de enlace VPN existente (si tiene uno).</span><span class="sxs-lookup"><span data-stu-id="3cb9c-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="3cb9c-104">de direcciones IP de puerta de enlace de hello toomodify, reemplazar de los valores de hello 'Sitio2' y 'TestRG1' con los suyos propios usando hello [actualizar la puerta de enlace local az red](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="3cb9c-105">Compruebe que la dirección IP de hello es correcta en la salida de hello:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```