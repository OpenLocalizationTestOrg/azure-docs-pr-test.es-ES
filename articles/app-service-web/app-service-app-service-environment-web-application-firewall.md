---
title: "aaaConfiguring un Firewall de aplicación Web (WAFS) para el entorno del servicio de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure una aplicación web de firewall delante de su entorno de servicio de aplicación."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configuración de un firewall de aplicaciones web (WAF) para entornos del Servicio de aplicaciones
## <a name="overview"></a>Información general
Web firewalls de aplicación como hello [Barracuda WAFS para Azure](https://www.barracuda.com/programs/azure) que está disponible en hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ayuda a proteger las aplicaciones web mediante la inspección del tráfico de web entrantes tooblock SQL Inyecciones, Scripting entre sitios, cargas de malware & aplicación DDoS y otros ataques. También examina las respuestas de Hola de servidores web back-end de Hola de prevención de pérdida de datos (DLP). Combina con aislamiento de Hola y ajustar la escala adicional proporcionada por entornos del servicio de aplicación, esto proporciona un entorno ideal toohost empresariales críticas web las aplicaciones que necesitan solicitudes malintencionadas de toowithstand y el tráfico de gran volumen.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Configuración
De este documento que se va a configurar nuestro entorno de servicio de aplicación detrás de carga varios equilibrada instancias de Barracuda WAFS para que únicamente el tráfico de hello WAFS puede llegar a Hola entorno del servicio de aplicaciones y no será accesible desde la red Perimetral de Hola. También tenemos Azure Traffic Manager delante de nuestro saldo de tooload Barracuda WAFS instancias a través de centros de datos de Azure y regiones. Un diagrama de alto nivel del programa de instalación de hello sería lo que se muestra a continuación.

![Arquitectura][Architecture] 

> Nota: con la introducción de Hola de [ILB compatibilidad con el entorno del servicio de aplicación](app-service-environment-with-internal-load-balancer.md), puede configurar toobe Hola ASE inaccesible desde la red Perimetral de Hola y solo puede red privada toohello disponible. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configuración del entorno del Servicio de aplicaciones
tooconfigure un entorno de servicio de aplicaciones, consulte demasiado[nuestra documentación](app-service-web-how-to-create-an-app-service-environment.md) en asunto Hola. Una vez que tenga un entorno de servicio de aplicación creado, puede crear [aplicaciones Web](app-service-web-overview.md), [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md) y [aplicaciones móviles](../app-service-mobile/app-service-mobile-value-prop.md) en este entorno que se protegerán detrás de hello WAFS se configurar en la siguiente sección de Hola.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configuración del servicio en la nube Barracuda WAF
Barracuda tiene un [artículo detallado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre la implementación de su WAF en una máquina virtual en Azure. Pero dado que se desea redundancia y no presentan un único punto de error, desea toodeploy al menos 2 WAFS en la instancia máquinas virtuales a Hola mismo servicio en la nube al seguir estas instrucciones.

### <a name="adding-endpoints-toocloud-service"></a>Agregar puntos de conexión tooCloud servicio
Una vez que tiene 2 o más VM WAFS instancias de servicio en la nube puede usar hello [portal de Azure](https://portal.azure.com/) tooadd extremos HTTP y HTTPS que se usan en la aplicación como se muestra en la imagen de hello siguiente.

![Configuración de extremos][ConfigureEndpoint]

Si las aplicaciones utilizan otros puntos de conexión, asegúrese de tooadd seguro también esos lista toothis. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configuración de Barracuda WAF mediante su portal de administración
Barracuda WAF utiliza el puerto TCP 8000 para la configuración a través de su portal de administración. Puesto que tenemos varias instancias de las máquinas virtuales de hello WAFS necesitará toorepeat Hola siguientes pasos para cada instancia de máquina virtual. 

> Nota: Una vez que haya terminado con la configuración de WAFS, quitar punto de conexión TCP/8000 Hola de su tookeep de máquinas virtuales WAFS su WAFS segura.
> 
> 

Agregar extremo de administración de hello tal como se muestra en la imagen de hello siguiente tooconfigure su WAFS Barracuda.

![Incorporación de extremos de administración][AddManagementEndpoint]

Usar un punto de conexión de explorador toobrowse toohello administración en su servicio de nube. Si su servicio en la nube se denomina test.cloudapp.net, podría tener acceso a este punto de conexión examinando toohttp://test.cloudapp.net:8000. Debería ver una página de inicio de sesión como las siguientes que puede iniciar sesión con credenciales especificadas en fase de la instalación de hello WAFS VM.

![Página de inicio de sesión de administración][ManagementLoginPage]

Una vez inicio de sesión debería ver un panel como Hola uno en la imagen de hello siguiente presentará estadísticas básicas sobre Hola protección WAFS.

![Panel de administración][ManagementDashboard]

Al hacer clic en la ficha de servicios de hello le permitirá configurar su WAFS para los servicios que se protege. Para obtener más información sobre cómo configurar Barracuda WAF, puede consultar [su documentación](https://techlib.barracuda.com/waf/getstarted1). En el ejemplo de Hola por debajo de una aplicación Web de Azure se ha configurado que sirve al tráfico de HTTP y HTTPS.

![Administración de agregar servicios][ManagementAddServices]

> Nota: Según la configuración de las aplicaciones y qué características se utilizan en el entorno de servicio de aplicaciones, deberá tooforward tráfico para los puertos TCP que no sea el 80 y 443, por ejemplo, si ha configurado SSL de IP para una aplicación Web. Para obtener una lista de puertos de red usados en entornos del servicio de aplicación, consulte demasiado[documentación de controlar el tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) sección de puertos de red.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configuración del Administrador de tráfico de Microsoft Azure (OPCIONAL)
Si la aplicación está disponible en varias regiones, desearía saldo tooload les detrás de [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). toodo para que pueda agregar un punto de conexión en hello [portal de Azure clásico](https://manage.azure.com) con nombre de servicio en la nube de Hola para su WAFS perfil de Traffic Manager Hola tal y como se muestra en la imagen de hello siguiente. 

![Extremo del Administrador de tráfico][TrafficManagerEndpoint]

Si la aplicación requiere autenticación, asegúrese de que tiene algún recurso que no requiere la autenticación para Traffic Manager tooping para disponibilidad hello de la aplicación. Puede configurar la dirección URL de hello en hello sección de configuración en hello [portal de Azure clásico](https://manage.azure.com) tal y como se muestra a continuación.

![Configuración del Administrador de tráfico][ConfigureTrafficManager]

tooforward Hola Traffic Manager comandos ping de la aplicación de tooyour WAFS, necesita las traducciones del sitio Web de toosetup en la aplicación de tooyour de Barracuda WAFS tooforward tráfico como se muestra en el siguiente ejemplo de Hola.

![Traducciones de sitios web][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Proteger el tráfico tooApp servicio entorno usando red seguridad grupos (NSG)
Siga hello [documentación de controlar el tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obtener más información sobre la restricción de tráfico tooyour entono de hello WAFS solo por dirección de hello VIP del servicio en la nube. A continuación se muestra un comando PowerShell de ejemplo para realizar esta tarea para el puerto TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Reemplace hello SourceAddressPrefix por dirección de IP Virtual (VIP) del servicio de nube de su WAFS Hola.

> Nota: Hola VIP de servicio en la nube cambiará al eliminar y volver a crear Hola servicio en la nube. Asegúrese de que dirección IP de tooupdate hello en el grupo de recursos de red de hello cuando lo haga. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
