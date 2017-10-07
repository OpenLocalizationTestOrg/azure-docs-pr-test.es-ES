---
title: "aaaHow toouse administración de API de Azure con red virtual interna | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosetup y configurar la administración de API de Azure en red virtual interna."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="7c9a9-103">Uso de Azure API Management con una red virtual interna</span><span class="sxs-lookup"><span data-stu-id="7c9a9-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="7c9a9-104">Con redes virtuales de Azure (redes virtuales), administración de API puede administrar las API no es accesible en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="7c9a9-105">Una serie de tecnologías VPN es conexiones de hello toomake disponibles y administración de API se pueden implementar en dos modos principales dentro de hello red virtual:</span><span class="sxs-lookup"><span data-stu-id="7c9a9-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="7c9a9-106">Externo</span><span class="sxs-lookup"><span data-stu-id="7c9a9-106">External</span></span>
* <span data-ttu-id="7c9a9-107">Interno</span><span class="sxs-lookup"><span data-stu-id="7c9a9-107">Internal</span></span>

## <span data-ttu-id="7c9a9-108"><a name="overview"></a>Información general</span><span class="sxs-lookup"><span data-stu-id="7c9a9-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="7c9a9-109">Cuando se implementa la API de administración en un modo de red Virtual interna, solo son visibles dentro de una red Virtual que controlan el acceso a todos los extremos de servicio de hello (puerta de enlace, portal para desarrolladores, portal para desarrolladores, la administración directa y Git).</span><span class="sxs-lookup"><span data-stu-id="7c9a9-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="7c9a9-110">Ninguno de los extremos de servicio de Hola se registran en hello servidor DNS público.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="7c9a9-111">Usar administración de API en modo interno, puede lograr Hola los escenarios siguientes</span><span class="sxs-lookup"><span data-stu-id="7c9a9-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="7c9a9-112">Hacer que las API se hospeden de manera segura en su centro de datos privado accesible por terceros que estén fuera de él por medio de conexiones de sitio a sitio o VPN de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="7c9a9-113">Habilitar escenarios de nube híbrida mediante la exposición de las API basadas en la nube y las API locales a través de una puerta de enlace común.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="7c9a9-114">Administrar las API hospedadas en diversas ubicaciones geográficas mediante un único punto de conexión de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="7c9a9-115"><a name="enable-vpn"></a>Creación de API Management en una red virtual interna</span><span class="sxs-lookup"><span data-stu-id="7c9a9-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="7c9a9-116">servicio de administración de API de red Virtual interna de Hola se hospeda detrás de un Balancer(ILB) de carga interno.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="7c9a9-117">Hola dirección IP de hello ILB está en hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) intervalo.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="7c9a9-118">Habilitación de la conexión de red virtual mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7c9a9-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="7c9a9-119">En primer lugar crear servicio de administración de API de hello, siga los pasos de hello [servicio de administración de API crear][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="7c9a9-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="7c9a9-120">A continuación, configurar Administración de API toobe implementado dentro de una red Virtual.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menú para configurar API Management en una red virtual interna][api-management-using-internal-vnet-menu]

<span data-ttu-id="7c9a9-122">Después de implementación de Hola se realiza correctamente, debería ver Hola dirección IP Virtual interna de su servicio en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![Panel de API Management con red virtual interna configurada][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="7c9a9-124">Habilitación de una conexión de VNET con cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c9a9-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="7c9a9-125">También puede habilitar la conectividad de red virtual con los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="7c9a9-126">**Crear un servicio de administración de API dentro de una red virtual**: usar el cmdlet de hello [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate una administración de API de Azure del servicio dentro de una red virtual y configurar tipo de red virtual interna de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="7c9a9-127">**Implementar un servicio de administración de API existente dentro de una red virtual**: usar el cmdlet de hello [AzureRmApiManagementDeployment actualización](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove una administración de API de Azure de servicio dentro de una red Virtual y configurar toouse Tipo de red virtual interna.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="7c9a9-128"><a name="apim-dns-configuration"></a>Configuración de DNS</span><span class="sxs-lookup"><span data-stu-id="7c9a9-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="7c9a9-129">Cuando se usa API Management en el modo de red virtual externa, DNS está administrado por Azure.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="7c9a9-130">Para el modo de red Virtual interna, tener toomanage su propio DNS.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="7c9a9-131">Servicio de administración de API no escucha toorequests proveniente de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="7c9a9-132">Sólo responde toorequests toohello nombre de host configurado en sus puntos de conexión de servicio (que incluye puerta de enlace, portal para desarrolladores, publisher Portal, punto de conexión de administración directa y git).</span><span class="sxs-lookup"><span data-stu-id="7c9a9-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="7c9a9-133">Acceso en nombres de host predeterminados:</span><span class="sxs-lookup"><span data-stu-id="7c9a9-133">Access on default host names:</span></span>
<span data-ttu-id="7c9a9-134">Cuando se crea un servicio de administración de API en la nube pública de Azure, denominado "contoso" por ejemplo, hello siguientes extremos de servicio se configuran de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="7c9a9-135">Puerta de enlace o proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="7c9a9-136">Portal para desarrolladores y portal para editores: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="7c9a9-137">Punto de conexión de administración directa: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="7c9a9-138">GIT: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="7c9a9-139">tooaccess estos puntos de conexión de servicio de administración de API, puede crear una máquina Virtual en una red de subred conectada toohello Virtual en el que se implementa la API de administración.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="7c9a9-140">Suponiendo que Hola dirección IP Virtual interna para el servicio 10.0.0.5, puede hacer Hola asignación del archivo de hosts (% SystemDrive%\drivers\etc\hosts) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="7c9a9-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="7c9a9-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="7c9a9-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="7c9a9-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="7c9a9-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7c9a9-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="7c9a9-145">A continuación, puede tener acceso a todos los extremos de servicio de Hola de hello Máquina Virtual que creó.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="7c9a9-146">Si utiliza un servidor DNS personalizado en una red virtual, también puede crear registros D de DNS y tener acceso a estos puntos de conexión desde cualquier lugar de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="7c9a9-147">Acceso en nombres de dominio personalizado:</span><span class="sxs-lookup"><span data-stu-id="7c9a9-147">Access on custom domain names:</span></span>
<span data-ttu-id="7c9a9-148">Si no desea hello tooaccess servicio de administración de API con nombres de host de hello predeterminado, puede configurar los nombres de dominio personalizados para todos los extremos de servicio como a continuación</span><span class="sxs-lookup"><span data-stu-id="7c9a9-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configuración de dominio personalizado para API Management][api-management-custom-domain-name]

<span data-ttu-id="7c9a9-150">A continuación, puede crear registros en el servidor DNS tooaccess estos puntos de conexión que solo son accesibles desde dentro de la red Virtual.</span><span class="sxs-lookup"><span data-stu-id="7c9a9-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="7c9a9-151"><a name="related-content"></a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="7c9a9-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="7c9a9-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues] (Problemas comunes de configuración de red al configurar API Management en la red virtual)</span><span class="sxs-lookup"><span data-stu-id="7c9a9-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="7c9a9-153">P+F de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="7c9a9-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* <span data-ttu-id="7c9a9-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx) (Creación de registro D en DNS)</span><span class="sxs-lookup"><span data-stu-id="7c9a9-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span></span>

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
