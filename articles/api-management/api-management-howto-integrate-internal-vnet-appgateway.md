---
title: "aaaHow toouse administración de API de Azure en red Virtual con la puerta de enlace de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosetup y configurar la administración de API de Azure en red Virtual interna con aplicación de puerta de enlace (WAFS) como front-end"
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
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="64e8c-103">Integración de API Management en una red virtual interna con Application Gateway</span><span class="sxs-lookup"><span data-stu-id="64e8c-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="64e8c-104"><a name="overview"></a> Información general</span><span class="sxs-lookup"><span data-stu-id="64e8c-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="64e8c-105">Hola servicio de administración de API se puede configurar en una red Virtual en modo interno que hace que sea accesible únicamente desde dentro de hello red Virtual.</span><span class="sxs-lookup"><span data-stu-id="64e8c-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="64e8c-106">Azure Application Gateway es un servicio de PAAS que proporciona un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="64e8c-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="64e8c-107">Actúa como un servicio de proxy inverso y proporciona entre su oferta un firewall de aplicaciones web (WAF).</span><span class="sxs-lookup"><span data-stu-id="64e8c-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="64e8c-108">Combinar aprovisionado en una red virtual interna con front-end de hello puerta de enlace de aplicaciones de administración de API permite Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="64e8c-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="64e8c-109">Use Hola mismo recurso de administración de API para su uso por los consumidores internos y externo a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="64e8c-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="64e8c-110">Utilizar un único recurso de API Management y tener definido un subconjunto de API en API Management disponible para los consumidores externos.</span><span class="sxs-lookup"><span data-stu-id="64e8c-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="64e8c-111">Proporcionar una manera de preparada tooswitch acceso tooAPI administración de hello Internet pública y desactivar.</span><span class="sxs-lookup"><span data-stu-id="64e8c-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="64e8c-112"><a name="scenario"></a> Escenario</span><span class="sxs-lookup"><span data-stu-id="64e8c-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="64e8c-113">En este artículo se tratan cómo toouse una única API de administración de servicio para los consumidores tanto internos como externos y hacer que actúe como un único servidor front-end para ambos local y las API en la nube.</span><span class="sxs-lookup"><span data-stu-id="64e8c-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="64e8c-114">También verá cómo tooexpose solo un subconjunto de las API (en el ejemplo de Hola que están resaltados en verde) para su uso externo con funcionalidad de PathBasedRouting de hello disponible en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="64e8c-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="64e8c-115">En el ejemplo de Hola primero el programa de instalación se administran todas las API sólo desde dentro de la red Virtual.</span><span class="sxs-lookup"><span data-stu-id="64e8c-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="64e8c-116">Los consumidores internos (resaltados en color naranja) pueden tener acceso a todas las API internas y externas.</span><span class="sxs-lookup"><span data-stu-id="64e8c-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="64e8c-117">Tráfico no sale nunca tooInternet que se entrega un alto rendimiento a través de circuitos Expressroute.</span><span class="sxs-lookup"><span data-stu-id="64e8c-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![ruta de dirección URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="64e8c-119"><a name="before-you-begin"></a> Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="64e8c-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="64e8c-120">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="64e8c-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="64e8c-121">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="64e8c-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="64e8c-122">Cree una red virtual y subredes independientes para API Management y Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="64e8c-123">Si tiene previsto toocreate un servidor DNS personalizado para hello red Virtual, debe hacerlo antes de iniciar la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="64e8c-124">Vuelve a revisar funciona que garantiza una máquina virtual creada en una subred nueva en hello red Virtual puede resolver y acceder a todos los extremos de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="64e8c-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="64e8c-125">¿Qué es necesario toocreate una integración entre administración de API y la puerta de enlace de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="64e8c-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="64e8c-126">**Grupo de servidores de back-end:** se trata de dirección IP virtual interna del Hola de hello servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="64e8c-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="64e8c-127">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="64e8c-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="64e8c-128">Estos valores son servidores tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="64e8c-129">**Puerto front-end:** es Hola puerto público que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="64e8c-130">Tráfico alcanzando obtiene tooone redirigida de hello servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="64e8c-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="64e8c-131">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="64e8c-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="64e8c-132">**Regla:** regla Hola enlaza un grupo de servidor back-end de tooa de agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="64e8c-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="64e8c-133">**Sondeo de estado personalizado:** puerta de enlace de la aplicación, de forma predeterminada, usa toofigure de sondeos basados en direcciones IP a qué servidores en hello BackendAddressPool están activas.</span><span class="sxs-lookup"><span data-stu-id="64e8c-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="64e8c-134">Hola servicio de administración de API sólo responde toorequests que tienen el encabezado de host correcto de hello, por lo tanto, un error Hola predeterminado sondeos.</span><span class="sxs-lookup"><span data-stu-id="64e8c-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="64e8c-135">Un sondeo de estado personalizado necesita toobe definido puerta de enlace de aplicaciones de toohelp determinar que el servicio de Hola esté activo, y deben reenviar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="64e8c-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="64e8c-136">**Certificado de dominio personalizado:** tooaccess administración de API de hello necesita toocreate una asignación de CNAME de su nombre DNS front-end de nombre de host toohello puerta de enlace de aplicaciones de internet.</span><span class="sxs-lookup"><span data-stu-id="64e8c-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="64e8c-137">Esto garantiza que, encabezado de nombre de host de Hola y el certificado enviado tooApplication puerta de enlace que se reenvía a tooAPI administración sea una que APIM pueda reconocer como válido.</span><span class="sxs-lookup"><span data-stu-id="64e8c-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="64e8c-138"><a name="overview-steps"></a> Pasos necesarios para integrar API Management y Application Gateway</span><span class="sxs-lookup"><span data-stu-id="64e8c-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="64e8c-139">Cree un grupo de recursos para Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64e8c-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="64e8c-140">Crear una red Virtual, subred y dirección IP pública para hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="64e8c-141">Cree otra subred para API Management.</span><span class="sxs-lookup"><span data-stu-id="64e8c-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="64e8c-142">Crear un servicio de administración de API dentro de la subred de red virtual de hello creado anteriormente y asegúrese de que se utiliza el modo de hello interno.</span><span class="sxs-lookup"><span data-stu-id="64e8c-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="64e8c-143">Configurar nombre de dominio personalizado de Hola Hola servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="64e8c-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="64e8c-144">Cree un objeto de configuración de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="64e8c-145">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="64e8c-146">Crear un CNAME de nombre DNS público de hello del nombre del servidor proxy de administración de API de hello Application Gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="64e8c-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="64e8c-147">Creación de un grupo de recursos para el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="64e8c-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="64e8c-148">Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="64e8c-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="64e8c-149">Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="64e8c-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="64e8c-150">Paso 1</span><span class="sxs-lookup"><span data-stu-id="64e8c-150">Step 1</span></span>

