---
title: "aaaDiagnose conectividad de local a través de puerta de enlace VPN con Monitor de red de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo toodiagnose local conectividad a través de puerta de enlace VPN con la solución de problemas de recursos de Monitor de red de Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnóstico de la conectividad local a través de puertas de enlace de VPN

Puerta de enlace de VPN de Azure permite solución híbrida de toocreate necesidades de Hola para una conexión segura entre su red local y la red virtual de Azure. Como sus requisitos son únicos, por lo que es la opción de hello de dispositivo VPN local. Azure admite actualmente [varios dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) que constantemente se validan en colaboración con proveedores de dispositivos de Hola. Revise los valores de configuración específicos de dispositivo de hello antes de configurar el dispositivo VPN local. Igualmente, Azure VPN Gateway está configurado con un conjunto de [parámetros de IPsec admitidos](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) que se utilizan para establecer conexiones. Actualmente no hay ninguna manera de toospecify o seleccione una combinación específica de parámetros de IPsec de hello puerta de enlace de VPN de Azure. Para establecer una conexión correcta entre local y Azure, Hola local de configuración del dispositivo VPN deberá ser conformes con los parámetros de IPsec Hola prescritos por puerta de enlace de VPN de Azure. Si hello configuración es correcta, hay una pérdida de conectividad y hasta ahora para solucionar estos problemas, no es trivial y normalmente tardó horas problema hello tooidentify y corrección.

Con Monitor de red de Azure hello solucionar problemas de característica, es capaz de toodiagnose cualquier problema con la puerta de enlace y las conexiones y en minutos tiene suficiente toomake información un problema de hello toorectify decisión informada.

## <a name="scenario"></a>Escenario

Desea conexión tooconfigure un sitio a sitio entre Azure y locales mediante FortiGate como Hola puerta de enlace de VPN local. tooachieve este escenario, necesitaría Hola después de la instalación:

