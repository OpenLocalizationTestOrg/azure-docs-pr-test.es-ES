---
title: "aaaSmooth complemento de transmisión por secuencias para hello marco de medios de origen abierto"
description: "Obtenga información acerca de cómo toouse Hola complemento de Azure Media Services Smooth Streaming para hello Adobe marco de medios de origen abierto."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="a7790-103">¿Cómo tooUse Hola complemento de transmisión por secuencias suave de Microsoft para hello Adobe Open origen Media Framework</span><span class="sxs-lookup"><span data-stu-id="a7790-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="a7790-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a7790-104">Overview</span></span>
<span data-ttu-id="a7790-105">Hola complemento Microsoft Smooth Streaming para abrir Source Media Framework 2.0 (SS para OSMF) amplía las capacidades de predeterminado de Hola de OSMF y agrega toonew de reproducción de contenido de Microsoft Smooth Streaming y OSMF existente reproductores.</span><span class="sxs-lookup"><span data-stu-id="a7790-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="a7790-106">complemento de Hello también agrega capacidades de reproducción Smooth Streaming tooStrobe Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="a7790-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="a7790-107">SS para OSMF incluye dos versiones del complemento:</span><span class="sxs-lookup"><span data-stu-id="a7790-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="a7790-108">Complemento Smooth Streaming estático para OSMF (.swc)</span><span class="sxs-lookup"><span data-stu-id="a7790-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="a7790-109">Complemento Smooth Streaming dinámico para OSMF (.swf)</span><span class="sxs-lookup"><span data-stu-id="a7790-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="a7790-110">Este documento se supone que el lector de hello tiene conocimientos prácticos generales de OSMF y OSMF complementos. Para obtener más información acerca de OSMF, consulte documentación de hello en hello [sitio oficial de OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="a7790-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="a7790-111">Complemento Smooth Streaming para OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="a7790-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="a7790-112">Hola complemento admite la carga y la reproducción de contenido de transmisión por secuencias suave a petición con hello siguientes características:</span><span class="sxs-lookup"><span data-stu-id="a7790-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="a7790-113">Reproducción de Smooth Streaming bajo demanda (Reproducir, Pausar, Buscar y Detener)</span><span class="sxs-lookup"><span data-stu-id="a7790-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="a7790-114">Reproducción de Smooth Streaming en directo (Reproducir)</span><span class="sxs-lookup"><span data-stu-id="a7790-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="a7790-115">Funciones de DVR en directo (Pausar, Buscar, Reproducción de DVR e Ir al directo)</span><span class="sxs-lookup"><span data-stu-id="a7790-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="a7790-116">Compatibilidad con códecs de vídeo - H.264</span><span class="sxs-lookup"><span data-stu-id="a7790-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="a7790-117">Compatibilidad con códecs de audio - AAC</span><span class="sxs-lookup"><span data-stu-id="a7790-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="a7790-118">Conmutación de varios idiomas de audio con API integradas de OSMF</span><span class="sxs-lookup"><span data-stu-id="a7790-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="a7790-119">Selección de calidad máxima de reproducción con API integradas de OSMF</span><span class="sxs-lookup"><span data-stu-id="a7790-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="a7790-120">Títulos cerrados adicionales con el complemento de títulos de OSMF</span><span class="sxs-lookup"><span data-stu-id="a7790-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="a7790-121">Adobe&reg; Flash&reg; Player 11.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="a7790-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="a7790-122">Esta versión solo admite OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="a7790-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="a7790-123">Características admitidas y problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="a7790-123">Supported features and known issues</span></span>
<span data-ttu-id="a7790-124">Para obtener una lista completa de las características admitidas, características no admitidas y problemas conocidos, consulte demasiado[este documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="a7790-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="a7790-125">Hola cargar complemento</span><span class="sxs-lookup"><span data-stu-id="a7790-125">Loading hello Plugin</span></span>
<span data-ttu-id="a7790-126">Los complementos de OSMF se pueden cargar estáticamente (en el momento de la compilación) o dinámicamente (en el tiempo de ejecución).</span><span class="sxs-lookup"><span data-stu-id="a7790-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="a7790-127">complemento de transmisión por secuencias suave de Hola para su descarga OSMF incluye versiones estáticas y dinámicas.</span><span class="sxs-lookup"><span data-stu-id="a7790-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="a7790-128">Carga estática: tooload estáticamente, se requiere un archivo de biblioteca estática (SWC).</span><span class="sxs-lookup"><span data-stu-id="a7790-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="a7790-129">Complementos estáticas se agregan como una referencia de archivo toohello proyectos y mezcla en el resultado final de hello en tiempo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7790-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="a7790-130">Carga dinámica: tooload dinámicamente, se requiere un archivo (SWF) precompilado.</span><span class="sxs-lookup"><span data-stu-id="a7790-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="a7790-131">Dinámicas complementos se cargan en tiempo de ejecución de hello y no se incluye en el resultado del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7790-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="a7790-132">(Resultado compilado) Los complementos dinámicos pueden cargarse con los protocolos HTTP y FILE.</span><span class="sxs-lookup"><span data-stu-id="a7790-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="a7790-133">Para obtener más información sobre la carga estática y dinámica, consulte oficial de hello [página de complemento OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="a7790-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="a7790-134">Carga estática de SS para OSMF</span><span class="sxs-lookup"><span data-stu-id="a7790-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="a7790-135">siguiente fragmento de código de Hello muestra cómo tooload Hola SS complemento para OSMF estáticamente y reproducir un vídeo básico mediante la clase de OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="a7790-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="a7790-136">Antes de incluir Hola SS para el código OSMF, por favor, asegúrese de que referencia de proyecto de hello incluye complemento estático Hola "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="a7790-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="a7790-137">Carga dinámica de SS para OSMF</span><span class="sxs-lookup"><span data-stu-id="a7790-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="a7790-138">siguiente fragmento de código de Hello muestra cómo tooload Hola SS complemento para OSMF dinámicamente y reproducir un vídeo básico mediante la clase de OSMF MediaFactory hello.</span><span class="sxs-lookup"><span data-stu-id="a7790-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="a7790-139">Antes de incluir Hola SS para el código OSMF, copie la carpeta de proyecto de toohello de Hola "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" complementos dinámico si desea tooload mediante el protocolo de archivo, o copiar en un servidor web para la carga HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7790-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="a7790-140">No hay ningún tooinclude necesidad "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" en hello referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a7790-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="a7790-141">paquete {</span><span class="sxs-lookup"><span data-stu-id="a7790-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="a7790-142">}</span><span class="sxs-lookup"><span data-stu-id="a7790-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="a7790-143">Strobe Media Playback con hello SS ODMF dinámica complemento</span><span class="sxs-lookup"><span data-stu-id="a7790-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="a7790-144">Hola Smooth Streaming de OSMF dinámica complemento es compatible con [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="a7790-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="a7790-145">Puede usar hello SS para tooSMP de reproducción de contenido Smooth Streaming de OSMF complemento tooadd.</span><span class="sxs-lookup"><span data-stu-id="a7790-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="a7790-146">toodo, copia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" en un servidor web para carga HTTP mediante Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="a7790-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="a7790-147">Examinar hello [página de instalación Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="a7790-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="a7790-148">Establezca Hola src tooa Smooth Streaming origen, (por ejemplo, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="a7790-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="a7790-149">Realizar cambios de configuración de hello deseado y haga clic en vista previa y actualización.</span><span class="sxs-lookup"><span data-stu-id="a7790-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="a7790-150">**Nota** : el servidor web de contenido necesita un archivo crossdomain.xml válido.</span><span class="sxs-lookup"><span data-stu-id="a7790-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="a7790-151">Copie y pegue Hola código tooa página HTML sencilla con su editor de texto que prefiera, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="a7790-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="a7790-152">Toohello de complemento OSMF de Smooth Streaming de agregar código para insertar y guardar.</span><span class="sxs-lookup"><span data-stu-id="a7790-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="a7790-153">Guarde la página HTML y publicar el servidor web de tooa.</span><span class="sxs-lookup"><span data-stu-id="a7790-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="a7790-154">Examinar toohello publicado página web con el Flash favoritos&reg; Reproductor habilitado el Explorador de Internet (Internet Explorer, Chrome, Firefox, etc.).</span><span class="sxs-lookup"><span data-stu-id="a7790-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="a7790-155">Disfrute del contenido de Smooth Streaming en Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="a7790-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="a7790-156">Para obtener más información sobre el desarrollo general de OSMF, vea oficial de hello [página de desarrollo de OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="a7790-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a7790-157">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="a7790-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7790-158">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a7790-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a7790-159">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a7790-159">See Also</span></span>
[<span data-ttu-id="a7790-160">Actualización del complemento de streaming adaptable para OSMF</span><span class="sxs-lookup"><span data-stu-id="a7790-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

