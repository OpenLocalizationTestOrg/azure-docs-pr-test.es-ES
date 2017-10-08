---
title: "Introducción de aplicaciones aaaAPI | Documentos de Microsoft"
description: "Aprenda cómo el Servicio de aplicaciones de Azure le ayuda a desarrollar, hospedar y consumir API de RESTful."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Información general sobre Aplicaciones de API
Aplicaciones de API en las características de la oferta de servicio de aplicaciones de Azure que hacen que sea más fácil toodevelop, hospedar y utilizar las API en la nube de Hola y local. Gracias a las aplicaciones de API, disfrutará de seguridad de categoría empresarial, control de acceso sencillo, conectividad híbrida, generación automática de SDK e integración completa con [Aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md).

[Servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) es una plataforma totalmente administrada para escenarios web, móviles y de integración. Aplicaciones de API son uno de los cuatro tipos que ofrece el [Servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md).

![Tipos de aplicaciones en el Servicio de aplicaciones de Azure](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>¿Por qué usar Aplicaciones de API?
Estas son algunas características clave de las aplicaciones de API:

* **Poner la API existente como-es** - no tiene toochange cualquier Hola código en su beneficio de tootake API existente de aplicaciones de API: implemente la aplicación de tooan API de código. La API puede usar cualquier lenguaje o marco admitido por el Servicio de aplicaciones, como ASP.NET y C#, Java, PHP, Node.js y Python.
* **Fácil consumo** : la compatibilidad integrada con [los metadatos de API de Swagger](http://swagger.io/) permite que una gran variedad de clientes pueda consumir las API de forma sencilla.  Generan automáticamente código de cliente para las API en diversos lenguajes, como C#, Java y Javascript. Configuran fácilmente [CORS](app-service-api-cors-consume-javascript.md) sin cambiar el código. Para más información, consulte [Metadatos de App Service API Apps para la detección de API y la generación de código](app-service-api-metadata.md) y [Consumo de una aplicación de API desde JavaScript con CORS](app-service-api-cors-consume-javascript.md). 
* **Control de acceso simple** -proteger una aplicación de API de acceso no autenticado con ningún código de tooyour de cambios. Los servicios de autenticación integrados protegen las API frente al acceso de otros servicios o de clientes que representan a los usuarios. Los proveedores de identidad compatibles incluyen Azure Active Directory, Facebook, Twitter, Google y cuenta Microsoft. Los clientes pueden usar la biblioteca de autenticación de Active Directory (ADAL) o hello SDK de aplicaciones móviles. Para más información, consulte [Autenticación y autorización para Aplicaciones de API en el Servicio de aplicaciones de Azure](app-service-api-authentication.md).
* **Integración de Visual Studio** -herramientas dedicadas en Visual Studio simplifican el trabajo Hola de crear, implementar, utilizar, depuración y administración de aplicaciones de API. Para obtener más información, consulte [anuncio Hola 2.8.1 del Azure SDK para .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Integración con aplicaciones lógicas** : las [aplicaciones lógicas del Servicio de aplicaciones](../logic-apps/logic-apps-what-are-logic-apps.md)pueden consumir las aplicaciones de API que cree.  Para más información, consulte [Uso de la API personalizada hospedada en App Service con Logic apps](../logic-apps/logic-apps-custom-hosted-api.md) y [Nueva versión de esquema 2015-08-01: versión preliminar](../logic-apps/logic-apps-schema-2015-08-01.md).

Además, una aplicación de API puede sacar partido de las características que ofrecen las [Web Apps](../app-service-web/app-service-web-overview.md) y [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md). Hola inversa también es cierto: si usa una aplicación web o aplicación móvil toohost una API, pueda aprovechar características de aplicaciones de API como metadatos de Swagger de cliente de generación de código y CORS para el acceso entre dominios del explorador. Hello solo diferencia entre Hola tres tipos de aplicaciones (API, web, móvil) es nombre de Hola y el icono que se utiliza para ellos en hello portal de Azure.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>¿Cuál es la diferencia de hello entre las aplicaciones de API y administración de API de Azure?
Aplicaciones de API y [Administración de API de Azure](../api-management/api-management-key-concepts.md) son servicios complementarios:

* Administración de API se dedica a la administración de API. Coloque un front-end de administración de API en un toomonitor de API y limitar el uso de, manipular la entrada y salida, consolidar varias API en un punto de conexión y así sucesivamente. Hola API se está administradas se puede hospedar en cualquier lugar.
* Aplicaciones de API se dedica al hospedaje de API. servicio de Hello incluye características que facilitan la API de desarrollo y mucho, pero no Hola tipos de supervisión, limitación, manipular o consolidar que administración de API no. Si no necesita las características de Administración de API, puede hospedar las API en Aplicaciones de API sin usar Administración de API.

A continuación hay un diagrama que ilustra Administración de API usada paras las API hospedadas en Aplicaciones de API y en cualquier otro lugar.

![P+F de Aplicaciones de API y Administración de API de Azure](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Algunas características de Administración de API y Aplicaciones de API tienen funciones similares.  Por ejemplo, ambos pueden automatizar la compatibilidad con CORS. Cuando utilices conjuntamente dos servicios de hello, usaría administración de API para CORS puesto que funciona como Hola aplicaciones tooyour API de front-end. 

## <a name="getting-started"></a>Introducción
tooget a trabajar con aplicaciones de API implementando tooone de código de ejemplo, vea tutorial de hello para el marco de trabajo que prefiera:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask preguntas acerca de las aplicaciones de API, iniciar un subproceso en hello [foro de aplicaciones de API](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

