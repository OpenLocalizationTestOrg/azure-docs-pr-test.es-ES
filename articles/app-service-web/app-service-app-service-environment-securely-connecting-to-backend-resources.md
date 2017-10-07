---
title: "aaaSecurely conexión tooBackEnd recursos desde un entorno de servicio de aplicaciones"
description: "Obtenga información sobre cómo se conectan toosecurely toobackend recursos desde un entorno de servicio de aplicaciones."
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
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="59d04-103">TooBackend de conexión segura recursos desde un entorno de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="59d04-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="59d04-104">Información general</span><span class="sxs-lookup"><span data-stu-id="59d04-104">Overview</span></span>
<span data-ttu-id="59d04-105">Puesto que siempre se crea un entorno de servicio de aplicación en **cualquier** una red virtual de Azure Resource Manager, **o** un modelo de implementación clásica [red virtual] [ virtualnetwork], las conexiones salientes desde un recursos de back-end de tooother de entorno de servicio de aplicaciones pueden fluir exclusivamente a través de la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="59d04-106">Tras el cambio reciente realizado en junio de 2016, los entornos ASE también se pueden implementar en redes virtuales que usen intervalos de direcciones públicas o espacios de direcciones de RFC1918 (es decir, direcciones privadas).</span><span class="sxs-lookup"><span data-stu-id="59d04-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="59d04-107">Por ejemplo, puede haber un servidor SQL Server que se ejecute en un clúster de máquinas virtuales con el puerto 1433 bloqueado.</span><span class="sxs-lookup"><span data-stu-id="59d04-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="59d04-108">punto de conexión de Hello puede ser encuentra tooonly permitir el acceso desde otros recursos en Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="59d04-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="59d04-109">Como otro ejemplo, extremos confidenciales pueden ejecutar de forma local y ser tooAzure conectado a través de cualquiera [sitio a sitio] [ SiteToSite] o [ExpressRoute de Azure] [ ExpressRoute] las conexiones.</span><span class="sxs-lookup"><span data-stu-id="59d04-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="59d04-110">Como resultado, sólo los recursos en redes virtuales conectado toohello sitio a sitio o ExpressRoute túneles serán puntos de conexión de tooaccess pueda local.</span><span class="sxs-lookup"><span data-stu-id="59d04-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="59d04-111">Para todos estos escenarios, aplicaciones que se ejecutan en un entorno de servicio de aplicaciones se pueda toosecurely conectará toohello varios servidores y recursos.</span><span class="sxs-lookup"><span data-stu-id="59d04-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="59d04-112">El tráfico saliente de aplicaciones que se ejecutan en los extremos del tooprivate un entorno de servicio de aplicaciones en hello misma red virtual (o conectado toohello misma red virtual), le flujo sólo a través de la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="59d04-113">Los puntos de conexión no fluirá a través de tooprivate de tráfico saliente Hola Internet pública.</span><span class="sxs-lookup"><span data-stu-id="59d04-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="59d04-114">Una advertencia aplica toooutbound tráfico de un tooendpoints de entorno de servicio de aplicaciones en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="59d04-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="59d04-115">Entornos del servicio de aplicación no pueden tener acceso a los puntos de conexión de máquinas virtuales ubicadas en hello **mismo** subred como Hola entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="59d04-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="59d04-116">Normalmente no debe ser un problema como entornos del servicio de aplicación se implementan en una subred reservada para uso exclusivo por hello solo entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="59d04-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="59d04-117">Requisitos de DNS y conectividad saliente</span><span class="sxs-lookup"><span data-stu-id="59d04-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="59d04-118">Para un entorno de servicio de aplicaciones toofunction correctamente, requiere acceso de salida toovarious extremos.</span><span class="sxs-lookup"><span data-stu-id="59d04-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="59d04-119">Una lista completa de extremos externos Hola utilizado por un ASE está en la sección "Requiere conectividad de red" de Hola Hola [configuración de red para ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artículo.</span><span class="sxs-lookup"><span data-stu-id="59d04-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="59d04-120">Los entornos del servicio de aplicación requieren una infraestructura DNS válida configurada para la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="59d04-121">Si para cualquier hello motivo se cambia la configuración de DNS después de crear un entorno de servicio de aplicaciones, los desarrolladores pueden forzar una toopick entono la nueva configuración de DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="59d04-122">Desencadenar un reinicio de entorno gradual utilizando Hola "Reinicio" icono situado en parte superior de Hola de hello entono hoja de administración en el portal de hello provocará Hola entorno toopick la configuración de DNS nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="59d04-123">También se recomienda que los servidores DNS personalizados en red virtual de hello sea el programa de instalación antes de tiempo anterior toocreating un entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="59d04-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="59d04-124">Si se cambia la configuración de DNS de una red virtual mientras se crea un entorno de servicio de aplicaciones, que producirá errores de proceso de creación de hello entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="59d04-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="59d04-125">En un modo similar, si existe un servidor DNS personalizado en hello otro extremo de una puerta de enlace VPN y el servidor DNS de hello es inaccesible o no está disponible, hello también se producirá un error del proceso de creación del entorno del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="59d04-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="59d04-126">Conexión tooa SQL Server</span><span class="sxs-lookup"><span data-stu-id="59d04-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="59d04-127">Una configuración común de SQL Server tiene un extremo que escucha en el puerto 1433:</span><span class="sxs-lookup"><span data-stu-id="59d04-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Extremo de SQL Server][SqlServerEndpoint]

