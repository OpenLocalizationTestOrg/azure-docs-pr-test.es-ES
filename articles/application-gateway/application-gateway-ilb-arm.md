---
title: puerta de enlace de aplicaciones de Azure con el equilibrador de carga interno - PowerShell aaaUsing | Documentos de Microsoft
description: "Esta página proporciona instrucciones toocreate, configurar, iniciar y eliminar una puerta de enlace de la aplicación de Azure con el equilibrador de carga interno (ILB) para el Administrador de recursos de Azure"
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
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="d1b92-103">Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB) mediante el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b92-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1b92-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1b92-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="d1b92-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b92-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="d1b92-106">Puerta de enlace de aplicación de Azure puede configurarse con una VIP accesible desde Internet o con un extremo interno que no está expuesta toohello Internet, también conocido como un punto de conexión de (ILB) de equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="d1b92-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="d1b92-107">Configurar puerta de enlace de hello con un ILB es útil para aplicaciones de línea de negocio internas que no están expuesta toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="d1b92-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="d1b92-108">También es útil para los servicios y niveles dentro de una aplicación de varios nivel que se colocan en un límite de seguridad que no está expuesta toohello Internet pero que aún requieren round robin cargar distribución, adherencia de sesión o de finalización de la capa de Sockets seguros (SSL).</span><span class="sxs-lookup"><span data-stu-id="d1b92-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="d1b92-109">Este artículo le guiará a través de hello pasos tooconfigure una puerta de enlace de la aplicación con un ILB.</span><span class="sxs-lookup"><span data-stu-id="d1b92-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d1b92-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d1b92-110">Before you begin</span></span>

1. <span data-ttu-id="d1b92-111">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="d1b92-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="d1b92-112">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d1b92-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d1b92-113">Tendrá que crear una red virtual y una subred para Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d1b92-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="d1b92-114">Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="d1b92-115">La puerta de enlace de aplicaciones debe encontrarse en una subred de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d1b92-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="d1b92-116">deben existir servidores Hola configurar la puerta de enlace de aplicaciones de toouse Hola o tener asignados de sus puntos de conexión creados en la red virtual de Hola o con una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="d1b92-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="d1b92-117">¿Qué es necesario toocreate una puerta de enlace de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="d1b92-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="d1b92-118">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="d1b92-119">Hello direcciones IP mostradas deben o bien pertenecer toohello de red virtual, pero en una subred diferente para la puerta de enlace de aplicaciones de Hola o debe ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="d1b92-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="d1b92-120">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="d1b92-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d1b92-121">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="d1b92-122">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="d1b92-123">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="d1b92-124">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="d1b92-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d1b92-125">**Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="d1b92-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="d1b92-126">Actualmente, solo Hola *básico* se admite la regla.</span><span class="sxs-lookup"><span data-stu-id="d1b92-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="d1b92-127">Hola *básica* regla es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="d1b92-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="d1b92-128">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d1b92-128">Create an application gateway</span></span>

<span data-ttu-id="d1b92-129">diferencia de Hello entre el uso de Azure clásico y el Administrador de recursos de Azure es orden de hello en el que crear puerta de enlace de aplicaciones de Hola y elementos de Hola que necesitan toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="d1b92-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="d1b92-130">Con el Administrador de recursos, todos los elementos que conforman una puerta de enlace de la aplicación se configura individualmente y, a continuación, reunir toocreate de recursos de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="d1b92-131">Estos son los pasos de Hola que son necesario toocreate una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d1b92-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="d1b92-132">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="d1b92-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="d1b92-133">Crear una red virtual y una subred de puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d1b92-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="d1b92-134">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d1b92-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="d1b92-135">Crear un recurso de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d1b92-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="d1b92-136">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="d1b92-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="d1b92-137">Asegúrese de que cambia el modo toouse hello Azure Resource Manager cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1b92-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="d1b92-138">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d1b92-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="d1b92-139">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d1b92-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="d1b92-140">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d1b92-140">Step 2</span></span>

<span data-ttu-id="d1b92-141">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="d1b92-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d1b92-142">Son tooauthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="d1b92-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="d1b92-143">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d1b92-143">Step 3</span></span>

<span data-ttu-id="d1b92-144">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b92-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="d1b92-145">Paso 4</span><span class="sxs-lookup"><span data-stu-id="d1b92-145">Step 4</span></span>

