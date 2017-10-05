---
title: "Configuración de SSL de extremo a extremo con Azure Application Gateway | Microsoft Docs"
description: "En este artículo se describe cómo configurar SSL de extremo a extremo con Application Gateway mediante PowerShell para Azure Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="10e78-103">Configuración de SSL de extremo a extremo con Application Gateway mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="10e78-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="10e78-104">Información general</span><span class="sxs-lookup"><span data-stu-id="10e78-104">Overview</span></span>

<span data-ttu-id="10e78-105">Application Gateway admite el cifrado de extremo a extremo del tráfico.</span><span class="sxs-lookup"><span data-stu-id="10e78-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="10e78-106">Para ello, lo que hace es terminar la conexión SSL en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="10e78-107">La puerta de enlace aplica entonces las reglas de enrutamiento al tráfico, vuelve a cifrar el paquete y lo reenvía al back-end adecuado según las reglas de enrutamiento definidas.</span><span class="sxs-lookup"><span data-stu-id="10e78-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="10e78-108">Cualquier respuesta del servidor web pasa por el mismo proceso en su regreso al usuario final.</span><span class="sxs-lookup"><span data-stu-id="10e78-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="10e78-109">Otra característica que admite Application Gateway es la definición de opciones SSL personalizadas.</span><span class="sxs-lookup"><span data-stu-id="10e78-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="10e78-110">Application Gateway admite deshabilitar la siguiente versión de protocolo; **TLSv1.0**, **TLSv1.1**, y **TLSv1.2** así como definir qué conjuntos de cifrado usar y el orden de preferencia.</span><span class="sxs-lookup"><span data-stu-id="10e78-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="10e78-111">Para más información sobre las opciones configurables de SSL, visite la [introducción a la directiva SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10e78-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="10e78-112">SSL 2.0 y SSL 3.0 están deshabilitados de manera predeterminada y no se pueden habilitar.</span><span class="sxs-lookup"><span data-stu-id="10e78-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="10e78-113">Se considera que no son seguros y no se pueden usar con Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="10e78-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![imagen de escenario][scenario]

## <a name="scenario"></a><span data-ttu-id="10e78-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="10e78-115">Scenario</span></span>

<span data-ttu-id="10e78-116">En este escenario, aprenderá a crear una puerta de enlace de aplicaciones mediante SSL de extremo a extremo con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10e78-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="10e78-117">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="10e78-117">This scenario will:</span></span>

* <span data-ttu-id="10e78-118">Creará un grupo de recursos llamado **appgw-rg**.</span><span class="sxs-lookup"><span data-stu-id="10e78-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="10e78-119">Creará una red virtual denominada **appgwvnet** con un espacio de direcciones de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="10e78-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="10e78-120">Creará dos subredes llamadas **appgwsubnet** y **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="10e78-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="10e78-121">Creará una puerta de enlace de aplicaciones pequeña que admite el cifrado SSL de extremo a extremo que limita las versiones de protocolos SSL y los conjuntos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="10e78-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="10e78-122">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="10e78-122">Before you begin</span></span>

<span data-ttu-id="10e78-123">Para configurar SSL de extremo a extremo con una puerta de enlace de aplicaciones, hacen falta certificados para la puerta de enlace y los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="10e78-124">El certificado de la puerta de enlace se usa para cifrar y descifrar el tráfico que se le envía mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="10e78-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="10e78-125">El certificado de puerta de enlace debe estar en formato de Intercambio de información personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="10e78-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="10e78-126">Este formato de archivo permite la exportación de la clave privada, necesaria para que la puerta de enlace de aplicaciones realice el cifrado y descifrado del tráfico.</span><span class="sxs-lookup"><span data-stu-id="10e78-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="10e78-127">Para el cifrado SSL de extremo a extremo, el back-end debe estar en la lista de permitidos junto con la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="10e78-128">Para ello, se carga el certificado público de los back-ends en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="10e78-129">Así se garantiza que la puerta de enlace de aplicaciones solo se comunica con instancias de back-end conocidas,</span><span class="sxs-lookup"><span data-stu-id="10e78-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="10e78-130">lo que protege aún más la comunicación de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="10e78-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="10e78-131">Este proceso se describe en los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="10e78-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="10e78-132">Crear el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="10e78-132">Create the Resource Group</span></span>

<span data-ttu-id="10e78-133">Esta sección le lleva por la creación de un grupo de recursos que contiene la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="10e78-134">Paso 1</span><span class="sxs-lookup"><span data-stu-id="10e78-134">Step 1</span></span>