<span data-ttu-id="59d04-129">Existen dos enfoques para restringir el punto de conexión de toothis de tráfico:</span><span class="sxs-lookup"><span data-stu-id="59d04-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="59d04-130">[Listas de control de acceso de red][NetworkAccessControlLists] (ACL de red)</span><span class="sxs-lookup"><span data-stu-id="59d04-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="59d04-131">[Grupos de seguridad de red][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="59d04-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="59d04-132">Restricción del acceso con una lista de control de acceso de red</span><span class="sxs-lookup"><span data-stu-id="59d04-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="59d04-133">El puerto 1433 se puede proteger mediante una lista de control de acceso de red.</span><span class="sxs-lookup"><span data-stu-id="59d04-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="59d04-134">ejemplo de Hola siguiente cliente listas blancas las direcciones que se origina desde dentro de una red virtual y bloquea el acceso tooall otros clientes.</span><span class="sxs-lookup"><span data-stu-id="59d04-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Ejemplo de lista de control de acceso de red][NetworkAccessControlListExample]

<span data-ttu-id="59d04-136">Las aplicaciones que se ejecutan en el entorno de servicio de aplicación en Hola misma red virtual como Hola SQL Server será tooconnect capaz de instancia de SQL Server toohello con hello **red virtual interna** dirección IP para la máquina virtual de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="59d04-137">cadena de conexión de ejemplo de Hola a continuación referencias Hola SQL Server mediante su dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="59d04-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="59d04-138">Aunque la máquina virtual de hello tiene también un punto de conexión público, los intentos de conexión con la dirección IP pública Hola se rechazarán debido a ACL de red Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="59d04-139">Restricción del acceso con un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="59d04-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="59d04-140">Un enfoque alternativo para proteger el acceso consiste en usar un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="59d04-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="59d04-141">Grupos de seguridad de red pueden ser tooindividual aplicado las máquinas virtuales o subred tooa que contienen máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="59d04-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="59d04-142">En primer lugar un grupo de seguridad de red necesita toobe creado:</span><span class="sxs-lookup"><span data-stu-id="59d04-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="59d04-143">Restringir el acceso tooonly tráfico de red virtual interno es muy simple con un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="59d04-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="59d04-144">las reglas predeterminadas de Hello en un grupo de seguridad de red sólo permiten el acceso desde otros clientes de red en hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="59d04-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="59d04-145">Como resultado bloquear el acceso tooSQL Server es tan sencillo como aplicación de un grupo de seguridad de red con sus valor predeterminado reglas tooeither Hola máquinas virtuales que ejecutan SQL Server o la subred de Hola que contienen máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="59d04-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="59d04-146">ejemplo de Hola siguiente aplica una seguridad grupo toohello contenedor subred:</span><span class="sxs-lookup"><span data-stu-id="59d04-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="59d04-147">resultado de Hello final es un conjunto de reglas de seguridad que bloquean el acceso externo, al permitir el acceso de red virtual interna:</span><span class="sxs-lookup"><span data-stu-id="59d04-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Reglas de seguridad de red predeterminadas][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="59d04-149">Introducción</span><span class="sxs-lookup"><span data-stu-id="59d04-149">Getting started</span></span>
<span data-ttu-id="59d04-150">Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="59d04-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="59d04-151">tooget iniciado con el entorno de servicio de aplicación, consulte [Introducción tooApp entorno del servicio][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="59d04-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="59d04-152">Para obtener detalles alrededor de controlar el tráfico entrante tooyour entorno del servicio de aplicaciones, consulte [controlar el tráfico entrante tooan entorno del servicio de aplicaciones][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="59d04-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="59d04-153">Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="59d04-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
