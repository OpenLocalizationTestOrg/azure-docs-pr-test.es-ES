---
title: "aaaConfigure Hola FMLE codificador toosend una secuencia en directo de velocidad de bits única | Documentos de Microsoft"
description: "Este tema muestra cómo tooconfigure Hola toosend de codificador de codificador de Live de medios de Flash (FMLE) a una velocidad de bits única secuencia tooAMS los canales que están habilitadas para la codificación en directo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="86830-103">Usar hello FMLE codificador toosend una secuencia en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="86830-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86830-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="86830-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="86830-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="86830-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="86830-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="86830-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="86830-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="86830-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="86830-108">Este tema se muestra cómo hello tooconfigure [Flash Live el Codificador multimedia de](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) codificador toosend una velocidad de bits única transmitir canales tooAMS que están habilitados para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="86830-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="86830-109">Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="86830-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="86830-110">Este tutorial muestra cómo toomanage servicios multimedia de Azure (AMS) con la herramienta Explorador de servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="86830-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="86830-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="86830-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="86830-112">Si se encuentra en Mac o Linux, use hello Azure toocreate portal [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="86830-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="86830-113">Tenga en cuenta que en este tutorial se describe el uso de AAC.</span><span class="sxs-lookup"><span data-stu-id="86830-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="86830-114">Sin embargo, FMLE no es compatible con AAC de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="86830-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="86830-115">Deberá toopurchase un complemento para la codificación AAC como MainConcept: [AAC complemento](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="86830-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86830-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="86830-116">Prerequisites</span></span>
* [<span data-ttu-id="86830-117">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="86830-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="86830-118">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="86830-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="86830-119">Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="86830-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="86830-120">Instalar la versión más reciente de hello del programa Hola a [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) herramienta.</span><span class="sxs-lookup"><span data-stu-id="86830-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="86830-121">Iniciar la herramienta de Hola y conectar con cuenta de tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="86830-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="86830-122">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="86830-122">Tips</span></span>
* <span data-ttu-id="86830-123">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="86830-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="86830-124">Una buena regla general al determinar los requisitos de ancho de banda es hello toodouble streaming de velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="86830-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="86830-125">Aunque esto no es un requisito obligatorio, ayudará a mitigar el impacto de Hola de congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="86830-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="86830-126">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="86830-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="86830-127">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="86830-127">Create a channel</span></span>
1. <span data-ttu-id="86830-128">En la herramienta AMSE de hello, navegue toohello **Live** ficha y haga clic en el área del canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="86830-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="86830-129">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="86830-129">Select **Create channel…**</span></span> <span data-ttu-id="86830-130">en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="86830-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="86830-132">Especifique un nombre de canal, el campo de descripción de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="86830-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="86830-133">En configuración de canal, seleccione **estándar** para Hola opción de codificación en directo con hello proporcionados por el protocolo establecido demasiado**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="86830-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="86830-134">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="86830-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="86830-135">Asegúrese de hello seguro **inicio Hola nuevo canal ahora** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="86830-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="86830-136">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="86830-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="86830-138">canal de Hello puede tardar tanto como toostart de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="86830-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="86830-139">Mientras se inicia el canal de hello puede [configurar codificador hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="86830-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86830-140">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="86830-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="86830-141">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="86830-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="86830-142"><a id=configure_fmle_rtmp></a>Configurar el codificador de hello FMLE</span><span class="sxs-lookup"><span data-stu-id="86830-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="86830-143">En este tutorial Hola se utilizan las siguientes opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="86830-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="86830-144">resto de Hola de esta sección describe los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="86830-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="86830-145">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="86830-145">**Video**:</span></span>

* <span data-ttu-id="86830-146">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="86830-146">Codec: H.264</span></span>
* <span data-ttu-id="86830-147">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="86830-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="86830-148">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="86830-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="86830-149">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="86830-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="86830-150">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="86830-150">Frame Rate: 30</span></span>

<span data-ttu-id="86830-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="86830-151">**Audio**:</span></span>

* <span data-ttu-id="86830-152">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="86830-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="86830-153">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="86830-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="86830-154">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="86830-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="86830-155">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="86830-155">Configuration steps</span></span>
1. <span data-ttu-id="86830-156">Navegue toohello que Flash Live Codificador multimedia (FMLE) de la interfaz en la máquina de Hola que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="86830-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="86830-157">interfaz de Hello es una página principal de configuración.</span><span class="sxs-lookup"><span data-stu-id="86830-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="86830-158">Tome nota de los siguientes Hola recomendadas configuración tooget a trabajar con la transmisión mediante FMLE.</span><span class="sxs-lookup"><span data-stu-id="86830-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="86830-159">Format (Formato): H.264, Frame Rate (Velocidad de fotogramas): 30.00</span><span class="sxs-lookup"><span data-stu-id="86830-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="86830-160">Input Size (Tamaño de entrada): 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="86830-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="86830-161">Bit Rate (Velocidad de bits): 5000 kbps (se puede ajustar en función de las limitaciones de red)</span><span class="sxs-lookup"><span data-stu-id="86830-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="86830-163">Al usar entrelazado orígenes, por favor, marca de verificación Hola "Desentrelazar" opción</span><span class="sxs-lookup"><span data-stu-id="86830-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="86830-164">Seleccione Hola llave inglesa icono siguiente tooFormat, deben tener estos valores adicionales:</span><span class="sxs-lookup"><span data-stu-id="86830-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="86830-165">Profile (Perfil): Main (Principal)</span><span class="sxs-lookup"><span data-stu-id="86830-165">Profile: Main</span></span>
   * <span data-ttu-id="86830-166">Level (Nivel): 4.0</span><span class="sxs-lookup"><span data-stu-id="86830-166">Level: 4.0</span></span>
   * <span data-ttu-id="86830-167">Keyframe Frequency (Frecuencia de fotogramas clave): 2 seconds (2 segundos)</span><span class="sxs-lookup"><span data-stu-id="86830-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="86830-169">Establecer Hola después de la configuración de audio importante:</span><span class="sxs-lookup"><span data-stu-id="86830-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="86830-170">Format (Formato): AAC</span><span class="sxs-lookup"><span data-stu-id="86830-170">Format: AAC</span></span>
   * <span data-ttu-id="86830-171">Sample Rate (Frecuencia de muestreo): 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="86830-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="86830-172">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="86830-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="86830-174">Obtener dirección URL de entrada del canal de hello en orden tooassign, toohello FMLE **RTMP extremo**.</span><span class="sxs-lookup"><span data-stu-id="86830-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="86830-175">Navegar por la herramienta AMSE toohello atrás y comprobar estado de finalización de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="86830-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="86830-176">Una vez que ha cambiado el estado de Hola de **iniciando** demasiado**ejecuta**, puede obtener la dirección URL de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="86830-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="86830-177">Cuando se ejecuta el canal de hello, haga clic con el nombre del canal de hello, desplácese hacia abajo toohover sobre **Copiar dirección URL de entrada tooclipboard** y, a continuación, seleccione **dirección URL de entrada principal**.</span><span class="sxs-lookup"><span data-stu-id="86830-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="86830-179">Pegar esta información en hello **FMS URL** campo de la sección de la salida de hello y asigne un nombre de la secuencia.</span><span class="sxs-lookup"><span data-stu-id="86830-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="86830-181">Para obtener redundancia adicional, repita estos pasos con hello secundaria de dirección URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="86830-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="86830-182">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="86830-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86830-183">Antes de hacer clic **conectar**, le **debe** Asegúrese de que el canal de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="86830-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="86830-184">Además, asegúrese de que no tooleave Hola canal en un estado listo sin una contribución entrada fuente durante más de 15 minutos de >.</span><span class="sxs-lookup"><span data-stu-id="86830-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="86830-185">Prueba de reproducción</span><span class="sxs-lookup"><span data-stu-id="86830-185">Test playback</span></span>

<span data-ttu-id="86830-186">Navegar por la herramienta AMSE toohello y haga clic en toobe de canal de hello probado.</span><span class="sxs-lookup"><span data-stu-id="86830-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="86830-187">En el menú de hello, mantenga el mouse sobre **Hola reproducción Preview** y seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="86830-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="86830-188">Si la secuencia Hola aparece en el Reproductor de hello, codificador Hola ha sido tooAMS tooconnect configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="86830-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="86830-189">Si se recibe un error, canal de hello deberá toobe la configuración de restablecimiento y codificador ajustada.</span><span class="sxs-lookup"><span data-stu-id="86830-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="86830-190">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="86830-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="86830-191">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="86830-191">Create a program</span></span>
1. <span data-ttu-id="86830-192">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="86830-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="86830-193">En hello **Live** ficha herramienta AMSE de hello, haga clic en el área del programa Hola y seleccione **crear un nuevo programa**.</span><span class="sxs-lookup"><span data-stu-id="86830-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="86830-195">Nombre de programa hello y, si es necesario, ajuste hello **duración de la ventana de archivo** (qué horas too4 de los valores predeterminados).</span><span class="sxs-lookup"><span data-stu-id="86830-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="86830-196">También puede especificar una ubicación de almacenamiento o deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="86830-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="86830-197">Comprobar hello **inicio Hola programa ahora** cuadro.</span><span class="sxs-lookup"><span data-stu-id="86830-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="86830-198">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="86830-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="86830-199">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="86830-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="86830-200">Una vez que se ejecuta el programa de hello, confirme la reproducción, haga clic en el programa hello y vaya demasiado**programas de reproducción hello** y, a continuación, seleccione **con el Reproductor de Media de Azure**.</span><span class="sxs-lookup"><span data-stu-id="86830-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="86830-201">Una vez confirmado, haga clic en programa Hola de nuevo y seleccione **copiar tooClipboard de dirección URL de salida de hello** (o recuperar la información desde hello **información y configuración de programas** opción de menú de hello).</span><span class="sxs-lookup"><span data-stu-id="86830-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="86830-202">secuencia de Hello ahora está listo toobe incrustado en un reproductor o distribuida tooan público para live visualización.</span><span class="sxs-lookup"><span data-stu-id="86830-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="86830-203">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="86830-203">Troubleshooting</span></span>
<span data-ttu-id="86830-204">Vea hello [solución de problemas](media-services-troubleshooting-live-streaming.md) tema para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="86830-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="86830-205">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="86830-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86830-206">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="86830-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
