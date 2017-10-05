---
title: Arquitectura de seguridad por capas con entornos del Servicio de aplicaciones
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
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="f11c2-103">Implementación de una arquitectura de seguridad por capas con entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f11c2-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="f11c2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f11c2-104">Overview</span></span>
<span data-ttu-id="f11c2-105">Como los entornos del Servicio de aplicaciones proporcionan un entorno de tiempo de ejecución aislado que está implementado en una red virtual, los desarrolladores pueden crear una arquitectura de seguridad por capas que proporcione diferentes niveles de acceso a la red para cada capa de aplicación física.</span><span class="sxs-lookup"><span data-stu-id="f11c2-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="f11c2-106">Un objetivo común es ocultar los back-ends de API al acceso general desde Internet y permitir que solo las aplicaciones web ascendentes puedan llamar a las API.</span><span class="sxs-lookup"><span data-stu-id="f11c2-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="f11c2-107">Los [Grupos de seguridad de red (NSG)][NetworkSecurityGroups] pueden usarse para restringir el acceso público a aplicaciones API en subredes que contengan los entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="f11c2-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="f11c2-108">El diagrama a continuación muestra una arquitectura de ejemplo con una aplicación basada en WebAPI, implementada en un entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f11c2-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="f11c2-109">Tres instancias de aplicación web independiente, implementadas en tres entornos del Servicio de aplicaciones independientes, realizan llamadas de back-end a la misma aplicación WebAPI.</span><span class="sxs-lookup"><span data-stu-id="f11c2-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Arquitectura conceptual][ConceptualArchitecture] 

