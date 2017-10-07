---
title: aaaTroubleshoot Azure VPN de sitio a sitio se desconecta de forma intermitente | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot Hola problema de conexión de VPN de sitio a sitio que Hola desconectado con regularidad."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Solución de problemas: la VPN de sitio a sitio de Azure se desconecta intermitentemente

Puede experimentar problemas de Hola que una conexión de Azure de Microsoft Point-to-Site VPN nueva o existente no es estable o desconecta con regularidad. Este artículo se proporcionan pasos toohelp identificar y resolver Hola causa del problema de Hola de solución de problemas. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas

### <a name="prerequisite-step"></a>Paso de requisito previo

Seleccione el tipo de saludo de puerta de enlace de red virtual de Azure:

1. Vaya demasiado[portal de Azure](https://portal.azure.com).
2. Comprobar hello **Introducción** página de puerta de enlace de red virtual de Hola para obtener información de tipo hello.
    
    ![información general de Hola de puerta de enlace de Hola](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Paso 1 Compruebe si se valida el dispositivo VPN en local de Hola

1. Compruebe si está usando una [versión del sistema operativo y dispositivo VPN validada](vpn-gateway-about-vpn-devices.md#devicetable). Si no se valida el dispositivo VPN de hello, puede tener toocontact Hola dispositivo fabricante toosee si hay algún problema de compatibilidad.
2. Asegúrese de que el dispositivo VPN Hola está configurado correctamente. Para obtener más información, vea [Edición de ejemplos de configuración de dispositivos](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Paso 2 parámetros de asociación de seguridad Hola de comprobación (para las puertas de enlace de red virtual Azure basada en directivas)

1. Asegúrese de que Hola red virtual, subredes y los intervalos de hello **puerta de enlace de red Local** definición en Microsoft Azure son los mismos que configuración de hello en dispositivo VPN de hello local.
2. Compruebe a que coinciden con la configuración de asociación de seguridad de Hola.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Paso 3: Comprobación de los grupos de seguridad de red o las rutas definidas por el usuario en la subred de puerta de enlace

Una ruta de subred de puerta de enlace de hello definido por el usuario se puede restringir el tráfico y lo que permite el tráfico restante. Esto hace parecer que la conexión de VPN de hello es confiable para parte del tráfico y conveniente que otros usuarios. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Paso 4 verificación Hola "un túnel de VPN por cada par de subred" (para las puertas de enlace de red virtual basada en directivas)

Asegúrese de que el dispositivo VPN se establece toohave en local de ese hello **un túnel VPN por cada par de subred** para puertas de enlace de red virtual basada en directivas.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Paso 5: Comprobación de la limitación de la asociación de seguridad (para puertas de enlace de red virtual basadas en directivas)

puerta de enlace de red virtual basada en directivas de Hello tiene un límite de 200 pares de asociación de seguridad de subred. Si multiplica por número de Hola de subredes de red virtual de Azure Hola número de subredes locales es mayor que 200, verá esporádicos subredes desconectar.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Paso 6: Comprobación de la dirección de la interfaz externa del dispositivo VPN local

- Si hello orientado a la dirección IP del dispositivo VPN de hello Internet se incluye en hello **puerta de enlace de red Local** definición en Azure, puede experimentar desconexiones esporádicos.
- Hello debe ser interfaz externa del dispositivo directamente en hello Internet. No debería haber ninguna traducción de direcciones de red (NAT) o un firewall entre Hola Internet y el dispositivo de Hola.
-  Si configura una dirección IP virtual toohave de agrupación en clústeres de servidor de seguridad, debe interrumpir clúster hello y exponer el dispositivo VPN de hello directamente tooa interfaz pública que Hola puerta de enlace puede comunicarse con.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Paso 7 Compruebe si el dispositivo VPN tiene confidencialidad directa perfecta habilitado a local de Hola

Hola **confidencialidad directa perfecta** característica puede causar problemas de desconexión de Hola. Si el dispositivo VPN hello tiene **confidencialidad directa perfecta** habilitado, deshabilite la característica de Hola. A continuación, [actualizar directiva de IPsec de puerta de enlace de red virtual de hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Pasos siguientes

- [Configurar una red virtual de sitio a sitio conexión tooa](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Configuración de la directiva IPsec/IKE para conexiones VPN de sitio a sitio](vpn-gateway-ipsecikepolicy-rm-powershell.md)

