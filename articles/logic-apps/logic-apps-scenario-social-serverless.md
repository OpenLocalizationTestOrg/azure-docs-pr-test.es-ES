---
title: "aaaScenario - crear un panel de información del cliente con Azure sin servidor | Documentos de Microsoft"
description: "Un ejemplo de cómo puede crear a un cliente de toomanage panel comentarios, datos sociales y mucho más con funciones de Azure y Azure Logic Apps."
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
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Cree un panel de Customer Insights en tiempo real con Azure Logic Apps y Azure Functions

Azure tools sin servidor proporcionan a poderosas capacidades tooquickly compilación y aplicaciones host en nube de hello, sin tener toothink acerca de la infraestructura.  En este escenario, se crea un panel tootrigger los comentarios del cliente, analizar comentarios con aprendizaje automático y publicar información en un origen como Power BI o Azure Data Lake.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Información general del escenario de Hola y herramientas que se usan

En orden tooimplement esta solución, aprovechamos componentes clave de hello dos de las aplicaciones sin servidor de Azure: [funciones de Azure](https://azure.microsoft.com/services/functions/) y [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).

Lógica de aplicaciones es un motor de flujo de trabajo sin servidor en la nube de Hola.  Proporciona la orquestación en componentes sin servidor y también se conecta tooover 100 servicios y API.  En este escenario, crearemos un tootrigger de aplicación lógica en comentarios de los clientes.  Algunos de los conectores de Hola que pueden ayudar a los comentarios de toocustomer reaccionando incluyen Outlook.com, Office 365, encuesta mono, Twitter y una solicitud HTTP [desde un formulario web Forms](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Para el flujo de trabajo de Hola a continuación, se va a supervisar una hashtag en Twitter.

Las funciones proporcionan compute sin servidor en la nube de Hola.  En este escenario, se usará las funciones de Azure tooflag tweets desde los clientes basándose en una serie de palabras clave predefinidas.

puede ser la solución completa de Hello [compilar en Visual Studio](logic-apps-deploy-from-vs.md) y [implementado como parte de una plantilla de recursos](logic-apps-create-deploy-template.md).  También hay tutorial en vídeo del escenario de hello [en Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Compilar tootrigger de aplicación lógica de hello en los datos del cliente

Después de [crear una aplicación de lógica](logic-apps-create-a-logic-app.md) en Visual Studio o hello portal de Azure:

1. Agregue un desencadenador para **On New Tweets** (En los tweets nuevos) de Twitter
2. Configurar Hola desencadenador toolisten tootweets en una palabra clave o hashtag.

   > [!NOTE]
   > propiedad de periodicidad de Hello en el desencadenador de hello determinará la frecuencia con aplicación de lógica de hello busca nuevos elementos en los desencadenadores basados en sondeo

   ![Ejemplo de desencadenador de Twitter][1]

Esta aplicación se activará ante todos los tweets nuevos.  A continuación, podemos tomar datos tweet y comprender mejor opiniones Hola expresada.  Para ello se utilice hello [servicio cognitivos Azure](https://azure.microsoft.com/services/cognitive-services/) toodetect opiniones de texto.

1. Haga clic en **New Step** (Paso nuevo).
1. Seleccionar o buscar hello **análisis de texto** conector
1. Seleccione hello **detectar opiniones** operación
1. Si se le solicite, proporcione una clave de servicios cognitivos válida para el servicio de análisis de texto hello
1. Agregar hello **texto Tweet** como Hola tooanalyze de texto.

Ahora que tenemos datos tweet de Hola y visión en tweet hello, un número de otros conectores puede ser relevante:
* Power BI: agregar filas tooStreaming conjunto de datos: vista tweets tiempo real en un panel de Power BI.
* Azure Data Lake - anexar el archivo: agregar tooinclude del conjunto de datos de Azure Data Lake de cliente datos tooan en trabajos de análisis.
* SQL: agregar filas: almacenar datos en una base de datos para su posterior recuperación.
* Slack: Enviar mensaje: alertar a un canal de Slack sobre comentarios negativos que requieren acciones.

Una función de Azure también puede ser usado toodo más personalizada de proceso además de los datos de Hola.

## <a name="enriching-hello-data-with-an-azure-function"></a>Enriquecer datos Hola con una función de Azure

Antes de que podemos crear una función, debemos toohave una aplicación de la función en nuestra suscripción de Azure.  Puede obtener más información acerca de cómo crear una función de Azure en el portal de hello [encontrarse aquí](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Para una toobe función llamar directamente desde una aplicación de lógica, se necesita toohave HTTP desencadenar de enlace.  Se recomienda usar hello **HttpTrigger** plantilla.

En este escenario, cuerpo de la solicitud de Hola de hello Azure función sería texto tweet de hello.  En el código de la función hello, defina simplemente lógica en si el texto de los mensajes hello contiene una palabra clave o frase.  podría mantenerse propia función Hello como simples o complejas según sea necesario para el escenario de Hola.

Al final de Hola de función hello, simplemente devuelven una aplicación de lógica de respuesta toohello con algunos datos.  Puede tratarse de un valor booleano simple (p. ej. `containsKeyword`) o de un objeto complejo.

![Paso de función de Azure configurado][2]

> [!TIP]
> Cuando obtiene acceso a una respuesta compleja desde una función en una aplicación de lógica, use la acción de analizar el JSON de Hola.

Una vez que se guarda la función hello, y puede agregar en la aplicación de la lógica de hello creada anteriormente.  En la aplicación de la lógica de hello:

1. Haga clic en tooadd un **nuevo paso**
1. Seleccione hello **funciones de Azure** conector
1. Seleccione toochoose una función existente y examinar función toohello creada
1. Enviar en hello **Tweet texto** para hello **cuerpo de solicitud**

## <a name="running-and-monitoring-hello-solution"></a>Ejecutar y supervisar la solución de Hola

Una de las ventajas de Hola de orquestaciones sin servidor de aplicaciones de la lógica de creación es depuración enriquecido Hola y capacidades de supervisión.  Cualquier ejecución (actual o histórica) puede verse desde dentro de Visual Studio, Hola portal de Azure, o a través de hello REST API y SDK.

Una tootest de maneras más fácil una aplicación de la lógica de hello usa hello **ejecutar** botón en el Diseñador de Hola.  Haga clic en **ejecutar** continuará desencadenador de hello toopoll cada 5 segundos hasta que se detecta un evento y proporcionan una vista dinámica a medida que progresa de hello ejecutar.

Los historiales de ejecución anteriores pueden verse en la hoja de información general de Hola Hola portal de Azure o con hello Explorador de Visual Studio en la nube.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Creación de una plantilla de implementación para implementaciones automatizadas

Una vez que se ha desarrollado una solución, puede capturar e implementado a través de un tooany de plantilla de implementación de Azure región de Azure en Hola a todos.  Esto resulta útil no solo para modificar los parámetros de las diferentes versiones de este flujo de trabajo, sino también para integrar esta solución en una canalización de compilación y lanzamiento.  [En este artículo](logic-apps-create-deploy-template.md) se puede encontrar información acerca de cómo crear una plantilla de implementación.

Las funciones de Azure también se pueden incorporar en la plantilla de implementación de hello - para que toda la solución con todas las dependencias Hola puede administrarse como una única plantilla.  Un ejemplo de una plantilla de implementación de la función puede encontrarse en hello [repositorio de plantilla de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Pasos siguientes

* [Vea otros ejemplos y escenarios comunes de Azure Logic Apps](logic-apps-examples-and-scenarios.md)
* [Vea un tutorial en vídeo sobre la creación de esta solución de un extremo a otro](http://aka.ms/logicappsdemo)
* [Obtenga información acerca de cómo toohandle y catch excepciones dentro de una aplicación de lógica](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png