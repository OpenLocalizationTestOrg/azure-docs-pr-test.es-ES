---
title: "Configuración de la descarga SSL para Azure Application Gateway mediante la CLI 2.0 de Azure | Microsoft Docs"
description: "En esta página se ofrecen instrucciones para crear una puerta de enlace de aplicaciones con descarga SSL mediante la CLI de Azure 2.0"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: e8c1ba09daef09ef5002e33345905772961c1d93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="44269-103">Configuración de una puerta de enlace de aplicaciones para la descarga SSL la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="44269-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="44269-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="44269-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="44269-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44269-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="44269-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="44269-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="44269-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="44269-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="44269-108">Azure Application Gateway puede configurarse para terminar la sesión Capa de sockets seguros (SSL) en la puerta de enlace para evitar las costosas tareas de descifrado SSL que tienen lugar en la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="44269-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="44269-109">La descarga SSL también simplifica la administración de certificados en el servidor front-end.</span><span class="sxs-lookup"><span data-stu-id="44269-109">SSL offload also simplifies certificate management at the front-end server.</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="44269-110">Requisito previo: instalar la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="44269-110">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="44269-111">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="44269-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="44269-112">Componentes necesarios</span><span class="sxs-lookup"><span data-stu-id="44269-112">Required components</span></span>

* <span data-ttu-id="44269-113">**Grupo de servidores back-end:** lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="44269-113">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="44269-114">Las direcciones IP que se enumeran deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="44269-114">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="44269-115">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="44269-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="44269-116">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="44269-116">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="44269-117">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="44269-117">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="44269-118">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="44269-118">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="44269-119">**Agente de escucha:** tiene un puerto front-end, un protocolo (Http o Https, que distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="44269-119">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="44269-120">**Regla:** enlaza el agente de escucha y el grupo de servidores back-end y define a qué grupo de servidores back-end se dirigirá el tráfico cuando llega a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="44269-120">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="44269-121">Actualmente, solo se admite la regla *básica* .</span><span class="sxs-lookup"><span data-stu-id="44269-121">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="44269-122">La regla *básica* es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="44269-122">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="44269-123">**Notas de configuración adicionales**</span><span class="sxs-lookup"><span data-stu-id="44269-123">**Additional configuration notes**</span></span>

<span data-ttu-id="44269-124">Para la configuración de certificados SSL, el protocolo de **HttpListener** debería cambiar a *Https* (con distinción entre mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="44269-124">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="44269-125">El elemento **SslCertificate** se agrega a **HttpListener** con el valor de la variable configurado para el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="44269-125">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="44269-126">El puerto front-end debe actualizarse al 443.</span><span class="sxs-lookup"><span data-stu-id="44269-126">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="44269-127">**Para habilitar la afinidad basada en cookies**: se puede configurar una puerta de enlace de aplicaciones para asegurarse de que las solicitudes de una sesión de cliente siempre se dirigen a la misma máquina virtual de la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="44269-127">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="44269-128">Este escenario se realiza mediante la inyección de una cookie de la sesión que permita a la puerta de enlace dirigir el tráfico de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="44269-128">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="44269-129">Para habilitar la afinidad basada en cookies, establezca **CookieBasedAffinity** en *Habilitado* en el elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="44269-129">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="44269-130">Configuración de la descarga de SSL en una puerta de enlace de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="44269-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port to be used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload the .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing the port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool to be used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using the new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking the listener to the back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="44269-131">Creación de una puerta de enlace de aplicaciones con la descarga de SSL</span><span class="sxs-lookup"><span data-stu-id="44269-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="44269-132">En el ejemplo siguiente se crea una puerta de enlace de aplicaciones con descarga de SSL.</span><span class="sxs-lookup"><span data-stu-id="44269-132">The following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="44269-133">El certificado y la contraseña de este se deben actualizar a una clave privada válida.</span><span class="sxs-lookup"><span data-stu-id="44269-133">The certificate and certificate password must be updated to a valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="44269-134">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="44269-134">Get application gateway DNS name</span></span>

<span data-ttu-id="44269-135">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="44269-135">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="44269-136">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="44269-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="44269-137">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="44269-137">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="44269-138">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="44269-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="44269-139">Para configurar un alias, recupere los detalles de la puerta de enlace de aplicaciones y su nombre de IP o DNS asociado mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="44269-139">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="44269-140">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="44269-140">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="44269-141">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="44269-141">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a><span data-ttu-id="44269-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44269-142">Next steps</span></span>

<span data-ttu-id="44269-143">Si desea configurar una puerta de enlace de aplicaciones para usarla con el equilibrador de carga interno (ILB), consulte [Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="44269-143">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="44269-144">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="44269-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="44269-145">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="44269-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="44269-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="44269-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