<span data-ttu-id="64e8c-151">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="64e8c-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="64e8c-152">Autentíquese con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="64e8c-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="64e8c-153">Paso 2</span><span class="sxs-lookup"><span data-stu-id="64e8c-153">Step 2</span></span>

<span data-ttu-id="64e8c-154">Compruebe las suscripciones de hello para la cuenta de hello y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="64e8c-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="64e8c-155">Paso 3</span><span class="sxs-lookup"><span data-stu-id="64e8c-155">Step 3</span></span>

<span data-ttu-id="64e8c-156">Cree un grupo de recursos (omita este paso si usa uno existente).</span><span class="sxs-lookup"><span data-stu-id="64e8c-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="64e8c-157">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="64e8c-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="64e8c-158">Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64e8c-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="64e8c-159">Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64e8c-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="64e8c-160">Crear una red Virtual y una subred de puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="64e8c-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="64e8c-161">Hola de ejemplo siguiente muestra cómo Hola a toocreate una red Virtual con el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="64e8c-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="64e8c-162">Paso 1</span><span class="sxs-lookup"><span data-stu-id="64e8c-162">Step 1</span></span>

<span data-ttu-id="64e8c-163">Asignar la subred Hola dirección intervalo 10.0.0.0/24 toohello variable toobe usará para puerta de enlace de aplicaciones mientras se crea una red Virtual.</span><span class="sxs-lookup"><span data-stu-id="64e8c-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="64e8c-164">Paso 2</span><span class="sxs-lookup"><span data-stu-id="64e8c-164">Step 2</span></span>

<span data-ttu-id="64e8c-165">Asignar la subred Hola dirección intervalo 10.0.1.0/24 toohello variable toobe usará para la administración de API mientras se crea una red Virtual.</span><span class="sxs-lookup"><span data-stu-id="64e8c-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="64e8c-166">Paso 3</span><span class="sxs-lookup"><span data-stu-id="64e8c-166">Step 3</span></span>

