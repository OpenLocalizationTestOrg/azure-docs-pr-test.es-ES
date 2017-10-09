---
title: aaaConfigure final tooend SSL con la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Este artículo describe cómo tooconfigure finalizar tooend SSL con la puerta de enlace de aplicaciones con el Administrador de recursos de Azure PowerShell"
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
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="2f927-103">Configurar final tooend SSL con la puerta de enlace de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f927-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="2f927-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2f927-104">Overview</span></span>

<span data-ttu-id="2f927-105">Admite aplicaciones de puerta de enlace finaliza tooend cifrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f927-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="2f927-106">Puerta de enlace de aplicación lo hace al terminar la conexión de SSL de hello en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="2f927-107">puerta de enlace de Hello, a continuación, aplica reglas de enrutamiento de hello toohello tráfico, vuelve a cifrar el paquete de saludo y reenvía Hola paquete toohello adecuado back-end basado en reglas de enrutamiento de hello definidas.</span><span class="sxs-lookup"><span data-stu-id="2f927-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="2f927-108">Las posibles respuestas del servidor web de hello atraviesa Hola mismo proceso de usuario de toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="2f927-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="2f927-109">Otra característica que admite Application Gateway es la definición de opciones SSL personalizadas.</span><span class="sxs-lookup"><span data-stu-id="2f927-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="2f927-110">Puerta de enlace de aplicaciones admite Hola deshabilitar después de la versión de protocolo; **TLSv1.0**, **TLSv1.1**, y **TLSv1.2** también definir hello que conjuntos toouse y Hola el orden de preferencia de cifrado.</span><span class="sxs-lookup"><span data-stu-id="2f927-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="2f927-111">toolearn más información acerca de opciones configurables de SSL, visite [Introducción a la directiva de SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f927-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2f927-112">SSL 2.0 y SSL 3.0 están deshabilitados de manera predeterminada y no se pueden habilitar.</span><span class="sxs-lookup"><span data-stu-id="2f927-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="2f927-113">Se consideran no seguras y no están toobe puede usar con la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2f927-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![imagen de escenario][scenario]

## <a name="scenario"></a><span data-ttu-id="2f927-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="2f927-115">Scenario</span></span>

<span data-ttu-id="2f927-116">En este escenario, aprenderá cómo toocreate una puerta de enlace de aplicaciones con finalizar tooend SSL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f927-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="2f927-117">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="2f927-117">This scenario will:</span></span>

* <span data-ttu-id="2f927-118">Creará un grupo de recursos llamado **appgw-rg**.</span><span class="sxs-lookup"><span data-stu-id="2f927-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="2f927-119">Creará una red virtual denominada **appgwvnet** con un espacio de direcciones de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="2f927-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="2f927-120">Creará dos subredes llamadas **appgwsubnet** y **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="2f927-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="2f927-121">Crear un pequeña aplicación puerta de enlace auxiliares final tooend cifrado SSL que las versiones de protocolos SSL de límites y los conjuntos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="2f927-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2f927-122">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2f927-122">Before you begin</span></span>

<span data-ttu-id="2f927-123">tooconfigure final tooend SSL con una puerta de enlace de la aplicación, un certificado es necesario para la puerta de enlace de Hola y se necesitan certificados para servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="2f927-124">certificado de puerta de enlace de Hello es usado tooencrypt y descifrar Hola el tráfico enviado tooit mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="2f927-125">certificado de puerta de enlace de Hello debe toobe en formato de intercambio de información Personal (pfx).</span><span class="sxs-lookup"><span data-stu-id="2f927-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="2f927-126">Este formato de archivo permite Hola privada toobe clave exportado que requiere Hola aplicación puerta de enlace tooperform Hola cifrado y descifrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f927-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="2f927-127">Para final tooend SSL cifrado Hola back-end debe ser la lista de permitidos con puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2f927-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="2f927-128">Para ello, cargar certificado público de Hola de puerta de enlace de hello back-ends toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f927-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="2f927-129">Esto garantiza que esa puerta de enlace de la aplicación hello sólo se comunica con instancias de conocidos back-end.</span><span class="sxs-lookup"><span data-stu-id="2f927-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="2f927-130">Esto protege aún más comunicación tooend de hello final.</span><span class="sxs-lookup"><span data-stu-id="2f927-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="2f927-131">Este proceso se describe en hello pasos:</span><span class="sxs-lookup"><span data-stu-id="2f927-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="2f927-132">Crear grupo de recursos de hello</span><span class="sxs-lookup"><span data-stu-id="2f927-132">Create hello Resource Group</span></span>

<span data-ttu-id="2f927-133">Esta sección explica cómo crear un grupo de recursos, que contiene la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="2f927-134">Paso 1</span><span class="sxs-lookup"><span data-stu-id="2f927-134">Step 1</span></span>

<span data-ttu-id="2f927-135">Inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f927-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="2f927-136">Paso 2</span><span class="sxs-lookup"><span data-stu-id="2f927-136">Step 2</span></span>

<span data-ttu-id="2f927-137">Seleccione hello toouse de suscripción para este escenario.</span><span class="sxs-lookup"><span data-stu-id="2f927-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="2f927-138">Paso 3</span><span class="sxs-lookup"><span data-stu-id="2f927-138">Step 3</span></span>

<span data-ttu-id="2f927-139">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="2f927-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="2f927-140">Crear una red virtual y una subred de puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="2f927-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="2f927-141">Hello en el ejemplo siguiente se crea una red virtual y dos subredes.</span><span class="sxs-lookup"><span data-stu-id="2f927-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="2f927-142">Una subred es la puerta de enlace de aplicaciones de uso toohold Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="2f927-143">Hola se usa otra subred para aplicación de web de hospedaje de back-ends de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="2f927-144">Paso 1</span><span class="sxs-lookup"><span data-stu-id="2f927-144">Step 1</span></span>

<span data-ttu-id="2f927-145">Asignar un intervalo de direcciones de subred de hello usará para hello aplicación puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f927-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="2f927-146">Las subredes configuradas para la puerta de enlace de aplicaciones deben tener el tamaño correcto.</span><span class="sxs-lookup"><span data-stu-id="2f927-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="2f927-147">Una puerta de enlace de aplicaciones puede configurarse para instancias de too10.</span><span class="sxs-lookup"><span data-stu-id="2f927-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="2f927-148">Cada instancia tiene una dirección IP de subred Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="2f927-149">Una subred demasiado pequeña puede afectar negativamente el escalado horizontal de una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2f927-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="2f927-150">Paso 2</span><span class="sxs-lookup"><span data-stu-id="2f927-150">Step 2</span></span>

<span data-ttu-id="2f927-151">Asignar un toobe de intervalo de direcciones utilizado para el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="2f927-152">Paso 3</span><span class="sxs-lookup"><span data-stu-id="2f927-152">Step 3</span></span>

<span data-ttu-id="2f927-153">Crear una red virtual con subredes Hola definidos en hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="2f927-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="2f927-154">Paso 4</span><span class="sxs-lookup"><span data-stu-id="2f927-154">Step 4</span></span>

<span data-ttu-id="2f927-155">Recuperar Hola red virtual recursos y subred recursos toobe usa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2f927-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="2f927-156">Crear una dirección IP pública para la configuración de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="2f927-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="2f927-157">Crear un toobe de recurso IP pública utilizado para la puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="2f927-158">Esta dirección IP pública se usa en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="2f927-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="2f927-159">Puerta de enlace de aplicaciones no admite el uso de Hola de una dirección IP pública que se creó con una etiqueta de dominio definida.</span><span class="sxs-lookup"><span data-stu-id="2f927-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="2f927-160">Solo se admite una dirección IP pública con una etiqueta de dominio creada dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="2f927-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="2f927-161">Si necesita un nombre descriptivo de dns para puerta de enlace de aplicaciones de hello, se recomienda toouse un CNAME se registre como un alias.</span><span class="sxs-lookup"><span data-stu-id="2f927-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="2f927-162">Creación de un objeto de configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2f927-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="2f927-163">Todos los elementos de configuración se establecen antes de crear la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="2f927-164">Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f927-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="2f927-165">Paso 1</span><span class="sxs-lookup"><span data-stu-id="2f927-165">Step 1</span></span>

<span data-ttu-id="2f927-166">Crear una configuración de IP de puerta de enlace de aplicaciones, esta configuración define qué aplicación de puerta de enlace de subred hello usa.</span><span class="sxs-lookup"><span data-stu-id="2f927-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="2f927-167">Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enruta las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="2f927-168">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="2f927-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="2f927-169">Paso 2</span><span class="sxs-lookup"><span data-stu-id="2f927-169">Step 2</span></span>

<span data-ttu-id="2f927-170">Crear una configuración de IP de front-end, esta configuración asigna un ip pública o privada dirección toohello front-end de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="2f927-171">Hola siguiendo el paso asocia la dirección IP pública de Hola Hola anterior paso con la configuración de IP de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="2f927-172">Paso 3</span><span class="sxs-lookup"><span data-stu-id="2f927-172">Step 3</span></span>

<span data-ttu-id="2f927-173">Configurar grupo de direcciones IP de hello back-end con las direcciones IP de servidores web de back-end de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="2f927-174">Estas direcciones IP son direcciones IP de Hola que reciben tráfico de red de Hola que provienen de extremo IP de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="2f927-175">Reemplace Hola después tooadd de direcciones IP de sus propios extremos de dirección IP de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f927-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="2f927-176">Un nombre de dominio completo (FQDN) también es un valor válido en lugar de una dirección ip para servidores de back-end de hello mediante hello - BackendFqdns conmutador.</span><span class="sxs-lookup"><span data-stu-id="2f927-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="2f927-177">Paso 4</span><span class="sxs-lookup"><span data-stu-id="2f927-177">Step 4</span></span>

<span data-ttu-id="2f927-178">Configurar puerto IP front-end de hello para el punto de conexión IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="2f927-179">Este puerto es Hola que se conectan a los usuarios finales a.</span><span class="sxs-lookup"><span data-stu-id="2f927-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="2f927-180">Paso 5</span><span class="sxs-lookup"><span data-stu-id="2f927-180">Step 5</span></span>

<span data-ttu-id="2f927-181">Configurar certificado de Hola para puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="2f927-182">Este certificado es toodecrypt usado y volver a cifrar el tráfico de hello en puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="2f927-183">Este ejemplo configura el certificado de hello usado para la conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="2f927-184">certificado de Hello debe toobe en formato .pfx y Hola contraseña debe tener entre 4 too12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f927-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="2f927-185">Paso 6</span><span class="sxs-lookup"><span data-stu-id="2f927-185">Step 6</span></span>

<span data-ttu-id="2f927-186">Crear Agente de escucha HTTP de Hola para puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="2f927-187">Asignar la configuración de ip de front-end de hello, puerto y toouse del certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="2f927-188">Paso 7</span><span class="sxs-lookup"><span data-stu-id="2f927-188">Step 7</span></span>

<span data-ttu-id="2f927-189">Cargar certificado de hello toobe usado en hello SSL habilitado recursos del grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="2f927-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="2f927-190">sondeo de Hello predeterminado Obtiene la clave pública de Hola de hello **predeterminado** enlace SSL dirección IP de Hola back-end de y compara Hola valor de clave pública que recibe el valor de clave pública toohello que proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="2f927-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="2f927-191">Hello recuperado clave pública no será necesariamente flujos de tráfico de hello pensado sitio toowhich **si** usa encabezados de host y SNI en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2f927-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="2f927-192">En caso de duda, visite https://127.0.0.1/ en tooconfirm de back-end de hello qué certificado se usa para hello **predeterminado** enlace SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="2f927-193">Use una clave pública Hola desde esa solicitud de esta sección.</span><span class="sxs-lookup"><span data-stu-id="2f927-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="2f927-194">Si usa encabezados de host y SNI en enlaces HTTPS y no recibe una respuesta y un certificado desde un explorador manual solicitud toohttps://127.0.0.1/ en hello back-end, debe configurar un enlace de SSL predeterminado en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2f927-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="2f927-195">Si no lo hace, producirá un error de sondeos y Hola back-end no está permitido.</span><span class="sxs-lookup"><span data-stu-id="2f927-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="2f927-196">certificado de Hello proporcionado en este paso debe ser clave pública de Hola de certificados pfx de hello presente en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2f927-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="2f927-197">Exporte el certificado de hello (no el certificado de raíz hello) instalado en el servidor de back-end de hello en. CER formatear y usar en este paso.</span><span class="sxs-lookup"><span data-stu-id="2f927-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="2f927-198">Este paso, las listas blancas Hola back-end con puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="2f927-199">Paso 8</span><span class="sxs-lookup"><span data-stu-id="2f927-199">Step 8</span></span>

<span data-ttu-id="2f927-200">Definir la configuración de http de back-end de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="2f927-201">Asignar certificado Hola cargado en hello anterior paso toohello http configuración.</span><span class="sxs-lookup"><span data-stu-id="2f927-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="2f927-202">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="2f927-202">Step 9</span></span>

<span data-ttu-id="2f927-203">Crear una regla de enrutamiento de equilibrador de carga que configura el comportamiento de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="2f927-204">En este ejemplo, se crea una regla básica de operaciones por turnos.</span><span class="sxs-lookup"><span data-stu-id="2f927-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="2f927-205">Paso 10</span><span class="sxs-lookup"><span data-stu-id="2f927-205">Step 10</span></span>

<span data-ttu-id="2f927-206">Configurar el tamaño de la instancia de puerta de enlace de aplicación Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="2f927-207">los tamaños disponibles de Hello son **estándar\_pequeño**, **estándar\_medio**, y **estándar\_grande**.</span><span class="sxs-lookup"><span data-stu-id="2f927-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="2f927-208">La capacidad, los valores disponibles de hello van de 1 a 10.</span><span class="sxs-lookup"><span data-stu-id="2f927-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="2f927-209">Para las pruebas se puede elegir 1 en Número de instancias.</span><span class="sxs-lookup"><span data-stu-id="2f927-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="2f927-210">Es importante tooknow que cualquier instancia de recuento de instancias en dos no está cubierto por hello SLA y, por tanto, se recomienda que no.</span><span class="sxs-lookup"><span data-stu-id="2f927-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="2f927-211">Las puertas de enlace pequeños son toobe utilizado para pruebas de desarrollo y no para fines de producción.</span><span class="sxs-lookup"><span data-stu-id="2f927-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="2f927-212">Paso 11</span><span class="sxs-lookup"><span data-stu-id="2f927-212">Step 11</span></span>

<span data-ttu-id="2f927-213">Configurar Hola SSL directiva toobe usado en hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2f927-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="2f927-214">Puerta de enlace de aplicaciones admite Hola capacidad tooset una versión mínima de versiones del protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="2f927-215">Hello los valores siguientes son una lista de versiones del protocolo que se pueden definir.</span><span class="sxs-lookup"><span data-stu-id="2f927-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="2f927-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="2f927-216">**TLSv1_0**</span></span>
* <span data-ttu-id="2f927-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="2f927-217">**TLSv1_1**</span></span>
* <span data-ttu-id="2f927-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="2f927-218">**TLSv1_2**</span></span>

<span data-ttu-id="2f927-219">Conjuntos de Hola versión del protocolo mínimo demasiado**TLSv1_2** y permite **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**y **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** solo.</span><span class="sxs-lookup"><span data-stu-id="2f927-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="2f927-220">Crear hello puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2f927-220">Create hello Application Gateway</span></span>

<span data-ttu-id="2f927-221">Con hello todos los pasos anteriores, cree Hola Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2f927-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="2f927-222">creación de Hello de puerta de enlace de hello es un proceso de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="2f927-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="2f927-223">Límite de las versiones de protocolo SSL en una instancia de Application Gateway existente</span><span class="sxs-lookup"><span data-stu-id="2f927-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="2f927-224">Hello pasos anteriores para ir a través de la creación de una aplicación con final tooend SSL y deshabilitar determinadas versiones del protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="2f927-225">Hello en el ejemplo siguiente se deshabilita determinadas directivas SSL a una puerta de enlace de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="2f927-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="2f927-226">Paso 1</span><span class="sxs-lookup"><span data-stu-id="2f927-226">Step 1</span></span>

<span data-ttu-id="2f927-227">Recuperar tooupdate de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="2f927-228">Paso 2</span><span class="sxs-lookup"><span data-stu-id="2f927-228">Step 2</span></span>

<span data-ttu-id="2f927-229">Defina una directiva SSL.</span><span class="sxs-lookup"><span data-stu-id="2f927-229">Define an SSL policy.</span></span> <span data-ttu-id="2f927-230">En el siguiente ejemplo de Hola, TLSv1.0 y TLSv1.1 están deshabilitados y Hola conjuntos de cifrado **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, y  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** es Hola únicos que permiten.</span><span class="sxs-lookup"><span data-stu-id="2f927-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="2f927-231">Paso 3</span><span class="sxs-lookup"><span data-stu-id="2f927-231">Step 3</span></span>

<span data-ttu-id="2f927-232">Por último, actualice la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-232">Finally, update hello gateway.</span></span> <span data-ttu-id="2f927-233">Es importante toonote que este último paso es una tarea de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="2f927-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="2f927-234">Cuando termine, finalizar tooend que SSL está configurado en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2f927-235">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2f927-235">Get application gateway DNS name</span></span>

<span data-ttu-id="2f927-236">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="2f927-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="2f927-237">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="2f927-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2f927-238">los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2f927-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="2f927-239">[Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2f927-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="2f927-240">toodo, detalles de recuperación de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f927-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="2f927-241">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="2f927-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="2f927-242">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2f927-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2f927-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f927-243">Next steps</span></span>

<span data-ttu-id="2f927-244">Obtenga información sobre cómo reforzar la seguridad de Hola de las aplicaciones web con el servidor de aplicaciones Web a través de puerta de enlace de aplicaciones visitando [información general sobre el servidor de seguridad de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2f927-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