1. Puerta de enlace de red virtual: Hola puerta de enlace de VPN en Azure
1. Puerta de enlace de red local - Hola [(FortiGate) puerta de enlace de VPN local](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) representación en la nube de Azure
1. Conexión de sitio a sitio (basado en directiva) - [conexión entre la puerta de enlace VPN de Hola y Hola enrutador local](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Configuración de FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Encontrará instrucciones paso a paso detalladas para establecer una configuración de sitio a sitio, visita: [crear una red virtual con una conexión de sitio a sitio mediante el portal de Azure de hello](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Uno de los pasos de configuración crítica de hello es la configuración de parámetros de comunicación de IPsec de hello, cualquier error de configuración conduce tooloss de conectividad entre la red local de Hola y Azure. Actualmente, las puertas de enlace VPN de Azure son hello toosupport configurado siguiendo los parámetros de IPsec durante la fase 1. Tenga en cuenta que, como ya se mencionó anteriormente, esta configuración no se puede modificar.  Como puede ver en la siguiente tabla se hello, algoritmos de cifrado de hello admitidos por la puerta de enlace de VPN de Azure son AES256 y AES128, 3DES.

### <a name="ike-phase-1-setup"></a>Configuración de la fase 1 de IKE

| **Propiedad** | **PolicyBased** | **Puerta de enlace de VPN de alto rendimiento o estándar y RouteBased** |
| --- | --- | --- |
| Versión de IKE |IKEv1 |IKEv2 |
| Grupo Diffie-Hellman |Grupo 2 (1024 bits) |Grupo 2 (1024 bits) |
| Método de autenticación |Clave previamente compartida |Clave previamente compartida |
| Algoritmos de cifrado |AES256 AES128 3DES |AES256 3DES |
| Algoritmo hash |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Vida útil (tiempo) de la asociación de seguridad (SA) de la fase 1 |28.800 segundos |10.800 segundos |

Como un usuario, sería necesario tooconfigure su FortiGate, un ejemplo de configuración puede encontrarse en [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Sin saberlo configuró su toouse FortiGate SHA-512 como Hola algoritmo hash. Como este algoritmo no es un algoritmo compatible con las conexiones basadas en directivas, la conexión VPN funciona.

Estos problemas son tootroubleshoot de disco duro y causas raíz suelen ser poco intuitivo. En este caso, puede abrir una ayuda de soporte técnico de vale tooget acerca de cómo resolver el problema de Hola. Pero con la API de solución de problemas de Azure Network Watcher puede identificar estos problemas por su cuenta.

## <a name="troubleshooting-using-azure-network-watcher"></a>Solución de problemas mediante Azure Network Watcher

toodiagnose la conexión, conectar tooAzure PowerShell e iniciar hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. Puede encontrar Hola detalles sobre el uso de este cmdlet en [solucionar problemas de la puerta de enlace de red Virtual y conexiones, PowerShell](network-watcher-troubleshoot-manage-powershell.md). Este cmdlet puede tardar toofew minutos toocomplete.

Una vez completado el cmdlet de hello, puede navegar toohello ubicación de almacenamiento especificada en cmdlet hello tooget información detallada en sobre el problema de Hola y los registros. Monitor de red de Azure crea una carpeta zip que contiene los siguientes archivos de registro de hello:

![1][1]

Archivo de hello abierto denominado IKEErrors.txt y muestra hello siguiente error, que indica un problema con una configuración incorrecta de IKE configuración local.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Puede obtener información detallada de hello Scrubbed wfpdiag.txt sobre error de hello, como en este caso menciona que ha habido `ERROR_IPSEC_IKE_POLICY_MATCH` ese tooconnection responsable no funciona correctamente.

Otro error de configuración común es hello especificar claves compartidas incorrectas. En el caso de hello anterior ejemplo hubiera especificado diferentes claves compartidas, hello IKEErrors.txt muestra hello siguiente error: `Error: Authentication failed. Check shared key`.

Característica de solución de problemas de Monitor de red de Azure permite toodiagnose y solucionar problemas de la puerta de enlace de VPN y la conexión con facilidad Hola de un sencillo cmdlet de PowerShell. Actualmente se admite Hola diagnosticar condiciones siguientes y están trabajando para agregar condición más.

### <a name="gateway"></a>Puerta de enlace

| Tipo de error | Motivo | Registro|
|---|---|---|
| NoFault | Cuando no se detecta ningún error. |Sí|
| GatewayNotFound | No se encuentra la puerta de enlace o no está aprovisionada. |No|
| PlannedMaintenance |  La instancia de puerta de enlace está en mantenimiento.  |No|
| UserDrivenUpdate | Cuando hay una actualización del usuario en curso. Podría tratarse de una operación de cambio de tamaño. | No |
| VipUnResponsive | No se puede llegar a la instancia principal de Hola de hello puerta de enlace. Esto sucede cuando se produce un error de sondeo de estado de Hola. | No |
| PlatformInActive | Hay un problema con la plataforma de Hola. | No|
| ServiceNotRunning | no se está ejecutando el servicio subyacente Hola. | No|
| NoConnectionsFoundForGateway | No hay ninguna conexión existe en la puerta de enlace de Hola. Esto es solo una advertencia.| No|
| ConnectionsNotConnected | Ninguna de las conexiones de hello están conectada. Esto es solo una advertencia.| Sí|
| GatewayCPUUsageExceeded | uso actual de puerta de enlace de Hello el uso de CPU es > 95%. | Sí |

### <a name="connection"></a>Conexión

| Tipo de error | Motivo | Registro|
|---|---|---|
| NoFault | Cuando no se detecta ningún error. |Sí|
| GatewayNotFound | No se encuentra la puerta de enlace o no está aprovisionada. |No|
| PlannedMaintenance | La instancia de puerta de enlace está en mantenimiento.  |No|
| UserDrivenUpdate | Cuando hay una actualización del usuario en curso. Podría tratarse de una operación de cambio de tamaño.  | No |
| VipUnResponsive | No se puede llegar a la instancia principal de Hola de hello puerta de enlace. Se produce cuando se produce un error de sondeo de estado de Hola. | No |
| ConnectionEntityNotFound | Falta una configuración de conexión. | No |
| ConnectionIsMarkedDisconnected | Hola conexión está marcada como "desconectada". |No|
| ConnectionNotConfiguredOnGateway | servicio de Hello subyacente no tiene Hola que conexión configurada. | Sí |
| ConnectionMarkedStandy | Hola servicio subyacente está marcada como en espera.| Sí|
| Autenticación | Error de coincidencia de clave previamente compartida. | Sí|
| PeerReachability | puerta de enlace de Hello del mismo nivel no está accesible. | Sí|
| IkePolicyMismatch | puerta de enlace de Hello del mismo nivel tiene directivas IKE que no son compatibles con Azure. | Sí|
| Error de WfpParse | Error al registro WFP Hola análisis. |Sí|

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de conectividad de puerta de enlace VPN toocheck con PowerShell y automatización de Azure visitando [puertas de enlace de VPN de Monitor con la solución de problemas de Monitor de red de Azure](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
