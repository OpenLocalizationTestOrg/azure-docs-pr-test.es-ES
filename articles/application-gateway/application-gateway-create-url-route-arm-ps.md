---
title: "reglas de una puerta de enlace de la aplicación mediante el enrutamiento de direcciones URL de aaaCreate | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones toocreate, configure una puerta de enlace de la aplicación de Azure mediante las reglas de enrutamiento de direcciones URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="b1c9a-103">Creación de una puerta de enlace de aplicaciones mediante enrutamiento basado en rutas de acceso</span><span class="sxs-lookup"><span data-stu-id="b1c9a-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1c9a-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b1c9a-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="b1c9a-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1c9a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="b1c9a-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b1c9a-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="b1c9a-107">Enrutamiento basado en la ruta de acceso de direcciones URL permite tooassociate rutas basándose en la ruta de acceso de dirección URL de Hola de una solicitud Http.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="b1c9a-108">Comprueba si hay un grupo de back-end de ruta tooa configurado para URL de hello presentado en hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="b1c9a-109">A continuación, envía toohello de tráfico de red de hello definido grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="b1c9a-110">Un uso común de enrutamiento basado en la dirección URL es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de diferentes tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="b1c9a-111">Enrutamiento basado en dirección URL, presenta una puerta de enlace de tooapplication de tipo de regla nueva.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="b1c9a-112">Application Gateway tiene dos tipos de reglas: básicas y PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="b1c9a-113">Tipo de regla básica proporciona servicio round robin para hello back-end grupos al PathBasedRouting además de la distribución competitiva tooround, también tiene modelo de ruta de acceso de dirección URL de solicitud de hello en cuenta al elegir grupo back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="b1c9a-114">Escenario</span><span class="sxs-lookup"><span data-stu-id="b1c9a-114">Scenario</span></span>

<span data-ttu-id="b1c9a-115">En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com con dos grupos de servidor back-end: grupo de servidores de vídeo y el grupo de servidores de la imagen.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="b1c9a-116">Las solicitudes de http://contoso.com/image * se enrutan se enrutan y grupo de servidores de tooimage (pool1) http://contoso.com/video * toovideo grupo de servidores (pool2).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="b1c9a-117">Si ninguno de los patrones de ruta de acceso de hello coinciden, se selecciona un grupo de servidores de forma predeterminada (pool1).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![ruta de dirección URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="b1c9a-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b1c9a-119">Before you begin</span></span>

1. <span data-ttu-id="b1c9a-120">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="b1c9a-121">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="b1c9a-122">Tendrá que crear una red virtual y subred para Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="b1c9a-123">Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="b1c9a-124">puerta de enlace de aplicaciones de Hello debe ser por sí solo en una subred de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="b1c9a-125">se agregaron servidores de Hello debe existir la puerta de enlace de la aplicación de Hola de toohello grupo back-end toouse o han creado sus puntos de conexión de red virtual de Hola o con una dirección IP pública/VIP asignada.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="b1c9a-126">¿Qué es necesario toocreate una puerta de enlace de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="b1c9a-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="b1c9a-127">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="b1c9a-128">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="b1c9a-129">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="b1c9a-130">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="b1c9a-131">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="b1c9a-132">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="b1c9a-133">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="b1c9a-134">**Regla:** regla Hola enlaza el agente de escucha de hello, grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="b1c9a-135">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b1c9a-135">Create an application gateway</span></span>

<span data-ttu-id="b1c9a-136">diferencia de Hello entre el uso de Azure clásico y el Administrador de recursos de Azure es orden de hello en el que crear puerta de enlace de aplicaciones de Hola y elementos de Hola que necesitan toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="b1c9a-137">Con el Administrador de recursos, todos los elementos que conforman una puerta de enlace de aplicaciones se configuran individualmente y, a continuación, reunir toocreate de recursos de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="b1c9a-138">Estos son los pasos de Hola que son necesario toocreate una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="b1c9a-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="b1c9a-139">Cree un grupo de recursos para Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="b1c9a-140">Crear una red virtual, subred y dirección IP pública para puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="b1c9a-141">Cree un objeto de configuración de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="b1c9a-142">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="b1c9a-143">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="b1c9a-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="b1c9a-144">Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b1c9a-145">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="b1c9a-146">Paso 1</span><span class="sxs-lookup"><span data-stu-id="b1c9a-146">Step 1</span></span>

