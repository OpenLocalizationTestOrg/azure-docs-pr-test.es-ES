Hola P+F de red virtual a red virtual aplica a las conexiones de puerta de enlace de tooVPN. Si busca información sobre el emparejamiento de redes virtuales, consulte [Emparejamiento de redes virtuales](../articles/virtual-network/virtual-network-peering-overview.md).

### <a name="does-azure-charge-for-traffic-between-vnets"></a>¿Cobra Azure por el tráfico entre redes virtuales?

Tráfico de red virtual a red virtual dentro de hello misma región es gratuita para ambas direcciones cuando se usa una conexión de puerta de enlace VPN. Entre la salida de la red virtual a red virtual de región tráfico se cobra con velocidades de transferencia de datos Hola entre redes virtuales saliente basándose en regiones de origen de Hola. Consulte toohello [página de precios de puerta de enlace de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway/) para obtener más información. Si va a conectar sus redes virtuales mediante el intercambio de tráfico de red virtual, en lugar de puerta de enlace de VPN, consulte hello [página de precios de red Virtual](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>¿Tráfico de red virtual a red virtual que se transmiten a través de hello Internet?

No. Tráfico de red virtual a red virtual pasa a través de la red troncal de Microsoft Azure, Internet y no Hola Hola.

### <a name="is-vnet-to-vnet-traffic-secure"></a>¿Es seguro el tráfico entre dos redes virtuales?

Sí, se protege mediante cifrado IPsec/IKE.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>¿Es necesario un tooconnect de dispositivo VPN redes virtuales entre sí?

No. La conexión simultánea de varias redes virtuales de Azure no requiere dispositivos VPN, a menos que sea necesaria la conectividad entre locales.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>¿Mis redes virtuales necesita toobe Hola misma región?

No. redes virtuales de Hello pueden estar en hello mismo o en distintas regiones Azure (ubicaciones).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>¿Si no está en redes virtuales Hola Hola mismo suscripciones, las suscripciones de hello necesitan toobe asociado Hola AD mismo inquilino?

No.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>¿Puedo usar las conexiones entre dos redes virtuales con conexiones multisitio?

Sí. La conectividad de red virtual se puede usar de forma simultánea con VPN de varios sitios.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>¿A cuántos sitios locales y redes virtuales se puede conectar una red virtual?

Consulte la tabla [Requisitos de la puerta de enlace](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>¿Puedo usar red virtual a red virtual tooconnect máquinas virtuales o servicios fuera de una red virtual en la nube?

No. VNet a VNet admite la conexión de redes virtuales. No admite la conexión de máquinas virtuales ni servicios en la nube que no estén en una red virtual.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>¿Abarca redes virtuales un servicio en la nube o un punto de conexión de equilibrio de carga?

No. Un servicio en la nube o un punto de conexión de equilibrio de carga no puede abarcar varias redes virtuales, aunque estas estén conectadas entre sí.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>¿Puedo usar un tipo de VPN PolicyBased para las conexiones entre dos redes virtuales o multisitio?

No. Las conexiones entre dos redes virtuales y multisitio requieren puertas de enlace de VPN de Azure con tipos de VPN RouteBased (antes denominado enrutamiento dinámico).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>¿Puedo conectar una red virtual con una red virtual de tipo de VPN del tipo routebased tooanother con un tipo de PolicyBased VPN?

No, ambas redes virtuales TIENEN QUE usar VPN basadas en enrutamiento (antes denominado enrutamiento dinámico).

### <a name="do-vpn-tunnels-share-bandwidth"></a>¿Comparten ancho de banda los túneles de VPN?

Sí. Todos los túneles VPN de red virtual de hello comparten el ancho de banda disponible de hello en puerta de enlace de VPN de Azure de Hola y Hola mismo SLA de tiempo de actividad de puerta de enlace VPN en Azure.

### <a name="are-redundant-tunnels-supported"></a>¿Se admiten túneles redundantes?

Los túneles redundantes entre dos redes virtuales se admiten cuando la puerta de enlace de una red virtual está configurada como activa-activa.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>¿Puedo tener espacios de direcciones superpuestos para configuraciones de red virtual a red virtual?

No. No puede tener intervalos de direcciones de IP superpuestos.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>¿Puede haber espacios de direcciones superpuestos entre las redes virtuales conectadas y los sitios locales?

No. No puede tener intervalos de direcciones de IP superpuestos.



