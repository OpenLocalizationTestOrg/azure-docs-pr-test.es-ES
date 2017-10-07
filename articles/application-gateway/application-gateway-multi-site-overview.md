---
title: aaaHosting varios sitios en la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello compatibilidad con varios sitio de puerta de enlace de aplicaciones."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Hospedaje de varios sitios de Puerta de enlace de aplicaciones

Alojamiento de varios sitios permite tooconfigure más de una aplicación web en hello misma instancia de puerta de enlace de aplicaciones. Esta característica permite tooconfigure una topología más eficaz para las implementaciones mediante la adición de puerta de enlace de aplicaciones de tooone de too20 sitios Web. Cada sitio Web puede ser dirigido tooits posee grupo back-end. En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com y fabrikam.com de dos grupos de servidor back-end denominado ContosoServerPool y FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Las reglas se procesan en orden de hello aparecen en el portal de Hola. Es muy recomendable tooconfigure los agentes de escucha de varios sitios primera anterior tooconfiguring un agente de escucha básico.  Así se asegurará de terminar en vuelta ese toohello enrutado en obtiene tráfico. Si un agente de escucha básico aparece en primer lugar y coincide con una solicitud entrante, lo procesa ese agente de escucha.

Las solicitudes de http://contoso.com son tooContosoServerPool enrutado y http://fabrikam.com son tooFabrikamServerPool enrutado.

De igual forma dos subdominios de hello mismo dominio principal se puede hospedar en Hola misma implementación de puerta de enlace de aplicaciones. Ejemplos de uso de subdominios podrían incluir http://blog.contoso.com y http://app.contoso.com hospedados en una única implementación de puerta de enlace de aplicaciones.

## <a name="host-headers-and-server-name-indication-sni"></a>Encabezados de host e Indicación de nombre de servidor (SNI)

Hay tres mecanismos habituales para habilitar varios sitio que se hospeda en hello mismo infraestructura.

1. Hospede varias aplicaciones web, cada una en una dirección IP única.
2. Nombre del host de uso toohost varias aplicaciones web en hello misma dirección IP.
3. Usar diferentes puertos toohost varias aplicaciones web en hello misma dirección IP.

Actualmente, una puerta de enlace de aplicaciones obtiene una dirección IP pública única en la que escucha el tráfico. Por lo tanto, la compatibilidad con varias aplicaciones, cada una con su propia dirección IP, no se admite actualmente. Puerta de enlace de aplicaciones admite hospedando varias aplicaciones cada escuchan en puertos diferentes, pero este escenario requiere tráfico de tooaccept aplicaciones de hello en puertos no estándar y no suele ser una configuración deseada. Puerta de enlace de aplicaciones se basa en HTTP 1.1 toohost de encabezados de host, más de un sitio Web en Hola la misma dirección IP pública y el puerto. sitios de Hello hospedados en puerta de enlace de aplicaciones también pueden descarga SSL de compatibilidad con la extensión de indicación de nombre de servidor (SNI) TLS. Este escenario significa que Hola cliente explorador y back-end de granja de servidores web debe ser compatible con HTTP/1.1 y la extensión TLS como se define en RFC 6066.

## <a name="listener-configuration-element"></a>Elemento de configuración de agente de escucha

HTTPListener existente es el elemento de configuración mejorada toosupport host nombre y el servidor nombre indicación elementos, que se usa por grupo de aplicaciones puerta de enlace tooroute tráfico tooappropriate back-end. Hola ejemplo de código siguiente es fragmento Hola de elemento de HttpListeners del archivo de plantilla.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Puede visitar [plantilla de administrador de recursos con alojamiento de varios sitios](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) para una implementación de extremo tooend basadas en plantillas.

## <a name="routing-rule"></a>Regla de enrutamiento

No hay ningún cambio necesario en la regla de enrutamiento de Hola. Hola 'Basic' debe continuar toobe elegido tootie Hola sitio adecuado del agente de escucha toohello correspondiente grupo back-end dirección de regla de enrutamiento.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Pasos siguientes

Después de aprender a alojamiento de varios sitios, vaya demasiado[crear una puerta de enlace de aplicaciones con alojamiento de varios sitios](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate una puerta de enlace de aplicaciones con capacidad toosupport más de una aplicación web.

