---
title: compatibilidad con aaaWebSocket en puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello compatibilidad con websocket para puerta de enlace de aplicaciones."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>Introducción a la compatibilidad de WebSocket en Application Gateway

Application Gateway proporciona una compatibilidad nativa con WebSocket en todas las puertas de enlace, con independencia de su tamaño. No hay ningún valor configurable por el usuario tooselectively habilitar o deshabilitar compatibilidad con WebSocket. 

El protocolo WebSocket, estándar en [RFC6455](https://tools.ietf.org/html/rfc6455) , permite una comunicación dúplex completa entre un servidor y un cliente a través de una conexión TCP de larga duración. Esta característica permite una comunicación entre el servidor web de Hola y el cliente de hello, que puede ser bidireccional, sin necesidad de hello para el sondeo como obligatorio en implementaciones basadas en HTTP más interactiva. WebSocket tiene baja sobrecarga a diferencia de HTTP y puede reutilizar Hola mismo conexión TCP de varias solicitudes/respuestas resultante en un uso más eficaz de recursos. Protocolos de WebSocket son toowork diseñada a través de puertos HTTP tradicionales de 80 y 443.

Puede seguir utilizando un agente de escucha HTTP estándar en el puerto 80 o 443 tooreceive tráfico de WebSocket. Tráfico de WebSocket es dirigido toohello WebSocket habilita el servidor back-end con grupo de back-end adecuados de Hola tal como se especifica en las reglas de puerta de enlace de aplicaciones. servidor de back-end de Hello debe responder sondeos de puerta de enlace de aplicación toohello, que se describen en hello [información general de sondeo de estado](application-gateway-probe-overview.md) sección. Los sondeos del estado de Application Gateway son solo HTTP o HTTPS. Cada servidor de back-end debe responder sondeos tooHTTP puerta de enlace tooroute WebSocket tráfico toohello para servidor de aplicaciones.

## <a name="listener-configuration-element"></a>Elemento de configuración de agente de escucha

Un agente de escucha HTTP existente puede ser usado toosupport tráfico de WebSocket. Hola aquí te mostramos un fragmento de código de un elemento de httpListeners desde un archivo de plantilla de ejemplo. ¿Necesita toosupport de agentes de escucha HTTP y HTTPS WebSocket y proteger el tráfico de WebSocket. Del mismo modo puede usar hello [portal](application-gateway-create-gateway-portal.md) o [PowerShell](application-gateway-create-gateway-arm.md) toocreate una puerta de enlace de la aplicación con los agentes de escucha de tráfico en el puerto 80/443 toosupport WebSocket.

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>Configuración de reglas de enrutamiento, BackendHttpSetting y BackendAddressPool

Un BackendAddressPool es toodefine utilizado un grupo back-end con servidores de WebSocket habilitado. Hola backendHttpSetting se define con un puerto de back-end 80 y 443. propiedades de Hola para afinidad basado en cookies y requestTimeouts no son relevantes tooWebSocket tráfico. Hay ningún cambio necesario en la regla de enrutamiento de hello, "Básica" es tootie usado Hola agentes de escucha adecuada toohello correspondiente grupo de direcciones de back-end. 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>Back-end con WebSocket habilitado

El back-end debe tener un servidor de web HTTP/HTTPS con hello configurado el puerto (normalmente 80/443) para toowork de WebSocket. Este requisito es porque requiere de protocolo WebSocket toobe de protocolo de enlace inicial de hello HTTP con el protocolo de actualización tooWebSocket como un campo de encabezado. Hola te mostramos un ejemplo de un encabezado:

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

Otro de los motivos es que el sondeo del estado del back-end de la puerta de enlace de aplicaciones solo admite los protocolos HTTP y HTTPS. Si el servidor de back-end de hello no responde tooHTTP o sondeos HTTPS, que se saca del grupo back-end.

## <a name="next-steps"></a>Pasos siguientes

Después de aprendizaje sobre la compatibilidad con WebSocket, vaya demasiado[crear una puerta de enlace de la aplicación](application-gateway-create-gateway.md) tooget a trabajar con un WebSocket la aplicación web habilitada.

