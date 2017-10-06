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
# <a name="delivering-live-streaming-with-azure-media-services"></a>Entrega de transmisión en directo con Servicios multimedia de Azure

## <a name="overview"></a>Información general

Servicios de multimedia de Microsoft Azure ofrece API que envían las solicitudes de operaciones de tooMedia Services toostart (por ejemplo: crear, iniciar, detener o eliminar un canal). Estas son operaciones de larga duración.

Hola Media Services .NET SDK proporciona API que envían la solicitud de Hola y esperan Hola operación toocomplete (internamente, Hola API sondean el progreso de la operación a intervalos). Por ejemplo, cuando se llama a canal. Start(), método hello devuelve una vez iniciado el canal de Hola. También puede usar la versión asincrónica de hello: await canal. StartAsync() (para obtener información sobre el patrón asincrónico basado en tareas, consulte [pulse](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). Las API que envían una solicitud de operación y, a continuación, el sondeo de estado de hello hasta que se complete la operación de Hola se denominan "métodos de sondeo". Estos métodos (especialmente versión de Async de Hola) se recomiendan para aplicaciones cliente enriquecidas y servicios con estado.

Existen escenarios donde una aplicación no puede esperar una solicitud de http de ejecución prolongada y quiere toopoll para el progreso de la operación de hello manualmente. Un ejemplo típico sería un explorador que interactúa con un servicio web sin estado: al explorador Hola solicita toocreate un canal, servicio web de hello inicia una operación de ejecución prolongada y devuelve Hola Explorador de toohello de Id. de operación. Explorador de Hello podría solicitarle entonces hello web tooget Hola operación estado del servicio según el identificador de Hola. Hola Media Services .NET SDK proporciona API que son útiles para este escenario. Estas API se denominan “métodos sin sondeo”.
"métodos sin sondeo" Hello tienen Hola seguir el patrón de nomenclatura: enviar*OperationName*operación (por ejemplo, SendCreateOperation). Enviar*OperationName*métodos de operación devuelven hello **IOperation** objeto; hello objeto devuelto contiene información que puede ser usado tootrack Hola operación. Hola envío*OperationName*OperationAsync métodos devuelven **tarea<IOperation>**.

Actualmente, Hola siguiendo métodos sin sondeo de soporte técnico de clases: **canal**, **StreamingEndpoint**, y **programa**.

toopoll de estado de la operación de hello, use hello **GetOperation** método en hello **OperationBaseCollection** clase. Usar hello siguiendo el estado de la operación de intervalos toocheck Hola: para **canal** y **StreamingEndpoint** operaciones, use 30 segundos; para **programa** operaciones, utilice 10 segundos.

## <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se define una clase denominada **ChannelOperations**. Esta definición de clase puede constituir un punto de partida para la definición de clase del servicio web. Para simplificar, hello en los ejemplos siguientes utilizan versiones no asincrónicas de Hola de métodos.

ejemplo de Hola también muestra cómo el cliente de hello puede usar esta clase.

### <a name="channeloperations-class-definition"></a>Definición de la clase ChannelOperations

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

### <a name="hello-client-code"></a>código de cliente Hello
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



## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

