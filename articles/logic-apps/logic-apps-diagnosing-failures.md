---
title: "errores de aaaDiagnose: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Toounderstand de formas comunes que se producen errores en las aplicaciones lógicas"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Diagnóstico de errores en las aplicaciones lógicas
Si experimenta problemas o errores con las aplicaciones lógicas, hay algunos enfoques puede ayudarle a entender mejor dónde proceden los errores de Hola.  

## <a name="azure-portal-tools"></a>Herramientas del Portal de Azure
Hola portal de Azure proporciona muchos toodiagnose herramientas cada aplicación lógica en cada paso.

### <a name="trigger-history"></a>Historial de desencadenamiento

Cada aplicación lógica tiene al menos un desencadenador. Si observa que las aplicaciones no están activación, buscan primero en el historial de desencadenador de Hola para obtener más información. Puede tener acceso a historial de desencadenador de hello en la hoja principal de hello lógica app'ss.

![Historial de desencadenador de localización Hola][1]

el historial de desencadenador de Hello enumera todos los intentos de desencadenador que realizan la lógica de aplicación. Puede hacer clic en cada toodrill de intento de desencadenador en los detalles de hello, en concreto, cualquier entradas o salidas que Hola intento de desencadenador generan. Si encuentra errores desencadenadores, seleccione el intento de desencadenador de Hola y elija hello **salidas** vincular tooreview cualquier error generado mensajes, por ejemplo, las credenciales de FTP que no son válidas.

Hola estados diferentes es posible que vea son:

* **Omitido**. punto de conexión de Hello era toocheck sondeo para los datos y recibe una respuesta que no había disponibles datos.
* **Correcto**. desencadenador de Hello recibió una respuesta que los datos estuvieran disponibles. Este estado podría proceder de un desencadenador manual, uno de periodicidad o uno de sondeo. Este estado suele ir acompañado hello **inicia** estado, pero podría no ser si tiene una condición o un comando de SplitOn en la vista de código que no se cumple.
* **Error**. Se generó un error.

#### <a name="start-a-trigger-manually"></a>Inicio manual de un desencadenador

Si desea toocheck de aplicación lógica de Hola para un desencadenador disponible inmediatamente sin esperar la siguiente periodicidad de hello, haga clic en **Seleccionar desencadenador** en hello hoja principal tooforce una comprobación. Por ejemplo, al hacer clic en este vínculo con un desencadenador de Dropbox hace que el sondeo de tooimmediately de flujo de trabajo de hello Dropbox para los nuevos archivos.

### <a name="run-history"></a>Historial de ejecuciones

Cada desencadenador que se activa produce una ejecución. Puede tener acceso a información de la ejecución de la hoja principal de hello, que contiene muchos detalles que pueden ayudarle a entender qué ha sucedido durante el flujo de trabajo de Hola.

![Buscar Hola historial de ejecución][2]

Una ejecución de muestra uno de hello siguientes estados:

* **Correcto**. Todas las acciones correctas. Si se produjo un error, dicho error se controlaba mediante una acción que se ha producido más adelante en el flujo de trabajo de Hola. Es decir, error de Hola se controlaba mediante una acción que se estableció toorun después de una acción de error.
* **Error**. Al menos una acción ha producido un error en el que no estaba controlado por una acción más adelante en el flujo de trabajo de Hola.
* **Cancelado**. flujo de trabajo de Hola se estaba ejecutando pero recibió una solicitud de cancelación.
* **En ejecución**. flujo de trabajo de saludo se está ejecutando actualmente. Este estado podría producirse para flujos de trabajo limitadas, o debido a Hola actual de plan de precios. Para obtener más información, consulte [límites de acción en la página de precios de hello](https://azure.microsoft.com/pricing/details/app-service/plans/). Configuración de diagnósticos (gráficos de Hola que aparecen en el historial de ejecución de hello) también puede proporcionar información sobre los eventos de limitación que se producen.

Cuando se encuentre ante un historial de ejecución, puede profundizar en él para obtener más detalles.  

#### <a name="trigger-outputs"></a>Salidas del desencadenador

Desencadenador genera mostrar datos de Hola que proceden de desencadenador de Hola. Estas salidas pueden ayudarle a determinar si se devolvieron todas las propiedades según lo previsto.

> [!NOTE]
> Si ve cualquier contenido que no conozca, aprenda cómo Azure Logic Apps [administra distintos tipos de contenido](../logic-apps/logic-apps-content-type.md).
> 

![Ejemplos de salidas del desencadenador][3]

#### <a name="action-inputs-and-outputs"></a>Entradas y salidas de acciones

Puede profundizar en hello entradas y salidas que recibió de una acción. Estos datos son útiles para entender el tamaño de Hola y la forma de salidas de Hola y también para buscar los mensajes de error que se han generado.

![Entradas y salidas de acciones][4]

## <a name="debug-workflow-runtime"></a>Depuración del flujo de trabajo en tiempo de ejecución

Junto con la supervisión Hola entradas, salidas y desencadenadores de una ejecución, puede agregar algunos flujos de trabajo de tooa de pasos que ayudan a depurar. 
[RequestBin](http://requestb.in) . Mediante el uso de RequestBin, puede configurar un tamaño exacto de HTTP solicitud inspector toodetermine hello, la forma y el formato de una solicitud HTTP. Puede crear un RequestBin y pegue la URL de hello en una aplicación de lógica acción HTTP POST con el contenido del cuerpo que desee tootest, por ejemplo, una expresión o salida del paso de otro. Después de ejecutar la aplicación de la lógica de hello, puede actualizar su toosee RequestBin cómo se formó solicitud hello cuando genera desde el motor de hello Logic Apps.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
