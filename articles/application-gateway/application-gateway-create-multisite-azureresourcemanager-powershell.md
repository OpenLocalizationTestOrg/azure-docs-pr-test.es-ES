---
title: "una puerta de enlace de la aplicación para hospedar varios sitios aaaCreate | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones toocreate, configure una puerta de enlace de la aplicación de Azure para hospedar varias aplicaciones web en hello misma puerta de enlace."
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
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="7907e-103">Creación de una puerta de enlace de aplicaciones para hospedar varias aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="7907e-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7907e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7907e-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="7907e-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="7907e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="7907e-106">Alojamiento de varios sitios permite toodeploy más de una aplicación web en hello misma puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="7907e-107">Se basa en la presencia del encabezado de host en la solicitud HTTP entrante hello, toodetermine qué agente de escucha reciba tráfico.</span><span class="sxs-lookup"><span data-stu-id="7907e-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="7907e-108">agente de escucha de Hello, a continuación, dirige el grupo de back-end de tráfico tooappropriate como está configurado en la definición de las reglas de Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="7907e-109">En las aplicaciones web se ha habilitado SSL, puerta de enlace de aplicaciones se basa en hello indicación de nombre de servidor (SNI) extensión toochoose Hola correcto agente de escucha para el tráfico de web Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="7907e-110">Un uso común de alojamiento de varios sitios es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de dominios de web diferente.</span><span class="sxs-lookup"><span data-stu-id="7907e-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="7907e-111">De igual forma varios subdominios de hello también se puede hospedar el dominio raíz del mismo en Hola misma puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="7907e-112">Escenario</span><span class="sxs-lookup"><span data-stu-id="7907e-112">Scenario</span></span>

<span data-ttu-id="7907e-113">En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com y fabrikam.com con dos grupos de servidor back-end: contoso grupo de servidores y el grupo de servidores de fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7907e-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="7907e-114">El programa de instalación similar podría ser subdominios toohost usado como app.contoso.com y blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7907e-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="7907e-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7907e-116">Before you begin</span></span>

1. <span data-ttu-id="7907e-117">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="7907e-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="7907e-118">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7907e-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="7907e-119">se agregaron servidores de Hello debe existir la puerta de enlace de la aplicación de Hola de toohello grupo back-end toouse o han creado sus puntos de conexión en red virtual de hello en una subred independiente o con una dirección IP pública/VIP asignada.</span><span class="sxs-lookup"><span data-stu-id="7907e-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="7907e-120">Requisitos</span><span class="sxs-lookup"><span data-stu-id="7907e-120">Requirements</span></span>

* <span data-ttu-id="7907e-121">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="7907e-122">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="7907e-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="7907e-123">También puede utilizarse el FQDN.</span><span class="sxs-lookup"><span data-stu-id="7907e-123">FQDN can also be used.</span></span>
* <span data-ttu-id="7907e-124">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="7907e-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="7907e-125">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="7907e-126">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="7907e-127">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="7907e-128">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="7907e-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="7907e-129">En el caso de las puertas de enlace de aplicaciones con sitios múltiples habilitados, también se agregan el nombre de host y los indicadores de SNI.</span><span class="sxs-lookup"><span data-stu-id="7907e-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="7907e-130">**Regla:** regla Hola enlaza el agente de escucha de hello, grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="7907e-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="7907e-131">Las reglas se procesan en orden de hello aparecen y se dirigirá el tráfico a través de la regla primera Hola que coincida con independientemente de especificidad.</span><span class="sxs-lookup"><span data-stu-id="7907e-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="7907e-132">Por ejemplo, si tiene una regla mediante un agente de escucha básico y una regla mediante una escucha de varios sitio ambos en hello misma regla de puerto, Hola con el agente de escucha de hello multisitio debe aparecer antes de la regla de hello con un agente de escucha básico de hello en orden para hello toofunction de regla de multisitio como se esperaba.</span><span class="sxs-lookup"><span data-stu-id="7907e-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="7907e-133">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7907e-133">Create an application gateway</span></span>

<span data-ttu-id="7907e-134">siguiente Hola es pasos de hello necesarios toocreate una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7907e-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="7907e-135">Cree un grupo de recursos para Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7907e-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="7907e-136">Crear una red virtual, subredes y dirección IP pública para puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="7907e-137">Cree un objeto de configuración de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7907e-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="7907e-138">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7907e-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="7907e-139">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="7907e-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="7907e-140">Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="7907e-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="7907e-141">En [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md), encontrará más información al respecto.</span><span class="sxs-lookup"><span data-stu-id="7907e-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="7907e-142">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7907e-142">Step 1</span></span>

