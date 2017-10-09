---
title: "aaaConfigure Hola toosend de codificador en vivo Elemental una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure Hola toosend de codificador en vivo Elemental canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="7f8f5-103">Usar toosend del codificador de Live Elemental de hello una secuencia en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="7f8f5-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f8f5-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="7f8f5-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="7f8f5-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="7f8f5-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="7f8f5-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="7f8f5-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="7f8f5-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="7f8f5-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="7f8f5-108">Este tema se muestra cómo hello tooconfigure [Live Elemental](http://www.elementaltechnologies.com/products/elemental-live) codificador toosend una velocidad de bits única transmitir canales tooAMS que están habilitados para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="7f8f5-109">Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="7f8f5-110">Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="7f8f5-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="7f8f5-112">Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f8f5-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7f8f5-113">Prerequisites</span></span>
* <span data-ttu-id="7f8f5-114">Debe tener conocimientos prácticos de utilizando Live Elemental web interfaz toocreate eventos en directo.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="7f8f5-115">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="7f8f5-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="7f8f5-116">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="7f8f5-117">Para más información, consulte [Administración de puntos de conexión de streaming en una cuenta de Media Services](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="7f8f5-118">Instalar la versión más reciente de hello del programa Hola a [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) herramienta.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="7f8f5-119">Iniciar la herramienta de Hola y conectar con cuenta de tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="7f8f5-120">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="7f8f5-120">Tips</span></span>
* <span data-ttu-id="7f8f5-121">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="7f8f5-122">Una buena regla general al determinar los requisitos de ancho de banda es hello toodouble streaming de velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="7f8f5-123">Aunque esto no es un requisito obligatorio, ayudará a mitigar el impacto de Hola de congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="7f8f5-124">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="7f8f5-125">Elemental Live con entrada RTP</span><span class="sxs-lookup"><span data-stu-id="7f8f5-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="7f8f5-126">Esta sección muestra cómo tooconfigure Hola Elemental codificador en directo que se envía a una velocidad de bits única secuencia en directo a través de RTP.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="7f8f5-127">Para obtener más información, consulte [Transmisión MPEG TS sobre RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="7f8f5-128">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="7f8f5-128">Create a channel</span></span>

1. <span data-ttu-id="7f8f5-129">En la herramienta AMSE de hello, navegue toohello **Live** ficha y haga clic en el área del canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="7f8f5-130">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="7f8f5-130">Select **Create channel…**</span></span> <span data-ttu-id="7f8f5-131">en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="7f8f5-133">Especifique un nombre de canal, el campo de descripción de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="7f8f5-134">En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="7f8f5-135">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="7f8f5-136">Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="7f8f5-137">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="7f8f5-139">canal de Hello puede tardar tanto como toostart de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="7f8f5-140">Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f8f5-141">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="7f8f5-142">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="7f8f5-143"><a id=configure_elemental_rtp></a>Configurar el codificador de Live Elemental Hola</span><span class="sxs-lookup"><span data-stu-id="7f8f5-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="7f8f5-144">En este tutorial Hola se utilizan las siguientes opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="7f8f5-145">resto de Hola de esta sección describe los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="7f8f5-146">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="7f8f5-146">**Video**:</span></span>

* <span data-ttu-id="7f8f5-147">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="7f8f5-147">Codec: H.264</span></span>
* <span data-ttu-id="7f8f5-148">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="7f8f5-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="7f8f5-149">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="7f8f5-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="7f8f5-150">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="7f8f5-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="7f8f5-151">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="7f8f5-151">Frame Rate: 30</span></span>

<span data-ttu-id="7f8f5-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="7f8f5-152">**Audio**:</span></span>

