---
title: "Creación de una puerta de enlace de aplicaciones para hospedar varios sitios | Microsoft Docs"
description: "Esta página proporciona instrucciones para crear y configurar una puerta de enlace de aplicaciones de Azure para hospedar varias aplicaciones web en la misma puerta de enlace."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="1e296-103">Creación de una puerta de enlace de aplicaciones para hospedar varias aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="1e296-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e296-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1e296-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="1e296-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1e296-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="1e296-106">El hospedaje de varios sitios permite implementar más de una aplicación web en la misma puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="1e296-107">Se basa en la presencia de un encabezado host en la solicitud HTTP entrante para determinar el agente de escucha que recibe el tráfico.</span><span class="sxs-lookup"><span data-stu-id="1e296-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="1e296-108">Luego, dicho agente dirige el tráfico al grupo de back-end adecuado, el configurado en la definición de las reglas de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1e296-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="1e296-109">En las aplicaciones web con SSL habilitado, la puerta de enlace de aplicaciones depende de la extensión de la indicación de nombre de servidor (SNI) para elegir el agente de escucha correcto para el tráfico web.En las aplicaciones web con SSL habilitado, Application Gateway depende de la extensión de la indicación de nombre de servidor (SNI) para elegir el agente de escucha correcto para el tráfico web.</span><span class="sxs-lookup"><span data-stu-id="1e296-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="1e296-110">Un uso común del hospedaje de varios sitios es el equilibrio de carga de las solicitudes de diferentes dominios web entre diferentes grupos de servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="1e296-111">De forma similar, varios subdominios del mismo dominio raíz también se pueden hospedar en la misma puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="1e296-112">Escenario</span><span class="sxs-lookup"><span data-stu-id="1e296-112">Scenario</span></span>

<span data-ttu-id="1e296-113">En el siguiente ejemplo, la puerta de enlace de aplicaciones sirve el tráfico a contoso.com y a fabrikam.com con dos grupos de servidores back-end: el grupo de servidores de contoso y el grupo de servidores de fabrikam.</span><span class="sxs-lookup"><span data-stu-id="1e296-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="1e296-114">Se puede usar una configuración similar para hospedar subdominios como app.contoso.com y blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1e296-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="1e296-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1e296-116">Before you begin</span></span>

1. <span data-ttu-id="1e296-117">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="1e296-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="1e296-118">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la página [Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1e296-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="1e296-119">Los servidores agregados al grupo de back-end para usar la puerta de enlace de aplicaciones deben existir, o bien sus puntos de conexión deben haberse creado en la red virtual en una red virtual o con una dirección IP/VIP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="1e296-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="1e296-120">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1e296-120">Requirements</span></span>

* <span data-ttu-id="1e296-121">**Grupo de servidores back-end** : lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="1e296-122">Las direcciones IP que se enumeran deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="1e296-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="1e296-123">También puede utilizarse el FQDN.</span><span class="sxs-lookup"><span data-stu-id="1e296-123">FQDN can also be used.</span></span>
* <span data-ttu-id="1e296-124">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="1e296-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="1e296-125">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="1e296-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="1e296-126">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="1e296-127">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="1e296-128">**Agente de escucha** : tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="1e296-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="1e296-129">En el caso de las puertas de enlace de aplicaciones con sitios múltiples habilitados, también se agregan el nombre de host y los indicadores de SNI.</span><span class="sxs-lookup"><span data-stu-id="1e296-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="1e296-130">**Regla:** enlaza el agente de escucha y el grupo de servidores back-end, y define a qué grupo de servidores back-end se debe redireccionar el tráfico que llegue a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="1e296-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="1e296-131">Las reglas se procesan en el orden en que aparecen y el tráfico se dirige a través de la primera regla que coincida independientemente de la especificidad.</span><span class="sxs-lookup"><span data-stu-id="1e296-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="1e296-132">Por ejemplo, si tiene una regla que usa un agente de escucha básico y una regla que usa un agente de escucha multisitio en el mismo puerto, la regla con el agente de escucha multisitio debe aparecer antes que la regla con el agente de escucha básico para que la regla multisitio funcione según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="1e296-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="1e296-133">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-133">Create an application gateway</span></span>

<span data-ttu-id="1e296-134">A continuación se muestran los pasos necesarios para crear una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="1e296-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="1e296-135">Cree un grupo de recursos para el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e296-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="1e296-136">Cree una red virtual, subredes y una IP pública para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="1e296-137">Cree un objeto de configuración de la Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="1e296-138">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="1e296-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="1e296-139">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="1e296-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="1e296-140">Asegúrese de que está usando la versión más reciente de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e296-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="1e296-141">En [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md), encontrará más información al respecto.</span><span class="sxs-lookup"><span data-stu-id="1e296-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="1e296-142">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1e296-142">Step 1</span></span>

<span data-ttu-id="1e296-143">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="1e296-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="1e296-144">Se le solicita que se autentique con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="1e296-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="1e296-145">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1e296-145">Step 2</span></span>

