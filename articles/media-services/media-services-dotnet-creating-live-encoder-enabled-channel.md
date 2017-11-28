---
title: aaaHow tooperform streaming en vivo con secuencias de velocidades de bits de toocreate de servicios multimedia de Azure .NET | Documentos de Microsoft
description: "Este tutorial le guía a través de los pasos de Hola de creación de un canal que recibe una secuencia en directo de velocidad de bits única y lo codifica en la secuencia de velocidad de bits toomulti mediante SDK de .NET."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a><span data-ttu-id="fed8c-103">¿Cómo tooperform streaming en vivo con servicios multimedia de Azure toocreate velocidades de bits se transmita por secuencias con .NET</span><span class="sxs-lookup"><span data-stu-id="fed8c-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fed8c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="fed8c-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="fed8c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fed8c-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="fed8c-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="fed8c-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="fed8c-107">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fed8c-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="fed8c-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fed8c-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="fed8c-109">Información general</span><span class="sxs-lookup"><span data-stu-id="fed8c-109">Overview</span></span>
<span data-ttu-id="fed8c-110">Este tutorial le guiará por los pasos de Hola de creación de un **canal** que recibe una secuencia en directo de velocidad de bits única y lo codifica en la secuencia de velocidad de bits toomulti.</span><span class="sxs-lookup"><span data-stu-id="fed8c-110">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

