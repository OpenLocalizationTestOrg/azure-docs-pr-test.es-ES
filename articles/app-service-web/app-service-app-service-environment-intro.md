---
title: "Introducción a App Service Environment v1"
description: "Aprenda sobre la característica App Service Environment v1 que proporciona unidades de escala dedicadas, seguras y en redes virtuales para ejecutar todas las aplicaciones."
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
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="d460f-103">Introducción a App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="d460f-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="d460f-104">Este artículo trata sobre App Service Environment v1.</span><span class="sxs-lookup"><span data-stu-id="d460f-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="d460f-105">Hay una versión más reciente de App Service Environment que resulta más fácil de usar y se ejecuta en una infraestructura más eficaz.</span><span class="sxs-lookup"><span data-stu-id="d460f-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="d460f-106">Para aprender más sobre la nueva versión, consulte [Introducción a App Service Environment](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="d460f-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="d460f-107">Información general</span><span class="sxs-lookup"><span data-stu-id="d460f-107">Overview</span></span>
<span data-ttu-id="d460f-108">Un entorno de App Service es una opción de plan de servicio [Premium][PremiumTier] de Azure App Serviceque proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service a gran escala, lo que incluye [Web Apps][WebApps], [Mobile Apps][MobileApps] y [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="d460f-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="d460f-109">Los entornos del Servicio de aplicaciones son ideales para cargas de trabajo de aplicaciones que requieren:</span><span class="sxs-lookup"><span data-stu-id="d460f-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="d460f-110">Muy grande escala</span><span class="sxs-lookup"><span data-stu-id="d460f-110">Very high scale</span></span>
* <span data-ttu-id="d460f-111">Aislamiento y acceso a redes seguro</span><span class="sxs-lookup"><span data-stu-id="d460f-111">Isolation and secure network access</span></span>

<span data-ttu-id="d460f-112">Los clientes pueden crear varios entornos del Servicio de aplicaciones en una o varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d460f-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="d460f-113">Esto hace que sean perfectos para los niveles de aplicación sin estado de escalado horizontal en el respaldo de cargas de trabajo RPS elevadas.</span><span class="sxs-lookup"><span data-stu-id="d460f-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="d460f-114">Los entornos del Servicios de aplicaciones están aislados para ejecutar únicamente las aplicaciones de un solo cliente, y siempre se implementan en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d460f-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="d460f-115">Los clientes tienen un mayor control sobre el tráfico de red entrante y saliente de las aplicaciones, y las aplicaciones pueden establecer conexiones seguras de alta velocidad a los recursos corporativos locales a través de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d460f-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="d460f-116">Todos los artículos y procedimientos acerca de los entornos del Servicio de aplicaciones están disponibles en el archivo [Léame para entornos del Servicio de aplicaciones](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="d460f-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="d460f-117">Para obtener información general del modo en que los entornos de App Service permiten el acceso de red a alta escala y seguro, consulte el [vídeo Deep Dive de AzureCon][AzureConDeepDive] sobre los entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="d460f-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="d460f-118">Para profundizar en el escalado horizontal con varios entornos de App Service, consulte el artículo sobre cómo configurar una [superficie de aplicaciones con distribución geográfica][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="d460f-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="d460f-119">Para ver cómo se ha configurado la arquitectura de seguridad mostrada en la inmersión en AzureCon, consulte el artículo sobre la implementación de una [arquitectura de seguridad en capas](app-service-app-service-environment-layered-security.md) con entornos del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d460f-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="d460f-120">Las aplicaciones que se ejecutan en entornos de aplicación de servicio pueden tener su acceso validado por dispositivos de subida como firewalls de aplicación web (WAF).</span><span class="sxs-lookup"><span data-stu-id="d460f-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="d460f-121">En el artículo sobre la [configuración de un WAF para entornos de aplicación de servicio](app-service-app-service-environment-web-application-firewall.md) se trata este escenario.</span><span class="sxs-lookup"><span data-stu-id="d460f-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="d460f-122">Recursos de proceso dedicados</span><span class="sxs-lookup"><span data-stu-id="d460f-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="d460f-123">Todos los recursos de proceso de un entorno del Servicio de aplicaciones están dedicados exclusivamente a una sola suscripción, y se puede configurar un entorno del Servicio de aplicaciones con hasta cincuenta recursos de proceso (50) para uso exclusivo de una única aplicación.</span><span class="sxs-lookup"><span data-stu-id="d460f-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="d460f-124">Un entorno de este tipo se compone de un grupo de recursos de proceso front-end y de entre uno a tres grupos de recursos de proceso de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d460f-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="d460f-125">El grupo de servidores front-end contiene los recursos de proceso responsables de la terminación SSL y del equilibrio de carga automático de las solicitudes de aplicación dentro de un entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d460f-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="d460f-126">Cada grupo de trabajo contiene recursos de proceso asignados a [Planes de App Service][AppServicePlan] que, a su vez, contienen una o más aplicaciones de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d460f-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="d460f-127">Como en un entorno del Servicio de aplicaciones puede haber hasta tres grupos de trabajo distintos, tiene la flexibilidad de elegir diferentes recursos de proceso para cada grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d460f-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="d460f-128">Esto permite, por ejemplo, crear un grupo de trabajo con recursos de proceso de menor eficacia para los planes del Servicio de aplicaciones destinados a aplicaciones de prueba o desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d460f-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="d460f-129">Un segundo (o incluso tercer) grupo de trabajo podría usar recursos de proceso más eficaces en los planes del Servicio de aplicaciones que ejecuten aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="d460f-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="d460f-130">Para obtener más detalles sobre la cantidad de recursos de proceso disponibles para los grupos de servidores front-end y los grupos de trabajo, consulte el artículo de [configuración de un entorno de App Service][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="d460f-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="d460f-131">Para obtener más detalles sobre los tamaños de los recursos de proceso disponibles admitidos en un entorno de App Service, consulte la página de [precios de App Service][AppServicePricing] y revise las opciones disponibles para este tipo de entornos en el plan de tarifa Premium.</span><span class="sxs-lookup"><span data-stu-id="d460f-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="d460f-132">Compatibilidad con redes virtuales</span><span class="sxs-lookup"><span data-stu-id="d460f-132">Virtual Network Support</span></span>
<span data-ttu-id="d460f-133">Puede crearse un entorno de App Service **en** una red virtual de Azure Resource Manager **o** en una del modelo de implementación clásica ([obtenga más información sobre las redes virtuales][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="d460f-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="d460f-134">Puesto que los entornos de este tipo residen siempre en una red virtual y, más concretamente, en una subred de una red virtual, puede aprovechar las características de seguridad de las redes virtuales para controlar las comunicaciones de red entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="d460f-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="d460f-135">Una instancia de App Service Environment puede tener conexión a Internet con una dirección IP pública, o tener una conexión interna solo con la dirección de un equilibrador de carga interno (ILB) de Azure.</span><span class="sxs-lookup"><span data-stu-id="d460f-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="d460f-136">Puede usar [grupos de seguridad de red][NetworkSecurityGroups] para restringir las comunicaciones de red entrantes a la subred donde reside el entorno de App Service.</span><span class="sxs-lookup"><span data-stu-id="d460f-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="d460f-137">Esto le permite ejecutar aplicaciones tras dispositivos y servicios ascendentes, como firewalls de aplicaciones web y proveedores de SaaS de red.</span><span class="sxs-lookup"><span data-stu-id="d460f-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="d460f-138">Las aplicaciones, además, suelen requerir acceso a recursos corporativos, como bases de datos internas y servicios web.</span><span class="sxs-lookup"><span data-stu-id="d460f-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="d460f-139">Un enfoque común consiste en poner estos extremos a disposición únicamente del flujo de tráfico de red interno de una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="d460f-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="d460f-140">Una vez que un entorno de App Service se une a la misma red virtual que los servicios internos, las aplicaciones que se ejecutan en el entorno pueden tener acceso a ellos, incluidos los puntos de conexión accesibles mediante conexiones [De sitio a sitio][SiteToSite] y [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="d460f-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="d460f-141">Para obtener más detalles sobre cómo funcionan los entornos de App Service con redes virtuales y locales, consulte los siguientes artículos sobre [información general sobre la arquitectura de red de los entornos de App Service][NetworkArchitectureOverview], de [cómo controlar el tráfico de entrada a un entorno de App Service][ControllingInboundTraffic] y sobre [conexión segura a los recursos de back-end desde un entorno de App Service][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="d460f-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="d460f-142">Introducción</span><span class="sxs-lookup"><span data-stu-id="d460f-142">Getting started</span></span>
<span data-ttu-id="d460f-143">Para empezar a trabajar con los entornos de App Service, consulte el artículo sobre [creación de un entorno de App Service][HowToCreateAnAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="d460f-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="d460f-144">Todos los artículos y procedimientos para los entornos del Servicio de aplicaciones están disponibles en el archivo [Léame para entornos del Servicio de aplicaciones](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="d460f-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="d460f-145">Para obtener más información sobre la plataforma Azure App Service, consulte [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="d460f-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="d460f-146">Para obtener información general sobre la arquitectura de red del entorno de App Service, consulte el artículo de [información general sobre la arquitectura de red de los entornos de App Service][NetworkArchitectureOverview].</span><span class="sxs-lookup"><span data-stu-id="d460f-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="d460f-147">Para obtener información detallada sobre el uso de un entorno de App Service con ExpressRoute, consulte el siguiente artículo sobre [detalles de configuración de red para entornos de App Service con ExpressRoute][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="d460f-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


