---
title: "uso de directivas de autorización de clave de contenido de aaaConfigure Hola portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure una directiva de autorización para una clave de contenido."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Configuración de la directiva de autorización de claves de contenido
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Información general
Servicios de multimedia de Microsoft Azure le permite toodeliver MPEG-DASH, Smooth Streaming y secuencias de HTTP-Live-Streaming (HLS) protegidas con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits) o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS también permite toodeliver guión streams cifrado con Widevine DRM. PlayReady y Widevine se cifran por hello especificación de cifrado común (ISO/IEC 23001-7 CENC).

Servicios multimedia también ofrecen una **servicio de entrega de clave/licencia** de que los clientes pueden obtener claves de AES o tooplay de licencias de PlayReady/Widevine Hola contenido cifrado.

Este tema muestra cómo toouse Hola directiva de autorización de clave de contenido de hello tooconfigure de portal de Azure. se pueden utilizar posteriormente clave Hello toodynamically cifrar el contenido. Tenga en cuenta que actualmente se puede cifrar Hola después de formatos de streaming: HLS, MPEG DASH y Smooth Streaming. No se pueden cifrar las descargas progresivas.

Cuando un Reproductor solicita una secuencia que se establece toobe dinámicamente cifrado, servicios multimedia usa Hola configurado clave toodynamically cifrar el contenido con cifrado de AES o DRM. secuencia de hello toodecrypt, Hola Reproductor solicitará clave Hola del servicio de entrega de claves de Hola. toodecide si es usuario de hello autorizado tooget clave de hello, servicio de hello evalúa las directivas de autorización de Hola que especificó para la clave de Hola.

Si plan toohave varias claves de contenido o si desea toospecify una **servicio de entrega de clave/licencia** dirección URL distinta a Hola servicio de entrega de claves de servicios multimedia, use Media Services .NET SDK o las API de REST.

[Configuración de la directiva de autorización de claves mediante el SDK de Servicios multimedia para .NET](media-services-dotnet-configure-content-key-auth-policy.md)

[Configuración de la directiva de autorización de claves mediante la API de REST de Servicios multimedia](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Se aplican algunas consideraciones:
* Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, el extremo de streaming tiene toobe en hello **ejecutando** estado. 
* El recurso debe contener un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable. Para obtener más información, consulte [Codificación de un recurso](media-services-encode-asset.md).
* Hola servicio de entrega de claves almacena en caché ContentKeyAuthorizationPolicy y sus objetos relacionados (opciones de directivas y restricciones) durante 15 minutos.  Si una contentkeyauthorizationpolicy y especificar una restricción de "Token", toouse, a continuación, probarlo y, a continuación, actualizar la directiva de Hola "Abierto" demasiado restricción, se tardará aproximadamente 15 minutos antes de hello conmutadores toohello "Abierta" versión de la directiva de directiva de Hola.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Cómo: configurar la directiva de autorización de claves de Hola
Directiva de autorización de claves de hello tooconfigure, seleccione hello **protección de contenido** página.

Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave. pueden tener directivas de autorización de clave de contenido de Hello **abrir**, **token**, o **IP** restricciones de autorización (**IP** pueden configurarse con SDK de .NET o REST).

### <a name="open-restriction"></a>Restricción open
Hola **abrir** restricción significa sistema Hola ofrecerá hello tooanyone clave que realiza una solicitud de clave. Esta restricción puede ser útil para realizar pruebas.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Restricción de token
Directiva, presione Hola restringida por token de hello toochoose **TOKEN** botón.

Hola **token** directiva restringida debe ir acompañada de un token emitido por un **servicio de Token seguro** (STS). Servicios multimedia admite tokens en hello **Tokens Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato y **JSON Web Token** formato (JWT). Para obtener información, consulte [Autenticación de token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Servicios multimedia no proporciona **Servicios de tokens seguros**. Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue. Hola STS debe estar configurado toocreate un token firmado con hello especificado clave y emitir notificaciones que especificó en la configuración de restricción de token de Hola. Hello servicio de entrega de claves de servicios multimedia devolverá a cliente de toohello clave de cifrado de hello si Hola token es válido y hello notificaciones de token de hello coinciden con los configurados para la clave de contenido de Hola. Para obtener más información, consulte [tokens de ACS de Azure de uso tooissue](http://mingfeiy.com/acs-with-key-services).

Al configurar hello **TOKEN** directiva restringida, debe establecer valores para **clave de verificación**, **emisor** y **audiencia**. clave de verificación principal Hello contiene Hola clave que Hola token se firmó con, el emisor es Hola servicio de token seguro que emite el token de Hola. audiencia de Hello (a veces denominado ámbito) describe intención de hello del token de Hola u Hola recursos Hola token autoriza acceso. Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola.

### <a name="playready"></a>PlayReady
Al proteger el contenido con **PlayReady**, uno de cosas Hola que debe toospecify en la directiva de autorización es una cadena XML que define la plantilla de licencia de PlayReady de Hola. De forma predeterminada, se establece Hola después de la directiva:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices><ContentKey i:type="ContentEncryptionKeyFromHeader" /><LicenseType>Nonpersistent</LicenseType><PlayRight><AllowPassingVideoContentToUnknownOutput>Permitido</AllowPassingVideoContentToUnknownOutput></PlayRight></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>

Puede hacer clic en hello **Importar directiva xml** botón y proporcionar un XML diferente que se ajusta toohello esquema XML definido [aquí](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

