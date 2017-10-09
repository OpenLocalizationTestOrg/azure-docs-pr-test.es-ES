---
title: aaaHow tooperform streaming en vivo con local codificadores mediante .NET | Documentos de Microsoft
description: "Este tema muestra cómo live toouse .NET tooperform codificación con codificadores locales."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/18/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 332582c9f925f8b9270929b3fa8140fce010bbf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="46a18-103">¿Cómo tooperform streaming en directo con codificadores locales mediante .NET</span><span class="sxs-lookup"><span data-stu-id="46a18-103">How tooperform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46a18-104">Portal</span><span class="sxs-lookup"><span data-stu-id="46a18-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="46a18-105">.NET</span><span class="sxs-lookup"><span data-stu-id="46a18-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="46a18-106">REST</span><span class="sxs-lookup"><span data-stu-id="46a18-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="46a18-107">Este tutorial le guiará por los pasos de hello del uso de hello Azure Media Services .NET SDK toocreate una **canal** que está configurado para la entrega de una acceso directo.</span><span class="sxs-lookup"><span data-stu-id="46a18-107">This tutorial walks you through hello steps of using hello Azure Media Services .NET SDK toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="46a18-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="46a18-108">Prerequisites</span></span>
<span data-ttu-id="46a18-109">tutorial de hello toocomplete necesarios son las siguientes de Hello:</span><span class="sxs-lookup"><span data-stu-id="46a18-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="46a18-110">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="46a18-110">An Azure account.</span></span>
* <span data-ttu-id="46a18-111">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="46a18-111">A Media Services account.</span></span>    <span data-ttu-id="46a18-112">toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="46a18-112">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="46a18-113">Configurar el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="46a18-113">Set up your dev environment.</span></span> <span data-ttu-id="46a18-114">Para obtener más información, consulte [Configuración del entorno](media-services-set-up-computer.md).</span><span class="sxs-lookup"><span data-stu-id="46a18-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="46a18-115">Una cámara web.</span><span class="sxs-lookup"><span data-stu-id="46a18-115">A webcam.</span></span> <span data-ttu-id="46a18-116">Por ejemplo, el [codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="46a18-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="46a18-117">Hola de tooreview recomendada siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="46a18-117">Recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="46a18-118">Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo.</span><span class="sxs-lookup"><span data-stu-id="46a18-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="46a18-119">Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple</span><span class="sxs-lookup"><span data-stu-id="46a18-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="46a18-120">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46a18-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="46a18-121">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="46a18-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="46a18-122">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="46a18-122">Example</span></span>
<span data-ttu-id="46a18-123">Hola el ejemplo de código siguiente muestra cómo hello tooachieve siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="46a18-123">hello following code example demonstrates how tooachieve hello following tasks:</span></span>

