---
title: "Inserción de un vídeo de streaming adaptable MPEG-DASH en una aplicación HTML5 con DASH.js | Microsoft Docs"
description: "En este vídeo se muestra cómo incluir un vídeo de streaming adaptable MPEG-DASH en una aplicación HTML5 con DASH.js."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="620a5-103">Incrustación de un vídeo de transmisión por secuencias adaptativa MPEG-DASH en una aplicación HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="620a5-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="620a5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="620a5-104">Overview</span></span>
<span data-ttu-id="620a5-105">MPEG-DASH es una norma ISO para la transmisión por secuencias adaptativa de contenido de vídeo, lo que ofrece ventajas significativas para aquellos que desean ofrecer salida de streaming de vídeo adaptable de alta calidad.</span><span class="sxs-lookup"><span data-stu-id="620a5-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="620a5-106">Con MPEG-DASH, la secuencia de vídeo se baja automáticamente a una definición inferior cuando la red está saturada.</span><span class="sxs-lookup"><span data-stu-id="620a5-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="620a5-107">Esto reduce la probabilidad de que el usuario vea un vídeo "pausado" mientras el reproductor descarga los siguientes segundos para reproducirlos (también conocido como almacenamiento en búfer).</span><span class="sxs-lookup"><span data-stu-id="620a5-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="620a5-108">A medida que se reduce la congestión de la red, el reproductor de vídeo a su vez volverá a una secuencia de mayor calidad.</span><span class="sxs-lookup"><span data-stu-id="620a5-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="620a5-109">Esta capacidad para adaptar el ancho de banda necesario también produce una hora de inicio más rápida para el vídeo.</span><span class="sxs-lookup"><span data-stu-id="620a5-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="620a5-110">Esto significa que los primeros segundos se pueden reproducir en un segmento de calidad inferior rápido para descargar y luego pasan a una calidad superior una vez se ha almacenado en búfer el contenido suficiente.</span><span class="sxs-lookup"><span data-stu-id="620a5-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="620a5-111">Dash.js es un reproductor de vídeo MPEG-DASH de código abierto escrito en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="620a5-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="620a5-112">Su objetivo es proporcionar un reproductor sólido entre plataformas que se pueda reutilizar libremente en aplicaciones que requieren reproducción de vídeo.</span><span class="sxs-lookup"><span data-stu-id="620a5-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="620a5-113">Ofrece reproducción MPEG-DASH en cualquier explorador que admite las extensiones de origen multimedia (MSE) W3C hoy en día, es decir, Chrome, Microsoft Edge e IE11 (otros exploradores han indicado su intención de ser compatibles con MSE).</span><span class="sxs-lookup"><span data-stu-id="620a5-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="620a5-114">Para obtener más información sobre DASH.js, vea el repositorio de GitHub dash.js.</span><span class="sxs-lookup"><span data-stu-id="620a5-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="620a5-115">Creación de un reproductor de vídeo de streaming basado en explorador</span><span class="sxs-lookup"><span data-stu-id="620a5-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="620a5-116">Para crear una página web sencilla que muestre un reproductor de vídeo con los controles esperados como reproducir, pausa, rebobinar, etc., necesitará:</span><span class="sxs-lookup"><span data-stu-id="620a5-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="620a5-117">Crear una página HTML</span><span class="sxs-lookup"><span data-stu-id="620a5-117">Create an HTML page</span></span>
2. <span data-ttu-id="620a5-118">Agregar la etiqueta de vídeo</span><span class="sxs-lookup"><span data-stu-id="620a5-118">Add the video tag</span></span>
3. <span data-ttu-id="620a5-119">Agregar el reproductor dash.js</span><span class="sxs-lookup"><span data-stu-id="620a5-119">Add the dash.js player</span></span>
4. <span data-ttu-id="620a5-120">Inicializar el reproductor</span><span class="sxs-lookup"><span data-stu-id="620a5-120">Initialize the player</span></span>
5. <span data-ttu-id="620a5-121">Agregar algún estilo CSS</span><span class="sxs-lookup"><span data-stu-id="620a5-121">Add some CSS style</span></span>
6. <span data-ttu-id="620a5-122">Ver los resultados en un explorador que implemente MSE</span><span class="sxs-lookup"><span data-stu-id="620a5-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="620a5-123">La inicialización del reproductor se puede completar con tan solo unas líneas de código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="620a5-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="620a5-124">Con dash.js, es realmente así de sencillo incrustar vídeo MPEG-DASH en sus aplicaciones basadas en explorador.</span><span class="sxs-lookup"><span data-stu-id="620a5-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="620a5-125">Creación de la página HTML</span><span class="sxs-lookup"><span data-stu-id="620a5-125">Creating the HTML Page</span></span>
<span data-ttu-id="620a5-126">El primer paso es crear una página HTML estándar con el elemento de **vídeo**, guardar este archivo como basicPlayer.html, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="620a5-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="620a5-127">Adición del reproductor dash.js</span><span class="sxs-lookup"><span data-stu-id="620a5-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="620a5-128">Para agregar la implementación de referencia de dash.js a la aplicación, deberá incluir el archivo dash.all.js desde la 1.0 versión del proyecto dash.js.</span><span class="sxs-lookup"><span data-stu-id="620a5-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="620a5-129">Este se debe guardar en la carpeta de JavaScript de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="620a5-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="620a5-130">Este archivo es un archivo de conveniencia que reúne todo el código de dash.js necesario en un solo archivo.</span><span class="sxs-lookup"><span data-stu-id="620a5-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="620a5-131">Si echa un vistazo al repositorio dash.js, observará los archivos individuales, probará código y mucho más, pero si todo lo que quiere hacer es usar dash.js, el archivo dash.all.js es lo que necesita.</span><span class="sxs-lookup"><span data-stu-id="620a5-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="620a5-132">Para agregar el reproductor de dash.js a sus aplicaciones, agregue una etiqueta de script a la sección de encabezado del archivo basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="620a5-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="620a5-133">A continuación, cree una función para inicializar el reproductor cuando se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="620a5-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="620a5-134">Agregue el siguiente script después de la línea en la que carga dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="620a5-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="620a5-135">Esta función crea primero un elemento DashContext.</span><span class="sxs-lookup"><span data-stu-id="620a5-135">This function first creates a DashContext.</span></span> <span data-ttu-id="620a5-136">Se usa para configurar la aplicación para un entorno de tiempo de ejecución específico.</span><span class="sxs-lookup"><span data-stu-id="620a5-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="620a5-137">Desde un punto de vista técnico, define las clases que debería usar el marco de inserción de dependencias al construir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="620a5-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="620a5-138">En la mayoría de los casos, usará Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="620a5-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="620a5-139">A continuación, cree una instancia de la clase principal del marco de dash.js, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="620a5-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="620a5-140">Esta clase contiene los métodos principales necesarios, como reproducción y pausa, administra la relación con el elemento de vídeo y también la interpretación del archivo de descripción de presentación multimedia (MPD) que describe el vídeo que se va a reproducir.</span><span class="sxs-lookup"><span data-stu-id="620a5-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="620a5-141">Se llama a la función startup() de la clase MediaPlayer para asegurarse de que el reproductor está listo para reproducir vídeo.</span><span class="sxs-lookup"><span data-stu-id="620a5-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="620a5-142">Entre otras cuestiones, esta función garantiza que se han cargado todas las clases necesarias (según se definen por el contexto).</span><span class="sxs-lookup"><span data-stu-id="620a5-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="620a5-143">Cuando el reproductor esté listo, puede asociar el elemento de vídeo mediante la función attachView().</span><span class="sxs-lookup"><span data-stu-id="620a5-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="620a5-144">Esto permite al MediaPlayer insertar la secuencia de vídeo en el elemento y controlar además la reproducción de controles según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="620a5-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="620a5-145">Pase la URL del archivo MPD al MediaPlayer para que sepa cuál el vídeo que se espera reproducir. La función setupVideo() recién creada deberá ejecutarse una vez que la página se haya cargado por completo.</span><span class="sxs-lookup"><span data-stu-id="620a5-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="620a5-146">Haga esto mediante el evento onload del elemento body.</span><span class="sxs-lookup"><span data-stu-id="620a5-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="620a5-147">Cambie el elemento <body> a:</span><span class="sxs-lookup"><span data-stu-id="620a5-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="620a5-148">Por último, establezca el tamaño del elemento de vídeo mediante CSS.</span><span class="sxs-lookup"><span data-stu-id="620a5-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="620a5-149">En un entorno de streaming adaptable, esto es especialmente importante porque el tamaño del vídeo que se reproduce puede cambiar a medida que la reproducción se adapta a las condiciones de red cambiantes.</span><span class="sxs-lookup"><span data-stu-id="620a5-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="620a5-150">En esta sencilla demo simplemente debe forzar el elemento de vídeo para que sea el 80 % de la ventana del explorador disponible agregando el CSS siguiente a la sección inicial de la página:</span><span class="sxs-lookup"><span data-stu-id="620a5-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="620a5-151">Reproducción de un vídeo</span><span class="sxs-lookup"><span data-stu-id="620a5-151">Playing a Video</span></span>
<span data-ttu-id="620a5-152">Para reproducir un vídeo, dirija el explorador al archivo basicPlayback.html y haga clic en Reproducir en el reproductor de vídeo que se muestra.</span><span class="sxs-lookup"><span data-stu-id="620a5-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="620a5-153">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="620a5-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="620a5-154">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="620a5-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="620a5-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="620a5-155">See Also</span></span>
[<span data-ttu-id="620a5-156">Desarrollo de aplicaciones para reproductor de vídeo</span><span class="sxs-lookup"><span data-stu-id="620a5-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="620a5-157">Repositorio dash.js de GitHub</span><span class="sxs-lookup"><span data-stu-id="620a5-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

