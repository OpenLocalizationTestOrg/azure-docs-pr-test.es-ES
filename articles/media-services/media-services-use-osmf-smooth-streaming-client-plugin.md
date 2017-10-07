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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>¿Cómo tooUse Hola complemento de transmisión por secuencias suave de Microsoft para hello Adobe Open origen Media Framework
## <a name="overview"></a>Información general
Hola complemento Microsoft Smooth Streaming para abrir Source Media Framework 2.0 (SS para OSMF) amplía las capacidades de predeterminado de Hola de OSMF y agrega toonew de reproducción de contenido de Microsoft Smooth Streaming y OSMF existente reproductores. complemento de Hello también agrega capacidades de reproducción Smooth Streaming tooStrobe Media Playback (SMP).

SS para OSMF incluye dos versiones del complemento:

* Complemento Smooth Streaming estático para OSMF (.swc)
* Complemento Smooth Streaming dinámico para OSMF (.swf)

Este documento se supone que el lector de hello tiene conocimientos prácticos generales de OSMF y OSMF complementos. Para obtener más información acerca de OSMF, consulte documentación de hello en hello [sitio oficial de OSMF](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Complemento Smooth Streaming para OSMF 2.0
Hola complemento admite la carga y la reproducción de contenido de transmisión por secuencias suave a petición con hello siguientes características:

* Reproducción de Smooth Streaming bajo demanda (Reproducir, Pausar, Buscar y Detener)
* Reproducción de Smooth Streaming en directo (Reproducir)
* Funciones de DVR en directo (Pausar, Buscar, Reproducción de DVR e Ir al directo)
* Compatibilidad con códecs de vídeo - H.264
* Compatibilidad con códecs de audio - AAC
* Conmutación de varios idiomas de audio con API integradas de OSMF
* Selección de calidad máxima de reproducción con API integradas de OSMF
* Títulos cerrados adicionales con el complemento de títulos de OSMF
* Adobe&reg; Flash&reg; Player 11.4 o superior.
* Esta versión solo admite OSMF 2.0.

## <a name="supported-features-and-known-issues"></a>Características admitidas y problemas conocidos
Para obtener una lista completa de las características admitidas, características no admitidas y problemas conocidos, consulte demasiado[este documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Hola cargar complemento
Los complementos de OSMF se pueden cargar estáticamente (en el momento de la compilación) o dinámicamente (en el tiempo de ejecución). complemento de transmisión por secuencias suave de Hola para su descarga OSMF incluye versiones estáticas y dinámicas.

* Carga estática: tooload estáticamente, se requiere un archivo de biblioteca estática (SWC). Complementos estáticas se agregan como una referencia de archivo toohello proyectos y mezcla en el resultado final de hello en tiempo de compilación de Hola.
* Carga dinámica: tooload dinámicamente, se requiere un archivo (SWF) precompilado. Dinámicas complementos se cargan en tiempo de ejecución de hello y no se incluye en el resultado del proyecto de Hola. (Resultado compilado) Los complementos dinámicos pueden cargarse con los protocolos HTTP y FILE.

Para obtener más información sobre la carga estática y dinámica, consulte oficial de hello [página de complemento OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>Carga estática de SS para OSMF
siguiente fragmento de código de Hello muestra cómo tooload Hola SS complemento para OSMF estáticamente y reproducir un vídeo básico mediante la clase de OSMF MediaFactory. Antes de incluir Hola SS para el código OSMF, por favor, asegúrese de que referencia de proyecto de hello incluye complemento estático Hola "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".

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


### <a name="ss-for-osmf-dynamic-loading"></a>Carga dinámica de SS para OSMF
siguiente fragmento de código de Hello muestra cómo tooload Hola SS complemento para OSMF dinámicamente y reproducir un vídeo básico mediante la clase de OSMF MediaFactory hello. Antes de incluir Hola SS para el código OSMF, copie la carpeta de proyecto de toohello de Hola "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" complementos dinámico si desea tooload mediante el protocolo de archivo, o copiar en un servidor web para la carga HTTP. No hay ningún tooinclude necesidad "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" en hello referencias del proyecto.

paquete {

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Strobe Media Playback con hello SS ODMF dinámica complemento
Hola Smooth Streaming de OSMF dinámica complemento es compatible con [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html). Puede usar hello SS para tooSMP de reproducción de contenido Smooth Streaming de OSMF complemento tooadd. toodo, copia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" en un servidor web para carga HTTP mediante Hola siguiendo los pasos:

1. Examinar hello [página de instalación Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html). 
2. Establezca Hola src tooa Smooth Streaming origen, (por ejemplo, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Realizar cambios de configuración de hello deseado y haga clic en vista previa y actualización.
   
   **Nota** : el servidor web de contenido necesita un archivo crossdomain.xml válido. 
4. Copie y pegue Hola código tooa página HTML sencilla con su editor de texto que prefiera, como en el siguiente ejemplo de Hola:

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



1. Toohello de complemento OSMF de Smooth Streaming de agregar código para insertar y guardar.
   
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
2. Guarde la página HTML y publicar el servidor web de tooa. Examinar toohello publicado página web con el Flash favoritos&reg; Reproductor habilitado el Explorador de Internet (Internet Explorer, Chrome, Firefox, etc.).
3. Disfrute del contenido de Smooth Streaming en Adobe&reg; Flash&reg; Player.

Para obtener más información sobre el desarrollo general de OSMF, vea oficial de hello [página de desarrollo de OSMF](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Actualización del complemento de streaming adaptable para OSMF](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