<span data-ttu-id="b1c9a-147">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="b1c9a-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b1c9a-148">Son tooauthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="b1c9a-149">Paso 2</span><span class="sxs-lookup"><span data-stu-id="b1c9a-149">Step 2</span></span>

<span data-ttu-id="b1c9a-150">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="b1c9a-151">Paso 3</span><span class="sxs-lookup"><span data-stu-id="b1c9a-151">Step 3</span></span>

<span data-ttu-id="b1c9a-152">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="b1c9a-153">Paso 4</span><span class="sxs-lookup"><span data-stu-id="b1c9a-153">Step 4</span></span>

<span data-ttu-id="b1c9a-154">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="b1c9a-155">También puede crear etiquetas para un grupo de recursos de la puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="b1c9a-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="b1c9a-156">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b1c9a-157">Este grupo de recursos se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="b1c9a-158">Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="b1c9a-159">En el ejemplo de Hola anterior, hemos creado un grupo de recursos denominado "appgw-RG" y la ubicación "West US".</span><span class="sxs-lookup"><span data-stu-id="b1c9a-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="b1c9a-160">Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="b1c9a-161">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="b1c9a-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="b1c9a-162">Crear una red virtual y una subred de puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="b1c9a-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="b1c9a-163">Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="b1c9a-164">Este ejemplo crea una red virtual para hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="b1c9a-165">Puerta de enlace de aplicaciones requiere su propia subred, por este motivo subred Hola creado para hello Application Gateway es menor que Hola espacio de direcciones de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="b1c9a-166">Esto permite que otros recursos, incluidos pero sin limitarse tooweb servidores toobe Hola misma configuración red virtual.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="b1c9a-167">Paso 1</span><span class="sxs-lookup"><span data-stu-id="b1c9a-167">Step 1</span></span>

<span data-ttu-id="b1c9a-168">Asignar Hola dirección intervalo 10.0.0.0/24 toohello subred toobe variable utiliza toocreate una red virtual.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="b1c9a-169">Esto crea el objeto de configuración de subred de Hola para puerta de enlace de aplicaciones, que se utiliza en el ejemplo siguiente se Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="b1c9a-170">Paso 2</span><span class="sxs-lookup"><span data-stu-id="b1c9a-170">Step 2</span></span>

<span data-ttu-id="b1c9a-171">Crear una red virtual denominada **appgwvnet** en grupo de recursos **appgw rg** de región de oeste de Estados Unidos de hello con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="b1c9a-172">Esto completa la configuración de Hola de hello red virtual con una sola subred para hello tooreside de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="b1c9a-173">Paso 3</span><span class="sxs-lookup"><span data-stu-id="b1c9a-173">Step 3</span></span>

<span data-ttu-id="b1c9a-174">Asignar pasos de variable de subred de Hola para hello, este argumento se pasa toohello `New-AzureRMApplicationGateway` cmdlet en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="b1c9a-175">Crear una dirección IP pública para la configuración de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="b1c9a-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="b1c9a-176">Crear un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="b1c9a-177">Puerta de enlace de aplicación puede usar una dirección IP pública, la dirección IP interna o ambas solicitudes tooreceive para equilibrar la carga.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="b1c9a-178">En este ejemplo, solo se usa una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-178">This example only uses a public IP address.</span></span> <span data-ttu-id="b1c9a-179">En el siguiente ejemplo de Hola, ningún nombre DNS está configurado para la creación de la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="b1c9a-180">Application Gateway no admite nombres DNS personalizados en direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="b1c9a-181">Si se requiere para el punto de conexión público Hola un nombre personalizado, se debe crear un registro CNAME toopoint toohello generada automáticamente nombre DNS para la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="b1c9a-182">Una dirección IP se asigna la puerta de enlace de toohello aplicación cuando se inicia el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="b1c9a-183">Creación de una configuración de puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b1c9a-183">Create application gateway configuration</span></span>