<span data-ttu-id="7907e-143">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="7907e-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="7907e-144">Son tooauthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="7907e-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="7907e-145">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7907e-145">Step 2</span></span>

<span data-ttu-id="7907e-146">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="7907e-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="7907e-147">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7907e-147">Step 3</span></span>

<span data-ttu-id="7907e-148">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7907e-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="7907e-149">Paso 4</span><span class="sxs-lookup"><span data-stu-id="7907e-149">Step 4</span></span>

<span data-ttu-id="7907e-150">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="7907e-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="7907e-151">También puede crear etiquetas para un grupo de recursos de la puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="7907e-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="7907e-152">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7907e-153">Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7907e-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="7907e-154">Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7907e-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="7907e-155">En el ejemplo de Hola anterior, hemos creado un grupo de recursos denominado **appgw RG** con una ubicación de **West US**.</span><span class="sxs-lookup"><span data-stu-id="7907e-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="7907e-156">Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7907e-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="7907e-157">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7907e-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="7907e-158">Creación una red virtual y subredes</span><span class="sxs-lookup"><span data-stu-id="7907e-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="7907e-159">Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="7907e-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="7907e-160">En este paso, se crean dos subredes.</span><span class="sxs-lookup"><span data-stu-id="7907e-160">Two subnets are created in this step.</span></span> <span data-ttu-id="7907e-161">primera subred de Hello es para la puerta de enlace de aplicaciones de hello propio.</span><span class="sxs-lookup"><span data-stu-id="7907e-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="7907e-162">Puerta de enlace de aplicaciones requiere su propio toohold subred sus instancias.</span><span class="sxs-lookup"><span data-stu-id="7907e-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="7907e-163">En dicha subred solo se pueden implementar otras puertas de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7907e-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="7907e-164">segunda subred de Hello es servidores de back-end de aplicación de hello toohold usado.</span><span class="sxs-lookup"><span data-stu-id="7907e-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="7907e-165">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7907e-165">Step 1</span></span>

<span data-ttu-id="7907e-166">Asignar Hola dirección intervalo 10.0.0.0/24 toohello subred toobe variable toohold usado Hola aplicación puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7907e-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="7907e-167">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7907e-167">Step 2</span></span>

<span data-ttu-id="7907e-168">Asignar subred2 Hola dirección intervalo 10.0.1.0/24 toohello variable toobe utilizado para grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="7907e-169">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7907e-169">Step 3</span></span>

<span data-ttu-id="7907e-170">Crear una red virtual denominada **appgwvnet** en grupo de recursos **appgw rg** de región de hello oeste de Estados Unidos con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24 y 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="7907e-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="7907e-171">Paso 4</span><span class="sxs-lookup"><span data-stu-id="7907e-171">Step 4</span></span>

<span data-ttu-id="7907e-172">Asignar una variable de subred para los pasos siguientes de hello, que crea una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="7907e-173">Crear una dirección IP pública para la configuración de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="7907e-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="7907e-174">Crear un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="7907e-175">Una dirección IP se asigna la puerta de enlace de toohello aplicación cuando se inicia el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="7907e-176">Creación de una configuración de puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7907e-176">Create application gateway configuration</span></span>

<span data-ttu-id="7907e-177">Tener tooset seguridad de todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="7907e-178">Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="7907e-179">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7907e-179">Step 1</span></span>

<span data-ttu-id="7907e-180">Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="7907e-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="7907e-181">Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="7907e-182">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="7907e-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="7907e-183">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7907e-183">Step 2</span></span>

<span data-ttu-id="7907e-184">Configurar el grupo de direcciones IP Hola back-end denominado **pool01** y **pool2** con direcciones IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** para **pool1** y **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  para **pool2**.</span><span class="sxs-lookup"><span data-stu-id="7907e-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="7907e-185">En este ejemplo, hay dos grupos de back-end tooroute el tráfico de red basado en sitio solicitado Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="7907e-186">Un grupo recibe el tráfico del sitio "contoso.com" y otro lo recibe del sitio "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="7907e-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="7907e-187">Tener hello tooreplace anterior tooadd de direcciones IP a sus propios extremos de dirección IP de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="7907e-188">En lugar de las direcciones IP internas, también se pueden usar direcciones IP públicas, el nombre de dominio completo o la NIC de una máquina virtual para las instancias de back-end.</span><span class="sxs-lookup"><span data-stu-id="7907e-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="7907e-189">toospecify FQDN en lugar de direcciones IP en PowerShell, use "-BackendFQDNs" parámetro.</span><span class="sxs-lookup"><span data-stu-id="7907e-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="7907e-190">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7907e-190">Step 3</span></span>

