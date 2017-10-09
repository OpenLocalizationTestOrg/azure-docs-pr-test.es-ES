---
title: la descarga de SSL aaaConfigure - puerta de enlace de aplicaciones de Azure - PowerShell | Documentos de Microsoft
description: "Esta página proporciona toocreate instrucciones la descarga de una puerta de enlace de la aplicación con SSL con el Administrador de recursos de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="d8e09-103">Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8e09-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8e09-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d8e09-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="d8e09-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="d8e09-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="d8e09-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8e09-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="d8e09-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d8e09-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="d8e09-108">Puerta de enlace de aplicación de Azure puede ser configurado tooterminate Hola Secure Sockets Layer (SSL) sesión en hello puerta de enlace tooavoid costoso SSL descifrado tareas toohappen en la granja de servidores de hello web.</span><span class="sxs-lookup"><span data-stu-id="d8e09-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="d8e09-109">Descarga SSL también simplifica la administración de aplicación web de Hola y el programa de instalación del servidor front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d8e09-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d8e09-110">Before you begin</span></span>

1. <span data-ttu-id="d8e09-111">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="d8e09-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="d8e09-112">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d8e09-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d8e09-113">Crear una red virtual y una subred de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="d8e09-114">Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="d8e09-115">La puerta de enlace de aplicaciones debe encontrarse en una subred de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d8e09-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="d8e09-116">deben existir servidores Hola configurar puerta de enlace de aplicaciones de toouse Hola o han creado sus puntos de conexión de red virtual de Hola o con una dirección IP pública/VIP asignada.</span><span class="sxs-lookup"><span data-stu-id="d8e09-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="d8e09-117">¿Qué es necesario toocreate una puerta de enlace de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="d8e09-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="d8e09-118">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="d8e09-119">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="d8e09-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="d8e09-120">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="d8e09-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d8e09-121">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="d8e09-122">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="d8e09-123">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="d8e09-124">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="d8e09-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d8e09-125">**Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="d8e09-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="d8e09-126">Actualmente, solo Hola *básico* se admite la regla.</span><span class="sxs-lookup"><span data-stu-id="d8e09-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="d8e09-127">Hola *básica* regla es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="d8e09-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="d8e09-128">**Notas de configuración adicionales**</span><span class="sxs-lookup"><span data-stu-id="d8e09-128">**Additional configuration notes**</span></span>

