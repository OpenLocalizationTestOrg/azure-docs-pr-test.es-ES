---
title: "aaaRedact caras con el tutorial de análisis de multimedia de Azure | Documentos de Microsoft"
description: "En este tema se muestra instrucciones paso a paso acerca de cómo toorun un flujo de trabajo de redacción completa mediante el Explorador de servicios multimedia de Azure (AMSE) y Azure Media Redactor visualizador (herramienta de código abierto)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="7959e-103">Tutorial de censura de rostros con Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="7959e-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="7959e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7959e-104">Overview</span></span>

<span data-ttu-id="7959e-105">**Redactor de Azure Media** es un [análisis de multimedia de Azure](media-services-analytics-overview.md) procesador multimedia (MP) que ofrece la redacción de cara escalable en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="7959e-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="7959e-106">Redacción de cara permite toomodify el vídeo en caras de tooblur de orden de los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="7959e-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="7959e-107">Puede desear toouse Hola el servicio de redacción de cara en escenarios de seguridad y medios de noticias públicos.</span><span class="sxs-lookup"><span data-stu-id="7959e-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="7959e-108">Unos pocos minutos después de material de archivo que contiene varios tipos pueden tardar horas tooredact manualmente, pero con esta imagen de hello servicio proceso de redacción requiere unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="7959e-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="7959e-109">Para más información, consulte [este blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="7959e-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="7959e-110">Para obtener más información acerca de **Redactor de multimedia de Azure**, vea hello [información general de redacción de cara](media-services-face-redaction.md) tema.</span><span class="sxs-lookup"><span data-stu-id="7959e-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="7959e-111">En este tema se muestra instrucciones paso a paso acerca de cómo toorun un flujo de trabajo de redacción completa mediante el Explorador de servicios multimedia de Azure (AMSE) y Azure Media Redactor visualizador (herramienta de código abierto).</span><span class="sxs-lookup"><span data-stu-id="7959e-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="7959e-112">Hola **Redactor de multimedia de Azure** MP está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="7959e-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="7959e-113">Está disponible en todas las regiones de Azure públicas, así como en los centros de datos de China y el gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="7959e-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="7959e-114">Actualmente, esta versión preliminar es gratuita.</span><span class="sxs-lookup"><span data-stu-id="7959e-114">This preview is currently free of charge.</span></span> <span data-ttu-id="7959e-115">En la versión actual de hello, hay un límite de 10 minutos en la duración del vídeo procesado.</span><span class="sxs-lookup"><span data-stu-id="7959e-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="7959e-116">Para más información, consulte [este blog](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) .</span><span class="sxs-lookup"><span data-stu-id="7959e-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="7959e-117">Flujo de trabajo del Explorador de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="7959e-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="7959e-118">Hello tooget de manera más fácil trabajar con Redactor es la herramienta de AMSE de código abierto toouse hello en github.</span><span class="sxs-lookup"><span data-stu-id="7959e-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="7959e-119">Puede ejecutar un flujo de trabajo simplificado a través de **combinan** modo si no necesita acceso toohello anotación json o hello cara imágenes jpg.</span><span class="sxs-lookup"><span data-stu-id="7959e-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="7959e-120">Descarga e instalación</span><span class="sxs-lookup"><span data-stu-id="7959e-120">Download and setup</span></span>

1. <span data-ttu-id="7959e-121">Herramienta de AMSE Hola descargar [aquí](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="7959e-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="7959e-122">Inicie sesión en tooyour cuenta de servicios multimedia mediante la clave del servicio.</span><span class="sxs-lookup"><span data-stu-id="7959e-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="7959e-123">tooobtain Hola nombre de cuenta y la información de clave, vaya toohello [portal de Azure](https://portal.azure.com/) y seleccione su cuenta de AMS.</span><span class="sxs-lookup"><span data-stu-id="7959e-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="7959e-124">A continuación, seleccione Configuración > Claves.</span><span class="sxs-lookup"><span data-stu-id="7959e-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="7959e-125">ventanas de Hello administrar claves muestra el nombre de la cuenta de hello y claves primarias y secundarias de Hola se muestra.</span><span class="sxs-lookup"><span data-stu-id="7959e-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="7959e-126">Copiar valores de nombre de la cuenta de Hola y Hola primary key.</span><span class="sxs-lookup"><span data-stu-id="7959e-126">Copy values of hello account name and hello primary key.</span></span>

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="7959e-128">Primer paso: Modo Analizar</span><span class="sxs-lookup"><span data-stu-id="7959e-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="7959e-129">Cargue el archivo multimedia a través de Activo – > Cargar, o bien arrástrelo y suéltelo.</span><span class="sxs-lookup"><span data-stu-id="7959e-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="7959e-130">Haga clic en el botón derecho y procese el archivo multimedia utilizando Análisis multimedia > Azure Media Redactor – > Modo Analizar.</span><span class="sxs-lookup"><span data-stu-id="7959e-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="7959e-133">salida de Hello incluirá un archivo json de anotaciones con datos de ubicación de fuente, así como un jpg de cada tipo detectado.</span><span class="sxs-lookup"><span data-stu-id="7959e-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="7959e-135">Segundo paso: Modo Redact (Censurar)</span><span class="sxs-lookup"><span data-stu-id="7959e-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="7959e-136">Cargue su toohello de recurso de vídeo original de salida desde la primera pasada de Hola y establecer como un recurso principal.</span><span class="sxs-lookup"><span data-stu-id="7959e-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="7959e-138">(Opcional) Cargar un archivo de 'Dance_idlist.txt' que incluye una lista de nueva línea delimitada de identificadores que se va tooredact hello.</span><span class="sxs-lookup"><span data-stu-id="7959e-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="7959e-140">(Opcional) Asegúrese de cualquier archivo de annotations.json toohello modificaciones, tal como aumentar Hola límites del cuadro de límite.</span><span class="sxs-lookup"><span data-stu-id="7959e-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="7959e-141">Haga clic Hola activo de salida desde la primera pasada de hello, seleccionar Hola Redactor y ejecutar con hello **Redact** modo.</span><span class="sxs-lookup"><span data-stu-id="7959e-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="7959e-143">Para descargar o compartirlos Hola salida redactado final activo.</span><span class="sxs-lookup"><span data-stu-id="7959e-143">Download or share hello final redacted output asset.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="7959e-145">Herramienta de código abierto Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="7959e-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="7959e-146">Un código abierto [herramienta visualizador](https://github.com/Microsoft/azure-media-redactor-visualizer) es toohelp diseñada a los desarrolladores iniciándose con formato de anotaciones de hello con salida de hello y análisis.</span><span class="sxs-lookup"><span data-stu-id="7959e-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="7959e-147">Después de clonar el repositorio de hello, en el proyecto de orden toorun hello, necesitará toodownload FFMPEG desde su [sitio oficial](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="7959e-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="7959e-148">Si es un desarrollador que trate de hello tooparse dato de anotación de JSON, buscar dentro de Models.MetaData para obtener ejemplos de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7959e-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="7959e-149">Configurar la herramienta de Hola</span><span class="sxs-lookup"><span data-stu-id="7959e-149">Set up hello tool</span></span>

1.  <span data-ttu-id="7959e-150">Descargue y generar solución completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="7959e-150">Download and build hello entire solution.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="7959e-152">Descargue FFMPEG desde [aquí](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="7959e-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="7959e-153">Este proyecto se desarrolló originalmente mediante la versión be1d324 (2016-10-04) con vinculación estática.</span><span class="sxs-lookup"><span data-stu-id="7959e-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="7959e-154">Copie ffmpeg.exe y ffprobe.exe toohello misma carpeta de salida como AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="7959e-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="7959e-156">Ejecute AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="7959e-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="7959e-157">Usar la herramienta Hola</span><span class="sxs-lookup"><span data-stu-id="7959e-157">Use hello tool</span></span>

1. <span data-ttu-id="7959e-158">Procesar sus vídeos en su cuenta de servicios multimedia de Azure con hello Redactor MP en modo de analizar.</span><span class="sxs-lookup"><span data-stu-id="7959e-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="7959e-159">Descargar archivo de vídeo original de Hola y de salida de hello de redacción de hello: analizar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="7959e-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="7959e-160">Ejecutar la aplicación del visualizador de hello y elija archivos Hola anteriores.</span><span class="sxs-lookup"><span data-stu-id="7959e-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="7959e-162">Obtenga una vista previa del archivo.</span><span class="sxs-lookup"><span data-stu-id="7959e-162">Preview your file.</span></span> <span data-ttu-id="7959e-163">Seleccione cara le gustaría tooblur a través de la barra lateral de hello en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="7959e-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="7959e-165">campo de texto de Hello inferior se actualizará con la cara Hola identificadores.</span><span class="sxs-lookup"><span data-stu-id="7959e-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="7959e-166">Cree un archivo denominado "idlist.txt" con estos identificadores como una lista delimitada de nueva línea.</span><span class="sxs-lookup"><span data-stu-id="7959e-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="7959e-167">Hola idlist.txt debe guardarse en ANSI.</span><span class="sxs-lookup"><span data-stu-id="7959e-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="7959e-168">Puede utilizar el Bloc de notas toosave en ANSI.</span><span class="sxs-lookup"><span data-stu-id="7959e-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="7959e-169">Cargar este recurso de salida de archivo toohello del paso 1.</span><span class="sxs-lookup"><span data-stu-id="7959e-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="7959e-170">Cargar activo original de vídeo toothis Hola así y establecer como elemento principal.</span><span class="sxs-lookup"><span data-stu-id="7959e-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="7959e-171">Ejecutar trabajo de redacción de este recurso con "Redact" modo tooget Hola redactado vídeo final.</span><span class="sxs-lookup"><span data-stu-id="7959e-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7959e-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7959e-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7959e-173">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="7959e-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="7959e-174">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="7959e-174">Related links</span></span>
[<span data-ttu-id="7959e-175">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="7959e-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="7959e-176">Demostraciones de Análisis multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="7959e-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="7959e-177">Anuncio de función de censura facial para Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="7959e-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
