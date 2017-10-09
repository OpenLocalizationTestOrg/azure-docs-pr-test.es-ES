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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="18e7d-103">Escenario: Desencadenado de aplicaciones lógicas con Azure Functions y Service Bus</span><span class="sxs-lookup"><span data-stu-id="18e7d-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="18e7d-104">Puede usar las funciones de Azure toocreate un desencadenador para una aplicación de lógica cuando necesite toodeploy un agente de escucha de ejecución prolongada o tareas.</span><span class="sxs-lookup"><span data-stu-id="18e7d-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="18e7d-105">Por ejemplo, puede crear una función que escuche en una cola y que active inmediatamente una aplicación lógica como desencadenador de push.</span><span class="sxs-lookup"><span data-stu-id="18e7d-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="18e7d-106">Compilar la aplicación de la lógica de hello</span><span class="sxs-lookup"><span data-stu-id="18e7d-106">Build hello logic app</span></span>
<span data-ttu-id="18e7d-107">En este ejemplo, tiene una función que se ejecuta para cada aplicación de lógica que necesita toobe desencadena.</span><span class="sxs-lookup"><span data-stu-id="18e7d-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="18e7d-108">En primer lugar, cree una aplicación lógica que tenga un desencadenador de solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="18e7d-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="18e7d-109">función Hello llama a ese punto de conexión cada vez que se recibe un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="18e7d-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="18e7d-110">Cree una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="18e7d-110">Create a logic app.</span></span>
2. <span data-ttu-id="18e7d-111">Seleccione hello **Manual: cuando se recibe una solicitud HTTP** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="18e7d-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="18e7d-112">Si lo desea, puede especificar un toouse de esquema JSON con el mensaje de bienvenida de cola mediante una herramienta como [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="18e7d-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="18e7d-113">Esquema de hello pegar en desencadenador Hola.</span><span class="sxs-lookup"><span data-stu-id="18e7d-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="18e7d-114">Esquemas para comprender el Diseñador de hello forma Hola de propiedades de datos y el flujo de hello más fácilmente a través de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e7d-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="18e7d-115">Agregue todos los pasos adicionales que desee toooccur después de que se recibe un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="18e7d-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="18e7d-116">Por ejemplo, enviar un correo electrónico a través de Office 365.</span><span class="sxs-lookup"><span data-stu-id="18e7d-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="18e7d-117">Guardar Hola lógica toogenerate Hola devolución de llamada dirección URL de aplicación para la aplicación de lógica de hello desencadenador toothis.</span><span class="sxs-lookup"><span data-stu-id="18e7d-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="18e7d-118">dirección URL de Hello aparece en la tarjeta de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e7d-118">hello URL appears on hello trigger card.</span></span>

![dirección URL de devolución de llamada de Hello aparece en la tarjeta de desencadenador de Hola][1]

## <a name="build-hello-function"></a><span data-ttu-id="18e7d-120">Crear función hello</span><span class="sxs-lookup"><span data-stu-id="18e7d-120">Build hello function</span></span>
<span data-ttu-id="18e7d-121">A continuación, debe crear una función que actúa como desencadenador de Hola y escucha de cola de toohello.</span><span class="sxs-lookup"><span data-stu-id="18e7d-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="18e7d-122">Hola [portal de Azure funciones](https://functions.azure.com/signin), seleccione **nueva función**y, a continuación, seleccione hello **ServiceBusQueueTrigger - C#** plantilla.</span><span class="sxs-lookup"><span data-stu-id="18e7d-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portal de Funciones de Azure][2]
2. <span data-ttu-id="18e7d-124">Configurar la cola de Bus de servicio de toohello de conexión hello, que usa Hola SDK del Bus de servicio de Azure `OnMessageReceive()` agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="18e7d-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="18e7d-125">Escribir un extremo de aplicación función básica toocall Hola lógica (creado anteriormente) mediante mensaje de bienvenida de cola como un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="18e7d-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="18e7d-126">Este es un ejemplo completo de una función.</span><span class="sxs-lookup"><span data-stu-id="18e7d-126">Here's a full example of a function.</span></span> <span data-ttu-id="18e7d-127">ejemplo de Hola se usa un `application/json` tipo de contenido de mensaje, pero puede cambiar este tipo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="18e7d-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="18e7d-128">tootest, agregar un mensaje de la cola a través de una herramienta como [Explorador de Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="18e7d-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="18e7d-129">Consulte aplicación de lógica de hello activarse inmediatamente después de función hello recibe el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="18e7d-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
