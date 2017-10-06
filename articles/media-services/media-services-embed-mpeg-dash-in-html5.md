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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Incrustación de un vídeo de transmisión por secuencias adaptativa MPEG-DASH en una aplicación HTML5 con DASH.js
## <a name="overview"></a>Información general
MPEG-DASH es un estándar ISO para hello adaptable de transmisión por secuencias de contenido de vídeo, lo que ofrece ventajas significativas para quienes desea vídeo de alta calidad, adaptable toodeliver salida de transmisión por secuencias. Con MPEG-DASH, secuencia de vídeo de hello quitará automáticamente definición inferior tooa cuando se satura red Hola. Esto reduce la probabilidad de Hola de Visor de hello ver un vídeo "en pausa" mientras hello, el Reproductor descarga Hola a continuación algunos tooplay segundos (también conocido como almacenamiento en búfer). Reduce la congestión de la red, Reproductor de vídeo de Hola a su vez devolverá tooa flujo de calidad superior. Este ancho de banda Hola del tooadapt de capacidad necesario también se produce en una hora de inicio más rápida de vídeo. Que significa que los primeros segundos de Hola puede reproducirse en un segmento de calidad inferior fast para descargar y, a continuación, el paso de calidad superior tooa una vez que se han almacenado en búfer suficiente contenido.

Dash.js es un reproductor de vídeo MPEG-DASH de código abierto escrito en JavaScript. Su objetivo es tooprovide un reproductor sólido entre plataformas que se pueda reutilizar libremente en aplicaciones que requieren la reproducción de vídeo. Proporciona reproducción MPEG-DASH en cualquier explorador que admita Hola W3C Media Source Extensions (MSE), hoy en día es Chrome, Microsoft Edge e IE11 (otros exploradores han indicado su intención toosupport MSE). Para obtener más información acerca de DASH.js, js vea repositorio dash.js de GitHub de Hola.

## <a name="creating-a-browser-based-streaming-video-player"></a>Creación de un reproductor de vídeo de streaming basado en explorador
toocreate una página web sencilla que muestra un Reproductor de vídeo Hola espera que controla este tipo reproducir, pausa, rebobinar etc., deberá:

1. Crear una página HTML
2. Agregar la etiqueta de vídeo de Hola
3. Agregar hello dash.js jugador
4. Inicializar Reproductor Hola
5. Agregar algún estilo CSS
6. Ver los resultados en un explorador que implementa MSE Hola

Al inicializar el Reproductor Hola se puede completar en unos pocos de las líneas de código de JavaScript. Con dash.js, realmente es que vídeo tooembed simple MPEG-DASH en las aplicaciones basadas en explorador.

## <a name="creating-hello-html-page"></a>Creación de hello página HTML
Hola primer paso es página toocreate un HTML estándar que contiene hello **vídeo** elemento, guarde este archivo como basicPlayer.html, como el siguiente ejemplo de Hola muestra:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Agregar Hola Reproductor DASH.js
aplicación de toohello de la implementación de referencia de dash.js con tooadd hello, necesitará toograb archivo de dash.all.js hello de versión de Hola 1.0 de proyecto dash.js. Esto se debe guardar en la carpeta de JavaScript de saludo de la aplicación. Este archivo es un archivo de conveniencia que reúne todo el código de hello dash.js necesarios en un único archivo. Si tiene un aspecto alrededor de repositorio dash.js de hello, observará Hola archivos individuales, probar el código y mucho más, pero si todo lo que desea toodo es usar dash.js, archivo dash.all.js de hello es lo que necesita.

aplicaciones de tooadd hello dash.js Reproductor tooyour, agregue una sección principal de secuencia de comandos etiqueta toohello de basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


A continuación, crear un Reproductor de hello tooinitialize de función cuando se carga la página de Hola. Agregue Hola siguiente secuencia de comandos después de la línea hello en el que se carga dash.all.js:

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

Esta función crea primero un elemento DashContext. Se trata de aplicación de hello tooconfigure usado para un entorno en tiempo de ejecución específica. Desde un punto de vista técnico, define hello las clases que Hola framework de inyección de dependencia deben utilizar al construir la aplicación hello. En la mayoría de los casos, usará Dash.di.DashContext.

A continuación, crear una instancia de la clase principal hello de marco de trabajo de hello dash.js, el Reproductor de Media. Esta clase contiene el núcleo de hello métodos necesarios como reproducirán y pausar, administra Hola relación con el elemento de vídeo de Hola y también administra la interpretación de Hola de archivo de descripción de la presentación de medios (MPD) hello que describe hello toobe vídeo reproducida.

función de startup() Hello de hello MediaPlayer (clase) se denomina tooensure que el Reproductor de hello es listo tooplay de vídeo. Entre otras cosas, esta función garantiza que todas las clases de hello necesarios (como se define según el contexto de Hola) se han cargado. Cuando el Reproductor Hola esté listo, puede adjuntar Hola elemento video tooit con hello attachView() función. Esto habilita la secuencia de vídeo de hello MediaPlayer tooinject hello en el elemento de Hola y también controlar la reproducción según sea necesario.

Pasar URL Hola de hello MPD archivo toohello MediaPlayer para que sepa sobre Hola vídeo se espera tooplay.hello setupVideo() función recién creado tendrá toobe ejecutada una vez que se haya cargado completamente página Hola. Hacer esto mediante el uso de eventos onload de hello del elemento de cuerpo de Hola. Cambie el elemento <body> a:

    <body onload="setupVideo()">

Por último, establecer tamaño de Hola de elemento vídeo Hola de CSS. En un entorno de transmisión por secuencias adaptativo, esto es especialmente importante porque puede cambiar tamaño de Hola de hello vídeo se reproduce como reproducción adapta a las condiciones de red toochanging. En esta demostración sencilla simplemente forzar Hola elemento video toobe 80% de la ventana del explorador disponible de hello agregando Hola pasos de CSS toohello la sección principal de la página de hello:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Reproducción de un vídeo
tooplay ver un vídeo, el explorador en el archivo de basicPlayback.html hello y haga clic en Reproducir en el Reproductor de vídeo de hello muestra.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Desarrollo de aplicaciones para reproductor de vídeo](media-services-develop-video-players.md)

[Repositorio dash.js de GitHub](https://github.com/Dash-Industry-Forum/dash.js) 

