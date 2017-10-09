---
title: aaaUse existente reproductores tooplayback su contenido, Azure | Documentos de Microsoft
description: Este tema enumeran los reproductores existentes que puede usar tooplayback su contenido.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>Reproducción de contenido con existentes
Servicios multimedia de Azure admite muchos formatos de streaming populares como Smooth Streaming, HTTP Live Streaming y MPEG-Dash. Este tema remite reproductores tooexisting que se pueden usar tootest sus secuencias.

### <a name="hello-azure-portal-media-services-content-player"></a>Reproductor de contenido de Hello Azure portal de servicios multimedia
Hola **Azure** portal proporciona un Reproductor de contenido que se puede usar tootest el vídeo.

Haga clic en hello deseado vídeo (asegúrese de que era [publicado](media-services-portal-publish.md)) y haga clic en hello **reproducir** situado en parte inferior de hello del portal de Hola.

Se aplican algunas consideraciones:

* Hola **Reproductor de contenido de servicios multimedia** reproduce desde predeterminado Hola extremo de streaming. Si desea tooplay desde un extremo de streaming no predeterminado, utilice otro reproductor. Por ejemplo, [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Reproductor multimedia de Azure
Use [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback su contenido (protegido o desactive) en cualquiera de hello siguientes formatos:

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progresivo

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Cifrado de AES con token
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Reproductores de Silverlight
#### <a name="monitoring"></a>Supervisión
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady con token
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Reproductores DASH
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Otros
tootest HLS, las direcciones URL también puede usar:

* **Safari** en un dispositivo iOS o
* **3ivx HLS Player** en Windows.

## <a name="developing-video-players"></a>Desarrollo de reproductores de vídeo
Para obtener información sobre cómo toodevelop sus propios reproductores, vea [desarrollar reproductores de vídeo](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
