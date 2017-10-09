### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>¿Qué sistemas operativos de cliente puedo usar para las conexiones de punto a sitio?

se admite Hola siguientes sistemas operativos de cliente:

* Windows 7 (32 bits y 64 bits)
* Windows Server 2008 R2 (solo 64 bits)
* Windows 8 (32 bits y 64 bits)
* Windows 8.1 (32 bits y 64 bits)
* Windows Server 2012 (solo 64 bits)
* Windows Server 2012 R2 (solo 64 bits)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>¿Puedo usar cualquier cliente de software VPN de punto a sitio que admita SSTP?

No. Compatibilidad con está limitado solo toohello Windows versiones de sistemas operativos enumeradas anteriormente.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>¿Cuántos puntos de conexión de cliente VPN puedo tener en mi configuración punto a sitio?

Se admiten too128 VPN clientes toobe pueda tooconnect tooa red virtual en hello mismo tiempo.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>¿Puedo usar mi propio CA raíz de PKI interna para la conectividad de punto a sitio?

Sí. Anteriormente, solo podían usarse certificados raíz autofirmados. Todavía puede cargar 20 certificados raíz.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>¿Puedo atravesar servidores proxy y firewalls con la funcionalidad de punto a sitio?

Sí. Usamos SSTP (Protocolo de túnel de sockets de seguros) tootunnel a través de firewalls. Este túnel aparecerá como una conexión HTTPs.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>¿Si reinicia un equipo cliente configurado para punto a sitio, se hello VPN volverán a conectar?

De forma predeterminada, equipo de cliente hello no volverá a establecer conexión de VPN de hello automáticamente.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>¿Admite punto a sitio la reconexión automática y DDNS en Hola los clientes VPN?

Las VPN de punto a sitio no admiten la reconexión automática y el DDNS.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>¿Tengo que el sitio a sitio y configuraciones de Point-to-Site coexistan en hello mismo red virtual?

Sí. Ambas soluciones funcionarán si tiene un tipo de VPN basada en enrutamiento para la puerta de enlace. Para el modelo de implementación clásica de hello, necesita una puerta de enlace dinámico. Hacemos no compatibilidad con Point-to-Site para puertas de enlace VPN de enrutamientos estáticos o puertas de enlace con hello `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>¿Se puede configurar una red virtual de Point-to-Site cliente tooconnect toomultiple en hello mismo tiempo?

Sí, es posible. Pero las redes virtuales hello no pueden tener prefijos IP que se superpongan y espacios de direcciones de hello Point-to-Site no deben solaparse entre redes virtuales Hola.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>¿Qué rendimiento puedo esperar en las conexiones de sitio a sitio o de punto a sitio?

Es difícil toomaintain Hola exacta el rendimiento de túneles VPN de Hola. IPsec y SSTP son protocolos VPN con mucho cifrado. El rendimiento también está limitado por la latencia de Hola y el ancho de banda entre las instalaciones locales y Hola Internet.
