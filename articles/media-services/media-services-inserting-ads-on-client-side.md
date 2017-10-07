---
title: aaaInserting anuncios en el lado del cliente de hello | Documentos de Microsoft
description: "Este tema muestra cómo tooinsert anuncios de Hola cliente."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Insertar anuncios en el lado del cliente de Hola
Este tema contiene información acerca de cómo tooinsert distintos tipos de anuncios en el lado del cliente de Hola.

Para obtener información acerca de la compatibilidad con anuncios y subtítulos en vídeos de streaming en vivo, consulte [Estándares de inserción de anuncios y subtítulos compatibles](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Actualmente, el Reproductor multimedia de Azure no admite anuncios.
> 
> 

## <a id="insert_ads_into_media"></a>Inserción de anuncios en contenido multimedia
Servicios multimedia de Azure proporciona compatibilidad para la inserción de anuncios a través de hello plataforma de Windows Media: marcos del Reproductor. Player framework con compatibilidad con anuncios está disponible para dispositivos Windows 8, Silverlight, Windows Phone 8 e iOS. Cada marco para Reproductor contiene código de ejemplo que muestra cómo tooimplement una aplicación de reproducción. Hay tres tipos diferentes de anuncios que se puede insertar en la lista multimedia:.

* **Lineal** – full anuncios en un marco que Pausar vídeo principal Hola.
* **No lineales** : anuncios superpuestos que se muestran cuando se está reproduciendo el vídeo principal hello, normalmente un logotipo u otra imagen estática coloca Reproductor Hola.
* **Complementaria** : anuncios que aparecen fuera de Reproductor de Hola.

Anuncios se pueden colocar en cualquier punto de la escala temporal del vídeo principal Hola. Debe indicar que el Reproductor de hello cuando tooplay Hola ad y que tooplay de anuncios. Esto se realiza con un conjunto de archivos XML estándar: Video Ad Service Template (VAST, plantilla de servicio de anuncio de vídeo), Digital Video Multiple Ad Playlist (VMAP, lista de reproducción de varios anuncios de vídeo digital), Media Abstract Sequencing Template (MAST, plantilla de secuenciación abstracta multimedia) y Digital Video Player Ad Interface Definition (VPAID, definición de interfaz de anuncios del reproductor de vídeo digital). Los archivos VAST especifican qué toodisplay de anuncios. Archivos VMAP especifican cuándo tooplay varios anuncios y contienen XML VAST. Los archivos MAST constituyen otra anuncios de toosequence de manera que también pueden contener XML VAST. Los archivos VPAID definen una interfaz entre el Reproductor de vídeo de Hola y anuncios de Hola o el servidor de anuncios.

Cada Player Framework funciona de forma diferente y cada uno se explicará en su propio tema. En este tema describirá tooinsert anuncios de Hola mecanismos básicos usados. Las aplicaciones de Reproductor de vídeo solicitan los anuncios desde un servidor de ad. el servidor de anuncios de Hola puede responder de varias maneras:

* Devolver un archivo VAST
* Devolver un archivo VMAP (con VAST insertado)
* Devolver un archivo MAST (con VAST insertado)
* Devolver un archivo VAST con anuncios VPAID

### <a name="using-a-video-ad-service-template-vast-file"></a>Mediante un archivo Video Ad Service Template (VAST)
Un archivo VAST especifica qué anuncios toodisplay. Hello XML siguiente es un ejemplo de un archivo VAST para un anuncio lineal:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

Hola describe anuncio lineal Hola <**lineal**> elemento. Especifica la duración de Hola de anuncio Hola, realizar el seguimiento de eventos, haga clic en, haga clic en seguimiento y un número de **MediaFile** elementos. Eventos de seguimiento se especifican en Hola <**TrackingEvents**> elemento y permitir que los diversos eventos que se producen durante la visualización de anuncios de Hola un tootrack de servidor de ad. En este caso Hola inicio, punto medio, finalización y expanda se realiza el seguimiento de eventos. evento de inicio de Hello tiene lugar cuando se muestra el anuncio de Hola. evento de punto medio de Hello tiene lugar cuando al menos se ha visto el 50% de la escala de tiempo del anuncio de Hola. evento de finalización de Hello ocurre cuando haya quedado ad hello toohello final. evento de expansión de Hola se produce cuando el usuario de Hola expande en pantalla de bienvenida Reproductor de vídeo toofull. Aviso se especifica con un <**Click-through**> elemento dentro de un <**VideoClicks**> elemento y especifica un toodisplay de recurso URI tooa cuando Hola usuario hace clic en el anuncio de Hola. ClickTracking se especifica en un <**ClickTracking**> elemento, también en Hola <**VideoClicks**> elemento y especifica un recurso de seguimiento para hello Reproductor toorequest Hola usuario haga clic en en ad.hello Hola <**MediaFile**> elementos especifican información sobre una codificación específica de un anuncio. Cuando hay más de un <**MediaFile**> elemento, Reproductor de vídeo de hello puede elegir la mejor codificación para la plataforma de Hola Hola. 

Los anuncios lineales pueden mostrarse en un orden especificado. toodo, agregar más <Ad> elementos toohello VAST de archivos y especificar orden hello mediante el atributo de secuencia de Hola. Hola de ejemplo siguiente se muestra cómo hacerlo:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

Los anuncios no lineales se especifican también en un elemento <Creative>. Hola siguiente ejemplo se muestra un <Creative> elemento que describe un anuncio no lineal.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


Hola <**NonLinearAds**> elemento puede contener uno o varios <**no lineales**> elementos, cada uno de los cuales puede describir un anuncio no lineal. Hola <**no lineales**> elemento especifica el recurso de hello para el anuncio no lineal Hola. Hola recurso puede ser una <**StaticResouce**>, <**IFrameResource**>, o un <**HTMLResouce**>. <**StaticResource**> describe un recurso no HTML y define un atributo creativeType que especifica cómo se muestran los recursos de hello:

Image/gif, image/jpeg, image/png: Hola recurso se muestra en una etiqueta HTML <**img**> etiqueta.

Application/x-javascript: recursos de Hola se muestra en una etiqueta HTML <**script**> etiqueta.

Application/x-shockwave-flash: recursos de Hola se muestra en un reproductor Flash.

**IFrameResource** describe un recurso HTML que se puede mostrar en un elemento IFrame. **HTMLResource** describe un fragmento de código HTML que se puede insertar en una página web. **TrackingEvents** especificar eventos de seguimiento y Hola URI toorequest cuando se produce el evento de Hola. Hola de este ejemplo se realiza el seguimiento de eventos acceptInvitation y collapse. Para obtener más información sobre hello **NonLinearAds** elemento y sus elementos secundarios, vea IAB.NET/vast. Tenga en cuenta que hello **TrackingEvents** elemento se encuentra dentro de hello **NonLinearAds** elemento en lugar de hello **no lineales** elemento.

Los anuncios complementarios se definen dentro de un elemento <CompanionAds>. Hola <CompanionAds> elemento puede contener uno o varios <Companion> elementos. Cada <Companion> elemento describe un anuncio complementario y puede contener una <StaticResource>, <IFrameResource>, o <HTMLResource> que se especifican en Hola de igual forma que en un anuncio no lineal. Un archivo VAST puede contener varios anuncios complementarios y aplicación de Reproductor de hello puede elegir hello más adecuado ad toodisplay. Para obtener más información acerca de VAST, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Uso de un archivo Digital Video Multiple Ad Playlist (VMAP)
Un archivo VMAP permite toospecify cuando se producen los saltos de ad, cada salto de cuánto tiempo es, cuántos se pueden mostrar dentro de un salto y qué tipos de anuncios se pueden mostrar durante una interrupción. Hola siguiente en un ejemplo de un archivo VMAP que define un salto de ad único:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Un archivo VMAP comienza con un elemento <VMAP> que contiene uno o más elementos <AdBreak>, cada uno de los cuales define una pausa comercial. Cada pausa comercial especifica un tipo de pausa, el identificador de la pausa y la compensación de tiempo. atributo de Hello breakType especifica el tipo de Hola de anuncio que se puede reproducir durante la interrupción de hello: lineal, no lineal o mostrar. Mostrar anuncios asignan anuncios complementarios de tooVAST. Se puede especificar más de un tipo de anuncio en una lista separada por comas (sin espacios). Hola breakID es un identificador opcional para anuncios de Hola. Hola timeOffset especifica cuándo se deben mostrar anuncios de Hola. Se puede especificar en uno de hello siguientes maneras:

1. Hora: en formato hh:mm:ss o hh:mm:ss.mmm, donde .mmm es milisegundos. valor de Hola de este atributo especifica la hora de Hola desde principio de hello del principio de toohello Hola vídeo de la escala de tiempo de interrupción para un anuncio Hola.
2. Porcentaje: en formato n % donde n es el porcentaje de Hola de hello tooplay de vídeo de la escala de tiempo antes de la reproducción de anuncios de Hola
3. Inicio/fin: Especifica que un anuncio debe mostrarse antes o después de que se ha mostrado vídeo Hola
4. Posición: especifica el orden de hello interrupciones del anuncio cuando el tiempo de Hola Hola interrupciones del anuncio es desconocido, como en el caso de transmisión por secuencias en directo. orden de Hola de cada interrupción se especifica en formato de hello #n donde n es un entero de 1 o mayor. 1 significa que el anuncio de Hola debe mostrarse en la primera oportunidad de hello, 2 significa anuncio de Hola debe mostrarse en la segunda oportunidad de Hola y así sucesivamente.

Dentro de Hola <**AdBreak**> elemento puede ser una <**AdSource**> elemento. Hola <**AdSource**> elemento contiene Hola siguientes atributos:

1. Id: especifica un identificador para el origen del anuncio de Hola
2. allowMultipleAds: un valor booleano que especifica si se pueden mostrar varios anuncios durante la interrupción para un anuncio Hola
3. followRedirects: un valor booleano opcional que especifica si debe respetar el Reproductor de vídeo de hello redirige en respuesta a un anuncio

Hola <**AdSource**> elemento proporciona Reproductor Hola respuesta a un anuncio en línea o una respuesta de referencia tooan ad. Puede contener uno de hello siguientes elementos:

* <VASTAdData>indica que una respuesta VAST ad está incrustada en el archivo VMAP de hello
* <AdTagURI>: un URI que hace referencia a una respuesta de anuncio desde otro sistema.
* <CustomAdData>: cadena arbitraria que representa una respuesta distinta de VAST.

En este ejemplo se especifica una respuesta de anuncio en línea con un elemento <VASTAdData> que contiene una respuesta de anuncio VAST. Para obtener más información acerca de hello otros elementos, consulte [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Hola <**AdBreak**> elemento también puede contener un <**TrackingEvents**> elemento. Hola <**TrackingEvents**> elemento le permite tootrack inicio de Hola o al final de una pausa publicitaria o si se produjo un error durante la interrupción para un anuncio Hola. Hola <**TrackingEvents**> elemento contiene uno o más <**seguimiento**> elementos, cada uno de los cuales especifica un evento de seguimiento y un URI de seguimiento. Hola eventos de seguimiento posibles son:

1. breakStart: sigue el principio de Hola de una pausa publicitaria
2. breakend: se sigue pista Hola finalización de una pausa publicitaria
3. Error: realiza un seguimiento de un error ocurrido durante la interrupción para un anuncio Hola

Hola de ejemplo siguiente muestra un archivo VMAP que especifica los eventos de seguimiento

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Para obtener más información sobre Hola <**TrackingEvents**> elemento y sus elementos secundarios, vea http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Uso de un archivo Media Abstract Sequencing Template (MAST)
Un archivo MAST le permite desencadenadores toospecify que definen cuándo se muestra un anuncio. Hola aquí te mostramos un ejemplo de un archivo MAST que contiene desencadenadores para un anuncio de cuña previa, una cuña intermedia y otro de cuña posterior a la.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



Un archivo MAST comienza con un elemento **MAST** que contiene un elemento **triggers**. Hola <triggers> elemento contiene uno o varios **desencadenador** elementos que definen cuándo se debe reproducir un anuncio. 

Hola **desencadenador** elemento contiene un **startConditions** elemento que especifican cuándo un anuncio debe comenzar tooplay. Hola **startConditions** elemento contiene uno o varios <condition> elementos. Cuando cada <condition> se evalúa como tootrue un desencadenador se inicia o revoca en función de si hello <condition> está dentro de un **startConditions** o **endConditions** elemento respectivamente. Cuando varios <condition> elementos están presentes, se tratan como un OR implícito, cualquier condición que se evalúe tootrue provocará Hola desencadenador tooinitiate. Los elementos <condition> pueden estar anidados. Cuando secundarios <condition> elementos están predefinidos, se tratan como un AND implícito, todas las condiciones deben evaluarse tootrue para hello desencadenador tooinitiate. Hola <condition> elemento contiene Hola siguientes atributos que definen la condición de hello: 

1. **tipo de** : especifica el tipo de saludo de condición, evento o propiedad
2. **nombre** : hello nombre de toobe de propiedad o evento de hello utilizada durante la evaluación
3. **valor** : Hola valor que se va a evaluar una propiedad en
4. **operador** : Hola toouse operación durante la evaluación: EQ (igual), NEQ (distinto), GTR (mayor que), GEQ (mayor o igual que), LT (menor que), LEQ (menor o igual que), MOD (módulo)

**endConditions** también contiene elementos <condition>. Cuando una condición se evalúa como desencadenador de hello tootrue es reset.hello <trigger> elemento también contiene un <sources> elemento que contiene uno o varios <source> elementos. Hola <source> elementos definen respuestas a los anuncios toohello Hola URI y el tipo de Hola de respuesta de ad. En este ejemplo se proporciona un URI tooa gran respuesta. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Uso de Video Player-Ad Interface Definition (VPAID)
VPAID es una API para permitir toocommunicate de unidades de anuncio ejecutable con un Reproductor de vídeo. Esto permite disfrutar de experiencias de anuncios altamente interactivas. Hola usuario puede interactuar con ad Hola y Hola puede responder tooactions realizada por el Visor de Hola. Por ejemplo, un anuncio puede mostrar botones que permitan Hola usuario tooview obtener más información o una versión más larga de anuncio Hola. Reproductor de vídeo de Hola debe admitir Hola API VPAID y anuncio de Hola ejecutable debe implementar Hola API. Cuando un Reproductor solicita un anuncio de un servidor de hello del servidor de anuncios puede responder con una respuesta VAST que contiene un anuncio vpaid.

Se crea un anuncio ejecutable en el código que debe ejecutarse en un entorno en tiempo de ejecución, como Adobe Flash ™ o JavaScript, que se pueden ejecutar en un explorador web. Cuando un servidor de anuncios devuelve una respuesta VAST que contiene un anuncio vpaid, Hola valor del atributo apiFramework de Hola Hola <MediaFile> elemento debe ser "VPAID". Este atributo especifica que ad Hola contenida es un anuncio ejecutable vpaid. atributo de tipo Hello debe establecerse toohello tipo MIME de hello ejecutable, como "application/x-shockwave-flash" o "application/x-javascript". Hello fragmento XML siguiente muestra hello <MediaFile> elemento de una respuesta VAST que contiene un anuncio ejecutable vpaid. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Un anuncio ejecutable se puede inicializar con hello <AdParameters> elemento dentro de hello <Linear> o <NonLinear> elementos en una respuesta VAST. Para obtener más información sobre hello <AdParameters> elemento, vea [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf). Para obtener más información acerca de la API VPAID hello, consulte [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Implementación de un reproductor de Windows o Windows Phone 8 con compatibilidad para anuncios
Hola plataforma de Microsoft Media: marco de Reproductor de Windows 8 y Windows Phone 8 contiene una colección de aplicaciones de ejemplo que muestran cómo tooimplement una aplicación de Reproductor de vídeo con Hola framework. Puede descargar los ejemplos de hello y marco para Reproductor de Hola de [Player Framework para Windows 8 y Windows Phone 8](https://playerframework.codeplex.com).

Cuando se abre la solución Microsoft.PlayerFramework.Xaml.Samples de hello verá varias carpetas en el proyecto de Hola. carpeta de anuncios de Hola contiene toocreating relevantes de código de ejemplo de Hola un Reproductor de vídeo con compatibilidad para anuncios. Carpeta de anuncios de Hola interior es un número de XAML/cs cada uno de los que mostrar archivos cómo tooinsert anuncios de forma diferente. Hola lista siguiente describe cada uno de ellos:

* AdPodPage.xaml muestra cómo toodisplay un anuncio pod.
* AdSchedulingPage.xaml muestra cómo tooschedule anuncios.
* FreeWheelPage.xaml muestra cómo toouse Hola FreeWheel complemento tooschedule anuncios.
* MastPage.xaml muestra cómo tooschedule anuncios con un archivo MAST.
* ProgrammaticAdPage.xaml muestra cómo programar los anuncios tooprogrammatically en un vídeo.
* ScheduleClipPage.xaml muestra cómo tooschedule un anuncio sin un archivo VAST.
* VastLinearCompanionPage.xaml muestra cómo tooinsert una lineal y anuncio complementario.
* VastNonLinearPage.xaml muestra cómo tooinsert un anuncio no lineal.
* VmapPage.xaml muestra cómo toospecify anuncios con un archivo VMAP.

Cada uno de estos ejemplos usa MediaPlayer (clase) Hola definida por el marco de trabajo de hello Reproductor. En la mayoría de los ejemplos se usan complementos que agregan compatibilidad para varios formatos de respuesta de anuncio. ejemplo de Hola ProgrammaticAdPage interactúa mediante programación con una instancia de MediaPlayer.

### <a name="adpodpage-sample"></a>Ejemplo AdPodPage
Este ejemplo utiliza hello AdSchedulerPlugin toodefine cuando toodisplay un anuncio. En este ejemplo, un anuncio de cuña intermedia es toobe programada reproducido después de 5 segundos. anuncios de Hola (un grupo de anuncios toodisplay en orden) se especifican en un archivo VAST devuelto desde un servidor de ad. archivo VAST de Hello URI toohello se especifica en hello <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

Para obtener más información acerca de hello AdSchedulerPlugin, consulte [anuncio Hola Player Framework en Windows 8 y Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
Este ejemplo también utiliza hello AdSchedulerPlugin. Programa tres anuncios, un anuncio de cuña previa, uno de cuña intermedia y uno de cuña posterior. Hola toohello VAST de URI para cada anuncio se especifica en un <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
Este ejemplo utiliza hello FreeWheelPlugin que especifica un atributo de origen que especifica un URI ese archivo SmartXML tooa de puntos que especifica el contenido de ad, así como información de programación de ad.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
Este ejemplo utiliza hello MastSchedulerPlugin que permita toouse un archivo MAST. atributo de origen de Hello especifica la ubicación de hello del archivo MAST de hello.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
Este ejemplo interactúa mediante programación con hello MediaPlayer. archivo de Hello ProgrammaticAdPage.xaml crea una instancia de hello MediaPlayer:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

archivo de Hello ProgrammaticAdPage.xaml.cs crea un AdHandlerPlugin, agrega un toospecify TimelineMarker cuando un anuncio debe mostrarse y, a continuación, agrega un controlador para el evento MarkerReached Hola que carga un RemoteAdSource especificando un archivo VAST de tooa URI y, a continuación, se reproduce anuncio de Hola.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
Este ejemplo utiliza hello AdSchedulerPlugin tooschedule una cuña intermedia especificando un archivo .wmv que contiene anuncios de Hola.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
Este ejemplo muestra cómo toouse Hola AdSchedulerPlugin tooschedule un anuncio lineal de cuña intermedia con un anuncio complementario. Hola <RemoteAdSource> elemento especifica la ubicación de hello del archivo VAST Hola.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
Este ejemplo utiliza hello AdSchedulerPlugin tooschedule un lineal y un anuncio no lineal. Hola ubicación del archivo VAST se especifica con hello <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
Este ejemplo utiliza anuncios de Hola VmapSchedulerPlugin tooschedule con un archivo VMAP. archivo de Hello URI toohello VMAP se especifica en el atributo de origen de Hola de hello <VmapSchedulerPlugin> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Implementación de un reproductor de vídeo de iOS con compatibilidad para anuncios
Hola plataforma de Microsoft Media: marco para Reproductor para iOS contiene una colección de aplicaciones de ejemplo que muestran cómo tooimplement una aplicación de Reproductor de vídeo con Hola framework. Puede descargar los ejemplos de hello y marco para Reproductor de Hola de [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). página de github Hello tiene un tooa vínculo Wiki que contiene información adicional sobre el marco de trabajo de hello Reproductor y un ejemplo de introducción toohello Reproductor: [Wiki de Azure Media Player](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>Programación de anuncios con VMAP
Hola siguiente ejemplo se muestra cómo tooschedule los anuncios con un archivo VMAP.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>Programación de anuncios con VAST
siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio VAST de enlace tiempo de ejecución.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio VAST de enlace temprano.
Programación de ejemplo: 4 un Hola de //Download del anuncio VAST de enlace temprano VAST archivo si (! [ framework.adResolver downloadManifest: & manifiesto withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[logFrameworkError propio];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

siguiente Hola de ejemplo se muestra cómo tooinsert un anuncio con edición de cortar aproximada (RCE)

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

Hello en el ejemplo siguiente se muestra cómo tooschedule un anuncio pod.

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hola siguiente ejemplo se muestra cómo tooschedule un anuncio de cuña intermedia no estático. Un anuncio no estático solo se reproduce una vez sin tener en cuenta cualquier Hola búsqueda realiza Visor.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hola siguiente ejemplo se muestra cómo tooschedule una cuña intermedia estática. Un anuncio estático se mostrará cada vez Hola especificado se alcanza el punto de la escala de tiempo de vídeo de Hola.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio de cuña posterior.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio de cuña previa.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hola siguiente ejemplo muestra cómo tooschedule una cuña intermedia superposición de ad.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Desarrollo de aplicaciones para reproductor de vídeo](media-services-develop-video-players.md)

