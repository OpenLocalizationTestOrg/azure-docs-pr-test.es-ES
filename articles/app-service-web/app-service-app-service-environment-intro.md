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
# <a name="introduction-tooapp-service-environment-v1"></a>Introducción tooApp v1 de entorno del servicio

> [!NOTE]
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones.  Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Información general
Un entorno de App Service es una opción de plan de servicio [Premium][PremiumTier] de Azure App Serviceque proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service a gran escala, lo que incluye [Web Apps][WebApps], [Mobile Apps][MobileApps] y [API Apps][APIApps].  

Los entornos del Servicio de aplicaciones son ideales para cargas de trabajo de aplicaciones que requieren:

* Muy grande escala
* Aislamiento y acceso a redes seguro

Los clientes pueden crear varios entornos del Servicio de aplicaciones en una o varias regiones de Azure.  Esto hace que sean perfectos para los niveles de aplicación sin estado de escalado horizontal en el respaldo de cargas de trabajo RPS elevadas.

Los entornos del servicio de aplicación son toorunning aislado sólo las aplicaciones de un único cliente y siempre se implementan en una red virtual.  Los clientes tienen control más preciso sobre el tráfico de red de aplicación entrantes y salientes, y las aplicaciones pueden establecer conexiones seguras a alta velocidad sobre los recursos corporativos de redes virtuales tooon local.

Todos los artículos y cómo-para sobre entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

Para obtener información general del proceso de habilitar a gran escala y proteger entornos del servicio de aplicación, acceso a la red, consulte hello [AzureCon profundización] [ AzureConDeepDive] en entornos del servicio de aplicación.

Para un análisis más profundo de ajuste de escala horizontal con varios entornos de servicio de aplicación consulte el artículo de hello acerca de cómo toosetup una [consumo de aplicaciones distribuidas geográficamente][GeodistributedAppFootprint].

toosee cómo se configuró la arquitectura de seguridad de Hola se muestra en hello AzureCon exhaustiva, consulte el artículo de hello en la implementación de un [en capas de arquitectura de seguridad](app-service-app-service-environment-layered-security.md) con entornos del servicio de aplicación.

Las aplicaciones que se ejecutan en entornos de aplicación de servicio pueden tener su acceso validado por dispositivos de subida como firewalls de aplicación web (WAF).  artículo de Hello en [configurar un WAFS para entornos del servicio de aplicación](app-service-app-service-environment-web-application-firewall.md) cubre este escenario. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Recursos de proceso dedicados
Todo proceso Hola recursos en un entorno de servicio de aplicaciones están dedicados exclusivamente tooa sola suscripción, y se puede configurar un entorno de servicio de aplicaciones con los recursos de proceso toofifty (50) para su uso exclusivo por una sola aplicación.

Un entorno de servicio de aplicaciones se compone de un grupo de recursos de proceso de front-end, así como grupos de recursos de proceso de trabajo de uno toothree. 

grupo de servidores front-end de Hello contiene recursos de proceso responsable de la terminación SSL como Equilibrio de carga también automática de las solicitudes de aplicación dentro de un entorno de servicio de aplicación. 

Cada grupo de trabajo contiene recursos de proceso que se asigna demasiado[planes de servicio de aplicación][AppServicePlan], que a su vez contienen una o más aplicaciones de servicio de aplicaciones de Azure.  Dado que puede haber los grupos de trabajo diferentes de toothree en un entorno de servicio de aplicaciones, tendrá Hola flexibilidad toochoose diferentes los recursos de proceso para cada grupo de trabajo.  

Por ejemplo, esto permite toocreate grupo de un trabajo con los recursos de proceso menos eficaces para planes de servicio de aplicación diseñada para las aplicaciones de desarrollo o de prueba.  Un segundo (o incluso tercer) grupo de trabajo podría usar recursos de proceso más eficaces en los planes del Servicio de aplicaciones que ejecuten aplicaciones de producción.

Para obtener más detalles sobre la cantidad de Hola de front-end de toohello disponible de recursos de proceso y los grupos de trabajo, consulte [cómo tooConfigure un entorno de servicio de aplicaciones][HowToConfigureanAppServiceEnvironment].  

Para obtener más información sobre Hola disponible calcula tamaños de recursos admitidos en un entorno de servicio de aplicaciones, consulte hello [precios del servicio de aplicación] [ AppServicePricing] página y revise Hola opciones disponibles para los entornos del servicio de aplicación en el nivel de precios de hello Premium.

## <a name="virtual-network-support"></a>Compatibilidad con redes virtuales
Puede crearse un entorno de App Service **en** una red virtual de Azure Resource Manager **o** en una del modelo de implementación clásica ([obtenga más información sobre las redes virtuales][MoreInfoOnVirtualNetworks]).  Puesto que siempre existe un entorno de servicio de aplicación en una red virtual y más concretamente dentro de una subred de una red virtual, puede aprovechar las características de seguridad de redes virtuales toocontrol hello las comunicaciones de red entrantes y salientes.  

Una instancia de App Service Environment puede tener conexión a Internet con una dirección IP pública, o tener una conexión interna solo con la dirección de un equilibrador de carga interno (ILB) de Azure.

Puede usar [grupos de seguridad de red] [ NetworkSecurityGroups] toorestrict entrada comunicaciones toohello subred donde reside un entorno de servicio de aplicaciones.  Esto le permite aplicaciones toorun detrás de servicios como firewalls de aplicación web y los proveedores de SaaS de red y dispositivos de nivel superior.

Las aplicaciones también a menudo necesitan tooaccess los recursos corporativos, como servicios web y bases de datos internas.  Un enfoque común es toomake estos extremos toointernal solo disponible el tráfico de red que fluyen en una red virtual de Azure.  Una vez que un entorno de servicio de aplicaciones se toohello combinada misma red virtual que los servicios internos hello, aplicaciones que se ejecutan en el entorno de hello puede tener acceso a ellos, incluidos los extremos accesibles a través de [sitio a sitio] [ SiteToSite]y [ExpressRoute de Azure] [ ExpressRoute] las conexiones.

Para obtener más detalles sobre cómo funcionan los entornos del servicio de aplicación con redes virtuales y redes locales Consulte Hola siguientes artículos [arquitectura de red][NetworkArchitectureOverview], [controlar la entrada Tráfico][ControllingInboundTraffic], y [conectarse de forma segura tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Introducción
tooget iniciado con el entorno de servicio de aplicación, vea [cómo tooCreate un entorno de servicio de aplicaciones][HowToCreateAnAppServiceEnvironment]

Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

Para obtener información general de arquitectura de red del entorno de servicio de aplicaciones de hello, vea hello [información general de la arquitectura de red] [ NetworkArchitectureOverview] artículo.

Para obtener más información sobre el uso de un entorno de servicio de aplicaciones con ExpressRoute, consulte Hola artículo siguiente [Express Route y entornos del servicio de aplicación][NetworkConfigDetailsForExpressRoute].

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