* <span data-ttu-id="46a18-124">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="46a18-124">Connect tooMedia Services</span></span>
* <span data-ttu-id="46a18-125">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="46a18-125">Create a channel</span></span>
* <span data-ttu-id="46a18-126">Canal de actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="46a18-126">Update hello channel</span></span>
* <span data-ttu-id="46a18-127">Recuperar el extremo de entrada del canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="46a18-127">Retrieve hello channel’s input endpoint.</span></span> <span data-ttu-id="46a18-128">extremo de entrada de Hello debe proporcionarse toohello codificador en directo local.</span><span class="sxs-lookup"><span data-stu-id="46a18-128">hello input endpoint should be provided toohello on-premises live encoder.</span></span> <span data-ttu-id="46a18-129">Hola codificador en directo convierte las señales de hello toostreams de cámara que se envían la entrada del canal de toohello (extremo de introducción).</span><span class="sxs-lookup"><span data-stu-id="46a18-129">hello live encoder converts signals from hello camera toostreams that are sent toohello channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="46a18-130">Recuperar el extremo de vista previa del canal de Hola</span><span class="sxs-lookup"><span data-stu-id="46a18-130">Retrieve hello channel’s preview endpoint</span></span>
* <span data-ttu-id="46a18-131">Crear e iniciar un programa.</span><span class="sxs-lookup"><span data-stu-id="46a18-131">Create and start a program</span></span>
* <span data-ttu-id="46a18-132">Crear un localizador necesario tooaccess Hola programa</span><span class="sxs-lookup"><span data-stu-id="46a18-132">Create a locator needed tooaccess hello program</span></span>
* <span data-ttu-id="46a18-133">Crear e iniciar un StreamingEndpoint.</span><span class="sxs-lookup"><span data-stu-id="46a18-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="46a18-134">Actualizar Hola extremo de streaming</span><span class="sxs-lookup"><span data-stu-id="46a18-134">Update hello streaming endpoint</span></span>
* <span data-ttu-id="46a18-135">Apagar los recursos.</span><span class="sxs-lookup"><span data-stu-id="46a18-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="46a18-136">Asegúrese de que esté Hola origen desde el que desea que el contenido de toostream Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="46a18-136">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="46a18-137">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="46a18-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="46a18-138">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="46a18-138">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="46a18-139">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="46a18-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="46a18-140">Para obtener información acerca de cómo tooconfigure un codificador en directo, vea [codificadores en directo y soporte RTMP para Azure Media Services](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span><span class="sxs-lookup"><span data-stu-id="46a18-140">For information on how tooconfigure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSLiveTest
    {
        class Program
        {
        private const string StreamingEndpointName = "streamingendpoint001";
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

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

            IChannel channel = CreateAndStartChannel();

            // Set hello Live Encoder toopoint toohello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use hello previewEndpoint toopreview and verify
            // that hello input from hello encoder is actually reaching hello Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want toochange hello Smooth fragments tooHLS segment ratio, you would set hello ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time tooexecute. toodetermine hello state of operations after calling Start or Stop, query hello IChannel.State .

            channel.Start();

            return channel;
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
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access tooIP addresses.
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
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access tooIP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            channel.Update();
        }

        public static IProgram CreateAndStartProgram(IChannel channel)
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            // Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
            // however each Program must have a unique name within your Media Services account.
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            program.Start();

            return program;
        }

        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            

            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                "Live Stream Policy",
                ArchiveWindowLength,
                AccessPermissions.Read
                )
            );

            return locator;
        }

        public static IStreamingEndpoint CreateAndStartStreamingEndpoint(bool createNew)
        {
            IStreamingEndpoint streamingEndpoint = null;
            if (createNew)
            {
            var options = new StreamingEndpointCreationOptions
            {
                Name = StreamingEndpointName,
                ScaleUnits = 1,
                AccessControl = GetAccessControl(),
                CacheControl = GetCacheControl()
            };

            streamingEndpoint = _context.StreamingEndpoints.Create(options);
            }
            else
            {
            streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            }


            if (streamingEndpoint.State == StreamingEndpointState.Stopped)
            streamingEndpoint.Start();

            return streamingEndpoint;
        }

        private static StreamingEndpointAccessControl GetAccessControl()
        {
            return new StreamingEndpointAccessControl
            {
            IPAllowList = new List<IPRange>
                {
                new IPRange
                {
                    Name = "Allow all",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                }
                },

            AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                {
                new AkamaiSignatureHeaderAuthenticationKey
                {
                    Identifier = "My key",
                    Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                    Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                }
                }
            };
        }

        private static byte[] GenerateRandomBytes(int length)
        {
            var bytes = new byte[length];
            using (var rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(bytes);
            }

            return bytes;
        }

        private static StreamingEndpointCacheControl GetCacheControl()
        {
            return new StreamingEndpointCacheControl
            {
            MaxAge = TimeSpan.FromSeconds(1000)
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            streamingEndpoint.Update();
        }

        public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                        IChannel channel)
        {
            if (streamingEndpoint != null)
            {
            streamingEndpoint.Stop();
            if(streamingEndpoint.Name != "default")
                streamingEndpoint.Delete();
            }

            IAsset asset;
            if (channel != null)
            {

            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                program.Stop();
                program.Delete();

                if (asset != null)
                {
                foreach (var l in asset.Locators)
                    l.Delete();

                asset.Delete();
                }
            }

            channel.Stop();
            channel.Delete();
            }
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="46a18-141">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="46a18-141">Next Step</span></span>
<span data-ttu-id="46a18-142">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="46a18-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="46a18-143">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="46a18-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

