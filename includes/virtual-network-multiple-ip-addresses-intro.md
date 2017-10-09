> [!div class="op_single_selector"]
> * [Portal](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Plantilla](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Una máquina Virtual (VM) de Azure tiene uno o más interfaces de red (NIC) conectados tooit. Una NIC puede tener uno o más estática o dinámica IP pública y privada direcciones tooit asignado. Asignar varias IP direcciones tooa VM permite Hola siguientes capacidades:

* Hospede varios sitios web o servicios con direcciones IP y certificados SSL diferentes en un único servidor.
* Actúe como aplicación de red virtual, como un firewall o equilibrador de carga.
* Hola tooadd capacidad cualquiera de IP privada Hola direcciones para cualquiera de hello NIC tooan grupo back-end de equilibrador de carga de Azure. Hola más allá, solo Hola dirección IP principal para hello que NIC principal podría ser agregado grupo back-end de tooa. toolearn Obtenga más información sobre cómo tooload equilibrar varias configuraciones de IP, lee hello [varias configuraciones de IP de equilibrio de carga](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.

Cada tooa NIC conectada VM tiene uno o más configuraciones de IP asociados tooit. Se asigna a cada configuración una dirección IP privada estática o dinámica. Cada configuración puede tener también un tooit de asociado de recurso de dirección IP pública. Un recurso de dirección IP público tiene ya sea un dinámico o estático público IP dirección asignada tooit. direcciones toolearn más información acerca de IP en Azure, lea hello [direcciones IP en Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) artículo. 

Hay un límite toohow IP privada muchas direcciones se pueden asignar tooa equipo NIC. También hay un límite toohow muchas direcciones IP públicas que pueden usarse en una suscripción de Azure. Vea hello [Azure tiene una limitación](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artículo para obtener más información.
