---
title: Tutorial de censura de rostros con Azure Media Analytics | Microsoft Docs
description: "En este tema se muestran instrucciones paso a paso sobre cómo ejecutar un flujo de trabajo de censura completa mediante el Explorador de Azure Media Services (AMSE) y Azure Media Redactor Visualizer (herramienta de código abierto)."
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
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="ed89b-103">Tutorial de censura de rostros con Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="ed89b-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="ed89b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ed89b-104">Overview</span></span>

<span data-ttu-id="ed89b-105">**Redactor multimedia de Azure** es un procesador multimedia (MP) de [Análisis multimedia de Azure](media-services-analytics-overview.md) que ofrece censura de rostros escalable en la nube.</span><span class="sxs-lookup"><span data-stu-id="ed89b-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="ed89b-106">La censura de rostros le permite modificar un vídeo con el fin de difuminar las caras de personas seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="ed89b-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="ed89b-107">Puede usar el servicio de censura de rostros en escenarios de seguridad pública y de noticias en los medios de comunicación.</span><span class="sxs-lookup"><span data-stu-id="ed89b-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="ed89b-108">Unos minutos de material de archivo que contenga varias caras puede tardar horas en censurarse manualmente, pero con este servicio, el proceso de censura de caras requiere solamente unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="ed89b-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="ed89b-109">Para más información, consulte [este blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="ed89b-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="ed89b-110">Para obtener más información sobre **Azure Media Redactor**, consulte el tema de [información general sobre Censura de rostros](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="ed89b-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="ed89b-111">En este tema se muestran instrucciones paso a paso sobre cómo ejecutar un flujo de trabajo de censura completa mediante el Explorador de Azure Media Services (AMSE) y Azure Media Redactor Visualizer (herramienta de código abierto).</span><span class="sxs-lookup"><span data-stu-id="ed89b-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="ed89b-112">El procesador de multimedia **Redactor multimedia de Azure** está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="ed89b-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="ed89b-113">Está disponible en todas las regiones de Azure públicas, así como en los centros de datos de China y el gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="ed89b-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="ed89b-114">Actualmente, esta versión preliminar es gratuita.</span><span class="sxs-lookup"><span data-stu-id="ed89b-114">This preview is currently free of charge.</span></span> <span data-ttu-id="ed89b-115">En la versión actual, hay un límite de 10 minutos en la duración del vídeo procesado.</span><span class="sxs-lookup"><span data-stu-id="ed89b-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="ed89b-116">Para más información, consulte [este blog](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) .</span><span class="sxs-lookup"><span data-stu-id="ed89b-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="ed89b-117">Flujo de trabajo del Explorador de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="ed89b-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="ed89b-118">La manera más fácil de empezar a trabajar con Censura de rostros es usar la herramienta AMSE de código abierto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ed89b-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="ed89b-119">Puede ejecutar un flujo de trabajo simplificado a través del modo **combinado** si no necesita acceso al JSON de anotaciones o a las imágenes JPG de rostros.</span><span class="sxs-lookup"><span data-stu-id="ed89b-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="ed89b-120">Descarga e instalación</span><span class="sxs-lookup"><span data-stu-id="ed89b-120">Download and setup</span></span>

1. <span data-ttu-id="ed89b-121">Descargue la herramienta AMSE [aquí](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="ed89b-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="ed89b-122">Inicie sesión en su cuenta de Media Services mediante la clave del servicio.</span><span class="sxs-lookup"><span data-stu-id="ed89b-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="ed89b-123">Para obtener el nombre de la cuenta y la información de la clave, vaya a [Azure Portal](https://portal.azure.com/) y seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="ed89b-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="ed89b-124">A continuación, seleccione Configuración > Claves.</span><span class="sxs-lookup"><span data-stu-id="ed89b-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="ed89b-125">Aparece la ventana Administrar claves que muestra el nombre de la cuenta y la clave principal y la secundaria.</span><span class="sxs-lookup"><span data-stu-id="ed89b-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="ed89b-126">Copie los valores del nombre de la cuenta y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="ed89b-126">Copy values of the account name and the primary key.</span></span>

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="ed89b-128">Primer paso: Modo Analizar</span><span class="sxs-lookup"><span data-stu-id="ed89b-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="ed89b-129">Cargue el archivo multimedia a través de Activo – > Cargar, o bien arrástrelo y suéltelo.</span><span class="sxs-lookup"><span data-stu-id="ed89b-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="ed89b-130">Haga clic en el botón derecho y procese el archivo multimedia utilizando Análisis multimedia > Azure Media Redactor – > Modo Analizar.</span><span class="sxs-lookup"><span data-stu-id="ed89b-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="ed89b-133">El resultado incluirá un archivo JSON de anotaciones con datos de ubicación de rostros, así como un JPG de cada rostro detectado.</span><span class="sxs-lookup"><span data-stu-id="ed89b-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="ed89b-135">Segundo paso: Modo Redact (Censurar)</span><span class="sxs-lookup"><span data-stu-id="ed89b-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="ed89b-136">Cargue el recurso de vídeo original en la salida del primer paso y establézcalo como un recurso principal.</span><span class="sxs-lookup"><span data-stu-id="ed89b-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="ed89b-138">Opcional: cargue un archivo Dance_idlist.txt que incluya una lista delimitada de nueva línea de los identificadores que se van a censurar.</span><span class="sxs-lookup"><span data-stu-id="ed89b-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="ed89b-140">Opcional: realice las modificaciones en el archivo annotations.json, por ejemplo, aumentar los límites del cuadro de límite.</span><span class="sxs-lookup"><span data-stu-id="ed89b-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="ed89b-141">Haga clic con el botón derecho en el recurso de salida del primer paso, seleccione Redactor y ejecútelo con el modo **Redact** (Censurar).</span><span class="sxs-lookup"><span data-stu-id="ed89b-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="ed89b-143">Descargue o comparta el recurso de salida censurado final.</span><span class="sxs-lookup"><span data-stu-id="ed89b-143">Download or share the final redacted output asset.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="ed89b-145">Herramienta de código abierto Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="ed89b-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="ed89b-146">La [herramienta de visualización](https://github.com/Microsoft/azure-media-redactor-visualizer) de código abierto está diseñada para ayudar a los desarrolladores a iniciarse en el formato de anotaciones analizando y utilizando la salida.</span><span class="sxs-lookup"><span data-stu-id="ed89b-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="ed89b-147">Después de clonar el repositorio, con el fin de ejecutar el proyecto, necesitará descargar FFMPEG desde el [sitio oficial](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ed89b-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="ed89b-148">Si como desarrollador trata de analizar los datos de anotaciones del JSON, busque dentro de Models.MetaData ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="ed89b-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="ed89b-149">Configuración de la herramienta</span><span class="sxs-lookup"><span data-stu-id="ed89b-149">Set up the tool</span></span>

1.  <span data-ttu-id="ed89b-150">Descargue y genere la solución completa.</span><span class="sxs-lookup"><span data-stu-id="ed89b-150">Download and build the entire solution.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="ed89b-152">Descargue FFMPEG desde [aquí](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ed89b-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="ed89b-153">Este proyecto se desarrolló originalmente mediante la versión be1d324 (2016-10-04) con vinculación estática.</span><span class="sxs-lookup"><span data-stu-id="ed89b-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="ed89b-154">Copie ffmpeg.exe y ffprobe.exe en la misma carpeta de salida que AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="ed89b-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="ed89b-156">Ejecute AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="ed89b-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="ed89b-157">Uso de la herramienta</span><span class="sxs-lookup"><span data-stu-id="ed89b-157">Use the tool</span></span>

1. <span data-ttu-id="ed89b-158">Procese sus vídeos en su cuenta de Azure Media Services con el módulo de administración de Redactor en Modo Analizar.</span><span class="sxs-lookup"><span data-stu-id="ed89b-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="ed89b-159">Descargue el archivo de vídeo original y la salida de Redaction (Censura) - trabajo Analizar.</span><span class="sxs-lookup"><span data-stu-id="ed89b-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="ed89b-160">Ejecute la aplicación de visualización y elija los archivos anteriores.</span><span class="sxs-lookup"><span data-stu-id="ed89b-160">Run the visualizer application and choose the files above.</span></span> 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="ed89b-162">Obtenga una vista previa del archivo.</span><span class="sxs-lookup"><span data-stu-id="ed89b-162">Preview your file.</span></span> <span data-ttu-id="ed89b-163">Seleccione qué rostros le gustaría desenfocar a través de la barra lateral de la derecha.</span><span class="sxs-lookup"><span data-stu-id="ed89b-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="ed89b-165">El campo de texto de la parte inferior se actualizará con los identificadores de los rostros.</span><span class="sxs-lookup"><span data-stu-id="ed89b-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="ed89b-166">Cree un archivo denominado "idlist.txt" con estos identificadores como una lista delimitada de nueva línea.</span><span class="sxs-lookup"><span data-stu-id="ed89b-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="ed89b-167">El archivo idlist.txt debe guardarse en ANSI.</span><span class="sxs-lookup"><span data-stu-id="ed89b-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="ed89b-168">Puede usar el Bloc de notas para guardarlo en tal codificación.</span><span class="sxs-lookup"><span data-stu-id="ed89b-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="ed89b-169">Cargue el archivo en el recurso de salida del paso 1.</span><span class="sxs-lookup"><span data-stu-id="ed89b-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="ed89b-170">Cargue el vídeo original en este recurso y establézcalo como recurso principal.</span><span class="sxs-lookup"><span data-stu-id="ed89b-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="ed89b-171">Ejecute el trabajo Redaction (Censura) de este recurso con el modo "Redact" (Censurar) para obtener el vídeo censurado final.</span><span class="sxs-lookup"><span data-stu-id="ed89b-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ed89b-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed89b-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ed89b-173">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="ed89b-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="ed89b-174">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="ed89b-174">Related links</span></span>
[<span data-ttu-id="ed89b-175">Azure Media Services Analytics Overview (Información general sobre Azure Media Services Analytics)</span><span class="sxs-lookup"><span data-stu-id="ed89b-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="ed89b-176">Demostraciones de Análisis multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="ed89b-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="ed89b-177">Anuncio de función de censura facial para Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="ed89b-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
