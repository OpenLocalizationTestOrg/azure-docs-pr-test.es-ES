---
title: "Inserción de anuncios en el lado cliente | Microsoft Docs"
description: "Este tema muestra cómo insertar anuncios en el lado cliente."
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
ms.openlocfilehash: 52ba731f88c630830560e3cf8406ba2e9613c8a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="inserting-ads-on-the-client-side"></a><span data-ttu-id="e5328-103">Inserción de anuncios en el lado cliente</span><span class="sxs-lookup"><span data-stu-id="e5328-103">Inserting ads on the client side</span></span>
<span data-ttu-id="e5328-104">Este tema contiene información sobre cómo insertar distintos tipos de anuncios en el lado cliente.</span><span class="sxs-lookup"><span data-stu-id="e5328-104">This topic contains information on how to insert various types of ads on the client side.</span></span>

<span data-ttu-id="e5328-105">Para obtener información acerca de la compatibilidad con anuncios y subtítulos en vídeos de streaming en vivo, consulte [Estándares de inserción de anuncios y subtítulos compatibles](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="e5328-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="e5328-106">Actualmente, el Reproductor multimedia de Azure no admite anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="e5328-107"><a id="insert_ads_into_media"></a>Inserción de anuncios en contenido multimedia</span><span class="sxs-lookup"><span data-stu-id="e5328-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="e5328-108">Servicios multimedia de Azure admite la inserción de anuncios mediante Plataforma multimedia de Microsoft: Player Frameworks.</span><span class="sxs-lookup"><span data-stu-id="e5328-108">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="e5328-109">Player framework con compatibilidad con anuncios está disponible para dispositivos Windows 8, Silverlight, Windows Phone 8 e iOS.</span><span class="sxs-lookup"><span data-stu-id="e5328-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="e5328-110">Cada Player Framework contiene código de ejemplo que muestra cómo implementar una aplicación de reproductor. Hay tres tipos diferentes de anuncios que se pueden insertar en los medios:</span><span class="sxs-lookup"><span data-stu-id="e5328-110">Each player framework contains sample code that shows you how to implement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="e5328-111">**Lineales** : anuncios de fotograma completo que pausan el vídeo principal.</span><span class="sxs-lookup"><span data-stu-id="e5328-111">**Linear** – full frame ads that pause the main video.</span></span>
* <span data-ttu-id="e5328-112">**No lineales** : anuncios superpuestos que se muestran mientras se reproduce el vídeo principal, normalmente un logotipo u otra imagen estática colocada dentro del reproductor.</span><span class="sxs-lookup"><span data-stu-id="e5328-112">**Nonlinear** – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player.</span></span>
* <span data-ttu-id="e5328-113">**Complementarios** : anuncios que se muestran fuera del reproductor.</span><span class="sxs-lookup"><span data-stu-id="e5328-113">**Companion** – ads that are displayed outside of the player.</span></span>

<span data-ttu-id="e5328-114">Los anuncios se pueden colocar en cualquier punto de la línea de tiempo del vídeo principal.</span><span class="sxs-lookup"><span data-stu-id="e5328-114">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="e5328-115">Debe indicar al reproductor cuándo reproducir el anuncio y qué anuncios reproducir.</span><span class="sxs-lookup"><span data-stu-id="e5328-115">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="e5328-116">Esto se realiza con un conjunto de archivos XML estándar: Video Ad Service Template (VAST, plantilla de servicio de anuncio de vídeo), Digital Video Multiple Ad Playlist (VMAP, lista de reproducción de varios anuncios de vídeo digital), Media Abstract Sequencing Template (MAST, plantilla de secuenciación abstracta multimedia) y Digital Video Player Ad Interface Definition (VPAID, definición de interfaz de anuncios del reproductor de vídeo digital).</span><span class="sxs-lookup"><span data-stu-id="e5328-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="e5328-117">Los archivos VAST especifican qué anuncios mostrar.</span><span class="sxs-lookup"><span data-stu-id="e5328-117">VAST files specify what ads to display.</span></span> <span data-ttu-id="e5328-118">Los archivos VMAP especifican cuándo reproducir varios anuncios y contienen XML VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-118">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="e5328-119">Los archivos MAST constituyen otra manera de secuenciar los anuncios que también pueden contener XML VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-119">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="e5328-120">Los archivos VPAID definen una interfaz entre el reproductor de vídeo y el anuncio o el servidor de anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-120">VPAID files define an interface between the video player and the ad or ad server.</span></span>

<span data-ttu-id="e5328-121">Cada Player Framework funciona de forma diferente y cada uno se explicará en su propio tema.</span><span class="sxs-lookup"><span data-stu-id="e5328-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="e5328-122">En este tema se describen los mecanismos básicos usados para insertar anuncios. Las aplicaciones de reproductor de vídeo solicitan anuncios a un servidor de anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-122">This topic will describe the basic mechanisms used to insert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="e5328-123">El servidor de anuncios puede responder de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="e5328-123">The ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="e5328-124">Devolver un archivo VAST</span><span class="sxs-lookup"><span data-stu-id="e5328-124">Return a VAST file</span></span>
* <span data-ttu-id="e5328-125">Devolver un archivo VMAP (con VAST insertado)</span><span class="sxs-lookup"><span data-stu-id="e5328-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="e5328-126">Devolver un archivo MAST (con VAST insertado)</span><span class="sxs-lookup"><span data-stu-id="e5328-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="e5328-127">Devolver un archivo VAST con anuncios VPAID</span><span class="sxs-lookup"><span data-stu-id="e5328-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="e5328-128">Mediante un archivo Video Ad Service Template (VAST)</span><span class="sxs-lookup"><span data-stu-id="e5328-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="e5328-129">Un archivo VAST especifica qué anuncios mostrar.</span><span class="sxs-lookup"><span data-stu-id="e5328-129">A VAST file specifies what ad or ads to display.</span></span> <span data-ttu-id="e5328-130">El siguiente código XML es un ejemplo de un archivo VAST para un anuncio lineal:</span><span class="sxs-lookup"><span data-stu-id="e5328-130">The following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="e5328-131">El anuncio lineal se describe en el elemento <**Linear**>.</span><span class="sxs-lookup"><span data-stu-id="e5328-131">The linear ad is described by the <**Linear**> element.</span></span> <span data-ttu-id="e5328-132">Especifica la duración del anuncio, eventos de seguimiento, click-through, el seguimiento de clics y diversos elementos **MediaFile**.</span><span class="sxs-lookup"><span data-stu-id="e5328-132">It specifies the duration of the ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="e5328-133">Los eventos de seguimiento se especifican dentro del elemento <**TrackingEvents**> y permiten que un servidor de anuncios realice el seguimiento de diversos eventos que se producen mientras se visualiza el anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-133">Tracking events are specified within the <**TrackingEvents**> element and allow an ad server to track various events that occur while viewing the ad.</span></span> <span data-ttu-id="e5328-134">En este caso se realiza un seguimiento de los eventos start, midpoint, complete y expand.</span><span class="sxs-lookup"><span data-stu-id="e5328-134">In this case the start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="e5328-135">El evento start se produce cuando se muestra el anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-135">The start event occurs when the ad is displayed.</span></span> <span data-ttu-id="e5328-136">El evento midpoint se produce cuando se visualiza al menos el 50% de la escala de tiempo del anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-136">The midpoint event occurs when at least 50% of the ad’s timeline has been viewed.</span></span> <span data-ttu-id="e5328-137">Cuando el anuncio llega al final, se produce el evento complete.</span><span class="sxs-lookup"><span data-stu-id="e5328-137">The complete event occurs when the ad has run to the end.</span></span> <span data-ttu-id="e5328-138">El evento expand se produce cuando el usuario expande el reproductor de vídeo a pantalla completa.</span><span class="sxs-lookup"><span data-stu-id="e5328-138">The Expand event occurs when the user expands the video player to full screen.</span></span> <span data-ttu-id="e5328-139">Los click-through se especifican con un elemento <**ClickThrough**> dentro de un elemento <**VideoClicks**>, que especifica el identificador URI de un recurso que se muestra cuando el usuario hace clic en el anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI to a resource to display when the user clicks on the ad.</span></span> <span data-ttu-id="e5328-140">ClickTracking se especifica en un elemento <**ClickTracking**>, también dentro del elemento <**VideoClicks**> y especifica un recurso de seguimiento para que el reproductor lo solicite cuando el usuario haga clic en el anuncio. Los elementos <**MediaFile**> especifican información sobre una codificación concreta de un anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-140">ClickTracking is specified in a <**ClickTracking**> element, also within the <**VideoClicks**> element and specifies a tracking resource for the player to request when the user clicks on the ad.The <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="e5328-141">Cuando haya más de un elemento <**MediaFile**>, el reproductor de vídeo puede elegir la mejor codificación para la plataforma.</span><span class="sxs-lookup"><span data-stu-id="e5328-141">When there is more than one <**MediaFile**> element, the video player can choose the best encoding for the platform.</span></span> 

<span data-ttu-id="e5328-142">Los anuncios lineales pueden mostrarse en un orden especificado.</span><span class="sxs-lookup"><span data-stu-id="e5328-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="e5328-143">Para ello, agregue elementos <Ad> adicionales al archivo VAST y especifique el orden usando el atributo sequence.</span><span class="sxs-lookup"><span data-stu-id="e5328-143">To do this, add additional <Ad> elements to the VAST file and specify the order using the sequence attribute.</span></span> <span data-ttu-id="e5328-144">Esto se ilustra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5328-144">The following example illustrates this:</span></span>

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

<span data-ttu-id="e5328-145">Los anuncios no lineales se especifican también en un elemento <Creative>.</span><span class="sxs-lookup"><span data-stu-id="e5328-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="e5328-146">El ejemplo siguiente muestra un elemento <Creative> que describe un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="e5328-146">The following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="e5328-147">El elemento <**NonLinearAds**> puede contener uno o varios elementos <**NonLinear**>, y cada uno de ellos puede describir un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="e5328-147">The <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="e5328-148">El elemento <**NonLinear**> especifica el recurso para el anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="e5328-148">The <**NonLinear**> element specifies the resource for the nonlinear ad.</span></span> <span data-ttu-id="e5328-149">El recurso puede ser <**StaticResouce**>, <**IFrameResource**> o <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="e5328-149">The resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="e5328-150"> <**StaticResource**> describe un recurso no HTML y define un atributo creativeType que especifica cómo se muestra el recurso:</span><span class="sxs-lookup"><span data-stu-id="e5328-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how the resource is displayed:</span></span>

<span data-ttu-id="e5328-151">Image/gif, image/jpeg, image/png: el recurso se muestra en una etiqueta HTML <**img**>.</span><span class="sxs-lookup"><span data-stu-id="e5328-151">Image/gif, image/jpeg, image/png – the resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="e5328-152">Application/x-javascript: el recurso se muestra en una etiqueta HTML <**script**>.</span><span class="sxs-lookup"><span data-stu-id="e5328-152">Application/x-javascript – the resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="e5328-153">Application/x-shockwave-flash: el recurso se muestra en un reproductor Flash.</span><span class="sxs-lookup"><span data-stu-id="e5328-153">Application/x-shockwave-flash – the resource is displayed in a Flash player.</span></span>

<span data-ttu-id="e5328-154">**IFrameResource** describe un recurso HTML que se puede mostrar en un elemento IFrame.</span><span class="sxs-lookup"><span data-stu-id="e5328-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="e5328-155">**HTMLResource** describe un fragmento de código HTML que se puede insertar en una página web.</span><span class="sxs-lookup"><span data-stu-id="e5328-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="e5328-156">**TrackingEvents** especifica los eventos de seguimiento y el identificador URI que se solicita cuando se produce el evento.</span><span class="sxs-lookup"><span data-stu-id="e5328-156">**TrackingEvents** specify tracking events and the URI to request when the event occurs.</span></span> <span data-ttu-id="e5328-157">En este ejemplo se realiza el seguimiento de los eventos acceptInvitation y collapse.</span><span class="sxs-lookup"><span data-stu-id="e5328-157">In this sample the acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="e5328-158">Para más información sobre el elemento **NonLinearAds** y sus elementos secundarios, consulte IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-158">For more information on the **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="e5328-159">Tenga en cuenta que el elemento **TrackingEvents** se encuentra dentro del elemento **NonLinearAds**, en lugar del elemento **NonLinear**.</span><span class="sxs-lookup"><span data-stu-id="e5328-159">Note that the **TrackingEvents** element is located within the **NonLinearAds** element rather than the **NonLinear** element.</span></span>

<span data-ttu-id="e5328-160">Los anuncios complementarios se definen dentro de un elemento <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="e5328-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="e5328-161">El elemento <CompanionAds> puede contener uno o varios elementos <Companion>.</span><span class="sxs-lookup"><span data-stu-id="e5328-161">The <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="e5328-162">Cada elemento <Companion> describe un anuncio complementario y puede contener un <StaticResource>, una <IFrameResource> o un <HTMLResource>, que se especifican de la misma forma que un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="e5328-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in the same way as in a nonlinear ad.</span></span> <span data-ttu-id="e5328-163">Un archivo VAST puede contener varios anuncios complementarios y la aplicación de reproductor puede elegir el anuncio más apropiado para mostrar.</span><span class="sxs-lookup"><span data-stu-id="e5328-163">A VAST file can contain multiple companion ads and the player application can choose the most appropriate ad to display.</span></span> <span data-ttu-id="e5328-164">Para obtener más información acerca de VAST, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="e5328-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="e5328-165">Uso de un archivo Digital Video Multiple Ad Playlist (VMAP)</span><span class="sxs-lookup"><span data-stu-id="e5328-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="e5328-166">Un archivo VMAP permite especificar cuándo se producen pausas comerciales, cuánto dura cada pausa, cuántos anuncios pueden mostrarse en una pausa y qué tipos de anuncios se pueden mostrar durante una pausa.</span><span class="sxs-lookup"><span data-stu-id="e5328-166">A VMAP file allows you to specify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="e5328-167">El siguiente en un ejemplo de un archivo VMAP que define una única pausa comercial:</span><span class="sxs-lookup"><span data-stu-id="e5328-167">The following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="e5328-168">Un archivo VMAP comienza con un elemento <VMAP> que contiene uno o más elementos <AdBreak>, cada uno de los cuales define una pausa comercial.</span><span class="sxs-lookup"><span data-stu-id="e5328-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="e5328-169">Cada pausa comercial especifica un tipo de pausa, el identificador de la pausa y la compensación de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e5328-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="e5328-170">El atributo breakType especifica el tipo de anuncio que se puede reproducir durante la pausa: linear, nonlinear o display.</span><span class="sxs-lookup"><span data-stu-id="e5328-170">The breakType attribute specifies the type of ad that can be played during the break: linear, nonlinear, or display.</span></span> <span data-ttu-id="e5328-171">Los anuncios display se corresponden con los anuncios complementarios de VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-171">Display ads map to VAST companion ads.</span></span> <span data-ttu-id="e5328-172">Se puede especificar más de un tipo de anuncio en una lista separada por comas (sin espacios).</span><span class="sxs-lookup"><span data-stu-id="e5328-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="e5328-173">breakID es el identificador opcional del anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-173">The breakID is an optional identifier for the ad.</span></span> <span data-ttu-id="e5328-174">timeOffset especifica cuándo se debe mostrar el anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-174">The timeOffset specifies when the ad should be displayed.</span></span> <span data-ttu-id="e5328-175">Se puede especificar de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="e5328-175">It can be specified in one of the following ways:</span></span>

1. <span data-ttu-id="e5328-176">Hora: en formato hh:mm:ss o hh:mm:ss.mmm, donde .mmm es milisegundos.</span><span class="sxs-lookup"><span data-stu-id="e5328-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="e5328-177">El valor de este atributo especifica el tiempo que transcurre desde el principio de la escala de tiempo del vídeo al principio de la pausa comercial.</span><span class="sxs-lookup"><span data-stu-id="e5328-177">The value of this attribute specifies the time from the beginning of the video timeline to the beginning of the ad break.</span></span>
2. <span data-ttu-id="e5328-178">Porcentaje: en formato n%, donde n es el porcentaje de la escala de tiempo de vídeo que se reproducirá antes del anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-178">Percentage – in n% format where n is the percentage of the video timeline to play before playing the ad</span></span>
3. <span data-ttu-id="e5328-179">Start/end: especifica que un anuncio debe mostrarse antes o después de que se muestre el vídeo.</span><span class="sxs-lookup"><span data-stu-id="e5328-179">Start/End – specifies that an ad should be displayed before or after the video has been displayed</span></span>
4. <span data-ttu-id="e5328-180">Posición: especifica el orden de las pausas comerciales cuando no se conoce la temporización de las mismas, como en el caso del streaming en vivo.</span><span class="sxs-lookup"><span data-stu-id="e5328-180">Position – specifies the order of ad breaks when the timing of the ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="e5328-181">El orden de cada pausa publicitaria en el formato #n, donde n es un entero igual o mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="e5328-181">The order of each ad break is specified in the #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="e5328-182">1 significa que el anuncio debe reproducirse en la primera oportunidad; 2 significa el anuncio debe reproducirse en la segunda oportunidad, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="e5328-182">1 signifies the ad should be played at the first opportunity, 2 signifies the ad should be played at the second opportunity and so on.</span></span>

<span data-ttu-id="e5328-183">En el elemento <**AdBreak**>, puede haber un elemento <**AdSource**>.</span><span class="sxs-lookup"><span data-stu-id="e5328-183">Within the <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="e5328-184">El elemento <**AdSource**> contiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="e5328-184">The <**AdSource**> element contains the following attributes:</span></span>

1. <span data-ttu-id="e5328-185">Id: especifica el identificador del origen del anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-185">Id – specifies an identifier for the ad source</span></span>
2. <span data-ttu-id="e5328-186">allowMultipleAds: valor booleano que especifica si se pueden mostrar varios anuncios durante la pausa comercial.</span><span class="sxs-lookup"><span data-stu-id="e5328-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during the ad break</span></span>
3. <span data-ttu-id="e5328-187">followRedirects: un valor booleano opcional que especifica si el reproductor de vídeo debe respetar las redirecciones dentro de una respuesta de anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-187">followRedirects – an optional Boolean value that specifies if the video player should honor redirects within an ad response</span></span>

<span data-ttu-id="e5328-188">El elemento <**AdSource**> proporciona al reproductor una respuesta de anuncio en línea o una referencia a una respuesta de anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-188">The <**AdSource**> element provides the player an inline ad response or a reference to an ad response.</span></span> <span data-ttu-id="e5328-189">Puede contener uno de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e5328-189">It can contain one of the following elements:</span></span>

* <span data-ttu-id="e5328-190"><VASTAdData>: indica que una respuesta de anuncio VAST se inserta dentro del archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="e5328-190"><VASTAdData> indicates a VAST ad response is embedded within the VMAP file</span></span>
* <span data-ttu-id="e5328-191"><AdTagURI>: un URI que hace referencia a una respuesta de anuncio desde otro sistema.</span><span class="sxs-lookup"><span data-stu-id="e5328-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="e5328-192"><CustomAdData>: cadena arbitraria que representa una respuesta distinta de VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="e5328-193">En este ejemplo se especifica una respuesta de anuncio en línea con un elemento <VASTAdData> que contiene una respuesta de anuncio VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="e5328-194">Para obtener más información acerca de los demás elementos, consulte [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="e5328-194">For more information about the other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="e5328-195">El elemento <**AdBreak**> también puede contener un elemento <**TrackingEvents**>.</span><span class="sxs-lookup"><span data-stu-id="e5328-195">The <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="e5328-196">El elemento <**TrackingEvents**> permite realizar el seguimiento del inicio o fin de una pausa comercial o de si se produjo un error durante la pausa comercial.</span><span class="sxs-lookup"><span data-stu-id="e5328-196">The <**TrackingEvents**> element allows you to track the start or end of an ad break or whether an error occurred during the ad break.</span></span> <span data-ttu-id="e5328-197">El elemento <**TrackingEvents**> contiene uno o más <**Tracking**>, cada uno de los cuales especifica un evento de seguimiento y un URI de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="e5328-197">The <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="e5328-198">Los posibles eventos de seguimiento son:</span><span class="sxs-lookup"><span data-stu-id="e5328-198">The possible tracking events are:</span></span>

1. <span data-ttu-id="e5328-199">breakStart: realiza un seguimiento del principio de una pausa comercial</span><span class="sxs-lookup"><span data-stu-id="e5328-199">breakStart – tracks the beginning of an ad break</span></span>
2. <span data-ttu-id="e5328-200">breakend: realiza un seguimiento de la finalización de una pausa comercial</span><span class="sxs-lookup"><span data-stu-id="e5328-200">breakEnd – track the completion of an ad break</span></span>
3. <span data-ttu-id="e5328-201">error: realiza un seguimiento de un error producido durante la pausa comercial</span><span class="sxs-lookup"><span data-stu-id="e5328-201">error – tracks an error that occurred during the ad break</span></span>

<span data-ttu-id="e5328-202">En el ejemplo siguiente se muestra un archivo VMAP que especifica eventos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="e5328-202">The following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="e5328-203">Para obtener más información sobre el elemento <**TrackingEvents**> y sus elementos secundarios, vea http://iab.org/VMAP.pdf.</span><span class="sxs-lookup"><span data-stu-id="e5328-203">For more information on the <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="e5328-204">Uso de un archivo Media Abstract Sequencing Template (MAST)</span><span class="sxs-lookup"><span data-stu-id="e5328-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="e5328-205">Un archivo MAST permite especificar desencadenadores que definen cuándo se muestra un anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-205">A MAST file allows you to specify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="e5328-206">El siguiente es un archivo MAST de ejemplo que contiene desencadenadores para un anuncio de cuña previa, de cuña intermedia y de cuña posterior.</span><span class="sxs-lookup"><span data-stu-id="e5328-206">The following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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
            <!--This 'resets' the trigger for the next clip-->
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



<span data-ttu-id="e5328-207">Un archivo MAST comienza con un elemento **MAST** que contiene un elemento **triggers**.</span><span class="sxs-lookup"><span data-stu-id="e5328-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="e5328-208">El elemento <triggers> contiene uno o varios elementos **trigger** que definen cuándo se debe reproducir un anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-208">The <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="e5328-209">El elemento **trigger** contiene un elemento **startConditions** que especifica cuándo debe comenzar a reproducirse un anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-209">The **trigger** element contains a **startConditions** element which specify when an ad should begin to play.</span></span> <span data-ttu-id="e5328-210">El elemento **startConditions** contiene uno o varios elementos <condition>.</span><span class="sxs-lookup"><span data-stu-id="e5328-210">The **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="e5328-211">Cuando cada <condition> se evalúa como true, se inicia o se revoca un desencadenador en función de si <condition> está dentro de un elemento **startConditions** o **endConditions**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e5328-211">When each <condition> evaluates to true a trigger is initiated or revoked depending upon whether the <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="e5328-212">Cuando hay varios elementos <condition> presentes, se tratan como un OR implícito y cualquier condición que se evalúe como true hará que el desencadenador se inicie.</span><span class="sxs-lookup"><span data-stu-id="e5328-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating to true will cause the trigger to initiate.</span></span> <span data-ttu-id="e5328-213">Los elementos <condition> pueden estar anidados.</span><span class="sxs-lookup"><span data-stu-id="e5328-213"><condition> elements can be nested.</span></span> <span data-ttu-id="e5328-214">Cuando hay elementos <condition> secundarios predefinidos, se tratan como un AND implícito y todas las condiciones deben evaluarse como true para iniciar el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="e5328-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate to true for the trigger to initiate.</span></span> <span data-ttu-id="e5328-215">El elemento <condition> contiene los siguientes atributos que definen la condición:</span><span class="sxs-lookup"><span data-stu-id="e5328-215">The <condition> element contains the following attributes that define the condition:</span></span> 

1. <span data-ttu-id="e5328-216">**type** : especifica el tipo de condición, evento o propiedad.</span><span class="sxs-lookup"><span data-stu-id="e5328-216">**type** – specifies the type of condition, event or property</span></span>
2. <span data-ttu-id="e5328-217">**name** : nombre de la propiedad o evento que se usará durante la evaluación.</span><span class="sxs-lookup"><span data-stu-id="e5328-217">**name** – the name of the property or event to be used during evaluation</span></span>
3. <span data-ttu-id="e5328-218">**value** : valor de una propiedad con la que se evaluará.</span><span class="sxs-lookup"><span data-stu-id="e5328-218">**value** – the value that a property will be evaluated against</span></span>
4. <span data-ttu-id="e5328-219">**operator** : operación que se va a usar durante la evaluación: EQ (igual), NEQ (distinto), GTR (mayor que), GEQ (mayor o igual que), LT (menor que), LEQ (menor o igual que), MOD (módulo)</span><span class="sxs-lookup"><span data-stu-id="e5328-219">**operator** – the operation to use during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="e5328-220">**endConditions** también contiene elementos <condition>.</span><span class="sxs-lookup"><span data-stu-id="e5328-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="e5328-221">Cuando una condición se evalúa como true, el desencadenador se restablece. El elemento <trigger> también contiene un elemento <sources> que contiene uno o más elementos <source>.</span><span class="sxs-lookup"><span data-stu-id="e5328-221">When a condition evaluates to true the trigger is reset.The <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="e5328-222">Los elementos <source> definen el URI a la respuesta de anuncio y el tipo de respuesta de anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-222">The <source> elements define the URI to the ad response and the type of ad response.</span></span> <span data-ttu-id="e5328-223">En este ejemplo se proporciona un URI a una respuesta VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-223">In this example a URI is given to a VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="e5328-224">Uso de Video Player-Ad Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="e5328-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="e5328-225">VPAID es una API que permite a las unidades de anuncios ejecutables comunicarse con un reproductor de vídeo.</span><span class="sxs-lookup"><span data-stu-id="e5328-225">VPAID is an API for enabling executable ad units to communicate with a video player.</span></span> <span data-ttu-id="e5328-226">Esto permite disfrutar de experiencias de anuncios altamente interactivas.</span><span class="sxs-lookup"><span data-stu-id="e5328-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="e5328-227">El usuario puede interactuar con el anuncio y el anuncio puede responder a las acciones realizadas por el espectador.</span><span class="sxs-lookup"><span data-stu-id="e5328-227">The user can interact with the ad and the ad can respond to actions taken by the viewer.</span></span> <span data-ttu-id="e5328-228">Por ejemplo, un anuncio puede mostrar botones que permiten al usuario ver más información o una versión más larga del anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-228">For example an ad may display buttons that allow the user to view more information or a longer version of the ad.</span></span> <span data-ttu-id="e5328-229">El reproductor de vídeo debe admitir la API VPAID y el anuncio ejecutable debe implementar la API.</span><span class="sxs-lookup"><span data-stu-id="e5328-229">The video player must support the VPAID API and the executable ad must implement the API.</span></span> <span data-ttu-id="e5328-230">Cuando un reproductor solicita un anuncio de un servidor de anuncios, el servidor puede responder con una respuesta VAST que contiene un anuncio VPAID.</span><span class="sxs-lookup"><span data-stu-id="e5328-230">When a player requests an ad from an ad server the server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="e5328-231">Se crea un anuncio ejecutable en el código que debe ejecutarse en un entorno en tiempo de ejecución, como Adobe Flash ™ o JavaScript, que se pueden ejecutar en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="e5328-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="e5328-232">Cuando un servidor de anuncios devuelve una respuesta VAST que contiene un anuncio VPAID, el valor del atributo apiFramework en el elemento <MediaFile> debe ser "VPAID".</span><span class="sxs-lookup"><span data-stu-id="e5328-232">When an ad server returns a VAST response containing a VPAID ad, the value of the apiFramework attribute in the <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="e5328-233">Este atributo especifica que el anuncio contenido es un ejecutable VPAID.</span><span class="sxs-lookup"><span data-stu-id="e5328-233">This attribute specifies that the contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="e5328-234">El atributo type debe establecerse en el tipo MIME del ejecutable, por ejemplo, "application/x-shockwave-flash" o "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="e5328-234">The type attribute must be set to the MIME type of the executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="e5328-235">El siguiente fragmento XML muestra el elemento <MediaFile> de una respuesta VAST que contiene un anuncio ejecutable VPAID.</span><span class="sxs-lookup"><span data-stu-id="e5328-235">The following XML snippet shows the <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI to executable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="e5328-236">Un anuncio ejecutable se puede inicializar usando el elemento <AdParameters> dentro de los elementos <Linear> o <NonLinear> en una respuesta VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-236">An executable ad can be initialized using the <AdParameters> element within the <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="e5328-237">Para obtener más información sobre el elemento <AdParameters>, vea [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="e5328-237">For more information on the <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="e5328-238">Para obtener más información acerca de la API VPAID, consulte [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="e5328-238">For more information about the VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="e5328-239">Implementación de un reproductor de Windows o Windows Phone 8 con compatibilidad para anuncios</span><span class="sxs-lookup"><span data-stu-id="e5328-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="e5328-240">Microsoft Media Platform: Player Framework para Windows 8 y Windows Phone 8 contiene una colección de aplicaciones de ejemplo que muestran cómo implementar una aplicación de reproductor de vídeo usando el marco.</span><span class="sxs-lookup"><span data-stu-id="e5328-240">The Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="e5328-241">Puede descargar Player Framework y los ejemplos de [Player Framework para Windows 8 y Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="e5328-241">You can download the Player Framework and the samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="e5328-242">Cuando abra la solución Microsoft.PlayerFramework.Xaml.Samples, verá varias carpetas en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e5328-242">When you open the Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within the project.</span></span> <span data-ttu-id="e5328-243">La carpeta Advertising contiene el código de ejemplo correspondiente a la creación de un reproductor de vídeo con compatibilidad para anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-243">The Advertising folder contains the sample code relevant to creating a video player with ad support.</span></span> <span data-ttu-id="e5328-244">Dentro de la carpeta Advertising, hay varios archivos XAML/cs que muestran diferentes maneras de insertar anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-244">Inside the Advertising folder is a number of XAML/cs files each of which show how to insert ads in a different way.</span></span> <span data-ttu-id="e5328-245">La lista siguiente describe cada una de ellas:</span><span class="sxs-lookup"><span data-stu-id="e5328-245">The following list describes each:</span></span>

* <span data-ttu-id="e5328-246">AdPodPage.xaml: ilustra cómo mostrar un bloque de anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-246">AdPodPage.xaml Shows how to display an ad pod.</span></span>
* <span data-ttu-id="e5328-247">AdSchedulingPage.xaml: muestra cómo programar anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-247">AdSchedulingPage.xaml Shows how to schedule ads.</span></span>
* <span data-ttu-id="e5328-248">FreeWheelPage.xaml: muestra cómo usar el complemento FreeWheel para programar anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-248">FreeWheelPage.xaml Shows how to use the FreeWheel plugin to schedule ads.</span></span>
* <span data-ttu-id="e5328-249">MastPage.xaml: muestra cómo programar anuncios con un archivo MAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-249">MastPage.xaml Shows how to schedule ads with a MAST file.</span></span>
* <span data-ttu-id="e5328-250">ProgrammaticAdPage.xaml: muestra cómo programar anuncios en un vídeo mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e5328-250">ProgrammaticAdPage.xaml Shows how to programmatically schedule ads into a video.</span></span>
* <span data-ttu-id="e5328-251">ScheduleClipPage.xaml: muestra cómo programar un anuncio sin un archivo VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-251">ScheduleClipPage.xaml Shows how to schedule an ad without a VAST file.</span></span>
* <span data-ttu-id="e5328-252">VastLinearCompanionPage.xaml: muestra cómo insertar un anuncio lineal y uno complementario.</span><span class="sxs-lookup"><span data-stu-id="e5328-252">VastLinearCompanionPage.xaml Shows how to insert a linear and companion ad.</span></span>
* <span data-ttu-id="e5328-253">VastNonLinearPage.xaml: muestra cómo insertar un anuncio no lineal.</span><span class="sxs-lookup"><span data-stu-id="e5328-253">VastNonLinearPage.xaml Shows how to insert a non-linear ad.</span></span>
* <span data-ttu-id="e5328-254">VmapPage.xaml: muestra cómo especificar anuncios con un archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="e5328-254">VmapPage.xaml Shows how to specify ads with a VMAP file.</span></span>

<span data-ttu-id="e5328-255">Cada uno de estos ejemplos usa la clase MediaPlayer definida por el Player Framework.</span><span class="sxs-lookup"><span data-stu-id="e5328-255">Each of these samples uses the MediaPlayer class defined by the player framework.</span></span> <span data-ttu-id="e5328-256">En la mayoría de los ejemplos se usan complementos que agregan compatibilidad para varios formatos de respuesta de anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="e5328-257">El ejemplo ProgrammaticAdPage interactúa mediante programación con una instancia de MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="e5328-257">The ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="e5328-258">Ejemplo AdPodPage</span><span class="sxs-lookup"><span data-stu-id="e5328-258">AdPodPage Sample</span></span>
<span data-ttu-id="e5328-259">Este ejemplo usa el AdSchedulerPlugin para definir cuándo se debe mostrar un anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-259">This sample uses the AdSchedulerPlugin to define when to display an ad.</span></span> <span data-ttu-id="e5328-260">En este ejemplo, se programa un anuncio de cuña intermedia para que se reproduzca transcurridos cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="e5328-260">In this example a mid-roll advertisement is scheduled to be played after 5 seconds.</span></span> <span data-ttu-id="e5328-261">El bloque de anuncios (un grupo de anuncios que se muestran en orden) se especifica en un archivo VAST que se devuelve desde un servidor de anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-261">The ad pod (a group of ads to display in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="e5328-262">El URI del archivo VAST se especifica en el elemento <RemoteAdSource>.</span><span class="sxs-lookup"><span data-stu-id="e5328-262">The URI to the VAST file is specified in the <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="e5328-263">Para obtener más información acerca del AdSchedulerPlugin, consulte [Publicidad en Player Framework en Windows 8 y Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="e5328-263">For more information about the AdSchedulerPlugin, see [Advertising in the Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="e5328-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="e5328-264">AdSchedulingPage</span></span>
<span data-ttu-id="e5328-265">Este ejemplo también usa el AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="e5328-265">This sample also uses the AdSchedulerPlugin.</span></span> <span data-ttu-id="e5328-266">Programa tres anuncios, un anuncio de cuña previa, uno de cuña intermedia y uno de cuña posterior.</span><span class="sxs-lookup"><span data-stu-id="e5328-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="e5328-267">El URI del archivo VAST de cada anuncio se especifica en un elemento <RemoteAdSource>.</span><span class="sxs-lookup"><span data-stu-id="e5328-267">The URI to the VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="e5328-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="e5328-268">FreeWheelPage</span></span>
<span data-ttu-id="e5328-269">Este ejemplo usa FreeWheelPlugin, que especifica un atributo Source que especifica un URI que apunta a un archivo SmartXML que especifica el contenido del anuncio así como la información de programación.</span><span class="sxs-lookup"><span data-stu-id="e5328-269">This sample uses the FreeWheelPlugin which specifies a Source attribute that specifies a URI that points to a SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="e5328-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="e5328-270">MastPage</span></span>
<span data-ttu-id="e5328-271">Este ejemplo usa el MastSchedulerPlugin, que permite usar un archivo MAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-271">This sample uses the MastSchedulerPlugin that allows you to use a MAST file.</span></span> <span data-ttu-id="e5328-272">El atributo Source especifica la ubicación del archivo MAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-272">The Source attribute specifies the location of the MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="e5328-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="e5328-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="e5328-274">Este ejemplo interactúa mediante programación con MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="e5328-274">This sample programmatically interacts with the MediaPlayer.</span></span> <span data-ttu-id="e5328-275">El archivo ProgrammaticAdPage.xaml crea una instancia de MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="e5328-275">The ProgrammaticAdPage.xaml file instantiates the MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="e5328-276">El archivo ProgrammaticAdPage.xaml.cs crea un AdHandlerPlugin, agrega un TimelineMarker para especificar cuándo se debe mostrar un anuncio y, después, agrega un controlador para el evento MarkerReached que carga un RemoteAdSource que especifica el URI de un archivo VAST y, después, reproduce el anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-276">The ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker to specify when an ad should be displayed, and then adds a handler for the MarkerReached event which loads a RemoteAdSource specifying a URI to a VAST file, and then plays the ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="e5328-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="e5328-277">ScheduleClipPage</span></span>
<span data-ttu-id="e5328-278">Este ejemplo usa el AdSchedulerPlugin para programar un anuncio de cuña intermedia especificando un archivo .wmv que contiene el anuncio.</span><span class="sxs-lookup"><span data-stu-id="e5328-278">This sample uses the AdSchedulerPlugin to schedule a mid-roll ad by specifying a .wmv file that contains the ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="e5328-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="e5328-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="e5328-280">Este ejemplo muestra cómo usar el AdSchedulerPlugin para programar un anuncio lineal de cuña intermedia con un anuncio complementario.</span><span class="sxs-lookup"><span data-stu-id="e5328-280">This sample illustrates how to use the AdSchedulerPlugin to schedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="e5328-281">El elemento <RemoteAdSource> especifica la ubicación del archivo VAST.</span><span class="sxs-lookup"><span data-stu-id="e5328-281">The <RemoteAdSource> element specifies the location of the VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="e5328-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="e5328-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="e5328-283">Este ejemplo usa el AdSchedulerPlugin para programar un anuncio lineal y uno no lineal.</span><span class="sxs-lookup"><span data-stu-id="e5328-283">This sample uses the AdSchedulerPlugin to schedule a linear and a non-linear ad.</span></span> <span data-ttu-id="e5328-284">La ubicación del archivo VAST se especifica con el elemento <RemoteAdSource>.</span><span class="sxs-lookup"><span data-stu-id="e5328-284">The VAST file location is specified with the <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="e5328-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="e5328-285">VMAPPage</span></span>
<span data-ttu-id="e5328-286">Los ejemplos usan el VmapSchedulerPlugin para programar anuncios con un archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="e5328-286">This samples uses the VmapSchedulerPlugin to schedule ads using a VMAP file.</span></span> <span data-ttu-id="e5328-287">El URI del archivo VMAP se especifica en el atributo Source del elemento <VmapSchedulerPlugin>.</span><span class="sxs-lookup"><span data-stu-id="e5328-287">The URI to the VMAP file is specified in the Source attribute of the <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="e5328-288">Implementación de un reproductor de vídeo de iOS con compatibilidad para anuncios</span><span class="sxs-lookup"><span data-stu-id="e5328-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="e5328-289">Microsoft Media Platform: Player Framework para iOS contiene una colección de aplicaciones de ejemplo que muestran cómo implementar una aplicación de reproductor de vídeo usando el marco.</span><span class="sxs-lookup"><span data-stu-id="e5328-289">The Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="e5328-290">Puede descargar el Reproductor multimedia y los ejemplos del [Marco de trabajo del Reproductor multimedia de Azure](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="e5328-290">You can download the Player Framework and the samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="e5328-291">La página de Github incluye un vínculo a un wiki que contiene información adicional sobre el Reproductor multimedia y una introducción al ejemplo del reproductor: [Wiki del Reproductor multimedia de Azure](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="e5328-291">The github page has a link to a Wiki that contains additional information on the player framework and an introduction to the player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="e5328-292">Programación de anuncios con VMAP</span><span class="sxs-lookup"><span data-stu-id="e5328-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="e5328-293">El ejemplo siguiente muestra cómo programar anuncios usando un archivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="e5328-293">The following example shows how to schedule ads using a VMAP file.</span></span>

    // How to schedule an Ad using VMAP.
    //First download the VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using the downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="e5328-294">Programación de anuncios con VAST</span><span class="sxs-lookup"><span data-stu-id="e5328-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="e5328-295">El ejemplo siguiente muestra cómo programar un anuncio VAST de enlace en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e5328-295">The following sample shows how to schedule a late binding VAST ad.</span></span>

    //Example:3 How to schedule a late binding VAST ad.
    // set the start time for the ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify the URI of the VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL to VAST file
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

   <span data-ttu-id="e5328-296">El ejemplo siguiente muestra cómo programar un anuncio VAST de enlace anticipado.</span><span class="sxs-lookup"><span data-stu-id="e5328-296">The following sample shows how to schedule an early binding VAST ad.</span></span>
<span data-ttu-id="e5328-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="e5328-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="e5328-298">El ejemplo siguiente muestra cómo insertar un anuncio usando RCE (edición tentativa)</span><span class="sxs-lookup"><span data-stu-id="e5328-298">The following sample shows how to insert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How to use RCE.
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

<span data-ttu-id="e5328-299">El ejemplo siguiente muestra cómo programar un bloque de anuncios.</span><span class="sxs-lookup"><span data-stu-id="e5328-299">The following example shows how to schedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL to content
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI to ad content
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

<span data-ttu-id="e5328-300">El ejemplo siguiente muestra cómo programar una cuña intermedia no estática.</span><span class="sxs-lookup"><span data-stu-id="e5328-300">The following example shows how to schedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="e5328-301">Un anuncio no estático solo se reproduce una vez independientemente de la búsqueda que realice el espectador.</span><span class="sxs-lookup"><span data-stu-id="e5328-301">A non-sticky ad is only played once regardless of any seeking the viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL to content
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

<span data-ttu-id="e5328-302">El ejemplo siguiente muestra cómo programar una cuña intermedia estática.</span><span class="sxs-lookup"><span data-stu-id="e5328-302">The following example shows how to schedule a sticky mid-roll ad.</span></span> <span data-ttu-id="e5328-303">Un anuncio estático se mostrará cada vez que se alcanza el punto especificado en la escala de tiempo del vídeo.</span><span class="sxs-lookup"><span data-stu-id="e5328-303">A sticky ad will be displayed each time the specified point on the video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI to ad
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


<span data-ttu-id="e5328-304">El ejemplo siguiente muestra cómo programar un anuncio de cuña posterior.</span><span class="sxs-lookup"><span data-stu-id="e5328-304">The following sample shows how to schedule a post-roll ad.</span></span>

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

<span data-ttu-id="e5328-305">El ejemplo siguiente muestra cómo programar un anuncio de cuña anterior.</span><span class="sxs-lookup"><span data-stu-id="e5328-305">The following sample shows how to schedule a pre-roll ad.</span></span>

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

<span data-ttu-id="e5328-306">El ejemplo siguiente muestra cómo programar un anuncio superpuesto de cuña intermedia.</span><span class="sxs-lookup"><span data-stu-id="e5328-306">The following sample shows how to schedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="e5328-307">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="e5328-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e5328-308">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="e5328-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e5328-309">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e5328-309">See Also</span></span>
[<span data-ttu-id="e5328-310">Desarrollo de aplicaciones para reproductor de vídeo</span><span class="sxs-lookup"><span data-stu-id="e5328-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

