---
title: "Configuración de la descarga de SSL para Azure Application Gateway mediante PowerShell | Microsoft Docs"
description: "En esta página se ofrecen instrucciones para crear una puerta de enlace de aplicaciones con descarga SSL mediante Azure Resource Manager"
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
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="4b086-103">Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b086-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b086-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4b086-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="4b086-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b086-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="4b086-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b086-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="4b086-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4b086-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="4b086-108">Azure Application Gateway puede configurarse para terminar la sesión Capa de sockets seguros (SSL) en la puerta de enlace para evitar las costosas tareas de descifrado SSL que tienen lugar en la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="4b086-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="4b086-109">La descarga SSL también simplifica la configuración del servidor front-end y la administración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4b086-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4b086-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4b086-110">Before you begin</span></span>

1. <span data-ttu-id="4b086-111">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="4b086-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="4b086-112">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la [página Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4b086-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4b086-113">Cree una red virtual y una subred para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="4b086-114">Asegúrese de que ninguna máquina virtual o implementación en la nube usan la subred.</span><span class="sxs-lookup"><span data-stu-id="4b086-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="4b086-115">La puerta de enlace de aplicaciones debe encontrarse en una subred de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="4b086-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="4b086-116">Los servidores que configure para que usen la Puerta de enlace de aplicaciones deben existir, o bien sus puntos de conexión deben haberse creado en la red virtual o tener una dirección IP/VIP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="4b086-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="4b086-117">¿Qué se necesita para crear una Puerta de enlace de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="4b086-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="4b086-118">**Grupo de servidores back-end:** lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="4b086-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4b086-119">Las direcciones IP que se enumeran deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="4b086-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4b086-120">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="4b086-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4b086-121">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="4b086-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4b086-122">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4b086-123">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="4b086-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4b086-124">**Agente de escucha:** tiene un puerto front-end, un protocolo (Http o Https, que distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="4b086-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4b086-125">**Regla:** enlaza el agente de escucha y el grupo de servidores back-end y define a qué grupo de servidores back-end se dirigirá el tráfico cuando llega a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="4b086-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="4b086-126">Actualmente, solo se admite la regla *básica* .</span><span class="sxs-lookup"><span data-stu-id="4b086-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="4b086-127">La regla *básica* es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="4b086-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="4b086-128">**Notas de configuración adicionales**</span><span class="sxs-lookup"><span data-stu-id="4b086-128">**Additional configuration notes**</span></span>