<span data-ttu-id="b1c9a-184">Todos los elementos de configuración deben estar configurados antes de crear la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="b1c9a-185">Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="b1c9a-186">Paso 1</span><span class="sxs-lookup"><span data-stu-id="b1c9a-186">Step 1</span></span>

<span data-ttu-id="b1c9a-187">Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="b1c9a-188">Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="b1c9a-189">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="b1c9a-190">Paso 2</span><span class="sxs-lookup"><span data-stu-id="b1c9a-190">Step 2</span></span>

<span data-ttu-id="b1c9a-191">Configurar el grupo de direcciones IP Hola back-end denominado **pool01** y **pool2** con direcciones IP para **pool1** y **pool2**.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="b1c9a-192">Estas direcciones IP son direcciones IP de Hola de recursos de Hola que hospedan toobe de aplicación web de hello protegido por la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="b1c9a-193">Estos miembros del grupo back-end son todos los toobe validado correcto por sondeos sean sondeos básicos o personalizados sondeos.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="b1c9a-194">A continuación, se enruta el tráfico toothem cuando las solicitudes procedan en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="b1c9a-195">Grupos back-end pueden utilizarse en varias reglas dentro de hello aplicación puerta de enlace, lo que significa un grupo back-end podría usarse para varias aplicaciones web que se encuentren en hello mismo host.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="b1c9a-196">En este ejemplo, hay dos grupos de back-end tooroute el tráfico de red en función de la ruta de acceso de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="b1c9a-197">Un grupo recibe el tráfico de la ruta de dirección URL "/video" y otro lo recibe de la ruta "/image".</span><span class="sxs-lookup"><span data-stu-id="b1c9a-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="b1c9a-198">Reemplace Hola anterior tooadd de direcciones IP a sus propios extremos de dirección IP de aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="b1c9a-199">Paso 3</span><span class="sxs-lookup"><span data-stu-id="b1c9a-199">Step 3</span></span>

<span data-ttu-id="b1c9a-200">Configuración de puerta de enlace de aplicaciones **poolsetting01** y **poolsetting02** para tráfico con equilibrio de carga de red de hello en grupo back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="b1c9a-201">En este ejemplo, se configura otro grupo back-end para grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="b1c9a-202">Cada grupo de back-end puede tener su propia configuración de grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="b1c9a-203">Configuración de HTTP de back-end se usa por miembros del grupo de reglas tooroute tráfico toohello correcta back-end.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="b1c9a-204">Esto determina el protocolo de Hola y el puerto que se usa al enviar tráfico toohello los miembros del grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="b1c9a-205">Configuración de HTTP de back-end de hello también dependen de las sesiones basado en cookies.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="b1c9a-206">Si está habilitada, la afinidad de sesión basado en cookies envía tráfico toohello mismo back-end como solicitudes anteriores para cada paquete.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="b1c9a-207">Paso 4</span><span class="sxs-lookup"><span data-stu-id="b1c9a-207">Step 4</span></span>

<span data-ttu-id="b1c9a-208">Configurar IP de front-end de hello con punto de conexión IP pública.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="b1c9a-209">objeto de configuración de IP de front-end de Hello usa un hello toorelate de agente de escucha exterior orientada hacia la dirección IP con el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="b1c9a-210">Paso 5</span><span class="sxs-lookup"><span data-stu-id="b1c9a-210">Step 5</span></span>

<span data-ttu-id="b1c9a-211">Configurar puerto front-end de Hola para una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="b1c9a-212">objeto de configuración de puerto front-end de Hello utiliza un agente de escucha toodefine qué puerto de escucha de puerta de enlace de aplicación hello para el tráfico en el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="b1c9a-213">Paso 6</span><span class="sxs-lookup"><span data-stu-id="b1c9a-213">Step 6</span></span>

