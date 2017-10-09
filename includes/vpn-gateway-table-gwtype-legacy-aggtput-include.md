Hello tabla siguiente muestran tipos de puerta de enlace de Hola y el rendimiento agregado estimado Hola SKU de puerta de enlace. Esta tabla aplica toohello el Administrador de recursos y los modelos de implementación clásica. 

Los precios difieren entre las SKU de puerta de enlace. Para obtener más información, vea [Precios de VPN Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway).

Tenga en cuenta esa puerta de enlace de hello UltraPerformance que SKU no se representa en esta tabla. Para obtener información acerca de hello UltraPerformance SKU, vea hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentación.

|  | **Rendimiento de puerta de enlace VPN (1)** | **Túneles IPsec máx. de puerta de enlace VPN (2)** | **Rendimiento de puerta de enlace de ExpressRoute** | **Puerta de enlace de VPN y ExpressRoute coexisten** |
| --- | --- | --- | --- | --- |
| **SKU básica (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |No |
| **SKU estándar (4)(5)** |100 Mbps |10 |1000 Mbps |Sí |
| **SKU de alto rendimiento (4)** |200 Mbps |30 |2000 Mbps |Sí |


(1) rendimiento VPN de hello es una estimación aproximada basándose en las medidas de hello entre redes virtuales en hello misma región de Azure. No es un rendimiento garantizado para las conexiones entre entornos a través de Internet de Hola. Es la medición del rendimiento máximo posible de Hola.

(2) número de Hola de túneles, consulte tooRouteBased VPN. Una VPN basada en directivas solo puede admitir un túnel VPN de sitio a sitio.

(3) BGP no se admite para hello SKU básica.

(4) Las VPN basadas en directivas no son compatibles con esta SKU. Se admiten para hello SKU básica.

(5) Esta SKU no admite conexiones de VPN Gateway S2S activo/activo. Activo / activo es compatible con hello HighPerformance SKU.

(6) La SKU de nivel Básico está obsoleta para su uso con ExpressRoute.
