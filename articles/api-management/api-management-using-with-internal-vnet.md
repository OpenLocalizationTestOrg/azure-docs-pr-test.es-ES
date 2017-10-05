---
title: Uso de API Management con red virtual interna | Microsoft Docs
description: "Obtenga información acerca de cómo instalar y configurar Azure API Management en una red virtual interna."
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
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="5b8bf-103">Uso de Azure API Management con una red virtual interna</span><span class="sxs-lookup"><span data-stu-id="5b8bf-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="5b8bf-104">Con redes virtuales de Azure (VNET), API Management puede administrar las API no accesibles en Internet.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="5b8bf-105">Hay varias tecnologías VPN disponibles para realizar la conexión, y API Management se puede implementar en dos modos principales dentro de la red virtual:</span><span class="sxs-lookup"><span data-stu-id="5b8bf-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="5b8bf-106">Externo</span><span class="sxs-lookup"><span data-stu-id="5b8bf-106">External</span></span>
* <span data-ttu-id="5b8bf-107">Interno</span><span class="sxs-lookup"><span data-stu-id="5b8bf-107">Internal</span></span>

## <span data-ttu-id="5b8bf-108"><a name="overview"> </a>Información general</span><span class="sxs-lookup"><span data-stu-id="5b8bf-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="5b8bf-109">Cuando se implementa API Management en un modo de red virtual interna, todos los puntos de conexión de servicio (puerta de enlace, portal para desarrolladores, portal para editores, administración directa y GIT) solo están visibles dentro de una red virtual a la que controla el acceso.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="5b8bf-110">Ninguno de los puntos de conexión de servicio se registra en el servidor DNS público.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="5b8bf-111">Al usar API Management en modo interno, puede conseguir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b8bf-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="5b8bf-112">Hacer que las API se hospeden de manera segura en su centro de datos privado accesible por terceros que estén fuera de él por medio de conexiones de sitio a sitio o VPN de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="5b8bf-113">Habilitar escenarios de nube híbrida mediante la exposición de las API basadas en la nube y las API locales a través de una puerta de enlace común.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="5b8bf-114">Administrar las API hospedadas en diversas ubicaciones geográficas mediante un único punto de conexión de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="5b8bf-115"><a name="enable-vpn"> </a>Creación de API Management en una red virtual interna</span><span class="sxs-lookup"><span data-stu-id="5b8bf-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="5b8bf-116">El servicio API Management en red virtual interna se hospeda detrás de un equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="5b8bf-117">La dirección IP del equilibrador de carga está en el intervalo [RFC1918](http://www.faqs.org/rfcs/rfc1918.html).</span><span class="sxs-lookup"><span data-stu-id="5b8bf-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="5b8bf-118">Habilitación de la conexión de red virtual mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b8bf-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="5b8bf-119">Primero cree el servicio API Management siguiendo los pasos de [Creación de una instancia de API Management][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="5b8bf-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="5b8bf-120">A continuación, configure API Management para que se implemente dentro de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menú para configurar API Management en una red virtual interna][api-management-using-internal-vnet-menu]

<span data-ttu-id="5b8bf-122">Una vez finalizada correctamente la implementación, debería ver la dirección IP virtual interna de su servicio en el panel.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![Panel de API Management con red virtual interna configurada][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="5b8bf-124">Habilitación de una conexión de VNET con cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b8bf-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="5b8bf-125">También puede habilitar la conectividad de VNET con los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="5b8bf-126">**Crear un servicio de API Management dentro de una red virtual**: use el cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) para crear un servicio de Azure API Management dentro de una VNET y configurarlo para usar el tipo de VNET interno.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="5b8bf-127"><seg>
  **Implementar un servicio existente de API Management dentro de una VNET**: use el cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) para mover un servicio existente de Azure API Management dentro de una red virtual y configurarlo para usar el tipo de VNET interno..</seg></span><span class="sxs-lookup"><span data-stu-id="5b8bf-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="5b8bf-128"><a name="apim-dns-configuration"></a>Configuración de DNS</span><span class="sxs-lookup"><span data-stu-id="5b8bf-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="5b8bf-129">Cuando se usa API Management en el modo de red virtual externa, DNS está administrado por Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="5b8bf-130">Para el modo de red virtual interna, tiene que administrar su propio DNS.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="5b8bf-131">El servicio API Management no escucha las solicitudes que llegan en direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="5b8bf-132">Solo responde a las solicitudes para el nombre de host configurado en sus puntos de conexión de servicio (entre los que están la puerta de enlace, el portal para desarrolladores, el portal para editores, el punto de conexión de administración directa y GIT).</span><span class="sxs-lookup"><span data-stu-id="5b8bf-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="5b8bf-133">Acceso en nombres de host predeterminados:</span><span class="sxs-lookup"><span data-stu-id="5b8bf-133">Access on default host names:</span></span>
<span data-ttu-id="5b8bf-134">Cuando se crea un servicio de API Management en la nube pública de Azure, denominada por ejemplo "contoso", los siguientes punto de conexión de servicio se configuran de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="5b8bf-135">Puerta de enlace o proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="5b8bf-136">Portal para desarrolladores y portal para editores: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="5b8bf-137">Punto de conexión de administración directa: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="5b8bf-138">GIT: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="5b8bf-139">Para obtener acceso a estos puntos de conexión de servicio de API Management, puede crear una máquina virtual en una subred conectada a la red virtual en el que se implementa API Management.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="5b8bf-140">Suponiendo que la dirección IP virtual interna para el servicio sea 10.0.0.5, puede realizar la asignación de archivos de host (%SystemDrive%\drivers\etc\hosts) del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b8bf-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="5b8bf-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="5b8bf-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="5b8bf-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="5b8bf-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5b8bf-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="5b8bf-145">Así podrá tener acceso a todos los puntos de conexión de servicio de la máquina virtual que creó.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="5b8bf-146">Si utiliza un servidor DNS personalizado en una red virtual, también puede crear registros D de DNS y tener acceso a estos puntos de conexión desde cualquier lugar de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="5b8bf-147">Acceso en nombres de dominio personalizado:</span><span class="sxs-lookup"><span data-stu-id="5b8bf-147">Access on custom domain names:</span></span>
<span data-ttu-id="5b8bf-148">Si no desea tener acceso al servicio API Management con los nombres de host predeterminados, puede configurar los nombres de dominio personalizados para todos los puntos de conexión de servicio del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b8bf-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configuración de dominio personalizado para API Management][api-management-custom-domain-name]

<span data-ttu-id="5b8bf-150">A continuación, puede crear registros D en el servidor DNS para tener acceso a estos puntos de conexión que solo son accesibles desde dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="5b8bf-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="5b8bf-151"><a name="related-content"> </a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="5b8bf-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="5b8bf-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues] (Problemas comunes de configuración de red al configurar API Management en la red virtual)</span><span class="sxs-lookup"><span data-stu-id="5b8bf-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="5b8bf-153">P+F de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="5b8bf-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* <span data-ttu-id="5b8bf-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx) (Creación de registro D en DNS)</span><span class="sxs-lookup"><span data-stu-id="5b8bf-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span></span>

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
