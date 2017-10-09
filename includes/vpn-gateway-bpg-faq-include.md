### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>¿Se admite BGP en todas las SKU de Azure VPN Gateway?
No, BGP se admite en las puertas de enlace de VPN de Azure **Standard** y **HighPerformance**. **Basic** NO se admite.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>¿Puedo usar BGP con puertas de enlace de VPN basadas en directivas de Azure?
No, BGP solo es compatible con puertas de enlace de VPN basadas en enrutamiento.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>¿Puedo usar ASN (números de sistema autónomos) privados?
Sí, puede usar sus propios ASN públicos o privados para sus redes locales y redes virtuales de Azure.

### <a name="are-there-asns-reserved-by-azure"></a>¿Hay ASN reservados por Azure?
Sí, hello ASN siguientes está reservados por Azure para emparejamientos internos y externos:

* ASN públicos: 8075, 8076, 12076
* ASN privados: 65515, 65517, 65518, 65519, 65520

No puede especificar estas ASN para los dispositivos VPN locales al conectar las puertas de enlace VPN de tooAzure.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>¿Hay algún otro ASN que no puedo usar?
Sí, es Hola después ASN [reservado por IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) y no se puede configurar en la puerta de enlace de VPN de Azure:

23456, 64496-64511, 65535-65551 y 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>¿Puedo usar Hola ASN mismo para ambos local redes VPN y redes virtuales de Azure?
No, debe asignar ASN diferentes entre las redes locales y sus redes virtuales de Azure si las está conectando con BGP. Las puertas de enlace de VPN de Azure tienen un ASN de 65515 predeterminado asignado, independientemente de que BGP esté habilitado, o no, para la conectividad entre locales. Puede invalidar este valor predeterminado asignando un ASN diferente al crear la puerta de enlace VPN de Hola o cambiar Hola ASN después de crea la puerta de enlace de Hola. Necesitará tooassign su toohello de ASN local correspondiente Azure puertas de enlace de red Local.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>¿Qué dirección prefijos will puertas de enlace VPN de Azure anuncian toome?
La puerta de enlace VPN Azure anunciará Hola siguiendo rutas tooyour local BGP dispositivos:

* Sus prefijos de dirección de red virtual
* Prefijos de dirección para cada puerta de enlace de VPN de Azure de puertas de enlace de red Local conectado toohello
* Las rutas aprendidas de otro BGP emparejamiento sesiones conectadas toohello puerta de enlace VPN, **excepto predeterminado o varias rutas coincidía con ningún prefijo de red virtual**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>¿Anunciar puertas de enlace predeterminadas (0.0.0.0/0) de la ruta tooAzure VPN?
Sí.

Tenga en cuenta esto obligará a todo el tráfico de red virtual de salida hacia su sitio local e impedirá que las máquinas virtuales de red virtual de hello aceptar comunicaciones públicas de hello Internet directamente, como RDP o SSH de hello Internet toohello máquinas virtuales.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>¿Puedo anunciar prefijos exacto de hello como mi prefijos de red Virtual?

No, Hola publicidad mismo prefijos como uno de los prefijos de direcciones de red Virtual se bloquea o se filtra Hola plataforma Windows Azure. Sin embargo, puede anunciar un prefijo que sea un superconjunto de lo que contenga su red virtual. 

