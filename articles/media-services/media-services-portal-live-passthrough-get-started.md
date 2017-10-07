---
title: secuencia de aaaLive con codificadores locales mediante Hola portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de creación de un canal que está configurado para la entrega de una acceso directo."
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
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="a1f90-103">¿Cómo tooperform streaming en vivo con local codificadores mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a1f90-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1f90-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a1f90-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="a1f90-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a1f90-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="a1f90-106">REST</span><span class="sxs-lookup"><span data-stu-id="a1f90-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="a1f90-107">Este tutorial le guiará por los pasos de hello del uso de hello Azure toocreate portal un **canal** que está configurado para la entrega de una acceso directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a1f90-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a1f90-108">Prerequisites</span></span>
<span data-ttu-id="a1f90-109">tutorial de hello toocomplete necesarios son las siguientes de Hello:</span><span class="sxs-lookup"><span data-stu-id="a1f90-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="a1f90-110">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f90-110">An Azure account.</span></span> <span data-ttu-id="a1f90-111">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1f90-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="a1f90-112">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="a1f90-112">A Media Services account.</span></span> <span data-ttu-id="a1f90-113">toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a1f90-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a1f90-114">Una cámara web.</span><span class="sxs-lookup"><span data-stu-id="a1f90-114">A webcam.</span></span> <span data-ttu-id="a1f90-115">Por ejemplo, el [codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="a1f90-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="a1f90-116">Se recomienda encarecidamente hello tooreview siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="a1f90-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="a1f90-117">Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="a1f90-118">Información general de streaming en vivo con Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="a1f90-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="a1f90-119">Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple</span><span class="sxs-lookup"><span data-stu-id="a1f90-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="a1f90-120"><a id="scenario"></a>Escenario común de streaming en vivo</span><span class="sxs-lookup"><span data-stu-id="a1f90-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="a1f90-121">Hello pasos siguientes describen las tareas implicadas en la creación de aplicaciones transmisión por secuencias en directo comunes que usan los canales que se configuran para la entrega de paso a través.</span><span class="sxs-lookup"><span data-stu-id="a1f90-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="a1f90-122">Este tutorial se muestra cómo toocreate y administrar un canal de acceso directo y eventos en directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="a1f90-123">Asegúrese de que esté Hola origen desde el que desea que el contenido de toostream Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="a1f90-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="a1f90-124">Conectar un equipo de tooa de cámara de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="a1f90-125">Inicie y configure un codificador en directo local que genere una transmisión de RTMP o MP4 fragmentado con velocidad de bits múltiple.</span><span class="sxs-lookup"><span data-stu-id="a1f90-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="a1f90-126">Para obtener más información, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="a1f90-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="a1f90-127">Este paso también puede realizarse después de crear el canal.</span><span class="sxs-lookup"><span data-stu-id="a1f90-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="a1f90-128">Cree e inicie un canal de paso a través.</span><span class="sxs-lookup"><span data-stu-id="a1f90-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="a1f90-129">URL de introducción de hello recuperar canales.</span><span class="sxs-lookup"><span data-stu-id="a1f90-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="a1f90-130">URL de introducción de Hola Hola codificador en directo toosend hello secuencia toohello canal utiliza.</span><span class="sxs-lookup"><span data-stu-id="a1f90-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="a1f90-131">Recuperar la dirección URL de vista previa de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="a1f90-132">Utilice este tooverify de dirección URL que el canal está recibiendo correctamente la secuencia en directo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="a1f90-133">Cree un evento o programa en directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="a1f90-134">Al usar hello portal de Azure, también crea un evento en directo crea un activo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="a1f90-135">Inicie Hola eventos/programa cuando esté listo toostart streaming y archivado.</span><span class="sxs-lookup"><span data-stu-id="a1f90-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="a1f90-136">Si lo desea, codificador en directo de hello puede ser señalado toostart un anuncio.</span><span class="sxs-lookup"><span data-stu-id="a1f90-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="a1f90-137">anuncio de Hola se inserta en el flujo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a1f90-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="a1f90-138">Detener Hola eventos/programa siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="a1f90-139">Eliminar eventos de Hola y programa (y opcionalmente eliminar recurso de hello).</span><span class="sxs-lookup"><span data-stu-id="a1f90-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="a1f90-140">Revise [de transmisión por secuencias en directo con codificadores locales que crean secuencias de velocidades de bits](media-services-live-streaming-with-onprem-encoders.md) toolearn sobre los conceptos y consideraciones relacionadas con streaming toolive con codificadores locales y los canales de acceso directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="a1f90-141">errores y las notificaciones de tooview</span><span class="sxs-lookup"><span data-stu-id="a1f90-141">tooview notifications and errors</span></span>
<span data-ttu-id="a1f90-142">Si desea que las notificaciones de tooview y los errores generados por hello portal de Azure, haga clic en el icono de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Notificaciones](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="a1f90-144">Creación e inicio de canales de paso a través y eventos</span><span class="sxs-lookup"><span data-stu-id="a1f90-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="a1f90-145">Un canal está asociado con programas y eventos que permiten la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="a1f90-146">Los canales administran los eventos.</span><span class="sxs-lookup"><span data-stu-id="a1f90-146">Channels manage events.</span></span> 

<span data-ttu-id="a1f90-147">Puede especificar Hola número de horas que quiere tooretain Hola registran contenido de programa Hola, establecer hello **ventana de archivo** longitud.</span><span class="sxs-lookup"><span data-stu-id="a1f90-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="a1f90-148">Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas.</span><span class="sxs-lookup"><span data-stu-id="a1f90-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="a1f90-149">Duración de la ventana de archivo también establece la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="a1f90-150">Se pueden ejecutar eventos sobre la cantidad de tiempo especificada de hello, pero continuamente se descarta el contenido que se encuentra detrás de la longitud de la ventana de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="a1f90-151">El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.</span><span class="sxs-lookup"><span data-stu-id="a1f90-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="a1f90-152">Cada evento está asociado a un recurso.</span><span class="sxs-lookup"><span data-stu-id="a1f90-152">Each event is associated with an asset.</span></span> <span data-ttu-id="a1f90-153">evento de hello toopublish, debe crear un localizador OnDemand para activo Hola asociado.</span><span class="sxs-lookup"><span data-stu-id="a1f90-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="a1f90-154">Este localizador permite toobuild una URL de streaming puede proporcionar a los clientes de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a1f90-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="a1f90-155">Un canal admite hasta toothree eventos en ejecución simultánea por lo que puede crear varios archivos de hello mismo flujo entrante.</span><span class="sxs-lookup"><span data-stu-id="a1f90-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="a1f90-156">Esto le permite toopublish y archivar diferentes partes de un evento según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a1f90-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="a1f90-157">Por ejemplo, sus necesidades de negocio es tooarchive 6 horas de un programa, pero toobroadcast solo últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a1f90-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="a1f90-158">tooaccomplish, necesita toocreate dos programas en ejecución simultáneos.</span><span class="sxs-lookup"><span data-stu-id="a1f90-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="a1f90-159">Un programa se establece tooarchive 6 horas de evento de hello pero no se publica el programa Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="a1f90-160">Hello otro programa es conjunto tooarchive durante 10 minutos y se publica este programa.</span><span class="sxs-lookup"><span data-stu-id="a1f90-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="a1f90-161">No debería reutilizar eventos en directo ya existentes.</span><span class="sxs-lookup"><span data-stu-id="a1f90-161">You should not reuse existing live events.</span></span> <span data-ttu-id="a1f90-162">En su lugar, cree e inicie un evento nuevo para cada evento.</span><span class="sxs-lookup"><span data-stu-id="a1f90-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="a1f90-163">Evento de hello cuando esté listo toostart streaming y archivado de inicio.</span><span class="sxs-lookup"><span data-stu-id="a1f90-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="a1f90-164">Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="a1f90-165">contenido toodelete archivado, detener y eliminar eventos de Hola y, a continuación, eliminar recurso asociado Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="a1f90-166">No se puede eliminar un recurso si se utiliza un evento; evento de Hello debe eliminarse en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="a1f90-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="a1f90-167">Incluso después de detener y eliminar un evento de hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="a1f90-168">Si desea hello tooretain archivado de contenido, pero no la tiene disponible para la transmisión por secuencias, eliminar Hola localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="a1f90-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="a1f90-169">toouse Hola portal toocreate un canal</span><span class="sxs-lookup"><span data-stu-id="a1f90-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="a1f90-170">Esta sección se muestra cómo hello toouse **creación rápida** opción toocreate un canal de acceso directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="a1f90-171">Para más información sobre este tipo de canales, consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="a1f90-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="a1f90-172">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f90-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a1f90-173">Hola **configuración** ventana, haga clic en **streaming en vivo**.</span><span class="sxs-lookup"><span data-stu-id="a1f90-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Introducción](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="a1f90-175">Hola **streaming en vivo** aparecerá la ventana.</span><span class="sxs-lookup"><span data-stu-id="a1f90-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="a1f90-176">Haga clic en **creación rápida** protocolo de introducción de toocreate un canal de acceso directo con hello RTMP.</span><span class="sxs-lookup"><span data-stu-id="a1f90-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="a1f90-177">Hola **crear un nuevo canal** aparecerá la ventana.</span><span class="sxs-lookup"><span data-stu-id="a1f90-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="a1f90-178">Asigne un nombre de canal nuevo de Hola y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="a1f90-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="a1f90-179">Esto crea un canal de acceso directo con hello protocolo de introducción RTMP.</span><span class="sxs-lookup"><span data-stu-id="a1f90-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="a1f90-180">Creación de eventos</span><span class="sxs-lookup"><span data-stu-id="a1f90-180">Create events</span></span>
1. <span data-ttu-id="a1f90-181">Seleccione un toowhich de canal que desee tooadd un evento.</span><span class="sxs-lookup"><span data-stu-id="a1f90-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="a1f90-182">Pulse el botón **Evento en directo** .</span><span class="sxs-lookup"><span data-stu-id="a1f90-182">Press **Live Event** button.</span></span>

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="a1f90-184">Obtención de direcciones URL de introducción</span><span class="sxs-lookup"><span data-stu-id="a1f90-184">Get ingest URLs</span></span>
<span data-ttu-id="a1f90-185">Una vez creado el canal de hello, puede obtener direcciones URL que proporcionará toohello de codificador en directo de entrada.</span><span class="sxs-lookup"><span data-stu-id="a1f90-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="a1f90-186">Codificador de Hello usa estos tooinput de direcciones URL de una secuencia en directo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Creado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="a1f90-188">Evento de Hola de inspección</span><span class="sxs-lookup"><span data-stu-id="a1f90-188">Watch hello event</span></span>
<span data-ttu-id="a1f90-189">evento de hello toowatch, haga clic en **inspección** en hello Azure Hola portal o copiar dirección URL de streaming y utilizar un Reproductor de su elección.</span><span class="sxs-lookup"><span data-stu-id="a1f90-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Creado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="a1f90-191">Evento en directo obtienen automáticamente contenido de tooon convertido a petición cuando se detuvo.</span><span class="sxs-lookup"><span data-stu-id="a1f90-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a1f90-192">Limpieza</span><span class="sxs-lookup"><span data-stu-id="a1f90-192">Clean up</span></span>
<span data-ttu-id="a1f90-193">Para más información sobre este tipo de canales, consulte [Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="a1f90-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="a1f90-194">Un canal se puede detener cuando se hayan detenido todos los programas y eventos en el canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="a1f90-195">Una vez que se detiene el canal de hello, no incurrirás en gastos.</span><span class="sxs-lookup"><span data-stu-id="a1f90-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="a1f90-196">Cuando necesite toostart nuevo, lo tendrá hello misma URL de introducción por lo que no necesita tooreconfigure su codificador.</span><span class="sxs-lookup"><span data-stu-id="a1f90-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="a1f90-197">Un canal puede eliminarse solo si se han eliminado todos los eventos en directo en el canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="a1f90-198">Visualización del contenido archivado</span><span class="sxs-lookup"><span data-stu-id="a1f90-198">View archived content</span></span>
<span data-ttu-id="a1f90-199">Incluso después de detener y eliminar un evento de hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f90-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="a1f90-200">No se puede eliminar un recurso si se utiliza un evento; evento de Hello debe eliminarse en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="a1f90-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="a1f90-201">Seleccionar de los activos de toomanage **configuración** y haga clic en **activos**.</span><span class="sxs-lookup"><span data-stu-id="a1f90-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Recursos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="a1f90-203">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="a1f90-203">Next step</span></span>
<span data-ttu-id="a1f90-204">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a1f90-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a1f90-205">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a1f90-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

