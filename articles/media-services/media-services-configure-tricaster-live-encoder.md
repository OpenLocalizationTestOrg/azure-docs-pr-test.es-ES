---
title: "aaaConfigure Hola NewTek TriCaster codificador toosend una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure hello Tricaster codificador toosend una velocidad de bits única secuencia tooAMS canales activos que están habilitadas para la codificación en directo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="3d91a-103">Usar hello NewTek TriCaster codificador toosend una secuencia en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="3d91a-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d91a-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="3d91a-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="3d91a-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="3d91a-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="3d91a-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="3d91a-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="3d91a-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="3d91a-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="3d91a-108">Este tema se muestra cómo hello tooconfigure [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live codificador toosend canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="3d91a-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="3d91a-109">Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="3d91a-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="3d91a-110">Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="3d91a-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="3d91a-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="3d91a-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="3d91a-112">Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="3d91a-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3d91a-113">Al usar Tricaster para el envío de una contribución fuente canales tooAMS que están habilitados para la codificación en directo, pueden producirse problemas de audio/vídeo en el evento en directo si se utilizan ciertas características de Tricaster, como cortar entre las fuentes de distribución rápida, o se modifica de pizarras .</span><span class="sxs-lookup"><span data-stu-id="3d91a-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="3d91a-114">Hola AMS equipo está trabajando sobre cómo solucionar estos problemas, hasta entonces, es recomendable no toouse estas características.</span><span class="sxs-lookup"><span data-stu-id="3d91a-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="3d91a-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3d91a-115">Prerequisites</span></span>
* [<span data-ttu-id="3d91a-116">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="3d91a-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="3d91a-117">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="3d91a-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="3d91a-118">Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="3d91a-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="3d91a-119">Instalar la versión más reciente de hello del programa Hola a [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) herramienta.</span><span class="sxs-lookup"><span data-stu-id="3d91a-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="3d91a-120">Iniciar la herramienta de Hola y conectar con cuenta de tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="3d91a-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="3d91a-121">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="3d91a-121">Tips</span></span>
* <span data-ttu-id="3d91a-122">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="3d91a-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="3d91a-123">Una buena regla general al determinar los requisitos de ancho de banda es hello toodouble streaming de velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="3d91a-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="3d91a-124">Aunque esto no es un requisito obligatorio, ayudará a mitigar el impacto de Hola de congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="3d91a-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="3d91a-125">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="3d91a-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="3d91a-126">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="3d91a-126">Create a channel</span></span>
1. <span data-ttu-id="3d91a-127">En la herramienta AMSE de hello, navegue toohello **Live** ficha y haga clic en el área del canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d91a-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="3d91a-128">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="3d91a-128">Select **Create channel…**</span></span> <span data-ttu-id="3d91a-129">en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d91a-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="3d91a-131">Especifique un nombre de canal, el campo de descripción de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="3d91a-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="3d91a-132">En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="3d91a-133">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="3d91a-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="3d91a-134">Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="3d91a-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="3d91a-135">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="3d91a-137">canal de Hello puede tardar tanto como toostart de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="3d91a-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="3d91a-138">Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="3d91a-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d91a-139">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="3d91a-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="3d91a-140">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="3d91a-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="3d91a-141"><a id=configure_tricaster_rtmp></a>Configurar Hola NewTek TriCaster codificador</span><span class="sxs-lookup"><span data-stu-id="3d91a-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="3d91a-142">En este tutorial Hola se utilizan las siguientes opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="3d91a-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="3d91a-143">resto de Hola de esta sección describe los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="3d91a-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="3d91a-144">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="3d91a-144">**Video**:</span></span>

* <span data-ttu-id="3d91a-145">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="3d91a-145">Codec: H.264</span></span>
* <span data-ttu-id="3d91a-146">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="3d91a-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="3d91a-147">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="3d91a-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="3d91a-148">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="3d91a-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="3d91a-149">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="3d91a-149">Frame Rate: 30</span></span>

<span data-ttu-id="3d91a-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="3d91a-150">**Audio**:</span></span>

* <span data-ttu-id="3d91a-151">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="3d91a-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="3d91a-152">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="3d91a-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="3d91a-153">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="3d91a-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="3d91a-154">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="3d91a-154">Configuration steps</span></span>
1. <span data-ttu-id="3d91a-155">Cree un nuevo proyecto de **NewTek TriCaster** según el origen de entrada de vídeo que se use.</span><span class="sxs-lookup"><span data-stu-id="3d91a-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="3d91a-156">Una vez dentro de ese proyecto, busque hello **flujo** botón y haga clic en hello engranaje icono siguiente tooit tooaccess hello secuencia menú Configuración.</span><span class="sxs-lookup"><span data-stu-id="3d91a-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="3d91a-158">Una vez que se abre el menú de hello, haga clic en **New** bajo el encabezado de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d91a-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="3d91a-159">Cuando se le solicite para el tipo de conexión de hello, seleccione **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="3d91a-161">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-161">Click **OK**.</span></span>
5. <span data-ttu-id="3d91a-162">Un perfil de FMLE ahora puede importarse, haga clic en hello desplegable flecha situada debajo **perfil Streaming** y navegar demasiado**examinar**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="3d91a-164">Navegue toowhere Hola configurado FMLE perfil se guardó.</span><span class="sxs-lookup"><span data-stu-id="3d91a-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="3d91a-165">Selecciónelo y presione **OK**(Aceptar).</span><span class="sxs-lookup"><span data-stu-id="3d91a-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="3d91a-166">Cuando se carga el perfil de hello, continuar toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="3d91a-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="3d91a-167">Obtener dirección URL de entrada del canal de hello en orden tooassign, toohello Tricaster **RTMP extremo**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="3d91a-168">Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d91a-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="3d91a-169">Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d91a-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="3d91a-170">Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="3d91a-172">Pegar esta información en hello **ubicación** campo **Flash Server** en proyecto de hello Tricaster.</span><span class="sxs-lookup"><span data-stu-id="3d91a-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="3d91a-173">Asignar un nombre de la secuencia en hello **Id. del Streaming** campo.</span><span class="sxs-lookup"><span data-stu-id="3d91a-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="3d91a-174">Si la información de la secuencia se ha agregado el perfil FMLE toohello, también se puede importar toothis sección haciendo clic en **importar la configuración**, navegar por toohello guarda FMLE perfil y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="3d91a-175">campos de Flash Server relevantes de Hello deben llenar con información de Hola desde FMLE.</span><span class="sxs-lookup"><span data-stu-id="3d91a-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="3d91a-177">Cuando termine, haga clic en **Aceptar** final Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="3d91a-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="3d91a-178">Cuando las entradas de vídeo y audio en hello Tricaster están listos, empezar a transmitir tooAMS haciendo clic en hello **flujo** botón.</span><span class="sxs-lookup"><span data-stu-id="3d91a-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="3d91a-180">Antes de hacer clic **flujo**, le **debe** Asegúrese de que el canal de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="3d91a-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="3d91a-181">Además, asegúrese de que no tooleave Hola canal en un estado listo sin una contribución entrada fuente durante más de 15 minutos de >.</span><span class="sxs-lookup"><span data-stu-id="3d91a-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="3d91a-182">Prueba de reproducción</span><span class="sxs-lookup"><span data-stu-id="3d91a-182">Test playback</span></span>
<span data-ttu-id="3d91a-183">Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado.</span><span class="sxs-lookup"><span data-stu-id="3d91a-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="3d91a-184">En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="3d91a-185">Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3d91a-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="3d91a-186">Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada.</span><span class="sxs-lookup"><span data-stu-id="3d91a-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="3d91a-187">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3d91a-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="3d91a-188">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="3d91a-188">Create a program</span></span>
1. <span data-ttu-id="3d91a-189">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="3d91a-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="3d91a-190">En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="3d91a-192">Nombre de programa hello y, si es necesario, ajuste hello **duración de la ventana de archivo** (qué horas too4 de los valores predeterminados).</span><span class="sxs-lookup"><span data-stu-id="3d91a-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="3d91a-193">También puede especificar una ubicación de almacenamiento o deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d91a-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="3d91a-194">Comprobar hello **inicio Hola programa ahora** cuadro.</span><span class="sxs-lookup"><span data-stu-id="3d91a-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="3d91a-195">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="3d91a-196">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="3d91a-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="3d91a-197">Una vez que se ejecuta el programa de hello, confirme la reproducción, haga clic en el programa hello y vaya demasiado**programas de reproducción hello** y, a continuación, seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d91a-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="3d91a-198">Una vez confirmado, haga clic en programa Hola de nuevo y seleccione **copiar tooClipboard de dirección URL de salida de hello** (o recuperar la información desde hello **información y configuración de programas** opción de menú de hello).</span><span class="sxs-lookup"><span data-stu-id="3d91a-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="3d91a-199">secuencia de Hello ahora está listo toobe incrustado en un reproductor o distribuida tooan público para live visualización.</span><span class="sxs-lookup"><span data-stu-id="3d91a-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="3d91a-200">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="3d91a-200">Troubleshooting</span></span>
<span data-ttu-id="3d91a-201">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3d91a-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="3d91a-202">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3d91a-202">Next step</span></span>
<span data-ttu-id="3d91a-203">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="3d91a-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3d91a-204">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="3d91a-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
