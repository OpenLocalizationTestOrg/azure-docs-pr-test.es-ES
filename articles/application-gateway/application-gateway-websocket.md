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
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="72034-103">Introducción a la compatibilidad de WebSocket en Application Gateway</span><span class="sxs-lookup"><span data-stu-id="72034-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="72034-104">Application Gateway proporciona una compatibilidad nativa con WebSocket en todas las puertas de enlace, con independencia de su tamaño.</span><span class="sxs-lookup"><span data-stu-id="72034-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="72034-105">No hay ningún valor configurable por el usuario tooselectively habilitar o deshabilitar compatibilidad con WebSocket.</span><span class="sxs-lookup"><span data-stu-id="72034-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="72034-106">El protocolo WebSocket, estándar en [RFC6455](https://tools.ietf.org/html/rfc6455) , permite una comunicación dúplex completa entre un servidor y un cliente a través de una conexión TCP de larga duración.</span><span class="sxs-lookup"><span data-stu-id="72034-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="72034-107">Esta característica permite una comunicación entre el servidor web de Hola y el cliente de hello, que puede ser bidireccional, sin necesidad de hello para el sondeo como obligatorio en implementaciones basadas en HTTP más interactiva.</span><span class="sxs-lookup"><span data-stu-id="72034-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="72034-108">WebSocket tiene baja sobrecarga a diferencia de HTTP y puede reutilizar Hola mismo conexión TCP de varias solicitudes/respuestas resultante en un uso más eficaz de recursos.</span><span class="sxs-lookup"><span data-stu-id="72034-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="72034-109">Protocolos de WebSocket son toowork diseñada a través de puertos HTTP tradicionales de 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="72034-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="72034-110">Puede seguir utilizando un agente de escucha HTTP estándar en el puerto 80 o 443 tooreceive tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="72034-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="72034-111">Tráfico de WebSocket es dirigido toohello WebSocket habilita el servidor back-end con grupo de back-end adecuados de Hola tal como se especifica en las reglas de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="72034-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="72034-112">servidor de back-end de Hello debe responder sondeos de puerta de enlace de aplicación toohello, que se describen en hello [información general de sondeo de estado](application-gateway-probe-overview.md) sección.</span><span class="sxs-lookup"><span data-stu-id="72034-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="72034-113">Los sondeos del estado de Application Gateway son solo HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="72034-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="72034-114">Cada servidor de back-end debe responder sondeos tooHTTP puerta de enlace tooroute WebSocket tráfico toohello para servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="72034-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="72034-115">Elemento de configuración de agente de escucha</span><span class="sxs-lookup"><span data-stu-id="72034-115">Listener configuration element</span></span>

<span data-ttu-id="72034-116">Un agente de escucha HTTP existente puede ser usado toosupport tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="72034-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="72034-117">Hola aquí te mostramos un fragmento de código de un elemento de httpListeners desde un archivo de plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="72034-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="72034-118">¿Necesita toosupport de agentes de escucha HTTP y HTTPS WebSocket y proteger el tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="72034-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="72034-119">Del mismo modo puede usar hello [portal](application-gateway-create-gateway-portal.md) o [PowerShell](application-gateway-create-gateway-arm.md) toocreate una puerta de enlace de la aplicación con los agentes de escucha de tráfico en el puerto 80/443 toosupport WebSocket.</span><span class="sxs-lookup"><span data-stu-id="72034-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="72034-120">Configuración de reglas de enrutamiento, BackendHttpSetting y BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="72034-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="72034-121">Un BackendAddressPool es toodefine utilizado un grupo back-end con servidores de WebSocket habilitado.</span><span class="sxs-lookup"><span data-stu-id="72034-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="72034-122">Hola backendHttpSetting se define con un puerto de back-end 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="72034-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="72034-123">propiedades de Hola para afinidad basado en cookies y requestTimeouts no son relevantes tooWebSocket tráfico.</span><span class="sxs-lookup"><span data-stu-id="72034-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="72034-124">Hay ningún cambio necesario en la regla de enrutamiento de hello, "Básica" es tootie usado Hola agentes de escucha adecuada toohello correspondiente grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="72034-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="72034-125">Back-end con WebSocket habilitado</span><span class="sxs-lookup"><span data-stu-id="72034-125">WebSocket enabled backend</span></span>

<span data-ttu-id="72034-126">El back-end debe tener un servidor de web HTTP/HTTPS con hello configurado el puerto (normalmente 80/443) para toowork de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="72034-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="72034-127">Este requisito es porque requiere de protocolo WebSocket toobe de protocolo de enlace inicial de hello HTTP con el protocolo de actualización tooWebSocket como un campo de encabezado.</span><span class="sxs-lookup"><span data-stu-id="72034-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="72034-128">Hola te mostramos un ejemplo de un encabezado:</span><span class="sxs-lookup"><span data-stu-id="72034-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="72034-129">Otro de los motivos es que el sondeo del estado del back-end de la puerta de enlace de aplicaciones solo admite los protocolos HTTP y HTTPS.</span><span class="sxs-lookup"><span data-stu-id="72034-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="72034-130">Si el servidor de back-end de hello no responde tooHTTP o sondeos HTTPS, que se saca del grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="72034-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72034-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72034-131">Next steps</span></span>

<span data-ttu-id="72034-132">Después de aprendizaje sobre la compatibilidad con WebSocket, vaya demasiado[crear una puerta de enlace de la aplicación](application-gateway-create-gateway.md) tooget a trabajar con un WebSocket la aplicación web habilitada.</span><span class="sxs-lookup"><span data-stu-id="72034-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

