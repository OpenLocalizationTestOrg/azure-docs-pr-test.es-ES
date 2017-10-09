---
title: aaaProtect su contenido con servicios multimedia de Azure | Documentos de Microsoft
description: "En este artículo se ofrece información general de protección de contenido con Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Información general de protección del contenido
Servicios de multimedia de Microsoft Azure permite toosecure su media de tiempo de hello sale del equipo a través de almacenamiento, procesamiento y entrega. Servicios multimedia permite toodeliver su contenido en directo y a petición cifrado dinámicamente con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits) o cualquiera de Hola DRMs principales: Microsoft PlayReady, Google Widevine y FairPlay de Apple. Servicios multimedia también proporciona un servicio de entrega de claves de AES y licencias de DRM (PlayReady, Widevine y FairPlay) tooauthorized clientes. 

Hola siguiente imagen muestra los flujos de trabajo de protección de contenido de Hola que admita AMS. 

![Protección con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

Este tema se explica [conceptos y terminología](media-services-content-protection-overview.md) protección del contenido relevante toounderstanding con AMS. Hola tema también contiene [vínculos](media-services-content-protection-overview.md#common-scenarios) tootopics que muestran cómo tooachieve tareas de protección de contenido. 

## <a name="dynamic-encryption"></a>Cifrado dinámico
Servicios de multimedia de Microsoft Azure le permite toodeliver su contenido dinámicamente cifra con clave sin cifrado de AES o el cifrado de DRM: Microsoft PlayReady, Google Widevine y FairPlay de Apple.

Actualmente, puede cifrar los siguientes formatos de streaming de Hola: HLS, MPEG DASH y Smooth Streaming. No se pueden cifrar las descargas progresivas.

Si desea para servicios multimedia tooencrypt un recurso, es necesario tooassociate una clave de cifrado (CommonEncryption o EnvelopeEncryption) con el recurso y configurar directivas de autorización para la clave de Hola.

También necesita directiva de entrega del activo de tooconfigure Hola. Si desea toostream un recurso cifrado de almacenamiento, asegúrese de toospecify seguro de cómo desea toodeliver, mediante la configuración de directiva de entrega de activos.

Cuando un Reproductor solicita una secuencia, los servicios multimedia usa Hola especificado toodynamically clave cifrar su contenido mediante la clave sin cifrado de AES o cifrado de DRM. secuencia de hello toodecrypt, Hola Reproductor solicitará clave Hola del servicio de entrega de claves de Hola. toodecide si es usuario de hello autorizado tooget clave de hello, servicio de hello evalúa las directivas de autorización de Hola que especificó para la clave de Hola.


## <a name="storage-encryption"></a>Cifrado de almacenamiento
Usar almacenamiento cifrado tooencrypt el contenido no localmente mediante cifrado AES de 256 bits y, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo. Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo. caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure sitúe los archivos multimedia de entrada de gran calidad con cifrado de alta seguridad en disco.

En orden toodeliver un recurso cifrado de almacenamiento, debe configurar Directiva de entrega del activo de Hola para que Servicios multimedia sepa cómo desea toodeliver su contenido. Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega (por ejemplo, AES, cifrado común o sin cifrado).

## <a name="common-encryption-cenc"></a>Cifrado común (CENC)
El cifrado común se utiliza al cifrar el contenido con PlayReady o Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Uso del cifrado cbcs-aapl
Cbcs-aapl se usa al cifrar el contenido con FairPlay.

## <a name="envelope-encryption"></a>Cifrado de sobre
Utilice esta opción si desea que tooprotect su contenido con la clave sin cifrado AES-128. Si desea una opción más segura, elija uno de hello DRMs enumerados en este tema. 

## <a name="licenses-and-keys-delivery-service"></a>Servicio de entrega de licencias y claves
Servicios multimedia proporciona un servicio para entregar licencias de DRM (PlayReady, Widevine, FairPlay) y los clientes de tooauthorized de claves sin cifrado AES. Puede usar [Hola portal de Azure](media-services-portal-protect-content.md), API de REST o el SDK de servicios multimedia para las directivas de autenticación y autorización del tooconfigure de .NET para las licencias y las claves.

## <a name="token-restriction"></a>Restricción de token
Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: abrir o símbolo (token) de restricción. directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS). Servicios multimedia admite tokens con formato Simple Web Tokens (SWT) de Hola y el formato de JSON Web Token (JWT). Los Servicios multimedia no proporcionan Servicios de tokens seguros. Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue. Hola STS debe estar configurado toocreate un token firmado con hello especificado clave y emitir notificaciones que especificó en la configuración de restricción de token de Hola. Servicios de multimedia de Hello servicio de entrega de claves devolverá Hola solicitado Hola y cliente de toohello (o licencias) de la clave si Hola token es válido notificaciones Hola token coinciden con las configuradas para las claves de hello (o licencias).

Al configurar la directiva restringida de tokens de hello, debe especificar la clave de verificación principal hello, emisor y parámetros de audiencia. clave de verificación principal Hello contiene Hola clave que Hola token se firmó con, el emisor es Hola servicio de token seguro que emite el token de Hola. audiencia de Hello (a veces denominado ámbito) describe intención de hello del token de Hola u Hola recursos Hola token autoriza acceso. Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola.

## <a name="streaming-urls"></a>Direcciones URL de streaming
Si el recurso se cifró con DRM de más de una, debe usar una etiqueta de cifrado en hello transmisión por secuencias de dirección URL: (formato = 'm3u8-aapl' cifrado = 'xxx').

Hola siguientes consideraciones se aplica:

* Se puede especificar solo un tipo de cifrado o ninguno.
* Tipo de cifrado no tiene toobe especificado en dirección url de hello si solo un cifrado estaba activo toohello aplicada.
* El tipo de cifrado distingue mayúsculas de minúsculas.
* Hola siguientes tipos de cifrado se puede especificar:  
  * **cenc**: cifrado común (Playready o Widevine)
  * **cbcs-aapl**: Fairplay
  * **cbc**: cifrado de sobre AES.

## <a name="common-scenarios"></a>Escenarios comunes
Hello en los temas siguientes se muestran cómo tooprotect contenido en el almacenamiento, proporcionar cifrado dinámicamente la transmisión por secuencias multimedia, usar el servicio de entrega de clave y licencia de AMS

* [Protección con AES](media-services-protect-with-aes128.md) 
* [Protección con PlayReady y/o Widevine ](media-services-protect-with-drm.md)
* [Transmisión de contenido HLS protegido con Apple FairPlay o PlayReady](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Otros escenarios
* [Cómo service toointegrate licencia de PlayReady de Azure con su propio servidor de sistema de cifrado/transmisión](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [Uso de tooAzure de licencias DRM castLabs toodeliver servicios multimedia](media-services-castlabs-integration.md)

>[!NOTE]
>Un escenario en el que usa un servidor DRM externo (tecnología) y flujo de AMS no se admite actualmente.


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Anuncio de PlayReady como servicio y cifrado dinámico AES con Servicios multimedia de Azure](http://mingfeiy.com/playready)

[Explicación del precio de la entrega de licencia de PlayReady de Servicios multimedia de Azure](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[¿Cómo toodebug para AES cifrada flujo en servicios multimedia de Azure](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Autenticación de token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Integración de la aplicación OWIN basada en MVC de Servicios multimedia de Azure con Azure Active Directory y restricción de la entrega de claves de contenido basada en notificaciones de JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Usar tokens de ACS de Azure tooissue](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
