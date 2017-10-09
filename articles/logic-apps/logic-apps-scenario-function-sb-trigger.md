---
title: "aaaScenario - desencadenador lógica aplicaciones con funciones de Azure y Azure Service Bus | Documentos de Microsoft"
description: "Crear una aplicación de lógica de una función tootrigger mediante las funciones de Azure y Azure Service Bus"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Escenario: Desencadenado de aplicaciones lógicas con Azure Functions y Service Bus

Puede usar las funciones de Azure toocreate un desencadenador para una aplicación de lógica cuando necesite toodeploy un agente de escucha de ejecución prolongada o tareas. Por ejemplo, puede crear una función que escuche en una cola y que active inmediatamente una aplicación lógica como desencadenador de push.

## <a name="build-hello-logic-app"></a>Compilar la aplicación de la lógica de hello
En este ejemplo, tiene una función que se ejecuta para cada aplicación de lógica que necesita toobe desencadena. En primer lugar, cree una aplicación lógica que tenga un desencadenador de solicitud HTTP. función Hello llama a ese punto de conexión cada vez que se recibe un mensaje de la cola.  

1. Cree una aplicación lógica.
2. Seleccione hello **Manual: cuando se recibe una solicitud HTTP** desencadenador.
   Si lo desea, puede especificar un toouse de esquema JSON con el mensaje de bienvenida de cola mediante una herramienta como [jsonschema.net](http://jsonschema.net). Esquema de hello pegar en desencadenador Hola. Esquemas para comprender el Diseñador de hello forma Hola de propiedades de datos y el flujo de hello más fácilmente a través de flujo de trabajo de Hola.
2. Agregue todos los pasos adicionales que desee toooccur después de que se recibe un mensaje de la cola. Por ejemplo, enviar un correo electrónico a través de Office 365.  
3. Guardar Hola lógica toogenerate Hola devolución de llamada dirección URL de aplicación para la aplicación de lógica de hello desencadenador toothis. dirección URL de Hello aparece en la tarjeta de desencadenador de Hola.

![dirección URL de devolución de llamada de Hello aparece en la tarjeta de desencadenador de Hola][1]

## <a name="build-hello-function"></a>Crear función hello
A continuación, debe crear una función que actúa como desencadenador de Hola y escucha de cola de toohello.

1. Hola [portal de Azure funciones](https://functions.azure.com/signin), seleccione **nueva función**y, a continuación, seleccione hello **ServiceBusQueueTrigger - C#** plantilla.
   
    ![portal de Funciones de Azure][2]
2. Configurar la cola de Bus de servicio de toohello de conexión hello, que usa Hola SDK del Bus de servicio de Azure `OnMessageReceive()` agente de escucha.
3. Escribir un extremo de aplicación función básica toocall Hola lógica (creado anteriormente) mediante mensaje de bienvenida de cola como un desencadenador. Este es un ejemplo completo de una función. ejemplo de Hola se usa un `application/json` tipo de contenido de mensaje, pero puede cambiar este tipo según sea necesario.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, agregar un mensaje de la cola a través de una herramienta como [Explorador de Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer). Consulte aplicación de lógica de hello activarse inmediatamente después de función hello recibe el mensaje de bienvenida.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
