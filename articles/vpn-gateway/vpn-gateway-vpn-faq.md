---
title: "Preguntas más frecuentes de puerta de enlace de VPN aaaAzure | Documentos de Microsoft"
description: "Hola preguntas más frecuentes de puerta de enlace de VPN. Preguntas más frecuentes sobre las conexiones entre locales, las conexiones de configuración híbrida y las puertas de enlace de VPN de Microsoft Azure Virtual Network."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>Preguntas más frecuentes sobre VPN Gateway

## <a name="connecting"></a>Conectar redes toovirtual

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>¿Puedo conectar redes virtuales en diferentes regiones de Azure?

Sí. De hecho, no hay ninguna restricción de región. Puede conectar una red virtual tooanother red virtual en hello misma región o en una región distinta de Azure. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>¿Puedo conectar redes virtuales en diferentes suscripciones?

Sí.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>¿Puedo conectarme toomultiple sitios desde una única red virtual?

Puede conectar sitios toomultiple mediante hello las API de REST de Azure y Windows PowerShell. Vea hello [multisitio y la conectividad de red virtual a red virtual](#V2VMulti) sección de preguntas más frecuentes.

### <a name="what-are-my-cross-premises-connection-options"></a>¿Cuáles son mis opciones de conexión entre locales?

Hola después entre entornos se admiten las conexiones:

* Sitio a sitio: conexión VPN sobre IPsec (IKE v1 e IKE v2). Este tipo de conexión requiere un dispositivo VPN o RRAS. Para más información, consulte [Sitio a sitio](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Punto a sitio: conexión VPN sobre SSTP (Protocolo de túnel de sockets seguros). Esta conexión no requiere un dispositivo VPN. Para más información, consulte [Punto a sitio](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* VNet a VNet: este tipo de conexión es Hola igual que una configuración de sitio a sitio. TooVNet de red virtual es una conexión VPN a través de IPsec (IKE v1 e IKE v2). No requiere un dispositivo VPN. Para más información, consulte [Red virtual a red virtual](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Varios sitios: Esto es una variación de una configuración de sitio a sitio que permite tooconnect varias redes virtuales de local sitios tooa. Para más información, consulte [Varios sitios](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* ExpressRoute – ExpressRoute es un tooAzure de conexión directa de la WAN, no una conexión de VPN a través de hello Internet pública. Para obtener más información, vea hello [información general técnica de ExpressRoute](../expressroute/expressroute-introduction.md) hello y [preguntas más frecuentes de ExpressRoute](../expressroute/expressroute-faqs.md).

Para más información acerca de las conexiones de puerta de enlace de VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>¿Cuál es la diferencia de hello entre una conexión de sitio a sitio y punto a sitio?

Las configuraciones **de sitio a sitio** (túnel de VPN sobre IPsec/IKE) se encuentran entre la ubicación local y Azure. Esto significa que puede conectarse desde cualquiera de los equipos ubicados en la máquina virtual de local tooany o instancia de rol dentro de la red virtual, dependiendo de cómo elija tooconfigure enrutamiento y los permisos. Es ideal para una conexión entre locales que esté siempre disponible y una opción que se adapta bien a las configuraciones híbridas. Este tipo de conexión se basa en un dispositivo VPN con IPsec (dispositivo de hardware o / software), que debe implementarse en el perímetro de saludo de la red. toocreate este tipo de conexión, debe tener una dirección IPv4 con orientación externa que no está detrás de un dispositivo NAT.

**Point-to-Site** configuraciones (VPN a través de SSTP) permiten conectarse desde un solo equipo desde cualquier lugar tooanything ubicado en la red virtual. Usa el cliente VPN de hello Windows de forma predeterminada. Como parte de la configuración de hello Point-to-Site, instale un certificado y un paquete de configuración de cliente VPN, que contiene la configuración de Hola que permiten a la máquina virtual de equipo tooconnect tooany o instancia de rol dentro de la red virtual de Hola. Es fantástico si desea la red virtual de tooconnect tooa, pero no están ubicados en local. También es una buena opción cuando no tienes acceso tooVPN hardware o una dirección IPv4 con orientación externa, ambos de los cuales son necesarios para una conexión de sitio a sitio.

Puede configurar su toouse de red virtual de sitio a sitio y tipo de punto a sitio simultáneamente, siempre y cuando se crea la conexión de sitio a sitio mediante una VPN basada en ruta para la puerta de enlace. Tipos VPN basadas en enrutamiento se denominan puertas de enlace dinámicos en el modelo de implementación clásica de Hola.

## <a name="gateways"></a>Puertas de enlace de red virtual

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>¿Es la puerta de enlace de VPN una puerta de enlace de red virtual?

Una puerta de enlace de VPN es un tipo de puerta de enlace de red virtual. Una puerta de enlace de VPN envía tráfico cifrado entre la red virtual y la ubicación local a través de una conexión pública. También puede utilizar un tráfico de toosend de puerta de enlace VPN entre redes virtuales. Cuando se crea una puerta de enlace VPN, se utiliza el valor de - el GatewayType de hello 'Vpn'. Para más información, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>¿Qué es una puerta de enlace basada en directivas (de enrutamiento estático)?

Las puertas de enlace basadas en directivas implementan VPN basadas en directivas. Las VPN basadas en directiva cifrar y dirigen paquetes a través de túneles de IPsec basados en combinaciones de Hola de prefijos de dirección entre la red local y Hola red virtual de Azure. Directiva de Hello (o Selector de tráfico) se define generalmente como una lista de acceso en la configuración de VPN de Hola.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>¿Qué es una puerta de enlace basada en enrutamiento (de enrutamiento dinámico)?

Implemente las puertas de enlace basado en enrutamiento Hola VPN basadas en la ruta. Las VPN basadas en enrutamiento usar "las rutas de" hello IP de reenvío o enrutar paquetes de toodirect de tabla en sus interfaces de túnel correspondiente. interfaces de túnel de Hello, a continuación, cifrar o descifrar los paquetes de saludo dentro y fuera de los túneles de Hola. Hola selector de directiva o tráfico VPN basadas en enrutamiento se configuran como-hacia cualquier (o "comodines").

### <a name="do-i-need-a-gatewaysubnet"></a>¿Necesito una "GatewaySubnet"?

Sí. subred de puerta de enlace de Hello contiene direcciones IP de Hola que utilizan los servicios de puerta de enlace de red virtual de Hola. Necesitará toocreate una subred de puerta de enlace para la red virtual en orden tooconfigure una puerta de enlace de red virtual. Todas las subredes de puerta de enlace deben denominarse "GatewaySubnet" toowork correctamente. No denomine de ninguna otra forma la subred de puerta de enlace. Y no implementar máquinas virtuales o la subred de puerta de enlace de toohello nada.

Cuando se crea la subred de puerta de enlace de hello, especifica Hola número de direcciones IP que Hola subred contiene. se asignan direcciones IP de Hello en la subred de puerta de enlace de hello toohello servicio de puerta de enlace. Algunas configuraciones requieren más toobe de direcciones IP asignada toohello servicios de puerta de enlace de hacer otras personas. Desea toomake seguro de que la subred de puerta de enlace contiene suficientes direcciones IP tooaccommodate el crecimiento futuro y posibles configuraciones adicionales de conexión nueva. Por lo tanto, aunque es posible crear una puerta de enlace tan pequeña como /29, se recomienda que sea de /27 o mayor (/27, /26, /25, etc.). Mire requisitos de hello para la configuración de Hola que desee toocreate y comprobar esa subred de puerta de enlace de hello que tiene cumplirá los requisitos.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>¿Puedo implementar máquinas virtuales o la subred de puerta de enlace de toomy de instancias de rol?

No.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>¿Puedo obtener mi dirección IP de puerta de enlace VPN antes de crearla?

No. Tiene la dirección IP de puerta de enlace primera tooget hello toocreate. dirección IP de Hello cambia si elimina y volver a crear la puerta de enlace VPN.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>¿Se puede solicitar una dirección IP pública estática para una puerta de enlace de VPN?

No. Solo se admite la asignación de direcciones IP dinámicas. Sin embargo, esto no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN. cambios de dirección IP de puerta de enlace VPN de hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear. Hola dirección pública de puerta de enlace VPN no cambia entre el cambio de tamaño, restablecer u otras mantenimiento o las actualizaciones internas de la puerta de enlace VPN. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>¿Cómo se autentica mi túnel VPN?

VPN de Azure usa autenticación PSK (clave previamente compartida). Se genera una clave precompartida (PSK) cuando se crea el túnel VPN de Hola. Puede cambiar Hola generado automáticamente PSK tooyour propio con el cmdlet de PowerShell de clave compartida previamente establecido de Hola o API de REST.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>¿Puedo usar Hola establecer API de clave compartida previamente tooconfigure mi basada en directivas (enrutamiento estático) puerta de enlace VPN?

Sí, cmdlet de PowerShell y API de clave compartida previamente establecido Hola puede ser usado tooconfigure Azure VPN (estático) basada en directivas y basadas en enrutamiento de VPN de enrutamiento (dinámico).

### <a name="can-i-use-other-authentication-options"></a>¿Puedo usar otras opciones de autenticación?

Estamos limitados toousing claves precompartidas (PSK) para la autenticación.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>¿Cómo puedo especificar que el tráfico se dirige a través de puerta de enlace VPN de hello?

#### <a name="resource-manager-deployment-model"></a>Modelo de implementación del Administrador de recursos

* PowerShell: use "AddressPrefix" toospecify tráfico para puerta de enlace de red local de Hola.
* Portal de Azure: navegar por la puerta de enlace de red Local toohello > Configuración > espacio de direcciones.

#### <a name="classic-deployment-model"></a>Modelo de implementación clásica

* Portal de Azure: navegar por la red virtual clásica de toohello > conexiones VPN > conexiones VPN de sitio a sitio > nombre de sitio Local > sitio Local > espacio de direcciones de cliente. 
* Portal clásico: agregue cada intervalo que desee enviar a través de puerta de enlace de hello para la red virtual en la página redes de hello redes locales. 

### <a name="can-i-configure-forced-tunneling"></a>¿Puedo configurar una tunelización forzada?

Sí. Consulte [Configurar una tunelización forzada](vpn-gateway-about-forced-tunneling.md).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>¿Puedo configurar mi propio servidor VPN en Azure y usarlo red local de tooconnect toomy?

Sí, puede implementar su propia puertas de enlace VPN o servidores en Azure desde hello Azure Marketplace o crear sus propios enrutadores VPN. Necesita rutas de tooconfigure definido por el usuario en la red virtual tooensure tráfico se enruta correctamente entre las redes locales y las subredes de red virtual.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>¿Por qué hay algunos puertos abiertos en mi puerta de enlace de VPN?

Son necesarios para la comunicación de la infraestructura de Azure. Están protegidos (bloqueados) mediante certificados de Azure. Sin los certificados apropiados, entidades externas, incluidos a los clientes de Hola de las puertas de enlace, no será capaz de toocause cualquier efecto en esos puntos de conexión.

Una puerta de enlace VPN es fundamentalmente un dispositivo de host múltiple con una NIC punteando en red privada de saludo del cliente y una NIC orientados al público Hola red pública. Las entidades de la infraestructura de Azure no se pulse en redes privadas de cliente por motivos de cumplimiento, por lo que necesitan los extremos públicos de tooutilize para la comunicación de infraestructura. extremos públicos de Hola se examinan periódicamente por auditoría de seguridad de Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Más información acerca de los tipos de puerta de enlace, los requisitos y el rendimiento

Para más información, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md).

## <a name="s2s"></a>Conexiones de sitio a sitio y dispositivos VPN

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>¿Qué tengo que tener en cuenta al seleccionar un dispositivo VPN?

Hemos validado un conjunto de dispositivos estándar VPN de sitio a sitio en colaboración con proveedores de dispositivos. Puede encontrar una lista de dispositivos VPN compatibles conocidos, sus correspondientes instrucciones de configuración o ejemplos y las especificaciones de los dispositivos en hello [dispositivos VPN sobre](vpn-gateway-about-vpn-devices.md) artículo. Todos los dispositivos en familias de dispositivos de hello aparecen como compatibles conocidos deben funcionar con la red Virtual. toohelp configurar el dispositivo VPN, consulte el ejemplo de configuración de dispositivo toohello o vínculo que corresponda tooappropriate familia de dispositivos.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>¿Dónde puedo encontrar los valores de configuración de los dispositivos VPN?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Edición de ejemplos de configuración de dispositivos VPN

Para obtener información sobre cómo modificar los ejemplos de configuración de dispositivo, vea [Edición de ejemplos](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>¿Dónde encuentro los parámetros de IPsec e IKE?

Para los parámetros de IPsec/IKE, vea [Parámetros](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>¿Por qué mi túnel de VPN basado en directivas deja de funcionar cuando el tráfico está inactivo?

Este es el comportamiento esperado para puertas de enlace de VPN basadas en directivas (también conocido como enrutamiento estático). Al tráfico de Hola a través de túnel de hello está inactivo durante más de 5 minutos, se cierra el túnel de Hola. Cuando inicia el tráfico que fluyen en cualquier dirección, túnel Hola se restablecerá inmediatamente.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>¿Puedo usar software VPN tooconnect tooAzure?

Para la configuración de sitio a sitio entre locales se admiten los servidores de Windows Server 2012 con servicio de enrutamiento y acceso remoto (RRAS).

Otras soluciones VPN de software deben funcionar con nuestra puerta de enlace siempre y cuando se ajusten las implementaciones IPsec estándar de tooindustry. Para obtener instrucciones de configuración y soporte técnico, póngase en contacto con el proveedor de Hola de software de Hola.

## <a name="P2S"></a>Conexiones de punto a sitio

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>Conexiones entre dos redes virtuales y multisitio

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>¿Puedo usar tráfico de tootransit de puerta de enlace de VPN de Azure entre Mis sitios locales o de red virtual de tooanother?

**Modelo de implementación de Resource Manager**<br>
Sí. Vea hello [BGP](#bgp) sección para obtener más información.

**Modelo de implementación clásica**<br>
Transferir el tráfico a través de puerta de enlace VPN de Azure es posible mediante el modelo de implementación clásica de hello, pero se basa en espacios de direcciones definidos de forma estática en el archivo de configuración de red de Hola. BGP no es compatible todavía con puertas de enlace de VPN y redes virtuales de Azure mediante el modelo de implementación clásica de Hola. Sin BGP, definir manualmente los espacios de direcciones de tránsito es difícil de hacer sin errores y no se recomienda.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>¿Azure genera Hola mismo IPsec/IKE compartido previamente clave todas mis conexiones VPN para hello mismo red virtual?

No, Azure de forma predeterminada genera distintas claves precompartidas para distintas conexiones VPN. Sin embargo, puede usar Hola establecer los API de REST de clave de puerta de enlace de VPN o PowerShell cmdlet tooset Hola clave-valor que prefiera. clave de Hello debe ser alfanumérica con una cadena de longitud de entre 1 too128 caracteres.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>¿Tengo más ancho de banda con más VPN de sitio a sitio que si tengo una única red virtual?

No, todos los túneles VPN, incluidos Point-to-Site VPN, comparten Hola mismo VPN de Azure hello y puerta de enlace de ancho de banda disponible.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>¿Puedo configurar varios túneles entre mi red virtual y mi sitio local utilizando VPN multisitio?

Sí, pero debe configurar BGP en ambos toohello túneles misma ubicación.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>¿Puedo usar VPN de punto a sitio con mi red virtual con varios túneles VPN?

Sí, se pueden usar VPN punto a sitio (P2S) con las puertas de enlace VPN de hello conectar sitios locales de toomultiple y otras redes virtuales.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>¿Puedo conectar una red virtual con VPN con IPsec toomy circuito de ExpressRoute?

Sí, este procedimiento se admite. Para más información, consulte [Configurar conexiones VPN ExpressRoute y sitio a sitio que coexistan](../expressroute/expressroute-howto-coexist-classic.md).

## <a name="ipsecike"></a>Directiva de IPsec o IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Conectividad entre locales y máquinas virtuales

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Si mi máquina virtual está en una red virtual y tener una conexión entre entornos, ¿cómo debo conectar toohello VM?

Dispone de varias opciones. Si tiene RDP habilitado para la máquina virtual, puede conectarse mediante el uso de direcciones IP privadas de hello tooyour virtual machine. En ese caso, debería especificar direcciones IP privadas de Hola y Hola puerto que desee tooconnect demasiado (normalmente 3389). Se necesita el puerto de hello tooconfigure en la máquina virtual para el tráfico de Hola.

También puede conectar máquina virtual de tooyour por dirección IP privada desde otra máquina virtual que se encuentra en hello misma red virtual. No es posible máquina virtual RDP tooyour mediante el uso de direcciones IP privadas de hello si se conecta desde una ubicación fuera de la red virtual. Por ejemplo, si tiene una red virtual de Point-to-Site configurada y no establece una conexión desde su equipo, no se puede conectar máquinas virtuales de toohello por dirección IP privada.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>¿Si mi máquina virtual está en una red virtual con conectividad entre entornos, todo el tráfico de Hola de mi máquina virtual vaya a través de esa conexión?

No. Solo el tráfico de Hola que tiene un destino de IP que se encuentra en intervalos de direcciones de IP de red Local de red virtual de Hola que especificó pasará a través de puerta de enlace de red virtual de Hola. Tráfico tiene un destino IP situado dentro de la red virtual de hello permanece dentro de la red virtual de Hola. El tráfico restante se enviados a través de redes públicas del toohello de equilibrador de carga Hola o si se usa la tunelización forzada, se envía a través de puerta de enlace de VPN de Azure de Hola.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>Cómo se puede solucionar un tooa de conexión RDP VM

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Preguntas más frecuentes sobre Virtual Network

Ver información de red virtuales adicionales en hello [P+F de red Virtual](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Pasos siguientes

* Para más información sobre VPN Gateway, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).
* Para más información acerca de la configuración de VPN Gateway, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md).