* <span data-ttu-id="7f8f5-153">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="7f8f5-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="7f8f5-154">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="7f8f5-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="7f8f5-155">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="7f8f5-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="7f8f5-156">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="7f8f5-156">Configuration steps</span></span>
1. <span data-ttu-id="7f8f5-157">Navegue toohello **Live Elemental** interfaz web y configurar el codificador de Hola para **UDP/TS** transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="7f8f5-158">Una vez que se crea un nuevo evento, desplácese hacia abajo de grupos de resultados toohello y agregar hello **UDP/TS** grupo de resultados.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="7f8f5-159">Para crear una salida, seleccione **New Stream** (Nueva transmisión) y haga clic en **Add Output** (Agregar salida).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="7f8f5-161">Se recomienda ese evento Elemental hello tiene código de hello tiempo establecido demasiado volver a conectar un codificador de hello toohelp "Reloj del sistema" en caso de hello de un error de secuencia.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="7f8f5-162">Ahora que hello salida se ha creado, haga clic en **Agregar secuencia**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="7f8f5-163">Ahora se puede configurar la configuración de salida de Hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="7f8f5-164">Desplácese hacia abajo toohello "Stream 1" que acaba de crear, haga clic en hello **vídeo** ficha Hola izquierda y expanda hello **avanzadas** sección de configuración.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="7f8f5-166">Aunque Live Elemental tiene una amplia gama de personalización disponibles, hello siguiente configuración se recomienda para comenzar a usar tooAMS de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="7f8f5-167">Resolution (Resolución): 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="7f8f5-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="7f8f5-168">Framerate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="7f8f5-168">Framerate: 30</span></span>
   * <span data-ttu-id="7f8f5-169">GOP Size (Tamaño de GOP): 60 fotogramas</span><span class="sxs-lookup"><span data-stu-id="7f8f5-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="7f8f5-170">Interlace Mode (Modo de vídeo entrelazado): Progresivo</span><span class="sxs-lookup"><span data-stu-id="7f8f5-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="7f8f5-171">Bit Rate (Velocidad de bits): 5000000 bits/s (se puede ajustar en función de las limitaciones de red)</span><span class="sxs-lookup"><span data-stu-id="7f8f5-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="7f8f5-173">Obtener dirección URL de entrada del canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="7f8f5-174">Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="7f8f5-175">Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="7f8f5-176">Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="7f8f5-178">Pegar esta información en hello **destino principal** campo de hello Elemental.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="7f8f5-179">Todas las demás opciones pueden permanecer predeterminado Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="7f8f5-181">Para obtener redundancia adicional, repita estos pasos con hello secundaria de dirección URL de entrada mediante la creación de una pestaña independiente de "Salida" para la transmisión por secuencias de UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="7f8f5-182">Haga clic en **crear** (si se ha creado un nuevo evento) o **actualización** (si está modificando un evento preexistente) y, a continuación, continuar codificador de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f8f5-183">Antes de hacer clic **iniciar** en interfaz web Live Elemental de hello, **debe** Asegúrese de que el canal de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="7f8f5-184">Además, asegúrese de que no tooleave Hola canal en un estado listo sin un evento durante más de 15 minutos de >.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="7f8f5-185">Después de que se ha ejecutado la secuencia de Hola durante 30 segundos, desplácese atrás toohello AMSE herramienta y prueba la reproducción.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="7f8f5-186">Prueba de reproducción</span><span class="sxs-lookup"><span data-stu-id="7f8f5-186">Test playback</span></span>

<span data-ttu-id="7f8f5-187">Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="7f8f5-188">En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="7f8f5-189">Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="7f8f5-190">Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="7f8f5-191">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="7f8f5-192">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="7f8f5-192">Create a program</span></span>
1. <span data-ttu-id="7f8f5-193">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="7f8f5-194">En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="7f8f5-196">Nombre de programa hello y, si es necesario, ajuste hello **duración de la ventana de archivo** (qué horas too4 de los valores predeterminados).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="7f8f5-197">También puede especificar una ubicación de almacenamiento o deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="7f8f5-198">Comprobar hello **inicio Hola programa ahora** cuadro.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="7f8f5-199">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="7f8f5-200">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="7f8f5-201">Una vez que se ejecuta el programa de hello, confirme la reproducción, haga clic en el programa hello y vaya demasiado**programas de reproducción hello** y, a continuación, seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="7f8f5-202">Una vez confirmado, haga clic en programa Hola de nuevo y seleccione **copiar tooClipboard de dirección URL de salida de hello** (o recuperar la información desde hello **información y configuración de programas** opción de menú de hello).</span><span class="sxs-lookup"><span data-stu-id="7f8f5-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="7f8f5-203">secuencia de Hello ahora está listo toobe incrustado en un reproductor o distribuida tooan público para live visualización.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="7f8f5-204">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7f8f5-204">Troubleshooting</span></span>
<span data-ttu-id="7f8f5-205">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="7f8f5-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7f8f5-206">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="7f8f5-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7f8f5-207">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="7f8f5-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
