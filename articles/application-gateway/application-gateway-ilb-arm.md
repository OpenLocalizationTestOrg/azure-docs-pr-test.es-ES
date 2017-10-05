---
title: Uso de Azure Application Gateway con el equilibrador de carga interno mediante PowerShell | Microsoft Docs
description: "En esta página se proporcionan instrucciones para crear, configurar, iniciar y eliminar una puerta de enlace de aplicaciones de Azure con un equilibrador de carga interno (ILB) en el Administrador de recursos de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="1228e-103">Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB) mediante el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1228e-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1228e-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="1228e-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="1228e-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1228e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="1228e-106">Puerta de enlace de aplicaciones de Azure se puede configurar con una VIP conexión a Internet o con un punto de conexión interno no expuesto a Internet, también conocido como punto de conexión ILB (equilibrador de carga interno).</span><span class="sxs-lookup"><span data-stu-id="1228e-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="1228e-107">La configuración de la puerta de enlace con un ILB es útil para aplicaciones de línea de negocio internas no expuestas a Internet.</span><span class="sxs-lookup"><span data-stu-id="1228e-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="1228e-108">También es útil para los distintos servicios y niveles de una aplicación de niveles múltiples que se encuentran dentro de un límite de seguridad no expuesto a Internet, pero que aún así siguen necesitando distribución de carga round robin, permanencia de sesión o terminación SSL (Capa de sockets seguros).</span><span class="sxs-lookup"><span data-stu-id="1228e-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="1228e-109">Este artículo le guía por los pasos necesarios para configurar una puerta de enlace de aplicaciones con un ILB.</span><span class="sxs-lookup"><span data-stu-id="1228e-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1228e-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1228e-110">Before you begin</span></span>

