---
title: escenarios de aaaAdvanced con Azure MFA y VPN de terceros
description: "Guías de configuración paso a paso para Azure MFA toointegrate con Citrix, Cisco y Juniper."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Escenarios avanzados con Azure Multi-Factor Authentication y soluciones de VPN de terceros
Puede utilizarse la autenticación multifactor Azure tooseamlessly conectarse con varias soluciones VPN de terceros. En este artículo se centra en el dispositivo VPN de Cisco® ASA y dispositivo VPN de SSL de NetScaler de Citrix, Hola redes proteger acceso/Pulse Secure conectarse seguros dispositivo Juniper SSL VPN. Hemos creado tooaddress de guías de configuración de estos tres dispositivos comunes, pero puede integrar el servidor de autenticación multifactor con la mayoría de los sistemas que utilizan RADIUS, LDAP, IIS o autenticación basada en notificaciones tooAD FS. Puede encontrar más detalles en las [configuraciones de Servidor MFA](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Aplicación VPN de Cisco ASA y Azure Multi-Factor Authentication
La autenticación multifactor Azure se integra con la VPN de Cisco® ASA dispositivo tooprovide una seguridad adicional para los inicios de sesión de Cisco AnyConnect® VPN y acceso al portal.  Esto puede hacerse mediante cualquier protocolo LDAP o RADIUS Hola.  Seleccione uno de hello después toodownload Hola detallada paso a paso de la configuración le guía.

| Guía de configuración | Description |
| --- | --- |
| [Configuración de Cisco ASA con Anyconnect VPN y Azure MFA para LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Integración de la aplicación VPN de Cisco ASA con Azure MFA mediante LDAP |
| [Configuración de Cisco ASA con Anyconnect VPN y Azure MFA para RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Integración perfecta de la aplicación VPN de Cisco ASA con Azure MFA mediante RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>VPN SSL de Citrix NetScaler y Azure Multi-Factor Authentication
La autenticación multifactor Azure se integra con la VPN de SSL de Citrix NetScaler dispositivo tooprovide una seguridad adicional para los inicios de sesión de Citrix NetScaler SSL VPN y acceso al portal.  Esto puede hacerse mediante cualquier protocolo LDAP o RADIUS Hola.  Seleccione uno de hello después toodownload Hola detallada paso a paso de la configuración le guía.

| Guía de configuración | Description |
| --- | --- |
| [Configuración de VPN SSL de Citrix NetScaler y Azure MFA para LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Integración de su VPN SSL de Citrix NetScaler con la aplicación de Azure MFA mediante LDAP |
| [Configuración de VPN SSL de Citrix NetScaler y Azure MFA para RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Integración de su aplicación VPN SSL de Citrix NetScaler con Azure MFA mediante RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Aplicación VPN SSL de Juniper/Pulse Secure y Azure Multi-Factor Authentication
La autenticación multifactor Azure se integra con la VPN de SSL de Juniper/Pulse Secure dispositivo tooprovide una seguridad adicional para los inicios de sesión de Juniper/Pulse Secure SSL VPN y acceso al portal.  Esto puede hacerse mediante cualquier protocolo LDAP o RADIUS Hola.  Seleccione uno de hello después toodownload Hola detallada paso a paso de la configuración le guía.

| Guía de configuración | Description |
| --- | --- |
| [Configuración de VPN SSL de Juniper/Pulse Secure y Azure MFA para LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Integración de su VPN SSL de Juniper/Pulse Secure con la aplicación de Azure MFA mediante LDAP |
| [Configuración de VPN SSL de Juniper/Pulse Secure y Azure MFA para RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Integración de su VPN SSL de Juniper/Pulse Secure con Azure MFA mediante RADIUS |

## <a name="next-steps"></a>Pasos siguientes

- [Aumentar la infraestructura de autenticación existente con hello extensión NPS para la autenticación multifactor de Azure](multi-factor-authentication-nps-extension.md)

- [Configuración de Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)