<span data-ttu-id="fed8c-111">Para obtener más información consulte tooChannels relacionados que están habilitados para la codificación en directo, [streaming en vivo al utilizar secuencias de velocidades de bits de servicios multimedia de Azure toocreate](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="fed8c-111">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="fed8c-112">Escenario común de streaming en vivo</span><span class="sxs-lookup"><span data-stu-id="fed8c-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="fed8c-113">Hola siguiendo los pasos describe las tareas implicadas en la creación de aplicaciones de transmisión por secuencias en directo común.</span><span class="sxs-lookup"><span data-stu-id="fed8c-113">hello following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="fed8c-114">Actualmente, Hola máximo recomendado de duración de un evento en directo es 8 horas.</span><span class="sxs-lookup"><span data-stu-id="fed8c-114">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="fed8c-115">Póngase en contacto con amslived Microsoft.com si necesitas toorun un canal para períodos más largos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="fed8c-115">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="fed8c-116">Conectar un equipo de tooa de cámara de vídeo.</span><span class="sxs-lookup"><span data-stu-id="fed8c-116">Connect a video camera tooa computer.</span></span> <span data-ttu-id="fed8c-117">Iniciar y configurar un codificador en directo local que pueda dar como resultado una secuencia de velocidad de bits única en uno de hello siguientes protocolos: RTP (MPEG-TS), Smooth Streaming o RTMP.</span><span class="sxs-lookup"><span data-stu-id="fed8c-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="fed8c-118">Para obtener más información, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="fed8c-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="fed8c-119">Este paso también puede realizarse después de crear el canal.</span><span class="sxs-lookup"><span data-stu-id="fed8c-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="fed8c-120">Cree e inicie un canal.</span><span class="sxs-lookup"><span data-stu-id="fed8c-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="fed8c-121">URL de introducción de hello recuperar canales.</span><span class="sxs-lookup"><span data-stu-id="fed8c-121">Retrieve hello Channel ingest URL.</span></span>

    <span data-ttu-id="fed8c-122">URL de introducción de Hola Hola codificador en directo toosend hello secuencia toohello canal utiliza.</span><span class="sxs-lookup"><span data-stu-id="fed8c-122">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>

4. <span data-ttu-id="fed8c-123">Recuperar la dirección URL de vista previa de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed8c-123">Retrieve hello Channel preview URL.</span></span>

    <span data-ttu-id="fed8c-124">Utilice este tooverify de dirección URL que el canal está recibiendo correctamente la secuencia en directo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed8c-124">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>

5. <span data-ttu-id="fed8c-125">Cree un recurso.</span><span class="sxs-lookup"><span data-stu-id="fed8c-125">Create an asset.</span></span>
6. <span data-ttu-id="fed8c-126">Si desea para hello asset toobe cifra dinámicamente durante la reproducción, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fed8c-126">If you want for hello asset toobe dynamically encrypted during playback, do hello following:</span></span>
7. <span data-ttu-id="fed8c-127">Cree una clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="fed8c-127">Create a content key.</span></span>
8. <span data-ttu-id="fed8c-128">Configurar la directiva de autorización de la clave de hello contenido.</span><span class="sxs-lookup"><span data-stu-id="fed8c-128">Configure hello content key's authorization policy.</span></span>
9. <span data-ttu-id="fed8c-129">Configure la directiva de entrega de recursos (usada por el empaquetado y el cifrado dinámicos).</span><span class="sxs-lookup"><span data-stu-id="fed8c-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="fed8c-130">Crear un programa y especifique los activos de hello toouse que ha creado.</span><span class="sxs-lookup"><span data-stu-id="fed8c-130">Create a program and specify toouse hello asset that you created.</span></span>
11. <span data-ttu-id="fed8c-131">Publicar asset Hola asociada programa Hola mediante la creación de un localizador OnDemand.</span><span class="sxs-lookup"><span data-stu-id="fed8c-131">Publish hello asset associated with hello program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="fed8c-132">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="fed8c-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="fed8c-133">Hola origen desde el que desea que el contenido de toostream tiene toobe en hello **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="fed8c-133">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

12. <span data-ttu-id="fed8c-134">Inicie el programa de hello cuando esté listo toostart streaming y archivado.</span><span class="sxs-lookup"><span data-stu-id="fed8c-134">Start hello program when you are ready toostart streaming and archiving.</span></span>
13. <span data-ttu-id="fed8c-135">Si lo desea, codificador en directo de hello puede ser señalado toostart un anuncio.</span><span class="sxs-lookup"><span data-stu-id="fed8c-135">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="fed8c-136">anuncio de Hola se inserta en el flujo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="fed8c-136">hello advertisement is inserted in hello output stream.</span></span>
14. <span data-ttu-id="fed8c-137">Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.</span><span class="sxs-lookup"><span data-stu-id="fed8c-137">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span>
15. <span data-ttu-id="fed8c-138">Eliminar programa Hola (y opcionalmente eliminar recurso de hello).</span><span class="sxs-lookup"><span data-stu-id="fed8c-138">Delete hello Program (and optionally delete hello asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="fed8c-139">Temas que se abordarán</span><span class="sxs-lookup"><span data-stu-id="fed8c-139">What you'll learn</span></span>
<span data-ttu-id="fed8c-140">Este tema muestra cómo tooexecute diferentes operaciones en los canales y programas mediante el SDK de .NET de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="fed8c-140">This topic shows you how tooexecute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="fed8c-141">Dado que la ejecución de muchas de las operaciones es prolongada, se usan las API de .NET que administran operaciones de este tipo.</span><span class="sxs-lookup"><span data-stu-id="fed8c-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="fed8c-142">Hola tema muestra cómo siguiente de Hola toodo:</span><span class="sxs-lookup"><span data-stu-id="fed8c-142">hello topic shows how toodo hello following:</span></span>

1. <span data-ttu-id="fed8c-143">Cree e inicie un canal.</span><span class="sxs-lookup"><span data-stu-id="fed8c-143">Create and start a channel.</span></span> <span data-ttu-id="fed8c-144">Se usan las API de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="fed8c-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="fed8c-145">Obtener canales Hola Introducción (entrada) de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="fed8c-145">Get hello channels ingest (input) endpoint.</span></span> <span data-ttu-id="fed8c-146">Este extremo se debe proporcionar codificador toohello que puede enviar una secuencia en directo de velocidad de bits única.</span><span class="sxs-lookup"><span data-stu-id="fed8c-146">This endpoint should be provided toohello encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="fed8c-147">Obtener el extremo de vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed8c-147">Get hello preview endpoint.</span></span> <span data-ttu-id="fed8c-148">Este extremo es toopreview usado en la secuencia.</span><span class="sxs-lookup"><span data-stu-id="fed8c-148">This endpoint is used toopreview your stream.</span></span>
4. <span data-ttu-id="fed8c-149">Crear un activo que será usado toostore su contenido.</span><span class="sxs-lookup"><span data-stu-id="fed8c-149">Create an asset that will be used toostore your content.</span></span> <span data-ttu-id="fed8c-150">directivas de entrega de activos de Hello deben configurarse también, como se muestra en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fed8c-150">hello asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="fed8c-151">Crear un programa y especifique los activos de hello toouse que crearon anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fed8c-151">Create a program and specify toouse hello asset that was created earlier.</span></span> <span data-ttu-id="fed8c-152">Iniciar programa Hola.</span><span class="sxs-lookup"><span data-stu-id="fed8c-152">Start hello program.</span></span> <span data-ttu-id="fed8c-153">Se usan las API de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="fed8c-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="fed8c-154">Cree un localizador de activo de hello, por lo que el contenido de Hola se publica y se puede transmitir a tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="fed8c-154">Create a locator for hello asset, so hello content gets published and can be streamed tooyour clients.</span></span>
7. <span data-ttu-id="fed8c-155">Mostrar y ocultar pizarras.</span><span class="sxs-lookup"><span data-stu-id="fed8c-155">Show and hide slates.</span></span> <span data-ttu-id="fed8c-156">Iniciar y detener anuncios.</span><span class="sxs-lookup"><span data-stu-id="fed8c-156">Start and stop advertisements.</span></span> <span data-ttu-id="fed8c-157">Se usan las API de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="fed8c-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="fed8c-158">Limpiar el canal y Hola a todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="fed8c-158">Clean up your channel and all hello associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fed8c-159">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fed8c-159">Prerequisites</span></span>
<span data-ttu-id="fed8c-160">los siguientes Hola son tutorial de hello toocomplete necesarios.</span><span class="sxs-lookup"><span data-stu-id="fed8c-160">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="fed8c-161">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fed8c-161">An Azure account.</span></span> <span data-ttu-id="fed8c-162">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="fed8c-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fed8c-163">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fed8c-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="fed8c-164">Obtenga créditos que pueden ser utilizado tootry out servicios de Azure de pago.</span><span class="sxs-lookup"><span data-stu-id="fed8c-164">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="fed8c-165">Incluso después de que se agoten los créditos hello, puede mantener la cuenta de hello y usar los servicios de Azure gratuitos y características, como la característica de las aplicaciones Web de hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="fed8c-165">Even after hello credits are used up, you can keep hello account and use free Azure services and features, such as hello Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="fed8c-166">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="fed8c-166">A Media Services account.</span></span> <span data-ttu-id="fed8c-167">toocreate una cuenta de servicios multimedia, consulte [crear cuenta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="fed8c-167">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="fed8c-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate o Express) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="fed8c-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="fed8c-169">Debe usar el SDK de Servicios multimedia para .NET versión 3.2.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="fed8c-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="fed8c-170">Una cámara web y un codificador que pueda enviar una secuencia en vivo de una sola velocidad de bits.</span><span class="sxs-lookup"><span data-stu-id="fed8c-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="fed8c-171">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="fed8c-171">Considerations</span></span>
* <span data-ttu-id="fed8c-172">Actualmente, Hola máximo recomendado de duración de un evento en directo es 8 horas.</span><span class="sxs-lookup"><span data-stu-id="fed8c-172">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="fed8c-173">Póngase en contacto con amslived Microsoft.com si necesitas toorun un canal para períodos más largos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="fed8c-173">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="fed8c-174">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="fed8c-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="fed8c-175">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="fed8c-175">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="fed8c-176">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="fed8c-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="fed8c-177">Descarga de un ejemplo</span><span class="sxs-lookup"><span data-stu-id="fed8c-177">Download sample</span></span>

<span data-ttu-id="fed8c-178">Puede descargar el ejemplo de Hola a los que se describe en este tema de [aquí](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="fed8c-178">You can download hello sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="fed8c-179">Configuración para el desarrollo con el SDK de Servicios multimedia para .NET</span><span class="sxs-lookup"><span data-stu-id="fed8c-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="fed8c-180">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="fed8c-180">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="fed8c-181">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="fed8c-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
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

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
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

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
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

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
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

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="fed8c-182">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="fed8c-182">Next step</span></span>
<span data-ttu-id="fed8c-183">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="fed8c-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fed8c-184">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="fed8c-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


