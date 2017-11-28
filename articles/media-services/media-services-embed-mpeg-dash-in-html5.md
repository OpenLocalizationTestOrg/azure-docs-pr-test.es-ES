---
title: "aaaEmbedding un vídeo de transmisión por secuencias adaptativa de MPEG-DASH en una aplicación HTML5 con DASH.js | Documentos de Microsoft"
description: "Este tema se muestra cómo tooembed un vídeo de transmisión por secuencias adaptativa de MPEG-DASH en una aplicación HTML5 con DASH.js."
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
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="6a95e-103">Incrustación de un vídeo de transmisión por secuencias adaptativa MPEG-DASH en una aplicación HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="6a95e-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="6a95e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="6a95e-104">Overview</span></span>
<span data-ttu-id="6a95e-105">MPEG-DASH es un estándar ISO para hello adaptable de transmisión por secuencias de contenido de vídeo, lo que ofrece ventajas significativas para quienes desea vídeo de alta calidad, adaptable toodeliver salida de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="6a95e-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="6a95e-106">Con MPEG-DASH, secuencia de vídeo de hello quitará automáticamente definición inferior tooa cuando se satura red Hola.</span><span class="sxs-lookup"><span data-stu-id="6a95e-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="6a95e-107">Esto reduce la probabilidad de Hola de Visor de hello ver un vídeo "en pausa" mientras hello, el Reproductor descarga Hola a continuación algunos tooplay segundos (también conocido como almacenamiento en búfer).</span><span class="sxs-lookup"><span data-stu-id="6a95e-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="6a95e-108">Reduce la congestión de la red, Reproductor de vídeo de Hola a su vez devolverá tooa flujo de calidad superior.</span><span class="sxs-lookup"><span data-stu-id="6a95e-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="6a95e-109">Este ancho de banda Hola del tooadapt de capacidad necesario también se produce en una hora de inicio más rápida de vídeo.</span><span class="sxs-lookup"><span data-stu-id="6a95e-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="6a95e-110">Que significa que los primeros segundos de Hola puede reproducirse en un segmento de calidad inferior fast para descargar y, a continuación, el paso de calidad superior tooa una vez que se han almacenado en búfer suficiente contenido.</span><span class="sxs-lookup"><span data-stu-id="6a95e-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="6a95e-111">Dash.js es un reproductor de vídeo MPEG-DASH de código abierto escrito en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6a95e-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="6a95e-112">Su objetivo es tooprovide un reproductor sólido entre plataformas que se pueda reutilizar libremente en aplicaciones que requieren la reproducción de vídeo.</span><span class="sxs-lookup"><span data-stu-id="6a95e-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="6a95e-113">Proporciona reproducción MPEG-DASH en cualquier explorador que admita Hola W3C Media Source Extensions (MSE), hoy en día es Chrome, Microsoft Edge e IE11 (otros exploradores han indicado su intención toosupport MSE).</span><span class="sxs-lookup"><span data-stu-id="6a95e-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="6a95e-114">Para obtener más información acerca de DASH.js, js vea repositorio dash.js de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a95e-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="6a95e-115">Creación de un reproductor de vídeo de streaming basado en explorador</span><span class="sxs-lookup"><span data-stu-id="6a95e-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="6a95e-116">toocreate una página web sencilla que muestra un Reproductor de vídeo Hola espera que controla este tipo reproducir, pausa, rebobinar etc., deberá:</span><span class="sxs-lookup"><span data-stu-id="6a95e-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="6a95e-117">Crear una página HTML</span><span class="sxs-lookup"><span data-stu-id="6a95e-117">Create an HTML page</span></span>
2. <span data-ttu-id="6a95e-118">Agregar la etiqueta de vídeo de Hola</span><span class="sxs-lookup"><span data-stu-id="6a95e-118">Add hello video tag</span></span>
3. <span data-ttu-id="6a95e-119">Agregar hello dash.js jugador</span><span class="sxs-lookup"><span data-stu-id="6a95e-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="6a95e-120">Inicializar Reproductor Hola</span><span class="sxs-lookup"><span data-stu-id="6a95e-120">Initialize hello player</span></span>
5. <span data-ttu-id="6a95e-121">Agregar algún estilo CSS</span><span class="sxs-lookup"><span data-stu-id="6a95e-121">Add some CSS style</span></span>
6. <span data-ttu-id="6a95e-122">Ver los resultados en un explorador que implementa MSE Hola</span><span class="sxs-lookup"><span data-stu-id="6a95e-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="6a95e-123">Al inicializar el Reproductor Hola se puede completar en unos pocos de las líneas de código de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6a95e-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="6a95e-124">Con dash.js, realmente es que vídeo tooembed simple MPEG-DASH en las aplicaciones basadas en explorador.</span><span class="sxs-lookup"><span data-stu-id="6a95e-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="6a95e-125">Creación de hello página HTML</span><span class="sxs-lookup"><span data-stu-id="6a95e-125">Creating hello HTML Page</span></span>
<span data-ttu-id="6a95e-126">Hola primer paso es página toocreate un HTML estándar que contiene hello **vídeo** elemento, guarde este archivo como basicPlayer.html, como el siguiente ejemplo de Hola muestra:</span><span class="sxs-lookup"><span data-stu-id="6a95e-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="6a95e-127">Agregar Hola Reproductor DASH.js</span><span class="sxs-lookup"><span data-stu-id="6a95e-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="6a95e-128">aplicación de toohello de la implementación de referencia de dash.js con tooadd hello, necesitará toograb archivo de dash.all.js hello de versión de Hola 1.0 de proyecto dash.js.</span><span class="sxs-lookup"><span data-stu-id="6a95e-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="6a95e-129">Esto se debe guardar en la carpeta de JavaScript de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a95e-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="6a95e-130">Este archivo es un archivo de conveniencia que reúne todo el código de hello dash.js necesarios en un único archivo.</span><span class="sxs-lookup"><span data-stu-id="6a95e-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="6a95e-131">Si tiene un aspecto alrededor de repositorio dash.js de hello, observará Hola archivos individuales, probar el código y mucho más, pero si todo lo que desea toodo es usar dash.js, archivo dash.all.js de hello es lo que necesita.</span><span class="sxs-lookup"><span data-stu-id="6a95e-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="6a95e-132">aplicaciones de tooadd hello dash.js Reproductor tooyour, agregue una sección principal de secuencia de comandos etiqueta toohello de basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="6a95e-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="6a95e-133">A continuación, crear un Reproductor de hello tooinitialize de función cuando se carga la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a95e-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="6a95e-134">Agregue Hola siguiente secuencia de comandos después de la línea hello en el que se carga dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="6a95e-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="6a95e-135">Esta función crea primero un elemento DashContext.</span><span class="sxs-lookup"><span data-stu-id="6a95e-135">This function first creates a DashContext.</span></span> <span data-ttu-id="6a95e-136">Se trata de aplicación de hello tooconfigure usado para un entorno en tiempo de ejecución específica.</span><span class="sxs-lookup"><span data-stu-id="6a95e-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="6a95e-137">Desde un punto de vista técnico, define hello las clases que Hola framework de inyección de dependencia deben utilizar al construir la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6a95e-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="6a95e-138">En la mayoría de los casos, usará Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="6a95e-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="6a95e-139">A continuación, crear una instancia de la clase principal hello de marco de trabajo de hello dash.js, el Reproductor de Media.</span><span class="sxs-lookup"><span data-stu-id="6a95e-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="6a95e-140">Esta clase contiene el núcleo de hello métodos necesarios como reproducirán y pausar, administra Hola relación con el elemento de vídeo de Hola y también administra la interpretación de Hola de archivo de descripción de la presentación de medios (MPD) hello que describe hello toobe vídeo reproducida.</span><span class="sxs-lookup"><span data-stu-id="6a95e-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="6a95e-141">función de startup() Hello de hello MediaPlayer (clase) se denomina tooensure que el Reproductor de hello es listo tooplay de vídeo.</span><span class="sxs-lookup"><span data-stu-id="6a95e-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="6a95e-142">Entre otras cosas, esta función garantiza que todas las clases de hello necesarios (como se define según el contexto de Hola) se han cargado.</span><span class="sxs-lookup"><span data-stu-id="6a95e-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="6a95e-143">Cuando el Reproductor Hola esté listo, puede adjuntar Hola elemento video tooit con hello attachView() función.</span><span class="sxs-lookup"><span data-stu-id="6a95e-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="6a95e-144">Esto habilita la secuencia de vídeo de hello MediaPlayer tooinject hello en el elemento de Hola y también controlar la reproducción según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6a95e-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="6a95e-145">Pasar URL Hola de hello MPD archivo toohello MediaPlayer para que sepa sobre Hola vídeo se espera tooplay.hello setupVideo() función recién creado tendrá toobe ejecutada una vez que se haya cargado completamente página Hola.</span><span class="sxs-lookup"><span data-stu-id="6a95e-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="6a95e-146">Hacer esto mediante el uso de eventos onload de hello del elemento de cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a95e-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="6a95e-147">Cambie el elemento <body> a:</span><span class="sxs-lookup"><span data-stu-id="6a95e-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="6a95e-148">Por último, establecer tamaño de Hola de elemento vídeo Hola de CSS.</span><span class="sxs-lookup"><span data-stu-id="6a95e-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="6a95e-149">En un entorno de transmisión por secuencias adaptativo, esto es especialmente importante porque puede cambiar tamaño de Hola de hello vídeo se reproduce como reproducción adapta a las condiciones de red toochanging.</span><span class="sxs-lookup"><span data-stu-id="6a95e-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="6a95e-150">En esta demostración sencilla simplemente forzar Hola elemento video toobe 80% de la ventana del explorador disponible de hello agregando Hola pasos de CSS toohello la sección principal de la página de hello:</span><span class="sxs-lookup"><span data-stu-id="6a95e-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="6a95e-151">Reproducción de un vídeo</span><span class="sxs-lookup"><span data-stu-id="6a95e-151">Playing a Video</span></span>
<span data-ttu-id="6a95e-152">tooplay ver un vídeo, el explorador en el archivo de basicPlayback.html hello y haga clic en Reproducir en el Reproductor de vídeo de hello muestra.</span><span class="sxs-lookup"><span data-stu-id="6a95e-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6a95e-153">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="6a95e-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6a95e-154">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="6a95e-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6a95e-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6a95e-155">See Also</span></span>
[<span data-ttu-id="6a95e-156">Desarrollo de aplicaciones para reproductor de vídeo</span><span class="sxs-lookup"><span data-stu-id="6a95e-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="6a95e-157">Repositorio dash.js de GitHub</span><span class="sxs-lookup"><span data-stu-id="6a95e-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

