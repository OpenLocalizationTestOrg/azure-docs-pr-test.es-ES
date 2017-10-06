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
# <a name="url-path-based-routing-overview"></a>Información general del enrutamiento basado en URL

Dirección URL de ruta de acceso de enrutamiento permite tooroute tráfico tooback final grupos de servidores en función de las rutas de acceso de dirección URL de solicitud de saludo. 

Uno de los escenarios de hello es tooroute solicitudes para grupos de servidores de back-end de toodifferent de diferentes tipos de contenido.

En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com de tres grupos de servidor back-end por ejemplo: VideoServerPool, ImageServerPool y DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

Las solicitudes para http://contoso.com/video * son tooVideoServerPool enrutado y http://contoso.com/images * son tooImageServerPool enrutado. DefaultServerPool está seleccionada si coincide con ninguno de los patrones de ruta de acceso de Hola.

> [!IMPORTANT]
> Las reglas se procesan en orden de hello aparecen en el portal de Hola. Es muy recomendable tooconfigure los agentes de escucha de varios sitios primera anterior tooconfiguring un agente de escucha básico.  Esto garantiza que en vuelta ese toohello enrutado en obtiene tráfico Finalizar. Si un agente de escucha básico aparece en primer lugar y coincide con una solicitud entrante, lo procesa ese agente de escucha.

## <a name="urlpathmap-configuration-element"></a>Elemento de configuración UrlPathMap

elemento de Hello urlPathMap es toospecify usa patrones de ruta de acceso tooback-end asignaciones de grupo de servidores. Hola ejemplo de código siguiente es fragmento Hola de elemento de urlPathMap del archivo de plantilla.

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
> PathPattern: Este valor es una lista de toomatch de patrones de ruta de acceso. Cada uno de ellos debe comenzar con / hello solo lugar y un "*" se permite en hello final sigue un "/". ¿Hola cadena fed buscador de coincidencias de ruta de acceso de toohello no incluye cualquier texto después de hello en primer lugar? o bien, # y los caracteres no se permiten aquí.

Para obtener más información, puede consultar una [plantilla de Resource Manager que use el enrutamiento basado en URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .

## <a name="pathbasedrouting-rule"></a>Regla de PathBasedRouting

RequestRoutingRule de tipo PathBasedRouting es toobind usado un urlPathMap de tooa de agente de escucha. Todas las solicitudes que se reciben para este agente de escucha se enrutan según la directiva especificada en urlPathMap.
Fragmento de código de la regla PathBasedRouting:

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

## <a name="next-steps"></a>Pasos siguientes

Después de aprender a enrutamiento contenido basado en dirección URL, vaya demasiado[crear una puerta de enlace de la aplicación mediante el enrutamiento basado en la dirección URL](application-gateway-create-url-route-portal.md) toocreate una puerta de enlace de la aplicación con las reglas de enrutamiento de direcciones URL.