<span data-ttu-id="64e8c-167">Crear una red Virtual denominado **appgwvnet** en grupo de recursos **apim-appGw-RG** para región de oeste de Estados Unidos de hello mediante Hola prefijo 10.0.0.0/16 con subredes 10.0.0.0/24 y 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="64e8c-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="64e8c-168">Paso 4</span><span class="sxs-lookup"><span data-stu-id="64e8c-168">Step 4</span></span>

<span data-ttu-id="64e8c-169">Asignar una variable de subred para los pasos siguientes Hola</span><span class="sxs-lookup"><span data-stu-id="64e8c-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="64e8c-170">Cree un servicio de API Management dentro de una red virtual configurada en modo interno.</span><span class="sxs-lookup"><span data-stu-id="64e8c-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="64e8c-171">Hello en el ejemplo siguiente se muestra cómo toocreate un servicio de administración de API en una red virtual configurado para el acceso interno solo.</span><span class="sxs-lookup"><span data-stu-id="64e8c-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="64e8c-172">Paso 1</span><span class="sxs-lookup"><span data-stu-id="64e8c-172">Step 1</span></span>
<span data-ttu-id="64e8c-173">Cree un objeto de red Virtual de administración de API con la subred de hello $apimsubnetdata creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64e8c-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="64e8c-174">Paso 2</span><span class="sxs-lookup"><span data-stu-id="64e8c-174">Step 2</span></span>
<span data-ttu-id="64e8c-175">Crear un servicio de administración de API dentro de hello red Virtual.</span><span class="sxs-lookup"><span data-stu-id="64e8c-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="64e8c-176">Después de hello por encima del comando se ejecuta correctamente, consulte demasiado[tooaccess servicio de administración de API de red virtual interna requiere una configuración de DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess lo.</span><span class="sxs-lookup"><span data-stu-id="64e8c-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="64e8c-177">Configuración de un nombre de dominio personalizado en API Management</span><span class="sxs-lookup"><span data-stu-id="64e8c-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="64e8c-178">Paso 1</span><span class="sxs-lookup"><span data-stu-id="64e8c-178">Step 1</span></span>
<span data-ttu-id="64e8c-179">Cargar Hola certificado con clave privada para el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="64e8c-180">En este ejemplo es `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="64e8c-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="64e8c-181">Paso 2</span><span class="sxs-lookup"><span data-stu-id="64e8c-181">Step 2</span></span>
<span data-ttu-id="64e8c-182">Una vez cargado el certificado de hello, crear un objeto de configuración de nombre de host para el proxy de hello con un nombre de host de `api.contoso.net`, tal y como certificado de ejemplo de Hola proporciona autoridad para hello `*.contoso.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="64e8c-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="64e8c-183">Crear una dirección IP pública para la configuración de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="64e8c-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="64e8c-184">Crear un recurso IP público **publicIP01** en grupo de recursos **apim-appGw-RG** de región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="64e8c-185">Una dirección IP se asigna la puerta de enlace de toohello aplicación cuando se inicia el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="64e8c-186">Creación de una configuración de puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="64e8c-186">Create application gateway configuration</span></span>

<span data-ttu-id="64e8c-187">Todos los elementos de configuración deben estar configurados antes de crear la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="64e8c-188">Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64e8c-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="64e8c-189">Paso 1</span><span class="sxs-lookup"><span data-stu-id="64e8c-189">Step 1</span></span>

<span data-ttu-id="64e8c-190">Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="64e8c-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="64e8c-191">Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="64e8c-192">Tenga en cuenta que cada instancia toma una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="64e8c-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="64e8c-193">Paso 2</span><span class="sxs-lookup"><span data-stu-id="64e8c-193">Step 2</span></span>

<span data-ttu-id="64e8c-194">Configurar puerto IP front-end de hello para el punto de conexión IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="64e8c-195">Este puerto es Hola que se conectan a los usuarios finales a.</span><span class="sxs-lookup"><span data-stu-id="64e8c-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="64e8c-196">Paso 3</span><span class="sxs-lookup"><span data-stu-id="64e8c-196">Step 3</span></span>

<span data-ttu-id="64e8c-197">Configurar IP de front-end de hello con punto de conexión IP pública.</span><span class="sxs-lookup"><span data-stu-id="64e8c-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="64e8c-198">Paso 4</span><span class="sxs-lookup"><span data-stu-id="64e8c-198">Step 4</span></span>

<span data-ttu-id="64e8c-199">Configurar certificado Hola de puerta de enlace de aplicaciones, hello usa toodecrypt y volver a cifrar el tráfico de hello pasan a través.</span><span class="sxs-lookup"><span data-stu-id="64e8c-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="64e8c-200">Paso 5</span><span class="sxs-lookup"><span data-stu-id="64e8c-200">Step 5</span></span>

