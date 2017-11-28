---
title: "aaaLayered arquitectura de seguridad con el entorno de servicio de aplicación"
description: "Implementación de una arquitectura de seguridad por capas con entornos del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="c4d72-103">Implementación de una arquitectura de seguridad por capas con entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c4d72-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="c4d72-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c4d72-104">Overview</span></span>
<span data-ttu-id="c4d72-105">Como los entornos del Servicio de aplicaciones proporcionan un entorno de tiempo de ejecución aislado que está implementado en una red virtual, los desarrolladores pueden crear una arquitectura de seguridad por capas que proporcione diferentes niveles de acceso a la red para cada capa de aplicación física.</span><span class="sxs-lookup"><span data-stu-id="c4d72-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="c4d72-106">Un deseo común es toohide API back-end de acceso general a Internet y solo se permiten toobe API llama a las aplicaciones web de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="c4d72-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="c4d72-107">[Grupos de seguridad (NSG) de red] [ NetworkSecurityGroups] puede utilizarse en las subredes que contiene aplicaciones de tooAPI de acceso público de toorestrict entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4d72-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="c4d72-108">diagrama de Hello siguiente muestra una arquitectura de ejemplo con una aplicación de WebAPI según implementada en un entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c4d72-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="c4d72-109">Tres instancias de aplicación web independiente, implementadas en tres entornos de servicio de aplicación independientes, realizar llamadas de back-end toohello misma aplicación WebAPI.</span><span class="sxs-lookup"><span data-stu-id="c4d72-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Arquitectura conceptual][ConceptualArchitecture] 

