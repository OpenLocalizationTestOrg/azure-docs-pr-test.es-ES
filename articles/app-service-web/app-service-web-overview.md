---
title: "información general de aplicaciones de aaaWeb | Documentos de Microsoft"
description: "Vea cómo el Servicio de aplicaciones de Azure lo ayuda a desarrollar y hospedar aplicaciones web."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Introducción a Aplicaciones web
*Aplicaciones web del Servicio de aplicaciones* es una plataforma de procesos completamente administrada que se ha optimizado para el hospedaje de sitios y aplicaciones web. Esto [plataforma como servicio](https://en.wikipedia.org/wiki/Platform_as_a_service) oferta (PaaS) de Microsoft Azure le permite centrarse en la lógica de negocios mientras Azure se encarga de hello infraestructura toorun y escalar sus aplicaciones.

Hola después de 5 minutos vídeo presenta aplicaciones de Web del servicio de aplicación de Azure.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>¿Qué es una aplicación web en el Servicio de aplicaciones?
En el servicio de aplicación, un *aplicación web* es hello recursos de proceso que proporciona Azure para hospedar un sitio Web o aplicación web.  

recursos de proceso de Hello pueden estar en compartido o dedicadas máquinas virtuales (VM), dependiendo de hello tarifa que elija. El código de la aplicación se ejecuta en una máquina virtual administrada que se aísla de otros clientes.

El código puede utilizar cualquier lenguaje o marco que sea compatible con el [Servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md), como ASP.NET, Node.js, Java, PHP o Python. También puede ejecutar scripts que usen [PowerShell y otros lenguajes de scripting](web-sites-create-web-jobs.md#acceptablefiles) en una aplicación web.

Para obtener ejemplos de escenarios de aplicación típicos que puede usar las aplicaciones Web para, vea [Web escenarios de aplicación](https://azure.microsoft.com/documentation/scenarios/web-app/) hello y **escenarios y recomendaciones para** sección de [servicio de aplicaciones de Azure, Virtual Comparación de las máquinas, Service Fabric y servicios en la nube](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>¿Por qué usar Aplicaciones web?
Estas son algunas características clave del servicio de aplicaciones que se aplican tooWeb aplicaciones:

* **Varios lenguajes y plataformas** : Servicio de aplicaciones es compatible con ASP.NET, Node.js, Java, PHP y Python. También puede ejecutar [PowerShell y otros scripts o ejecutables](web-sites-create-web-jobs.md) en máquinas virtuales del Servicio de aplicaciones.
* **Optimización de DevOps** : configure la [integración y la implementación continuas](app-service-continuous-deployment.md) con Visual Studio Team Services, GitHub o BitBucket. Promueva actualizaciones a través de [entornos de ensayo y prueba](web-sites-staged-publishing.md). Realice [las pruebas A/B](app-service-web-test-in-production-get-start.md). Administrar las aplicaciones de servicio de aplicaciones mediante [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [multiplataforma interfaz de línea de comandos (CLI)](../cli-install-nodejs.md).
* **Escala global con alta disponibilidad**: escale [verticalmente](web-sites-scale.md) u [horizontalmente](../monitoring-and-diagnostics/insights-how-to-scale.md) de forma manual o automática. Permite hospedar las aplicaciones en cualquier parte de la infraestructura de centro de datos globales de Microsoft y Hola servicio de aplicaciones [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) compromisos de alta disponibilidad.
* **Datos de plataformas y local de conexiones tooSaaS** -elegir entre más de 50 [conectores](../connectors/apis-list.md) para sistemas empresariales (como SAP, Siebel y Oracle), servicios de SaaS (por ejemplo, Salesforce y Office 365) e internet servicios (por ejemplo, Facebook y Twitter). Acceda a los datos locales mediante [Conexiones híbridas](../biztalk-services/integration-hybrid-connection-overview.md) y [Azure Virtual Networks](web-sites-integrate-with-vnet.md).
* **Seguridad y cumplimiento** : Servicio de aplicaciones cumple con [ISO, SOC y PCI](https://www.microsoft.com/TrustCenter/).
* **Plantillas de aplicación** -elegir entre una amplia lista de plantillas de aplicación Hola [Azure Marketplace](https://azure.microsoft.com/marketplace/) que le permiten usar un software de código abierto populares de asistente tooinstall como WordPress, Joomla y Drupal.
* **Integración de Visual Studio** -herramientas dedicadas en Visual Studio simplifican el trabajo Hola de crear, implementar y depurar.

Además, una aplicación web puede aprovechar las características ofrecidas por [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (como la compatibilidad con CORS) y [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (por ejemplo, las notificaciones push). Para más información sobre los tipos de aplicaciones del Servicio de aplicaciones, consulte [¿Qué es Servicios de aplicaciones de Azure?](../app-service/app-service-value-prop-what-is.md).

Además de Aplicaciones web en el Servicio de aplicaciones, Azure ofrece otros servicios que se pueden utilizar para hospedar aplicaciones web y sitios web. Para la mayoría de los escenarios, las aplicaciones Web es mejor opción de Hola.  Arquitectura de microservicio, considere la posibilidad de [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)y si necesita más control sobre hello las máquinas virtuales que el código se ejecuta en, considere la posibilidad de [máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/). Para obtener más información acerca de cómo toochoose entre estos servicios de Azure, consulte [comparación de servicio de aplicaciones de Azure, máquinas virtuales, Service Fabric y servicios en la nube](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Introducción
tooget iniciado mediante la implementación de ejemplo código tooa nueva aplicación web en el servicio de aplicaciones, siga uno de los tutoriales de Hola Hola después el cuadro de lista desplegable. Necesitará una cuenta gratis de Azure.

> [!div class="op_single_selector"]
> * [Implementar su primer tooAzure de aplicación ASP.NET web en 5 minutos](app-service-web-get-started-dotnet.md)
> * [Implementar su primer tooAzure de aplicación de web PHP en 5 minutos](app-service-web-get-started-php.md)
> * [Implementar su primer tooAzure de aplicación de web Node.js en 5 minutos](app-service-web-get-started-nodejs.md)
> * [Implementar su primer tooAzure de aplicación de web de Java en 5 minutos](app-service-web-get-started-java.md)
> * [Implementar su primer tooAzure de aplicación de web de Python en 5 minutos](app-service-web-get-started-python.md)
> * [Implementar su primer tooAzure de sitio HTML en 5 minutos](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure. Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.
> 
> 
