### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>¿Se admite la directiva de IPsec o IKE personalizada en todas las SKU de Azure VPN Gateway?
La directiva IPsec/IKE personalizada se admite en las puertas de enlace Azure VPN Gateway **VpnGw1, VpnGw2, VpnGw3, Estándar** y **HighPerformance**. **Basic** NO se admite.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>¿Cuántas directivas puedo especificar en una conexión?
Solo se puede especificar ***una*** combinación de directivas para una conexión dada.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>¿Se puede especificar una directiva parcial en una conexión? (p. ej., solo algoritmos IKE, no IPsec)
No, es preciso especificar todos los algoritmos y parámetros de IKE (modo principal) e IPsec (modo rápido). No se permite la especificación de una directiva parcial.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>¿Cuáles son los algoritmos de Hola y ventajas claves admitidos de directiva personalizada de hello?
tabla de Hello siguiente muestra hello admitido los algoritmos criptográficos y ventajas claves configurables por los clientes de Hola. Es preciso seleccionar una opción en cada campo.

| **IPsec o IKEv2**  | **Opciones**                                                                   |
| ---              | ---                                                                           |
| Cifrado IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Integridad de IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Grupo DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, Ninguno |
| Cifrado IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, No      |
| Integridad de IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Grupo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, No                              |
| Vigencia de SA QM   | Segundos (entero; **mín. 300**/predeterminado 27000 segundos)<br>KBytes (entero; **mín. 1024**/predeterminado 102400000 KBytes)           |
| Selector de tráfico | UsePolicyBasedTrafficSelectors ($True/$False; default $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 se Hola igual como grupo Diffie-Hellman **14** en IKE e IPsec PFS. Vea [grupos Diffie-Hellman](#DH) por hello, realice las asignaciones.
> 2. Para los algoritmos GCMAES, debe especificar Hola misma longitud GCMAES el algoritmo y la clave de cifrado de IPsec y la integridad.
> 3. Duración de la SA de modo principal IKEv2 se fija en 28.800 segundos en puertas de enlace de VPN de Azure Hola
> 4. Las vigencias de SA de QM son parámetros opcionales. Si no se ha especificado ninguna, se usan los valores predeterminados de 27 000 segundos (7,5 hrs) y 102400000 KBytes (102 GB).
> 5. UsePolicyBasedTrafficSelector es un parámetro de opción de conexión de Hola. Vea la siguiente pregunta Frecuente de hello elemento para "UsePolicyBasedTrafficSelectors"

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>¿Todo lo que necesita toomatch entre Hola directiva de puerta de enlace de VPN de Azure y mis configuraciones del dispositivo VPN local?
La configuración del dispositivo VPN local debe coincidir o contener Hola después de algoritmos y parámetros que especifican en Hola directiva IPsec/IKE de Azure:

* Algoritmo de cifrado IKE
* Algoritmo de integridad de IKE
* Grupo DH
* Algoritmo de cifrado IPsec
* Algoritmo de integridad de IPsec
* Grupo PFS
* Selector de tráfico (*)

vigencias de SA Hola solo especificaciones local, no es necesario toomatch.

Si habilita **UsePolicyBasedTrafficSelectors**, deberá tooensure el dispositivo VPN tiene Hola coincidencia selectores de tráfico definidos con todas las combinaciones de los prefijos de (puerta de enlace de red local) de la red local de Hola Prefijos de red virtual de Azure, en lugar de y a cualquier. Por ejemplo, si los prefijos de red local son 10.1.0.0/16 y 10.2.0.0/16 y los prefijos de red virtual son 192.168.0.0/16 y 172.16.0.0/16, necesita hello toospecify siguiendo los selectores de tráfico:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Consulte demasiado[conectar varios dispositivos VPN locales de basada en directivas](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obtener más información acerca de cómo toouse esta opción.

### <a name ="DH"></a>¿Qué grupos Diffie-Hellman se admiten?
tabla de Hello siguiente muestra hello admitida grupos de Diffie-Hellman de IKE (DHGroup) e IPsec (PFSGroup):

| **Grupo Diffie-Hellman**  | **Grupo DH**              | **Grupo PFS** | **Longitud de clave** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP de 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP de 1024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP de 2048 bits  |
| 19                        | ECP256                   | ECP256       | ECP de 256 bits    |
| 20 |                        | ECP384                   | ECP284       | ECP de 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP de 2048 bits  |
|                           |                          |              |                |

Consulte demasiado[RFC3526](https://tools.ietf.org/html/rfc3526) y [RFC5114](https://tools.ietf.org/html/rfc5114) para obtener más detalles.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>¿Reemplace directiva personalizada de hello conjuntos de directivas de IPsec/IKE Hola predeterminados para puertas de enlace de VPN de Azure?
Sí, una vez que se especifica una directiva personalizada en una conexión, puerta de enlace VPN de Azure solo utilizará Directiva hello en conexión hello, como iniciador IKE y contestador IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>¿Si quita una directiva de IPsec/IKE personalizada, conexión Hola se convierten en no protegido?
No, conexión Hola permanecerá protegido por IPsec/IKE. Una vez que quita la directiva personalizada de Hola desde una conexión, puerta de enlace de VPN de Azure de hello volverá atrás toohello [lista predeterminada de las propuestas de IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) y vuelva a iniciar Hola negociación IKE nuevo con el dispositivo VPN local.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>¿Afectarían a mi conexión VPN la incorporación o actualización de una directiva de IPsec o IKE?
Sí, que podría causar una pequeña interrupción (unos segundos) como puerta de enlace de VPN de Azure de Hola se caer la conexión existente de Hola y vuelva a iniciar hello toore de protocolo de enlace de IKE-establecer Hola de túnel de IPsec con nuevos algoritmos criptográficos de Hola y parámetros. Asegúrese de que el dispositivo VPN local también se configura con algoritmos de búsqueda de coincidencias de Hola y las interrupciones de hello toominimize de ventajas clave.

### <a name="can-i-use-different-policies-on-different-connections"></a>¿Se pueden usar distintas directivas en conexiones diferentes?
Sí. La directiva personalizada se aplica en función de la conexión. Puede crear y aplicar distintas directivas de IPsec o IKE en conexiones diferentes. También puede elegir tooapply directivas personalizadas en un subconjunto de las conexiones. Hola los restantes usará conjuntos de directivas de IPsec/IKE de hello predeterminado de Azure.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>¿Puedo usar directivas personalizadas de hello en así la conexión de red virtual a red virtual?
Sí, puede aplicar directivas personalizadas en las conexiones entre entornos de IPsec o las conexiones entre redes virtuales.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>¿Necesito toospecify Hola la misma directiva en los recursos de conexión de red virtual a red virtual?
Sí. Un túnel entre redes virtuales consta de dos recursos de conexión en Azure, una para cada dirección. Necesita tooensure los recursos de conexión tienen Hola misma directiva othereise Hola conexión de red virtual a red virtual, no se establecerá.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>¿Funciona la directiva de IPsec o IKE personalizada en una conexión ExpressRoute?
No. Directiva IPsec/IKE solo funciona en conexiones de red virtual a red virtual a través de las puertas de enlace VPN de Azure de Hola y de VPN de S2S.
