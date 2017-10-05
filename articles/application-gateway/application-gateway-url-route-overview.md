---
title: "Información general del enrutamiento de contenido basado en URL | Microsoft Docs"
description: "En esta página se proporciona información general sobre el enrutamiento de contenido basado en URL de Application Gateway, la configuración de UrlPathMap y la regla PathBasedRouting."
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
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="acc52-103">Información general del enrutamiento basado en URL</span><span class="sxs-lookup"><span data-stu-id="acc52-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="acc52-104">El enrutamiento basado en URL le permite enrutar el tráfico a los grupos de servidores back-end en función de las direcciones URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="acc52-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="acc52-105">Por ejemplo, puede enrutar las solicitudes de diferentes tipos de contenido a diferentes grupos de servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="acc52-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="acc52-106">En el ejemplo siguiente, Application Gateway atiende el tráfico de contoso.com desde tres grupos de servidores back-end: VideoServerPool, ImageServerPool y DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="acc52-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="acc52-108">Las solicitudes de http://contoso.com/video* se enrutan a VideoServerPool y las de http://contoso.com/images* a ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="acc52-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="acc52-109">DefaultServerPool se selecciona si ninguno de los patrones de ruta de acceso coincide.</span><span class="sxs-lookup"><span data-stu-id="acc52-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acc52-110">Las reglas se procesan en el orden en que aparecen en el portal.</span><span class="sxs-lookup"><span data-stu-id="acc52-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="acc52-111">Es muy recomendable configurar a los agentes de escucha multisitio antes de configurar un agente de escucha básico.</span><span class="sxs-lookup"><span data-stu-id="acc52-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="acc52-112">De esta forma se asegura de que el tráfico se enruta al back-end adecuado.</span><span class="sxs-lookup"><span data-stu-id="acc52-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="acc52-113">Si un agente de escucha básico aparece en primer lugar y coincide con una solicitud entrante, lo procesa ese agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="acc52-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="acc52-114">Elemento de configuración UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="acc52-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="acc52-115">El elemento UrlPathMap se utiliza para especificar patrones de ruta de acceso para las asignaciones de grupos de servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="acc52-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="acc52-116">A continuación se muestra el fragmento de código del elemento urlPathMap del archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="acc52-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="acc52-117">PathPattern: esta opción es una lista de patrones de ruta de acceso con los que se buscan coincidencias.</span><span class="sxs-lookup"><span data-stu-id="acc52-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="acc52-118">Cada uno de ellos debe comenzar con / y el único lugar donde se permite un carácter "*" es al final, después de un carácter "/".</span><span class="sxs-lookup"><span data-stu-id="acc52-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="acc52-119">La cadena que se suministra al comprobador de rutas de acceso no incluye texto después del primer ? o #, y esos caracteres no se permiten aquí.</span><span class="sxs-lookup"><span data-stu-id="acc52-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="acc52-120">Para obtener más información, puede consultar una [plantilla de Resource Manager que use el enrutamiento basado en URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .</span><span class="sxs-lookup"><span data-stu-id="acc52-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="acc52-121">Regla de PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="acc52-121">PathBasedRouting rule</span></span>

<span data-ttu-id="acc52-122">RequestRoutingRule de tipo PathBasedRouting se usa para enlazar un agente de escucha a un elemento urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="acc52-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="acc52-123">Todas las solicitudes que se reciben para este agente de escucha se enrutan según la directiva especificada en urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="acc52-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="acc52-124">Fragmento de código de la regla PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="acc52-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="acc52-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="acc52-125">Next steps</span></span>

<span data-ttu-id="acc52-126">Ahora que conoce el enrutamiento de contenido basado en URL, vaya a [Create an application gateway using URL based routing](application-gateway-create-url-route-portal.md) (Creación de una puerta de enlace de aplicaciones mediante el enrutamiento basado en URL) para crear una puerta de enlace de aplicaciones con reglas de enrutamiento de direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="acc52-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