<span data-ttu-id="64e8c-201">Crear Agente de escucha HTTP de Hola para hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="64e8c-202">Asignar configuración de IP de front-end de hello, puerto y tooit del certificado ssl.</span><span class="sxs-lookup"><span data-stu-id="64e8c-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="64e8c-203">Paso 6</span><span class="sxs-lookup"><span data-stu-id="64e8c-203">Step 6</span></span>

<span data-ttu-id="64e8c-204">Crear un servicio de administración de API de sondeo personalizado toohello `ContosoApi` extremo proxy de dominio.</span><span class="sxs-lookup"><span data-stu-id="64e8c-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="64e8c-205">ruta de acceso de Hello `/status-0123456789abcdef` es un extremo de estado predeterminado hospedado en todos los servicios de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="64e8c-206">Establecer `api.contoso.net` como un toosecure de nombre de host de sondeo personalizado con el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="64e8c-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="64e8c-207">Hola hostname `contosoapi.azure-api.net` es el nombre de host de hello predeterminado proxy configurado cuando un servicio denominado `contosoapi` se crea en Azure pública.</span><span class="sxs-lookup"><span data-stu-id="64e8c-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="64e8c-208">Paso 7</span><span class="sxs-lookup"><span data-stu-id="64e8c-208">Step 7</span></span>

<span data-ttu-id="64e8c-209">Cargar certificado de hello toobe usado en los recursos de grupo habilitado para SSL de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="64e8c-210">Se trata de hello mismo certificado que proporciona en el paso 4 anterior.</span><span class="sxs-lookup"><span data-stu-id="64e8c-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="64e8c-211">Paso 8</span><span class="sxs-lookup"><span data-stu-id="64e8c-211">Step 8</span></span>

<span data-ttu-id="64e8c-212">La configuración de back-end HTTP de hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="64e8c-213">Esto incluye el establecimiento de un límite de tiempo de espera para la solicitud de back-end después del cual se cancela.</span><span class="sxs-lookup"><span data-stu-id="64e8c-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="64e8c-214">Este valor es diferente de tiempo de espera de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="64e8c-215">Paso 9:</span><span class="sxs-lookup"><span data-stu-id="64e8c-215">Step 9</span></span>

<span data-ttu-id="64e8c-216">Configurar un grupo de direcciones IP de back-end denominado **apimbackend** con dirección IP virtual interna Hola dirección del servicio de administración de API de Hola creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64e8c-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="64e8c-217">Paso 10</span><span class="sxs-lookup"><span data-stu-id="64e8c-217">Step 10</span></span>

<span data-ttu-id="64e8c-218">Cree una configuración para un back-end ficticio (inexistente).</span><span class="sxs-lookup"><span data-stu-id="64e8c-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="64e8c-219">Rutas de acceso de solicitudes tooAPI que deseamos tooexpose de la API de administración a través de puerta de enlace de aplicaciones se alcanza este back-end y se devolverá 404.</span><span class="sxs-lookup"><span data-stu-id="64e8c-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="64e8c-220">Configurar opciones de HTTP de back-end ficticio de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="64e8c-221">Configurar un back-end ficticio **dummyBackendPool**, que señala la dirección de FQDN tooa **dummybackend.com**. Esta dirección FQDN no existe en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="64e8c-222">Crear una regla de configuración que Hola puerta de enlace de aplicación utilizará de forma predeterminada que señala el back-end de toohello inexistente **dummybackend.com** Hola red Virtual.</span><span class="sxs-lookup"><span data-stu-id="64e8c-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="64e8c-223">Paso 11</span><span class="sxs-lookup"><span data-stu-id="64e8c-223">Step 11</span></span>

