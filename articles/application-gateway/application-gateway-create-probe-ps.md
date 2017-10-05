---
title: "Creación de un sondeo personalizado para Azure Application Gateway mediante PowerShell | Microsoft Docs"
description: Aprenda a crear un sondeo personalizado para Puerta de enlace de aplicaciones mediante PowerShell en el Administrador de recursos
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="27325-103">Creación de un sondeo personalizado para Puerta de enlace de aplicaciones de Azure mediante PowerShell en el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="27325-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27325-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="27325-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="27325-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27325-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="27325-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="27325-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="27325-107">En este artículo, agregará un sondeo personalizado a una puerta de enlace de aplicaciones existente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27325-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="27325-108">Los sondeos personalizados son útiles para aplicaciones que tienen una página de comprobación del estado o para aplicaciones que no proporcionan una respuesta correcta en la aplicación web predeterminada.</span><span class="sxs-lookup"><span data-stu-id="27325-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="27325-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="27325-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="27325-110">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del [modelo de implementación clásica](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="27325-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="27325-111">Creación de una puerta de enlace de aplicaciones con un sondeo personalizado</span><span class="sxs-lookup"><span data-stu-id="27325-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="27325-112">Inicio de sesión y creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="27325-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="27325-113">Use `Login-AzureRmAccount` para autenticar.</span><span class="sxs-lookup"><span data-stu-id="27325-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="27325-114">Obtenga las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="27325-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="27325-115">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="27325-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="27325-116">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="27325-116">Create a resource group.</span></span> <span data-ttu-id="27325-117">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="27325-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="27325-118">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="27325-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="27325-119">Esta ubicación se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="27325-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="27325-120">Asegúrese de que todos los comandos para crear una puerta de enlace de aplicaciones usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="27325-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="27325-121">En el ejemplo anterior, creamos un grupo de recursos denominado **appgw-RG** en la ubicación **oeste de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="27325-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="27325-122">Creación de una red virtual y una subred</span><span class="sxs-lookup"><span data-stu-id="27325-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="27325-123">En el siguiente ejemplo, se crea una red virtual y una subred para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="27325-124">La puerta de enlace de aplicaciones requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="27325-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="27325-125">Por este motivo, la subred creada para la puerta de enlace de aplicaciones debe ser menor que el espacio de direcciones de la red virtual para permitir que se puedan crear y usar otras subredes.</span><span class="sxs-lookup"><span data-stu-id="27325-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="27325-126">Creación de una dirección IP pública para la configuración del front-end</span><span class="sxs-lookup"><span data-stu-id="27325-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="27325-127">Cree un recurso IP público **publicIP01** en el grupo de recursos **appgw-rg** para la región Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="27325-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="27325-128">En este ejemplo se utiliza una dirección IP pública para la dirección IP de front-end de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="27325-129">La puerta de enlace de aplicaciones requiere que la dirección IP pública tenga un nombre DNS creado de forma dinámica. Por lo tanto, `-DomainNameLabel` no se puede especificar durante la creación de la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="27325-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="27325-130">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="27325-130">Create an application gateway</span></span>

<span data-ttu-id="27325-131">Debe configurar todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="27325-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="27325-132">En el ejemplo siguiente, se crean los elementos de configuración necesarios para un recurso de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="27325-133">**Componente**</span><span class="sxs-lookup"><span data-stu-id="27325-133">**Component**</span></span> | <span data-ttu-id="27325-134">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="27325-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="27325-135">**Configuración de IP de puerta de enlace**</span><span class="sxs-lookup"><span data-stu-id="27325-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="27325-136">Una configuración de IP para una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="27325-137">**Grupo de back-end**</span><span class="sxs-lookup"><span data-stu-id="27325-137">**Backend pool**</span></span> | <span data-ttu-id="27325-138">Un grupo de direcciones IP, FQDN o NIC de los servidores de aplicaciones que hospedan a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="27325-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="27325-139">**Sondeo de estado**</span><span class="sxs-lookup"><span data-stu-id="27325-139">**Health probe**</span></span> | <span data-ttu-id="27325-140">Un sondeo personalizado utilizado para supervisar el estado de los miembros del grupo de back-end</span><span class="sxs-lookup"><span data-stu-id="27325-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="27325-141">**Configuración de HTTP**</span><span class="sxs-lookup"><span data-stu-id="27325-141">**HTTP settings**</span></span> | <span data-ttu-id="27325-142">Una colección de configuraciones, incluidos el puerto, el protocolo, la afinidad basada en cookies y el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="27325-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="27325-143">Esta configuración determina cómo se enruta el tráfico a los miembros del grupo de back-end</span><span class="sxs-lookup"><span data-stu-id="27325-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="27325-144">**Puerto de front-end**</span><span class="sxs-lookup"><span data-stu-id="27325-144">**Frontend port**</span></span> | <span data-ttu-id="27325-145">El puerto que escucha la puerta de enlace de aplicaciones para el tráfico</span><span class="sxs-lookup"><span data-stu-id="27325-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="27325-146">**Agente de escucha**</span><span class="sxs-lookup"><span data-stu-id="27325-146">**Listener**</span></span> | <span data-ttu-id="27325-147">Una combinación de un protocolo, una configuración de IP de front-end y el puerto de front-end.</span><span class="sxs-lookup"><span data-stu-id="27325-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="27325-148">Esto es lo que se escucha en las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="27325-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="27325-149">**Regla**</span><span class="sxs-lookup"><span data-stu-id="27325-149">**Rule**</span></span>| <span data-ttu-id="27325-150">Enruta el tráfico al back-end adecuado según la configuración HTTP.</span><span class="sxs-lookup"><span data-stu-id="27325-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="27325-151">Agregar un sondeo a una puerta de enlace de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="27325-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="27325-152">El fragmento de código siguiente agrega un sondeo a una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="27325-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="27325-153">Eliminación de un sondeo de una puerta de enlace de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="27325-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="27325-154">El fragmento de código siguiente quita un sondeo de una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="27325-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="27325-155">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="27325-155">Get application gateway DNS name</span></span>

<span data-ttu-id="27325-156">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="27325-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="27325-157">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="27325-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="27325-158">Para asegurarse de que los usuarios finales puedan llegar a la puerta de enlace de aplicaciones, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="27325-159">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="27325-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="27325-160">Para ello, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="27325-161">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="27325-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="27325-162">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27325-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="27325-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="27325-163">Next steps</span></span>

<span data-ttu-id="27325-164">Aprenda a configurar la descarga de SSL visitando [Configuración de la descarga SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="27325-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