<span data-ttu-id="4b086-129">Para la configuración de certificados SSL, el protocolo de **HttpListener** debería cambiar a *Https* (con distinción entre mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="4b086-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="4b086-130">El elemento **SslCertificate** se agrega a **HttpListener** con el valor de la variable configurado para el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="4b086-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="4b086-131">El puerto front-end debe actualizarse al 443.</span><span class="sxs-lookup"><span data-stu-id="4b086-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="4b086-132">**Para habilitar la afinidad basada en cookies**: se puede configurar una puerta de enlace de aplicaciones para asegurarse de que las solicitudes de una sesión de cliente siempre se dirigen a la misma máquina virtual de la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="4b086-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="4b086-133">Este escenario se realiza mediante la inyección de una cookie de la sesión que permita a la puerta de enlace dirigir el tráfico de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="4b086-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="4b086-134">Para habilitar la afinidad basada en cookies, establezca **CookieBasedAffinity** en *Habilitado* en el elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="4b086-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="4b086-135">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-135">Create an application gateway</span></span>

<span data-ttu-id="4b086-136">La diferencia entre el uso del modelo de implementación clásica de Azure y el de Azure Resource Manager es el orden en que se crea una puerta de enlace de aplicaciones y los elementos que es preciso configurar.</span><span class="sxs-lookup"><span data-stu-id="4b086-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="4b086-137">Con Resource Manager, todos los componentes de una puerta de enlace de aplicaciones se configuran individualmente y, luego, se unen para crear un recurso de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="4b086-138">Estos son los pasos necesarios para crear una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="4b086-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="4b086-139">Creación de un grupo de recursos para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b086-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="4b086-140">Creación de una red virtual, una subred y una IP pública para la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="4b086-141">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="4b086-142">Crear un recurso de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="4b086-143">Creación de un grupo de recursos para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b086-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="4b086-144">Asegúrese de cambiar el modo de PowerShell para que use los cmdlets de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4b086-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="4b086-145">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4b086-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="4b086-146">Paso 1</span><span class="sxs-lookup"><span data-stu-id="4b086-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="4b086-147">Paso 2</span><span class="sxs-lookup"><span data-stu-id="4b086-147">Step 2</span></span>

<span data-ttu-id="4b086-148">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="4b086-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="4b086-149">Se le solicita que se autentique con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="4b086-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="4b086-150">Paso 3</span><span class="sxs-lookup"><span data-stu-id="4b086-150">Step 3</span></span>

<span data-ttu-id="4b086-151">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="4b086-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="4b086-152">Paso 4</span><span class="sxs-lookup"><span data-stu-id="4b086-152">Step 4</span></span>

<span data-ttu-id="4b086-153">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="4b086-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="4b086-154">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="4b086-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4b086-155">Esta configuración se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4b086-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="4b086-156">Asegúrese de que todos los comandos para crear una puerta de enlace de aplicaciones usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4b086-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="4b086-157">En el ejemplo anterior, creamos un grupo de recursos denominado **appgw-RG** y la ubicación **Oeste de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="4b086-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="4b086-158">Creación de una red virtual y una subred para la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="4b086-159">En el ejemplo siguiente se muestra cómo crear una red virtual con Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4b086-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="4b086-160">Paso 1</span><span class="sxs-lookup"><span data-stu-id="4b086-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="4b086-161">En este ejemplo se asigna el intervalo de direcciones 10.0.0.0/24 a la variable de subred que se va a usar para crear una red virtual.</span><span class="sxs-lookup"><span data-stu-id="4b086-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="4b086-162">Paso 2</span><span class="sxs-lookup"><span data-stu-id="4b086-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="4b086-163">En este ejemplo se crea una red virtual denominada **appgwvnet** en el grupo de recursos **appgw-rg** para la región oeste de EE. UU. con el prefijo 10.0.0.0/16 y la subred 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="4b086-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="4b086-164">Paso 3</span><span class="sxs-lookup"><span data-stu-id="4b086-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="4b086-165">En este ejemplo se asigna el objeto de subred a la variable $subnet para los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="4b086-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="4b086-166">Creación de una dirección IP pública para la configuración del front-end</span><span class="sxs-lookup"><span data-stu-id="4b086-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="4b086-167">En este ejemplo se crea un recurso de IP público **publicIP01** en el grupo de recursos **appgw-rg** para la región oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="4b086-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="4b086-168">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="4b086-169">Paso 1</span><span class="sxs-lookup"><span data-stu-id="4b086-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="4b086-170">En este ejemplo se crea una configuración de la IP de la puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="4b086-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="4b086-171">Cuando se inicia la Puerta de enlace de aplicaciones, elige una dirección IP de la subred configurada y redirige el tráfico de red a las direcciones IP en el grupo IP de back-end.</span><span class="sxs-lookup"><span data-stu-id="4b086-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="4b086-172">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="4b086-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="4b086-173">Paso 2</span><span class="sxs-lookup"><span data-stu-id="4b086-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="4b086-174">En este ejemplo se configura el grupo de direcciones IP de back-end denominado **pool01** con las direcciones IP **134.170.185.46**, **134.170.188.221** y **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="4b086-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="4b086-175">Estos valores las direcciones IP que reciben el tráfico de red procedente del punto de conexión de la IP del front-nd.</span><span class="sxs-lookup"><span data-stu-id="4b086-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="4b086-176">Reemplace las direcciones IP del ejemplo anterior por las de los puntos de conexión de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4b086-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="4b086-177">Paso 3</span><span class="sxs-lookup"><span data-stu-id="4b086-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="4b086-178">En este ejemplo se configura la opción de la puerta de enlace de aplicaciones **poolsetting01** para el tráfico de red con carga equilibrada del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="4b086-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="4b086-179">Paso 4</span><span class="sxs-lookup"><span data-stu-id="4b086-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="4b086-180">En este ejemplo se configura el puerto IP del front-end denominado **frontendport01** para el punto de conexión de la IP pública.</span><span class="sxs-lookup"><span data-stu-id="4b086-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="4b086-181">Paso 5</span><span class="sxs-lookup"><span data-stu-id="4b086-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="4b086-182">En este ejemplo se configura el certificado que se usa para la conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="4b086-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="4b086-183">Es preciso que el certificado tenga el formato .pfx y que la contraseña tenga entre 4 y 12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4b086-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="4b086-184">Paso 6</span><span class="sxs-lookup"><span data-stu-id="4b086-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="4b086-185">En este ejemplo se crea la configuración de la IP de front-end denominada **fipconfig01** y asocia la dirección IP pública con dicha configuración.</span><span class="sxs-lookup"><span data-stu-id="4b086-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="4b086-186">Paso 7</span><span class="sxs-lookup"><span data-stu-id="4b086-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="4b086-187">En este ejemplo se crea el nombre de agente de escucha **listener01** y se asocia el puerto de front-end con la configuración de la IP del front-end y el certificado.</span><span class="sxs-lookup"><span data-stu-id="4b086-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="4b086-188">Paso 8</span><span class="sxs-lookup"><span data-stu-id="4b086-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="4b086-189">En este ejemplo se crea la regla de enrutamiento del equilibrador de carga denominada **rule01** que configura el comportamiento del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4b086-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="4b086-190">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="4b086-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="4b086-191">En este ejemplo se configura el tamaño de instancia de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="4b086-192">El valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="4b086-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="4b086-193">El valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="4b086-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="4b086-194">Se puede elegir entre Standard_Small, Standard_Medium y Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="4b086-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="4b086-195">Paso 10</span><span class="sxs-lookup"><span data-stu-id="4b086-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="4b086-196">Este paso permite definir la directiva SSL que se usará en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="4b086-197">Para más información, visite [Configuración de versiones de directivas SSL y conjuntos de cifrado en Application Gateway](application-gateway-configure-ssl-policy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4b086-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="4b086-198">Creación de una puerta de enlace de aplicaciones con New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="4b086-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="4b086-199">En este ejemplo se crea una puerta de enlace de aplicaciones con todos los elementos de configuración de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="4b086-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="4b086-200">En el ejemplo, la puerta de enlace de aplicaciones se denomina **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="4b086-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4b086-201">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b086-201">Get application gateway DNS name</span></span>

<span data-ttu-id="4b086-202">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="4b086-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4b086-203">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="4b086-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4b086-204">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="4b086-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="4b086-205">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4b086-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4b086-206">Para ello, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="4b086-207">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="4b086-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="4b086-208">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b086-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="4b086-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b086-209">Next steps</span></span>

<span data-ttu-id="4b086-210">Si desea configurar una puerta de enlace de aplicaciones para usarla con el equilibrador de carga interno (ILB), consulte [Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="4b086-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4b086-211">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="4b086-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4b086-212">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="4b086-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4b086-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4b086-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

