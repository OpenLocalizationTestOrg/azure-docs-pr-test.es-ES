---
title: aaaExamples & comunes escenarios - Azure Logic Apps | Documentos de Microsoft
description: "Más información sobre las aplicaciones lógicas con ejemplos, escenarios y tutoriales"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Ejemplos y escenarios comunes de Azure Logic Apps

toohelp obtener más información acerca de Hola muchos patrones y capacidades en las aplicaciones lógicas de Azure, estos son ejemplos y escenarios comunes.

## <a name="key-scenarios-for-logic-apps"></a>Escenarios clave de aplicaciones lógicas

Azure Logic Apps ofrece orquestación resistente e integración para los distintos servicios. Hola servicio Logic Apps es "sin servidor", por lo que no tienes tooworry acerca de la escala o instancias, ya que todo lo que tener toodo es definir hello y flujo de trabajo (desencadenador acciones). la plataforma subyacente Hola controla la escalabilidad, disponibilidad y rendimiento. Cualquier escenario donde sea necesario toocoordinate varias acciones, especialmente entre varios sistemas, es un buen caso de uso para las aplicaciones lógicas de Azure. A continuación puede ver algunos patrones y ejemplos.

## <a name="respond-tootriggers-and-extend-actions"></a>Responder tootriggers y ampliar acciones

Cada aplicación lógica comienza con un desencadenador. Por ejemplo, puede iniciar el flujo de trabajo con un evento de programación, una invocación manual o un evento desde un sistema externo, como Hola desencadenador "cuando se agrega un archivo tooan FTP server". Aplicaciones lógicas de Azure admite actualmente más de 100 conectores listos para usar, comprendido entre locales SAP tooMicrosoft servicios cognitivos. En el caso de los sistemas y servicios que podrían no tener conectores publicados, también puede extender las aplicaciones lógicas.

* [Creación de desencadenadores o acciones personalizadas](../logic-apps/logic-apps-create-api-app.md)
* [Configuración de acciones de ejecución prolongada para ejecuciones de flujo de trabajo](../logic-apps/logic-apps-create-api-app.md)
* [Responder tooexternal eventos y acciones de webhook](../logic-apps/logic-apps-create-api-app.md)
* [Llamar a, desencadenador, o anidar los flujos de trabajo con las respuestas sincrónicas tooHTTP solicitudes](../logic-apps/logic-apps-http-endpoint.md)
* [Tutorial: Responder tooTwilio SMS webhooks y enviar una respuesta de texto](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI](http://aka.ms/logicappsdemo) (Tutorial: Crear un panel social con tecnología de AI en minutos con Logic Apps y Power BI)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Funcionalidades de flujo de control, registros y control de errores

Las aplicaciones lógicas incluyen amplias funciones de flujo de control avanzado, como condiciones, modificadores, bucles y ámbitos. tooensure soluciones resistente, también se pueden implementar de errores y control de excepciones en los flujos de trabajo. Para los registros de notificación y diagnóstico del estado de ejecución del flujo de trabajo, Azure Logic Apps también ofrece supervisión y alertas.

* [Uso de acciones distintas con instrucciones switch](../logic-apps/logic-apps-switch-case.md)
* [Proceso de elementos en matrices y colecciones con bucles y lotes en aplicaciones lógicas](../logic-apps/logic-apps-loops-and-scopes.md)
* [Creación de control de errores y excepciones en un flujo de trabajo](../logic-apps/logic-apps-exception-handling.md)
* [Supervisar el estado, configurar el registro de diagnósticos y activar alertas para Azure Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Turn on monitoring and diagnostics logging when creating logic apps](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md) (Activación de la supervisión y el registro de diagnóstico al crear aplicaciones lógicas)
* [Caso de uso: Cómo una empresa de atención sanitaria usa el control de excepciones de aplicaciones lógicas para los flujos de trabajo de HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Implementación y administración de aplicaciones lógicas

Puede desarrollar e implementar aplicaciones lógicas completamente con Visual Studio, Visual Studio Team Services o cualquier otra herramienta de compilación automatizada o de control de código fuente. implementación de toosupport para los flujos de trabajo y las conexiones dependientes en una plantilla de recursos, las aplicaciones lógicas de usan plantillas de implementación de recursos de Azure. Herramientas de Visual Studio generan automáticamente estas plantillas, que puede comprobar en el control de toosource para control de versiones.

* [Creación de una plantilla de implementación automatizada](../logic-apps/logic-apps-create-deploy-template.md)
* [Creación e implementación de aplicaciones lógicas en Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Supervisar el estado de Hola de las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Tipos de contenido, conversiones y transformaciones dentro de una ejecución

Puede tener acceso a, convertir y transformar varios tipos de contenido mediante el uso de hello muchas funciones de hello Azure Logic Apps [lenguaje de definición de flujo de trabajo](http://aka.ms/logicappsdocs). Por ejemplo, puede convertir entre una cadena, JSON y XML con hello `@json()` y `@xml()` expresiones de flujo de trabajo. motor de Logic Apps Hola conserva a la transferencia de contenido de toosupport de tipos de contenido de una manera sin pérdida de datos entre los servicios.

* [Administración de los tipos de contenido no JSON](../logic-apps/logic-apps-content-type.md), como `application/xml`, `application/octet-stream` y `multipart/formdata`
* [Funcionamiento de las expresiones de flujo de trabajo en las aplicaciones lógicas](../logic-apps/logic-apps-author-definitions.md)
* [Referencia: Lenguaje de definición de flujo de trabajo de Azure Logic Apps](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Otras integraciones y funcionalidades

Las aplicaciones lógicas también ofrecen integración con muchos servicios, como Azure Functions, Azure API Management, Azure App Services y puntos de conexión HTTP personalizados, por ejemplo, REST y SOAP.

* [Creación de un panel de redes sociales en tiempo real y sin servidor con Azure](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Llamada a Azure Functions desde aplicaciones lógicas](../logic-apps/logic-apps-azure-functions.md)
* [Escenario: Desencadenamiento de aplicaciones lógicas con Azure Functions](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog: Call SOAP endpoints from logic apps](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/) (Blog: Llamada a puntos de conexión SAP desde aplicaciones lógicas)

## <a name="end-to-end-scenarios"></a>Escenarios de un extremo a otro

* [Notas del producto: Administración de un caso completo de integración empresarial con servicios de Azure, como Logic Apps](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>Pasos siguientes

- [Control de errores y excepciones en aplicaciones lógicas](../logic-apps/logic-apps-exception-handling.md)
- [Crear definiciones de flujo de trabajo con el lenguaje de definición de flujo de trabajo de Hola](../logic-apps/logic-apps-author-definitions.md)
- [Envío de comentarios, preguntas o sugerencias sobre cómo podemos mejorar Azure Logic Apps](https://feedback.azure.com/forums/287593-logic-apps)