---
title: aaaUsing castLabs toodeliver Widevine licencias de servicios de multimedia de tooAzure | Documentos de Microsoft
description: "Este artículo describe cómo puede usar servicios de multimedia de Azure (AMS) toodeliver una secuencia que se cifra dinámicamente por AMS con PlayReady y Widevine DRMs. licencia de PlayReady Hola procede del servidor de licencias de PlayReady de servicios multimedia y licencias de Widevine enviada por el servidor de licencias de castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>Uso de tooAzure de licencias de Widevine castLabs toodeliver servicios multimedia
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Información general
Este artículo describe cómo puede usar servicios de multimedia de Azure (AMS) toodeliver una secuencia que se cifra dinámicamente por AMS con PlayReady y Widevine DRMs. licencia de PlayReady Hola procede del servidor de licencias de PlayReady de servicios multimedia y licencias de Widevine enviada por **castLabs** servidor de licencias.

tooplayback transmisión por secuencias el contenido protegido por CENC (PlayReady o Widevine), puede usar [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Consulte el [documento AMP](http://amp.azure.net/libs/amp/latest/docs/) para obtener información detallada.

Hola siguiente diagrama muestra una arquitectura de integración de servicios multimedia de Azure y castLabs alto nivel.

![integración](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Configuración de sistema típico
* El contenido multimedia se almacena en AMS.
* Los id. de clave de claves de contenido se almacenan en castLabs y AMS.
* Tanto castLabs como AMS tienen la autenticación de tokens integrada. Hola siguientes secciones describe los tokens de autenticación. 
* Cuando un cliente solicita el vídeo de hello toostream, contenido de hello dinámicamente se cifran con **cifrado común** (CENC) y empaquetar AMS tooSmooth dinámicamente la transmisión por secuencias y el guión. También ofrecemos cifrado de streaming elemental de PlayReady M2TS para el protocolo de streaming HLS.
* La licencia de PlayReady se recupera del servidor de licencias de AMS y la licencia de Widevine se recupera del servidor de licencias de castLabs. 
* El Reproductor de Media automáticamente decide qué toofetch de licencia en función de la capacidad de la plataforma cliente Hola. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Generación de tokens de autenticación para obtener una licencia
CastLabs y AMS admite JWT (JSON Web Token) tooauthorize de formato de token usa una licencia. 

### <a name="jwt-token-in-ams"></a>Token JWT en AMS
Hello en la tabla siguiente describe los tokens JWT en AMS. 

| Emisor | Cadena de emisor de hello elegido el servicio de Token seguro (STS) |
| --- | --- |
| Público |Cadena de audiencia de hello usa STS |
| Notificaciones |Un conjunto de notificaciones |
| NotBefore |Iniciar la validez del token de Hola |
| Expira |Final de validez del token de Hola |
| SigningCredentials |clave de Hola que se comparte entre el servidor de licencias de PlayReady, castLabs servidor de licencias y STS, podría ser clave simétrica o asimétrica. |

### <a name="jwt-token-in-castlabs"></a>Token JWT en castLabs
Hello en la tabla siguiente describe el token JWT en castLabs. 

| Nombre | Description |
| --- | --- |
| optData |Cadena JSON que contiene información sobre el usuario. |
| crt |Un JSON cadena que contiene información sobre activos hello, sus derechos de reproducción y la información de licencia. |
| iat |Hola datetime actual en tiempo. |
| jti |Un identificador único sobre este token (cada token sólo puede utilizarse una vez en el sistema de hello castLabs). |

## <a name="sample-solution-set-up"></a>Configuración de soluciones de ejemplo
Hola [solución de ejemplo](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consta de dos proyectos:

* Una aplicación de consola que puede ser utilizados tooset DRM restricciones en un activo ya integrado, para PlayReady y Widevine.
* Una aplicación web que distribuye tokens, que podrían considerarse como una versión MUY SIMPLIFICADA de un STS.

aplicación de consola de Hola toouse:

1. Cambiar las credenciales de hello app.config toosetup AMS, castLabs credenciales, configuración de STS y una clave compartida.
2. Cargue un activo en AMS.
3. Get hello UUID de hello cargado activo y cambia 32 de línea en el archivo Program.cs de hello:
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Aplique un AssetId de activos de hello en sistema de hello castLabs (44 de línea en el archivo Program.cs de hello).
   
   Debe establecer AssetId para **castLabs**; debe toobe una cadena alfanumérica única.
5. Ejecutar programa Hola.

Hola toouse aplicación Web (STS):

1. Toosetup castlabs comerciante de cambio Hola web.config Id., configuración de STS de Hola y Hola una clave compartida.
2. Implementar tooAzure sitios Web.
3. Explorar el sitio Web de toohello.

## <a name="playing-back-a-video"></a>Reproducir un vídeo
tooplayback un vídeo cifrada con cifrado común (PlayReady o Widevine), puede usar hello [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Cuando se ejecuta la aplicación de consola de hello, se reflejan el identificador de clave de contenido de Hola y Hola dirección URL del manifiesto.

1. Abra una nueva pestaña e inicie STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].
2. Vaya demasiado[Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Pegue en hello transmisión por secuencias de dirección URL.
4. Haga clic en hello **opciones avanzadas** casilla de verificación.
5. Hola **protección** lista desplegable, seleccione PlayReady o Widevine.
6. Pegue el token de Hola que obtuvo en los STS en el cuadro de texto de hello símbolo (token). 
   
   no es necesario el servidor de licencias de castLab de Hola Hola "portador =" prefijo delante del símbolo (token) de Hola. Así que quite antes de enviar el token de Hola.
7. Actualizar el Reproductor de Hola.
8. Hola vídeo debe ser reproducción en curso.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