<span data-ttu-id="f11c2-111">El signo más de color verde indica que el grupo de seguridad de red en la subred que contiene "apiase" permite llamadas entrantes desde las aplicaciones web ascendentes, así como llamadas de sí mismo.</span><span class="sxs-lookup"><span data-stu-id="f11c2-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="f11c2-112">Sin embargo el mismo grupo de seguridad de red deniega explícitamente el acceso al tráfico general de entrada desde Internet.</span><span class="sxs-lookup"><span data-stu-id="f11c2-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="f11c2-113">El resto de este tema le guía por los pasos necesarios para configurar el grupo de seguridad de red en la subred que contiene "apiase".</span><span class="sxs-lookup"><span data-stu-id="f11c2-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="f11c2-114">Determinación del comportamiento de la red</span><span class="sxs-lookup"><span data-stu-id="f11c2-114">Determining the Network Behavior</span></span>
<span data-ttu-id="f11c2-115">Para saber qué reglas de seguridad de red son necesarias, tiene que determinar a qué clientes de red se les permitirá ponerse en contacto con el entorno del Servicio de aplicaciones que contiene la aplicación de API, y a qué clientes se bloqueará.</span><span class="sxs-lookup"><span data-stu-id="f11c2-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="f11c2-116">Puesto que los [Grupos de seguridad de red (NSG)][NetworkSecurityGroups] están aplicados a las subredes y los entornos de App Service están implementados en las subredes, las reglas contenidas en un NSG se aplican a **todas** las aplicaciones que se ejecutan en un entorno de App Service.</span><span class="sxs-lookup"><span data-stu-id="f11c2-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="f11c2-117">En la arquitectura de ejemplo de este artículo, una vez que un grupo de seguridad de red se aplica a la subred que contiene "apiase", todas las aplicaciones que se ejecuten en el entorno del Servicio de aplicaciones "apiase" estarán protegidas por el mismo conjunto de reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f11c2-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="f11c2-118">**Determinar la dirección IP saliente de los autores de llamadas que preceden en la cadena:** ¿cuál es la dirección o direcciones IP de los autores de llamadas que preceden en la cadena?</span><span class="sxs-lookup"><span data-stu-id="f11c2-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="f11c2-119">Se tiene que garantizar de forma explícita el acceso de estas direcciones en el NSG.</span><span class="sxs-lookup"><span data-stu-id="f11c2-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="f11c2-120">Dado que las llamadas entre los entornos del Servicio de aplicaciones se consideran llamadas de "Internet", se tiene que permitir el acceso en el NSG de la dirección IP saliente asignada a cada uno de los tres entornos del Servicio de aplicaciones ascendentes para la subred "apiase".</span><span class="sxs-lookup"><span data-stu-id="f11c2-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="f11c2-121">Para obtener más información acerca de cómo determinar la dirección IP saliente para aplicaciones que se ejecutan en un entorno de App Service, consulte el artículo de información general sobre la [arquitectura de red][NetworkArchitecture].</span><span class="sxs-lookup"><span data-stu-id="f11c2-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="f11c2-122">**¿Tiene la aplicación de API de back-end que llamarse a sí misma?**</span><span class="sxs-lookup"><span data-stu-id="f11c2-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="f11c2-123">Un punto sutil que a veces se pasa por alto es el escenario en el que la aplicación back-end tiene que llamarse a sí misma.</span><span class="sxs-lookup"><span data-stu-id="f11c2-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="f11c2-124">Si una aplicación de API de back-end en un entorno del Servicio de aplicaciones tiene que llamarse a sí misma, esta llamada se trata también como una llamada de "Internet".</span><span class="sxs-lookup"><span data-stu-id="f11c2-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="f11c2-125">En la arquitectura de ejemplo, esto requiere que se permita también el acceso desde la dirección IP saliente del entorno del Servicio de aplicaciones "apiase".</span><span class="sxs-lookup"><span data-stu-id="f11c2-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="f11c2-126">Creación del grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="f11c2-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="f11c2-127">Una vez que se conozca el conjunto de direcciones IP salientes, el siguiente paso es crear un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="f11c2-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="f11c2-128">Se pueden crear grupos de seguridad de red para las redes virtuales basadas en Resource Manager, así como para las redes virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="f11c2-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="f11c2-129">Los ejemplos siguientes muestran la creación y configuración de un grupo de seguridad de red en una red virtual clásica mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="f11c2-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="f11c2-130">Para la arquitectura del ejemplo, los entornos se encuentran en "South Central US", por lo que se crea un NSG vacío en esa región:</span><span class="sxs-lookup"><span data-stu-id="f11c2-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="f11c2-131">En primer lugar, se agrega una regla de permiso explícito para la infraestructura de administración de Azure como se indica en el artículo sobre [tráfico de entrada][InboundTraffic] para entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="f11c2-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="f11c2-132">A continuación, se agregan dos reglas para permitir las llamadas HTTP y HTTPS desde el primer entorno del Servicio de aplicaciones ascendente ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="f11c2-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="f11c2-133">Repetir para el segundo y tercer entorno del Servicio de aplicaciones ascendente ("fe2ase" y "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="f11c2-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="f11c2-134">Por último, conceder acceso a la dirección IP saliente del entorno del Servicio de aplicaciones de la API de back-end para que puede devolverse la llamada a sí misma.</span><span class="sxs-lookup"><span data-stu-id="f11c2-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="f11c2-135">No es necesario configurar ninguna otra regla de seguridad de red porque cada NSG tiene un conjunto de reglas predeterminadas que bloquean el acceso de entrada desde Internet de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f11c2-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="f11c2-136">La lista completa de las reglas en el grupo de seguridad de red se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="f11c2-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="f11c2-137">Observe cómo la última regla, que aparece resaltada, bloquea el acceso de entrada de todos los autores de llamadas que no sean aquellos a los que se concedió acceso explícitamente.</span><span class="sxs-lookup"><span data-stu-id="f11c2-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configuración NSG][NSGConfiguration] 

<span data-ttu-id="f11c2-139">El último paso es aplicar el NSG a la subred que contiene el entorno del Servicio de aplicaciones "apiase".</span><span class="sxs-lookup"><span data-stu-id="f11c2-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="f11c2-140">Con el NSG aplicado a la subred, solo los tres entornos del Servicio de aplicaciones y el entorno del Servicio de aplicaciones que contiene el back-end de API tienen permitido llamar en el entorno de "apiase".</span><span class="sxs-lookup"><span data-stu-id="f11c2-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="f11c2-141">Información y vínculos adicionales</span><span class="sxs-lookup"><span data-stu-id="f11c2-141">Additional Links and Information</span></span>
<span data-ttu-id="f11c2-142">Todos los artículos y procedimientos correspondientes a los entornos del Servicio de aplicaciones están disponibles en el archivo [Léame para entornos del Servicio de aplicaciones](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="f11c2-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="f11c2-143">Información acerca de los [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f11c2-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="f11c2-144">Descripción de las [direcciones IP saliente][NetworkArchitecture] y entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="f11c2-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="f11c2-145">[Puertos de red][InboundTraffic] usados en un entorno de App Service</span><span class="sxs-lookup"><span data-stu-id="f11c2-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
