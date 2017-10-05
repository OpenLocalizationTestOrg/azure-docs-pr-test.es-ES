---
title: "Configuración del firewall de aplicaciones web en una instancia de Azure Application Gateway | Microsoft Docs"
description: "En este artículo se proporcionan instrucciones sobre cómo comenzar a usar el firewall de aplicaciones web en una instancia de Application Gateway nueva o existente."
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
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="5e0d1-103">Configuración del firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente</span><span class="sxs-lookup"><span data-stu-id="5e0d1-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e0d1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5e0d1-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="5e0d1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e0d1-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="5e0d1-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5e0d1-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="5e0d1-107">Aprenda a crear una instancia de Application Gateway habilitada para un firewall de aplicaciones web o a agregar un firewall de aplicaciones web a una instancia de Application Gateway existente.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="5e0d1-108">El firewall de aplicaciones web (WAF) de Azure Application Gateway protege las aplicaciones web de ataques web comunes, como inyección de código SQL, ataques de scripts entre sitios y secuestros de sesiones.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="5e0d1-109">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="5e0d1-110">Proporciona conmutación por error, solicitudes HTTP de enrutamiento de rendimiento entre distintos servidores, independientemente de que se encuentren en la nube o en una implementación local.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="5e0d1-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="5e0d1-112">Para obtener una lista completa de las características admitidas, consulte la [información general sobre Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="5e0d1-113">En el artículo siguiente se muestra cómo [agregar el firewall de aplicaciones web a una instancia de Application Gateway existente](#add-web-application-firewall-to-an-existing-application-gateway) y [crear una instancia de Application Gateway que usa el firewall de aplicaciones web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagen de escenario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="5e0d1-115">Diferencias de configuración de WAF</span><span class="sxs-lookup"><span data-stu-id="5e0d1-115">WAF configuration differences</span></span>

<span data-ttu-id="5e0d1-116">Si ha leído [Creación de una puerta de enlace de aplicaciones con PowerShell](application-gateway-create-gateway-arm.md), comprenderá los valores de SKU que se deben configurar al crear una instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="5e0d1-117">WAF proporciona una configuración adicional que se puede definir al configurar la SKU en una instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="5e0d1-118">No hay ningún otro cambio que deba realizar en la instancia de Application Gateway propiamente dicha.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="5e0d1-119">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="5e0d1-119">**Setting**</span></span> | <span data-ttu-id="5e0d1-120">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="5e0d1-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="5e0d1-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="5e0d1-121">**SKU**</span></span> |<span data-ttu-id="5e0d1-122">Una instancia de Application Gateway normal sin WAF admite los tamaños **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="5e0d1-123">Con la introducción de WAF, hay dos SKU adicionales, **WAF\_Medium** y **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="5e0d1-124">No se admite WAF en instancias de Application Gateway de pequeño tamaño.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="5e0d1-125">**Nivel**</span><span class="sxs-lookup"><span data-stu-id="5e0d1-125">**Tier**</span></span> | <span data-ttu-id="5e0d1-126">Los valores disponibles son **Estándar** o **WAF**.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="5e0d1-127">Cuando se usa el firewall de aplicaciones web, se debe seleccionar **WAF**.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="5e0d1-128">**Modo**</span><span class="sxs-lookup"><span data-stu-id="5e0d1-128">**Mode**</span></span> | <span data-ttu-id="5e0d1-129">Esta configuración es el modo de WAF.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="5e0d1-130">Los valores permitidos son **Detección** y **Prevención**.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="5e0d1-131">Cuando WAF está configurado en modo de detección, todas las amenazas se almacenan en un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="5e0d1-132">En modo de prevención, los eventos se siguen registrando pero el atacante recibe una respuesta 403 no autorizado de la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="5e0d1-133">Adición del firewall de aplicaciones web a una instancia de Application Gateway existente</span><span class="sxs-lookup"><span data-stu-id="5e0d1-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="5e0d1-134">Asegúrese de que está usando la versión más reciente de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="5e0d1-135">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="5e0d1-136">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="5e0d1-137">Seleccione la suscripción que se usará en este escenario.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="5e0d1-138">Recupere la puerta de enlace a la que va a agregar el firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="5e0d1-139">Configure la SKU del firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="5e0d1-140">Los tamaños disponibles son **WAF\_Large** y **WAF\_Medium**.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="5e0d1-141">Cuando se usa un firewall de aplicaciones web el nivel debe ser **WAF** y la capacidad se debe confirmar cuando se establece la SKU.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="5e0d1-142">Configure las opciones de WAF, tal como se define en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5e0d1-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="5e0d1-143">Para **FirewallMode**, los valores disponibles son prevención y detección.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="5e0d1-144">Actualice la instancia de Application Gateway con la configuración definida en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="5e0d1-145">Este comando actualiza la instancia de Application Gateway con el firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="5e0d1-146">Consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md) para entender cómo ver los registros de la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="5e0d1-147">Debido a la naturaleza de la seguridad de WAF, los registros se deben revisar periódicamente para entender la postura de seguridad de las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="5e0d1-148">Creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="5e0d1-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="5e0d1-149">Los pasos siguientes le llevan por el proceso entero de creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="5e0d1-150">Asegúrese de que está usando la versión más reciente de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="5e0d1-151">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="5e0d1-152">Inicie sesión en Azure mediante la ejecución de `Login-AzureRmAccount`; se le pedirá que se autentique con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="5e0d1-153">Compruebe las suscripciones de la cuenta mediante la ejecución de `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="5e0d1-154">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="5e0d1-155">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5e0d1-155">Create a resource group</span></span>

<span data-ttu-id="5e0d1-156">Cree un grupo de recursos para la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="5e0d1-157">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="5e0d1-158">Esta ubicación se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="5e0d1-159">Asegúrese de que todos los comandos para crear una instancia de Application Gateway usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="5e0d1-160">En el ejemplo anterior, creamos un grupo de recursos denominado "appgw-RG" y la ubicación "West US".</span><span class="sxs-lookup"><span data-stu-id="5e0d1-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="5e0d1-161">Si necesita configurar un sondeo personalizado para la instancia de Application Gateway, consulte [Creación de una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="5e0d1-162">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="5e0d1-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="5e0d1-163">Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="5e0d1-163">Configure virtual network</span></span>

<span data-ttu-id="5e0d1-164">Azure Application Gateway requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="5e0d1-165">En este paso, creará una red virtual con un espacio de direcciones de 10.0.0.0/16 y dos subredes, una para la instancia de Application Gateway y otra para los miembros del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="5e0d1-166">Configuración de direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="5e0d1-166">Configure public IP address</span></span>

<span data-ttu-id="5e0d1-167">Para controlar las solicitudes externas, la instancia de Application Gateway requiere una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="5e0d1-168">Esta dirección IP pública no debe tener definido un elemento `DomainNameLabel` para que lo pueda usar la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="5e0d1-169">Configuración de la instancia de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="5e0d1-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="5e0d1-170">Las instancias de Application Gateway creadas con la configuración de firewall de aplicación web básica se configuran con CRS 3.0 para protección.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="5e0d1-171">Obtención del nombre DNS de una instancia de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="5e0d1-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="5e0d1-172">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="5e0d1-173">Cuando se utiliza una dirección IP pública, la instancia de Application Gateway requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="5e0d1-174">Para asegurarse de que los usuarios finales puedan llegar a la instancia de Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de esa instancia.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="5e0d1-175">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="5e0d1-176">Para configurar un alias, recupere los detalles de la instancia de Application Gateway y su nombre de IP o DNS asociado mediante el elemento PublicIPAddress asociado a dicha instancia.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="5e0d1-177">El nombre DNS de la instancia de Application Gateway se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="5e0d1-178">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5e0d1-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5e0d1-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e0d1-179">Next steps</span></span>

<span data-ttu-id="5e0d1-180">Aprenda a configurar el registro de diagnóstico para registrar los eventos que se detectan o impiden con el firewall de aplicaciones web en [Diagnósticos de Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5e0d1-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
