---
title: "aplicaciones de Reproductor de vídeo aaaDevelop"
description: "Hola tema proporcionan vínculos tooPlayer marcos y complementos que puede usar toodevelop sus propias aplicaciones de cliente que puedan consumir contenido multimedia de transmisión por secuencias de servicios multimedia."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Desarrollo de aplicaciones para reproductor de vídeo
## <a name="overview"></a>Información general
Servicios multimedia de Azure proporciona hello las herramientas necesita toocreate enriquecido, aplicaciones de reproducción de cliente dinámico para la mayoría de las plataformas incluidas: dispositivos con iOS, dispositivos Android, Windows, Windows Phone, Xbox y Set-top cuadros. En este tema también proporciona vínculos tooSDKs y marcos de Reproductor puede usar toodevelop en sus propias aplicaciones de cliente que puedan consumir contenido multimedia de transmisión por secuencias de servicios multimedia de Azure.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 
 
## <a name="azure-media-player"></a>Reproductor multimedia de Azure
[El Reproductor de Media Azure](http://aka.ms/ampinfo) un Reproductor de vídeo web depende de la tooplay medios back-contenidos de servicios multimedia de Microsoft Azure una gran variedad de exploradores y dispositivos. El Reproductor de Media Azure emplea estándares del sector, como HTML5, Media Source Extensions (MSE) y las extensiones de medios de cifrado (EME) tooprovide una experiencia de transmisión por secuencias adaptativa enriquecida. Cuando estos estándares no están disponibles en un dispositivo o en un explorador, el Reproductor multimedia de Azure usa Flash y Silverlight como tecnología de reserva. Independientemente de la tecnología de reproducción de hello usa, los desarrolladores tendrán un tooaccess de interfaz de JavaScript API unificada. Esto permite contenido atendido por toobe de servicios multimedia de Azure que se reproduce a través de una amplia gama de dispositivos y exploradores sin ningún esfuerzo adicional.

Servicios de multimedia de Microsoft Azure permite contenido toobe servida con DASH, Smooth Streaming y HLS tooplay formatos de streaming nuevo contenido. El Reproductor multimedia de Azure tiene en cuenta estos diversos formatos y automáticamente desempeña Hola vínculo recomendado en función de las capacidades del explorador de plataforma/hello. Servicios multimedia de Microsoft Azure también permite el cifrado dinámico de recursos con el cifrado PlayReady o el cifrado de sellado de AES de 128 bits. Reproductor multimedia de Azure permite el descifrado del contenido cifrado de AES de 128 bits y PlayReady cuando se configura correctamente. 

Para obtener más información:

* [Reproductor multimedia de Azure](http://aka.ms/ampinfo)
* [Documentación de Reproductor multimedia de Azure](http://aka.ms/ampdocs) 
* [Blog de Introducción a Reproductor multimedia de Azure](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Suscríbase toostay una toodate con hello más reciente del Reproductor de multimedia de Azure](http://aka.ms/ampsignup)
* [Agregue nuevas solicitudes, ideas, comentarios](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Otras herramientas para crear aplicaciones del reproductor
También puede usar cualquiera de hello siguientes SDK:

* [SDK de cliente de Smooth Streaming](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Aplicación de la Tienda Windows de Smooth Streaming](media-services-build-smooth-streaming-apps.md)
* [Plataforma multimedia de Microsoft: Player Framework](http://playerframework.codeplex.com/) 
* [Documentación de HTML5 Player Framework](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Complemento Microsoft Smooth Streaming para OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licencias de kit de migración de cliente de Microsoft® Smooth Streaming](http://aka.ms/sspk) 
* [Desarrollo de aplicaciones de vídeo de XBOX](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Publicidad
Servicios multimedia de Azure proporciona compatibilidad para la inserción de anuncios a través de hello plataforma de Windows Media: marcos del Reproductor. Player framework con compatibilidad con anuncios está disponible para dispositivos Windows 8, Silverlight, Windows Phone 8 e iOS. Cada marco para Reproductor contiene código de ejemplo que muestra cómo tooimplement una aplicación de reproducción. Hay tres tipos diferentes de anuncios que se pueden insertar en el archivo multimedia:

Lineales: anuncios en un marco completo que pausan el vídeo principal Hola

No lineales: anuncios superpuestos que se muestran cuando se está reproduciendo el vídeo principal hello, normalmente un logotipo u otra imagen estática colocada dentro de Reproductor de Hola

Complementarios: anuncios que aparecen fuera de Reproductor de Hola

Anuncios se pueden colocar en cualquier punto de la escala temporal del vídeo principal Hola. Debe indicar que el Reproductor de hello cuando tooplay Hola ad y que tooplay de anuncios. Esto se realiza con un conjunto de archivos XML estándar: Video Ad Service Template (VAST, plantilla de servicio de anuncio de vídeo), Digital Video Multiple Ad Playlist (VMAP, lista de reproducción de varios anuncios de vídeo digital), Media Abstract Sequencing Template (MAST, plantilla de secuenciación abstracta multimedia) y Digital Video Player Ad Interface Definition (VPAID, definición de interfaz de anuncios del reproductor de vídeo digital). Los archivos VAST especifican qué toodisplay de anuncios. Archivos VMAP especifican cuándo tooplay varios anuncios y contienen XML VAST. Los archivos MAST constituyen otra anuncios de toosequence de manera que también pueden contener XML VAST. Los archivos VPAID definen una interfaz entre el Reproductor de vídeo de Hola y anuncios de Hola o el servidor de anuncios. Para obtener más información, vea [Inserción de anuncios](https://msdn.microsoft.com/library/dn387398.aspx).

Para obtener información sobre la compatibilidad con anuncios y subtítulos en vídeos de streaming en vivo, vea [Estándares de inserción de anuncios y subtítulos compatibles](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Incrustación de un vídeo de transmisión por secuencias adaptativa MPEG-DASH en una aplicación HTML5 con DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[Repositorio dash.js de GitHub](https://github.com/Dash-Industry-Forum/dash.js)

