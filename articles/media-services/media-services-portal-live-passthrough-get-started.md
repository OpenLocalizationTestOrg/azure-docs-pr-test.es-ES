---
title: Streaming en vivo con codificadores locales mediante Azure Portal | Microsoft Docs
description: "Este tutorial le guiará por los pasos para crear un canal que esté configurado para una entrega de paso a través."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="d7d0d-103">Realización de streaming en vivo con codificadores locales mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d7d0d-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7d0d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d7d0d-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="d7d0d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d7d0d-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="d7d0d-106">REST</span><span class="sxs-lookup"><span data-stu-id="d7d0d-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="d7d0d-107">Este tutorial le guiará por los pasos para usar el Portal de Azure para crear un **Canal** que esté configurado para una entrega de paso a través.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d7d0d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7d0d-108">Prerequisites</span></span>
<span data-ttu-id="d7d0d-109">Estos son los requisitos previos para completar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="d7d0d-110">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-110">An Azure account.</span></span> <span data-ttu-id="d7d0d-111">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="d7d0d-112">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-112">A Media Services account.</span></span> <span data-ttu-id="d7d0d-113">Para crear una cuenta de Media Services, consulte el tema [Creación de una cuenta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d7d0d-114">Una cámara web.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-114">A webcam.</span></span> <span data-ttu-id="d7d0d-115">Por ejemplo, el [codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="d7d0d-116">Es importante que revise los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d7d0d-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="d7d0d-117">Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="d7d0d-118">Información general de streaming en vivo con Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="d7d0d-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="d7d0d-119">Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple</span><span class="sxs-lookup"><span data-stu-id="d7d0d-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="d7d0d-120"><a id="scenario"></a>Escenario común de streaming en vivo</span><span class="sxs-lookup"><span data-stu-id="d7d0d-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="d7d0d-121">Los pasos siguientes describen las tareas que conlleva la creación de aplicaciones comunes de streaming en vivo que usan canales configurados para entregas de paso a través.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="d7d0d-122">Este tutorial muestra cómo crear y administrar un canal de paso a través y eventos en directo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="d7d0d-123">Asegúrese de que el punto de conexión de streaming desde el que va a transmitir el contenido esté en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="d7d0d-124">Conecte una cámara de vídeo a un equipo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="d7d0d-125">Inicie y configure un codificador en directo local que genere una transmisión de RTMP o MP4 fragmentado con velocidad de bits múltiple.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="d7d0d-126">Para obtener más información, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="d7d0d-127">Este paso también puede realizarse después de crear el canal.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="d7d0d-128">Cree e inicie un canal de paso a través.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="d7d0d-129">Recupere la URL de ingesta de canales.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="d7d0d-130">El codificador en directo usa la URL de ingesta para enviar la secuencia al canal.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="d7d0d-131">Recupere la URL de vista previa de canal.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="d7d0d-132">Use esta dirección URL para comprobar que el canal recibe correctamente la secuencia en vivo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="d7d0d-133">Cree un evento o programa en directo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="d7d0d-134">Con el Portal de Azure, al crear un evento en directo también se crea un recurso.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="d7d0d-135">Inicie el evento o programa cuando esté listo para iniciar el streaming y el archivo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="d7d0d-136">Si lo desea, puede señalar el codificador en directo para iniciar un anuncio.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="d7d0d-137">El anuncio se inserta en el flujo de salida.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="d7d0d-138">Detenga el evento o programa cuando quiera detener el streaming y el archivo del evento.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="d7d0d-139">Elimine el evento o programa (y, opcionalmente, elimine el recurso).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="d7d0d-140">Consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md) para obtener información acerca de los conceptos y las consideraciones relacionadas con el streaming en vivo con codificadores locales y canales de paso a través.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="d7d0d-141">Visualización de notificaciones y errores</span><span class="sxs-lookup"><span data-stu-id="d7d0d-141">To view notifications and errors</span></span>
<span data-ttu-id="d7d0d-142">Si desea ver las notificaciones y los errores generados por el Portal de Azure, haga clic en el icono de notificación.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Notificaciones](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="d7d0d-144">Creación e inicio de canales de paso a través y eventos</span><span class="sxs-lookup"><span data-stu-id="d7d0d-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="d7d0d-145">Un canal está asociado a eventos y programas que le permiten controlar la publicación y el almacenamiento de segmentos en una transmisión en vivo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="d7d0d-146">Los canales administran los eventos.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-146">Channels manage events.</span></span> 

<span data-ttu-id="d7d0d-147">Puede especificar la cantidad de horas que desea conservar el contenido grabado del programa en la configuración de la duración de **Ventana de archivo** .</span><span class="sxs-lookup"><span data-stu-id="d7d0d-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="d7d0d-148">Este valor se puede establecer desde un mínimo de cinco minutos a un máximo de 25 horas.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="d7d0d-149">La duración de la ventana de archivo también indica el tiempo máximo que los clientes pueden buscar hacia atrás a partir de la posición en vivo actual.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="d7d0d-150">Los eventos pueden transmitirse durante la cantidad de tiempo especificada, pero el contenido que escape de esa longitud de ventana se descartará continuamente.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="d7d0d-151">El valor de esta propiedad también determina durante cuánto tiempo los manifiestos de cliente pueden crecer.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="d7d0d-152">Cada evento está asociado a un recurso.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-152">Each event is associated with an asset.</span></span> <span data-ttu-id="d7d0d-153">Para publicar el evento, debe crear un localizador a petición para el recurso asociado.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="d7d0d-154">Contar con este localizador le permite crear una dirección URL de streaming que puede proporcionar a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="d7d0d-155">Un canal es compatible con hasta tres eventos en ejecución simultánea, por lo que puede crear varios archivos de la misma transmisión entrante.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="d7d0d-156">Esto le permite publicar y archivar distintas partes de un evento, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="d7d0d-157">Por ejemplo, el requisito de su empresa es solo archivar seis horas de un programa, pero difundir solo los últimos diez minutos.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="d7d0d-158">Para lograrlo, necesita crear dos programas en ejecución simultánea.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="d7d0d-159">Un programa está definido para archivar seis horas del evento, pero no está publicado.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="d7d0d-160">El otro programa está definido para archivar durante diez minutos y este programa sí se publica.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="d7d0d-161">No debería reutilizar eventos en directo ya existentes.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-161">You should not reuse existing live events.</span></span> <span data-ttu-id="d7d0d-162">En su lugar, cree e inicie un evento nuevo para cada evento.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="d7d0d-163">Inicie el evento cuando esté listo para iniciar el streaming y el archivo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="d7d0d-164">Detenga el programa cuando quiera detener el streaming y el archivo del evento.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="d7d0d-165">Para eliminar contenido archivado, detenga y elimine el evento y, a continuación, elimine el recurso asociado.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="d7d0d-166">No se puede eliminar un recurso si lo está usando un evento; primero se debe eliminar el evento.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="d7d0d-167">Incluso después de detener y eliminar el evento, los usuarios podrán transmitir el contenido archivado como un vídeo a petición siempre que no elimine el recurso.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="d7d0d-168">Si desea conservar el contenido archivado, pero no hacerlo disponible para la transmisión, elimine el localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="d7d0d-169">Uso del portal para crear un canal</span><span class="sxs-lookup"><span data-stu-id="d7d0d-169">To use the portal to create a channel</span></span>
<span data-ttu-id="d7d0d-170">Esta sección muestra cómo utilizar la opción **Creación rápida** para crear un canal de paso a través.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="d7d0d-171">Para más información sobre este tipo de canales, consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="d7d0d-172">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d7d0d-173">En la ventana **Configuración**, haga clic en **Streaming en vivo**.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Introducción](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="d7d0d-175">Aparece la ventana **Streaming en vivo** .</span><span class="sxs-lookup"><span data-stu-id="d7d0d-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="d7d0d-176">Haga clic en **Creación rápida** para crear un canal de paso a través con el protocolo de introducción RTMP.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="d7d0d-177">Aparece la ventana **CREAR UN NUEVO CANAL** .</span><span class="sxs-lookup"><span data-stu-id="d7d0d-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="d7d0d-178">Asigne un nombre al nuevo canal y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="d7d0d-179">Con ello, se crea un canal de paso a través con el protocolo de introducción RTMP.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="d7d0d-180">Creación de eventos</span><span class="sxs-lookup"><span data-stu-id="d7d0d-180">Create events</span></span>
1. <span data-ttu-id="d7d0d-181">Seleccione el canal al que desea agregar un evento.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="d7d0d-182">Pulse el botón **Evento en directo** .</span><span class="sxs-lookup"><span data-stu-id="d7d0d-182">Press **Live Event** button.</span></span>

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="d7d0d-184">Obtención de direcciones URL de introducción</span><span class="sxs-lookup"><span data-stu-id="d7d0d-184">Get ingest URLs</span></span>
<span data-ttu-id="d7d0d-185">Una vez creado el canal, obtendrá direcciones URL de introducción que se proporcionarán al codificador en directo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="d7d0d-186">El codificador usa estas direcciones URL para introducir una secuencia en vivo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-186">The encoder uses these URLs to input a live stream.</span></span>

![Creado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="d7d0d-188">Visualización del evento</span><span class="sxs-lookup"><span data-stu-id="d7d0d-188">Watch the event</span></span>
<span data-ttu-id="d7d0d-189">Para ver el evento, haga clic en **Inspección** en el Portal de Azure o copie la dirección URL de streaming y use el reproductor que prefiera.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Creado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="d7d0d-191">El evento en directo se convierte automáticamente en contenido a petición cuando se detiene.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="d7d0d-192">Limpieza</span><span class="sxs-lookup"><span data-stu-id="d7d0d-192">Clean up</span></span>
<span data-ttu-id="d7d0d-193">Para más información sobre este tipo de canales, consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="d7d0d-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="d7d0d-194">Un canal se puede detener solo cuando se hayan detenido todos los eventos o programas del canal.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="d7d0d-195">Cuando se detiene el canal, no se incurre en ningún cargo.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="d7d0d-196">Cuando necesite iniciarlo de nuevo, tendrá la misma URL de introducción, por lo que no necesitará volver a configurar su codificador.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="d7d0d-197">Un canal se puede eliminar solo cuando se hayan eliminado todos los eventos en directo del canal.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="d7d0d-198">Visualización del contenido archivado</span><span class="sxs-lookup"><span data-stu-id="d7d0d-198">View archived content</span></span>
<span data-ttu-id="d7d0d-199">Incluso después de detener y eliminar el evento, los usuarios podrán transmitir el contenido archivado como un vídeo a petición siempre que no elimine el recurso.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="d7d0d-200">No se puede eliminar un recurso si lo está usando un evento; primero se debe eliminar el evento.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="d7d0d-201">Para administrar los recursos seleccione **Configuración** y haga clic en **Recursos**.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![recursos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="d7d0d-203">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="d7d0d-203">Next step</span></span>
<span data-ttu-id="d7d0d-204">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d7d0d-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7d0d-205">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d7d0d-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

