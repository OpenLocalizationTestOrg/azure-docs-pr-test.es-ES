Hola heredado (antiguo) puerta de enlace VPN SKU son:

* Básica
* Estándar
* HighPerformance

Puerta de enlace de VPN no utiliza la puerta de enlace de hello UltraPerformance SKU. Para obtener información acerca de hello UltraPerformance SKU, vea hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentación.

Cuando se trabaja con Hola SKU heredadas, tenga en cuenta los siguiente hello:

* Si desea toouse un tipo de PolicyBased VPN, debe usar hello SKU básica. Las VPN PolicyBased (que anteriormente se denominaba enrutamiento estático) no se admiten en otra SKU.
* BGP no se admite en hello SKU básica.
* Coexistencia de puerta de enlace VPN de ExpressRoute no se admiten configuraciones en hello SKU básica.
* Conexiones de puerta de enlace de VPN de S2S de activo / activo pueden configurarse en hello HighPerformance SKU.