<span data-ttu-id="10e78-135">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="10e78-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="10e78-136">Paso 2</span><span class="sxs-lookup"><span data-stu-id="10e78-136">Step 2</span></span>

<span data-ttu-id="10e78-137">Seleccione la suscripción que se usará en este escenario.</span><span class="sxs-lookup"><span data-stu-id="10e78-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="10e78-138">Paso 3</span><span class="sxs-lookup"><span data-stu-id="10e78-138">Step 3</span></span>

<span data-ttu-id="10e78-139">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="10e78-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="10e78-140">Creación de una red virtual y una subred para la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="10e78-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="10e78-141">En el ejemplo siguiente se crea una red virtual y dos subredes.</span><span class="sxs-lookup"><span data-stu-id="10e78-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="10e78-142">Una subred se usa para alojar la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="10e78-143">La otra se usa para los back-ends que hospedan la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="10e78-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="10e78-144">Paso 1</span><span class="sxs-lookup"><span data-stu-id="10e78-144">Step 1</span></span>

<span data-ttu-id="10e78-145">Asigne un intervalo de direcciones para la subred de la puerta de enlace de aplicaciones propiamente dicha.</span><span class="sxs-lookup"><span data-stu-id="10e78-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="10e78-146">Las subredes configuradas para la puerta de enlace de aplicaciones deben tener el tamaño correcto.</span><span class="sxs-lookup"><span data-stu-id="10e78-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="10e78-147">Las puertas de enlace de aplicaciones se puede configurar para un máximo de diez instancias.</span><span class="sxs-lookup"><span data-stu-id="10e78-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="10e78-148">Cada instancia toma una dirección IP de la subred.</span><span class="sxs-lookup"><span data-stu-id="10e78-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="10e78-149">Una subred demasiado pequeña puede afectar negativamente el escalado horizontal de una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="10e78-150">Paso 2</span><span class="sxs-lookup"><span data-stu-id="10e78-150">Step 2</span></span>

<span data-ttu-id="10e78-151">Asigne un intervalo de direcciones para el grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="10e78-152">Paso 3</span><span class="sxs-lookup"><span data-stu-id="10e78-152">Step 3</span></span>

<span data-ttu-id="10e78-153">Cree una red virtual con las subredes definidas en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="10e78-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="10e78-154">Paso 4</span><span class="sxs-lookup"><span data-stu-id="10e78-154">Step 4</span></span>

<span data-ttu-id="10e78-155">Recupere el recurso de red virtual y los recursos de subred que se usarán en los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="10e78-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="10e78-156">Creación de una dirección IP pública para la configuración del front-end</span><span class="sxs-lookup"><span data-stu-id="10e78-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="10e78-157">Cree un recurso de IP pública para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="10e78-158">Esta dirección IP pública se usa en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="10e78-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="10e78-159">Application Gateway no admite el uso de una dirección IP pública creada con una etiqueta de dominio definida.</span><span class="sxs-lookup"><span data-stu-id="10e78-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="10e78-160">Solo se admite una dirección IP pública con una etiqueta de dominio creada dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="10e78-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="10e78-161">Si necesita un nombre DNS descriptivo para la puerta de enlace de aplicaciones, se recomienda usar un registro CNAME como alias.</span><span class="sxs-lookup"><span data-stu-id="10e78-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="10e78-162">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="10e78-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="10e78-163">Se deben establecer todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="10e78-164">En los pasos siguientes, se crean los elementos de configuración necesarios para un recurso de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="10e78-165">Paso 1</span><span class="sxs-lookup"><span data-stu-id="10e78-165">Step 1</span></span>

<span data-ttu-id="10e78-166">Cree una configuración de IP de puerta de enlace de aplicaciones. Esta configuración determina la subred que usará Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="10e78-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="10e78-167">Cuando se inicia Application Gateway, elige una dirección IP de la subred configurada y redirige el tráfico de red a las direcciones IP en el grupo IP de back-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="10e78-168">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="10e78-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="10e78-169">Paso 2</span><span class="sxs-lookup"><span data-stu-id="10e78-169">Step 2</span></span>

<span data-ttu-id="10e78-170">Cree una configuración IP de front-end. Esta configuración asigna una dirección IP pública o privada al front-end de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="10e78-171">El paso siguiente asocia la dirección IP pública del paso anterior con la configuración IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="10e78-172">Paso 3</span><span class="sxs-lookup"><span data-stu-id="10e78-172">Step 3</span></span>

