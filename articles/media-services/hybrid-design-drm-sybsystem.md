---
title: "diseño de aaaHybrid de subsistemas DRM con servicios multimedia de Azure | Documentos de Microsoft"
description: "En este tema se describe el diseño híbrido de subsistemas DRM con Azure Media Services."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>Diseño híbrido de subsistemas DRM

En este tema se describe el diseño híbrido de subsistemas DRM con Azure Media Services.

## <a name="overview"></a>Información general

Servicios multimedia de Azure proporciona compatibilidad para hello después de tres sistema DRM:

* PlayReady
* Widevine (Modular)
* FairPlay

compatibilidad con DRM de Hello incluye cifrado de DRM (cifrado dinámico) y la entrega de licencia, con el Reproductor de Media de Azure admite todos los 3 DRMs como un Reproductor de explorador SDK.

Para obtener un tratamiento detallado de DRM/CENC subsistema diseño e implementación, vea documento Hola titulado [CENC con DRM de múltiples y Control de acceso](media-services-cenc-with-multidrm-access-control.md).

Aunque se ofrece compatibilidad total con tres sistemas DRM, en ocasiones, los clientes necesitan toouse distintas partes de sus propia infraestructura/subsistemas suma tooAzure servicios multimedia toobuild un subsistema DRM híbrido.

A continuación se incluyen algunas preguntas comunes planteadas por los clientes:

* "¿Puedo usar mis propio servidores de licencias DRM?" (En este caso, los clientes han invertido en una granja de servidores de licencias DRM con lógica de negocios insertada).
* "¿Puedo usar únicamente la entrega de licencias DRM en Azure Media Services sin hospedar contenido de AMS?"

## <a name="modularity-of-hello-ams-drm-platform"></a>Modularidad de hello plataforma DRM AMS

Como parte de una plataforma integral de vídeo en la nube, DRM de Azure Media Services tiene en mente un diseño flexible modular. Puede usar los servicios multimedia de Azure con cualquiera de hello siguiendo diferentes combinaciones descritas en tabla de hello siguiente (después de obtener una explicación de la notación de Hola que se utiliza en la tabla de Hola). 

|**Hospedaje y origen del contenido**|**Cifrado de contenido**|**Entrega de licencia DRM**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|Aplicaciones de terceros|
|AMS|Aplicaciones de terceros|AMS|
|AMS|Aplicaciones de terceros|Aplicaciones de terceros|
|Aplicaciones de terceros|Aplicaciones de terceros|AMS|

### <a name="content-hosting--origin"></a>Hospedaje y origen del contenido

* AMS: el recurso de vídeo se hospeda en AMS y el streaming se realiza a través de puntos de conexión de streaming de AMS (pero no necesariamente de empaquetado dinámico).
* Aplicaciones de terceros: el vídeo se hospeda y se entrega en una plataforma de streaming de terceros fuera AMS.

### <a name="content-encryption"></a>Cifrado de contenido

* AMS: el cifrado de contenido se realiza de forma dinámica o a petición mediante cifrado dinámico de AMS.
* Aplicaciones de terceros: el cifrado de contenido se realiza fuera de AMS mediante un flujo de trabajo previo al procesamiento.

### <a name="drm-license-delivery"></a>Entrega de licencias DRM

* AMS: el servicio de entrega de licencias de AMS entrega la licencia DRM.
* Aplicaciones de terceros: la licencia DRM se entrega mediante un servidor de licencias DRM de terceros fuera de AMS.

## <a name="configure-based-on-your-hybrid-scenario"></a>Configuración en función del escenario híbrido

### <a name="content-key"></a>Clave de contenido

Configuración de una clave de contenido, puede controlar Hola siguientes atributos de cifrado dinámico AMS y servicio de entrega de licencia de AMS:

* clave de contenido Hola usado para el cifrado dinámico de DRM.
* Toobe contenido de licencias DRM entregado por servicios de entrega de licencia: derechos, clave de contenido y las restricciones.
* Tipo de **restricción de la directiva de autorización de claves de contenido**: abierta, IP o restricción de token.
* Si **token** tipo de **se utiliza la restricción de la directiva de autorización de clave de contenido**, hello **restricción de la directiva de autorización de claves de contenido** deben cumplirse antes de que se emite una licencia.

### <a name="asset-delivery-policy"></a>Directiva de entrega de recursos

A través de la configuración de una directiva de entrega del activo, puede controlar Hola siguiendo los atributos utilizados por la funcionalidad de paquetes dinámico AMS y cifrado dinámico de un extremo de streaming de AMS:

* Combinación de protocolo de streaming y cifrado de DRM, como DASH en CENC (PlayReady y Widevine), Smooth Streaming en PlayReady, HLS en Widevine o PlayReady.
* Hola predeterminado/incrustado licencia entrega las direcciones URL para cada uno de hello implicados DRMs.
* Si las direcciones URL de adquisición de licencia (LA_URL) en DASH MPD o la lista de reproducción de HLS contienen la cadena de consulta del identificador de clave (KID) para Widevine y FairPlay, respectivamente.

## <a name="scenarios-and-samples"></a>Escenarios y ejemplos

Según explicaciones de hello en la sección anterior de hello, use respectivos Hola siguiendo cinco escenarios híbridos **clave de contenido**-**directiva de entrega activo** combinaciones de configuración (Hola ejemplos mencionados en la última columna de hello siguen tabla hello):

|**Hospedaje y origen del contenido**|**Cifrado de DRM**|**Entrega de licencia DRM**|**Configurar la clave de contenido**|**Configuración de directivas de entrega de activos**|**Ejemplo**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|Sí|Sí|Ejemplo 1|
|AMS|AMS|Aplicaciones de terceros|Sí|Sí|Ejemplo 2|
|AMS|Aplicaciones de terceros|AMS|Sí|No|Ejemplo 3|
|AMS|Aplicaciones de terceros|Externo|No|No|Ejemplo 4|
|Aplicaciones de terceros|Aplicaciones de terceros|AMS|Sí|No|    

En los ejemplos de hello, funciona la protección de PlayReady para DASH y smooth streaming. Hola vídeo las direcciones URL siguientes son smooth streaming las direcciones URL. tooget Hola correspondientes direcciones URL de guión, simplemente anexar "(formato = mpd: tiempo-csf)". Puede usar hello [multimedia de azure probar Reproductor](http://aka.ms/amtest) tootest en un explorador. Le permite tooconfigure que toouse de protocolo, en qué tecnología de transmisión por secuencias. IE11 y MS Edge en Windows 10 admiten PlayReady a través de EME. Para obtener más información, consulte [detalles sobre Hola probar herramienta](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).

### <a name="sample-1"></a>Ejemplo 1

* Dirección URL (base) de origen: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* LA_URL de PlayReady (DASH y Smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* LA_URL de Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* LA_URL de FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>Ejemplo 2

* Dirección URL (base) de origen: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* LA_URL de PlayReady (DASH y Smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>Ejemplo 3

* Dirección URL de origen: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* LA_URL de PlayReady (DASH y Smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>Ejemplo 4

* Dirección URL de origen: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* LA_URL de PlayReady (DASH y smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>Resumen

En resumen, los componentes DRM de Azure Media Services son flexibles y se pueden usar en un escenario híbrido mediante la configuración correcta de la clave de contenido y la directiva de entrega de activos, como se describe en este tema.

## <a name="next-steps"></a>Pasos siguientes
Ver las rutas de aprendizaje de Media Services

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

