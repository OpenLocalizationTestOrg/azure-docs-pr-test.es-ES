---
title: "código de aaaCustom para las aplicaciones de la lógica de Azure con funciones de Azure | Documentos de Microsoft"
description: "Cree y ejecute código personalizado para Azure Logic Apps con Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Adición y ejecución de código personalizado para aplicaciones lógicas con Azure Functions

toorun fragmentos de código personalizado de C# o node.js en las aplicaciones lógicas, puede crear funciones personalizadas a través de funciones de Azure. 
[Azure Functions](../azure-functions/functions-overview.md) ofrece una computación sin servidor en Microsoft Azure y es útil para realizar estas tareas:

* Formato o proceso avanzados de los campos de Logic Apps.
* Realización de cálculos en un flujo de trabajo.
* Ampliar la funcionalidad de la aplicación hello lógica con funciones que se admiten en C# o node.js

## <a name="create-custom-functions-for-your-logic-apps"></a>Creación de funciones personalizadas para las aplicaciones lógicas

Le recomendamos que cree una función en portal de Azure funciones hello, de hello **Webhook genérico - nodo** o **Webhook genérico - C#** plantillas. resultado de Hello crea un rellena automáticamente una plantilla que acepta `application/json` desde una aplicación de lógica. Las funciones que cree a partir de estas plantillas se detectan automáticamente y aparecen en hello Diseñador de la aplicación lógica en **funciones de Azure en mi región.**

En el portal de Azure, en Hola Hola **integrar** panel de la función, la plantilla debe mostrar que **modo** establecido demasiado**Webhook** y **Webhook tipo** se establece demasiado**JSON genérico**. 

Funciones de Webhook Aceptar una solicitud y lo pasa en el método de Hola a través de un `data` variable. Puede tener acceso a propiedades de saludo de la carga mediante el uso de la notación de puntos como `data.function-name`. Por ejemplo, una función de JavaScript simple que convierte un valor de fecha y hora en una cadena de fecha aspecto Hola siguiente ejemplo:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Llamada a Azure Functions desde Logic Apps

contenedores de hello toolist en su suscripción y la función hello select que desea toocall, en el Diseñador de la aplicación de lógica, haga clic en hello **acciones** menú y seleccione desde **funciones de Azure en mi región**.

Después de seleccionar la función hello, es más frecuentes toospecify un objeto de carga de la entrada. Este objeto es mensaje Hola Hola lógica aplicación envía toohello función y debe ser un objeto JSON. Por ejemplo, si desea toopass Hola **última modificación** fecha desde un desencadenador de Salesforce, carga de función hello podría ser similar a este ejemplo:

![Fecha de última modificación][1]

## <a name="trigger-logic-apps-from-a-function"></a>Desencadenamiento de aplicaciones lógicas desde una función

Una aplicación lógica se puede desencadenar desde dentro de una función. Consulte [Aplicaciones lógicas como puntos de conexión invocables](logic-apps-http-endpoint.md). Crear una aplicación de lógica que tiene un desencadenador manual y, a continuación, desde dentro de la función, generar una dirección URL de desencadenador manual de HTTP POST toohello con una carga de Hola que desee enviar la aplicación de la lógica de toohello.

### <a name="create-a-function-from-logic-app-designer"></a>Creación de una función en el Diseñador de aplicaciones lógicas

También puede crear una función de webhook de node.js desde el Diseñador de Hola. En primer lugar, seleccione **Azure Functions in my region** (Funciones de Azure en mi región) y elija un contenedor para la función. Si aún no tiene un contenedor, deberá toocreate de hello [portal de Azure funciones](https://functions.azure.com/signin). Seleccione **Crear nuevo**.  

toogenerate una plantilla basada en datos de saludo que desea que toocompute, especifique el objeto de contexto de Hola que planea toopass a una función. que debe ser un objeto JSON. Por ejemplo, si se pasa el contenido del archivo de Hola desde una acción de FTP, carga de contexto de hello es similar en este ejemplo:

![Carga de contexto][2]

> [!NOTE]
> Dado que este objeto no se ha convertido en una cadena, contenido de Hola se agrega directamente toohello carga JSON. Sin embargo, se produce un error si el objeto de hello no es un token JSON (es decir, una cadena o una JSON/matriz de objetos). objeto de hello toocast como una cadena, agregar comillas tal y como se muestra en la primera ilustración de hello en este artículo.
> 

Diseñador de Hello, a continuación, genera una plantilla de función que se puede crear en línea. Las variables se crean previamente basándose en el contexto de Hola que planea toopass en función de Hola.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