<span data-ttu-id="64e8c-224">Configurar rutas de acceso de regla de dirección URL para grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="64e8c-225">Esto permite seleccionar solo algunas de hello las API de administración de API para que se va a exponen toohello público.</span><span class="sxs-lookup"><span data-stu-id="64e8c-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="64e8c-226">Por ejemplo, en el caso de encontrar `Echo API` (/echo/), `Calculator API` (/calc/), etc., haga que solo `Echo API` resulte accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="64e8c-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="64e8c-227">Hello en el ejemplo siguiente se crea una regla sencilla para hello "/ eco /" ruta de acceso enrutamiento tráfico toohello back-end "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="64e8c-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="64e8c-228">Si no coincide con la ruta de acceso de Hola queremos tooenable de la administración de API, configuración de mapa de ruta de acceso también configura un grupo de direcciones de back-end de manera predeterminada con el nombre de regla de Hola de reglas de ruta de acceso de hello **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="64e8c-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="64e8c-229">Por ejemplo, http://api.contoso.net/calc/ * va demasiado**dummyBackendPool** tal y como se define como grupo predeterminado de hello para el tráfico no coincidente.</span><span class="sxs-lookup"><span data-stu-id="64e8c-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="64e8c-230">Hola encima paso garantiza que sólo las solicitudes de ruta de acceso de Hola "/ echo" se permiten a través de hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="64e8c-231">Tooother solicitudes que API configuradas en administración de API producirá 404 errores de puerta de enlace de aplicaciones cuando se tiene acceso desde Internet Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="64e8c-232">Paso 12</span><span class="sxs-lookup"><span data-stu-id="64e8c-232">Step 12</span></span>

<span data-ttu-id="64e8c-233">Cree una configuración de regla para hello Application Gateway toouse basado en ruta enrutamiento de direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="64e8c-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="64e8c-234">Paso 13</span><span class="sxs-lookup"><span data-stu-id="64e8c-234">Step 13</span></span>

<span data-ttu-id="64e8c-235">Configurar el número de Hola de instancias y el tamaño de hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="64e8c-236">Aquí usamos hello [WAFS SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para aumentar la seguridad del programa Hola a recursos de administración de API.</span><span class="sxs-lookup"><span data-stu-id="64e8c-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="64e8c-237">Paso 14</span><span class="sxs-lookup"><span data-stu-id="64e8c-237">Step 14</span></span>

<span data-ttu-id="64e8c-238">Configurar WAFS toobe en modo de "Prevención".</span><span class="sxs-lookup"><span data-stu-id="64e8c-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="64e8c-239">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="64e8c-239">Create Application Gateway</span></span>

<span data-ttu-id="64e8c-240">Crear una puerta de enlace de la aplicación con todos los objetos de configuración de Hola de hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="64e8c-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="64e8c-241">CNAME Hola administración de API proxy hostname toohello nombre DNS público del programa Hola a recursos de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="64e8c-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="64e8c-242">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="64e8c-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="64e8c-243">Cuando se usa una IP pública, puerta de enlace de aplicación requiere un nombre DNS asignado dinámicamente, que no puede ser fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="64e8c-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="64e8c-244">Hello nombre DNS de la puerta de enlace de aplicaciones debe ser toocreate usa un registro CNAME que señala el nombre de host de hello APIM proxy (por ejemplo, `api.contoso.net` en los ejemplos de hello anteriores) toothis nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="64e8c-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="64e8c-245">front-end de tooconfigure Hola un registro CNAME de IP, recuperar detalles de Hola de Hola puerta de enlace de aplicación y su nombre IP/DNS asociado usando el elemento de hello PublicIPAddress.</span><span class="sxs-lookup"><span data-stu-id="64e8c-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="64e8c-246">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64e8c-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="64e8c-247"><a name="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="64e8c-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="64e8c-248">Administración de API de Azure configurado en una red virtual proporciona una interfaz de puerta de enlace único para todas las API configuradas, independientemente de si están hospedados en local o en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e8c-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="64e8c-249">Integración de puerta de enlace de aplicaciones con la API de administración proporciona la flexibilidad de Hola de habilitación selectiva determinado toobe API accesible en Internet de hello, así como proporcionar un servidor de aplicaciones Web como una instancia de administración de API de tooyour de front-end.</span><span class="sxs-lookup"><span data-stu-id="64e8c-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="64e8c-250"><a name="next-steps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64e8c-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="64e8c-251">Obtenga más información sobre Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="64e8c-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="64e8c-252">Introducción a Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="64e8c-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="64e8c-253">Firewall de aplicaciones web de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="64e8c-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="64e8c-254">Application Gateway mediante enrutamiento basado en rutas de acceso</span><span class="sxs-lookup"><span data-stu-id="64e8c-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="64e8c-255">Más información acerca de API Management y redes virtuales</span><span class="sxs-lookup"><span data-stu-id="64e8c-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="64e8c-256">Utilizando la API de administración disponibles solo en hello red virtual</span><span class="sxs-lookup"><span data-stu-id="64e8c-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="64e8c-257">Usar Azure API Management con redes virtuales</span><span class="sxs-lookup"><span data-stu-id="64e8c-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
