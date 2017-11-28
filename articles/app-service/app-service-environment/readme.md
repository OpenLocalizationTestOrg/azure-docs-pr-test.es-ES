---
title: "Léame de aaaAzure entorno del servicio de aplicaciones"
description: "Documentación de Hola de listas que describe el entorno de servicio de aplicaciones de Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="605f9-103">Documentación de App Service Environment</span><span class="sxs-lookup"><span data-stu-id="605f9-103">App Service environment documentation</span></span>
 <span data-ttu-id="605f9-104">Azure App Service Environment es una característica de Azure App Service que proporciona un entorno completamente aislado y dedicado para ejecutar de forma segura las aplicaciones de App Service a gran escala.</span><span class="sxs-lookup"><span data-stu-id="605f9-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="605f9-105">Esta funcionalidad puede hospedar instancias de [Web Apps][webapps], [Mobile Apps][mobileapps], [API Apps][APIApps] y [Functions][Functions].</span><span class="sxs-lookup"><span data-stu-id="605f9-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="605f9-106">Las instancias de App Service Environment (ASE) son ideales para cargas de trabajo de aplicaciones que necesitan:</span><span class="sxs-lookup"><span data-stu-id="605f9-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="605f9-107">Escala muy grande.</span><span class="sxs-lookup"><span data-stu-id="605f9-107">Very high scale.</span></span>
* <span data-ttu-id="605f9-108">Aislamiento y acceso de red seguro.</span><span class="sxs-lookup"><span data-stu-id="605f9-108">Isolation and secure network access.</span></span>

<span data-ttu-id="605f9-109">Los clientes pueden crear varias instancias de ASE en una y en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="605f9-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="605f9-110">Esta versatilidad hace que las instancias de ASE sean perfectas para capas de aplicación sin estado de escalado horizontal que apoyan a cargas de trabajo RPS elevadas.</span><span class="sxs-lookup"><span data-stu-id="605f9-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="605f9-111">ASEs están aislada toorunning sólo las aplicaciones de un único cliente y siempre se implementan en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="605f9-111">ASEs are isolated toorunning only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="605f9-112">Los clientes tienen un mayor control sobre el tráfico de red entrante y saliente de la aplicación mediante [grupos de seguridad de red][NSGs].</span><span class="sxs-lookup"><span data-stu-id="605f9-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="605f9-113">Las aplicaciones también pueden establecer conexiones seguras a alta velocidad sobre los recursos corporativos de redes virtuales tooon local.</span><span class="sxs-lookup"><span data-stu-id="605f9-113">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="605f9-114">Aplicaciones a menudo necesitan tooaccess los recursos corporativos, como servicios web y bases de datos internas.</span><span class="sxs-lookup"><span data-stu-id="605f9-114">Apps frequently need tooaccess corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="605f9-115">Las aplicaciones que se ejecutan en instancias de ASE pueden acceder a recursos a través de conexiones VPN de [sitio a sitio][SiteToSite] y de [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="605f9-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="605f9-116">[¿Qué es App Service Environment?][Intro]</span><span class="sxs-lookup"><span data-stu-id="605f9-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="605f9-117">[Creación de una instancia de App Service Environment][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="605f9-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="605f9-118">[Creación de una instancia de App Service Environment de equilibrador de carga interno][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="605f9-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="605f9-119">[Uso de una instancia de App Service Environment][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="605f9-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="605f9-120">[Hello entorno de servicio de aplicaciones y consideraciones de red][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="605f9-120">[Networking considerations and hello App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="605f9-121">[Creación de una instancia de App Service Environment a partir de una plantilla][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="605f9-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="605f9-122">Vídeos</span><span class="sxs-lookup"><span data-stu-id="605f9-122">Videos</span></span>
<span data-ttu-id="605f9-123">Master moderno PaaS para hello empresarial con el servicio de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="605f9-123">Master Modern PaaS for hello Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="605f9-124">Deploying Highly Scalable and Secure Apps (Implementación de aplicaciones seguras y altamente escalables)</span><span class="sxs-lookup"><span data-stu-id="605f9-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="605f9-125">Running Enterprise Web and Mobile Apps on Azure App Service (Ejecución de aplicaciones web y móviles para empresas en Azure App Service)</span><span class="sxs-lookup"><span data-stu-id="605f9-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="605f9-126">App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="605f9-126">App Service Environment v1</span></span> ##
<span data-ttu-id="605f9-127">Hay dos versiones de App Service Environment: ASEv1 y ASEv2.</span><span class="sxs-lookup"><span data-stu-id="605f9-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="605f9-128">Para más información sobre ASEv1, vea la [documentación sobre App Service Environment v1][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="605f9-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
