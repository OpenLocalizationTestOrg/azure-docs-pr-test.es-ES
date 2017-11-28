---
title: "Introducción al enrutamiento contenido basado en aaaURL | Documentos de Microsoft"
description: "Esta página proporciona una visión general de enrutamiento de hello basado en la dirección URL de puerta de enlace de la aplicación contenido, configuración de UrlPathMap y PathBasedRouting regla."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="f6a3e-103">Información general del enrutamiento basado en URL</span><span class="sxs-lookup"><span data-stu-id="f6a3e-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="f6a3e-104">Dirección URL de ruta de acceso de enrutamiento permite tooroute tráfico tooback final grupos de servidores en función de las rutas de acceso de dirección URL de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="f6a3e-105">Uno de los escenarios de hello es tooroute solicitudes para grupos de servidores de back-end de toodifferent de diferentes tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="f6a3e-106">En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com de tres grupos de servidor back-end por ejemplo: VideoServerPool, ImageServerPool y DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="f6a3e-108">Las solicitudes para http://contoso.com/video * son tooVideoServerPool enrutado y http://contoso.com/images * son tooImageServerPool enrutado.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="f6a3e-109">DefaultServerPool está seleccionada si coincide con ninguno de los patrones de ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6a3e-110">Las reglas se procesan en orden de hello aparecen en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="f6a3e-111">Es muy recomendable tooconfigure los agentes de escucha de varios sitios primera anterior tooconfiguring un agente de escucha básico.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="f6a3e-112">Esto garantiza que en vuelta ese toohello enrutado en obtiene tráfico Finalizar.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="f6a3e-113">Si un agente de escucha básico aparece en primer lugar y coincide con una solicitud entrante, lo procesa ese agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="f6a3e-114">Elemento de configuración UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="f6a3e-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="f6a3e-115">elemento de Hello urlPathMap es toospecify usa patrones de ruta de acceso tooback-end asignaciones de grupo de servidores.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="f6a3e-116">Hola ejemplo de código siguiente es fragmento Hola de elemento de urlPathMap del archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> <span data-ttu-id="f6a3e-117">PathPattern: Este valor es una lista de toomatch de patrones de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="f6a3e-118">Cada uno de ellos debe comenzar con / hello solo lugar y un "*" se permite en hello final sigue un "/".</span><span class="sxs-lookup"><span data-stu-id="f6a3e-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="f6a3e-119">¿Hola cadena fed buscador de coincidencias de ruta de acceso de toohello no incluye cualquier texto después de hello en primer lugar? o bien, # y los caracteres no se permiten aquí.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="f6a3e-120">Para obtener más información, puede consultar una [plantilla de Resource Manager que use el enrutamiento basado en URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .</span><span class="sxs-lookup"><span data-stu-id="f6a3e-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="f6a3e-121">Regla de PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="f6a3e-121">PathBasedRouting rule</span></span>

<span data-ttu-id="f6a3e-122">RequestRoutingRule de tipo PathBasedRouting es toobind usado un urlPathMap de tooa de agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="f6a3e-123">Todas las solicitudes que se reciben para este agente de escucha se enrutan según la directiva especificada en urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="f6a3e-124">Fragmento de código de la regla PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="f6a3e-124">Snippet of PathBasedRouting rule:</span></span>

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="f6a3e-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6a3e-125">Next steps</span></span>

<span data-ttu-id="f6a3e-126">Después de aprender a enrutamiento contenido basado en dirección URL, vaya demasiado[crear una puerta de enlace de la aplicación mediante el enrutamiento basado en la dirección URL](application-gateway-create-url-route-portal.md) toocreate una puerta de enlace de la aplicación con las reglas de enrutamiento de direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="f6a3e-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
