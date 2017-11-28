---
title: "Creación y administración de Azure Application Gateway: PowerShell | Microsoft Docs"
description: "Esta página proporciona instrucciones para crear, configurar, iniciar y eliminar una Puerta de enlace de aplicaciones de Azure mediante el Administrador de recursos de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 5f1713365406764998de505ff62309bab9fa2567
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="234a5-103">Creación, inicio o eliminación de una Puerta de enlace de aplicaciones con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="234a5-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="234a5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="234a5-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="234a5-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="234a5-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="234a5-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="234a5-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="234a5-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="234a5-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="234a5-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="234a5-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="234a5-109">Puerta de enlace de aplicaciones de Azure es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="234a5-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="234a5-110">Proporciona solicitudes HTTP de enrutamiento del rendimiento y conmutación por error y entre distintos servidores, independientemente de que se encuentren en la nube o en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="234a5-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="234a5-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="234a5-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="234a5-112">Para encontrar una lista completa de las características admitidas, visite [Introducción a Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="234a5-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="234a5-113">Este artículo le guiará por los pasos necesarios para crear, configurar, iniciar y eliminar una Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="234a5-114">Antes de trabajar con recursos de Azure, es importante comprender que Azure tiene actualmente dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="234a5-114">Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="234a5-115">Antes de trabajar con los recursos de Azure asegúrese de que conoce los [modelos de implementación y las herramientas](../azure-classic-rm.md) .</span><span class="sxs-lookup"><span data-stu-id="234a5-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="234a5-116">Puede ver la documentación de las distintas herramientas haciendo clic en las fichas en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="234a5-116">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="234a5-117">Este documento describe la creación de una puerta de enlace de aplicaciones con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="234a5-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="234a5-118">Para utilizar la versión clásica, vaya a [Creación, inicio o eliminación de una puerta de enlace de aplicaciones](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="234a5-118">To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="234a5-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="234a5-119">Before you begin</span></span>

1. <span data-ttu-id="234a5-120">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="234a5-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="234a5-121">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la [página Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="234a5-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="234a5-122">Si tiene una red virtual existente, seleccione una subred vacía existente o cree una subred en la red virtual existente, únicamente para uso de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="234a5-123">No se puede implementar la puerta de enlace de la aplicación en una red virtual diferente de los recursos que se van a implementar detrás de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="234a5-124">Los servidores que configure para que usen la Puerta de enlace de aplicaciones deben existir, o bien sus puntos de conexión deben haberse creado en la red virtual o tener una dirección IP/VIP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="234a5-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="234a5-125">¿Qué se necesita para crear una Puerta de enlace de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="234a5-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="234a5-126">**Grupo de servidores back-end**: lista de direcciones IP, FQDN y NIC de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="234a5-126">**Backend server pool:** The list of IP addresses, FQDNs, or NICs of the backend servers.</span></span> <span data-ttu-id="234a5-127">Si se utilizan direcciones IP, estas deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="234a5-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="234a5-128">**Configuración del grupo de servidores back-end** : cada grupo tiene una configuración como el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="234a5-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="234a5-129">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="234a5-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="234a5-130">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-130">**frontend port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="234a5-131">El tráfico llega a este puerto y, a continuación, se redirige a uno de los servidores backend.</span><span class="sxs-lookup"><span data-stu-id="234a5-131">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="234a5-132">**Agente de escucha**: tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="234a5-132">**Listener:** The listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="234a5-133">**Regla**: enlaza el agente de escucha y el grupo de servidores back-end, y define a qué grupo de servidores back-end se debe dirigir el tráfico cuando llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="234a5-133">**Rule:** The rule binds the listener, the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="234a5-134">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="234a5-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="234a5-135">Asegúrese de que está usando la versión más reciente de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="234a5-135">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="234a5-136">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="234a5-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="234a5-137">Inicie sesión en Azure y escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="234a5-137">Log in to Azure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="234a5-138">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="234a5-138">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="234a5-139">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="234a5-139">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="234a5-140">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="234a5-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="234a5-141">El Administrador de recursos de Azure requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="234a5-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="234a5-142">Esta ubicación se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="234a5-142">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="234a5-143">Asegúrese de que todos los comandos para crear una puerta de enlace de aplicaciones usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="234a5-143">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="234a5-144">En el ejemplo anterior, creamos un grupo de recursos denominado **ContosoRG** y la ubicación **Este de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="234a5-144">In the example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="234a5-145">Si necesita configurar un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [Creación de una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="234a5-145">If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="234a5-146">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="234a5-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="234a5-147">Creación de objetos de configuración de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="234a5-147">Create the application gateway configuration objects</span></span>

<span data-ttu-id="234a5-148">Se deben haber definido todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-148">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="234a5-149">En los pasos siguientes, se crean los elementos de configuración necesarios para un recurso de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-149">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign the address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with the address space of 10.0.0.0/16 and add the subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used to connect to the application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. The gateway picks up an IP addressfrom the configured subnet and routes network traffic to the IP addresses in the backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with the addresses of your web servers. These backend pool members are all validated to be healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed to them when requests come into the application gateway. Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings to determine the protocol and port that is used when sending traffic to the backend servers. Cookie-based sessions are also determined by the backend HTTP settings.  If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used to connect to the application gateway through the public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure the frontend IP configuration with the public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure the listener.  The listener is a combination of the front end IP configuration, protocol, and port and is used to receive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used to route traffic to the backend servers. The backend pool settings, listener, and backend pool created in the previous steps make up the rule. Based on the criteria defined traffic is routed to the appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU for the application gateway, this determines the size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="234a5-150">Cuando finalice, recupere los detalles sobre DNS y VIP de la puerta de enlace de aplicaciones del recurso de IP pública asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-150">When complete, retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="234a5-151">Eliminación de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="234a5-151">Delete the application gateway</span></span>

<span data-ttu-id="234a5-152">En el ejemplo siguiente se elimina la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-152">The following example deletes the application gateway.</span></span>

```powershell
# Retrieve the application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops the application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="234a5-153">Se puede usar el modificador **-force** para suprimir el mensaje de confirmación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="234a5-153">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="234a5-154">Para comprobar que se ha quitado el servicio, puede usar el cmdlet `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="234a5-154">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="234a5-155">Este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="234a5-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="234a5-156">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="234a5-156">Get application gateway DNS name</span></span>

<span data-ttu-id="234a5-157">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="234a5-157">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="234a5-158">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="234a5-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="234a5-159">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="234a5-159">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="234a5-160">Para ello, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="234a5-161">Esta operación se puede realizar con Azure DNS u otro proveedor de DNS, mediante la creación de un registro CNAME que apunte a la [dirección IP pública](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="234a5-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="234a5-162">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="234a5-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="234a5-163">Se asigna una dirección IP a la puerta de enlace de aplicaciones cuando se inicia el servicio.</span><span class="sxs-lookup"><span data-stu-id="234a5-163">An IP address is assigned to the application gateway when the service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="234a5-164">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="234a5-164">Delete all resources</span></span>

<span data-ttu-id="234a5-165">Para eliminar todos los recursos creados en este artículo, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="234a5-165">To delete all resources created in this article, complete the following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="234a5-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="234a5-166">Next steps</span></span>

<span data-ttu-id="234a5-167">Si desea configurar la descarga de SSL, consulte [Configuración de una instancia de Application Gateway para la descarga de SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="234a5-167">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="234a5-168">Si quiere configurar una instancia de Application Gateway para usarla con un equilibrador de carga interno, consulte [Creación de una instancia de Application Gateway con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="234a5-168">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="234a5-169">Si desea más información acerca de las opciones de equilibrio de carga en general, visite:</span><span class="sxs-lookup"><span data-stu-id="234a5-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="234a5-170">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="234a5-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="234a5-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="234a5-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