<span data-ttu-id="b1c9a-214">Configurar el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-214">Configure hello listener.</span></span> <span data-ttu-id="b1c9a-215">Este paso configura el agente de escucha de hello para la dirección IP pública hello y utiliza el puerto tooreceive tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="b1c9a-216">Hola siguiente ejemplo toma la configuración de IP de front-end de hello configurado previamente, la configuración de puerto front-end y un protocolo (http o https) y configura el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="b1c9a-217">En este ejemplo, el agente de escucha de hello escucha tooHTTP tráfico en el puerto 80 en la dirección IP pública Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="b1c9a-218">Paso 7</span><span class="sxs-lookup"><span data-stu-id="b1c9a-218">Step 7</span></span>

<span data-ttu-id="b1c9a-219">Configurar rutas de acceso de regla de dirección URL para grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="b1c9a-220">Este paso configura Hola ruta de acceso relativa utilizado por la puerta de enlace de aplicaciones y define Hola asignación entre la ruta de acceso de dirección URL de Hola y Hola un grupo back-end se asigna el tráfico entrante de toohandle Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1c9a-221">Cada ruta de acceso debe comenzar con / hello solo lugar y un "\*" está permitida, está al final de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="b1c9a-222">Algunos ejemplos válidos son /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="b1c9a-223">Hello cadena fed buscador de coincidencias de ruta de acceso de toohello no incluye cualquier texto después de hello primero "?" o "#" y los caracteres no se permiten.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="b1c9a-224">Hello en el ejemplo siguiente se crea dos reglas: uno para el enrutamiento de ruta de acceso "/ imágenes /" tráfico tooback-end "pool1" y otra para "/ vídeo /" ruta de acceso de enrutamiento de tráfico tooback-end "pool2."</span><span class="sxs-lookup"><span data-stu-id="b1c9a-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="b1c9a-225">Estas reglas aseguran de que el tráfico para cada conjunto de direcciones URL es toohello enrutado back-end.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="b1c9a-226">Por ejemplo, http://contoso.com/image/figure1.jpg va toopool1 y http://contoso.com/video/example.mp4 va toopool2.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="b1c9a-227">Si la ruta de acceso de hello no coincide con ninguna de las reglas de ruta de acceso definida previamente hello, configuración del mapa de ruta de acceso de regla de hello también configura un grupo de direcciones de back-end de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="b1c9a-228">Por ejemplo, http://contoso.com/shoppingcart/test.html va toopool1 tal y como se define como grupo predeterminado de hello para el tráfico no coincidente.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="b1c9a-229">Paso 8</span><span class="sxs-lookup"><span data-stu-id="b1c9a-229">Step 8</span></span>

<span data-ttu-id="b1c9a-230">Creación de una configuración de regla</span><span class="sxs-lookup"><span data-stu-id="b1c9a-230">Create a rule setting.</span></span> <span data-ttu-id="b1c9a-231">Este paso configura el enrutamiento basado en la ruta de acceso de hello aplicación puerta de enlace toouse dirección URL.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="b1c9a-232">Hola `$urlPathMap` variable definida en hello paso anterior es ahora usa toocreate Hola ruta de acceso una regla de.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="b1c9a-233">En este paso, asociamos de regla de hello con un agente de escucha y la asignación de ruta de acceso de dirección url de hello creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="b1c9a-234">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="b1c9a-234">Step 9</span></span>

<span data-ttu-id="b1c9a-235">Configurar el número de Hola de instancias y el tamaño de la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="b1c9a-236">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b1c9a-236">Create Application Gateway</span></span>

<span data-ttu-id="b1c9a-237">Crear una puerta de enlace de la aplicación con todos los objetos de configuración de hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b1c9a-238">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b1c9a-238">Get application gateway DNS name</span></span>

<span data-ttu-id="b1c9a-239">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="b1c9a-240">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b1c9a-241">los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="b1c9a-242">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="b1c9a-243">front-end de tooconfigure Hola un registro CNAME de IP, recuperar los detalles de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="b1c9a-244">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="b1c9a-245">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b1c9a-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b1c9a-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1c9a-246">Next steps</span></span>

<span data-ttu-id="b1c9a-247">Si desea que toolearn la descarga de capa de Sockets seguros (SSL), consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b1c9a-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

