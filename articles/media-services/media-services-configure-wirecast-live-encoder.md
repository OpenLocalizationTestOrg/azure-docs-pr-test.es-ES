---
title: "aaaConfigure Hola toosend de codificador Telestream Wirecast una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure hello Wirecast codificador toosend una velocidad de bits única secuencia tooAMS canales activos que están habilitadas para la codificación en directo. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="efe8a-103">Usar hello Wirecast codificador toosend una secuencia en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="efe8a-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="efe8a-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="efe8a-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="efe8a-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="efe8a-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="efe8a-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="efe8a-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="efe8a-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="efe8a-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="efe8a-108">Este tema se muestra cómo hello tooconfigure [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live codificador toosend canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="efe8a-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="efe8a-109">Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="efe8a-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="efe8a-110">Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="efe8a-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="efe8a-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="efe8a-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="efe8a-112">Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="efe8a-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe8a-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="efe8a-113">Prerequisites</span></span>
* [<span data-ttu-id="efe8a-114">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="efe8a-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="efe8a-115">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="efe8a-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="efe8a-116">Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="efe8a-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="efe8a-117">Instalar la versión más reciente de hello del programa Hola a [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) herramienta.</span><span class="sxs-lookup"><span data-stu-id="efe8a-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="efe8a-118">Iniciar la herramienta de Hola y conectar con cuenta de tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="efe8a-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="efe8a-119">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="efe8a-119">Tips</span></span>
* <span data-ttu-id="efe8a-120">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="efe8a-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="efe8a-121">Una buena regla general al determinar los requisitos de ancho de banda es hello toodouble streaming de velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="efe8a-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="efe8a-122">Aunque esto no es un requisito obligatorio, ayudará a mitigar el impacto de Hola de congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="efe8a-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="efe8a-123">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="efe8a-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="efe8a-124">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="efe8a-124">Create a channel</span></span>
1. <span data-ttu-id="efe8a-125">En la herramienta AMSE de hello, navegue toohello **Live** ficha y haga clic en el área del canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="efe8a-126">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="efe8a-126">Select **Create channel…**</span></span> <span data-ttu-id="efe8a-127">en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="efe8a-129">Especifique un nombre de canal, el campo de descripción de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="efe8a-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="efe8a-130">En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="efe8a-131">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="efe8a-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="efe8a-132">Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="efe8a-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="efe8a-133">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="efe8a-135">canal de Hello puede tardar tanto como toostart de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="efe8a-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="efe8a-136">Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="efe8a-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efe8a-137">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="efe8a-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="efe8a-138">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="efe8a-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="efe8a-139"><a id=configure_wirecast_rtmp></a>Configurar Hola codificador Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="efe8a-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="efe8a-140">En este tutorial Hola se utilizan las siguientes opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="efe8a-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="efe8a-141">resto de Hola de esta sección describe los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="efe8a-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="efe8a-142">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="efe8a-142">**Video**:</span></span>

* <span data-ttu-id="efe8a-143">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="efe8a-143">Codec: H.264</span></span>
* <span data-ttu-id="efe8a-144">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="efe8a-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="efe8a-145">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="efe8a-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="efe8a-146">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="efe8a-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="efe8a-147">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="efe8a-147">Frame Rate: 30</span></span>

<span data-ttu-id="efe8a-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="efe8a-148">**Audio**:</span></span>

* <span data-ttu-id="efe8a-149">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="efe8a-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="efe8a-150">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="efe8a-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="efe8a-151">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="efe8a-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="efe8a-152">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="efe8a-152">Configuration steps</span></span>
1. <span data-ttu-id="efe8a-153">Abra la aplicación de Telestream Wirecast de hello en hello máquina que se va a usar y configurar para la transmisión por secuencias RTMP.</span><span class="sxs-lookup"><span data-stu-id="efe8a-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="efe8a-154">Configurar la salida de hello desplazándose toohello **salida** ficha y seleccionando **configuración de salida...** .</span><span class="sxs-lookup"><span data-stu-id="efe8a-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="efe8a-155">Asegúrese de hello seguro **destino de salida** se establece demasiado**servidor RTMP**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="efe8a-156">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-156">Click **OK**.</span></span>
4. <span data-ttu-id="efe8a-157">En la página de configuración de hello, Establece hello **destino** campo toobe **servicios multimedia de Azure**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="efe8a-158">Hola perfil de codificación está preseleccionada demasiado**Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="efe8a-159">toocustomize estas opciones, seleccione Hola engranaje icono toohello derecha del saludo de lista desplegable y, a continuación, elija **nuevo valor predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="efe8a-161">Configure los valores preestablecidos del codificador.</span><span class="sxs-lookup"><span data-stu-id="efe8a-161">Configure encoder presets.</span></span>

    <span data-ttu-id="efe8a-162">Hola nombre preestablecido y busque siguiente Hola configuración recomendada:</span><span class="sxs-lookup"><span data-stu-id="efe8a-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="efe8a-163">**Vídeo**</span><span class="sxs-lookup"><span data-stu-id="efe8a-163">**Video**</span></span>

   * <span data-ttu-id="efe8a-164">Encoder (Codificador): MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="efe8a-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="efe8a-165">Frames per Second (Fotogramas por segundo): 30</span><span class="sxs-lookup"><span data-stu-id="efe8a-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="efe8a-166">Bit Rate (Velocidad de bits): 5000 kbps/sec (seg.) (se puede ajustar en función de las limitaciones de red)</span><span class="sxs-lookup"><span data-stu-id="efe8a-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="efe8a-167">Profile (Perfil): Main (Principal)</span><span class="sxs-lookup"><span data-stu-id="efe8a-167">Profile: Main</span></span>
   * <span data-ttu-id="efe8a-168">Key frame every (Fotograma clave cada): 60 frames (fotogramas)</span><span class="sxs-lookup"><span data-stu-id="efe8a-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="efe8a-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="efe8a-169">**Audio**</span></span>

   * <span data-ttu-id="efe8a-170">Target bit rate (Velocidad de bits de destino): 192 kbits/sec (seg)</span><span class="sxs-lookup"><span data-stu-id="efe8a-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="efe8a-171">Sample Rate (Frecuencia de muestreo): 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="efe8a-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="efe8a-173">Presione **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="efe8a-173">Press **Save**.</span></span>

    <span data-ttu-id="efe8a-174">campo de codificación de Hello tiene ahora disponibles para la selección de perfil de hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="efe8a-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="efe8a-175">Asegúrese de que está seleccionado el nuevo perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="efe8a-176">Obtener dirección URL de entrada del canal de hello en orden tooassign, toohello Wirecast **RTMP extremo**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="efe8a-177">Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="efe8a-178">Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="efe8a-179">Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="efe8a-181">Hola Wirecast **configuración de salida** ventana, pegar esta información en hello **dirección** campo de la sección de la salida de hello y asigne un nombre de la secuencia.</span><span class="sxs-lookup"><span data-stu-id="efe8a-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="efe8a-183">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-183">Select **OK**.</span></span>
2. <span data-ttu-id="efe8a-184">En hello principal **Wirecast** , confirme los orígenes de entrada de vídeo y audio están listos y, a continuación, presione **flujo** en la esquina superior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="efe8a-186">Antes de hacer clic **flujo**, le **debe** Asegúrese de que el canal de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="efe8a-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="efe8a-187">Además, asegúrese de que no tooleave Hola canal en un estado listo sin una contribución entrada fuente durante más de 15 minutos de >.</span><span class="sxs-lookup"><span data-stu-id="efe8a-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="efe8a-188">Prueba de reproducción</span><span class="sxs-lookup"><span data-stu-id="efe8a-188">Test playback</span></span>

<span data-ttu-id="efe8a-189">Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado.</span><span class="sxs-lookup"><span data-stu-id="efe8a-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="efe8a-190">En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="efe8a-191">Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="efe8a-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="efe8a-192">Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada.</span><span class="sxs-lookup"><span data-stu-id="efe8a-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="efe8a-193">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="efe8a-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="efe8a-194">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="efe8a-194">Create a program</span></span>
1. <span data-ttu-id="efe8a-195">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="efe8a-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="efe8a-196">En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="efe8a-198">Nombre de programa hello y, si es necesario, ajuste hello **duración de la ventana de archivo** (qué horas too4 de los valores predeterminados).</span><span class="sxs-lookup"><span data-stu-id="efe8a-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="efe8a-199">También puede especificar una ubicación de almacenamiento o deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="efe8a-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="efe8a-200">Comprobar hello **inicio Hola programa ahora** cuadro.</span><span class="sxs-lookup"><span data-stu-id="efe8a-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="efe8a-201">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="efe8a-202">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="efe8a-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="efe8a-203">Una vez que se ejecuta el programa de hello, confirme la reproducción, haga clic en el programa hello y vaya demasiado**programas de reproducción hello** y, a continuación, seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="efe8a-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="efe8a-204">Una vez confirmado, haga clic en programa Hola de nuevo y seleccione **copiar tooClipboard de dirección URL de salida de hello** (o recuperar la información desde hello **información y configuración de programas** opción de menú de hello).</span><span class="sxs-lookup"><span data-stu-id="efe8a-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="efe8a-205">secuencia de Hello ahora está listo toobe incrustado en un reproductor o distribuida tooan público para live visualización.</span><span class="sxs-lookup"><span data-stu-id="efe8a-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="efe8a-206">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="efe8a-206">Troubleshooting</span></span>
<span data-ttu-id="efe8a-207">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="efe8a-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="efe8a-208">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="efe8a-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="efe8a-209">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="efe8a-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
