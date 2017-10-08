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
# <a name="app-service-environment-documentation"></a>Documentación de App Service Environment
 Azure App Service Environment es una característica de Azure App Service que proporciona un entorno completamente aislado y dedicado para ejecutar de forma segura las aplicaciones de App Service a gran escala. Esta funcionalidad puede hospedar instancias de [Web Apps][webapps], [Mobile Apps][mobileapps], [API Apps][APIApps] y [Functions][Functions].

Las instancias de App Service Environment (ASE) son ideales para cargas de trabajo de aplicaciones que necesitan:

* Escala muy grande.
* Aislamiento y acceso de red seguro.

Los clientes pueden crear varias instancias de ASE en una y en varias regiones de Azure. Esta versatilidad hace que las instancias de ASE sean perfectas para capas de aplicación sin estado de escalado horizontal que apoyan a cargas de trabajo RPS elevadas.

ASEs están aislada toorunning sólo las aplicaciones de un único cliente y siempre se implementan en una red virtual de Azure. Los clientes tienen un mayor control sobre el tráfico de red entrante y saliente de la aplicación mediante [grupos de seguridad de red][NSGs]. Las aplicaciones también pueden establecer conexiones seguras a alta velocidad sobre los recursos corporativos de redes virtuales tooon local.

Aplicaciones a menudo necesitan tooaccess los recursos corporativos, como servicios web y bases de datos internas. Las aplicaciones que se ejecutan en instancias de ASE pueden acceder a recursos a través de conexiones VPN de [sitio a sitio][SiteToSite] y de [Azure ExpressRoute][ExpressRoute].

* [¿Qué es App Service Environment?][Intro]
* [Creación de una instancia de App Service Environment][MakeExternalASE]
* [Creación de una instancia de App Service Environment de equilibrador de carga interno][MakeILBASE]
* [Uso de una instancia de App Service Environment][UsingASE]
* [Hello entorno de servicio de aplicaciones y consideraciones de red][ASENetwork]
* [Creación de una instancia de App Service Environment a partir de una plantilla][MakeASEfromTemplate]


## <a name="videos"></a>Vídeos
Master moderno PaaS para hello empresarial con el servicio de aplicación de Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Deploying Highly Scalable and Secure Apps (Implementación de aplicaciones seguras y altamente escalables)
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Running Enterprise Web and Mobile Apps on Azure App Service (Ejecución de aplicaciones web y móviles para empresas en Azure App Service)
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>App Service Environment v1 ##
Hay dos versiones de App Service Environment: ASEv1 y ASEv2. Para más información sobre ASEv1, vea la [documentación sobre App Service Environment v1][ASEv1README].


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
