---
title: "Sondeo de operaciones de larga duración | Microsoft Docs"
description: "En este tema se muestra cómo sondear las operaciones de larga duración."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="8fddb-103">Entrega de transmisión en directo con Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="8fddb-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="8fddb-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8fddb-104">Overview</span></span>

<span data-ttu-id="8fddb-105">Servicios multimedia de Microsoft Azure ofrece determinadas API que envían solicitudes a los Servicios multimedia para iniciar operaciones (por ejemplo, crear, iniciar, detener o eliminar un canal).</span><span class="sxs-lookup"><span data-stu-id="8fddb-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="8fddb-106">Estas son operaciones de larga duración.</span><span class="sxs-lookup"><span data-stu-id="8fddb-106">These operations are long-running.</span></span>

<span data-ttu-id="8fddb-107">El SDK .NET de Servicios multimedia proporciona las API que envían la solicitud y esperan a que la operación se complete (internamente, las API sondean el progreso de la operación a intervalos determinados).</span><span class="sxs-lookup"><span data-stu-id="8fddb-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="8fddb-108">Por ejemplo, cuando se llama a channel.Start(), se devuelve el método después de que se inicie el canal.</span><span class="sxs-lookup"><span data-stu-id="8fddb-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="8fddb-109">También puede usar la versión asincrónica: await channel.StartAsync() (para obtener información sobre el patrón asincrónico basado en tareas, consulte [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="8fddb-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="8fddb-110">Las API que envían una solicitud de operación y, después, sondean el estado hasta que se completa la operación se llaman “métodos de sondeo”.</span><span class="sxs-lookup"><span data-stu-id="8fddb-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="8fddb-111">Estos métodos (sobre todo la versión asincrónica) se recomiendan para las aplicaciones cliente enriquecidas y para servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="8fddb-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="8fddb-112">En ciertos casos, una aplicación no puede esperar a una solicitud HTTP de ejecución prolongada y desea sondear el progreso de la operación manualmente.</span><span class="sxs-lookup"><span data-stu-id="8fddb-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="8fddb-113">Un ejemplo típico sería un explorador que interactúa con un servicio web sin estado: cuando el explorador solicita crear un canal, el servicio web inicia una operación de ejecución prolongada y devuelve el identificador de la operación al explorador.</span><span class="sxs-lookup"><span data-stu-id="8fddb-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="8fddb-114">A continuación, el explorador puede solicitar al servicio web que obtenga el estado de la operación en función del identificador.</span><span class="sxs-lookup"><span data-stu-id="8fddb-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="8fddb-115">El SDK .NET de Servicios multimedia proporciona las API que son útiles para este escenario.</span><span class="sxs-lookup"><span data-stu-id="8fddb-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="8fddb-116">Estas API se denominan “métodos sin sondeo”.</span><span class="sxs-lookup"><span data-stu-id="8fddb-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="8fddb-117">Los "métodos sin sondeo" tienen el siguiente modelo de nomenclatura: Send*OperationName*Operation (por ejemplo, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="8fddb-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="8fddb-118">Los métodos Send*OperationName*Operation devuelven el objeto **IOperation** ; el objeto devuelto contiene información que puede usarse para realizar un seguimiento de la operación.</span><span class="sxs-lookup"><span data-stu-id="8fddb-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="8fddb-119">Los métodos Send*OperationName*OperationAsync devuelven **Task<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="8fddb-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="8fddb-120">Las siguientes clases admiten métodos sin sondeo actualmente:  **Channel**, **StreamingEndpoint** y **Program**.</span><span class="sxs-lookup"><span data-stu-id="8fddb-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="8fddb-121">Para sondear el estado de la operación, use el método **GetOperation** en la clase **OperationBaseCollection**.</span><span class="sxs-lookup"><span data-stu-id="8fddb-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="8fddb-122">Use los siguientes intervalos para comprobar el estado de la operación: para las operaciones **Channel** y **StreamingEndpoint**, use 30 segundos; para las operaciones **Program**, use 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="8fddb-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8fddb-123">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fddb-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="8fddb-124">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8fddb-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="8fddb-125">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8fddb-125">Example</span></span>

<span data-ttu-id="8fddb-126">En el ejemplo siguiente se define una clase llamada **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="8fddb-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="8fddb-127">Esta definición de clase puede constituir un punto de partida para la definición de clase del servicio web.</span><span class="sxs-lookup"><span data-stu-id="8fddb-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="8fddb-128">Para simplificar, en los siguientes ejemplos se usan las versiones no asincrónicas de los métodos.</span><span class="sxs-lookup"><span data-stu-id="8fddb-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="8fddb-129">También se muestra cómo el cliente puede usar esta clase.</span><span class="sxs-lookup"><span data-stu-id="8fddb-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="8fddb-130">Definición de la clase ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="8fddb-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="the-client-code"></a><span data-ttu-id="8fddb-131">El código de cliente</span><span class="sxs-lookup"><span data-stu-id="8fddb-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="8fddb-132">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="8fddb-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8fddb-133">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="8fddb-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

