---
title: aaaApp entorno del servicio | Documentos de Microsoft
description: "¿Qué es un Entorno del Servicio de aplicaciones de Azure? Un entorno de servicio de introducción tooApp."
keywords: entorno del servicio de aplicaciones de Azure, red virtual, redes seguras
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="d9bc9-105">Documentación del Entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9bc9-105">App Service Environment Documentation</span></span>
<span data-ttu-id="d9bc9-106">Un entorno de App Service es una opción de plan de servicio [Premium][PremiumTier] de Azure App Serviceque proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service a gran escala, lo que incluye [Web Apps][WebApps], [Mobile Apps][MobileApps] y [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="d9bc9-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="d9bc9-107">Los entornos del Servicio de aplicaciones son ideales para cargas de trabajo de aplicaciones que requieren:</span><span class="sxs-lookup"><span data-stu-id="d9bc9-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="d9bc9-108">Muy grande escala</span><span class="sxs-lookup"><span data-stu-id="d9bc9-108">Very high scale</span></span>
* <span data-ttu-id="d9bc9-109">Aislamiento y acceso a redes seguro</span><span class="sxs-lookup"><span data-stu-id="d9bc9-109">Isolation and secure network access</span></span>

<span data-ttu-id="d9bc9-110">Los clientes pueden crear varios entornos del Servicio de aplicaciones en una o varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc9-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="d9bc9-111">Esto hace que sean perfectos para los niveles de aplicación sin estado de escalado horizontal en el respaldo de cargas de trabajo RPS elevadas.</span><span class="sxs-lookup"><span data-stu-id="d9bc9-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="d9bc9-112">Los entornos del servicio de aplicación son toorunning aislado sólo las aplicaciones de un único cliente y siempre se implementan en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d9bc9-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="d9bc9-113">Los clientes tienen un mayor control sobre el tráfico de red entrante y saliente de la aplicación si usan [grupos de seguridad de red][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="d9bc9-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="d9bc9-114">Las aplicaciones también pueden establecer conexiones seguras a alta velocidad sobre los recursos corporativos de redes virtuales tooon local.</span><span class="sxs-lookup"><span data-stu-id="d9bc9-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="d9bc9-115">Aplicaciones a menudo necesitan tooaccess los recursos corporativos, como servicios web y bases de datos internas.</span><span class="sxs-lookup"><span data-stu-id="d9bc9-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="d9bc9-116">Las aplicaciones que se ejecutan en entornos de App Service pueden tener acceso a los recursos accesibles mediante conexiones VPN [de sitio a sitio][SiteToSite] y [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="d9bc9-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="d9bc9-117">¿Qué es un entorno del Servicio de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="d9bc9-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="d9bc9-118">Creación de un Entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9bc9-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="d9bc9-119">Creación de aplicaciones en un Entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9bc9-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="d9bc9-120">Creación y uso de un equilibrador de carga interno con entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9bc9-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="d9bc9-121">Configuración de un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9bc9-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="d9bc9-122">Escalado de aplicaciones en un Entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9bc9-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="d9bc9-123">Arquitectura y seguridad de red</span><span class="sxs-lookup"><span data-stu-id="d9bc9-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="d9bc9-124">Procedimientos</span><span class="sxs-lookup"><span data-stu-id="d9bc9-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="d9bc9-125">Vídeos</span><span class="sxs-lookup"><span data-stu-id="d9bc9-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
