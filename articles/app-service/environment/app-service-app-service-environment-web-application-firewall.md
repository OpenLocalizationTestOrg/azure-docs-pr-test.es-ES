---
title: "Configuración de un firewall de aplicaciones web (WAF) para entornos de App Service"
description: "Obtenga información sobre cómo configurar un firewall de aplicaciones web delante del entorno de App Service."
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
ms.topic: tutorial
ms.date: 08/17/2016
ms.author: naziml
ms.custom: mvc
ms.openlocfilehash: bfe36ee5365e71db4280e8e2ccff6db8e552dd39
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configuración de un firewall de aplicaciones web (WAF) para entornos de App Service
## <a name="overview"></a>Información general
Los firewalls de aplicaciones web como [Barracuda WAF para Azure](https://www.barracuda.com/programs/azure), que está disponible en [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/), ayudan a proteger las aplicaciones web mediante la inspección del tráfico web entrante para bloquear las inyecciones de código SQL, scripts entre sitios, cargas de malware, DDoS de aplicaciones y otros ataques. También examina las respuestas de los servidores web back-end para prevención de pérdida de datos (DLP). Combinado con el aislamiento y la escala adicional proporcionados por los entornos de App Service, esto proporciona un entorno ideal para hospedar importantes aplicaciones web empresariales que deben soportar peticiones malintencionadas y tráfico de gran volumen.

[!INCLUDE [app-service-web-to-api-and-mobile](../../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Configuración
Para este documento, configuraremos el entorno de App Service detrás de varias instancias de carga equilibrada de Barracuda WAF para que únicamente el tráfico del WAF pueda ponerse en contacto con el entorno de App Service y no se pueda acceder a este desde la red perimetral. También dispondremos de Azure Traffic Manager delante de las instancias de Barracuda WAF para equilibrar la carga entre las regiones y los centros de datos de Azure. Un diagrama de alto nivel del programa de instalación tendría el aspecto que se muestra a continuación:

![Arquitectura][Architecture] 

> [!NOTE]
> Con la introducción de [la compatibilidad de ILB con el entorno de App Service](app-service-environment-with-internal-load-balancer.md), puede configurar el ASE para que no pueda accederse a este desde la red perimetral y solo esté disponible en la red privada. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configuración del entorno de App Service
Para configurar un entorno de App Service, consulte [nuestra documentación](app-service-web-how-to-create-an-app-service-environment.md) sobre el tema. Después de crear una instancia de App Service Environment, puede crear en él Web Apps, API Apps y [Mobile Apps](../../app-service-mobile/app-service-mobile-value-prop.md) que se protegerán detrás del WAF que se configurará en la próxima sección.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configuración del servicio en la nube Barracuda WAF
Barracuda tiene un [artículo detallado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre la implementación de su WAF en una máquina virtual en Azure. No obstante, habida cuenta de que queremos redundancia y no introducir un único punto de error, hay que implementar al menos dos máquinas virtuales de la instancia de WAF en el mismo servicio en la nube al seguir estas instrucciones.

### <a name="adding-endpoints-to-cloud-service"></a>Incorporación de extremos al servicio en la nube
Cuando ya tenga dos o más instancias de máquina virtual de WAF en el servicio en la nube, puede usar [Azure Portal](https://portal.azure.com/) para agregar puntos de conexión HTTP y HTTPS que la aplicación use, como se muestra en la imagen siguiente:

![Configuración de extremos][ConfigureEndpoint]

Si las aplicaciones usan otros puntos de conexión, asegúrese de agregarlos también a esta lista. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configuración de Barracuda WAF mediante su portal de administración
Barracuda WAF utiliza el puerto TCP 8000 para la configuración a través de su portal de administración. Si tiene varias instancias de máquinas virtuales de WAF, debe repetir los pasos siguientes para cada instancia de máquina virtual. 

> [!NOTE]
> Una vez que haya terminado con la configuración de WAF, quite el punto de conexión TCP/8000 de todas las máquinas virtuales de WAF para preservar la seguridad del WAF.
> 
> 

Agregue el punto de conexión de administración como se muestra en la imagen siguiente para configurar Barracuda WAF.

![Incorporación de extremos de administración][AddManagementEndpoint]

Utilice un explorador para examinar el extremo de administración en el servicio en la nube. Si el servicio en la nube se llama test.cloudapp.net, para acceder a este punto de conexión sería preciso dirigirse a http://test.cloudapp.net:8000. Debería ver una página de inicio de sesión como la siguiente en la que pueda iniciar sesión con las credenciales especificadas en la fase de instalación de la máquina virtual de WAF.

![Página de inicio de sesión de administración][ManagementLoginPage]

Tras iniciar sesión, debe aparecer un panel de información como el de la imagen siguiente que presente las estadísticas básicas sobre la protección de WAF.

![Panel de administración][ManagementDashboard]

Al hacer clic en la pestaña **Servicios**, podrá configurar el WAF para los servicios que protege. Para obtener más información sobre cómo configurar Barracuda WAF, puede consultar [su documentación](https://techlib.barracuda.com/waf/getstarted1). En el ejemplo siguiente, se ha configurado una aplicación web de Azure que atiende el tráfico en HTTP y HTTPS.

![Administración de agregar servicios][ManagementAddServices]

> [!NOTE]
> En función de cómo se configuran las aplicaciones y qué características se utilizan en el entorno de App Service, deberá reenviar el tráfico para los puertos TCP distintos del 80 y el 443, por ejemplo, si ha configurado SSL de IP para una aplicación web. Para obtener una lista de los puertos de red usados en entornos de App Service, vea la sección dedicada a los puertos de red en la [documentación del control del tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md).
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configuración de Microsoft Azure Traffic Manager (OPCIONAL)
Si la aplicación se encuentra disponible en varias regiones, debe equilibrar la carga entre ellas detrás del [Administrador de tráfico de Azure](../../traffic-manager/traffic-manager-overview.md). Para ello, puede agregar un punto de conexión en [Azure Portal](https://portal.azure.com) con el nombre del servicio en la nube de su WAF en el perfil de Traffic Manager, como se muestra en la imagen siguiente. 

![Extremo del Administrador de tráfico][TrafficManagerEndpoint]

Si la aplicación requiere autenticación, asegúrese de que tiene algún recurso que no requiere ninguna autenticación para que el Administrador de tráfico haga ping para la disponibilidad de la aplicación. Puede configurar la dirección URL en la página **Configuración** de [Azure Portal](https://portal.azure.com) tal como se muestra en la siguiente imagen:

![Configuración del Administrador de tráfico][ConfigureTrafficManager]

Para reenviar los pings de Traffic Manager desde el WAF a la aplicación, debe configurar las traducciones de sitios web en Barracuda WAF para reenviar el tráfico a la aplicación, tal como se muestra en el ejemplo siguiente:

![Traducciones de sitios web][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a>Protección del tráfico en el entorno de App Service mediante grupos de recursos de red (NSG)
Vea la [documentación sobre el control del tráfico de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obtener detalles sobre la restricción del tráfico en el entorno de App Service desde el WAF solo mediante la utilización de la dirección IP virtual del servicio en la nube. A continuación se muestra un comando PowerShell de ejemplo para realizar esta tarea para el puerto TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Reemplace SourceAddressPrefix con la dirección IP virtual (VIP) del servicio en la nube del WAF.

> [!NOTE]
> La dirección VIP del servicio en la nube cambiará al eliminar y volver a crear el servicio en la nube. Asegúrese de actualizar la dirección IP en el grupo de recursos de red una vez hecho esto. 
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
