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
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="1fe59-103">Hospedaje de varios sitios de Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1fe59-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="1fe59-104">Alojamiento de varios sitios permite tooconfigure más de una aplicación web en hello misma instancia de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1fe59-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="1fe59-105">Esta característica permite tooconfigure una topología más eficaz para las implementaciones mediante la adición de puerta de enlace de aplicaciones de tooone de too20 sitios Web.</span><span class="sxs-lookup"><span data-stu-id="1fe59-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="1fe59-106">Cada sitio Web puede ser dirigido tooits posee grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="1fe59-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="1fe59-107">En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com y fabrikam.com de dos grupos de servidor back-end denominado ContosoServerPool y FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="1fe59-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="1fe59-109">Las reglas se procesan en orden de hello aparecen en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fe59-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="1fe59-110">Es muy recomendable tooconfigure los agentes de escucha de varios sitios primera anterior tooconfiguring un agente de escucha básico.</span><span class="sxs-lookup"><span data-stu-id="1fe59-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="1fe59-111">Así se asegurará de terminar en vuelta ese toohello enrutado en obtiene tráfico.</span><span class="sxs-lookup"><span data-stu-id="1fe59-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="1fe59-112">Si un agente de escucha básico aparece en primer lugar y coincide con una solicitud entrante, lo procesa ese agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="1fe59-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="1fe59-113">Las solicitudes de http://contoso.com son tooContosoServerPool enrutado y http://fabrikam.com son tooFabrikamServerPool enrutado.</span><span class="sxs-lookup"><span data-stu-id="1fe59-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="1fe59-114">De igual forma dos subdominios de hello mismo dominio principal se puede hospedar en Hola misma implementación de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1fe59-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="1fe59-115">Ejemplos de uso de subdominios podrían incluir http://blog.contoso.com y http://app.contoso.com hospedados en una única implementación de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1fe59-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="1fe59-116">Encabezados de host e Indicación de nombre de servidor (SNI)</span><span class="sxs-lookup"><span data-stu-id="1fe59-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="1fe59-117">Hay tres mecanismos habituales para habilitar varios sitio que se hospeda en hello mismo infraestructura.</span><span class="sxs-lookup"><span data-stu-id="1fe59-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="1fe59-118">Hospede varias aplicaciones web, cada una en una dirección IP única.</span><span class="sxs-lookup"><span data-stu-id="1fe59-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="1fe59-119">Nombre del host de uso toohost varias aplicaciones web en hello misma dirección IP.</span><span class="sxs-lookup"><span data-stu-id="1fe59-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="1fe59-120">Usar diferentes puertos toohost varias aplicaciones web en hello misma dirección IP.</span><span class="sxs-lookup"><span data-stu-id="1fe59-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="1fe59-121">Actualmente, una puerta de enlace de aplicaciones obtiene una dirección IP pública única en la que escucha el tráfico.</span><span class="sxs-lookup"><span data-stu-id="1fe59-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="1fe59-122">Por lo tanto, la compatibilidad con varias aplicaciones, cada una con su propia dirección IP, no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="1fe59-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="1fe59-123">Puerta de enlace de aplicaciones admite hospedando varias aplicaciones cada escuchan en puertos diferentes, pero este escenario requiere tráfico de tooaccept aplicaciones de hello en puertos no estándar y no suele ser una configuración deseada.</span><span class="sxs-lookup"><span data-stu-id="1fe59-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="1fe59-124">Puerta de enlace de aplicaciones se basa en HTTP 1.1 toohost de encabezados de host, más de un sitio Web en Hola la misma dirección IP pública y el puerto.</span><span class="sxs-lookup"><span data-stu-id="1fe59-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="1fe59-125">sitios de Hello hospedados en puerta de enlace de aplicaciones también pueden descarga SSL de compatibilidad con la extensión de indicación de nombre de servidor (SNI) TLS.</span><span class="sxs-lookup"><span data-stu-id="1fe59-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="1fe59-126">Este escenario significa que Hola cliente explorador y back-end de granja de servidores web debe ser compatible con HTTP/1.1 y la extensión TLS como se define en RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="1fe59-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="1fe59-127">Elemento de configuración de agente de escucha</span><span class="sxs-lookup"><span data-stu-id="1fe59-127">Listener configuration element</span></span>

<span data-ttu-id="1fe59-128">HTTPListener existente es el elemento de configuración mejorada toosupport host nombre y el servidor nombre indicación elementos, que se usa por grupo de aplicaciones puerta de enlace tooroute tráfico tooappropriate back-end.</span><span class="sxs-lookup"><span data-stu-id="1fe59-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="1fe59-129">Hola ejemplo de código siguiente es fragmento Hola de elemento de HttpListeners del archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="1fe59-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="1fe59-130">Puede visitar [plantilla de administrador de recursos con alojamiento de varios sitios](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) para una implementación de extremo tooend basadas en plantillas.</span><span class="sxs-lookup"><span data-stu-id="1fe59-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="1fe59-131">Regla de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="1fe59-131">Routing rule</span></span>

<span data-ttu-id="1fe59-132">No hay ningún cambio necesario en la regla de enrutamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fe59-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="1fe59-133">Hola 'Basic' debe continuar toobe elegido tootie Hola sitio adecuado del agente de escucha toohello correspondiente grupo back-end dirección de regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="1fe59-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1fe59-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1fe59-134">Next steps</span></span>

<span data-ttu-id="1fe59-135">Después de aprender a alojamiento de varios sitios, vaya demasiado[crear una puerta de enlace de aplicaciones con alojamiento de varios sitios](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate una puerta de enlace de aplicaciones con capacidad toosupport más de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1fe59-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