<span data-ttu-id="d8e09-129">Para la configuración de certificados SSL, Hola protocolo en **HttpListener** debe cambiar también*Https* (con distinción entre mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="d8e09-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="d8e09-130">Hola **SslCertificate** elemento se agrega demasiado**HttpListener** con valor de la variable Hola configurado para el certificado SSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="d8e09-131">puerto front-end de Hello deben too443 actualizada.</span><span class="sxs-lookup"><span data-stu-id="d8e09-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="d8e09-132">**tooenable basado en cookies afinidad**: una puerta de enlace de la aplicación puede ser configurado tooensure que una solicitud de una sesión de cliente siempre está dirigido toohello misma máquina virtual en la granja de servidores de hello web.</span><span class="sxs-lookup"><span data-stu-id="d8e09-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="d8e09-133">Este escenario se realiza mediante la inyección de una cookie de sesión que permita el tráfico de toodirect de puerta de enlace de hello adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="d8e09-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="d8e09-134">establece la afinidad basado en cookies tooenable, **CookieBasedAffinity** demasiado*habilitado* en hello **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="d8e09-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="d8e09-135">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e09-135">Create an application gateway</span></span>

<span data-ttu-id="d8e09-136">diferencia de Hello entre utilizar el modelo de implementación de Azure clásico de Hola y el Administrador de recursos de Azure es orden de Hola que creas un elementos de hello y puerta de enlace de aplicaciones que requieren toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="d8e09-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="d8e09-137">Con el Administrador de recursos, todos los componentes de una puerta de enlace de aplicaciones se configuran individualmente y, a continuación, colocar junto toocreate un recurso de puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e09-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="d8e09-138">Estos es Hola pasos necesarios toocreate una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d8e09-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="d8e09-139">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="d8e09-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="d8e09-140">Crear red virtual, subred y dirección IP pública para puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d8e09-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="d8e09-141">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e09-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="d8e09-142">Crear un recurso de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e09-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="d8e09-143">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="d8e09-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="d8e09-144">Asegúrese de que cambia el modo toouse hello Azure Resource Manager cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8e09-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="d8e09-145">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d8e09-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="d8e09-146">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d8e09-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="d8e09-147">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d8e09-147">Step 2</span></span>

<span data-ttu-id="d8e09-148">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e09-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d8e09-149">Son tooauthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="d8e09-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="d8e09-150">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d8e09-150">Step 3</span></span>

<span data-ttu-id="d8e09-151">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e09-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="d8e09-152">Paso 4</span><span class="sxs-lookup"><span data-stu-id="d8e09-152">Step 4</span></span>

<span data-ttu-id="d8e09-153">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="d8e09-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="d8e09-154">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="d8e09-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d8e09-155">Esta configuración se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8e09-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d8e09-156">Asegúrese de que todos los toocreate de comandos utiliza una puerta de enlace de la aplicación Hola mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8e09-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="d8e09-157">En el ejemplo de Hola anterior, hemos creado un grupo de recursos denominado **appgw RG** y la ubicación **West US**.</span><span class="sxs-lookup"><span data-stu-id="d8e09-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="d8e09-158">Crear una red virtual y una subred de puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="d8e09-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="d8e09-159">Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="d8e09-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="d8e09-160">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d8e09-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="d8e09-161">Este ejemplo asigna Hola dirección intervalo 10.0.0.0/24 tooa subred toobe variable utiliza toocreate una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d8e09-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="d8e09-162">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d8e09-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="d8e09-163">Este ejemplo crea una red virtual denominada **appgwvnet** en grupo de recursos **appgw rg** de región de oeste de Estados Unidos de hello con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="d8e09-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="d8e09-164">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d8e09-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="d8e09-165">Este ejemplo asigna Hola subred objeto toovariable $subnet para obtener instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="d8e09-166">Crear una dirección IP pública para la configuración de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="d8e09-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="d8e09-167">Este ejemplo crea un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="d8e09-168">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e09-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="d8e09-169">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d8e09-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="d8e09-170">En este ejemplo se crea una configuración de la IP de la puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="d8e09-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="d8e09-171">Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="d8e09-172">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="d8e09-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="d8e09-173">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d8e09-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="d8e09-174">Este ejemplo configura el grupo de direcciones IP Hola back-end denominado **pool01** con direcciones IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="d8e09-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="d8e09-175">Esos valores son direcciones IP de Hola que reciben tráfico de red de Hola que provienen de extremo IP de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="d8e09-176">Reemplazar las direcciones IP Hola Hola anterior ejemplo con direcciones IP de Hola de los extremos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d8e09-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="d8e09-177">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d8e09-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="d8e09-178">Este ejemplo configura la configuración de puerta de enlace de aplicaciones **poolsetting01** tooload equilibrada de tráfico de red en el grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="d8e09-179">Paso 4</span><span class="sxs-lookup"><span data-stu-id="d8e09-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="d8e09-180">Este ejemplo configura el puerto IP front-end Hola denominado **frontendport01** para punto de conexión IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="d8e09-181">Paso 5</span><span class="sxs-lookup"><span data-stu-id="d8e09-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="d8e09-182">Este ejemplo configura el certificado de hello usado para la conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="d8e09-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="d8e09-183">certificado de Hello debe toobe en formato .pfx y Hola contraseña debe tener entre 4 too12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d8e09-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="d8e09-184">Paso 6</span><span class="sxs-lookup"><span data-stu-id="d8e09-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="d8e09-185">Este ejemplo crea la configuración de IP front-end de hello denominado **fipconfig01** y asocia Hola la dirección IP pública con la configuración de IP de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="d8e09-186">Paso 7</span><span class="sxs-lookup"><span data-stu-id="d8e09-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="d8e09-187">Este ejemplo crea el nombre de agente de escucha de hello **listener01** y asocia Hola configuración de IP de front-end de puerto front-end toohello y el certificado.</span><span class="sxs-lookup"><span data-stu-id="d8e09-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="d8e09-188">Paso 8</span><span class="sxs-lookup"><span data-stu-id="d8e09-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="d8e09-189">Este ejemplo crea Hola regla equilibrador de carga enrutamiento denominado **rule01** que configura el comportamiento de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="d8e09-190">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="d8e09-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="d8e09-191">Este ejemplo configura el tamaño de la instancia de puerta de enlace de aplicación Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="d8e09-192">Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="d8e09-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="d8e09-193">Hola valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="d8e09-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="d8e09-194">Se puede elegir entre Standard_Small, Standard_Medium y Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="d8e09-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="d8e09-195">Paso 10</span><span class="sxs-lookup"><span data-stu-id="d8e09-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="d8e09-196">Este paso define en puerta de enlace de aplicación Hola Hola SSL directiva toouse.</span><span class="sxs-lookup"><span data-stu-id="d8e09-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="d8e09-197">Visite [versiones de directivas de configurar SSL y conjuntos de cifrado en la puerta de enlace de aplicaciones](application-gateway-configure-ssl-policy-powershell.md) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="d8e09-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="d8e09-198">Creación de una puerta de enlace de aplicaciones con New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="d8e09-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="d8e09-199">Este ejemplo crea una puerta de enlace de la aplicación con todos los elementos de configuración de hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="d8e09-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="d8e09-200">En el ejemplo de Hola, se denomina puerta de enlace de aplicaciones de hello **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="d8e09-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d8e09-201">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e09-201">Get application gateway DNS name</span></span>

<span data-ttu-id="d8e09-202">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="d8e09-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="d8e09-203">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="d8e09-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d8e09-204">los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="d8e09-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="d8e09-205">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8e09-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="d8e09-206">toodo, detalles de recuperación de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e09-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="d8e09-207">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="d8e09-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="d8e09-208">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d8e09-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="d8e09-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8e09-209">Next steps</span></span>

<span data-ttu-id="d8e09-210">Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno (ILB), consulte [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="d8e09-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="d8e09-211">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="d8e09-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="d8e09-212">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="d8e09-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="d8e09-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d8e09-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

