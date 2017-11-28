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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="1b0ea-103">Insertar anuncios en el lado del cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="1b0ea-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="1b0ea-104">Este tema contiene información acerca de cómo tooinsert distintos tipos de anuncios en el lado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="1b0ea-105">Para obtener información acerca de la compatibilidad con anuncios y subtítulos en vídeos de streaming en vivo, consulte [Estándares de inserción de anuncios y subtítulos compatibles](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="1b0ea-106">Actualmente, el Reproductor multimedia de Azure no admite anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="1b0ea-107"><a id="insert_ads_into_media"></a>Inserción de anuncios en contenido multimedia</span><span class="sxs-lookup"><span data-stu-id="1b0ea-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="1b0ea-108">Servicios multimedia de Azure proporciona compatibilidad para la inserción de anuncios a través de hello plataforma de Windows Media: marcos del Reproductor.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="1b0ea-109">Player framework con compatibilidad con anuncios está disponible para dispositivos Windows 8, Silverlight, Windows Phone 8 e iOS.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="1b0ea-110">Cada marco para Reproductor contiene código de ejemplo que muestra cómo tooimplement una aplicación de reproducción. Hay tres tipos diferentes de anuncios que se puede insertar en la lista multimedia:.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="1b0ea-111">**Lineal** – full anuncios en un marco que Pausar vídeo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="1b0ea-112">**No lineales** : anuncios superpuestos que se muestran cuando se está reproduciendo el vídeo principal hello, normalmente un logotipo u otra imagen estática coloca Reproductor Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="1b0ea-113">**Complementaria** : anuncios que aparecen fuera de Reproductor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="1b0ea-114">Anuncios se pueden colocar en cualquier punto de la escala temporal del vídeo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="1b0ea-115">Debe indicar que el Reproductor de hello cuando tooplay Hola ad y que tooplay de anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="1b0ea-116">Esto se realiza con un conjunto de archivos XML estándar: Video Ad Service Template (VAST, plantilla de servicio de anuncio de vídeo), Digital Video Multiple Ad Playlist (VMAP, lista de reproducción de varios anuncios de vídeo digital), Media Abstract Sequencing Template (MAST, plantilla de secuenciación abstracta multimedia) y Digital Video Player Ad Interface Definition (VPAID, definición de interfaz de anuncios del reproductor de vídeo digital).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="1b0ea-117">Los archivos VAST especifican qué toodisplay de anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="1b0ea-118">Archivos VMAP especifican cuándo tooplay varios anuncios y contienen XML VAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="1b0ea-119">Los archivos MAST constituyen otra anuncios de toosequence de manera que también pueden contener XML VAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="1b0ea-120">Los archivos VPAID definen una interfaz entre el Reproductor de vídeo de Hola y anuncios de Hola o el servidor de anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="1b0ea-121">Cada Player Framework funciona de forma diferente y cada uno se explicará en su propio tema.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="1b0ea-122">En este tema describirá tooinsert anuncios de Hola mecanismos básicos usados. Las aplicaciones de Reproductor de vídeo solicitan los anuncios desde un servidor de ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="1b0ea-123">el servidor de anuncios de Hola puede responder de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="1b0ea-124">Devolver un archivo VAST</span><span class="sxs-lookup"><span data-stu-id="1b0ea-124">Return a VAST file</span></span>
* <span data-ttu-id="1b0ea-125">Devolver un archivo VMAP (con VAST insertado)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="1b0ea-126">Devolver un archivo MAST (con VAST insertado)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="1b0ea-127">Devolver un archivo VAST con anuncios VPAID</span><span class="sxs-lookup"><span data-stu-id="1b0ea-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="1b0ea-128">Mediante un archivo Video Ad Service Template (VAST)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="1b0ea-129">Un archivo VAST especifica qué anuncios toodisplay.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="1b0ea-130">Hello XML siguiente es un ejemplo de un archivo VAST para un anuncio lineal:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="1b0ea-131">Hola describe anuncio lineal Hola <**lineal**> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="1b0ea-132">Especifica la duración de Hola de anuncio Hola, realizar el seguimiento de eventos, haga clic en, haga clic en seguimiento y un número de **MediaFile** elementos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="1b0ea-133">Eventos de seguimiento se especifican en Hola <**TrackingEvents**> elemento y permitir que los diversos eventos que se producen durante la visualización de anuncios de Hola un tootrack de servidor de ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="1b0ea-134">En este caso Hola inicio, punto medio, finalización y expanda se realiza el seguimiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="1b0ea-135">evento de inicio de Hello tiene lugar cuando se muestra el anuncio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="1b0ea-136">evento de punto medio de Hello tiene lugar cuando al menos se ha visto el 50% de la escala de tiempo del anuncio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="1b0ea-137">evento de finalización de Hello ocurre cuando haya quedado ad hello toohello final.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="1b0ea-138">evento de expansión de Hola se produce cuando el usuario de Hola expande en pantalla de bienvenida Reproductor de vídeo toofull.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="1b0ea-139">Aviso se especifica con un <**Click-through**> elemento dentro de un <**VideoClicks**> elemento y especifica un toodisplay de recurso URI tooa cuando Hola usuario hace clic en el anuncio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="1b0ea-140">ClickTracking se especifica en un <**ClickTracking**> elemento, también en Hola <**VideoClicks**> elemento y especifica un recurso de seguimiento para hello Reproductor toorequest Hola usuario haga clic en en ad.hello Hola <**MediaFile**> elementos especifican información sobre una codificación específica de un anuncio.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="1b0ea-141">Cuando hay más de un <**MediaFile**> elemento, Reproductor de vídeo de hello puede elegir la mejor codificación para la plataforma de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="1b0ea-142">Los anuncios lineales pueden mostrarse en un orden especificado.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="1b0ea-143">toodo, agregar más <Ad> elementos toohello VAST de archivos y especificar orden hello mediante el atributo de secuencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="1b0ea-144">Hola de ejemplo siguiente se muestra cómo hacerlo:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="1b0ea-145">Los anuncios no lineales se especifican también en un elemento <Creative>.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="1b0ea-146">Hola siguiente ejemplo se muestra un <Creative> elemento que describe un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="1b0ea-147">Hola <**NonLinearAds**> elemento puede contener uno o varios <**no lineales**> elementos, cada uno de los cuales puede describir un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="1b0ea-148">Hola <**no lineales**> elemento especifica el recurso de hello para el anuncio no lineal Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="1b0ea-149">Hola recurso puede ser una <**StaticResouce**>, <**IFrameResource**>, o un <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="1b0ea-150"> <**StaticResource**> describe un recurso no HTML y define un atributo creativeType que especifica cómo se muestran los recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="1b0ea-151">Image/gif, image/jpeg, image/png: Hola recurso se muestra en una etiqueta HTML <**img**> etiqueta.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="1b0ea-152">Application/x-javascript: recursos de Hola se muestra en una etiqueta HTML <**script**> etiqueta.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="1b0ea-153">Application/x-shockwave-flash: recursos de Hola se muestra en un reproductor Flash.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="1b0ea-154">**IFrameResource** describe un recurso HTML que se puede mostrar en un elemento IFrame.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="1b0ea-155">**HTMLResource** describe un fragmento de código HTML que se puede insertar en una página web.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="1b0ea-156">**TrackingEvents** especificar eventos de seguimiento y Hola URI toorequest cuando se produce el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="1b0ea-157">Hola de este ejemplo se realiza el seguimiento de eventos acceptInvitation y collapse.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="1b0ea-158">Para obtener más información sobre hello **NonLinearAds** elemento y sus elementos secundarios, vea IAB.NET/vast.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="1b0ea-159">Tenga en cuenta que hello **TrackingEvents** elemento se encuentra dentro de hello **NonLinearAds** elemento en lugar de hello **no lineales** elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="1b0ea-160">Los anuncios complementarios se definen dentro de un elemento <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="1b0ea-161">Hola <CompanionAds> elemento puede contener uno o varios <Companion> elementos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="1b0ea-162">Cada <Companion> elemento describe un anuncio complementario y puede contener una <StaticResource>, <IFrameResource>, o <HTMLResource> que se especifican en Hola de igual forma que en un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="1b0ea-163">Un archivo VAST puede contener varios anuncios complementarios y aplicación de Reproductor de hello puede elegir hello más adecuado ad toodisplay.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="1b0ea-164">Para obtener más información acerca de VAST, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="1b0ea-165">Uso de un archivo Digital Video Multiple Ad Playlist (VMAP)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="1b0ea-166">Un archivo VMAP permite toospecify cuando se producen los saltos de ad, cada salto de cuánto tiempo es, cuántos se pueden mostrar dentro de un salto y qué tipos de anuncios se pueden mostrar durante una interrupción.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="1b0ea-167">Hola siguiente en un ejemplo de un archivo VMAP que define un salto de ad único:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="1b0ea-168">Un archivo VMAP comienza con un elemento <VMAP> que contiene uno o más elementos <AdBreak>, cada uno de los cuales define una pausa comercial.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="1b0ea-169">Cada pausa comercial especifica un tipo de pausa, el identificador de la pausa y la compensación de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="1b0ea-170">atributo de Hello breakType especifica el tipo de Hola de anuncio que se puede reproducir durante la interrupción de hello: lineal, no lineal o mostrar.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="1b0ea-171">Mostrar anuncios asignan anuncios complementarios de tooVAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="1b0ea-172">Se puede especificar más de un tipo de anuncio en una lista separada por comas (sin espacios).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="1b0ea-173">Hola breakID es un identificador opcional para anuncios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="1b0ea-174">Hola timeOffset especifica cuándo se deben mostrar anuncios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="1b0ea-175">Se puede especificar en uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="1b0ea-176">Hora: en formato hh:mm:ss o hh:mm:ss.mmm, donde .mmm es milisegundos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="1b0ea-177">valor de Hola de este atributo especifica la hora de Hola desde principio de hello del principio de toohello Hola vídeo de la escala de tiempo de interrupción para un anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="1b0ea-178">Porcentaje: en formato n % donde n es el porcentaje de Hola de hello tooplay de vídeo de la escala de tiempo antes de la reproducción de anuncios de Hola</span><span class="sxs-lookup"><span data-stu-id="1b0ea-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="1b0ea-179">Inicio/fin: Especifica que un anuncio debe mostrarse antes o después de que se ha mostrado vídeo Hola</span><span class="sxs-lookup"><span data-stu-id="1b0ea-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="1b0ea-180">Posición: especifica el orden de hello interrupciones del anuncio cuando el tiempo de Hola Hola interrupciones del anuncio es desconocido, como en el caso de transmisión por secuencias en directo.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="1b0ea-181">orden de Hola de cada interrupción se especifica en formato de hello #n donde n es un entero de 1 o mayor.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="1b0ea-182">1 significa que el anuncio de Hola debe mostrarse en la primera oportunidad de hello, 2 significa anuncio de Hola debe mostrarse en la segunda oportunidad de Hola y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="1b0ea-183">Dentro de Hola <**AdBreak**> elemento puede ser una <**AdSource**> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="1b0ea-184">Hola <**AdSource**> elemento contiene Hola siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="1b0ea-185">Id: especifica un identificador para el origen del anuncio de Hola</span><span class="sxs-lookup"><span data-stu-id="1b0ea-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="1b0ea-186">allowMultipleAds: un valor booleano que especifica si se pueden mostrar varios anuncios durante la interrupción para un anuncio Hola</span><span class="sxs-lookup"><span data-stu-id="1b0ea-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="1b0ea-187">followRedirects: un valor booleano opcional que especifica si debe respetar el Reproductor de vídeo de hello redirige en respuesta a un anuncio</span><span class="sxs-lookup"><span data-stu-id="1b0ea-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="1b0ea-188">Hola <**AdSource**> elemento proporciona Reproductor Hola respuesta a un anuncio en línea o una respuesta de referencia tooan ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="1b0ea-189">Puede contener uno de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="1b0ea-190"><VASTAdData>indica que una respuesta VAST ad está incrustada en el archivo VMAP de hello</span><span class="sxs-lookup"><span data-stu-id="1b0ea-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="1b0ea-191"><AdTagURI>: un URI que hace referencia a una respuesta de anuncio desde otro sistema.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="1b0ea-192"><CustomAdData>: cadena arbitraria que representa una respuesta distinta de VAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="1b0ea-193">En este ejemplo se especifica una respuesta de anuncio en línea con un elemento <VASTAdData> que contiene una respuesta de anuncio VAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="1b0ea-194">Para obtener más información acerca de hello otros elementos, consulte [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="1b0ea-195">Hola <**AdBreak**> elemento también puede contener un <**TrackingEvents**> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="1b0ea-196">Hola <**TrackingEvents**> elemento le permite tootrack inicio de Hola o al final de una pausa publicitaria o si se produjo un error durante la interrupción para un anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="1b0ea-197">Hola <**TrackingEvents**> elemento contiene uno o más <**seguimiento**> elementos, cada uno de los cuales especifica un evento de seguimiento y un URI de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="1b0ea-198">Hola eventos de seguimiento posibles son:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="1b0ea-199">breakStart: sigue el principio de Hola de una pausa publicitaria</span><span class="sxs-lookup"><span data-stu-id="1b0ea-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="1b0ea-200">breakend: se sigue pista Hola finalización de una pausa publicitaria</span><span class="sxs-lookup"><span data-stu-id="1b0ea-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="1b0ea-201">Error: realiza un seguimiento de un error ocurrido durante la interrupción para un anuncio Hola</span><span class="sxs-lookup"><span data-stu-id="1b0ea-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="1b0ea-202">Hola de ejemplo siguiente muestra un archivo VMAP que especifica los eventos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="1b0ea-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="1b0ea-203">Para obtener más información sobre Hola <**TrackingEvents**> elemento y sus elementos secundarios, vea http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="1b0ea-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="1b0ea-204">Uso de un archivo Media Abstract Sequencing Template (MAST)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="1b0ea-205">Un archivo MAST le permite desencadenadores toospecify que definen cuándo se muestra un anuncio.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="1b0ea-206">Hola aquí te mostramos un ejemplo de un archivo MAST que contiene desencadenadores para un anuncio de cuña previa, una cuña intermedia y otro de cuña posterior a la.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="1b0ea-207">Un archivo MAST comienza con un elemento **MAST** que contiene un elemento **triggers**.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="1b0ea-208">Hola <triggers> elemento contiene uno o varios **desencadenador** elementos que definen cuándo se debe reproducir un anuncio.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="1b0ea-209">Hola **desencadenador** elemento contiene un **startConditions** elemento que especifican cuándo un anuncio debe comenzar tooplay.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="1b0ea-210">Hola **startConditions** elemento contiene uno o varios <condition> elementos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="1b0ea-211">Cuando cada <condition> se evalúa como tootrue un desencadenador se inicia o revoca en función de si hello <condition> está dentro de un **startConditions** o **endConditions** elemento respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="1b0ea-212">Cuando varios <condition> elementos están presentes, se tratan como un OR implícito, cualquier condición que se evalúe tootrue provocará Hola desencadenador tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="1b0ea-213">Los elementos <condition> pueden estar anidados.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-213"><condition> elements can be nested.</span></span> <span data-ttu-id="1b0ea-214">Cuando secundarios <condition> elementos están predefinidos, se tratan como un AND implícito, todas las condiciones deben evaluarse tootrue para hello desencadenador tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="1b0ea-215">Hola <condition> elemento contiene Hola siguientes atributos que definen la condición de hello:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="1b0ea-216">**tipo de** : especifica el tipo de saludo de condición, evento o propiedad</span><span class="sxs-lookup"><span data-stu-id="1b0ea-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="1b0ea-217">**nombre** : hello nombre de toobe de propiedad o evento de hello utilizada durante la evaluación</span><span class="sxs-lookup"><span data-stu-id="1b0ea-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="1b0ea-218">**valor** : Hola valor que se va a evaluar una propiedad en</span><span class="sxs-lookup"><span data-stu-id="1b0ea-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="1b0ea-219">**operador** : Hola toouse operación durante la evaluación: EQ (igual), NEQ (distinto), GTR (mayor que), GEQ (mayor o igual que), LT (menor que), LEQ (menor o igual que), MOD (módulo)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="1b0ea-220">**endConditions** también contiene elementos <condition>.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="1b0ea-221">Cuando una condición se evalúa como desencadenador de hello tootrue es reset.hello <trigger> elemento también contiene un <sources> elemento que contiene uno o varios <source> elementos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="1b0ea-222">Hola <source> elementos definen respuestas a los anuncios toohello Hola URI y el tipo de Hola de respuesta de ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="1b0ea-223">En este ejemplo se proporciona un URI tooa gran respuesta.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="1b0ea-224">Uso de Video Player-Ad Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="1b0ea-225">VPAID es una API para permitir toocommunicate de unidades de anuncio ejecutable con un Reproductor de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="1b0ea-226">Esto permite disfrutar de experiencias de anuncios altamente interactivas.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="1b0ea-227">Hola usuario puede interactuar con ad Hola y Hola puede responder tooactions realizada por el Visor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="1b0ea-228">Por ejemplo, un anuncio puede mostrar botones que permitan Hola usuario tooview obtener más información o una versión más larga de anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="1b0ea-229">Reproductor de vídeo de Hola debe admitir Hola API VPAID y anuncio de Hola ejecutable debe implementar Hola API.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="1b0ea-230">Cuando un Reproductor solicita un anuncio de un servidor de hello del servidor de anuncios puede responder con una respuesta VAST que contiene un anuncio vpaid.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="1b0ea-231">Se crea un anuncio ejecutable en el código que debe ejecutarse en un entorno en tiempo de ejecución, como Adobe Flash ™ o JavaScript, que se pueden ejecutar en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="1b0ea-232">Cuando un servidor de anuncios devuelve una respuesta VAST que contiene un anuncio vpaid, Hola valor del atributo apiFramework de Hola Hola <MediaFile> elemento debe ser "VPAID".</span><span class="sxs-lookup"><span data-stu-id="1b0ea-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="1b0ea-233">Este atributo especifica que ad Hola contenida es un anuncio ejecutable vpaid.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="1b0ea-234">atributo de tipo Hello debe establecerse toohello tipo MIME de hello ejecutable, como "application/x-shockwave-flash" o "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="1b0ea-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="1b0ea-235">Hello fragmento XML siguiente muestra hello <MediaFile> elemento de una respuesta VAST que contiene un anuncio ejecutable vpaid.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="1b0ea-236">Un anuncio ejecutable se puede inicializar con hello <AdParameters> elemento dentro de hello <Linear> o <NonLinear> elementos en una respuesta VAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="1b0ea-237">Para obtener más información sobre hello <AdParameters> elemento, vea [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="1b0ea-238">Para obtener más información acerca de la API VPAID hello, consulte [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="1b0ea-239">Implementación de un reproductor de Windows o Windows Phone 8 con compatibilidad para anuncios</span><span class="sxs-lookup"><span data-stu-id="1b0ea-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="1b0ea-240">Hola plataforma de Microsoft Media: marco de Reproductor de Windows 8 y Windows Phone 8 contiene una colección de aplicaciones de ejemplo que muestran cómo tooimplement una aplicación de Reproductor de vídeo con Hola framework.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="1b0ea-241">Puede descargar los ejemplos de hello y marco para Reproductor de Hola de [Player Framework para Windows 8 y Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="1b0ea-242">Cuando se abre la solución Microsoft.PlayerFramework.Xaml.Samples de hello verá varias carpetas en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="1b0ea-243">carpeta de anuncios de Hola contiene toocreating relevantes de código de ejemplo de Hola un Reproductor de vídeo con compatibilidad para anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="1b0ea-244">Carpeta de anuncios de Hola interior es un número de XAML/cs cada uno de los que mostrar archivos cómo tooinsert anuncios de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="1b0ea-245">Hola lista siguiente describe cada uno de ellos:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-245">hello following list describes each:</span></span>

* <span data-ttu-id="1b0ea-246">AdPodPage.xaml muestra cómo toodisplay un anuncio pod.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="1b0ea-247">AdSchedulingPage.xaml muestra cómo tooschedule anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="1b0ea-248">FreeWheelPage.xaml muestra cómo toouse Hola FreeWheel complemento tooschedule anuncios.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="1b0ea-249">MastPage.xaml muestra cómo tooschedule anuncios con un archivo MAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="1b0ea-250">ProgrammaticAdPage.xaml muestra cómo programar los anuncios tooprogrammatically en un vídeo.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="1b0ea-251">ScheduleClipPage.xaml muestra cómo tooschedule un anuncio sin un archivo VAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="1b0ea-252">VastLinearCompanionPage.xaml muestra cómo tooinsert una lineal y anuncio complementario.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="1b0ea-253">VastNonLinearPage.xaml muestra cómo tooinsert un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="1b0ea-254">VmapPage.xaml muestra cómo toospecify anuncios con un archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="1b0ea-255">Cada uno de estos ejemplos usa MediaPlayer (clase) Hola definida por el marco de trabajo de hello Reproductor.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="1b0ea-256">En la mayoría de los ejemplos se usan complementos que agregan compatibilidad para varios formatos de respuesta de anuncio.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="1b0ea-257">ejemplo de Hola ProgrammaticAdPage interactúa mediante programación con una instancia de MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="1b0ea-258">Ejemplo AdPodPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-258">AdPodPage Sample</span></span>
<span data-ttu-id="1b0ea-259">Este ejemplo utiliza hello AdSchedulerPlugin toodefine cuando toodisplay un anuncio.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="1b0ea-260">En este ejemplo, un anuncio de cuña intermedia es toobe programada reproducido después de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="1b0ea-261">anuncios de Hola (un grupo de anuncios toodisplay en orden) se especifican en un archivo VAST devuelto desde un servidor de ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="1b0ea-262">archivo VAST de Hello URI toohello se especifica en hello <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="1b0ea-263">Para obtener más información acerca de hello AdSchedulerPlugin, consulte [anuncio Hola Player Framework en Windows 8 y Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="1b0ea-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-264">AdSchedulingPage</span></span>
<span data-ttu-id="1b0ea-265">Este ejemplo también utiliza hello AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="1b0ea-266">Programa tres anuncios, un anuncio de cuña previa, uno de cuña intermedia y uno de cuña posterior.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="1b0ea-267">Hola toohello VAST de URI para cada anuncio se especifica en un <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="1b0ea-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-268">FreeWheelPage</span></span>
<span data-ttu-id="1b0ea-269">Este ejemplo utiliza hello FreeWheelPlugin que especifica un atributo de origen que especifica un URI ese archivo SmartXML tooa de puntos que especifica el contenido de ad, así como información de programación de ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="1b0ea-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-270">MastPage</span></span>
<span data-ttu-id="1b0ea-271">Este ejemplo utiliza hello MastSchedulerPlugin que permita toouse un archivo MAST.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="1b0ea-272">atributo de origen de Hello especifica la ubicación de hello del archivo MAST de hello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="1b0ea-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="1b0ea-274">Este ejemplo interactúa mediante programación con hello MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="1b0ea-275">archivo de Hello ProgrammaticAdPage.xaml crea una instancia de hello MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="1b0ea-276">archivo de Hello ProgrammaticAdPage.xaml.cs crea un AdHandlerPlugin, agrega un toospecify TimelineMarker cuando un anuncio debe mostrarse y, a continuación, agrega un controlador para el evento MarkerReached Hola que carga un RemoteAdSource especificando un archivo VAST de tooa URI y, a continuación, se reproduce anuncio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="1b0ea-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-277">ScheduleClipPage</span></span>
<span data-ttu-id="1b0ea-278">Este ejemplo utiliza hello AdSchedulerPlugin tooschedule una cuña intermedia especificando un archivo .wmv que contiene anuncios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="1b0ea-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="1b0ea-280">Este ejemplo muestra cómo toouse Hola AdSchedulerPlugin tooschedule un anuncio lineal de cuña intermedia con un anuncio complementario.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="1b0ea-281">Hola <RemoteAdSource> elemento especifica la ubicación de hello del archivo VAST Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="1b0ea-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="1b0ea-283">Este ejemplo utiliza hello AdSchedulerPlugin tooschedule un lineal y un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="1b0ea-284">Hola ubicación del archivo VAST se especifica con hello <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="1b0ea-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="1b0ea-285">VMAPPage</span></span>
<span data-ttu-id="1b0ea-286">Este ejemplo utiliza anuncios de Hola VmapSchedulerPlugin tooschedule con un archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="1b0ea-287">archivo de Hello URI toohello VMAP se especifica en el atributo de origen de Hola de hello <VmapSchedulerPlugin> elemento.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="1b0ea-288">Implementación de un reproductor de vídeo de iOS con compatibilidad para anuncios</span><span class="sxs-lookup"><span data-stu-id="1b0ea-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="1b0ea-289">Hola plataforma de Microsoft Media: marco para Reproductor para iOS contiene una colección de aplicaciones de ejemplo que muestran cómo tooimplement una aplicación de Reproductor de vídeo con Hola framework.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="1b0ea-290">Puede descargar los ejemplos de hello y marco para Reproductor de Hola de [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="1b0ea-291">página de github Hello tiene un tooa vínculo Wiki que contiene información adicional sobre el marco de trabajo de hello Reproductor y un ejemplo de introducción toohello Reproductor: [Wiki de Azure Media Player](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="1b0ea-292">Programación de anuncios con VMAP</span><span class="sxs-lookup"><span data-stu-id="1b0ea-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="1b0ea-293">Hola siguiente ejemplo se muestra cómo tooschedule los anuncios con un archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="1b0ea-294">Programación de anuncios con VAST</span><span class="sxs-lookup"><span data-stu-id="1b0ea-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="1b0ea-295">siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio VAST de enlace tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="1b0ea-296">siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio VAST de enlace temprano.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="1b0ea-297">Programación de ejemplo: 4 un Hola de //Download del anuncio VAST de enlace temprano VAST archivo si (! [ framework.adResolver downloadManifest: & manifiesto withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[logFrameworkError propio];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="1b0ea-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="1b0ea-298">siguiente Hola de ejemplo se muestra cómo tooinsert un anuncio con edición de cortar aproximada (RCE)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="1b0ea-299">Hello en el ejemplo siguiente se muestra cómo tooschedule un anuncio pod.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="1b0ea-300">Hola siguiente ejemplo se muestra cómo tooschedule un anuncio de cuña intermedia no estático.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="1b0ea-301">Un anuncio no estático solo se reproduce una vez sin tener en cuenta cualquier Hola búsqueda realiza Visor.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="1b0ea-302">Hola siguiente ejemplo se muestra cómo tooschedule una cuña intermedia estática.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="1b0ea-303">Un anuncio estático se mostrará cada vez Hola especificado se alcanza el punto de la escala de tiempo de vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="1b0ea-304">siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio de cuña posterior.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="1b0ea-305">siguiente Hola de ejemplo se muestra cómo tooschedule un anuncio de cuña previa.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="1b0ea-306">Hola siguiente ejemplo muestra cómo tooschedule una cuña intermedia superposición de ad.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="1b0ea-307">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1b0ea-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1b0ea-308">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1b0ea-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1b0ea-309">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1b0ea-309">See Also</span></span>
[<span data-ttu-id="1b0ea-310">Desarrollo de aplicaciones para reproductor de vídeo</span><span class="sxs-lookup"><span data-stu-id="1b0ea-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

