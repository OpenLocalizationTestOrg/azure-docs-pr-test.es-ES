---
title: "aaaTroubleshoot una conexión de VPN de sitio a sitio Azure que no se puede conectar | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot una conexión de VPN de sitio a sitio que de repente deja de funcionar y no se puede volver a conectar."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Solución de problemas: la conexión VPN de sitio a sitio de Azure no puede conectarse y deja de funcionar

Después de configurar una conexión de VPN de sitio a sitio entre una red local y una red virtual de Azure, Hola conexión VPN de repente deja de funcionar y no se puede volver a conectar. Este artículo proporciona toohelp de pasos de solución de problemas para resolver este problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas

problema de hello tooresolve, en primer lugar intente demasiado[puerta de enlace de VPN de Azure de Hola de restablecimiento](vpn-gateway-resetgw-classic.md) y restablecer el túnel de hello de dispositivo VPN de hello local. Si persiste el problema de hello, siga estos hacen que hello tooidentify pasos de problema de Hola.

### <a name="prerequisite-step"></a>Paso de requisito previo

Comprobar el tipo de saludo de puerta de enlace de VPN de Azure de Hola.

1. Vaya toohello [portal de Azure](https://portal.azure.com).

2. Comprobar hello **Introducción** página de puerta de enlace VPN de Hola para obtener información de tipo hello.
    
    ![Información general de puerta de enlace de Hola](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Paso 1. Compruebe si se valida el dispositivo VPN de hello local

1. Compruebe si está usando una [versión del sistema operativo y dispositivo VPN validada](vpn-gateway-about-vpn-devices.md#devicetable). Si Hola dispositivo no es un dispositivo VPN validado, podría tener toocontact Hola dispositivo fabricante toosee si hay un problema de compatibilidad.

2. Asegúrese de que el dispositivo VPN Hola está configurado correctamente. Para más información, consulte [Ejemplos de edición de configuración de dispositivos](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Paso 2: Compruebe la clave compartida de Hola

Compare la clave compartida de Hola Hola local VPN dispositivo toohello VPN de red Virtual de Azure toomake seguro de que coinciden con las claves de Hola. 

tooview Hola una clave compartida para hello conexión VPN de Azure, use uno de los siguientes métodos de hello:

**Portal de Azure**

1. Vaya toohello conexión de sitio a sitio de puerta de enlace VPN que ha creado.

2. Hola **configuración** sección, haga clic en **clave compartida**.
    
    ![Clave compartida](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Para el modelo de implementación de hello Azure Resource Manager:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Para el modelo de implementación clásica de hello:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Paso 3: Comprobar del mismo nivel de hello VPN direcciones IP

-   Hola definición de IP en hello **puerta de enlace de red Local** objeto en Azure debe coincidir con la IP del dispositivo local Hola.
-   definición de IP de puerta de enlace de Azure que está establecido en Hola Hola local dispositivo debe coincidir con la IP de puerta de enlace de Azure de Hola.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Paso 4 Compruebe UDR y NSG de subred de puerta de enlace de Hola

Busque y quite enrutamiento definido por el usuario (UDR) o grupos de seguridad de red (NSG) en la subred de puerta de enlace de hello y, a continuación, el resultado de hello de pruebas. Si se resuelve el problema de hello, validar la configuración de Hola que aplica UDR o NSG.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Paso 5. Hola de comprobación de dirección de interfaz externa del dispositivo VPN local

- Si se incluye Hola dirección IP de conexión a Internet del dispositivo VPN de hello en hello **red Local** definición en Azure, podría experimentar desconexiones esporádicos.
- Hello debe ser interfaz externa del dispositivo directamente en hello Internet. No debería haber ningún firewall entre Hola Internet y el dispositivo de Hola o traducción de direcciones de red.
- tooconfigure firewall toohave agrupación en clústeres una dirección IP virtual, debe interrumpir clúster hello y exponer el dispositivo VPN de hello directamente la interfaz pública de tooa esa puerta de enlace de hello puede comunicarse con.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Paso 6. Compruebe que las subredes de hello coinciden exactamente (Azure basada en directivas con puertas de enlace)

-   Compruebe que las subredes de hello coinciden exactamente entre Hola red virtual de Azure y las definiciones de local de hello red virtual de Azure.
-   Compruebe que las subredes de hello coinciden exactamente entre hello **puerta de enlace de red Local** y definiciones de red local de hello en local.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Paso 7. Compruebe el sondeo de estado de Azure de la puerta de enlace de Hola

1. Vaya toohello [sondeo de estado](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Haga clic en a través de advertencia de certificado de Hola.
3. Si recibe una respuesta, la puerta de enlace VPN de Hola se considera correcta. Si no recibe una respuesta, puerta de enlace de hello no sea correcto o un NSG de subred de puerta de enlace de hello está causando el problema de Hola. Hola después de texto es una respuesta de ejemplo:

    &lt;?xml version="1.0"?&gt; <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6&lt;/string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Paso 8. Compruebe si Hola local dispositivo VPN tenga habilitada la característica de confidencialidad directa total de Hola

características de confidencialidad directa total Hola pueden causar problemas de desconexión. Si el dispositivo VPN de hello tiene confidencialidad directa total habilitada, deshabilite la característica de Hola. A continuación, actualice la directiva de IPsec de puerta de enlace VPN de Hola.

## <a name="next-steps"></a>Pasos siguientes

-   [Configurar una red virtual de tooa de conexión de sitio a sitio](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Configuración de una directiva IPsec/IKE para conexiones VPN de sitio a sitio](vpn-gateway-ipsecikepolicy-rm-powershell.md)
