---
title: "aplicaciones de aaaConnect e integrar los datos con flujos de trabajo: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Creación de flujos de trabajo y automatización de procesos mediante la conexión de aplicaciones y la integración de datos en Azure Logic Apps."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>¿Qué es Logic Apps?
Las aplicaciones lógicas proporcionan una manera toosimplify e implementan integraciones escalables y flujos de trabajo en la nube de Hola. Proporciona un toomodel diseñador visual y automatizar el proceso como una serie de pasos que se conoce como un flujo de trabajo.  Hay [muchos conectores](../connectors/apis-list.md) a través de hello en la nube y locales tooquickly integrarse en los servicios y protocolos.  Una aplicación lógica comienza con un desencadenador (igual que 'cuando se agrega una cuenta tooDynamics CRM') y después de activación puede empezar a muchas combinaciones de acciones, conversiones y condición lógica.

ventajas de Hello del uso de las aplicaciones lógicas Hola siguientes:  

* Ahorro de tiempo al diseñar procesos complejos con herramientas de diseño de fácil toounderstand
* Implementación de patrones y flujos de trabajo sin problemas, que de otro modo sería difícil tooimplement en código
* Introducción rápida desde plantillas
* Personalización de aplicaciones lógicas con API, código y acciones propios
* Conectarse y sincronizar sistemas dispares entre locales y hello en la nube
* Generación del servidor de BizTalk, API Management, Azure Functions y Azure Service Bus compatible con integración de primera clase

La lógica de aplicaciones es un iPaaS totalmente administrados (integración de plataforma como servicio) que permite a los desarrolladores no toohave tooworry sobre la creación de hospedaje, escalabilidad, disponibilidad y administración.  Lógica de aplicaciones se escalará la petición de toomeet automáticamente.

![Diseñador de aplicación de flujo](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Como se ha mencionado, con Logic Apps puede automatizar procesos empresariales. Estos son algunos ejemplos:  

* Mover el servidor FTP tooan de cargar archivos en el almacenamiento de Azure
* Procesamiento y redirección de pedidos de sistemas locales y en la nube
* Supervisar todos los tuits acerca de un tema determinado, analizar opiniones de Hola y crear alertas y las tareas para los elementos que necesitan seguimiento.

Escenarios como los siguientes se pueden configurar desde el diseñador visual de Hola y sin escribir una sola línea de código. Comience a [crear una aplicación lógica ahora][create].  Una vez escritas, las aplicaciones lógicas [se implementan rápidamente y se vuelven a configurar](../logic-apps/logic-apps-create-deploy-template.md) en varios entornos y regiones.

## <a name="why-logic-apps"></a>¿Por qué Logic Apps?
Lógica de aplicaciones pone la velocidad y la escalabilidad en espacio de integración empresarial Hola.  facilidad de Hola de uso del Diseñador de hello, variedad de desencadenadores, acciones y herramientas de administración eficaces de realizar centralizar las API más sencillas que nunca.  Como las empresas se desplazan hacia la digitalización, Logic Apps permite tooconnect heredado y vanguardistas sistemas juntos.

Además, con nuestras [cuenta de integración de Enterprise] [ biztalk] puede escalar los escenarios de integración de toomature la potencia de Hola de un [mensajería XML] [ xml], [administración de socios comerciales][tpm]y mucho más.

* **Herramientas de diseño de fácil toouse** -Logic Apps puede ser diseñado-to-end en el Explorador de Hola o con herramientas de Visual Studio. Comience con un desencadenador: desde un toowhen de programación simple, que se crea un problema de GitHub. A continuación, coordinar cualquier número de acciones mediante la Galería enriquecido Hola de conectores.
* **Conectar con facilidad las API** -tareas de composición incluso toodescribe fácil son difíciles de tooimplement en el código. Lógica de aplicaciones resulta fácil tooconnect diversos sistemas. ¿Desea tooconnect en la nube de solución de marketing tooyour sistema de facturación local? ¿Desea toocentralize mensajería a través de las API y los sistemas con un Bus de servicio empresarial? Las aplicaciones lógicas son hello más rápidas y confiables de manera toodeliver soluciones toothese problemas.
* **Empezar a trabajar rápidamente desde plantillas** -toohelp comenzar hemos proporcionado un [Galería de plantillas de] [ templates] que le permiten toorapidly crear algunas soluciones comunes. De soluciones avanzadas de B2B toosimple conectividad de SaaS y que incluso unos son 'para divertirse' - Galería hello es tooget de manera más rápida de hello inició la potencia de Hola de lógica de aplicaciones.
* **¿Extensibilidad preparadas** -no ve el conector de hello necesita? La lógica de aplicaciones es toowork diseñada con su propia API y el código; puede crear su propios toouse de aplicación de API como un conector personalizado fácilmente o llamar a un [función Azure](https://functions.azure.com) tooexecute fragmentos de código a petición. 
* **Eficacia de integración real** : empiece por algo sencillo y crezca a medida que sea necesario. Lógica de aplicaciones fácilmente puede aprovechar la eficacia de Hola de BizTalk, sector iniciales solución tooenable integración profesionales toobuild Hola soluciones de integración de Microsoft que necesitan. Obtener más información acerca de hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Conceptos de aplicaciones lógicas
siguiente Hola es algunos de los elementos clave de Hola que conforman la experiencia de las aplicaciones lógicas de Hola. 

* **Flujo de trabajo** -Logic Apps proporciona una manera gráfica toomodel sus procesos empresariales como una serie de pasos o un flujo de trabajo.
* **Administrar conectores** -necesitan tener acceso a las aplicaciones lógicas toodata y servicios. Conectores administrados se crean específicamente tooaid vez que se va a conectar tooand trabajar con los datos. Ver lista de Hola de conectores está disponibles ahora en [administrado conectores][managedapis].
* **Desencadenadores** : algunos conectores administrados también pueden hacer de desencadenador. Un desencadenador, inicia una nueva instancia de un flujo de trabajo en función de un evento concreto, como la llegada de Hola de un correo electrónico o a un cambio en la cuenta de almacenamiento de Azure.
* **Acciones** -cada paso después de llama a una acción de desencadenador de hello en un flujo de trabajo. Cada acción asigna normalmente tooan operación en el conector administrado o aplicaciones de API personalizadas.
* **Enterprise Integration Pack**: para escenarios más avanzados de integración, Logic Apps incluye funcionalidades de BizTalk. BizTalk es la plataforma de integración líder del sector de Microsoft. los conectores de paquete de integración empresarial Hola permiten tooeasily incluye validación, transformación y mucho más en flujos de trabajo de aplicación lógica de tooyour.

## <a name="getting-started"></a>Introducción
* tooget partió Logic Apps, siga hello [crear una aplicación de la lógica de] [ create] tutorial.  
* [Ejemplos de aplicaciones lógicas y escenarios comunes](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Con las aplicaciones lógicas puede automatizar procesos empresariales.](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Obtenga información acerca de cómo tooIntegrate los sistemas con las aplicaciones lógicas](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
