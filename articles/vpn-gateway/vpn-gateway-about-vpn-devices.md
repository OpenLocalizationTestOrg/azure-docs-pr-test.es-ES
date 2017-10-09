---
title: aaaAbout los dispositivos VPN para las conexiones de Azure entre entornos | Documentos de Microsoft
description: "En este artículo se describen los dispositivos VPN y los parámetros de IPsec de las conexiones entre locales de VPN Gateway S2S. Se proporcionan vínculos ejemplos e instrucciones de tooconfiguration."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>Acerca de los dispositivos VPN y los parámetros de IPsec/IKE para conexiones de VPN Gateway de sitio a sitio

Un dispositivo VPN es tooconfigure requiere una conexión de VPN de sitio a sitio (S2S) entre entornos con una puerta de enlace VPN. Las conexiones de sitio a sitio pueden ser toocreate usa una solución híbrida o cada vez que desee proteger las conexiones entre las redes locales y las redes virtuales. Este artículo incluye la lista de dispositivos VPN validados y una lista de parámetros IPsec/IKE para las puertas de enlace de VPN.

> [!IMPORTANT]
> Si experimenta problemas de conectividad entre los dispositivos VPN local y las puertas de enlace VPN, consulte demasiado[los problemas de compatibilidad de dispositivo](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Elementos toonote al ver las tablas de hello:

* Ha habido un cambio terminológico en las puertas de enlace de VPN de Azure. Solo los nombres de hello han cambiado. No hay ningún cambio de funcionalidad.
  * Enrutamiento estático = PolicyBased
  * Enrutamiento dinámico = RouteBased
* Especificaciones de puerta de enlace VPN HighPerformance y puerta de enlace VPN RouteBased se Hola mismo, a menos que se indique lo contrario. Por ejemplo, hello validado de los dispositivos VPN que son compatibles con puertas de enlace VPN RouteBased también son compatibles con hello puerta de enlace VPN HighPerformance.

## <a name="devicetable"></a>Dispositivos VPN validados y guías de configuración de dispositivos

> [!NOTE]
> Al configurar una conexión de sitio a sitio, una dirección IP IPv4 pública es necesaria para el dispositivo VPN.
>

En colaboración con proveedores de dispositivos, hemos validado un conjunto de dispositivos VPN estándar. Todos los dispositivos de hello en familias de dispositivos de Hola Hola lista siguiente deben funcionar con las puertas de enlace VPN. Vea [acerca de la configuración de puerta de enlace de VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand Hola VPN escriba use (PolicyBased o del tipo routebased.) para hello solución de puerta de enlace VPN que desea tooconfigure.

toohelp configurar el dispositivo VPN, consulte los vínculos de toohello que corresponden tooappropriate familia de dispositivos. se proporcionan instrucciones de tooconfiguration de vínculos de Hello en forma de mejor esfuerzo. Para obtener soporte para los dispositivos VPN, póngase en contacto con el fabricante.

|**Proveedor**          |**Familia de dispositivos**     |**Versión mínima de sistema operativo** |**Instrucciones de configuración PolicyBased** |**Instrucciones de configuración RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |No compatible  |[Guía de configuración](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |Enrutadores VPN de la serie AR |2.9.2                  |Próximamente     |No compatible  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall de la serie F |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Guía de configuración](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Guía de configuración](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall de la serie X |Barracuda Firewall 6.5 |[Guía de configuración](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |No compatible |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Guía de configuración](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |No compatible |
| Punto de comprobación |Security Gateway |R77.30 |[Guía de configuración](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Guía de configuración](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |No compatible |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Ejemplos de configuración*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 y superior |[Guía de configuración](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |No compatible |
| F5 |Serie BIG-IP |12.0 |[Guía de configuración](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Guía de configuración](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Guía de configuración](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Serie SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Guía de configuración](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |No compatible |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Serie J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Ejemplos de configuración](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Servicio de acceso remoto y enrutamiento |Windows Server 2012 |No compatible |[Ejemplos de configuración](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Mission Control Security Gateway |N/D |[Guía de configuración](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |No compatible |
| Openswan |Openswan |2.6.32 |(Próximamente) |No compatible |
| Palo Alto Networks |Todos los dispositivos que ejecutan PAN-OS |PAN-OS<br>PolicyBased: 6.1.5 o posterior<br>RouteBased: 7.1.4 |[Guía de configuración](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Guía de configuración](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |Serie TZ, serie NSA<br>Serie SuperMassive<br>Serie E-Class NSA |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Guía de configuración para SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guía de configuración para SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Guía de configuración para SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guía de configuración para SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Todo |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Guía de configuración](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Guía de configuración](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) Los enrutadores de la serie ISR 7200 solo admiten VPN PolicyBased.

## <a name="additionaldevices"></a>Dispositivos VPN no validados

Si no ve su dispositivo en la lista de tabla de dispositivos VPN validados hello, el dispositivo sigue puede funcionar con una conexión de sitio a sitio. Póngase en contacto con el fabricante del dispositivo para obtener instrucciones adicionales de soporte técnico y configuración.

## <a name="editing"></a>Edición de ejemplos de configuración de dispositivos

Después de descargar el ejemplo de configuración de dispositivo VPN Hola proporcionado, necesitará tooreplace algunos Hola valores de configuración de hello tooreflect para su entorno.

### <a name="tooedit-a-sample"></a>tooedit un ejemplo:

1. Abra el Bloc de notas de ejemplo de Hola.
2. Buscar y reemplazar todo <*texto*> cadenas con valores de hello que pertenezcan tooyour entorno. Ser seguro tooinclude < y >. Cuando se especifica un nombre, nombre de Hola que seleccione debe ser único. Si un comando no funciona, consulte la documentación del fabricante del dispositivo.

| **Texto de ejemplo** | **Cambiar a** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |Nombre elegido para este objeto. Ejemplo: miRedLocal |
| &lt;RP_AzureNetwork&gt; |Nombre elegido para este objeto. Ejemplo: miRedAzure |
| &lt;RP_AccessList&gt; |Nombre elegido para este objeto. Ejemplo: miListaAccesoAzure |
| &lt;RP_IPSecTransformSet&gt; |Nombre elegido para este objeto. Ejemplo: miConjuntoTransIPSec |
| &lt;RP_IPSecCryptoMap&gt; |Nombre elegido para este objeto. Ejemplo: miAsignCifradoIPSec |
| &lt;SP_AzureNetworkIpRange&gt; |Especifique el rango. Ejemplo: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Especifique la máscara de subred. Ejemplo: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Especifique el rango local. Ejemplo: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Especifique la máscara de subred local. Ejemplo: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Esta red virtual de tooyour específicas de información y se encuentra en el Portal de administración de hello como **dirección IP de puerta de enlace**. |
| &lt;SP_PresharedKey&gt; |Esta información es específica tooyour red virtual y se encuentra en hello Portal de administración como administrar la clave. |

## <a name="ipsec"></a>Parámetros de IPsec/IKE

> [!NOTE]
> Aunque se admiten valores de hello enumerados en hello en la tabla siguiente puerta de enlace de VPN de hello, actualmente no existe no es ningún mecanismo para toospecify o seleccione una combinación específica de algoritmos o los parámetros de puerta de enlace VPN de Hola. Debe especificar las restricciones de dispositivo VPN de hello local. Además, tiene que fijar el **tamaño de segmento máximo** en **1350**.
> 
>

Hola las tablas siguientes:

* SA = Asociación de seguridad
* La fase 1 de IKE también se denomina "Modo principal"
* La fase 2 de IKE también se denomina "Modo rápido"

### <a name="ike-phase-1-main-mode-parameters"></a>Parámetros de la fase 1 de IKE (Modo principal)

| **Propiedad**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Versión de IKE           |IKEv1              |IKEv2              |
| Grupo Diffie-Hellman  |Grupo 2 (1024 bits) |Grupo 2 (1024 bits) |
| Método de autenticación |Clave previamente compartida     |Clave previamente compartida     |
| Algoritmos de cifrado y hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Vigencia de SA           |28.800 segundos     |28.800 segundos     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Parámetros de la fase 2 de IKE (modo rápido)

| **Propiedad**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Versión de IKE                   |IKEv1          |IKEv2                                        |
| Algoritmos de cifrado y hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Ofertas de SA de QM del tipo routebased](#RouteBasedOffers) |
| Vigencia de SA (tiempo)            |3.600 segundos  |27 000 segundos                                |
| Vigencia de SA (bytes)           |102.400.000 KB | -                                           |
| Confidencialidad directa perfecta (PFS) |No             |[Ofertas de SA de QM del tipo routebased](#RouteBasedOffers) |
| Dead Peer Detection (DPD)     |No compatible  |Compatible                                    |


### <a name ="RouteBasedOffers"></a>Ofertas de asociación de seguridad de IPsec (SA de modo rápido de IKE) de VPN del tipo routebased

Hello tabla siguiente enumeran las ofertas de SA de IPsec (modo rápido IKE). Ofertas son orden Hola enumerados de preferencia se presentan dicha oferta de Hola o se acepta.

#### <a name="azure-gateway-as-initiator"></a>Puerta de enlace de Azure como iniciador

|-  |**Cifrado**|**Autenticación**|**Grupo PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |

#### <a name="azure-gateway-as-responder"></a>Puerta de enlace de Azure como respondedor

|-  |**Cifrado**|**Autenticación**|**Grupo PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |
| 7 |DES           |SHA1              |None         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20 ||AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |None         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* Puede especificar el cifrado IPsec ESP NULL con puertas de enlace de VPN RouteBased y HighPerformance. Cifrado basado en null no proporciona protección toodata en tránsito y solo se debe utilizar al máximo rendimiento y la mínima latencia es necesaria. Los clientes pueden decidir toouse esto en escenarios de comunicación de red virtual a red virtual, o cuando se aplica el cifrado en otra parte de solución de Hola.
* Para la conectividad entre entornos a través de Internet de hello, use configuración de puerta de enlace de VPN de Azure de hello predeterminado con cifrado y algoritmos hash que se enumeran en las tablas de hello anteriormente tooensure de seguridad de sus comunicaciones críticas.

## <a name="known"></a>Problemas conocidos de compatibilidad de dispositivos

> [!IMPORTANT]
> Estos son Hola problemas de compatibilidad conocidos entre los dispositivos VPN de terceros y puertas de enlace VPN de Azure. Hola, equipo de Azure está trabajando activamente con los proveedores de hello tooaddress Hola problemas se enumeran aquí. Una vez que se resuelven los problemas de hello, esta página se actualizará con la información más actualizada de Hola. Consúltela periódicamente.
>
>

### <a name="feb-16-2017"></a>16 de febrero de 2017

**Dispositivos de redes de Palo Alto con la versión anterior too7.1.4** para VPN basadas en enrutamiento Azure: si se usan dispositivos VPN de Palo Alto Networks con too7.1.4 de PAN-OS versión anterior y que experimenta conectividad emite tooAzure basadas en enrutamiento puertas de enlace VPN, lleve a cabo Hola pasos:

1. Comprobar la versión de firmware de hello de dispositivo Palo Alto Networks. Si la versión de SO del molde es anterior a 7.1.4, actualizar too7.1.4.
2. En dispositivos de redes de Palo Alto hello, cambiar too28 de duración de SA de fase 2 (o SA de modo rápido) hello, 800 segundos (8 horas) al conectarse toohello puerta de enlace de VPN de Azure.
3. Si sigue experimentando problemas de conectividad, abra una solicitud de soporte técnico de hello portal de Azure.
