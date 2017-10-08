---
title: aaaChoose entre flujo, Logic Apps, funciones y los trabajos Web | Documentos de Microsoft
description: "Comparar y contrastar hello para servicios de integración en la nube de Microsoft y decida cuáles son los servicios que debe usar."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "microsoft flow, flow, logic apps, azure functions, functions, azure webjobs, webjobs, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Elección entre Flow, Logic Apps, Functions y WebJobs
Este artículo compara y contrasta Hola después de servicios de nube de Microsoft hello, que puede todos solucionar problemas de integración y automatización de procesos empresariales:

* [Microsoft Flow](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure Functions](https://azure.microsoft.com/services/functions/)
* [Azure App Service](../app-service-web/web-sites-create-web-jobs.md)

Todos estos servicios son útiles cuando se agrupan sistemas dispares. Todos pueden definir entradas, acciones, condiciones y salidas. Todos se pueden ejecutar según una programación o un desencadenador. Sin embargo, cada servicio agrega un conjunto único de valor y compararlos no es una pregunta de "servicio que es mejor Hola?" sino cuál es el más adecuado para su situación. A menudo, una combinación de estos servicios es mejor manera de hello toorapidly crear una solución escalable y completa integración con todas las características.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Flow frente a Logic Apps
Podemos hablar sobre Microsoft Flow y Logic Apps de Azure entre sí porque ambas están *configuración primero* integration services, que resulta fácil toobuild procesos y flujos de trabajo e integrar con varios SaaS y enterprise aplicaciones. 

* Flow se crea encima de Logic Apps
* Tienen Hola mismo diseñador de flujo de trabajo
* [Conectores](../connectors/apis-list.md) que el trabajo en uno también puede trabajar en hello otro

Permite a los flujos de las integraciones de office trabajo tooperform simple (por ejemplo, obtener SMS para mensajes de correo electrónico importantes) sin pasar por los desarrolladores o TI. En Hola otra parte, Logic Apps puede habilitar una importancia decisiva o avanzados integraciones (por ejemplo, los procesos de B2B) que son necesarias las prácticas de DevOps y seguridad de nivel de empresa. Es habitual que una toogrow de flujo de trabajo de negocios en horas extraordinarias de complejidad. En consecuencia, puede empezar con un flujo al principio y luego convertirlo en aplicación de la lógica de tooa según sea necesario.

Hello tabla siguiente le ayuda a determinar si es más adecuado para la integración de una determinado flujo o Logic Apps.

|  | Flujo | Aplicaciones lógicas |
| --- | --- | --- |
| Público |trabajadores de oficina, usuarios empresariales |profesionales de TI, desarrolladores |
| Escenarios |Autoservicio |Críticas |
| Herramienta de diseño |En el explorador y aplicación móvil, solo UI |En el explorador y [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [visualización del código](../logic-apps/logic-apps-author-definitions.md) disponible |
| DevOps |Ad hoc, desarrollo en producción |control del código fuente, prueba, soporte técnico, automatización y manejabilidad en [Administración de recursos de Azure](../logic-apps/logic-apps-arm-provision.md) |
| Experiencia del administrador |[https://flow.microsoft.com](https://flow.microsoft.com) |[https://portal.azure.com](https://portal.azure.com) |
| Seguridad |Procedimientos estándar: [soberanía de datos](https://wikipedia.org/wiki/Technological_Sovereignty), [cifrado en reposo](https://wikipedia.org/wiki/Data_at_rest#Encryption) para datos confidenciales, etc. |Garantía de seguridad de Azure: [Seguridad de Azure](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Security Center](https://azure.microsoft.com/services/security-center/), [registros de auditoría](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/), y mucho más. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Functions frente a Trabajos web
Analizaremos Azure Functions y Azure App Service WebJobs juntos porque ambos son servicios de integración *Code First* y están diseñados para los desarrolladores. Le permiten toorun un script o un fragmento de código de respuesta toovarious eventos, como [nuevos Blobs de almacenamiento](functions-bindings-storage.md) o [una solicitud de WebHook](functions-bindings-http-webhook.md). Estas son sus similitudes: 

* Ambos se basan en [Azure App Service](../app-service/app-service-value-prop-what-is.md) y disfrutan de características como [control del código fuente](../app-service-web/app-service-continuous-deployment.md), [autenticación](../app-service/app-service-authentication-overview.md) y [supervisión](../app-service-web/web-sites-monitor.md).
* Ambos son servicios orientados al desarrollador.
* Ambos admiten lenguajes de script y de programación estándar.
* Ambos con compatibles con NuGet y NPM.

Las funciones es evolución natural de Hola de trabajos Web en que se toma mejores cosas acerca de WebJobs de Hola y mejora en ellos. Hola mejoras: 

* Pruebas de desarrollo simplificada y ejecución del código, directamente en el Explorador de Hola.
* Integración incorporada con más servicios de Azure y servicios de terceros como [GitHub WebHooks](https://developer.github.com/webhooks/creating/).
* Pago por uso, no toopay necesario para un [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* [Escalado dinámico](functions-scale.md)automático.
* Para los clientes existentes del servicio de aplicación, en ejecución en el plan de servicio de aplicaciones posible (tootake aprovechar los recursos en exceso).
* Integración con Logic Apps.

Hello en la tabla siguiente resume las diferencias de hello entre las funciones y los trabajos Web:

|  | Functions | Trabajos web |
| --- | --- | --- |
| Escalado |Escalado sin configuración |escalado con plan de App Service |
| Precios |Pago por uso o parte del plan de App Service |parte del plan de App Service |
| Tipo ejecución |desencadenada, programada (por desencadenador de temporizador) |desencadenada, continua, programada |
| Desencadenar eventos |[temporizador](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [Azure Event Hubs](functions-bindings-event-hubs.md), [HTTP/WebHook (GitHub, Slack)](functions-bindings-http-webhook.md), [Azure App Service Mobile Apps](functions-bindings-mobile-apps.md), [Azure Notification Hubs](functions-bindings-notification-hubs.md), [Azure Service Bus](functions-bindings-service-bus.md), [Azure Storage](functions-bindings-storage.md) |[Azure Storage](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Azure Service Bus](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Desarrollo en el explorador |admitido | no admitido |
| Scripts de ventana |experimental |admitido |
| PowerShell |experimental |admitido |
| C# |admitido |admitido |
| F# |admitido |no admitido |
| Bash |experimental |admitido |
| PHP |experimental |admitido |
| Python |experimental |admitido |
| JavaScript |admitido |admitido |

Si las funciones de toouse o trabajos Web depende en última instancia ya trabajar con el servicio de aplicaciones. Si tiene una aplicación de servicio de aplicaciones para el que desea que los fragmentos de código de toorun y desea que toomanage en ellos Hola mismo entorno de DevOps, debe usar trabajos Web. Si desea que los fragmentos de código de toorun para otros servicios de Azure o incluso 3rd terceros, o si desea demasiado administrar por separado los fragmentos de código de integración de aplicaciones de servicio de aplicaciones, o si desea toocall los fragmentos de código desde una aplicación de lógica, le conviene aprovechar de todas las mejoras de Hello en funciones.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, Logic Apps y Functions juntos
Como se mencionó anteriormente, servicio que es mejor tooyou adecuada depende de su situación. 

* Para una optimización empresarial sencilla, use Flow.
* Si su escenario de integración es demasiado avanzado para Flow, o si necesita funcionalidades de DevOps y cumplimiento de seguridad, use entonces Logic Apps.
* Si en uno de los pasos del escenario de integración hace falta una gran transformación personalizada o código especializado, escriba una aplicación de función y luego desencadene una función como una acción en la aplicación lógica.

Puede llamar a una aplicación lógica en un flujo. También puede llamar a una función en una aplicación lógica y a una aplicación lógica en una función. integración de Hello entre flujo, lógica de aplicaciones y funciones continuar tooimprove extra. Puede compilar algo en un servicio y utilizarlo en hello otros servicios. Por lo tanto, cualquier inversión que realice en estas tres tecnologías merecerá la pena.

## <a name="next-steps"></a>Pasos siguientes
Empezar a trabajar con cada uno de los servicios de hello mediante la creación de su primer flujo, aplicación lógica, aplicación de función o trabajo Web. Haga clic en cualquiera de los siguientes vínculos de hello:

* [Get started with Microsoft Flow](https://flow.microsoft.com/en-us/documentation/getting-started/) (Introducción a Microsoft Flow)
* [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Creación de su primera función de Azure](functions-create-first-azure-function.md)
* [Implementar trabajos web con Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

O bien, obtenga más información sobre estos servicios de integración con hello siguientes vínculos:

* [Leveraging Azure Functions &amp; Azure App Service for integration scenarios](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/) (Aprovechamiento de Azure Functions y Azure App Service para escenarios de integración) por Christopher Anderson
* [Integrations Made Simple](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Webcast en directo sobre Logic Apps](http://aka.ms/logicappslive)
* [Preguntas frecuentes sobre Microsoft Flow](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Recursos de documentación de WebJobs de Azure](../app-service-web/websites-webjobs-resources.md)

