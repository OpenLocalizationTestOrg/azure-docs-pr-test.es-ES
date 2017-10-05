---
title: "Configuración del codificador FMLE para enviar una transmisión en vivo con velocidad de bits única | Microsoft Docs"
description: "En este tema se muestra cómo configurar el codificador Flash Media Live Encoder (FMLE) para enviar una transmisión con velocidad de bits única a canales AMS habilitados para la codificación en directo."
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
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="19e4c-103">Uso del codificador FMLE para enviar una transmisión por secuencias en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="19e4c-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19e4c-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="19e4c-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="19e4c-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="19e4c-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="19e4c-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="19e4c-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="19e4c-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="19e4c-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="19e4c-108">En este tema se muestra cómo configurar el codificador [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) para enviar una transmisión con velocidad de bits única a canales AMS habilitados para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="19e4c-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="19e4c-109">Para obtener más información, consulte [Uso de canales habilitados para realizar la codificación en directo con Servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="19e4c-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="19e4c-110">En este tutorial se muestra cómo administrar Servicios multimedia de Azure (AMS) con la herramienta Explorador de Servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="19e4c-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="19e4c-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="19e4c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="19e4c-112">Si se encuentra en Mac o Linux, use Azure Portal para crear [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="19e4c-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="19e4c-113">Tenga en cuenta que en este tutorial se describe el uso de AAC.</span><span class="sxs-lookup"><span data-stu-id="19e4c-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="19e4c-114">Sin embargo, FMLE no es compatible con AAC de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19e4c-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="19e4c-115">Deberá adquirir un complemento para la codificación de AAC como el de MainConcept: [Complemento de AAC](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="19e4c-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19e4c-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19e4c-116">Prerequisites</span></span>
* [<span data-ttu-id="19e4c-117">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="19e4c-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="19e4c-118">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="19e4c-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="19e4c-119">Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="19e4c-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="19e4c-120">Debe instalar la última versión de la herramienta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="19e4c-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="19e4c-121">Inicie la herramienta y conéctese a la cuenta de AMS.</span><span class="sxs-lookup"><span data-stu-id="19e4c-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="19e4c-122">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="19e4c-122">Tips</span></span>
* <span data-ttu-id="19e4c-123">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="19e4c-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="19e4c-124">Una buena regla general al determinar los requisitos de ancho de banda consiste en duplicar las velocidades de bits de streaming.</span><span class="sxs-lookup"><span data-stu-id="19e4c-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="19e4c-125">Aunque no se trata de un requisito obligatorio, contribuirá a mitigar el impacto de la congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="19e4c-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="19e4c-126">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="19e4c-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="19e4c-127">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="19e4c-127">Create a channel</span></span>
1. <span data-ttu-id="19e4c-128">En la herramienta AMSE, navegue a la pestaña **Directo** y haga clic con el botón derecho dentro del área de canales.</span><span class="sxs-lookup"><span data-stu-id="19e4c-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="19e4c-129">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="19e4c-129">Select **Create channel…**</span></span> <span data-ttu-id="19e4c-130">en el menú.</span><span class="sxs-lookup"><span data-stu-id="19e4c-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="19e4c-132">Especifique un nombre de canal (el campo de descripción es opcional).</span><span class="sxs-lookup"><span data-stu-id="19e4c-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="19e4c-133">En Configuración de canal, seleccione **Estándar** para la opción Live Encoding, con el protocolo de entrada establecido en **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="19e4c-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="19e4c-134">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="19e4c-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="19e4c-135">Asegúrese de que la opción **Iniciar el nuevo canal ahora** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="19e4c-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="19e4c-136">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="19e4c-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="19e4c-138">El canal puede tardar hasta 20 minutos en iniciarse.</span><span class="sxs-lookup"><span data-stu-id="19e4c-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="19e4c-139">Mientras se inicia el canal puede [configurar el codificador](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="19e4c-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e4c-140">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="19e4c-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="19e4c-141">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="19e4c-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="19e4c-142"><a id=configure_fmle_rtmp></a>Configuración del codificador FMLE</span><span class="sxs-lookup"><span data-stu-id="19e4c-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="19e4c-143">En este tutorial se usa la siguiente configuración de salida.</span><span class="sxs-lookup"><span data-stu-id="19e4c-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="19e4c-144">En el resto de esta sección se describen los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="19e4c-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="19e4c-145">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="19e4c-145">**Video**:</span></span>

* <span data-ttu-id="19e4c-146">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="19e4c-146">Codec: H.264</span></span>
* <span data-ttu-id="19e4c-147">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="19e4c-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="19e4c-148">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="19e4c-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="19e4c-149">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="19e4c-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="19e4c-150">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="19e4c-150">Frame Rate: 30</span></span>

<span data-ttu-id="19e4c-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="19e4c-151">**Audio**:</span></span>

* <span data-ttu-id="19e4c-152">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="19e4c-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="19e4c-153">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="19e4c-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="19e4c-154">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="19e4c-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="19e4c-155">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="19e4c-155">Configuration steps</span></span>
1. <span data-ttu-id="19e4c-156">Vaya a la interfaz de Flash Media Live Encoder (FMLE) en el equipo que esté usando.</span><span class="sxs-lookup"><span data-stu-id="19e4c-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="19e4c-157">La interfaz es una página principal de configuración.</span><span class="sxs-lookup"><span data-stu-id="19e4c-157">The interface is one main page of settings.</span></span> <span data-ttu-id="19e4c-158">Tome nota de la siguiente configuración recomendada para empezar a trabajar con streaming mediante FMLE.</span><span class="sxs-lookup"><span data-stu-id="19e4c-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="19e4c-159">Format (Formato): H.264, Frame Rate (Velocidad de fotogramas): 30.00</span><span class="sxs-lookup"><span data-stu-id="19e4c-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="19e4c-160">Input Size (Tamaño de entrada): 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="19e4c-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="19e4c-161">Bit Rate (Velocidad de bits): 5000 kbps (se puede ajustar en función de las limitaciones de red)</span><span class="sxs-lookup"><span data-stu-id="19e4c-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="19e4c-163">Al usar orígenes entrelazados, marque la opción "Deinterlace" (Desentrelazar).</span><span class="sxs-lookup"><span data-stu-id="19e4c-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="19e4c-164">Seleccione el icono de llave junto a Format (Formato). Estas opciones de configuración adicionales deben ser:</span><span class="sxs-lookup"><span data-stu-id="19e4c-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="19e4c-165">Profile (Perfil): Main (Principal)</span><span class="sxs-lookup"><span data-stu-id="19e4c-165">Profile: Main</span></span>
   * <span data-ttu-id="19e4c-166">Level (Nivel): 4.0</span><span class="sxs-lookup"><span data-stu-id="19e4c-166">Level: 4.0</span></span>
   * <span data-ttu-id="19e4c-167">Keyframe Frequency (Frecuencia de fotogramas clave): 2 seconds (2 segundos)</span><span class="sxs-lookup"><span data-stu-id="19e4c-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="19e4c-169">Establezca la siguiente configuración de audio importante:</span><span class="sxs-lookup"><span data-stu-id="19e4c-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="19e4c-170">Format (Formato): AAC</span><span class="sxs-lookup"><span data-stu-id="19e4c-170">Format: AAC</span></span>
   * <span data-ttu-id="19e4c-171">Sample Rate (Frecuencia de muestreo): 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="19e4c-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="19e4c-172">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="19e4c-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="19e4c-174">Obtenga la dirección URL de entrada del canal para asignarla al **punto de conexión de RTMP**de FMLE.</span><span class="sxs-lookup"><span data-stu-id="19e4c-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="19e4c-175">Navegue de nuevo a la herramienta AMSE y compruebe el estado de finalización del canal.</span><span class="sxs-lookup"><span data-stu-id="19e4c-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="19e4c-176">Una vez que ha cambiado el estado de **Iniciando** a **En ejecución**, puede obtener la dirección URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="19e4c-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="19e4c-177">Mientras se ejecuta el canal, haga clic con el botón derecho en el nombre del canal, desplácese hacia abajo y mantenga el puntero sobre **Copy Input URL to clipboard** (Copiar dirección URL de entrada en el Portapapeles) y seleccione **Primary Input URL** (Dirección URL de entrada principal).</span><span class="sxs-lookup"><span data-stu-id="19e4c-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="19e4c-179">Pegue esta información en el campo **Dirección URL de FMS** de la sección de salida y asigne un nombre de transmisión.</span><span class="sxs-lookup"><span data-stu-id="19e4c-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="19e4c-181">Para obtener redundancia adicional, repita estos pasos con la dirección URL de entrada secundaria.</span><span class="sxs-lookup"><span data-stu-id="19e4c-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="19e4c-182">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="19e4c-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e4c-183">Antes de hacer clic en **Conectar**, **debe** asegurarse de que el canal esté listo.</span><span class="sxs-lookup"><span data-stu-id="19e4c-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="19e4c-184">Además, asegúrese de no dejar el canal en un estado Listo sin una fuente de contribución de entrada durante más de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="19e4c-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="19e4c-185">Reproducción de pruebas</span><span class="sxs-lookup"><span data-stu-id="19e4c-185">Test playback</span></span>

<span data-ttu-id="19e4c-186">Vaya a la herramienta AMSE y haga clic con el botón derecho en el canal que se va a probar.</span><span class="sxs-lookup"><span data-stu-id="19e4c-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="19e4c-187">En el menú, mantenga el puntero sobre **Playback the Preview** (Reproducir la vista previa) y seleccione **with Azure Media Player** (con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="19e4c-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="19e4c-188">Si la transmisión aparece en el reproductor, entonces el codificador se configuró correctamente para conectarse a AMS.</span><span class="sxs-lookup"><span data-stu-id="19e4c-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="19e4c-189">Si se recibe un error, se deberá restablecer el canal y ajustar la configuración del codificador.</span><span class="sxs-lookup"><span data-stu-id="19e4c-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="19e4c-190">Consulte el tema de [solución de problemas](media-services-troubleshooting-live-streaming.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="19e4c-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="19e4c-191">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="19e4c-191">Create a program</span></span>
1. <span data-ttu-id="19e4c-192">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="19e4c-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="19e4c-193">En la pestaña **Live** (Directo) de la herramienta AMSE, haga clic con el botón derecho dentro del área de programas y seleccione **Create New Program** (Crear programa).</span><span class="sxs-lookup"><span data-stu-id="19e4c-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="19e4c-195">Dé nombre al programa y, si es necesario, ajuste el valor de **Duración de la ventana de archivo** (que de forma predeterminada es 4 horas).</span><span class="sxs-lookup"><span data-stu-id="19e4c-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="19e4c-196">También puede especificar una ubicación de almacenamiento o dejar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="19e4c-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="19e4c-197">Active la casilla **Iniciar el programa ahora** .</span><span class="sxs-lookup"><span data-stu-id="19e4c-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="19e4c-198">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="19e4c-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="19e4c-199">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="19e4c-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="19e4c-200">Cuando el programa esté en ejecución, confirme la reproducción. Para ello, haga clic con el botón derecho en el programa y vaya a **Playback the program(s)** (Reproducir los programas). Luego, seleccione **with Azure Media Player** (con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="19e4c-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="19e4c-201">Una vez confirmada, haga clic con el botón derecho de nuevo en el programa y seleccione **Copy the Output URL to Clipboard** (Copiar la dirección URL de salida en el Portapapeles) o recupere esta información con la opción **Program information and settings**(Información y configuración del programa) en el menú.</span><span class="sxs-lookup"><span data-stu-id="19e4c-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="19e4c-202">La transmisión está ahora preparada para insertarse en un reproductor o distribuirse a una audiencia para su visualización en directo.</span><span class="sxs-lookup"><span data-stu-id="19e4c-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="19e4c-203">solución de problemas</span><span class="sxs-lookup"><span data-stu-id="19e4c-203">Troubleshooting</span></span>
<span data-ttu-id="19e4c-204">Consulte el tema de [solución de problemas](media-services-troubleshooting-live-streaming.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="19e4c-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="19e4c-205">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="19e4c-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="19e4c-206">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="19e4c-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
