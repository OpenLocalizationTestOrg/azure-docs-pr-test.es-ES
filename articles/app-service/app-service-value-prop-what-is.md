---
title: "aaaAzure servicio de aplicaciones para web, móviles y aplicaciones de API | Documentos de Microsoft"
description: "Descubra cómo el Servicio de aplicaciones de Azure le ayuda a desarrollar, implementar y administrar aplicaciones web y móviles."
keywords: "app service, azure app service, costo de app service, escala, escalable, implementación de aplicaciones, implementación de aplicaciones de azure, paas, plataforma como servicio, sitio web, web, azure mobile"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>¿Qué es Servicios de aplicaciones de Azure?
*Servicio de aplicaciones* es una oferta de [plataforma como servicio](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) de Microsoft Azure. Cree aplicaciones web y móviles para cualquier plataforma o dispositivo. Integre sus aplicaciones con soluciones SaaS, conecte con aplicaciones locales y automatice los procesos empresariales. Azure ejecuta las aplicaciones en máquinas virtuales totalmente administradas, con la elección de los recursos compartidos de máquinas virtuales o máquinas virtuales dedicadas.

Servicio de aplicaciones incluye web hello y capacidades móviles que se incluía anteriormente por separado como sitios Web de Azure y servicios móviles de Azure. También incluye nuevas funcionalidades para automatizar procesos empresariales y hospedar las API en la nube. Como un servicio integrado único, Servicio de aplicaciones le permite crear distintos componentes, como sitios web, back-end de aplicación móvil, API de RESTful y procesos empresariales, en una única solución.

vídeo de 4 minutos siguiente Hello proporciona una breve explicación de cómo el servicio de aplicaciones se relaciona con tooearlier Azure ofertas y cuáles son las novedades en ella.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>¿Por qué usar el Servicio de aplicaciones?
Estas son algunas de las características y funcionalidades principales del Servicio de aplicaciones:

* **Varios lenguajes y plataformas** : Servicio de aplicaciones es compatible con ASP.NET, Node.js, Java, PHP y Python. También puede ejecutar [Windows PowerShell y otros scripts o ejecutables](../app-service-web/web-sites-create-web-jobs.md) en máquinas virtuales del Servicio de aplicaciones.
* **Optimización de DevOps** : configure la [integración y la implementación continuas](../app-service-web/app-service-continuous-deployment.md) con Visual Studio Team Services, GitHub o BitBucket. Promueva actualizaciones a través de [entornos de ensayo y prueba](../app-service-web/web-sites-staged-publishing.md). Realice [las pruebas A/B](../app-service-web/app-service-web-test-in-production-get-start.md). Administrar las aplicaciones de servicio de aplicaciones mediante [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [multiplataforma interfaz de línea de comandos (CLI)](../cli-install-nodejs.md).
* **Escala global con alta disponibilidad**: escale [verticalmente](../app-service-web/web-sites-scale.md) u [horizontalmente](../monitoring-and-diagnostics/insights-how-to-scale.md) de forma manual o automática. Permite hospedar las aplicaciones en cualquier parte de la infraestructura de centro de datos globales de Microsoft y Hola servicio de aplicaciones [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) compromisos de alta disponibilidad.
* **Datos de plataformas y local de conexiones tooSaaS** -elegir entre más de 50 [conectores](../connectors/apis-list.md) para sistemas empresariales (como SAP, Siebel y Oracle), servicios de SaaS (por ejemplo, Salesforce y Office 365) e internet servicios (por ejemplo, Facebook y Twitter). Acceda a los datos locales mediante [Conexiones híbridas](../biztalk-services/integration-hybrid-connection-overview.md) y [Azure Virtual Networks](../app-service-web/web-sites-integrate-with-vnet.md).
* **Seguridad y cumplimiento** : Servicio de aplicaciones cumple con [ISO, SOC y PCI](https://www.microsoft.com/TrustCenter/).
* **Plantillas de aplicación** -elegir entre una amplia lista de plantillas en hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) que le permiten usar un software de código abierto populares de asistente tooinstall como WordPress, Joomla y Drupal.
* **Integración de Visual Studio** -herramientas dedicadas en Visual Studio simplifican el trabajo Hola de crear, implementar y depurar.

## <a name="app-types-in-app-service"></a>Tipos de aplicaciones en el Servicio de aplicaciones
Servicio de aplicaciones ofrece varios *tipos de aplicación*, cada una de las cuales es toohost previsto una carga de trabajo específico:

* [**Aplicaciones web**](../app-service-web/app-service-web-overview.md): para hospedar sitios y aplicaciones web.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md): para hospedar back-ends de aplicaciones móviles.
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md): para hospedar API de RESTful.
* [**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md): para automatizar procesos empresariales e integrar sistemas y datos a través de nubes sin escribir código.

