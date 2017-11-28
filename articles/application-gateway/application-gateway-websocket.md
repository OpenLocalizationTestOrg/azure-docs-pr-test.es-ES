---
title: Compatibilidad de WebSocket en Application Gateway | Microsoft Docs
description: "En esta página se proporciona información general sobre la compatibilidad de Application Gateway con WebSocket."
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
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="59dce-103">Introducción a la compatibilidad de WebSocket en Application Gateway</span><span class="sxs-lookup"><span data-stu-id="59dce-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="59dce-104">Application Gateway proporciona una compatibilidad nativa con WebSocket en todas las puertas de enlace, con independencia de su tamaño.</span><span class="sxs-lookup"><span data-stu-id="59dce-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="59dce-105">No hay ninguna opción de configuración que permita al usuario habilitar o deshabilitar la compatibilidad con WebSocket.</span><span class="sxs-lookup"><span data-stu-id="59dce-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="59dce-106">El protocolo WebSocket, estándar en [RFC6455](https://tools.ietf.org/html/rfc6455) , permite una comunicación dúplex completa entre un servidor y un cliente a través de una conexión TCP de larga duración.</span><span class="sxs-lookup"><span data-stu-id="59dce-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="59dce-107">Esta característica permite una comunicación más interactiva entre el servidor web y el cliente, que puede ser bidireccional sin necesidad de realizar sondeos como en las implementaciones basadas en HTTP.</span><span class="sxs-lookup"><span data-stu-id="59dce-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="59dce-108">A diferencia de HTTP, WebSocket tiene poca sobrecarga y puede reutilizar la misma conexión TCP para varias solicitudes y respuestas, lo que conlleva un uso más eficaz de los recursos.</span><span class="sxs-lookup"><span data-stu-id="59dce-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="59dce-109">Los protocolos WebSocket están diseñados para utilizarse a través de los puertos HTTP tradicionales 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="59dce-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="59dce-110">Puede seguir usando una escucha HTTP estándar en los puertos 80 o 443 para recibir tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="59dce-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="59dce-111">Después, el tráfico de WebSocket se dirige al servidor back-end con este protocolo habilitado utilizando el grupo back-end adecuado según lo especificado en las reglas de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="59dce-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="59dce-112">El servidor back-end debe responder a los sondeos de la puerta de enlace de aplicaciones, que se describen en la sección de [información general sobre el sondeo de estado](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="59dce-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="59dce-113">Los sondeos del estado de Application Gateway son solo HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59dce-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="59dce-114">Cada servidor de back-end debe responder a los sondeos HTTP de Application Gateway para enrutar el tráfico de WebSocket al servidor.</span><span class="sxs-lookup"><span data-stu-id="59dce-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="59dce-115">Elemento de configuración de agente de escucha</span><span class="sxs-lookup"><span data-stu-id="59dce-115">Listener configuration element</span></span>

<span data-ttu-id="59dce-116">Una escucha HTTP existente se puede utilizar para admitir tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="59dce-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="59dce-117">A continuación, se muestra un fragmento de código de un elemento httpListeners de un archivo de plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="59dce-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="59dce-118">Necesitaría los agentes de escucha de HTTP y HTTPS para admitir WebSocket y proteger el tráfico procedente de este protocolo.</span><span class="sxs-lookup"><span data-stu-id="59dce-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="59dce-119">De forma similar, puede usar el [portal](application-gateway-create-gateway-portal.md) o [PowerShell](application-gateway-create-gateway-arm.md) para crear una puerta de enlace de aplicaciones con agentes de escucha en el puerto 80 o 443, con el fin de permitir el tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="59dce-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="59dce-120">Configuración de reglas de enrutamiento, BackendHttpSetting y BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="59dce-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="59dce-121">BackendAddressPool se usa para definir un grupo back-end con servidores con WebSocket habilitado.</span><span class="sxs-lookup"><span data-stu-id="59dce-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="59dce-122">backendHttpSetting se define con un puerto de back-end 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="59dce-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="59dce-123">Las propiedades de la afinidad basada en cookies y requestTimeouts no son pertinentes para el tráfico de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="59dce-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="59dce-124">No se requiere ningún cambio en la regla de enrutamiento, se usa "Básico" para vincular el agente de escucha adecuado al grupo de direcciones back-end correspondiente.</span><span class="sxs-lookup"><span data-stu-id="59dce-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="59dce-125">Back-end con WebSocket habilitado</span><span class="sxs-lookup"><span data-stu-id="59dce-125">WebSocket enabled backend</span></span>

<span data-ttu-id="59dce-126">El back-end debe tener un servidor web HTTP o HTTPS que se esté ejecutando en el puerto configurado (normalmente, el 80 o 443) para que WebSocket funcione.</span><span class="sxs-lookup"><span data-stu-id="59dce-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="59dce-127">Este requisito se debe a que el protocolo WebSocket necesita que el protocolo de enlace inicial sea HTTP con la actualización a protocolo WebSocket como campo de encabezado.</span><span class="sxs-lookup"><span data-stu-id="59dce-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="59dce-128">A continuación, se muestra un ejemplo de un encabezado:</span><span class="sxs-lookup"><span data-stu-id="59dce-128">The following is an example of a header:</span></span>

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

<span data-ttu-id="59dce-129">Otro de los motivos es que el sondeo del estado del back-end de la puerta de enlace de aplicaciones solo admite los protocolos HTTP y HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59dce-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="59dce-130">Si el servidor back-end no responde a sondeos HTTP o HTTPS, se saca del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="59dce-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59dce-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59dce-131">Next steps</span></span>

<span data-ttu-id="59dce-132">Cuando haya terminado de leer la información sobre compatibilidad con WebSocket, vaya al artículo sobre [cómo crear una puerta de enlace de aplicaciones](application-gateway-create-gateway.md) para empezar a trabajar con una aplicación web con WebSocket habilitado.</span><span class="sxs-lookup"><span data-stu-id="59dce-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