1. <span data-ttu-id="1228e-111">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="1228e-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="1228e-112">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la página [Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1228e-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="1228e-113">Tendrá que crear una red virtual y una subred para Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1228e-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="1228e-114">Asegúrese de que ninguna máquina virtual o implementación en la nube usan la subred.</span><span class="sxs-lookup"><span data-stu-id="1228e-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="1228e-115">La puerta de enlace de aplicaciones debe encontrarse en una subred de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="1228e-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="1228e-116">Los servidores que configure para que usen la Puerta de enlace de aplicaciones deben existir, o bien sus puntos de conexión deben haberse creado en la red virtual o tener una dirección IP/VIP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="1228e-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="1228e-117">¿Qué se necesita para crear una Puerta de enlace de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="1228e-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="1228e-118">**Grupo de servidores back-end:** lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="1228e-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="1228e-119">Las direcciones IP que se enumeran deben pertenecer a la red virtual, pero a otra subred de la puerta de enlace de aplicaciones, o deben ser IP/VIP públicas.</span><span class="sxs-lookup"><span data-stu-id="1228e-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="1228e-120">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="1228e-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="1228e-121">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="1228e-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="1228e-122">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1228e-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="1228e-123">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="1228e-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="1228e-124">**Agente de escucha** : tiene un puerto front-end, un protocolo (Http o Https, que distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="1228e-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="1228e-125">**Regla** : enlaza el agente de escucha y el grupo de servidores back-end y define a qué grupo de servidores back-end se dirigirá el tráfico cuando llega a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="1228e-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="1228e-126">Actualmente, solo se admite la regla *básica* .</span><span class="sxs-lookup"><span data-stu-id="1228e-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="1228e-127">La regla *básica* es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="1228e-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="1228e-128">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-128">Create an application gateway</span></span>

<span data-ttu-id="1228e-129">La diferencia entre el uso del Portal de Azure clásico y Azure Resource Manager es el orden en que se crea la puerta de enlace de aplicaciones y los elementos que es necesario configurar.</span><span class="sxs-lookup"><span data-stu-id="1228e-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="1228e-130">Con Resource Manager, todos los elementos que componen una puerta de enlace de aplicaciones se configuran individualmente y, luego, se unen para crear el recurso de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1228e-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="1228e-131">Estos son los pasos necesarios para crear una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="1228e-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="1228e-132">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="1228e-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="1228e-133">Creación de una red virtual y una subred para la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="1228e-134">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="1228e-135">Crear un recurso de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="1228e-136">Creación de un grupo de recursos para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1228e-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="1228e-137">Asegúrese de cambiar el modo de PowerShell para que use los cmdlets de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1228e-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="1228e-138">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1228e-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="1228e-139">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1228e-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="1228e-140">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1228e-140">Step 2</span></span>

<span data-ttu-id="1228e-141">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="1228e-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1228e-142">Se le solicita que se autentique con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="1228e-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="1228e-143">Paso 3</span><span class="sxs-lookup"><span data-stu-id="1228e-143">Step 3</span></span>

<span data-ttu-id="1228e-144">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="1228e-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="1228e-145">Paso 4</span><span class="sxs-lookup"><span data-stu-id="1228e-145">Step 4</span></span>

<span data-ttu-id="1228e-146">Cree un grupo de recursos nuevo (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="1228e-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="1228e-147">El Administrador de recursos de Azure requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="1228e-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="1228e-148">Esta se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1228e-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="1228e-149">Asegúrese de que todos los comandos para crear una puerta de enlace de aplicaciones usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1228e-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="1228e-150">En el ejemplo anterior, creamos un grupo de recursos denominado "appgw-rg" y la ubicación "West US".</span><span class="sxs-lookup"><span data-stu-id="1228e-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="1228e-151">Creación de una red virtual y una subred para la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="1228e-152">En el ejemplo siguiente se muestra cómo crear una red virtual con Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="1228e-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="1228e-153">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1228e-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="1228e-154">Este paso asigna el intervalo de direcciones 10.0.0.0/24 a la variable de subred que se va a usar para crear una red virtual.</span><span class="sxs-lookup"><span data-stu-id="1228e-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="1228e-155">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1228e-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="1228e-156">Este paso crea una red virtual denominada "appgwvnet" en el grupo de recursos "appgw-rg" para la región West US con el prefijo 10.0.0.0/16 y la subred 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="1228e-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="1228e-157">Paso 3</span><span class="sxs-lookup"><span data-stu-id="1228e-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="1228e-158">Este paso asigna el objeto de subred a la variable $subnet para los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="1228e-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="1228e-159">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="1228e-160">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1228e-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="1228e-161">Este paso crea una configuración de la IP de la puerta de enlace de aplicaciones denominada "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="1228e-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="1228e-162">Cuando se inicia la Puerta de enlace de aplicaciones, elige una dirección IP de la subred configurada y redirige el tráfico de red a las direcciones IP en el grupo IP de back-end.</span><span class="sxs-lookup"><span data-stu-id="1228e-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="1228e-163">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="1228e-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="1228e-164">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1228e-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="1228e-165">Este paso configura el grupo de direcciones IP de back-end denominado "pool01" con las direcciones IP "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="1228e-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="1228e-166">Son las direcciones IP que reciben el tráfico de red procedente del punto de conexión de la IP del front-end.</span><span class="sxs-lookup"><span data-stu-id="1228e-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="1228e-167">Reemplaza las direcciones IP anteriores para agregar sus propios puntos de conexión de direcciones IP de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1228e-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="1228e-168">Paso 3</span><span class="sxs-lookup"><span data-stu-id="1228e-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="1228e-169">Este paso configura la opción de la puerta de enlace de aplicaciones "poolsetting01" para el tráfico de red con carga equilibrada del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="1228e-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="1228e-170">Paso 4</span><span class="sxs-lookup"><span data-stu-id="1228e-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="1228e-171">Este paso configura el puerto IP del front-end denominado "frontendport01" para el ILB.</span><span class="sxs-lookup"><span data-stu-id="1228e-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="1228e-172">Paso 5</span><span class="sxs-lookup"><span data-stu-id="1228e-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="1228e-173">Este paso crea la configuración de la IP del front-end llamada "fipconfig01" y la asocia una dirección IP privada de la subred de la red virtual actual.</span><span class="sxs-lookup"><span data-stu-id="1228e-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="1228e-174">Paso 6</span><span class="sxs-lookup"><span data-stu-id="1228e-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="1228e-175">Este paso crea el agente de escucha "listener01" y asocia el puerto front-end con la configuración de la IP del front-end.</span><span class="sxs-lookup"><span data-stu-id="1228e-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="1228e-176">Paso 7</span><span class="sxs-lookup"><span data-stu-id="1228e-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="1228e-177">Este paso crea la regla de enrutamiento del equilibrador de carga denominada "rule01" que configura el comportamiento del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1228e-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="1228e-178">Paso 8</span><span class="sxs-lookup"><span data-stu-id="1228e-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="1228e-179">Este paso configura el tamaño de instancia de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1228e-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="1228e-180">El valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="1228e-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="1228e-181">El valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="1228e-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="1228e-182">Se puede elegir entre Standard_Small, Standard_Medium y Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="1228e-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="1228e-183">Creación de una puerta de enlace de aplicaciones con New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="1228e-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="1228e-184">Cree una puerta de enlace de aplicaciones con todos los elementos de configuración de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="1228e-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="1228e-185">En el ejemplo, la puerta de enlace de aplicaciones se denomina "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="1228e-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="1228e-186">Este paso crea una puerta de enlace de aplicaciones con todos los elementos de configuración de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="1228e-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="1228e-187">En el ejemplo, la Puerta de enlace de aplicaciones se denomina "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="1228e-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="1228e-188">Eliminación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1228e-188">Delete an application gateway</span></span>

<span data-ttu-id="1228e-189">Para eliminar una puerta de enlace de aplicaciones, deberá realizar los pasos siguientes en orden:</span><span class="sxs-lookup"><span data-stu-id="1228e-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="1228e-190">Use el cmdlet `Stop-AzureRmApplicationGateway` para detener la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1228e-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="1228e-191">Utilice el cmdlet `Remove-AzureRmApplicationGateway` para quitar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1228e-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="1228e-192">Compruebe que se quitó la puerta de enlace con el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="1228e-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="1228e-193">Paso 1</span><span class="sxs-lookup"><span data-stu-id="1228e-193">Step 1</span></span>

<span data-ttu-id="1228e-194">Obtenga el objeto de puerta de enlace de aplicaciones y asócielo a una variable "$getgw".</span><span class="sxs-lookup"><span data-stu-id="1228e-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="1228e-195">Paso 2</span><span class="sxs-lookup"><span data-stu-id="1228e-195">Step 2</span></span>

<span data-ttu-id="1228e-196">Use `Stop-AzureRmApplicationGateway` para detener la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1228e-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="1228e-197">Este ejemplo muestra el cmdlet `Stop-AzureRmApplicationGateway` en la primera línea, seguido de la salida.</span><span class="sxs-lookup"><span data-stu-id="1228e-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="1228e-198">Cuando el estado de la puerta de enlace de aplicaciones sea detenido, use el cmdlet `Remove-AzureRmApplicationGateway` para quitar el servicio.</span><span class="sxs-lookup"><span data-stu-id="1228e-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="1228e-199">Se puede usar el modificador **-force** para suprimir el mensaje de confirmación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="1228e-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="1228e-200">Para comprobar que se ha quitado el servicio, puede usar el cmdlet `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="1228e-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="1228e-201">Este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="1228e-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="1228e-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1228e-202">Next steps</span></span>

<span data-ttu-id="1228e-203">Si desea configurar la descarga de SSL, consulte [Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante el modelo de implementación clásica](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="1228e-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="1228e-204">Si desea configurar una puerta de enlace de aplicaciones para usarla con un ILB, consulte [Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="1228e-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="1228e-205">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="1228e-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="1228e-206">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="1228e-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="1228e-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="1228e-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

