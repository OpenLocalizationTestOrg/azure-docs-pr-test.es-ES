---
title: "directivas de protección de contenido aaaConfiguring mediante Hola portal de Azure | Documentos de Microsoft"
description: "Este artículo demuestra cómo toouse Hola las directivas de protección de contenido de tooconfigure de portal de Azure. Hola artículo también se muestra cómo tooenable cifrado dinámico para los activos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Configuración de directivas de protección de contenido mediante Hola portal de Azure
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Información general
Servicios de multimedia de Microsoft Azure (AMS) permite toosecure su media de tiempo de hello sale del equipo a través de almacenamiento, procesamiento y entrega. Servicios multimedia permite toodeliver el contenido cifrado dinámicamente con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits), cifrado común (CENC) con PlayReady o Widevine DRM y FairPlay de Apple. 

AMS proporciona un servicio para entregar licencias de DRM y los clientes de tooauthorized de claves sin cifrado AES. Hello portal de Azure permite toocreate uno **clave/directiva de autorización de licencia** para todos los tipos de cifrado.

Este artículo demuestra cómo tooconfigure contenido directivas de protección con hello portal de Azure. Hola artículo también se muestra cómo tooyour activos de tooapply cifrado dinámico.


> [!NOTE]
> Si usa directivas de protección de Azure toocreate portal clásico de hello, directivas de hello no pueden aparecer en hello [portal de Azure](https://portal.azure.com/). Sin embargo, todos los Hola antiguo directivas todavía existe. Puede examinarlas utilizando hello Azure Media Services .NET SDK o hello [Azure-Media-Explorador de servicios](https://github.com/Azure/Azure-Media-Services-Explorer/releases) herramienta (directivas de hello toosee, contextual en activo hello -> Mostrar información (F4) -> haga clic en -> pestaña de claves de contenido Haga clic en clave de hello). 
> 
> Si desea tooencrypt su activo mediante nuevas directivas, configurarlos con hello portal de Azure, haga clic en Guardar y aplicar el cifrado dinámico. 
> 
> 

## <a name="start-configuring-content-protection"></a>Empezar a configurar la protección de contenido
toouse Hola portal toostart configuración de protección del contenido, la cuenta tooyour global AMS, Hola siguientes:

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Seleccione **Ajustes** > **Protección de contenido**.

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>directiva de autorización de licencias o claves
AMS admite varias formas de autenticar a los usuarios que realizan solicitudes de clave o licencia. Directiva de autorización de clave de contenido de Hello debe configurarse por parte del usuario y cumplir el cliente para hello clave/licencia toobe toohello delived cliente. Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: **abrir** o **token** restricción.

Hello portal de Azure permite toocreate uno **clave/directiva de autorización de licencia** para todos los tipos de cifrado.

### <a name="open"></a>Abrir
Restricción abierta significa que el sistema de hello cumplirán lo hello tooanyone clave que realiza una solicitud de clave. Esta restricción puede ser útil para realizar pruebas. 

### <a name="token"></a>SWT
directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS). Servicios multimedia admite tokens con formato Simple Web Tokens (SWT) de Hola y el formato de JSON Web Token (JWT). Los Servicios multimedia no proporcionan Servicios de tokens seguros. Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue. Hola STS debe estar configurado toocreate un token firmado con hello especificado clave y emitir notificaciones que especificó en la configuración de restricción de token de Hola. Servicios de multimedia de Hello servicio de entrega de claves devolverá Hola solicitado Hola y cliente de toohello (o licencias) de la clave si Hola token es válido notificaciones Hola token coinciden con las configuradas para las claves de hello (o licencias).

Al configurar la directiva restringida de tokens de hello, debe especificar la clave de verificación principal hello, emisor y parámetros de audiencia. clave de verificación principal Hello contiene Hola clave que Hola token se firmó con, el emisor es Hola servicio de token seguro que emite el token de Hola. audiencia de Hello (a veces denominado ámbito) describe intención de hello del token de Hola u Hola recursos Hola token autoriza acceso. Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola.

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>Plantilla de derechos de PlayReady
Para obtener información detallada acerca de la plantilla de derechos de hello PlayReady, vea [Media Services PlayReady licencia plantilla Overview](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>No persistente
Si configura licencia como no persistentes, solo se mantiene en memoria mientras Reproductor Hola está usando la licencia de Hola.  

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Persistente
Si configura licencia hello como persistente, se guarda en el almacenamiento persistente en el cliente de Hola.

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Plantilla de derechos de Widevine
Para obtener información detallada acerca de la plantilla de hello Widevine permisos, consulte [información general de plantilla de licencias de Widevine](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Básica
Cuando se selecciona **básica**, se creará la plantilla de Hola a todos los valores de los valores predeterminados.

### <a name="advanced"></a>Avanzado
Para una explicación detallada acerca de la opción avanzada de configuraciones de Widevine, consulte [este tema](media-services-widevine-license-template-overview.md) .

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>Configuración de FairPlay
tooenable FairPlay cifrado, necesita tooprovide Hola certificado de la aplicación y clave de secreto de aplicación (consulte) a través de la opción de configuración FairPlay Hola. Para más información sobre la configuración y los requisitos de FairPlay, consulte [este artículo](media-services-protect-hls-with-fairplay.md) .

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Aplicar activos tooyour de cifrado dinámico
tootake ventaja del cifrado dinámico, debe tooencode el archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Seleccione un recurso que desea tooencrypt
toosee todos sus activos, seleccione **configuración** > **activos**.

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Cifrado con AES o DRM
Cuando presiona **Cifrar** en un recurso, se le presentan dos opciones: **AES** o **DRM**. 

#### <a name="aes"></a>AES
El cifrado de claves sin cifrado AES se habilitará en todos los protocolos de streaming: Smooth Streaming, HLS y MPEG-DASH.

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Cuando se selecciona la pestaña DRM de hello, se presentan con las diferentes opciones de directivas de protección de contenido (que debe haber configurado hasta ahora) + un conjunto de protocolos de transmisión de datos.

* **PlayReady y Widevine con MPEG-DASH** : cifrará dinámicamente su transmisión MPEG-DASH con DRM de PlayReady y Widevine.
* **PlayReady y Widevine con MPEG-DASH más FairPlay con HLS** : cifrará dinámicamente su transmisión MPEG-DASH con DRM de PlayReady y Widevine. También se cifrarán las transmisiones HLS con FairPlay.
* **PlayReady solo con Smooth Streaming, HLS y MPEG-DASH** : cifrará dinámicamente Smooth Streaming, HLS, transmisiones MPEG DASH con DRM de PlayReady.
* **Widevine solo con MPEG-DASH** : cifrará dinámicamente MPEG-DASH con DRM de Widevine.
* **FairPlay solo con HLS** : cifrará dinámicamente su transmisión HLS con FairPlay.

tooenable FairPlay cifrado, necesita tooprovide Hola certificado de la aplicación y clave de secreto de aplicación (consulte) a través de la opción de configuración de FairPlay de hoja de configuración de protección de contenido de Hola Hola.

![Proteger contenido](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Una vez realizada la selección de cifrado de hello, presione **aplicar**.

>[!NOTE] 
>Si tiene previsto tooplay un AES cifrado HLS en Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