<span data-ttu-id="1e296-146">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="1e296-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="1e296-147">Paso 3</span><span class="sxs-lookup"><span data-stu-id="1e296-147">Step 3</span></span>

<span data-ttu-id="1e296-148">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="1e296-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="1e296-149">Paso 4</span><span class="sxs-lookup"><span data-stu-id="1e296-149">Step 4</span></span>

<span data-ttu-id="1e296-150">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="1e296-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="1e296-151">También puede crear etiquetas para un grupo de recursos de la puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="1e296-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="1e296-152">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="1e296-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="1e296-153">Esta ubicación se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e296-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="1e296-154">Asegúrese de que todos los comandos para crear una puerta de enlace de aplicaciones usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e296-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="1e296-155">En el ejemplo anterior, creamos un grupo de recursos denominado **appgw-RG** cuya ubicación es **oeste de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="1e296-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="1e296-156">Si necesita configurar un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [Creación de una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1e296-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="1e296-157">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e296-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="1e296-158">Creación una red virtual y subredes</span><span class="sxs-lookup"><span data-stu-id="1e296-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="1e296-159">En el ejemplo siguiente se muestra cómo crear una red virtual con el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e296-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="1e296-160">En este paso, se crean dos subredes.</span><span class="sxs-lookup"><span data-stu-id="1e296-160">Two subnets are created in this step.</span></span> <span data-ttu-id="1e296-161">La primera es para la propia puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="1e296-162">La puerta de enlace de aplicaciones requiere una subred propia que contenga sus instancias.</span><span class="sxs-lookup"><span data-stu-id="1e296-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="1e296-163">En dicha subred solo se pueden implementar otras puertas de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="1e296-164">La segunda subred se usa para contener los servidores back-end de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="1e296-165">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1e296-165">Step 1</span></span>

<span data-ttu-id="1e296-166">Asigne el intervalo de direcciones 10.0.0.0/24 a la variable subnet que se va a usar para contener la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="1e296-167">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1e296-167">Step 2</span></span>

<span data-ttu-id="1e296-168">Asigne el intervalo de direcciones 10.0.1.0/24 a la variable subnet2 que se va a usar para los grupos back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="1e296-169">Paso 3</span><span class="sxs-lookup"><span data-stu-id="1e296-169">Step 3</span></span>

<span data-ttu-id="1e296-170">Cree una red virtual denominada **appgwvnet** en el grupo de recursos **appgw-rg** para la región oeste de EE. UU. con el prefijo 10.0.0.0/16 y las subredes 10.0.0.0/24, y 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="1e296-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="1e296-171">Paso 4</span><span class="sxs-lookup"><span data-stu-id="1e296-171">Step 4</span></span>

<span data-ttu-id="1e296-172">Asignación de una variable de subred en los pasos siguientes para crear una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="1e296-173">Creación de una dirección IP pública para la configuración del front-end</span><span class="sxs-lookup"><span data-stu-id="1e296-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="1e296-174">Cree un recurso IP público **publicIP01** en el grupo de recursos **appgw-rg** para la región Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="1e296-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="1e296-175">Se asigna una dirección IP a la puerta de enlace de aplicaciones cuando se inicia el servicio.</span><span class="sxs-lookup"><span data-stu-id="1e296-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="1e296-176">Creación de una configuración de puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-176">Create application gateway configuration</span></span>

<span data-ttu-id="1e296-177">Antes de crear la puerta de enlace de aplicaciones, debe configurar todos los elementos de configuración.</span><span class="sxs-lookup"><span data-stu-id="1e296-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="1e296-178">En los pasos siguientes, se crean los elementos de configuración necesarios para un recurso de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="1e296-179">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1e296-179">Step 1</span></span>

<span data-ttu-id="1e296-180">Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="1e296-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="1e296-181">Cuando se inicia la puerta de enlace de aplicaciones, elige una dirección IP de la subred configurada y redirige el tráfico de la red a las direcciones IP en el grupo IP de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="1e296-182">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="1e296-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="1e296-183">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1e296-183">Step 2</span></span>

<span data-ttu-id="1e296-184">Configure el grupo de direcciones IP de back-end llamado **pool01** y **pool2** con las direcciones IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** para **pool1** y **134.170.186.46**, **134.170.189.221**, **134.170.186.50** para **pool2**.</span><span class="sxs-lookup"><span data-stu-id="1e296-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="1e296-185">En este ejemplo, hay dos grupos de back-end para enrutar el tráfico de red en función del sitio solicitado.</span><span class="sxs-lookup"><span data-stu-id="1e296-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="1e296-186">Un grupo recibe el tráfico del sitio "contoso.com" y otro lo recibe del sitio "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="1e296-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="1e296-187">Tiene que reemplazar las direcciones IP anteriores para agregar sus propios puntos de conexión de direcciones IP de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1e296-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="1e296-188">En lugar de las direcciones IP internas, también se pueden usar direcciones IP públicas, el nombre de dominio completo o la NIC de una máquina virtual para las instancias de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="1e296-189">Use el parámetro "-BackendFQDNs" en PowerShell para especificar FQDN, en lugar de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1e296-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="1e296-190">Paso 3</span><span class="sxs-lookup"><span data-stu-id="1e296-190">Step 3</span></span>

<span data-ttu-id="1e296-191">Configure la opción de la puerta de enlace de aplicaciones **poolsetting01** y **poolsetting02** para el tráfico de red con carga equilibrada en el grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="1e296-192">En este ejemplo, se configuran distintas opciones de configuración para los grupos de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="1e296-193">Cada grupo de back-end puede tener su propia configuración de grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e296-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="1e296-194">Paso 4</span><span class="sxs-lookup"><span data-stu-id="1e296-194">Step 4</span></span>

<span data-ttu-id="1e296-195">Configuración de la dirección IP de front-end con el punto de conexión de IP pública</span><span class="sxs-lookup"><span data-stu-id="1e296-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="1e296-196">Paso 5</span><span class="sxs-lookup"><span data-stu-id="1e296-196">Step 5</span></span>

<span data-ttu-id="1e296-197">Configuración del puerto front-end de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="1e296-198">Paso 6</span><span class="sxs-lookup"><span data-stu-id="1e296-198">Step 6</span></span>

<span data-ttu-id="1e296-199">Configuración de dos certificados SSL para los dos sitios web que vamos a admitir en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e296-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="1e296-200">Uno de ellos es para el tráfico de contoso.com y el otro es para el de fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="1e296-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="1e296-201">Deben ser certificados emitidos por una entidad de certificación para sus sitios web.</span><span class="sxs-lookup"><span data-stu-id="1e296-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="1e296-202">Los certificados autofirmados se admiten, pero no se recomiendan para el tráfico de producción.</span><span class="sxs-lookup"><span data-stu-id="1e296-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="1e296-203">Paso 7</span><span class="sxs-lookup"><span data-stu-id="1e296-203">Step 7</span></span>

<span data-ttu-id="1e296-204">Configuración de dos agentes de escucha para los dos sitios web del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e296-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="1e296-205">En este paso se configuran los agentes de escucha para la dirección IP pública, el puerto y el host usados para recibir el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="1e296-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="1e296-206">El parámetro HostName es necesario para lograr la compatibilidad con varios sitios y se debe establecer en el sitio web adecuado para el que se recibe el tráfico.</span><span class="sxs-lookup"><span data-stu-id="1e296-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="1e296-207">El parámetro RequireServerNameIndication debe establecerse en true para los sitios web que necesitan compatibilidad con SSL en un escenario de múltiples hosts.</span><span class="sxs-lookup"><span data-stu-id="1e296-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="1e296-208">Si se requiere compatibilidad con SSL, también es preciso especificar el certificado SSL que se usa para proteger el tráfico de esa aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1e296-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="1e296-209">La combinación de FrontendIPConfiguration, FrontendPort y HostName debe ser única en cada agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="1e296-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="1e296-210">Cada agente de escucha puede admitir solo un certificado.</span><span class="sxs-lookup"><span data-stu-id="1e296-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="1e296-211">Paso 8</span><span class="sxs-lookup"><span data-stu-id="1e296-211">Step 8</span></span>

<span data-ttu-id="1e296-212">Creación de la configuración de dos reglas para las dos aplicaciones web de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e296-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="1e296-213">Una regla une los agentes de escucha, los grupos de back-end y la configuración de http.</span><span class="sxs-lookup"><span data-stu-id="1e296-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="1e296-214">En este paso se configura la puerta de enlace de aplicaciones para que use una regla de enrutamiento básica, una para cada sitio web.</span><span class="sxs-lookup"><span data-stu-id="1e296-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="1e296-215">El tráfico para cada sitio web lo recibe el agente de escucha que tenga configurado y, luego, se dirige a su grupo de back-end configurado, para lo que se usan las propiedades especificadas en BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="1e296-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="1e296-216">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="1e296-216">Step 9</span></span>

<span data-ttu-id="1e296-217">Configuración del número de instancias y el tamaño de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="1e296-218">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-218">Create application gateway</span></span>

<span data-ttu-id="1e296-219">Cree una puerta de enlace de aplicaciones con todos los objetos de configuración de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="1e296-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="1e296-220">El aprovisionamiento de Application Gateway es una operación larga y puede tardar algún tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="1e296-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="1e296-221">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1e296-221">Get application gateway DNS name</span></span>

<span data-ttu-id="1e296-222">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="1e296-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="1e296-223">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="1e296-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="1e296-224">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="1e296-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="1e296-225">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1e296-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="1e296-226">Para ello, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="1e296-227">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="1e296-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="1e296-228">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1e296-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1e296-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e296-229">Next steps</span></span>

<span data-ttu-id="1e296-230">Aprenda a proteger sitios web con [Firewall de aplicaciones web de Application Gateway (versión preliminar)](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1e296-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