Hello word *aplicación* aquí hace referencia toohello aloja recursos dedicados toorunning una carga de trabajo. Llevar a cabo "aplicación web" por ejemplo, probablemente esté acostumbrado toothinking de una aplicación web como recursos de proceso de Hola y aplicación ese explorador tooa de funcionalidad de conjunto, reporta el código. Pero en el servicio de aplicaciones un *aplicación web* es hello recursos de proceso que proporciona Azure para hospedar el código de aplicación. 

La aplicación puede estar compuesta de varias aplicaciones de Servicio de aplicaciones de diferentes tipos. Por ejemplo, si la aplicación se compone de un front-end web y un back-end de la API de RESTful, se pueden realizar las operaciones siguientes:

- Implementar (front-end y api) tooa web única aplicación  
- Implementar la aplicación web de tooa de código front-end y la aplicación de tooan API de código del back-end. 



## <a name="app-service-plans"></a>Planes del Servicio de aplicaciones
[Planes de servicio de aplicaciones](azure-web-sites-web-hosting-plans-in-depth-overview.md) representan colección Hola de recursos físicos que usa toohost sus aplicaciones.

Los planes de App Service definen lo siguiente:

- **Región** (oeste de EE. UU., este de EE. UU., etc.).
- **Recuento de escala** (uno, dos, tres instancias, etc.)
- **Tamaño de la instancia** (pequeño, mediano, grande)
- **SKU** (gratis, compartido, básico, estándar y Premium)

Todas las aplicaciones asignan tooan **plan de servicio de aplicaciones** compartir recursos de hello definidos por dicha permitiéndole toosave costo al hospedar varias aplicaciones.

Su **plan de servicio de aplicaciones** puede escalarse desde **libre** y **Shared** SKU demasiado**básica**, **estándar**, y **Premium** SKU que lo que le proporciona acceso a recursos de toomore y características a lo largo de hello forma. Una vez que su Plan de servicio de aplicaciones se establece demasiado**básica** o versiones posteriores también puede controlar hello **tamaño** y escalar el recuento de hello las máquinas virtuales.

Hola **SKU** y **escala** de servicio de aplicaciones de hello plan determina Hola costo y no Hola el número de aplicaciones hospedadas en ella. 

Si necesita mayor escalabilidad y aislamiento de red, puede ejecutar las aplicaciones en un [entorno del Servicio de aplicaciones](../app-service-web/app-service-app-service-environment-intro.md).

## <a name="pricing"></a>Precios
Para más información sobre el costo de Servicio de aplicaciones, consulte [Precios de Servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="test-drive-app-service"></a>Prueba de App Service
[Cree una aplicación web, móvil o lógica de prueba](https://azure.microsoft.com/try/app-service/) y utilícela durante una hora sin necesidad de proporcionar ninguna tarjeta de crédito, sin compromiso y sin complicaciones.

También puede abrir una [cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/)y seguir uno de nuestros tutoriales de introducción:

* [Implementación de su primera aplicación web en Azure en 5 minutos](../app-service-web/app-service-web-get-started.md)
* [Creación de una aplicación de Android](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Introducción a Aplicaciones de API, ASP.NET y Swagger en el Servicio de aplicaciones de Azure](../app-service-api/app-service-api-dotnet-get-started.md)
* [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md)

