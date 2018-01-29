### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>¿Se admite la directiva de IPsec o IKE personalizada en todas las SKU de Azure VPN Gateway?
La directiva IPsec/IKE personalizada se admite en las puertas de enlace Azure VPN Gateway **VpnGw1, VpnGw2, VpnGw3, Estándar** y **HighPerformance**. La SKU **Basic** **no** se admite.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>¿Cuántas directivas puedo especificar en una conexión?
Solo se puede especificar ***una*** combinación de directivas para una conexión dada.

### <a name="can-i-specify-a-partial-policy-on-a-connection-for-example-only-ike-algorithms-but-not-ipsec"></a>¿Se puede especificar una directiva parcial en una conexión? (por ejemplo, solo algoritmos IKE, pero no IPsec)
No, es preciso especificar todos los algoritmos y parámetros de IKE (modo principal) e IPsec (modo rápido). No se permite la especificación de una directiva parcial.

### <a name="what-are-the-algorithms-and-key-strengths-supported-in-the-custom-policy"></a>¿Cuáles son los algoritmos y los niveles de las claves que se admiten en la directiva personalizada?
En la tabla siguiente se enumeran los algoritmos criptográficos y los niveles de las claves admitidos que pueden configurar los clientes. Es preciso seleccionar una opción en cada campo.

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
> 1. DHGroup2048 y PFS2048 son los mismos que el grupo Diffie-Hellman **14** en IKE e IPsec PFS. Consulte [Grupos Diffie-Hellman](#DH) para las asignaciones completas.
> 2. Para los algoritmos GCMAES, debe especificar el mismo algoritmo GCMAES y longitud de clave para el cifrado e integridad de IPsec.
> 3. La vigencia de SA del modo principal de IKEv2 se fija en 28 800 segundos en las puertas de enlace de VPN de Azure
> 4. Las vigencias de SA de QM son parámetros opcionales. Si no se ha especificado ninguno, se usan los valores predeterminados de 27 000 segundos (7,5 h) y 102 400 000 KBytes (102 GB).
> 5. UsePolicyBasedTrafficSelector es un parámetro de opción en la conexión. Consulte las preguntas frecuentes acerca de "UsePolicyBasedTrafficSelectors".

### <a name="does-everything-need-to-match-between-the-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>¿Es preciso que coincidan todos los elementos de la directiva de Azure VPN Gateway con las configuraciones de mis dispositivos VPN locales?
La configuración de su dispositivo VPN local debe coincidir o contener los siguientes algoritmos y parámetros que se especifican en la directiva de IPsec o IKE de Azure:

* Algoritmo de cifrado IKE
* Algoritmo de integridad de IKE
* Grupo DH
* Algoritmo de cifrado IPsec
* Algoritmo de integridad de IPsec
* Grupo PFS
* Selector de tráfico (*)

Las vigencias de SA solo son especificaciones locales, no es preciso que coincidan.

Si habilita **UsePolicyBasedTrafficSelectors**, debe asegurarse de que el dispositivo VPN tiene los selectores de tráfico coincidentes definidos con todas las combinaciones de sus prefijos de red local (puerta de enlace de red local) a o desde los prefijos de red virtual de Azure, en lugar de cualquiera a cualquiera. Por ejemplo, si sus prefijos de red local son 10.1.0.0/16 y 10.2.0.0/16, y sus prefijos de red virtual son 192.168.0.0/16 y 172.16.0.0/16, debe especificar los siguientes selectores de tráfico:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Para más información, consulte [Connect multiple on-premises policy-based VPN devices](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) (Conexión de varios dispositivos VPN basados en directivas locales).

### <a name ="DH"></a>¿Qué grupos Diffie-Hellman se admiten?
En la tabla siguiente se enumeran los grupos Diffie-Hellman compatibles para IKE (DHGroup) e IPsec (PFSGroup):

| **Grupo Diffie-Hellman**  | **Grupo DH**              | **Grupo PFS** | **Longitud de clave** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP de 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP de 1024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP de 2048 bits  |
| 19                        | ECP256                   | ECP256       | ECP de 256 bits    |
| 20 |                        | ECP384                   | ECP284       | ECP de 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP de 2048 bits  |
|                           |                          |              |                |

Para más información, consulte [RFC3526](https://tools.ietf.org/html/rfc3526) y [RFC5114](https://tools.ietf.org/html/rfc5114).

### <a name="does-the-custom-policy-replace-the-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>¿Reemplaza la directiva personalizada los conjuntos de directivas de IPsec o IKE predeterminados en las puertas de enlace de VPN de Azure?
Sí, una vez que se especifica una directiva personalizada en una conexión, Azure VPN Gateway solo utilizará la directiva en la conexión, no solo como iniciador de IKE sino también como respondedor de IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-the-connection-become-unprotected"></a>Si quito una directiva de IPsec o IKE personalizada, ¿se que la conexión desprotegida?
No, IPsec o IKE seguirán protegiendo la protección. Una vez que se quite la directiva personalizada de una conexión, Azure VPN Gateway vuelve a la [lista predeterminada de las propuestas de IPsec o IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md), y vuelve a iniciar el protocolo de enlace de IKE con un dispositivo VPN local.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>¿Afectarían a mi conexión VPN la incorporación o actualización de una directiva de IPsec o IKE?
Sí, podría producirse una pequeña interrupción (unos segundos), ya que Azure VPN Gateway anula la conexión existente y vuelve a iniciar el protocolo de enlace de IKE para restablecer el túnel IPsec con los nuevos parámetros y algoritmos criptográficos. Asegúrese de que el dispositivo VPN local también se configura con los algoritmos y niveles de claves coincidentes para minimizar dicha interrupción.

### <a name="can-i-use-different-policies-on-different-connections"></a>¿Se pueden usar distintas directivas en conexiones diferentes?
Sí. La directiva personalizada se aplica en función de la conexión. Puede crear y aplicar distintas directivas de IPsec o IKE en conexiones diferentes. También puede elegir aplicar directivas personalizadas a un subconjunto de las conexiones. Las restantes usan los conjuntos de directivas de IPsec o IKE predeterminados de Azure.

### <a name="can-i-use-the-custom-policy-on-vnet-to-vnet-connection-as-well"></a>¿Se puedo usar la directiva personalizada también en una conexión entre redes virtuales?
Sí, puede aplicar directivas personalizadas en las conexiones entre entornos de IPsec o las conexiones entre redes virtuales.

### <a name="do-i-need-to-specify-the-same-policy-on-both-vnet-to-vnet-connection-resources"></a>¿Es preciso especificar la misma directiva en los dos recursos de la conexión entre redes virtuales?
Sí. Un túnel entre redes virtuales consta de dos recursos de conexión en Azure, una para cada dirección. Asegúrese de que los dos recursos de conexión tienen la misma directiva, ya que, de no ser así, la conexión entre redes virtuales no se establecerá.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>¿Funciona la directiva de IPsec o IKE personalizada en una conexión ExpressRoute?
No. La directiva de IPsec o IKE solo funciona en conexiones entre redes virtuales a través de las puertas de enlace de VPN de Azure y VPN de S2S.