<span data-ttu-id="7907e-191">Configuración de puerta de enlace de aplicaciones **poolsetting01** y **poolsetting02** para tráfico con equilibrio de carga de red de hello en grupo back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="7907e-192">En este ejemplo, se configura otro grupo back-end para grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="7907e-193">Cada grupo de back-end puede tener su propia configuración de grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="7907e-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="7907e-194">Paso 4</span><span class="sxs-lookup"><span data-stu-id="7907e-194">Step 4</span></span>

<span data-ttu-id="7907e-195">Configurar IP de front-end de hello con punto de conexión IP pública.</span><span class="sxs-lookup"><span data-stu-id="7907e-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="7907e-196">Paso 5</span><span class="sxs-lookup"><span data-stu-id="7907e-196">Step 5</span></span>

<span data-ttu-id="7907e-197">Configurar puerto front-end de Hola para una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="7907e-198">Paso 6</span><span class="sxs-lookup"><span data-stu-id="7907e-198">Step 6</span></span>

<span data-ttu-id="7907e-199">Configurar dos certificados SSL para los sitios Web de hello dos vamos toosupport en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7907e-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="7907e-200">Un certificado es para el tráfico de contoso.com y Hola otro es para el tráfico de fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="7907e-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="7907e-201">Deben ser certificados emitidos por una entidad de certificación para sus sitios web.</span><span class="sxs-lookup"><span data-stu-id="7907e-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="7907e-202">Los certificados autofirmados se admiten, pero no se recomiendan para el tráfico de producción.</span><span class="sxs-lookup"><span data-stu-id="7907e-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="7907e-203">Paso 7</span><span class="sxs-lookup"><span data-stu-id="7907e-203">Step 7</span></span>

<span data-ttu-id="7907e-204">Configurar dos agentes de escucha para los sitios web de dos hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7907e-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="7907e-205">Este paso configura los agentes de escucha de Hola por dirección IP, puerto y host pública utilizan tooreceive el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="7907e-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="7907e-206">Parámetro de nombre de host es necesario para la compatibilidad con múltiples sitios y debe ser el sitio de Web de conjunto toohello adecuado para qué Hola se recibe el tráfico.</span><span class="sxs-lookup"><span data-stu-id="7907e-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="7907e-207">Parámetro RequireServerNameIndication debe establecerse tootrue para sitios Web que necesita compatibilidad con SSL en un escenario de host múltiple.</span><span class="sxs-lookup"><span data-stu-id="7907e-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="7907e-208">Si se requiere compatibilidad con SSL, también necesitará toospecify Hola SSL certificado que se tráfico toosecure usado para esa aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7907e-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="7907e-209">combinación de Hola de FrontendIPConfiguration, FrontendPort y nombre de host debe ser tooa único agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="7907e-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="7907e-210">Cada agente de escucha puede admitir solo un certificado.</span><span class="sxs-lookup"><span data-stu-id="7907e-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="7907e-211">Paso 8</span><span class="sxs-lookup"><span data-stu-id="7907e-211">Step 8</span></span>

<span data-ttu-id="7907e-212">Crear dos reglas establecer para hello dos aplicaciones web en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7907e-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="7907e-213">Una regla une los agentes de escucha, los grupos de back-end y la configuración de http.</span><span class="sxs-lookup"><span data-stu-id="7907e-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="7907e-214">Este paso configura Hola aplicación puerta de enlace toouse básica regla de enrutamiento, uno para cada sitio Web.</span><span class="sxs-lookup"><span data-stu-id="7907e-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="7907e-215">Sitio Web de tooeach de tráfico recibe su agente de escucha configurado y, a continuación, se dirige tooits configurado grupo back-end, con propiedades de hello especificadas en hello BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="7907e-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="7907e-216">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="7907e-216">Step 9</span></span>

<span data-ttu-id="7907e-217">Configurar el número de Hola de instancias y el tamaño de la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="7907e-218">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7907e-218">Create application gateway</span></span>

<span data-ttu-id="7907e-219">Crear una puerta de enlace de la aplicación con todos los objetos de configuración de hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="7907e-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="7907e-220">Aprovisionamiento de puerta de enlace de aplicaciones es una operación larga y puede tardar algún tiempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7907e-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="7907e-221">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7907e-221">Get application gateway DNS name</span></span>

<span data-ttu-id="7907e-222">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="7907e-223">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="7907e-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="7907e-224">los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7907e-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="7907e-225">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7907e-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="7907e-226">toodo, detalles de recuperación de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="7907e-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="7907e-227">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="7907e-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="7907e-228">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7907e-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7907e-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7907e-229">Next steps</span></span>

<span data-ttu-id="7907e-230">Obtenga información acerca de cómo tooprotect sus sitios Web con [puerta de enlace de aplicaciones - servidor de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7907e-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