<span data-ttu-id="10e78-173">Configure el grupo de direcciones IP de back-end con las direcciones IP de los servidores web de back-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="10e78-174">Estas direcciones IP son las direcciones que reciben el tráfico de red procedente del punto de conexión de la IP del front-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="10e78-175">Reemplazará las siguientes direcciones IP para agregar sus propios puntos de conexión de dirección IP de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="10e78-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="10e78-176">Un nombre de dominio completo (FQDN) es también un valor válido, en lugar de una dirección IP, para los servidores back-end mediante el modificador -BackendFqdns.</span><span class="sxs-lookup"><span data-stu-id="10e78-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="10e78-177">Paso 4</span><span class="sxs-lookup"><span data-stu-id="10e78-177">Step 4</span></span>

<span data-ttu-id="10e78-178">Configure el puerto IP de front-end para el punto de conexión de IP pública.</span><span class="sxs-lookup"><span data-stu-id="10e78-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="10e78-179">Este puerto es el puerto al que se conectan los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="10e78-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="10e78-180">Paso 5</span><span class="sxs-lookup"><span data-stu-id="10e78-180">Step 5</span></span>

<span data-ttu-id="10e78-181">Configure el certificado de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="10e78-182">Este certificado se usa para descifrar y volver a cifrar el tráfico de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="10e78-183">En este ejemplo se configura el certificado que se usa para la conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="10e78-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="10e78-184">Es preciso que el certificado tenga el formato .pfx y que la contraseña tenga entre 4 y 12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="10e78-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="10e78-185">Paso 6</span><span class="sxs-lookup"><span data-stu-id="10e78-185">Step 6</span></span>

<span data-ttu-id="10e78-186">Cree el agente de escucha HTTP para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="10e78-187">Asigne la configuración IP de front-end, el puerto y el certificado SSL que se usarán.</span><span class="sxs-lookup"><span data-stu-id="10e78-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="10e78-188">Paso 7</span><span class="sxs-lookup"><span data-stu-id="10e78-188">Step 7</span></span>

<span data-ttu-id="10e78-189">Cargue el certificado que se usará en los recursos del grupo de back-end habilitado para SSL.</span><span class="sxs-lookup"><span data-stu-id="10e78-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="10e78-190">El sondeo predeterminado obtiene la clave pública del enlace SSL **predeterminado** en la dirección IP del back-end y compara el valor de la clave pública que recibe con el valor de la clave pública que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="10e78-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="10e78-191">Es posible que la clave pública recuperada no sea necesariamente el sitio previsto al que el tráfico fluirá **si** se usan encabezados de host y SNI en el back-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="10e78-192">En caso de duda, visite https://127.0.0.1/ en los back-ends para confirmar qué certificado se usa para el enlace SSL **predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="10e78-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="10e78-193">Utilice la clave pública de dicha solicitud en esta sección.</span><span class="sxs-lookup"><span data-stu-id="10e78-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="10e78-194">Si usa encabezados de host y SNI en enlaces HTTPS y no recibe una respuesta y un certificado de una solicitud manual de un explorador a https://127.0.0.1/ en los back-ends, debe configurar un enlace SSL de forma predeterminada en los back-ends.</span><span class="sxs-lookup"><span data-stu-id="10e78-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="10e78-195">Si no lo hace, se producirán errores en los sondeos y el back-end no estará en la lista de permitidos.</span><span class="sxs-lookup"><span data-stu-id="10e78-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="10e78-196">El certificado proporcionado en este paso debe ser la clave pública del certificado pfx presente en el back-end.</span><span class="sxs-lookup"><span data-stu-id="10e78-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="10e78-197">Exporte el certificado (no el certificado raíz) instalado en el servidor backend en formato .CER y utilícelo en este paso.</span><span class="sxs-lookup"><span data-stu-id="10e78-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="10e78-198">En este paso se coloca el back-end en la lista de permitidos con la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="10e78-199">Paso 8</span><span class="sxs-lookup"><span data-stu-id="10e78-199">Step 8</span></span>

<span data-ttu-id="10e78-200">Configure los valores HTTP de back-end de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="10e78-201">Asigne el certificado cargado en el paso anterior a la configuración HTTP.</span><span class="sxs-lookup"><span data-stu-id="10e78-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="10e78-202">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="10e78-202">Step 9</span></span>

<span data-ttu-id="10e78-203">Cree una regla de enrutamiento del equilibrador de carga que configure el comportamiento del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="10e78-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="10e78-204">En este ejemplo, se crea una regla básica de operaciones por turnos.</span><span class="sxs-lookup"><span data-stu-id="10e78-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="10e78-205">Paso 10</span><span class="sxs-lookup"><span data-stu-id="10e78-205">Step 10</span></span>