<span data-ttu-id="c4d72-111">Hello verde signos de más indicar ese Hola grupo de seguridad de red en la subred de Hola que contiene "apiase" permite llamadas entrantes de hello las aplicaciones web de nivel superior, como bien llamadas de sí misma.</span><span class="sxs-lookup"><span data-stu-id="c4d72-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="c4d72-112">Sin embargo, Hola deniega explícitamente el mismo grupo de seguridad de red acceder a toogeneral el tráfico entrante desde Internet Hola.</span><span class="sxs-lookup"><span data-stu-id="c4d72-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="c4d72-113">resto de Hola de este tema le guía a través del grupo de seguridad de red de Hola Hola pasos tooconfigure necesarios de subred de Hola que contiene "apiase".</span><span class="sxs-lookup"><span data-stu-id="c4d72-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="c4d72-114">Determinar Hola comportamiento de la red</span><span class="sxs-lookup"><span data-stu-id="c4d72-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="c4d72-115">En orden tooknow la seguridad de la red son necesarias las reglas, debe toodetermine se permitirá que los clientes de red aplicación tooreach Hola entono contenedor hello API y qué clientes se bloquearán.</span><span class="sxs-lookup"><span data-stu-id="c4d72-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="c4d72-116">Puesto que [grupos de seguridad (NSG) de red] [ NetworkSecurityGroups] son toosubnets aplicado, y entornos del servicio de aplicación se implementan en subredes, Hola contenidas en un NSG se aplican reglas demasiado**todos los** aplicaciones que se ejecutan en un entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c4d72-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="c4d72-117">Mediante la arquitectura de ejemplo de Hola para este artículo, una vez que un grupo de seguridad de red se subred toohello aplicados que contiene "apiase", todas las aplicaciones que se ejecutan en hello "apiase" entorno del servicio de aplicación se protegerán Hola mismo conjunto de reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c4d72-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="c4d72-118">**Determinar la dirección IP saliente Hola de llamadores de nivel superior:** ¿qué es Hola dirección o direcciones IP de los llamadores de nivel superior de hello?</span><span class="sxs-lookup"><span data-stu-id="c4d72-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="c4d72-119">Estas direcciones deberá toobe permitidos explícitamente acceso en hello NSG.</span><span class="sxs-lookup"><span data-stu-id="c4d72-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="c4d72-120">Dado que las llamadas entre entornos del servicio de aplicación se consideran llamadas "Internet", esto significa Hola salida IP dirección asignada tooeach de hello tres ascendente entornos del servicio de aplicación necesidades toobe puede tener acceso en hello NSG para la subred de "apiase" Hola.</span><span class="sxs-lookup"><span data-stu-id="c4d72-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="c4d72-121">Para obtener más información acerca de cómo determinar la dirección IP de la salida Hola para aplicaciones que se ejecutan en un entorno de servicio de aplicaciones, consulte hello [arquitectura de red] [ NetworkArchitecture] artículo de información general.</span><span class="sxs-lookup"><span data-stu-id="c4d72-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="c4d72-122">**¿Será necesario aplicaciones de API de back-end de hello toocall propio?**</span><span class="sxs-lookup"><span data-stu-id="c4d72-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="c4d72-123">Un punto en ocasiones, se pasa por alto y sutil es escenario Hola donde la aplicación de back-end de hello necesita toocall propio.</span><span class="sxs-lookup"><span data-stu-id="c4d72-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="c4d72-124">Si una aplicación de API de back-end en un entorno de servicio de aplicaciones necesita toocall propio, también se trata como una llamada de "Internet".</span><span class="sxs-lookup"><span data-stu-id="c4d72-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="c4d72-125">En la arquitectura de ejemplo de Hola Esto requiere que permite el acceso de la dirección IP saliente Hola Hola "apiase" entono así.</span><span class="sxs-lookup"><span data-stu-id="c4d72-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="c4d72-126">Configuración de grupo de seguridad de red de Hola</span><span class="sxs-lookup"><span data-stu-id="c4d72-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="c4d72-127">Una vez Hola conjunto de direcciones IP salientes se conocen, Hola siguiente paso es tooconstruct un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c4d72-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="c4d72-128">Se pueden crear grupos de seguridad de red para las redes virtuales basadas en Resource Manager, así como para las redes virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="c4d72-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="c4d72-129">ejemplos de Hello siguientes muestran la creación y configuración de un NSG en una red virtual clásica mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="c4d72-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="c4d72-130">De arquitectura de ejemplo de Hola, entornos de Hola se encuentran en el Ee.uu. Central sur, por lo que se crea un NSG vacío en dicha región:</span><span class="sxs-lookup"><span data-stu-id="c4d72-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="c4d72-131">En primer lugar explícito Permitir que se agrega la regla para la infraestructura de administración de Azure de hello como se indica en el artículo de hello en [el tráfico entrante] [ InboundTraffic] para entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4d72-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="c4d72-132">A continuación, dos reglas se agregan tooallow HTTP y HTTPS llamadas de Hola primer entorno del servicio de aplicación de nivel superior ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="c4d72-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="c4d72-133">Enjuagar y repita la operación para Hola segunda y tercera ascendente aplicación entornos del servicio ("fe2ase" y "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="c4d72-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="c4d72-134">Por último, conceder acceso toohello saliente dirección IP del entorno de servicio de aplicaciones de la API de back-end de Hola de manera que puede devolver la llamada a sí misma.</span><span class="sxs-lookup"><span data-stu-id="c4d72-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="c4d72-135">Ninguna otra regla de seguridad de red necesita toobe configurado porque cada NSG tiene un conjunto de reglas predeterminadas que bloqueen el acceso entrante de hello Internet de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c4d72-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="c4d72-136">lista completa de Hola de reglas en el grupo de seguridad de red de Hola se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="c4d72-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="c4d72-137">Tenga en cuenta cómo regla última hello, que está resaltado, bloquea el acceso entrante desde todos los llamadores distintos de los que ha concedido acceso explícitamente.</span><span class="sxs-lookup"><span data-stu-id="c4d72-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configuración NSG][NSGConfiguration] 

<span data-ttu-id="c4d72-139">Hola último paso es tooapply hello NSG toohello máscara de subred que contiene Hola "apiase" entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c4d72-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="c4d72-140">Con hello NSG aplica toohello subred, sólo hello tres entornos del servicio de aplicación de nivel superior y Hola Hola de contenedor de entorno del servicio de aplicaciones back-end de API, se permiten toocall en entorno de "apiase" Hola.</span><span class="sxs-lookup"><span data-stu-id="c4d72-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="c4d72-141">Información y vínculos adicionales</span><span class="sxs-lookup"><span data-stu-id="c4d72-141">Additional Links and Information</span></span>
<span data-ttu-id="c4d72-142">Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="c4d72-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="c4d72-143">Información acerca de los [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c4d72-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="c4d72-144">Descripción de las [direcciones IP saliente][NetworkArchitecture] y entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="c4d72-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="c4d72-145">[Puertos de red][InboundTraffic] usados en un entorno de App Service</span><span class="sxs-lookup"><span data-stu-id="c4d72-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
