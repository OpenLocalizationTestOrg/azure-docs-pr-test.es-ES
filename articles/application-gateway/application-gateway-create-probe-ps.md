---
title: aaaCreate personalizado sondeo - puerta de enlace de aplicaciones de Azure - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate personalizado de sondeo para puerta de enlace de aplicaciones mediante el uso de PowerShell en el Administrador de recursos"
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
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="42559-103">Creación de un sondeo personalizado para Puerta de enlace de aplicaciones de Azure mediante PowerShell en el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="42559-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="42559-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="42559-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="42559-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42559-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="42559-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="42559-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="42559-107">En este artículo, se agregará un sondeo personalizado tooan aplicación puerta de enlace existente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42559-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="42559-108">Sondeos personalizados son útiles para las aplicaciones que tienen una página de comprobación de mantenimiento específico o para aplicaciones que no proporcionan una respuesta correcta en la aplicación web de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="42559-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="42559-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="42559-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="42559-110">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="42559-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="42559-111">Creación de una puerta de enlace de aplicaciones con un sondeo personalizado</span><span class="sxs-lookup"><span data-stu-id="42559-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="42559-112">Inicio de sesión y creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="42559-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="42559-113">Use `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="42559-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="42559-114">Obtener suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="42559-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="42559-115">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="42559-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="42559-116">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="42559-116">Create a resource group.</span></span> <span data-ttu-id="42559-117">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="42559-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="42559-118">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="42559-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="42559-119">Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="42559-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="42559-120">Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="42559-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="42559-121">En el anterior ejemplo de Hola, hemos creado un grupo de recursos denominado **appgw RG** en ubicación **oeste de Estados Unidos**.</span><span class="sxs-lookup"><span data-stu-id="42559-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="42559-122">Creación de una red virtual y una subred</span><span class="sxs-lookup"><span data-stu-id="42559-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="42559-123">Hello en el ejemplo siguiente se crea una red virtual y una subred de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="42559-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="42559-124">La puerta de enlace de aplicaciones requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="42559-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="42559-125">Por esta razón, subred Hola creado para la puerta de enlace de aplicaciones de hello debe ser menor que el espacio de direcciones de Hola de hello tooallow de red virtual para otro toobe subredes crea y usa.</span><span class="sxs-lookup"><span data-stu-id="42559-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="42559-126">Crear una dirección IP pública para la configuración de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="42559-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="42559-127">Crear un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="42559-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="42559-128">Este ejemplo utiliza una dirección IP pública para la dirección IP front-end de Hola de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="42559-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="42559-129">Puerta de enlace de aplicación requiere un nombre DNS creado de forma dinámica, por tanto, Hola Hola pública IP dirección toohave `-DomainNameLabel` no se puede especificar durante la creación de hello de dirección IP pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="42559-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="42559-130">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="42559-130">Create an application gateway</span></span>

<span data-ttu-id="42559-131">Configure todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="42559-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="42559-132">Hello en el ejemplo siguiente se crea Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42559-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="42559-133">**Componente**</span><span class="sxs-lookup"><span data-stu-id="42559-133">**Component**</span></span> | <span data-ttu-id="42559-134">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="42559-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="42559-135">**Configuración de IP de puerta de enlace**</span><span class="sxs-lookup"><span data-stu-id="42559-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="42559-136">Una configuración de IP para una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42559-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="42559-137">**Grupo de back-end**</span><span class="sxs-lookup"><span data-stu-id="42559-137">**Backend pool**</span></span> | <span data-ttu-id="42559-138">Un grupo de direcciones IP, FQDN o NIC que son servidores de aplicaciones de toohello que hospedan la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="42559-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="42559-139">**Sondeo de estado**</span><span class="sxs-lookup"><span data-stu-id="42559-139">**Health probe**</span></span> | <span data-ttu-id="42559-140">Un sondeo personalizado utiliza el estado de hello toomonitor de los miembros del grupo back-end Hola</span><span class="sxs-lookup"><span data-stu-id="42559-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="42559-141">**Configuración de HTTP**</span><span class="sxs-lookup"><span data-stu-id="42559-141">**HTTP settings**</span></span> | <span data-ttu-id="42559-142">Una colección de configuraciones, incluidos el puerto, el protocolo, la afinidad basada en cookies y el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="42559-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="42559-143">Esta configuración determina la forma de tráfico enrutado toohello los miembros del grupo back-end</span><span class="sxs-lookup"><span data-stu-id="42559-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="42559-144">**Puerto de front-end**</span><span class="sxs-lookup"><span data-stu-id="42559-144">**Frontend port**</span></span> | <span data-ttu-id="42559-145">puerto de Hola Hola puerta de enlace de aplicación escucha el tráfico en</span><span class="sxs-lookup"><span data-stu-id="42559-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="42559-146">**Agente de escucha**</span><span class="sxs-lookup"><span data-stu-id="42559-146">**Listener**</span></span> | <span data-ttu-id="42559-147">Una combinación de un protocolo, una configuración de IP de front-end y el puerto de front-end.</span><span class="sxs-lookup"><span data-stu-id="42559-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="42559-148">Esto es lo que se escucha en las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="42559-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="42559-149">**Regla**</span><span class="sxs-lookup"><span data-stu-id="42559-149">**Rule**</span></span>| <span data-ttu-id="42559-150">Rutas Hola tráfico toohello back-end adecuados en función de la configuración de HTTP.</span><span class="sxs-lookup"><span data-stu-id="42559-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="42559-151">Agregar un sondeo tooan aplicación puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="42559-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="42559-152">Hello fragmento de código siguiente agrega un sondeo tooan aplicación puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="42559-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="42559-153">Eliminación de un sondeo de una puerta de enlace de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="42559-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="42559-154">Hola siguiente fragmento de código quita un sondeo de una puerta de enlace de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="42559-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="42559-155">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="42559-155">Get application gateway DNS name</span></span>

<span data-ttu-id="42559-156">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="42559-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="42559-157">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="42559-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="42559-158">los usuarios finales de tooensure puede presionar la puerta de enlace de aplicaciones de hello puede usarse un registro CNAME toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="42559-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="42559-159">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="42559-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="42559-160">toodo, detalles de recuperación de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="42559-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="42559-161">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="42559-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="42559-162">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42559-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="42559-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42559-163">Next steps</span></span>

<span data-ttu-id="42559-164">Obtenga información acerca de la descarga de SSL tooconfigure visitando: [configurar la descarga de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="42559-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

