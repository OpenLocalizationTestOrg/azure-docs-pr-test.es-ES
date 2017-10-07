---
title: "configuración de aaaSample - dispositivos Cisco ASA conectar las puertas de enlace VPN de tooAzure | Documentos de Microsoft"
description: "Este artículo proporciona un ejemplo de configuración para dispositivos Cisco ASA conectar las puertas de enlace VPN de tooAzure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Ejemplo de configuración: dispositivo Cisco ASA (IKEv2/no BGP)
Este artículo proporciona ejemplos de configuraciones para dispositivos Cisco ASA conectar las puertas de enlace VPN de tooAzure.

## <a name="device-at-a-glance"></a>Detalles del dispositivo

|                        |                                   |
| ---                    | ---                               |
| Fabricante del dispositivo          | Cisco                             |
| Modelo de dispositivo           | ASA (Adaptive Security Appliance) |
| Versión de destino         | 8.4+                              |
| Modelo probado           | ASA 5505                          |
| Versión probada         | 9.2                               |
| Versión de IKE            | **IKEv2**                         |
| BGP                    | **No**                            |
| Tipo de puerta de enlace de VPN de Azure | Puerta de enlace de VPN **basada en rutas**       |
|                        |                                   |

> [!NOTE]
> 1. configuración de Hola a continuación conecta a un tooan de dispositivos Cisco ASA Azure **basadas en enrutamiento** puerta de enlace VPN mediante la directiva personalizada de IPsec/IKE con la opción "UserPolicyBasedTrafficSelectors", como se describe en [este artículo](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. Requiere ASA dispositivos toouse **IKEv2** con las configuraciones basadas en lista de acceso, no basada en VTI.
> 3. Póngase en contacto con las especificaciones de proveedor de dispositivo VPN directiva de Hola de tooensure es compatible con los dispositivos VPN local.

## <a name="vpn-device-requirements"></a>Requisitos del dispositivo VPN
Puertas de enlace VPN Azure usar túneles de VPN de S2S de tooestablish conjuntos de protocolo de IPsec/IKE estándares. Consulte demasiado[dispositivos VPN sobre](vpn-gateway-about-vpn-devices.md) para hello detallado parámetros de protocolo IPsec/IKE y algoritmos criptográficos predeterminados para las puertas de enlace de VPN de Azure. Puede especificar opcionalmente Hola exactamente la combinación de algoritmos criptográficos y las ventajas claves para una conexión específica, como se describe en [sobre los requisitos de cifrado](vpn-gateway-about-compliance-crypto.md). Si selecciona una combinación específica de algoritmos criptográficos y las ventajas claves, asegúrese de que usar correspondientes especificaciones de hello en los dispositivos VPN.

## <a name="single-vpn-tunnel"></a>Un solo túnel VPN
Esta topología consta de un solo túnel VPN S2S entre una puerta de enlace de VPN de Azure y el dispositivo VPN local. Opcionalmente puede configurar BGP a través del túnel VPN de Hola.

![túnel único](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Consulte demasiado[el programa de instalación único túnel](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) para obtener, instrucciones paso a paso toobuild Hola configuraciones de Azure.

### <a name="network-and-vpn-gateway-information"></a>Información de puerta de enlace de VPN y de red
En esta sección se indican los parámetros de Hola para hello en este ejemplo.

| **Parámetro**                | **Valor**                    |
| ---                          | ---                          |
| Prefijos de dirección de red virtual        | 10.11.0.0/16<br>10.12.0.0/16 |
| IP de la puerta de enlace de VPN de Azure         | Azure_Gateway_Public_IP      |
| Prefijos de direcciones locales | 10.51.0.0/16<br>10.52.0.0/16 |
| Dirección IP del dispositivo VPN local    | OnPrem_Device_Public_IP     |
| *ASN de BGP de red virtual                | 65010                        |
| *Dirección IP del par BGP de Azure           | 10.12.255.30                 |
| *ASN de BGP local         | 65050                        |
| *Dirección IP del par BGP local     | 10.52.255.254                |
|                              |                              |

* (*) Parámetros opcionales solo para BGP.

### <a name="ipsecike-policy--parameters"></a>Parámetros y directivas de IPsec o IKE

tabla de Hello siguiente contiene algoritmos de IPsec/IKE de Hola y parámetros utilizados en el ejemplo de Hola. Consulte la toomake de especificaciones de dispositivo VPN que todos los algoritmos enumerados anteriormente son compatibles con los modelos de dispositivo VPN y las versiones de firmware.

| **IPsec o IKEv2**  | **Valor**                            |
| ---              | ---                                  |
| Cifrado IKEv2 | AES256                               |
| Integridad de IKEv2  | SHA384                               |
| Grupo DH         | DHGroup24                            |
| Cifrado IPsec | AES256                               |
| Integridad de IPsec  | SHA1                                 |
| Grupo PFS        | PFS24                                |
| Vigencia de SA (QM)   | 7200 segundos                         |
| Selector de tráfico | UsePolicyBasedTrafficSelectors $True |
| Clave previamente compartida   | PreSharedKey                         |
|                  |                                      |

- (*) En algunos dispositivos, la integridad de IPsec debe ser "null" si se usa AES GCM como algoritmo de cifrado de IPsec.

### <a name="device-notes"></a>Notas del dispositivo

>[!NOTE]
>
> 1. La compatibilidad con IKEv2 requiere ASA versión 8.4 y versiones posteriores.
> 2. La compatibilidad con grupos DH y PFS superiores (por encima del Grupo 5) requiere la versión ASA 9.x.
> 3. Cifrado IPsec con AES-GCM e integridad IPsec con compatibilidad con SHA-256, SHA-384, SHA-512 requiere la versión ASA 9.x en el hardware ASA más reciente; **no** se admite ASA 5505, 5510, 5520, 5540, 5550, 5580. (Compruebe Hola proveedor especificaciones tooconfirm.)
>


### <a name="sample-device-configurations"></a>Ejemplos de configuraciones de dispositivo
script de Hola siguiente proporciona un ejemplo de configuración en función de la topología de Hola y los parámetros mencionados anteriormente. configuración de un túnel VPN S2S Hola consta de hello siguientes componentes:

1. Interfaces y rutas
2. Listas de acceso
3. Directiva y parámetros de IKE (Fase 1 o Modo principal)
4. Directiva y parámetros de IPsec (Fase 2 o Modo rápido)
5. Otros parámetros (bloqueo MSS de TCP, etc.)

>[!IMPORTANT] 
>Asegúrese de completar la configuración adicional de hello enumerada a continuación y reemplace los marcadores de posición de hello con valores reales de hello:
> 
> - Configuración de interfaz para interfaces internas y externas
> - Rutas para las redes internas o privadas, y públicas o externas
> - Asegúrese de que todos los nombres y números de directiva son únicos en el dispositivo de Hola
> - Asegúrese de que se admiten los algoritmos criptográficos de hello en el dispositivo
> - Reemplace Hola siguientes marcadores de posición con valores reales de Hola
>   - Nombre de la interfaz externa: "outside"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - Pre_Shared_Key de IKE
>   - Nombres de la red virtual y la puerta de enlace de red local (VNetName, LNGName)
>   - Prefijos de direcciones de red de la red virtual y local
>   - Máscaras de red correctas

#### <a name="sample-configuration"></a>Configuración de ejemplo

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Comandos de depuración simples

Estos son algunos comandos de ASA para fines de depuración:

1. Mostrar Hola IPsec e IKE SA
    - "show crypto ipsec sa"
    - "show crypto ikev2 sa"
2. Al escribir el modo de depuración: Esto puede obtener con mucho ruido en la consola de Hola
    - "debug crypto ikev2 platform <level>"
    - "debug crypto ikev2 protocol <level>"
3. Enumerar configuraciones actuales
    - "show ejecución" - muestra Hola configuraciones actuales en el dispositivo de hello; Puede usar Hola varios subcomandos toolist determinadas partes de configuración de Hola. Por ejemplo, "show run crypto", "show run access-list", "show run tunnel-group", etc.


## <a name="next-steps"></a>Pasos siguientes
Vea [configuración activo / activo VPN las puertas de enlace para las conexiones de red virtual a red virtual y entre entornos](vpn-gateway-activeactive-rm-powershell.md) para las conexiones de red virtual a red virtual y pasos tooconfigure de activo / activo entre entornos.