Por ejemplo, si la red virtual usa Hola dirección espacio 10.0.0.0/16, puede anunciar 10.0.0.0/8. Sin embargo, no se pueden anunciar 10.0.0.0/16 o 10.0.0.0/24.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>¿Puedo usar BGP con mis conexiones de red virtual a red virtual?
Sí, puede utilizar BGP para conexiones entre locales y conexiones de red virtual a red virtual.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>¿Puedo combinar BGP con conexiones no de BGP para mi puertas de enlace de VPN de Azure?
Sí, es posible mezclar ambos BGP y las conexiones no BGP para Hola misma puerta de enlace de VPN de Azure.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>¿Azure VPN Gateway admite el enrutamiento del tránsito de BGP?
Sí, el enrutamiento del tránsito BGP es compatible, con excepción de Hola que las puertas de enlace de VPN de Azure **no** anunciar predeterminado enruta los pares BGP tooother. tooenable tránsito enrutar a través de varias puertas de enlace de VPN de Azure, debe habilitar BGP en todas las conexiones de red virtual a red virtual intermedias.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>¿Puedo tener más de un túnel entre mi red local y Azure VPN Gateway?
Sí, puede establecer más de un túnel VPN S2S entre Azure VPN Gateway y la red local. Tenga en cuenta que todos estos túneles se contarán con el número total de Hola de túneles para las puertas de enlace de VPN de Azure y debe habilitar BGP en dos túneles.

Por ejemplo, si tiene dos túneles redundantes entre la puerta de enlace de VPN de Azure y una de las redes locales, utilizarán 2 túneles fuera de la cuota total de hello para la puerta de enlace de VPN de Azure (10 estándar) y el 30 de alto rendimiento.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>¿Puedo tener varios túneles entre dos redes virtuales de Azure con BGP?
Sí, pero al menos una de las puertas de enlace de red virtual de hello debe estar en la configuración activo / activo.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>¿Se puede usar BGP para VPN de sitio a sitio en que coexisten VPN de sitio a sitio y ExpressRoute?
Sí. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>¿Qué dirección utiliza la puerta de enlace de VPN de Azure para la dirección IP del par BGP?
puerta de enlace de VPN de Azure de Hola asignará una única dirección IP del intervalo de GatewaySubnet definido para la red virtual de Hola Hola. De forma predeterminada, es Hola segunda última dirección de intervalo de Hola. Por ejemplo, si la GatewaySubnet es 10.12.255.0/27, comprendido entre 10.12.255.0 too10.12.255.31, dirección IP del mismo nivel de BGP en puerta de enlace de VPN de Azure de Hola Hola será 10.12.255.30. Puede encontrar esta información al mostrar información de puerta de enlace de VPN de Azure Hola.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>¿Cuáles son los requisitos de Hola para las direcciones IP de BGP del mismo nivel de Hola en mi dispositivo VPN?
Su dirección de punto BGP locales **no debe** Hola igual como dirección IP pública de hello de dispositivo VPN. Usar una dirección IP diferente en el dispositivo VPN de hello para la dirección IP del mismo nivel de BGP. Puede ser una dirección asignada toohello interfaz de bucle invertido en el dispositivo de Hola. Especifique esta dirección en hello puerta de enlace de red Local que representan Hola ubicación correspondiente.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>¿Qué debo especificar como mi prefijos de direcciones de puerta de enlace de red Local de hello cuando utilizo BGP?
Puerta de enlace de red Local Azure especifica los prefijos de dirección inicial de Hola para red local de Hola. Con BGP, debe asignar el prefijo del host de hello (/ 32 del prefijo) de su dirección IP de BGP del mismo nivel como espacio de direcciones de Hola para dicha red local. Si la IP del mismo nivel de BGP es 10.52.255.254, debe especificar "10.52.255.254/32" como localNetworkAddressSpace Hola Hola puerta de enlace de red Local que representa esta red local. Se trata de tooensure que Hola VPN de Azure puerta de enlace establece la sesión BGP de Hola a través de túnel de VPN de S2S Hola.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>¿Qué debo agregar dispositivo VPN de toomy local para la sesión de emparejamiento de BGP Hola?
Debe agregar una ruta al host de hello dirección IP de Azure BGP del mismo nivel en el dispositivo VPN que señala el túnel de VPN con IPsec S2S toohello. Por ejemplo, si hello Azure VPN del mismo nivel IP es "10.12.255.30", debe agregar una ruta de host para "10.12.255.30" con una interfaz de próximo salto de la interfaz de túnel de IPsec coincidente de hello en el dispositivo VPN.

