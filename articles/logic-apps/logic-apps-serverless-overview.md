---
title: aaaOverview de Azure sin servidor | Documentos de Microsoft
description: Crear soluciones eficaces en la nube de hello sin tener toothink acerca de la infraestructura.
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Introducción a Azure sin servidor con Functions y Logic Apps

Las aplicaciones sin servidor proporcionan las ventajas de aumento en la velocidad de desarrollo, reducción del código necesario y simplicidad con la escala.  En este artículo entra en diferentes atributos de Hola de soluciones sin servidor, ofertas y de Azure sin servidor.

## <a name="what-is-serverless"></a>¿Qué significa sin servidor?

Sin servidor no significa que no hay ningún servidor: simplemente significa desarrollador hello no tiene tooworry acerca de los servidores.  Gran parte del desarrollo de aplicaciones tradicionales es responder a preguntas acerca de la escala, hospedaje y la supervisión exigencias de hello toomeet de soluciones de aplicación hello.  Con Serverless, estas preguntas se ocupa de como parte de la solución de Hola.  Además, las aplicaciones sin servidor se facturan según un plan de consumo.  Si nunca se utiliza la aplicación hello, nunca se incurre en un cargo.  Estas características permiten a los desarrolladores toofocus solamente en la lógica de negocios de Hola de solución de Hola.

servicios centrales de Hello en Azure alrededor Serverless son [funciones de Azure](https://azure.microsoft.com/services/functions/) y [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).  Ambas soluciones siguen principios de hello anteriores y permiten a los desarrolladores de aplicaciones en la nube sólida toobuild con código mínimo.

## <a name="what-are-azure-functions"></a>¿Qué es Azure Functions?

Las funciones de Azure es una solución para ejecutar fácilmente pequeños fragmentos de código, o "funciones", en la nube de Hola. Puede escribir solo el código de hello que necesarios para el problema de hello en cuestión, sin preocuparse un toorun de infraestructura de aplicación o hello todo lo. Functions puede hacer que el desarrollo sea aún más productivo y, además, le permite utilizar el lenguaje de desarrollo que prefiera, como C#, F#, Node.js, Python o PHP. Solo paga por tiempo Hola que se ejecuta el código y Azure escala según sea necesario.

Si desea que right toojump y empezar a trabajar con funciones de Azure, comience con [crear su primera función Azure](../azure-functions/functions-create-first-azure-function.md). Si desea obtener más información técnica acerca de las funciones, vea hello [material de referencia](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>¿Qué es Azure Logic Apps?

Aplicaciones lógicas de Azure proporciona una manera toosimplify e implementar integraciones escalables y flujos de trabajo en la nube de Hola. Proporciona un toomodel diseñador visual y automatizar el proceso como una serie de pasos que se llama a un flujo de trabajo.  Hay [muchos conectores](../connectors/apis-list.md) a través de servicios de nube y locales tooquickly conectarse un tooother de aplicación sin servidor API.  Una aplicación lógica comienza con un desencadenador (igual que 'cuando se agrega una cuenta tooDynamics CRM') y después de activación puede empezar a muchas acciones de combinaciones, conversiones y lógica de la condición.  Lógica de aplicaciones es una excelente opción cuando orquestar diferentes funciones de Azure en un proceso - especialmente cuando el proceso de hello requiere interactuar con un sistema externo o la API.

tooget se inició a las aplicaciones lógicas, empiece con [crear su primera aplicación de lógica](logic-apps-create-a-logic-app.md).  Si desea obtener más información técnica acerca de las aplicaciones lógicas, consulte hello [material de referencia](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>¿Cómo puedo crear e implementar aplicaciones sin servidor en Azure?

Azure proporciona un conjunto abundante de herramientas para el desarrollo, la implementación y la administración de aplicaciones sin servidor.  Las aplicaciones pueden crearse directamente en el portal de Azure de Hola o con [herramientas de Visual Studio](logic-apps-serverless-get-started-vs.md).  Una vez que se ha desarrollado una aplicación, se puede [implementar al instante](logic-apps-create-deploy-template.md).  Azure también proporciona supervisión para aplicaciones sin servidor.  Esta supervisión puede tener acceso desde Hola portal de Azure, a través de API de Hola o SDK, o con tooOMS de herramientas integrado y Application Insights.

## <a name="next-steps"></a>Pasos siguientes

* [Introducción a la creación de una aplicación sin servidor en Visual Studio](logic-apps-serverless-get-started-vs.md)
* [Creación de un panel de Customer Insights con una aplicación sin servidor](logic-apps-scenario-social-serverless.md)
* [Creación de una plantilla de implementación para una aplicación lógica](logic-apps-create-deploy-template.md)