---
title: "Configuración del firewall de aplicaciones web en una instancia de Azure Application Gateway | Microsoft Docs"
description: "En este artículo se proporcionan instrucciones sobre cómo comenzar a usar el firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente."
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
ms.openlocfilehash: ac6c629ceaf1a8036643f593ce3d7ef9ea096ef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="e37d7-103">Configuración del firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e37d7-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e37d7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e37d7-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="e37d7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e37d7-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="e37d7-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e37d7-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="e37d7-107">Aprenda a crear una puerta de enlace de aplicaciones habilitada para un firewall de aplicaciones web o a agregar un firewall de aplicaciones web a una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="e37d7-107">Learn how to create a web application firewall enabled application gateway or add web application firewall to an existing application gateway.</span></span>

<span data-ttu-id="e37d7-108">El firewall de aplicaciones web (WAF) de Azure Application Gateway protege las aplicaciones web de ataques web comunes, como inyección de código SQL, ataques de scripts entre sitios y secuestros de sesiones.</span><span class="sxs-lookup"><span data-stu-id="e37d7-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="e37d7-109">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="e37d7-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e37d7-110">Proporciona conmutación por error, solicitudes HTTP de enrutamiento de rendimiento entre distintos servidores, independientemente de que se encuentren en la nube o en una implementación local.</span><span class="sxs-lookup"><span data-stu-id="e37d7-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="e37d7-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="e37d7-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="e37d7-112">Para obtener una lista completa de las características admitidas, consulte la [información general sobre Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e37d7-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="e37d7-113">En el artículo siguiente se muestra cómo [agregar el firewall de aplicaciones web a una puerta de enlace de aplicaciones existente](#add-web-application-firewall-to-an-existing-application-gateway) y [crear una puerta de enlace de aplicaciones que usa el firewall de aplicaciones web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="e37d7-113">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagen de escenario][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="e37d7-115">Requisito previo: instalar la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e37d7-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="e37d7-116">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e37d7-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="e37d7-117">Diferencias de configuración de WAF</span><span class="sxs-lookup"><span data-stu-id="e37d7-117">WAF configuration differences</span></span>

<span data-ttu-id="e37d7-118">Si ha leído [Creación de una puerta de enlace de aplicaciones con la CLI de Azure](application-gateway-create-gateway-cli.md), comprenderá los valores de SKU que se deben configurar al crear una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e37d7-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="e37d7-119">WAF proporciona una configuración adicional que se puede definir al configurar la SKU en una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e37d7-119">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="e37d7-120">No hay ningún otro cambio que deba realizar en la puerta de enlace de aplicaciones propiamente dicha.</span><span class="sxs-lookup"><span data-stu-id="e37d7-120">There are no additional changes that you make on the application gateway itself.</span></span>

| <span data-ttu-id="e37d7-121">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="e37d7-121">**Setting**</span></span> | <span data-ttu-id="e37d7-122">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="e37d7-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="e37d7-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="e37d7-123">**SKU**</span></span> |<span data-ttu-id="e37d7-124">Una puerta de enlace de aplicaciones normal sin WAF admite los tamaños **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="e37d7-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="e37d7-125">Con la introducción de WAF, hay dos SKU adicionales, **WAF\_Medium** y **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="e37d7-125">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="e37d7-126">No se admite WAF en puertas de enlace de aplicaciones de pequeño tamaño.</span><span class="sxs-lookup"><span data-stu-id="e37d7-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="e37d7-127">**Modo**</span><span class="sxs-lookup"><span data-stu-id="e37d7-127">**Mode**</span></span> | <span data-ttu-id="e37d7-128">Esta configuración es el modo de WAF.</span><span class="sxs-lookup"><span data-stu-id="e37d7-128">This setting is the mode of WAF.</span></span> <span data-ttu-id="e37d7-129">Los valores permitidos son **Detección** y **Prevención**.</span><span class="sxs-lookup"><span data-stu-id="e37d7-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="e37d7-130">Cuando WAF está configurado en modo de detección, todas las amenazas se almacenan en un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="e37d7-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="e37d7-131">En modo de prevención, los eventos se siguen registrando pero el atacante recibe una respuesta 403 no autorizado de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e37d7-131">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="e37d7-132">Adición del firewall de aplicaciones web a una puerta de enlace de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="e37d7-132">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="e37d7-133">El siguiente comando cambia la puerta de enlace de aplicaciones estándar existente a una puerta de enlace de aplicaciones con WAF habilitado.</span><span class="sxs-lookup"><span data-stu-id="e37d7-133">The follow command changes an existing standard application gateway to a WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="e37d7-134">Este comando actualiza la puerta de enlace de aplicaciones con el firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="e37d7-134">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="e37d7-135">Consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md) para entender cómo ver los registros de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e37d7-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="e37d7-136">Debido a la naturaleza de la seguridad de WAF, los registros se deben revisar periódicamente para entender la postura de seguridad de las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="e37d7-136">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="e37d7-137">Creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="e37d7-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="e37d7-138">El comando siguiente permite crear una instancia de Application Gateway con firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="e37d7-138">The following command creates an Application Gateway with web application firewall.</span></span>

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
> <span data-ttu-id="e37d7-139">Las puertas de enlace de la aplicación creadas con la configuración de firewall de aplicación web básica se configuran con CRS 3.0 para protección.</span><span class="sxs-lookup"><span data-stu-id="e37d7-139">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e37d7-140">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e37d7-140">Get application gateway DNS name</span></span>

<span data-ttu-id="e37d7-141">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="e37d7-141">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="e37d7-142">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="e37d7-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e37d7-143">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e37d7-143">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="e37d7-144">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e37d7-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="e37d7-145">Para configurar un registro CNAME, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e37d7-145">To configure a CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="e37d7-146">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="e37d7-146">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="e37d7-147">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e37d7-147">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e37d7-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e37d7-148">Next steps</span></span>

<span data-ttu-id="e37d7-149">Aprenda a personalizar reglas de WAF visitando: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md) (Personalización de reglas de firewall de aplicaciones web a través de la CLI de Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="e37d7-149">Learn how to customize WAF rules by visiting: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
