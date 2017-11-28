---
title: "Uso del codificador Telestream Wirecast para enviar una transmisión en vivo con velocidad de bits única | Microsoft Docs"
description: "En este tema se muestra cómo configurar el codificador en directo Wirecast para enviar una transmisión con velocidad de bits única a canales AMS habilitados para la codificación en directo. "
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
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="97214-103">Uso del codificador Wirecast para enviar una transmisión por secuencias en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="97214-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97214-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="97214-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="97214-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="97214-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="97214-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="97214-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="97214-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="97214-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="97214-108">En este tema se muestra cómo configurar el codificador en directo [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) para enviar una transmisión con velocidad de bits única a canales AMS habilitados para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="97214-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="97214-109">Para obtener más información, consulte [Uso de canales habilitados para realizar la codificación en directo con Servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="97214-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="97214-110">En este tutorial se muestra cómo administrar Servicios multimedia de Azure (AMS) con la herramienta Explorador de Servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="97214-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="97214-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="97214-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="97214-112">Si se encuentra en Mac o Linux, use Azure Portal para crear [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="97214-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97214-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="97214-113">Prerequisites</span></span>
* [<span data-ttu-id="97214-114">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="97214-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="97214-115">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="97214-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="97214-116">Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="97214-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="97214-117">Debe instalar la última versión de la herramienta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="97214-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="97214-118">Inicie la herramienta y conéctese a la cuenta de AMS.</span><span class="sxs-lookup"><span data-stu-id="97214-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="97214-119">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="97214-119">Tips</span></span>
* <span data-ttu-id="97214-120">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="97214-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="97214-121">Una buena regla general al determinar los requisitos de ancho de banda consiste en duplicar las velocidades de bits de streaming.</span><span class="sxs-lookup"><span data-stu-id="97214-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="97214-122">Aunque no se trata de un requisito obligatorio, contribuirá a mitigar el impacto de la congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="97214-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="97214-123">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="97214-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="97214-124">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="97214-124">Create a channel</span></span>
1. <span data-ttu-id="97214-125">En la herramienta AMSE, navegue a la pestaña **Directo** y haga clic con el botón derecho dentro del área de canales.</span><span class="sxs-lookup"><span data-stu-id="97214-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="97214-126">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="97214-126">Select **Create channel…**</span></span> <span data-ttu-id="97214-127">en el menú.</span><span class="sxs-lookup"><span data-stu-id="97214-127">from the menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="97214-129">Especifique un nombre de canal (el campo de descripción es opcional).</span><span class="sxs-lookup"><span data-stu-id="97214-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="97214-130">En Configuración de canal, seleccione **Estándar** para la opción Live Encoding, con el protocolo de entrada establecido en **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="97214-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="97214-131">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="97214-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="97214-132">Asegúrese de que la opción **Iniciar el nuevo canal ahora** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="97214-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="97214-133">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="97214-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="97214-135">El canal puede tardar hasta 20 minutos en iniciarse.</span><span class="sxs-lookup"><span data-stu-id="97214-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="97214-136">Mientras se inicia el canal puede [configurar el codificador](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="97214-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97214-137">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="97214-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="97214-138">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="97214-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="97214-139"><a id=configure_wirecast_rtmp></a>Configuración del codificador Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="97214-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="97214-140">En este tutorial se usa la siguiente configuración de salida.</span><span class="sxs-lookup"><span data-stu-id="97214-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="97214-141">En el resto de esta sección se describen los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="97214-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="97214-142">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="97214-142">**Video**:</span></span>

* <span data-ttu-id="97214-143">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="97214-143">Codec: H.264</span></span>
* <span data-ttu-id="97214-144">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="97214-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="97214-145">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="97214-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="97214-146">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="97214-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="97214-147">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="97214-147">Frame Rate: 30</span></span>

<span data-ttu-id="97214-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="97214-148">**Audio**:</span></span>

* <span data-ttu-id="97214-149">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="97214-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="97214-150">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="97214-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="97214-151">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="97214-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="97214-152">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="97214-152">Configuration steps</span></span>
1. <span data-ttu-id="97214-153">Abra la aplicación de Telestream Wirecast en el equipo que está usando y configúrela para el streaming de RTMP.</span><span class="sxs-lookup"><span data-stu-id="97214-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="97214-154">Para configurar la salida, vaya a la pestaña **Output** (Salida) y seleccione **Output Settings** (Configuración de salida).</span><span class="sxs-lookup"><span data-stu-id="97214-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="97214-155">Asegúrese de que **Output Destination** (Destino de salida) esté establecido en **RTMP Server** (Servidor RTMP).</span><span class="sxs-lookup"><span data-stu-id="97214-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="97214-156">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="97214-156">Click **OK**.</span></span>
4. <span data-ttu-id="97214-157">En la página de configuración, establezca el campo **Destination** (Destino) en **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="97214-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="97214-158">El perfil de codificación está previamente seleccionado como **Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="97214-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="97214-159">Para personalizar esta configuración, seleccione el icono de engranaje a la derecha de la lista desplegable y, luego, elija **New Preset**(Nuevo valor preestablecido).</span><span class="sxs-lookup"><span data-stu-id="97214-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="97214-161">Configure los valores preestablecidos del codificador.</span><span class="sxs-lookup"><span data-stu-id="97214-161">Configure encoder presets.</span></span>

    <span data-ttu-id="97214-162">Asigne un nombre al valor preestablecido y busque la siguiente configuración recomendada:</span><span class="sxs-lookup"><span data-stu-id="97214-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="97214-163">**Vídeo**</span><span class="sxs-lookup"><span data-stu-id="97214-163">**Video**</span></span>

   * <span data-ttu-id="97214-164">Encoder (Codificador): MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="97214-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="97214-165">Frames per Second (Fotogramas por segundo): 30</span><span class="sxs-lookup"><span data-stu-id="97214-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="97214-166">Bit Rate (Velocidad de bits): 5000 kbps/sec (seg.) (se puede ajustar en función de las limitaciones de red)</span><span class="sxs-lookup"><span data-stu-id="97214-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="97214-167">Profile (Perfil): Main (Principal)</span><span class="sxs-lookup"><span data-stu-id="97214-167">Profile: Main</span></span>
   * <span data-ttu-id="97214-168">Key frame every (Fotograma clave cada): 60 frames (fotogramas)</span><span class="sxs-lookup"><span data-stu-id="97214-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="97214-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="97214-169">**Audio**</span></span>

   * <span data-ttu-id="97214-170">Target bit rate (Velocidad de bits de destino): 192 kbits/sec (seg)</span><span class="sxs-lookup"><span data-stu-id="97214-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="97214-171">Sample Rate (Frecuencia de muestreo): 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="97214-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="97214-173">Presione **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="97214-173">Press **Save**.</span></span>

    <span data-ttu-id="97214-174">El campo de codificación tiene ahora el perfil recién creado disponible para la selección.</span><span class="sxs-lookup"><span data-stu-id="97214-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="97214-175">Asegúrese de que esté seleccionado el nuevo perfil.</span><span class="sxs-lookup"><span data-stu-id="97214-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="97214-176">Obtenga la dirección URL de entrada del canal para asignarla al **punto de conexión de RTMP**de Wirecast.</span><span class="sxs-lookup"><span data-stu-id="97214-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="97214-177">Navegue de nuevo a la herramienta AMSE y compruebe el estado de finalización del canal.</span><span class="sxs-lookup"><span data-stu-id="97214-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="97214-178">Una vez que ha cambiado el estado de **Iniciando** a **En ejecución**, puede obtener la dirección URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="97214-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="97214-179">Mientras se ejecuta el canal, haga clic con el botón derecho en el nombre del canal, desplácese hacia abajo y mantenga el puntero sobre **Copy Input URL to clipboard** (Copiar dirección URL de entrada en el Portapapeles) y seleccione **Primary Input URL** (Dirección URL de entrada principal).</span><span class="sxs-lookup"><span data-stu-id="97214-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="97214-181">En la ventana **Output Settings** (Configuración de salida) de Wirecast, pegue esta información en el campo **Address** (Dirección) de la sección de salida y asigne un nombre de transmisión.</span><span class="sxs-lookup"><span data-stu-id="97214-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="97214-183">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="97214-183">Select **OK**.</span></span>
2. <span data-ttu-id="97214-184">En la pantalla principal de **Wirecast**, confirme que los orígenes de audio y vídeo están listos y haga clic en **Stream** (Transmitir) en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="97214-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="97214-186">Antes de hacer clic en **Stream** (Transmitir), **debe** asegurarse de que el canal esté listo.</span><span class="sxs-lookup"><span data-stu-id="97214-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="97214-187">Además, asegúrese de no dejar el canal en un estado Listo sin una fuente de contribución de entrada durante más de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="97214-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="97214-188">Reproducción de pruebas</span><span class="sxs-lookup"><span data-stu-id="97214-188">Test playback</span></span>

<span data-ttu-id="97214-189">Vaya a la herramienta AMSE y haga clic con el botón derecho en el canal que se va a probar.</span><span class="sxs-lookup"><span data-stu-id="97214-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="97214-190">En el menú, mantenga el puntero sobre **Playback the Preview** (Reproducir la vista previa) y seleccione **with Azure Media Player** (con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="97214-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="97214-191">Si la transmisión aparece en el reproductor, entonces el codificador se configuró correctamente para conectarse a AMS.</span><span class="sxs-lookup"><span data-stu-id="97214-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="97214-192">Si se recibe un error, se deberá restablecer el canal y ajustar la configuración del codificador.</span><span class="sxs-lookup"><span data-stu-id="97214-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="97214-193">Consulte el tema de [solución de problemas](media-services-troubleshooting-live-streaming.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="97214-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="97214-194">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="97214-194">Create a program</span></span>
1. <span data-ttu-id="97214-195">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="97214-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="97214-196">En la pestaña **Live** (Directo) de la herramienta AMSE, haga clic con el botón derecho dentro del área de programas y seleccione **Create New Program** (Crear programa).</span><span class="sxs-lookup"><span data-stu-id="97214-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="97214-198">Dé nombre al programa y, si es necesario, ajuste el valor de **Duración de la ventana de archivo** (que de forma predeterminada es 4 horas).</span><span class="sxs-lookup"><span data-stu-id="97214-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="97214-199">También puede especificar una ubicación de almacenamiento o dejar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="97214-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="97214-200">Active la casilla **Iniciar el programa ahora** .</span><span class="sxs-lookup"><span data-stu-id="97214-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="97214-201">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="97214-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="97214-202">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="97214-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="97214-203">Cuando el programa esté en ejecución, confirme la reproducción. Para ello, haga clic con el botón derecho en el programa y vaya a **Playback the program(s)** (Reproducir los programas). Luego, seleccione **with Azure Media Player** (con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="97214-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="97214-204">Una vez confirmada, haga clic con el botón derecho de nuevo en el programa y seleccione **Copy the Output URL to Clipboard** (Copiar la dirección URL de salida en el Portapapeles) o recupere esta información con la opción **Program information and settings**(Información y configuración del programa) en el menú.</span><span class="sxs-lookup"><span data-stu-id="97214-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="97214-205">La transmisión está ahora preparada para insertarse en un reproductor o distribuirse a una audiencia para su visualización en directo.</span><span class="sxs-lookup"><span data-stu-id="97214-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="97214-206">solución de problemas</span><span class="sxs-lookup"><span data-stu-id="97214-206">Troubleshooting</span></span>
<span data-ttu-id="97214-207">Consulte el tema de [solución de problemas](media-services-troubleshooting-live-streaming.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="97214-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="97214-208">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="97214-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="97214-209">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="97214-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
