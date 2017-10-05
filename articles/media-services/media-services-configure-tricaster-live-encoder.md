---
title: "Configuración del codificador NewTek TriCaster para enviar una transmisión en vivo con velocidad de bits única | Microsoft Docs"
description: "En este tema se muestra cómo configurar el codificador en directo TriCaster para enviar una transmisión con velocidad de bits única a canales AMS habilitados para la codificación en directo."
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
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="fcf2f-103">Uso del codificador NewTek TriCaster para enviar una transmisión por secuencias en directo de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="fcf2f-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcf2f-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="fcf2f-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="fcf2f-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="fcf2f-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="fcf2f-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="fcf2f-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="fcf2f-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="fcf2f-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="fcf2f-108">En este tema se muestra cómo configurar el codificador en directo [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) para enviar una transmisión con velocidad de bits única a canales AMS habilitados para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="fcf2f-109">Para obtener más información, consulte [Uso de canales habilitados para realizar la codificación en directo con Servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="fcf2f-110">En este tutorial se muestra cómo administrar Servicios multimedia de Azure (AMS) con la herramienta Explorador de Servicios multimedia de Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="fcf2f-111">Esta herramienta solo se ejecuta en Windows PC.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="fcf2f-112">Si se encuentra en Mac o Linux, use Azure Portal para crear [canales](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) y [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fcf2f-113">Cuando se utiliza Tricaster para enviar una fuente de contribución a canales de AMS que están habilitados para la codificación en directo, puede haber problemas de audio y vídeo en el evento en directo si utiliza determinadas características de Tricaster, como un corte rápido entre las fuentes o el cambio a/de caretas.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="fcf2f-114">El equipo de AMS está trabajando en la solución de estos problemas; hasta entonces, no es recomendable usar estas características.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="fcf2f-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fcf2f-115">Prerequisites</span></span>
* [<span data-ttu-id="fcf2f-116">Creación de una cuenta de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="fcf2f-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="fcf2f-117">Asegúrese de que hay un punto de conexión de streaming en ejecución.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="fcf2f-118">Para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="fcf2f-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="fcf2f-119">Debe instalar la última versión de la herramienta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="fcf2f-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="fcf2f-120">Inicie la herramienta y conéctese a la cuenta de AMS.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="fcf2f-121">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="fcf2f-121">Tips</span></span>
* <span data-ttu-id="fcf2f-122">Siempre que sea posible, use una conexión a Internet por cable.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="fcf2f-123">Una buena regla general al determinar los requisitos de ancho de banda consiste en duplicar las velocidades de bits de streaming.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="fcf2f-124">Aunque no se trata de un requisito obligatorio, contribuirá a mitigar el impacto de la congestión de la red.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="fcf2f-125">Cuando se usen codificadores por software, cierre todos los programas innecesarios.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="fcf2f-126">Crear un canal</span><span class="sxs-lookup"><span data-stu-id="fcf2f-126">Create a channel</span></span>
1. <span data-ttu-id="fcf2f-127">En la herramienta AMSE, navegue a la pestaña **Directo** y haga clic con el botón derecho dentro del área de canales.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="fcf2f-128">Seleccione **Crear canal...**</span><span class="sxs-lookup"><span data-stu-id="fcf2f-128">Select **Create channel…**</span></span> <span data-ttu-id="fcf2f-129">en el menú.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="fcf2f-131">Especifique un nombre de canal (el campo de descripción es opcional).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="fcf2f-132">En Configuración de canal, seleccione **Estándar** para la opción Live Encoding, con el protocolo de entrada establecido en **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="fcf2f-133">Puede dejar todas las demás opciones como están.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="fcf2f-134">Asegúrese de que la opción **Iniciar el nuevo canal ahora** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="fcf2f-135">Haga clic en **Crear canal**.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="fcf2f-137">El canal puede tardar hasta 20 minutos en iniciarse.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="fcf2f-138">Mientras se inicia el canal puede [configurar el codificador](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcf2f-139">Tenga en cuenta que la facturación comienza tan pronto como el canal entra en un estado Listo.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="fcf2f-140">Para obtener más información, consulte [Estados del canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="fcf2f-141"><a id=configure_tricaster_rtmp></a>Configuración del codificador NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="fcf2f-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="fcf2f-142">En este tutorial se usa la siguiente configuración de salida.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="fcf2f-143">En el resto de esta sección se describen los pasos de configuración con más detalle.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="fcf2f-144">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="fcf2f-144">**Video**:</span></span>

* <span data-ttu-id="fcf2f-145">Codec (Códec): H.264</span><span class="sxs-lookup"><span data-stu-id="fcf2f-145">Codec: H.264</span></span>
* <span data-ttu-id="fcf2f-146">Profile (Perfil): High (Level 4.0) (Alto [Nivel 4.0])</span><span class="sxs-lookup"><span data-stu-id="fcf2f-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="fcf2f-147">Bitrate (Velocidad de bits): 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="fcf2f-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="fcf2f-148">Keyframe (Fotograma clave): 2 seconds (60 seconds) (2 segundos [60 segundos])</span><span class="sxs-lookup"><span data-stu-id="fcf2f-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="fcf2f-149">Frame Rate (Velocidad de fotogramas): 30</span><span class="sxs-lookup"><span data-stu-id="fcf2f-149">Frame Rate: 30</span></span>

<span data-ttu-id="fcf2f-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="fcf2f-150">**Audio**:</span></span>

* <span data-ttu-id="fcf2f-151">Codec (Códec): AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="fcf2f-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="fcf2f-152">Bitrate (Velocidad de bits): 192 kbps</span><span class="sxs-lookup"><span data-stu-id="fcf2f-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="fcf2f-153">Sample Rate (Frecuencia de muestreo): 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="fcf2f-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="fcf2f-154">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="fcf2f-154">Configuration steps</span></span>
1. <span data-ttu-id="fcf2f-155">Cree un nuevo proyecto de **NewTek TriCaster** según el origen de entrada de vídeo que se use.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="fcf2f-156">Una vez dentro de ese proyecto, busque el botón **Stream** (Transmitir) y haga clic en el icono de engranaje junto a él para acceder al menú de configuración de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="fcf2f-158">Cuando se abra el menú, haga clic en **New** (Nueva) bajo el encabezado de la conexión.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="fcf2f-159">Cuando se le pregunte por el tipo de conexión, seleccione **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="fcf2f-161">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-161">Click **OK**.</span></span>
5. <span data-ttu-id="fcf2f-162">Ahora se puede importar un perfil FMLE; para ello, haga clic en la flecha desplegable bajo **Streaming Profile** (Perfil de streaming) y vaya a **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="fcf2f-164">Vaya a la ubicación donde guardó el perfil FMLE configurado.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="fcf2f-165">Selecciónelo y presione **OK**(Aceptar).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="fcf2f-166">Una vez cargado el perfil, continúe con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="fcf2f-167">Obtenga la dirección URL de entrada del canal para asignarla al **punto de conexión de RTMP**de Tricaster.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="fcf2f-168">Navegue de nuevo a la herramienta AMSE y compruebe el estado de finalización del canal.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="fcf2f-169">Una vez que ha cambiado el estado de **Iniciando** a **En ejecución**, puede obtener la dirección URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="fcf2f-170">Mientras se ejecuta el canal, haga clic con el botón derecho en el nombre del canal, desplácese hacia abajo y mantenga el puntero sobre **Copy Input URL to clipboard** (Copiar dirección URL de entrada en el Portapapeles) y seleccione **Primary Input URL** (Dirección URL de entrada principal).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="fcf2f-172">Pegue esta información en el campo **Location** (Ubicación) en **Flash Server** dentro del proyecto de Tricaster.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="fcf2f-173">Además, asigne un nombre de transmisión en el campo **Id. de transmisión** .</span><span class="sxs-lookup"><span data-stu-id="fcf2f-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="fcf2f-174">Si se ha agregado la información de la transmisión al perfil FMLE, también se puede importar en esta sección; para ello, haga clic en **Import Settings** (Importar configuración), desplácese hasta el perfil FMLE guardado y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="fcf2f-175">Se deben rellenar los campos correspondientes de Flash Server con la información de FMLE.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="fcf2f-177">Cuando termine, haga clic en **OK** (Aceptar) en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="fcf2f-178">Cuando las entradas de audio y vídeo en Tricaster estén preparadas, comience a transmitir a AMS haciendo clic en el botón **Stream** (Transmitir).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="fcf2f-180">Antes de hacer clic en **Stream** (Transmitir), **debe** asegurarse de que el canal esté listo.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="fcf2f-181">Además, asegúrese de no dejar el canal en un estado Listo sin una fuente de contribución de entrada durante más de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="fcf2f-182">Reproducción de pruebas</span><span class="sxs-lookup"><span data-stu-id="fcf2f-182">Test playback</span></span>
<span data-ttu-id="fcf2f-183">Vaya a la herramienta AMSE y haga clic con el botón derecho en el canal que se va a probar.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="fcf2f-184">En el menú, mantenga el puntero sobre **Playback the Preview** (Reproducir la vista previa) y seleccione **with Azure Media Player** (con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="fcf2f-185">Si la transmisión aparece en el reproductor, entonces el codificador se configuró correctamente para conectarse a AMS.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="fcf2f-186">Si se recibe un error, se deberá restablecer el canal y ajustar la configuración del codificador.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="fcf2f-187">Consulte el tema de [solución de problemas](media-services-troubleshooting-live-streaming.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="fcf2f-188">Creación de un programa</span><span class="sxs-lookup"><span data-stu-id="fcf2f-188">Create a program</span></span>
1. <span data-ttu-id="fcf2f-189">Una vez confirmada la reproducción de canales, cree un programa.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="fcf2f-190">En la pestaña **Live** (Directo) de la herramienta AMSE, haga clic con el botón derecho dentro del área de programas y seleccione **Create New Program** (Crear programa).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="fcf2f-192">Dé nombre al programa y, si es necesario, ajuste el valor de **Duración de la ventana de archivo** (que de forma predeterminada es 4 horas).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="fcf2f-193">También puede especificar una ubicación de almacenamiento o dejar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="fcf2f-194">Active la casilla **Iniciar el programa ahora** .</span><span class="sxs-lookup"><span data-stu-id="fcf2f-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="fcf2f-195">Haga clic en **Crear programa**.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="fcf2f-196">La creación de programas tarda menos que la creación de canales.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="fcf2f-197">Cuando el programa esté en ejecución, confirme la reproducción. Para ello, haga clic con el botón derecho en el programa y vaya a **Playback the program(s)** (Reproducir los programas). Luego, seleccione **with Azure Media Player** (con Azure Media Player).</span><span class="sxs-lookup"><span data-stu-id="fcf2f-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="fcf2f-198">Una vez confirmada, haga clic con el botón derecho de nuevo en el programa y seleccione **Copy the Output URL to Clipboard** (Copiar la dirección URL de salida en el Portapapeles) o recupere esta información con la opción **Program information and settings**(Información y configuración del programa) en el menú.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="fcf2f-199">La transmisión está ahora preparada para insertarse en un reproductor o distribuirse a una audiencia para su visualización en directo.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="fcf2f-200">solución de problemas</span><span class="sxs-lookup"><span data-stu-id="fcf2f-200">Troubleshooting</span></span>
<span data-ttu-id="fcf2f-201">Consulte el tema de [solución de problemas](media-services-troubleshooting-live-streaming.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="fcf2f-202">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="fcf2f-202">Next step</span></span>
<span data-ttu-id="fcf2f-203">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="fcf2f-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fcf2f-204">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="fcf2f-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
