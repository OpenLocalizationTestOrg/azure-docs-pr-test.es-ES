---
title: "firewall de aplicación web de aaaConfigure: puerta de enlace de aplicaciones de Azure | Documentos de Microsoft"
description: "Este artículo proporciona instrucciones sobre cómo usar toostart web servidor de aplicaciones en una puerta de enlace de aplicación nueva o existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="6e8d8-103">Configuración del firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6e8d8-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e8d8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e8d8-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="6e8d8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e8d8-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="6e8d8-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6e8d8-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="6e8d8-107">Obtenga información acerca de cómo toocreate un servidor de seguridad de la aplicación web habilita la puerta de enlace de aplicaciones o agregar web aplicación firewall tooan aplicación puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="6e8d8-108">servidor de aplicaciones web Hello (WAFS) en la puerta de enlace de aplicaciones de Azure protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL, ataques XSS y apropiaciones de sesión.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="6e8d8-109">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="6e8d8-110">Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="6e8d8-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="6e8d8-112">toofind una lista completa de las características admitidas, visite: [información general de Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e8d8-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="6e8d8-113">Hello siguiente artículo se muestra cómo demasiado[Agregar aplicación firewall tooan existente aplicación puerta de enlace web](#add-web-application-firewall-to-an-existing-application-gateway) y [crear una puerta de enlace de la aplicación que utiliza el servidor de aplicaciones web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="6e8d8-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagen de escenario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="6e8d8-115">Requisito previo: Instalar Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6e8d8-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="6e8d8-116">Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6e8d8-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="6e8d8-117">Diferencias de configuración de WAF</span><span class="sxs-lookup"><span data-stu-id="6e8d8-117">WAF configuration differences</span></span>

<span data-ttu-id="6e8d8-118">Si ha leído [crear una puerta de enlace de aplicaciones con Azure CLI](application-gateway-create-gateway-cli.md), comprender Hola SKU configuración tooconfigure al crear una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="6e8d8-119">WAFS proporciona toodefine de opciones de configuración adicionales al configurar Hola SKU en una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="6e8d8-120">No hay ningún otro cambio que realice en la puerta de enlace de aplicaciones de hello propio.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="6e8d8-121">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="6e8d8-121">**Setting**</span></span> | <span data-ttu-id="6e8d8-122">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="6e8d8-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="6e8d8-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="6e8d8-123">**SKU**</span></span> |<span data-ttu-id="6e8d8-124">Una puerta de enlace de aplicaciones normal sin WAF admite los tamaños **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="6e8d8-125">Con la introducción de Hola de WAFS, hay dos SKU adicionales, **WAFS\_medio** y **WAFS\_grande**.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="6e8d8-126">No se admite WAF en puertas de enlace de aplicaciones de pequeño tamaño.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="6e8d8-127">**Modo**</span><span class="sxs-lookup"><span data-stu-id="6e8d8-127">**Mode**</span></span> | <span data-ttu-id="6e8d8-128">Esta opción es modo de saludo de WAFS.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="6e8d8-129">Los valores permitidos son **Detección** y **Prevención**.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="6e8d8-130">Cuando WAF está configurado en modo de detección, todas las amenazas se almacenan en un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="6e8d8-131">En el modo de prevención, todavía se registran eventos pero atacante Hola recibe una respuesta no autorizado 403 puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="6e8d8-132">Agregar aplicación firewall tooan existente aplicación puerta de enlace web</span><span class="sxs-lookup"><span data-stu-id="6e8d8-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="6e8d8-133">Hola seguir los cambios de comando estándar de la aplicación puerta de enlace tooa WAFS aplicación habilitada puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="6e8d8-134">Este comando actualiza la puerta de enlace de aplicaciones de hello con servidor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="6e8d8-135">Visite [puerta de enlace de Application Diagnostics](application-gateway-diagnostics.md) toounderstand cómo tooview registros para la puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="6e8d8-136">Debido a toohello la naturaleza de seguridad de WAFS, registros necesidad toobe revisarse periódicamente postura de seguridad de hello toounderstand de las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="6e8d8-137">Creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="6e8d8-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="6e8d8-138">Hola siguiente comando crea una puerta de enlace de la aplicación con el servidor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-138">hello following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="6e8d8-139">Las puertas de enlace de aplicaciones creadas con la configuración del firewall de aplicación de hello web básico se configuran con CRS 3.0 para protección.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6e8d8-140">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6e8d8-140">Get application gateway DNS name</span></span>

<span data-ttu-id="6e8d8-141">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="6e8d8-142">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6e8d8-143">los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="6e8d8-144">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6e8d8-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="6e8d8-145">tooconfigure un registro CNAME, recuperar los detalles de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="6e8d8-146">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="6e8d8-147">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6e8d8-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="6e8d8-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e8d8-148">Next steps</span></span>

<span data-ttu-id="6e8d8-149">Obtenga información acerca de cómo las reglas de toocustomize WAFS visitando: [Personalizar reglas de firewall de aplicación web a través de hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6e8d8-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
