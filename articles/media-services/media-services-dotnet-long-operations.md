---
title: "Operaciones de larga duración aaaPolling | Documentos de Microsoft"
description: "Este tema se muestra cómo toopoll operaciones de larga duración."
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
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="1041b-103">Entrega de transmisión en directo con Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="1041b-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="1041b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1041b-104">Overview</span></span>

<span data-ttu-id="1041b-105">Servicios de multimedia de Microsoft Azure ofrece API que envían las solicitudes de operaciones de tooMedia Services toostart (por ejemplo: crear, iniciar, detener o eliminar un canal).</span><span class="sxs-lookup"><span data-stu-id="1041b-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="1041b-106">Estas son operaciones de larga duración.</span><span class="sxs-lookup"><span data-stu-id="1041b-106">These operations are long-running.</span></span>

<span data-ttu-id="1041b-107">Hola Media Services .NET SDK proporciona API que envían la solicitud de Hola y esperan Hola operación toocomplete (internamente, Hola API sondean el progreso de la operación a intervalos).</span><span class="sxs-lookup"><span data-stu-id="1041b-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="1041b-108">Por ejemplo, cuando se llama a canal. Start(), método hello devuelve una vez iniciado el canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1041b-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="1041b-109">También puede usar la versión asincrónica de hello: await canal. StartAsync() (para obtener información sobre el patrón asincrónico basado en tareas, consulte [pulse](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="1041b-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="1041b-110">Las API que envían una solicitud de operación y, a continuación, el sondeo de estado de hello hasta que se complete la operación de Hola se denominan "métodos de sondeo".</span><span class="sxs-lookup"><span data-stu-id="1041b-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="1041b-111">Estos métodos (especialmente versión de Async de Hola) se recomiendan para aplicaciones cliente enriquecidas y servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="1041b-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="1041b-112">Existen escenarios donde una aplicación no puede esperar una solicitud de http de ejecución prolongada y quiere toopoll para el progreso de la operación de hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="1041b-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="1041b-113">Un ejemplo típico sería un explorador que interactúa con un servicio web sin estado: al explorador Hola solicita toocreate un canal, servicio web de hello inicia una operación de ejecución prolongada y devuelve Hola Explorador de toohello de Id. de operación.</span><span class="sxs-lookup"><span data-stu-id="1041b-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="1041b-114">Explorador de Hello podría solicitarle entonces hello web tooget Hola operación estado del servicio según el identificador de Hola.</span><span class="sxs-lookup"><span data-stu-id="1041b-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="1041b-115">Hola Media Services .NET SDK proporciona API que son útiles para este escenario.</span><span class="sxs-lookup"><span data-stu-id="1041b-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="1041b-116">Estas API se denominan “métodos sin sondeo”.</span><span class="sxs-lookup"><span data-stu-id="1041b-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="1041b-117">"métodos sin sondeo" Hello tienen Hola seguir el patrón de nomenclatura: enviar*OperationName*operación (por ejemplo, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="1041b-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="1041b-118">Enviar*OperationName*métodos de operación devuelven hello **IOperation** objeto; hello objeto devuelto contiene información que puede ser usado tootrack Hola operación.</span><span class="sxs-lookup"><span data-stu-id="1041b-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="1041b-119">Hola envío*OperationName*OperationAsync métodos devuelven **tarea<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="1041b-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="1041b-120">Actualmente, Hola siguiendo métodos sin sondeo de soporte técnico de clases: **canal**, **StreamingEndpoint**, y **programa**.</span><span class="sxs-lookup"><span data-stu-id="1041b-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="1041b-121">toopoll de estado de la operación de hello, use hello **GetOperation** método en hello **OperationBaseCollection** clase.</span><span class="sxs-lookup"><span data-stu-id="1041b-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="1041b-122">Usar hello siguiendo el estado de la operación de intervalos toocheck Hola: para **canal** y **StreamingEndpoint** operaciones, use 30 segundos; para **programa** operaciones, utilice 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="1041b-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1041b-123">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1041b-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="1041b-124">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1041b-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="1041b-125">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1041b-125">Example</span></span>

<span data-ttu-id="1041b-126">Hello en el ejemplo siguiente se define una clase denominada **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="1041b-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="1041b-127">Esta definición de clase puede constituir un punto de partida para la definición de clase del servicio web.</span><span class="sxs-lookup"><span data-stu-id="1041b-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="1041b-128">Para simplificar, hello en los ejemplos siguientes utilizan versiones no asincrónicas de Hola de métodos.</span><span class="sxs-lookup"><span data-stu-id="1041b-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="1041b-129">ejemplo de Hola también muestra cómo el cliente de hello puede usar esta clase.</span><span class="sxs-lookup"><span data-stu-id="1041b-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="1041b-130">Definición de la clase ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="1041b-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
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
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
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
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
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

### <a name="hello-client-code"></a><span data-ttu-id="1041b-131">código de cliente Hello</span><span class="sxs-lookup"><span data-stu-id="1041b-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="1041b-132">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1041b-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1041b-133">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1041b-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

