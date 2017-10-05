---
title: "Conexión segura a los recursos de back-end desde un entorno del Servicio de aplicaciones"
description: "Obtenga información acerca de cómo conectarse de forma segura a los recursos de back-end desde un entorno del Servicio de aplicaciones."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="ae8c4-103">Conexión segura a los recursos de back-end desde un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ae8c4-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="ae8c4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ae8c4-104">Overview</span></span>
<span data-ttu-id="ae8c4-105">Dado que siempre se crea un entorno de App Service **en** una red virtual de Azure Resource Manager **o** en [una][virtualnetwork] del modelo de implementación clásica, las conexiones salientes de dicho entorno a otros recursos de back-end solo pueden fluir a través de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="ae8c4-106">Tras el cambio reciente realizado en junio de 2016, los ASE también se pueden implementar en redes virtuales que usen intervalos de direcciones públicas o espacios de direcciones de RFC1918 (es decir,</span><span class="sxs-lookup"><span data-stu-id="ae8c4-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="ae8c4-107">direcciones privadas).</span><span class="sxs-lookup"><span data-stu-id="ae8c4-107">private addresses).</span></span>  

<span data-ttu-id="ae8c4-108">Por ejemplo, puede haber un servidor SQL Server que se ejecute en un clúster de máquinas virtuales con el puerto 1433 bloqueado.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="ae8c4-109">En el extremo puede incluirse una lista de control de acceso para permitir únicamente el acceso de otros recursos de la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="ae8c4-110">Otro ejemplo: los puntos de conexión con información confidencial pueden ejecutarse localmente y conectarse a Azure mediante conexiones [De sitio a sitio][SiteToSite] o [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="ae8c4-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="ae8c4-111">Como resultado, solo los recursos de las redes virtuales conectadas a túneles ExpressRoute o De sitio a sitio podrán tener acceso a los extremos locales.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="ae8c4-112">En todos estos escenarios, las aplicaciones que se ejecutan en un entorno del Servicio de aplicaciones podrán conectarse de forma segura a los distintos servidores y recursos.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="ae8c4-113">El tráfico saliente de las aplicaciones que se ejecutan en un entorno del Servicio de aplicaciones hacia extremos privados de la misma red virtual (o conectadas a la misma red virtual) solamente fluirá a través de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="ae8c4-114">El tráfico saliente hacia extremos privados no fluirá a través de la red pública de Internet.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="ae8c4-115">Existe una excepción en cuanto al tráfico saliente desde un Entorno del Servicio de aplicaciones hacia los puntos de conexión de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="ae8c4-116">Los Entornos del Servicio de aplicaciones no pueden acceder a los puntos de conexión de máquinas virtuales ubicadas en la **misma** subred que el Entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="ae8c4-117">Normalmente, esto no debería causar ningún problema siempre y cuando el Entorno del Servicio de aplicaciones se implemente en una subred reservada para uso exclusivo del mismo.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="ae8c4-118">Requisitos de DNS y conectividad saliente</span><span class="sxs-lookup"><span data-stu-id="ae8c4-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="ae8c4-119">Para que un Entorno del Servicio de aplicaciones funcione correctamente, necesita acceso de salida a varios puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="ae8c4-120">Una lista completa de los puntos de conexión externos utilizados por un ASE en la sección "Conectividad de red necesaria" del artículo [Detalles de configuración de red para entornos del Servicio de aplicaciones con ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="ae8c4-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="ae8c4-121">Los Entornos del Servicio de aplicaciones requieren una infraestructura DNS válida configurada para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="ae8c4-122">Si por algún motivo se cambia la configuración de DNS después de haber creado un entorno del Servicio de aplicaciones, los desarrolladores pueden forzar a un entorno del Servicio de aplicaciones para recoger la nueva configuración de DNS.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="ae8c4-123">Si se desencadena un reinicio gradual del entorno mediante el icono de Reiniciar, ubicado en la parte superior de la hoja de administración del entorno del Servicio de aplicaciones en el portal, el entorno recogerá la nueva configuración de DNS.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="ae8c4-124">También se recomienda configurar de antemano los servidores DNS personalizados de la red virtual antes de crear un entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="ae8c4-125">Si se cambia la configuración de DNS de una red virtual al crear un entorno del Servicio de aplicaciones, se generará un error en el proceso de creación de dicho entorno.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="ae8c4-126">De manera similar, si existe un servidor DNS personalizado en el otro extremo de una puerta de enlace de VPN y el servidor DNS es inaccesible o no está disponible, el proceso de creación del entorno de servicio de aplicaciones también producirá un error.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="ae8c4-127">Conexión a un servidor SQL Server</span><span class="sxs-lookup"><span data-stu-id="ae8c4-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="ae8c4-128">Una configuración común de SQL Server tiene un extremo que escucha en el puerto 1433:</span><span class="sxs-lookup"><span data-stu-id="ae8c4-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Extremo de SQL Server][SqlServerEndpoint]

<span data-ttu-id="ae8c4-130">Existen dos formas de restringir el tráfico a este extremo:</span><span class="sxs-lookup"><span data-stu-id="ae8c4-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="ae8c4-131">[Listas de control de acceso de red][NetworkAccessControlLists] (ACL de red)</span><span class="sxs-lookup"><span data-stu-id="ae8c4-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="ae8c4-132">[Grupos de seguridad de red][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="ae8c4-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="ae8c4-133">Restricción del acceso con una lista de control de acceso de red</span><span class="sxs-lookup"><span data-stu-id="ae8c4-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="ae8c4-134">El puerto 1433 se puede proteger mediante una lista de control de acceso de red.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="ae8c4-135">En el ejemplo siguiente se incluyen en una lista blanca las direcciones de cliente que proceden de una red virtual concreta y se bloquea el acceso al resto de clientes.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Ejemplo de lista de control de acceso de red][NetworkAccessControlListExample]

<span data-ttu-id="ae8c4-137">Todas las aplicaciones que se ejecuten en el entorno del Servicio de aplicaciones en la misma red virtual que el servidor SQL Server pueden conectarse a la instancia de SQL Server mediante la dirección IP **interna de la red virtual** para la máquina virtual SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="ae8c4-138">La cadena de conexión de ejemplo siguiente hace referencia a SQL Server mediante su dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="ae8c4-139">Aunque la máquina virtual tiene también un extremo público, los intentos de conexión mediante la dirección IP pública se rechazarán debido a la lista de control de acceso de red.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="ae8c4-140">Restricción del acceso con un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="ae8c4-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="ae8c4-141">Un enfoque alternativo para proteger el acceso consiste en usar un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="ae8c4-142">Los grupos de seguridad de red pueden aplicarse a máquinas virtuales individuales o a una subred que contenga máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="ae8c4-143">En primer lugar, es necesario crear un grupo de seguridad de red:</span><span class="sxs-lookup"><span data-stu-id="ae8c4-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="ae8c4-144">Restringir el acceso exclusivamente al tráfico interno de la red virtual es muy sencillo con un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="ae8c4-145">Las reglas predeterminadas de un grupo de este tipo solo permiten el acceso de otros clientes de la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="ae8c4-146">Como resultado, bloquear el acceso a SQL Server es tan sencillo como aplicar un grupo de seguridad de red con sus reglas predeterminadas a las máquinas virtuales que ejecutan SQL Server o a la subred que contiene las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ae8c4-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="ae8c4-147">En el ejemplo siguiente se aplica un grupo de seguridad de red a la subred contenedora:</span><span class="sxs-lookup"><span data-stu-id="ae8c4-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="ae8c4-148">El resultado final es un conjunto de reglas de seguridad que bloquean el acceso externo y permiten el acceso interno de la red virtual:</span><span class="sxs-lookup"><span data-stu-id="ae8c4-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Reglas de seguridad de red predeterminadas][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="ae8c4-150">Introducción</span><span class="sxs-lookup"><span data-stu-id="ae8c4-150">Getting started</span></span>
<span data-ttu-id="ae8c4-151">Todos los artículos y procedimientos para los entornos del Servicio de aplicaciones están disponibles en el archivo [Léame para entornos del Servicio de aplicaciones](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="ae8c4-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="ae8c4-152">Para empezar a trabajar con los entornos de App Service, consulte [Introducción al entorno de App Service][IntroToAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="ae8c4-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="ae8c4-153">Para obtener más detalles sobre cómo controlar el tráfico entrante en el entorno de App Service, vea el artículo sobre el [control del tráfico entrante en un entorno de App Service][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="ae8c4-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="ae8c4-154">Para obtener más información sobre la plataforma Azure App Service, consulte [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="ae8c4-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
