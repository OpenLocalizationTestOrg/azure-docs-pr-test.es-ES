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
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="9d5fd-103">Configuración del firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente</span><span class="sxs-lookup"><span data-stu-id="9d5fd-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d5fd-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9d5fd-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="9d5fd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d5fd-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="9d5fd-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9d5fd-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="9d5fd-107">Obtenga información acerca de cómo toocreate un servidor de seguridad de la aplicación web habilita la puerta de enlace de aplicaciones o agregar tooan de firewall de aplicación web existente de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="9d5fd-108">servidor de aplicaciones web Hello (WAFS) en la puerta de enlace de aplicaciones de Azure protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL, ataques XSS y apropiaciones de sesión.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="9d5fd-109">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="9d5fd-110">Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="9d5fd-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="9d5fd-112">toofind una lista completa de las características admitidas, visite: [información general de Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d5fd-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="9d5fd-113">Hello siguiente artículo se muestra cómo demasiado[agregar tooan de firewall de aplicación web existente de la puerta de enlace de aplicaciones](#add-web-application-firewall-to-an-existing-application-gateway) y [crear una puerta de enlace de la aplicación que utiliza el servidor de aplicaciones web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="9d5fd-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagen de escenario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="9d5fd-115">Diferencias de configuración de WAF</span><span class="sxs-lookup"><span data-stu-id="9d5fd-115">WAF configuration differences</span></span>

<span data-ttu-id="9d5fd-116">Si ha leído [crear una puerta de enlace de la aplicación con PowerShell](application-gateway-create-gateway-arm.md), comprender Hola SKU configuración tooconfigure al crear una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="9d5fd-117">WAFS proporciona toodefine de opciones de configuración adicionales al configurar Hola SKU en una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="9d5fd-118">No hay ningún otro cambio que realice en hello aplicación puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="9d5fd-119">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="9d5fd-119">**Setting**</span></span> | <span data-ttu-id="9d5fd-120">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="9d5fd-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="9d5fd-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="9d5fd-121">**SKU**</span></span> |<span data-ttu-id="9d5fd-122">Una instancia de Application Gateway normal sin WAF admite los tamaños **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="9d5fd-123">Con la introducción de Hola de WAFS, hay dos SKU adicionales, **WAFS\_medio** y **WAFS\_grande**.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="9d5fd-124">No se admite WAF en instancias de Application Gateway de pequeño tamaño.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="9d5fd-125">**Nivel**</span><span class="sxs-lookup"><span data-stu-id="9d5fd-125">**Tier**</span></span> | <span data-ttu-id="9d5fd-126">Hola los valores disponibles son **estándar** o **WAFS**.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="9d5fd-127">Cuando se usa el firewall de aplicaciones web, se debe seleccionar **WAF**.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="9d5fd-128">**Modo**</span><span class="sxs-lookup"><span data-stu-id="9d5fd-128">**Mode**</span></span> | <span data-ttu-id="9d5fd-129">Esta opción es modo de saludo de WAFS.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="9d5fd-130">Los valores permitidos son **Detección** y **Prevención**.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="9d5fd-131">Cuando WAF está configurado en modo de detección, todas las amenazas se almacenan en un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="9d5fd-132">En el modo de prevención, todavía se registran eventos pero atacante Hola recibe una respuesta no autorizado 403 Hola Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="9d5fd-133">Agregar tooan de firewall de aplicación web existente de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9d5fd-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="9d5fd-134">Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9d5fd-135">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9d5fd-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="9d5fd-136">Inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="9d5fd-137">Seleccione hello toouse de suscripción para este escenario.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="9d5fd-138">Recuperar la puerta de enlace de Hola que va a agregar el servidor de aplicaciones web a.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="9d5fd-139">Configurar la aplicación firewall sku de hello web.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="9d5fd-140">los tamaños disponibles de Hello son **WAFS\_grande** y **WAFS\_medio**.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="9d5fd-141">Cuando se usa firewall de aplicación web debe ser el nivel de hello **WAFS**, capacidad de Hola se debe confirmar al establecer Hola sku.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="9d5fd-142">Configurar opciones de hello WAFS tal como se define en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="9d5fd-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="9d5fd-143">Para **FirewallMode**, valores disponibles de hello son la detección y prevención.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="9d5fd-144">Actualizar Hola puerta de enlace de aplicaciones con valores de hello definidos en hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="9d5fd-145">Este comando actualiza Hola puerta de enlace de aplicación con el servidor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="9d5fd-146">Visite [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md) toounderstand cómo tooview registros para la puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="9d5fd-147">Debido a toohello la naturaleza de seguridad de WAFS, registros necesidad toobe revisarse periódicamente postura de seguridad de hello toounderstand de las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="9d5fd-148">Creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="9d5fd-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="9d5fd-149">Hello pasos siguientes le conducen por proceso completo de Hola desde principio tooend para crear una puerta de enlace de la aplicación con el servidor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="9d5fd-150">Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9d5fd-151">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9d5fd-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="9d5fd-152">Inicie sesión en tooAzure ejecutando `Login-AzureRmAccount`, son tooauthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="9d5fd-153">Compruebe las suscripciones de hello para la cuenta de hello ejecutando`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="9d5fd-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="9d5fd-154">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="9d5fd-155">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9d5fd-155">Create a resource group</span></span>

<span data-ttu-id="9d5fd-156">Crear un grupo de recursos para hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="9d5fd-157">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9d5fd-158">Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9d5fd-159">Asegúrese de que todos los comandos que utiliza toocreate una puerta de enlace de aplicación Hola mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="9d5fd-160">En el anterior ejemplo de Hola, hemos creado un grupo de recursos denominado "Appgw-RG" y la ubicación "oeste de Estados Unidos."</span><span class="sxs-lookup"><span data-stu-id="9d5fd-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="9d5fd-161">Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9d5fd-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="9d5fd-162">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="9d5fd-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="9d5fd-163">Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="9d5fd-163">Configure virtual network</span></span>

<span data-ttu-id="9d5fd-164">Azure Application Gateway requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="9d5fd-165">En este paso, creará una red virtual con un espacio de direcciones de 10.0.0.0/16 y dos subredes, uno para la puerta de enlace de aplicación hello y otro para los miembros del grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="9d5fd-166">Configuración de direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="9d5fd-166">Configure public IP address</span></span>

<span data-ttu-id="9d5fd-167">En solicitudes externas de orden toohandle, puerta de enlace de aplicaciones requiere una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="9d5fd-168">Esta dirección IP pública no debe tener un `DomainNameLabel` definido toobe usa Hola Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="9d5fd-169">Configurar la puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="9d5fd-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="9d5fd-170">Las puertas de enlace de aplicaciones creadas con la configuración del firewall de aplicación de hello web básico se configuran con CRS 3.0 para protección.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9d5fd-171">Obtención del nombre DNS de una instancia de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9d5fd-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="9d5fd-172">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9d5fd-173">Cuando se utiliza una dirección IP pública, la instancia de Application Gateway requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9d5fd-174">los usuarios finales de tooensure puede llegar a Hola puerta de enlace de aplicaciones, un registro CNAME puede ser usado toopoint toohello extremo público de hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="9d5fd-175">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d5fd-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9d5fd-176">tooconfigure un alias, recuperar los detalles de hello puerta de enlace de aplicaciones y su nombre IP/DNS asociado mediante hello PublicIPAddress elemento adjunta toohello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="9d5fd-177">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="9d5fd-178">no se recomienda el uso de Hola de registros de un puesto que Hola VIP puede cambiar en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d5fd-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9d5fd-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d5fd-179">Next steps</span></span>

<span data-ttu-id="9d5fd-180">Obtenga información acerca de cómo tooconfigure el registro de diagnóstico, eventos de hello toolog si se detecta o prevenir con servidor de aplicaciones web visitando [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="9d5fd-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