<span data-ttu-id="d1b92-146">Cree un grupo de recursos nuevo (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="d1b92-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="d1b92-147">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="d1b92-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d1b92-148">Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1b92-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d1b92-149">Asegúrese de que todos los toocreate de comandos utiliza una puerta de enlace de la aplicación Hola mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1b92-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="d1b92-150">En el anterior ejemplo de Hola, hemos creado un grupo de recursos denominado "Appgw-rg" y la ubicación "West US".</span><span class="sxs-lookup"><span data-stu-id="d1b92-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="d1b92-151">Crear una red virtual y una subred de puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d1b92-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="d1b92-152">Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="d1b92-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="d1b92-153">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d1b92-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="d1b92-154">Este paso asigna Hola dirección intervalo 10.0.0.0/24 tooa subred toobe variable utiliza toocreate una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d1b92-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="d1b92-155">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d1b92-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="d1b92-156">Este paso crea una red virtual denominada "appgwvnet" en recurso grupo "appgw-rg" de región de oeste de Estados Unidos de hello con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="d1b92-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="d1b92-157">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d1b92-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="d1b92-158">Este paso asigna Hola subred objeto toovariable $subnet para obtener instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="d1b92-159">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d1b92-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="d1b92-160">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d1b92-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="d1b92-161">Este paso crea una configuración de la IP de la puerta de enlace de aplicaciones denominada "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="d1b92-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="d1b92-162">Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="d1b92-163">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="d1b92-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="d1b92-164">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d1b92-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="d1b92-165">Este paso configura el grupo de direcciones IP Hola back-end denominado "pool01" con la dirección IP se refiere a "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="d1b92-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="d1b92-166">Esos son direcciones IP de Hola que reciben tráfico de red de Hola que provienen de extremo IP de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="d1b92-167">Reemplace Hola anterior tooadd de direcciones IP de sus propios extremos de dirección IP de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1b92-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="d1b92-168">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d1b92-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="d1b92-169">Este paso configura el tráfico de red de puerta de enlace configuración "poolsetting01" para la carga de hello equilibrada de aplicación en el grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="d1b92-170">Paso 4</span><span class="sxs-lookup"><span data-stu-id="d1b92-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="d1b92-171">Este paso configura el puerto IP front-end Hola denominado "frontendport01" para hello ILB.</span><span class="sxs-lookup"><span data-stu-id="d1b92-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="d1b92-172">Paso 5</span><span class="sxs-lookup"><span data-stu-id="d1b92-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="d1b92-173">Este paso crea Hola la configuración de IP front-end denominada "fipconfig01" y lo asocia con una dirección de IP privada de la subred de red virtual de hello actual.</span><span class="sxs-lookup"><span data-stu-id="d1b92-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="d1b92-174">Paso 6</span><span class="sxs-lookup"><span data-stu-id="d1b92-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="d1b92-175">Este paso crea el agente de escucha de hello denominado "listener01" y asocia la configuración de IP front-end de hello puerto front-end toohello.</span><span class="sxs-lookup"><span data-stu-id="d1b92-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="d1b92-176">Paso 7</span><span class="sxs-lookup"><span data-stu-id="d1b92-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="d1b92-177">Este paso crea Hola regla equilibrador de carga enrutamiento denominado "rule01" que configura el comportamiento de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="d1b92-178">Paso 8</span><span class="sxs-lookup"><span data-stu-id="d1b92-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="d1b92-179">Este paso configura el tamaño de la instancia de puerta de enlace de aplicación Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="d1b92-180">Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="d1b92-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="d1b92-181">Hola valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="d1b92-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="d1b92-182">Se puede elegir entre Standard_Small, Standard_Medium y Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="d1b92-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="d1b92-183">Creación de una puerta de enlace de aplicaciones con New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="d1b92-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="d1b92-184">Crea una puerta de enlace de la aplicación con todos los elementos de configuración de hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="d1b92-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="d1b92-185">En este ejemplo, la puerta de enlace de aplicaciones de Hola se denomina "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="d1b92-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="d1b92-186">Este paso crea una puerta de enlace de la aplicación con todos los elementos de configuración de hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="d1b92-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="d1b92-187">En el ejemplo de Hola, puerta de enlace de aplicaciones de Hola se denomina "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="d1b92-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="d1b92-188">Eliminación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d1b92-188">Delete an application gateway</span></span>

<span data-ttu-id="d1b92-189">toodelete una puerta de enlace de la aplicación, necesita hello toodo siguiendo los pasos en orden:</span><span class="sxs-lookup"><span data-stu-id="d1b92-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="d1b92-190">Hola de uso `Stop-AzureRmApplicationGateway` puerta de enlace de cmdlet toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="d1b92-191">Hola de uso `Remove-AzureRmApplicationGateway` puerta de enlace de cmdlet tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="d1b92-192">Compruebe dicha puerta de enlace de Hola se ha eliminado mediante el uso de hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d1b92-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="d1b92-193">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d1b92-193">Step 1</span></span>

<span data-ttu-id="d1b92-194">Obtener el objeto de puerta de enlace de aplicación hello y asócielo variable tooa "$getgw".</span><span class="sxs-lookup"><span data-stu-id="d1b92-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="d1b92-195">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d1b92-195">Step 2</span></span>

<span data-ttu-id="d1b92-196">Use `Stop-AzureRmApplicationGateway` puerta de enlace de aplicaciones de toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="d1b92-197">Este ejemplo muestra hello `Stop-AzureRmApplicationGateway` cmdlet en la primera línea hello, seguido de la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="d1b92-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="d1b92-198">Una vez que la puerta de enlace de aplicaciones de hello está en estado detenido, use hello `Remove-AzureRmApplicationGateway` servicio de cmdlet tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b92-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

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
> <span data-ttu-id="d1b92-199">Hola **-forzar** conmutador puede ser el mensaje de confirmación de toosuppress usado Hola remove.</span><span class="sxs-lookup"><span data-stu-id="d1b92-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="d1b92-200">se ha quitado tooverify que Hola servicio, puede usar hello `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d1b92-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="d1b92-201">Este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="d1b92-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="d1b92-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1b92-202">Next steps</span></span>

<span data-ttu-id="d1b92-203">Si desea que tooconfigure la descarga de SSL, consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="d1b92-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="d1b92-204">Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un ILB, vea [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="d1b92-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="d1b92-205">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="d1b92-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="d1b92-206">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b92-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="d1b92-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d1b92-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

