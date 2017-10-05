---
title: Uso de Azure API Management en una red virtual con Application Gateway | Microsoft Docs
description: Aprenda a instalar y configurar Azure API Management en una red virtual interna con Application Gateway (WAF) como front-end.
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="7eeec-103">Integración de API Management en una red virtual interna con Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7eeec-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="7eeec-104"><a name="overview"> </a> Información general</span><span class="sxs-lookup"><span data-stu-id="7eeec-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="7eeec-105">El servicio API Management se puede configurar en una red virtual en un modo interno que hace que esta sea accesible únicamente desde dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="7eeec-106">Azure Application Gateway es un servicio de PAAS que proporciona un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="7eeec-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="7eeec-107">Actúa como un servicio de proxy inverso y proporciona entre su oferta un firewall de aplicaciones web (WAF).</span><span class="sxs-lookup"><span data-stu-id="7eeec-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="7eeec-108">La combinación de una instancia de API Management aprovisionada en una red virtual interna con el front-end de Application Gateway permite los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="7eeec-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="7eeec-109">Utilizar el mismo recurso de API Management para su uso por los consumidores internos y los consumidores externos.</span><span class="sxs-lookup"><span data-stu-id="7eeec-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="7eeec-110">Utilizar un único recurso de API Management y tener definido un subconjunto de API en API Management disponible para los consumidores externos.</span><span class="sxs-lookup"><span data-stu-id="7eeec-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="7eeec-111">Proporcionar una solución de llave en mano para activar y desactivar el acceso a API Management desde la red Internet pública.</span><span class="sxs-lookup"><span data-stu-id="7eeec-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="7eeec-112"><a name="scenario"> </a> Escenario</span><span class="sxs-lookup"><span data-stu-id="7eeec-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="7eeec-113">En este artículo se explica cómo usar un único servicio de API Management para los consumidores tanto internos como externos y hacer que actúe como un único servidor de front-end para las API locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="7eeec-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="7eeec-114">También verá cómo exponer solo un subconjunto de las API (resaltado en verde en el ejemplo) para permitir su uso externo, usando para ello la funcionalidad PathBasedRouting disponible en Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="7eeec-115">En el primer ejemplo de la configuración, todas las API se administran únicamente desde dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="7eeec-116">Los consumidores internos (resaltados en color naranja) pueden tener acceso a todas las API internas y externas.</span><span class="sxs-lookup"><span data-stu-id="7eeec-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="7eeec-117">El tráfico nunca se envía a Internet y se entrega un alto rendimiento a través de circuitos Express Route.</span><span class="sxs-lookup"><span data-stu-id="7eeec-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![ruta de dirección URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="7eeec-119"><a name="before-you-begin"> </a> Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7eeec-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="7eeec-120">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="7eeec-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="7eeec-121">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la página [Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7eeec-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="7eeec-122">Cree una red virtual y subredes independientes para API Management y Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="7eeec-123">Si desea crear un servidor DNS personalizado para la red virtual, debe hacerlo antes de iniciar la implementación.</span><span class="sxs-lookup"><span data-stu-id="7eeec-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="7eeec-124">Vuelva a comprobar que funciona asegurando que la máquina virtual creada en una subred nueva de la red virtual puede resolver y acceder a todos los puntos de conexión de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="7eeec-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="7eeec-125">¿Qué se necesita para crear una integración entre API Management y Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="7eeec-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="7eeec-126">**Grupo de servidores de back-end:** se trata de la dirección IP virtual interna del servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="7eeec-127">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="7eeec-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="7eeec-128">Estos valores se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="7eeec-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="7eeec-129">**Puerto front-end:** es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7eeec-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="7eeec-130">El tráfico que llega se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="7eeec-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="7eeec-131">**Agente de escucha** : tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="7eeec-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="7eeec-132">**Regla:** la regla enlaza un agente de escucha con un grupo de servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="7eeec-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="7eeec-133">**Sondeo de mantenimiento personalizado:** Application Gateway, de forma predeterminada, usa sondeos basados en direcciones IP para determinar cuáles son los servidores de BackendAddressPool que están activos.</span><span class="sxs-lookup"><span data-stu-id="7eeec-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="7eeec-134">El servicio API Management responde solo a las solicitudes que tienen el encabezado de host correcto, por lo tanto, los sondeos predeterminados no podrán completarse.</span><span class="sxs-lookup"><span data-stu-id="7eeec-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="7eeec-135">Es necesario definir el sondeo de mantenimiento personalizado para ayudar a la puerta de enlace de aplicaciones a determinar que el servicio está activo y debe reenviar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="7eeec-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="7eeec-136">**Certificado de dominio personalizado:** para tener acceso a API Management desde Internet, debe crear una asignación de CNAME del nombre de host en el nombre DNS de front-end de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="7eeec-137">Esto garantiza que el encabezado de nombre de host y el certificado enviados a Application Gateway que se reenvían a API Management pueden ser reconocidos como válidos por APIM.</span><span class="sxs-lookup"><span data-stu-id="7eeec-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="7eeec-138"><a name="overview-steps"> </a> Pasos necesarios para integrar API Management y Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7eeec-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="7eeec-139">Cree un grupo de recursos para el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eeec-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="7eeec-140">Cree una red virtual, una subred y una IP pública para Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="7eeec-141">Cree otra subred para API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="7eeec-142">Cree un servicio API Management en la subred de la red virtual creada anteriormente y asegúrese de que usa el modo interno.</span><span class="sxs-lookup"><span data-stu-id="7eeec-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="7eeec-143">Configure el nombre de dominio personalizado del servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="7eeec-144">Cree un objeto de configuración de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="7eeec-145">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="7eeec-146">Cree un CNAME del nombre DNS público de Application Gateway en el nombre de host de proxy de API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="7eeec-147">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="7eeec-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="7eeec-148">Asegúrese de que está usando la versión más reciente de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7eeec-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="7eeec-149">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7eeec-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="7eeec-150">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7eeec-150">Step 1</span></span>

<span data-ttu-id="7eeec-151">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="7eeec-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7eeec-152">Autentíquese con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="7eeec-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="7eeec-153">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7eeec-153">Step 2</span></span>

<span data-ttu-id="7eeec-154">Compruebe las suscripciones para la cuenta y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="7eeec-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="7eeec-155">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7eeec-155">Step 3</span></span>

<span data-ttu-id="7eeec-156">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="7eeec-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="7eeec-157">El Administrador de recursos de Azure requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7eeec-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7eeec-158">Esta se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eeec-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="7eeec-159">Asegúrese de que todos los comandos para crear una puerta de enlace de aplicaciones usan el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eeec-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="7eeec-160">Creación de una red virtual y una subred para la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7eeec-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="7eeec-161">En el ejemplo siguiente se muestra cómo crear una red virtual con Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="7eeec-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="7eeec-162">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7eeec-162">Step 1</span></span>

<span data-ttu-id="7eeec-163">Asigne el intervalo de direcciones 10.0.0.0/24 a la variable subnet que se va a usar para Application Gateway al crear la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="7eeec-164">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7eeec-164">Step 2</span></span>

<span data-ttu-id="7eeec-165">Asigne el intervalo de direcciones 10.0.1.0/24 a la variable subnet que se va a usar para API Management al crear la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="7eeec-166">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7eeec-166">Step 3</span></span>

<span data-ttu-id="7eeec-167">Cree una red virtual denominada **appgwvnet** en el grupo de recursos **apim-appGw-RG** para la región Oeste de EE. UU. con el prefijo 10.0.0.0/16 y las subredes 10.0.0.0/24 y 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="7eeec-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="7eeec-168">Paso 4</span><span class="sxs-lookup"><span data-stu-id="7eeec-168">Step 4</span></span>

<span data-ttu-id="7eeec-169">Asigne una variable de subred para los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="7eeec-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="7eeec-170">Cree un servicio de API Management dentro de una red virtual configurada en modo interno.</span><span class="sxs-lookup"><span data-stu-id="7eeec-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="7eeec-171">En el ejemplo siguiente se muestra cómo crear un servicio de API Management en una red virtual configurada únicamente para el acceso interno.</span><span class="sxs-lookup"><span data-stu-id="7eeec-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="7eeec-172">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7eeec-172">Step 1</span></span>
<span data-ttu-id="7eeec-173">Cree un objeto de red virtual de API Management con la subred $apimsubnetdata creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7eeec-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="7eeec-174">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7eeec-174">Step 2</span></span>
<span data-ttu-id="7eeec-175">Cree un servicio de API Management dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="7eeec-176">Cuando el comando anterior se complete con éxito, consulte [la configuración de DNS necesaria para tener acceso al servicio de API Management en una red virtual interna](api-management-using-with-internal-vnet.md#apim-dns-configuration) para tener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="7eeec-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="7eeec-177">Configuración de un nombre de dominio personalizado en API Management</span><span class="sxs-lookup"><span data-stu-id="7eeec-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="7eeec-178">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7eeec-178">Step 1</span></span>
<span data-ttu-id="7eeec-179">Cargue el certificado con clave privada para el dominio.</span><span class="sxs-lookup"><span data-stu-id="7eeec-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="7eeec-180">En este ejemplo es `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="7eeec-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="7eeec-181">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7eeec-181">Step 2</span></span>
<span data-ttu-id="7eeec-182">Una vez cargado el certificado, cree un objeto de configuración de nombre de host para el proxy con el nombre de host de `api.contoso.net`, ya que el certificado de ejemplo proporciona la autoridad para el dominio `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="7eeec-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="7eeec-183">Creación de una dirección IP pública para la configuración del front-end</span><span class="sxs-lookup"><span data-stu-id="7eeec-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="7eeec-184">Cree un recurso IP público **publicIP01** en el grupo de recursos **apim-appGw-RG** para la región Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7eeec-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="7eeec-185">Se asigna una dirección IP a la puerta de enlace de aplicaciones cuando se inicia el servicio.</span><span class="sxs-lookup"><span data-stu-id="7eeec-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="7eeec-186">Creación de una configuración de puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7eeec-186">Create application gateway configuration</span></span>

<span data-ttu-id="7eeec-187">Se deben haber definido todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7eeec-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="7eeec-188">En los pasos siguientes, se crean los elementos de configuración necesarios para un recurso de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7eeec-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="7eeec-189">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7eeec-189">Step 1</span></span>

<span data-ttu-id="7eeec-190">Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="7eeec-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="7eeec-191">Cuando se inicia Application Gateway, elige una dirección IP de la subred configurada y redirige el tráfico de red a las direcciones IP en el grupo IP de back-end.</span><span class="sxs-lookup"><span data-stu-id="7eeec-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="7eeec-192">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="7eeec-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="7eeec-193">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7eeec-193">Step 2</span></span>

<span data-ttu-id="7eeec-194">Configure el puerto IP de front-end para el punto de conexión de IP pública.</span><span class="sxs-lookup"><span data-stu-id="7eeec-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="7eeec-195">Este puerto es el puerto al que se conectan los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="7eeec-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="7eeec-196">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7eeec-196">Step 3</span></span>

<span data-ttu-id="7eeec-197">Configuración de la dirección IP de front-end con el punto de conexión de IP pública</span><span class="sxs-lookup"><span data-stu-id="7eeec-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="7eeec-198">Paso 4</span><span class="sxs-lookup"><span data-stu-id="7eeec-198">Step 4</span></span>

<span data-ttu-id="7eeec-199">Configure el certificado para Application Gateway, usado para descifrar y volver a cifrar el tráfico que pasa por ella.</span><span class="sxs-lookup"><span data-stu-id="7eeec-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="7eeec-200">Paso 5</span><span class="sxs-lookup"><span data-stu-id="7eeec-200">Step 5</span></span>

<span data-ttu-id="7eeec-201">Cree el agente de escucha HTTP para Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="7eeec-202">Asigne la configuración IP de front-end, el puerto y el certificado SSL que se usarán.</span><span class="sxs-lookup"><span data-stu-id="7eeec-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="7eeec-203">Paso 6</span><span class="sxs-lookup"><span data-stu-id="7eeec-203">Step 6</span></span>

<span data-ttu-id="7eeec-204">Cree un sondeo personalizado para el punto de conexión de dominio del proxy `ContosoApi` del servicio de API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="7eeec-205">La ruta de acceso `/status-0123456789abcdef` es un punto de conexión de mantenimiento predeterminado hospedado en todos los servicios de API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="7eeec-206">Establezca `api.contoso.net` como un nombre de host de sondeo personalizado para protegerlo con el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="7eeec-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="7eeec-207">El nombre de host `contosoapi.azure-api.net` es el nombre de host de proxy predeterminado configurado cuando se crea un servicio denominado `contosoapi` en el ámbito público de Azure.</span><span class="sxs-lookup"><span data-stu-id="7eeec-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="7eeec-208">Paso 7</span><span class="sxs-lookup"><span data-stu-id="7eeec-208">Step 7</span></span>

<span data-ttu-id="7eeec-209">Cargue el certificado que se usará en los recursos del grupo de back-end habilitado para SSL.</span><span class="sxs-lookup"><span data-stu-id="7eeec-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="7eeec-210">Este es el mismo certificado que ha proporcionado en el paso 4 anterior.</span><span class="sxs-lookup"><span data-stu-id="7eeec-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="7eeec-211">Paso 8</span><span class="sxs-lookup"><span data-stu-id="7eeec-211">Step 8</span></span>

<span data-ttu-id="7eeec-212">Configure las opciones de back-end HTTP para Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="7eeec-213">Esto incluye el establecimiento de un límite de tiempo de espera para la solicitud de back-end después del cual se cancela.</span><span class="sxs-lookup"><span data-stu-id="7eeec-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="7eeec-214">Este valor es distinto del tiempo de espera del sondeo.</span><span class="sxs-lookup"><span data-stu-id="7eeec-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="7eeec-215">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="7eeec-215">Step 9</span></span>

<span data-ttu-id="7eeec-216">Configure el grupo de direcciones IP de back-end denominado **apimbackend** con dirección IP virtual interna para el servicio de API Management creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7eeec-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="7eeec-217">Paso 10</span><span class="sxs-lookup"><span data-stu-id="7eeec-217">Step 10</span></span>

<span data-ttu-id="7eeec-218">Cree una configuración para un back-end ficticio (inexistente).</span><span class="sxs-lookup"><span data-stu-id="7eeec-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="7eeec-219">Las solicitudes a las rutas de acceso de API que no se desean exponer desde API Management a través de Application Gateway llegarán a este back-end y se devolverá un error 404.</span><span class="sxs-lookup"><span data-stu-id="7eeec-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="7eeec-220">Defina la configuración HTTP para el back-end ficticio.</span><span class="sxs-lookup"><span data-stu-id="7eeec-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="7eeec-221">Configure un back-end ficticio **dummyBackendPool**, que señale a una dirección FQDN **dummybackend.com**. Esta dirección FQDN no existe en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="7eeec-222">Cree una configuración de regla que Application Gateway utilice de forma predeterminada y que señale al back-end inexistente **dummybackend.com** en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7eeec-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="7eeec-223">Paso 11</span><span class="sxs-lookup"><span data-stu-id="7eeec-223">Step 11</span></span>

<span data-ttu-id="7eeec-224">Configuración de rutas de acceso de reglas de URL para los grupos de back-end</span><span class="sxs-lookup"><span data-stu-id="7eeec-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="7eeec-225">Esto permite seleccionar solo algunas de las API en API Management para que se expongan al público.</span><span class="sxs-lookup"><span data-stu-id="7eeec-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="7eeec-226">Por ejemplo, en el caso de encontrar `Echo API` (/echo/), `Calculator API` (/calc/), etc., haga que solo `Echo API` resulte accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="7eeec-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="7eeec-227">En el ejemplo siguiente se crea una regla sencilla para la ruta de acceso "/echo/" que enruta el tráfico al back-end "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="7eeec-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="7eeec-228">Si la ruta de acceso no coincide con las reglas de ruta de acceso que se desean habilitar desde API Management, la configuración de asignación de ruta de acceso de regla también configura un grupo de direcciones de back-end predeterminado llamado **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="7eeec-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="7eeec-229">Por ejemplo, http://api.contoso.net/calc/* dirige a **dummyBackendPool**, ya que es el grupo predeterminado para el tráfico no coincidente.</span><span class="sxs-lookup"><span data-stu-id="7eeec-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="7eeec-230">El paso anterior garantiza que solo se permiten las solicitudes para la ruta de acceso "/echo" a través de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="7eeec-231">Las solicitudes a otras API configuradas en API Management generarán errores 404 desde Application Gateway cuando se tiene acceso a ellas desde Internet.</span><span class="sxs-lookup"><span data-stu-id="7eeec-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="7eeec-232">Paso 12</span><span class="sxs-lookup"><span data-stu-id="7eeec-232">Step 12</span></span>

<span data-ttu-id="7eeec-233">Cree una configuración de regla para que Application Gateway use el enrutamiento basado en la ruta de acceso de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7eeec-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="7eeec-234">Paso 13</span><span class="sxs-lookup"><span data-stu-id="7eeec-234">Step 13</span></span>

<span data-ttu-id="7eeec-235">Configure el número de instancias y el tamaño de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="7eeec-236">Aquí usamos [WAFS SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para aumentar la seguridad de los recursos de API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="7eeec-237">Paso 14</span><span class="sxs-lookup"><span data-stu-id="7eeec-237">Step 14</span></span>

<span data-ttu-id="7eeec-238">Configuración de WAFS para que esté en modo "Prevención".</span><span class="sxs-lookup"><span data-stu-id="7eeec-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="7eeec-239">Creación de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7eeec-239">Create Application Gateway</span></span>

<span data-ttu-id="7eeec-240">Cree una instancia de Application Gateway con todos los objetos de configuración de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="7eeec-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="7eeec-241">Aplicación de un CNAME al nombre de host del proxy de API Management para el nombre DNS público del recurso de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7eeec-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="7eeec-242">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="7eeec-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="7eeec-243">Cuando se utiliza una dirección IP pública, Application Gateway requiere un nombre DNS asignado dinámicamente, que puede no ser fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="7eeec-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="7eeec-244">El nombre DNS de Application Gateway se debe utilizar para crear un registro CNAME, que apunta el nombre de host del proxy (por ejemplo, `api.contoso.net` en los ejemplos anteriores) a este nombre de DNS.</span><span class="sxs-lookup"><span data-stu-id="7eeec-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="7eeec-245">Para configurar el registro IP CNAME de front-end, recupere los detalles de Application Gateway y su nombre DNS o IP asociados mediante el elemento PublicIPAddress.</span><span class="sxs-lookup"><span data-stu-id="7eeec-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="7eeec-246">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7eeec-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="7eeec-247"><a name="summary"> </a>Resumen</span><span class="sxs-lookup"><span data-stu-id="7eeec-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="7eeec-248">El servicio Azure API Management configurado en una red virtual proporciona una interfaz de puerta de enlace única para todas las API configuradas, independientemente de si están hospedadas en local o en la nube.</span><span class="sxs-lookup"><span data-stu-id="7eeec-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="7eeec-249">La integración de Application Gateway con API Management proporciona la flexibilidad de habilitar de manera selectiva API determinadas para que estén accesibles en Internet, así como la provisión de un firewall de aplicación web como front-end para la instancia de API Management.</span><span class="sxs-lookup"><span data-stu-id="7eeec-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="7eeec-250"><a name="next-steps"> </a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7eeec-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="7eeec-251">Obtenga más información sobre Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7eeec-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="7eeec-252">Introducción a Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7eeec-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="7eeec-253">Firewall de aplicaciones web de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7eeec-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="7eeec-254">Application Gateway mediante enrutamiento basado en rutas de acceso</span><span class="sxs-lookup"><span data-stu-id="7eeec-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="7eeec-255">Más información acerca de API Management y redes virtuales</span><span class="sxs-lookup"><span data-stu-id="7eeec-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="7eeec-256">El uso de API Management solo está disponible en la red virtual</span><span class="sxs-lookup"><span data-stu-id="7eeec-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="7eeec-257">Usar Azure API Management con redes virtuales</span><span class="sxs-lookup"><span data-stu-id="7eeec-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
