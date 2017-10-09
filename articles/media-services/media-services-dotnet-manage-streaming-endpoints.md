---
title: "aaaManage puntos de conexión con el SDK de .NET de transmisión por secuencias. | Microsoft Docs"
description: "Este tema muestra cómo los extremos de streaming con toomanage Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="cdbb4-104">Administración de los puntos de conexión de streaming con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="cdbb4-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="cdbb4-105">Realizar seguro hello tooreview [Introducción](media-services-streaming-endpoints-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="cdbb4-106">Además, revise [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="cdbb4-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="cdbb4-107">código de Hello en este tema muestra cómo hello toodo siguiente las tareas con hello Azure Media Services .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="cdbb4-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="cdbb4-108">Examine predeterminado Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="cdbb4-109">Cree/agregue un nuevo punto de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="cdbb4-110">Es recomendable toohave varios extremos de streaming si tiene previsto toohave CDN diferente o una CDN y el acceso directo.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cdbb4-111">Solo se le cobrará cuando StreamingEndpoint esté en estado en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="cdbb4-112">Actualizar extremo de streaming de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="cdbb4-113">Asegúrese de que toocall Hola Update(), función.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="cdbb4-114">Eliminar Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="cdbb4-115">no se puede eliminar predeterminado Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="cdbb4-116">Para obtener información acerca de cómo tooscale Hola extremo de streaming, vea [esto](media-services-portal-scale-streaming-endpoints.md) tema.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="cdbb4-117">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdbb4-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="cdbb4-118">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cdbb4-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="cdbb4-119">Agregue código que administre los puntos de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="cdbb4-120">Reemplace el código de hello en hello Program.cs con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="cdbb4-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="cdbb4-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cdbb4-121">Next steps</span></span>
<span data-ttu-id="cdbb4-122">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="cdbb4-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cdbb4-123">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="cdbb4-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

