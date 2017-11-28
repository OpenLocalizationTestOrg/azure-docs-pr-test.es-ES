---
title: "Configuración de la telemetría de Azure Media Services con .NET | Microsoft Docs"
description: "En este artículo se muestra cómo usar la telemetría de Azure Media Services mediante el SDK de .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 1d857f3d062d8d1b15c64fa4b8c3e27ad6c2247e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="9b37d-103">Configuración de la telemetría de Azure Media Services con .NET</span><span class="sxs-lookup"><span data-stu-id="9b37d-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="9b37d-104">En este tema se describen los pasos generales que puede llevar a cabo al configurar la telemetría de Azure Media Services (AMS) mediante el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="9b37d-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="9b37d-105">Para una explicación detallada de lo que es la telemetría AMS y cómo consumirla, consulte el tema de [información general](media-services-telemetry-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b37d-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="9b37d-106">Puede utilizar los datos de telemetría de una de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b37d-106">You can consume telemetry data in one of the following ways:</span></span>

- <span data-ttu-id="9b37d-107">Leer datos directamente desde Almacenamiento de tablas de Azure (por ejemplo, mediante el SDK de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="9b37d-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span></span> <span data-ttu-id="9b37d-108">Para la descripción de las tablas de almacenamiento de datos de telemetría, consulte la sección sobre **uso de información de telemetría** de [este](https://msdn.microsoft.com/library/mt742089.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="9b37d-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="9b37d-109">O</span><span class="sxs-lookup"><span data-stu-id="9b37d-109">Or</span></span>

- <span data-ttu-id="9b37d-110">Aproveche la compatibilidad del SDK de .NET de Servicios multimedia para leer los datos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b37d-110">Use the support in the Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="9b37d-111">Este tema muestra cómo habilitar la telemetría de la cuenta de AMS especifica y cómo consultar las métricas usando el SDK de .NET de Servicios Multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b37d-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="9b37d-112">Configuración de telemetría para una cuenta de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9b37d-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="9b37d-113">Para habilitar la telemetría es necesario realizar los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b37d-113">The following steps are needed to enable telemetry:</span></span>

- <span data-ttu-id="9b37d-114">Obtener las credenciales de la cuenta de almacenamiento vinculada a la cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="9b37d-114">Get the credentials of the storage account attached to the Media Services account.</span></span> 
- <span data-ttu-id="9b37d-115">Cree un punto de conexión de notificación con **EndPointType** establecido en **AzureTable** y endPointAddress apuntando a la tabla de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b37d-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="9b37d-116">Crear unos valores de configuración de supervisión para los servicios que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="9b37d-116">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="9b37d-117">No se permite más que una configuración de supervisión.</span><span class="sxs-lookup"><span data-stu-id="9b37d-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="9b37d-118">uso de información de telemetría</span><span class="sxs-lookup"><span data-stu-id="9b37d-118">Consuming telemetry information</span></span>

<span data-ttu-id="9b37d-119">Para información sobre el consumo de la información de telemetría, consulte [este](media-services-telemetry-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="9b37d-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9b37d-120">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b37d-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="9b37d-121">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9b37d-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="9b37d-122">Agregue los siguientes elementos al elemento **appSettings** definido en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="9b37d-122">Add the following element to **appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="9b37d-123">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b37d-123">Example</span></span>  
    
<span data-ttu-id="9b37d-124">El ejemplo siguiente muestra cómo habilitar la telemetría de la cuenta de AMS especifica y cómo consultar las métricas usando el SDK de .NET de Servicios Multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b37d-124">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print the channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="9b37d-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b37d-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b37d-126">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9b37d-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
