---
title: aaaIntroduction tooApp v1 de entorno del servicio
description: "Obtenga información acerca de la característica de hello v1 de entorno del servicio de aplicaciones que proporciona unidades de escalado seguro, unirse a la red virtual dedicado para ejecutar todas las aplicaciones."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="eef97-103">Introducción tooApp v1 de entorno del servicio</span><span class="sxs-lookup"><span data-stu-id="eef97-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="eef97-104">Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="eef97-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="eef97-105">Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz.</span><span class="sxs-lookup"><span data-stu-id="eef97-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="eef97-106">toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="eef97-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="eef97-107">Información general</span><span class="sxs-lookup"><span data-stu-id="eef97-107">Overview</span></span>
<span data-ttu-id="eef97-108">Un entorno de App Service es una opción de plan de servicio [Premium][PremiumTier] de Azure App Serviceque proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service a gran escala, lo que incluye [Web Apps][WebApps], [Mobile Apps][MobileApps] y [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="eef97-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="eef97-109">Los entornos del Servicio de aplicaciones son ideales para cargas de trabajo de aplicaciones que requieren:</span><span class="sxs-lookup"><span data-stu-id="eef97-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="eef97-110">Muy grande escala</span><span class="sxs-lookup"><span data-stu-id="eef97-110">Very high scale</span></span>
* <span data-ttu-id="eef97-111">Aislamiento y acceso a redes seguro</span><span class="sxs-lookup"><span data-stu-id="eef97-111">Isolation and secure network access</span></span>

<span data-ttu-id="eef97-112">Los clientes pueden crear varios entornos del Servicio de aplicaciones en una o varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="eef97-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="eef97-113">Esto hace que sean perfectos para los niveles de aplicación sin estado de escalado horizontal en el respaldo de cargas de trabajo RPS elevadas.</span><span class="sxs-lookup"><span data-stu-id="eef97-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="eef97-114">Los entornos del servicio de aplicación son toorunning aislado sólo las aplicaciones de un único cliente y siempre se implementan en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="eef97-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="eef97-115">Los clientes tienen control más preciso sobre el tráfico de red de aplicación entrantes y salientes, y las aplicaciones pueden establecer conexiones seguras a alta velocidad sobre los recursos corporativos de redes virtuales tooon local.</span><span class="sxs-lookup"><span data-stu-id="eef97-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="eef97-116">Todos los artículos y cómo-para sobre entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="eef97-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="eef97-117">Para obtener información general del proceso de habilitar a gran escala y proteger entornos del servicio de aplicación, acceso a la red, consulte hello [AzureCon profundización] [ AzureConDeepDive] en entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="eef97-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="eef97-118">Para un análisis más profundo de ajuste de escala horizontal con varios entornos de servicio de aplicación consulte el artículo de hello acerca de cómo toosetup una [consumo de aplicaciones distribuidas geográficamente][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="eef97-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="eef97-119">toosee cómo se configuró la arquitectura de seguridad de Hola se muestra en hello AzureCon exhaustiva, consulte el artículo de hello en la implementación de un [en capas de arquitectura de seguridad](app-service-app-service-environment-layered-security.md) con entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="eef97-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="eef97-120">Las aplicaciones que se ejecutan en entornos de aplicación de servicio pueden tener su acceso validado por dispositivos de subida como firewalls de aplicación web (WAF).</span><span class="sxs-lookup"><span data-stu-id="eef97-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="eef97-121">artículo de Hello en [configurar un WAFS para entornos del servicio de aplicación](app-service-app-service-environment-web-application-firewall.md) cubre este escenario.</span><span class="sxs-lookup"><span data-stu-id="eef97-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="eef97-122">Recursos de proceso dedicados</span><span class="sxs-lookup"><span data-stu-id="eef97-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="eef97-123">Todo proceso Hola recursos en un entorno de servicio de aplicaciones están dedicados exclusivamente tooa sola suscripción, y se puede configurar un entorno de servicio de aplicaciones con los recursos de proceso toofifty (50) para su uso exclusivo por una sola aplicación.</span><span class="sxs-lookup"><span data-stu-id="eef97-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="eef97-124">Un entorno de servicio de aplicaciones se compone de un grupo de recursos de proceso de front-end, así como grupos de recursos de proceso de trabajo de uno toothree.</span><span class="sxs-lookup"><span data-stu-id="eef97-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="eef97-125">grupo de servidores front-end de Hello contiene recursos de proceso responsable de la terminación SSL como Equilibrio de carga también automática de las solicitudes de aplicación dentro de un entorno de servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="eef97-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="eef97-126">Cada grupo de trabajo contiene recursos de proceso que se asigna demasiado[planes de servicio de aplicación][AppServicePlan], que a su vez contienen una o más aplicaciones de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="eef97-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="eef97-127">Dado que puede haber los grupos de trabajo diferentes de toothree en un entorno de servicio de aplicaciones, tendrá Hola flexibilidad toochoose diferentes los recursos de proceso para cada grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eef97-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="eef97-128">Por ejemplo, esto permite toocreate grupo de un trabajo con los recursos de proceso menos eficaces para planes de servicio de aplicación diseñada para las aplicaciones de desarrollo o de prueba.</span><span class="sxs-lookup"><span data-stu-id="eef97-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="eef97-129">Un segundo (o incluso tercer) grupo de trabajo podría usar recursos de proceso más eficaces en los planes del Servicio de aplicaciones que ejecuten aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="eef97-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="eef97-130">Para obtener más detalles sobre la cantidad de Hola de front-end de toohello disponible de recursos de proceso y los grupos de trabajo, consulte [cómo tooConfigure un entorno de servicio de aplicaciones][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="eef97-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="eef97-131">Para obtener más información sobre Hola disponible calcula tamaños de recursos admitidos en un entorno de servicio de aplicaciones, consulte hello [precios del servicio de aplicación] [ AppServicePricing] página y revise Hola opciones disponibles para los entornos del servicio de aplicación en el nivel de precios de hello Premium.</span><span class="sxs-lookup"><span data-stu-id="eef97-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="eef97-132">Compatibilidad con redes virtuales</span><span class="sxs-lookup"><span data-stu-id="eef97-132">Virtual Network Support</span></span>
<span data-ttu-id="eef97-133">Puede crearse un entorno de App Service **en** una red virtual de Azure Resource Manager **o** en una del modelo de implementación clásica ([obtenga más información sobre las redes virtuales][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="eef97-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="eef97-134">Puesto que siempre existe un entorno de servicio de aplicación en una red virtual y más concretamente dentro de una subred de una red virtual, puede aprovechar las características de seguridad de redes virtuales toocontrol hello las comunicaciones de red entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="eef97-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="eef97-135">Una instancia de App Service Environment puede tener conexión a Internet con una dirección IP pública, o tener una conexión interna solo con la dirección de un equilibrador de carga interno (ILB) de Azure.</span><span class="sxs-lookup"><span data-stu-id="eef97-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="eef97-136">Puede usar [grupos de seguridad de red] [ NetworkSecurityGroups] toorestrict entrada comunicaciones toohello subred donde reside un entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="eef97-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="eef97-137">Esto le permite aplicaciones toorun detrás de servicios como firewalls de aplicación web y los proveedores de SaaS de red y dispositivos de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="eef97-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="eef97-138">Las aplicaciones también a menudo necesitan tooaccess los recursos corporativos, como servicios web y bases de datos internas.</span><span class="sxs-lookup"><span data-stu-id="eef97-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="eef97-139">Un enfoque común es toomake estos extremos toointernal solo disponible el tráfico de red que fluyen en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="eef97-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="eef97-140">Una vez que un entorno de servicio de aplicaciones se toohello combinada misma red virtual que los servicios internos hello, aplicaciones que se ejecutan en el entorno de hello puede tener acceso a ellos, incluidos los extremos accesibles a través de [sitio a sitio] [ SiteToSite]y [ExpressRoute de Azure] [ ExpressRoute] las conexiones.</span><span class="sxs-lookup"><span data-stu-id="eef97-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="eef97-141">Para obtener más detalles sobre cómo funcionan los entornos del servicio de aplicación con redes virtuales y redes locales Consulte Hola siguientes artículos [arquitectura de red][NetworkArchitectureOverview], [controlar la entrada Tráfico][ControllingInboundTraffic], y [conectarse de forma segura tooBackends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="eef97-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="eef97-142">Introducción</span><span class="sxs-lookup"><span data-stu-id="eef97-142">Getting started</span></span>
<span data-ttu-id="eef97-143">tooget iniciado con el entorno de servicio de aplicación, vea [cómo tooCreate un entorno de servicio de aplicaciones][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="eef97-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="eef97-144">Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="eef97-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="eef97-145">Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="eef97-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="eef97-146">Para obtener información general de arquitectura de red del entorno de servicio de aplicaciones de hello, vea hello [información general de la arquitectura de red] [ NetworkArchitectureOverview] artículo.</span><span class="sxs-lookup"><span data-stu-id="eef97-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="eef97-147">Para obtener más información sobre el uso de un entorno de servicio de aplicaciones con ExpressRoute, consulte Hola artículo siguiente [Express Route y entornos del servicio de aplicación][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="eef97-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