<span data-ttu-id="10e78-206">Configure el tamaño de la instancia de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="10e78-207">Los tamaños disponibles son **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="10e78-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="10e78-208">Para la capacidad, los valores disponibles son de 1 a 10.</span><span class="sxs-lookup"><span data-stu-id="10e78-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="10e78-209">Para las pruebas se puede elegir 1 en Número de instancias.</span><span class="sxs-lookup"><span data-stu-id="10e78-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="10e78-210">Es importante saber que el SLA no cubre ningún número de instancias que esté por debajo de las dos instancias y, por consiguiente, no se recomienda.</span><span class="sxs-lookup"><span data-stu-id="10e78-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="10e78-211">Las puertas de enlace pequeñas se deben usar para pruebas de desarrollo, no con fines de producción.</span><span class="sxs-lookup"><span data-stu-id="10e78-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="10e78-212">Paso 11</span><span class="sxs-lookup"><span data-stu-id="10e78-212">Step 11</span></span>

<span data-ttu-id="10e78-213">Configure la directiva SSL que se usará en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="10e78-214">Application Gateway admite la posibilidad de establecer una versión mínima para las versiones del protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="10e78-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="10e78-215">Los valores siguientes son una lista de versiones de protocolo que se pueden definir.</span><span class="sxs-lookup"><span data-stu-id="10e78-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="10e78-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="10e78-216">**TLSv1_0**</span></span>
* <span data-ttu-id="10e78-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="10e78-217">**TLSv1_1**</span></span>
* <span data-ttu-id="10e78-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="10e78-218">**TLSv1_2**</span></span>

<span data-ttu-id="10e78-219">Establece la versión mínima del protocolo en **TLSv1_2** y solo habilita **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** y solo **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**.</span><span class="sxs-lookup"><span data-stu-id="10e78-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="10e78-220">Creación de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="10e78-220">Create the Application Gateway</span></span>

<span data-ttu-id="10e78-221">Con todos los pasos anteriores, cree la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="10e78-222">La creación de la puerta de enlace de aplicaciones es un proceso de ejecución largo.</span><span class="sxs-lookup"><span data-stu-id="10e78-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="10e78-223">Límite de las versiones de protocolo SSL en una instancia de Application Gateway existente</span><span class="sxs-lookup"><span data-stu-id="10e78-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="10e78-224">Los pasos anteriores le llevan por la creación de una aplicación con SSL de extremo a extremo y la deshabilitación de determinadas versiones del protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="10e78-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="10e78-225">En el ejemplo siguiente se deshabilitan determinadas directivas SSL en una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="10e78-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="10e78-226">Paso 1</span><span class="sxs-lookup"><span data-stu-id="10e78-226">Step 1</span></span>

<span data-ttu-id="10e78-227">Recupere la puerta de enlace de aplicaciones que se actualizará.</span><span class="sxs-lookup"><span data-stu-id="10e78-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="10e78-228">Paso 2</span><span class="sxs-lookup"><span data-stu-id="10e78-228">Step 2</span></span>

<span data-ttu-id="10e78-229">Defina una directiva SSL.</span><span class="sxs-lookup"><span data-stu-id="10e78-229">Define an SSL policy.</span></span> <span data-ttu-id="10e78-230">En el ejemplo siguiente, se deshabilitan TLSv1.0 y TLSv1.1 y los conjuntos de cifrado **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** y **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** son los únicos permitidos.</span><span class="sxs-lookup"><span data-stu-id="10e78-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="10e78-231">Paso 3</span><span class="sxs-lookup"><span data-stu-id="10e78-231">Step 3</span></span>

<span data-ttu-id="10e78-232">Por último, actualice la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="10e78-232">Finally, update the gateway.</span></span> <span data-ttu-id="10e78-233">Es importante tener en cuenta que este último paso es una tarea de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="10e78-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="10e78-234">Una vez terminado, SSL de extremo a extremo está configurado en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="10e78-235">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="10e78-235">Get application gateway DNS name</span></span>

<span data-ttu-id="10e78-236">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="10e78-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="10e78-237">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="10e78-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="10e78-238">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="10e78-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="10e78-239">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="10e78-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="10e78-240">Para ello, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="10e78-241">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="10e78-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="10e78-242">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10e78-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="10e78-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10e78-243">Next steps</span></span>

<span data-ttu-id="10e78-244">Aprenda sobre la protección de la seguridad de las aplicaciones web con el firewall de aplicaciones web mediante Application Gateway en [Información general sobre el firewall de aplicaciones web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="10e78-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
