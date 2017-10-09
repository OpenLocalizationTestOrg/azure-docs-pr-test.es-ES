---
title: "notas de la versión de servicios de aaaMedia | Documentos de Microsoft"
description: "Notas de la versión de Servicios multimedia"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Notas de la versión de Azure Media Services
Estas notas de la versión resumen los cambios realizados desde las versiones anteriores y los problemas conocidos.

> [!NOTE]
> Se desea toohear de nuestros clientes y centrarnos en resolver los problemas que le afectan. tooreport un problema o realizar preguntas, publique en hello [foro de MSDN de Azure Media Services].
> 
> 

## <a id="issues"></a>Problemas actualmente conocidos
### <a id="general_issues"></a>Problemas generales de Servicios multimedia
| Problema | Descripción |
| --- | --- |
| No se proporcionan varios encabezados HTTP comunes en hello API de REST. |Si desarrolla aplicaciones de servicios multimedia mediante Hola API de REST, encontrará que algunos campos de encabezado HTTP comunes (incluidos CLIENT-REQUEST-ID, REQUEST-ID y RETURN-CLIENT-REQUEST-ID) no se admiten. se agregarán los encabezados de Hello en una futura actualización. |
| No se permite la codificación porcentual. |Servicios multimedia usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual. Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Además, solo puede haber un "." para la extensión de nombre de archivo de Hola. |
| Hola método ListBlobs que forma parte de la versión del SDK de almacenamiento de Azure Hola 3.x genera un error. |Servicios multimedia genera direcciones URL de SAS basadas en hello [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) versión. Si desea que los blobs de toolist toouse SDK de almacenamiento de Azure en un contenedor de blobs, use hello [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) método que forma parte del SDK de almacenamiento de Azure versión 2.x. Hola método ListBlobs que forma parte de la versión del SDK de almacenamiento de Azure Hola 3.x generará un error. |
| Servicios multimedia de mecanismo de limitación restringe el uso de recursos de Hola para aplicaciones que realizan el servicio de toohello solicitudes excesivas. servicio de Hello puede devolver el código de estado HTTP Service Unavailable (503) Hola. |Para obtener más información, consulte Descripción de Hola de código de estado HTTP 503 Hola Hola [códigos de Error de Azure Media Services](media-services-encoding-error-codes.md) tema. |
| Cuando se consultan las entidades, hay un límite de 1000 entidades devueltas al mismo tiempo porque pública v2 REST limita los resultados de too1000 de resultados de consulta. |Necesita toouse **omitir** y **tomar** (. NET) / **arriba** (REST) como se describe en [en este ejemplo .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) y [esta API de REST en el ejemplo se](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Algunos clientes pueden proceder a través de un problema de etiqueta repetir en el manifiesto de Smooth Streaming Hola. |Para obtener más información, consulte [esta](media-services-deliver-content-overview.md#known-issues) sección. |
| Los objetos del SDK de .NET de Servicios multimedia de Azure no se pueden serializar y, como resultado, no funcionan con el almacenamiento en caché de Azure. |Si intentas tooserialize hello assetcollection del SDK objeto tooadd tooAzure el almacenamiento en caché, una excepción se produce. |
| Los trabajos de codificación generan un error con esta cadena de mensaje "Fase: DownloadFile. Código: System.NullReferenceException". |flujo de trabajo codificación Hola típico es tooupload archivos de vídeo de entrada tooan recurso de entrada así como enviar uno o más trabajos de codificación para ese recurso, de entrada sin modificar más que recurso de entrada. Sin embargo, si modifica Hola recurso (por ejemplo, agregar/eliminar o cambiar el nombre de archivos dentro de hello activos) de entrada, pueden producir un error de DownloadFile trabajos posteriores. solución de Hello es toodelete Hola recurso de entrada y volver a cargar tooa de los archivos de entrada activo nuevo. |

## <a id="rest_version_history"></a>Historial de versiones de API de REST
Para obtener información acerca de hello historial de versiones de API de REST de servicios multimedia, consulte [Azure Media Services REST API Reference].

## <a name="june-2017-release"></a>Versión de junio de 2017

Media Services ahora admite la [autenticación basada en Azure Active Directory (Azure AD)](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Actualmente, servicios multimedia admite el modelo de autenticación de servicio de Control de acceso de Azure Hola. Sin embargo, la autorización de Access Control dejará de usarse el 1 de junio de 2018. Se recomienda que migre modelo de autenticación de Azure AD toohello tan pronto como sea posible.

## <a name="march-2017-release"></a>Versión de marzo de 2017

Ahora puede usar el estándar de multimedia de Azure demasiado[genere automáticamente una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) especificando Hola "Transmisión por secuencias adaptativa" cadena cuando se crea una tarea de codificación de valores predefinidos. "Transmisión por secuencias adaptativa" es valor preestablecido de hello recomendada si desea tooencode un vídeo para streaming con servicios multimedia. Si necesita toocustomize una codificación preestablecida para su escenario concreto, puede comenzar por [estos](media-services-mes-presets-overview.md) valores preestablecidos.

Ahora puede usar Azure Media estándar o flujo de trabajo de Premium de codificación de medios demasiado[crear una tarea de codificación que genera fragmentos fmp4 dinámico](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Versión de febrero de 2017

A partir del 1 de abril de 2017, cualquier registro de trabajo en su cuenta de más de 90 días se eliminarán automáticamente, junto con sus registros de tarea asociados, incluso si el número total de Hola de registros está por debajo de la cuota máxima de Hola. Si necesita información de trabajo o tarea hello tooarchive, puede usar código de hello descrito [aquí](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Versión de enero de 2017

En Microsoft Azure Media Services (AMS), un **extremo de transmisión por secuencias** representa un servicio de streaming que puede entregar contenido directamente tooa aplicación de reproducción de cliente o tooa red de entrega de contenido (CDN) para su distribución posterior. Servicios multimedia también proporciona integración sin problemas de CDN de Azure. flujo de salida de Hello de un servicio de StreamingEndpoint puede ser una secuencia en directo, un vídeo a petición o la descarga progresiva del recurso en su cuenta de servicios multimedia. Cada cuenta de Azure Media Services incluye un punto de conexión de streaming predeterminado. StreamingEndpoints adicionales pueden crearse en la cuenta de hello. Existen dos versiones de puntos de conexión de streaming: 1.0 y 2.0. A partir del 10 de enero de 2017, las cuentas recién creadas de AMS incluirán de manera **predeterminada** la versión 2.0 del punto de conexión de streaming. Agregar cuenta de toothis de extremos de streaming adicional también será versión 2.0. Este cambio no afectará a las cuentas existentes de hello; StreamingEndpoints existente serán versión 1.0 y pueden ser actualizado tooversion 2.0. Este cambio implicará modificaciones en cuanto al comportamiento, la facturación y las características (para obtener más información, consulte [este](media-services-streaming-endpoints-overview.md) tema).

Además, empezando con la versión de Hola 2.15, servicios multimedia de Azure agregado Hola después de la entidad de extremo de transmisión por secuencias de propiedades toohello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Para obtener información general detallada de estas propiedades, consulte [aquí](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Versión de diciembre de 2016

Servicios multimedia de Azure ahora le permite tooaccess los datos de telemetría y las métricas para sus servicios. versión actual de Hola de AMS le permite recopilar datos de telemetría de canal en vivo, StreamingEndpoint, y en vivo de las entidades de archivo. Para obtener más información, consulte [este tema](media-services-telemetry-overview.md) .

## <a id="july_changes16"></a>Versión de julio de 2016
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Archivo de actualizaciones toomanifest (*. ISM) generado mediante la codificación de tareas
Cuando una tarea de codificación es enviado tooMedia codificador estándar o Codificador multimedia de Azure, tarea de codificación de hello genera un [archivo de manifiesto de transmisión por secuencias](media-services-deliver-content-overview.md) (* .ism) activo de salida de archivo en Hola. Con la versión de servicio más reciente de hello, se ha actualizado la sintaxis de Hola de este archivo de manifiesto de transmisión por secuencias.

> [!NOTE]
> sintaxis de Hola de hello transmisión por secuencias de archivo de manifiesto (.ism) está reservado para uso interno y está sujeto toochange en futuras versiones. No modifique ni manipular Hola contenido de este archivo.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Un nuevo manifiesto de cliente (*. Archivo ISMC) se genera en hello activo de salida cuando una tarea de codificación genera uno o varios archivos MP4
A partir de versión de servicio más reciente de hello, después de finalizar una tarea de codificación que genera uno o más archivos MP4, Hola Hola salida que activo también contendrá un archivo de manifiesto (*.ismc) de cliente transmisión por secuencias. archivo .ismc de Hello ayuda a mejorar el rendimiento de Hola de transmisión de datos dinámicos. 

> [!NOTE]
> Hola sintaxis del archivo de manifiesto (.ismc) del cliente de hello está reservado para uso interno y está sujeto toochange en futuras versiones. No modifique ni manipular Hola contenido de este archivo.
> 
> 

Para más información, consulte [este blog](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) .

### <a name="known-issues"></a>Problemas conocidos
Algunos clientes pueden proceder a través de un problema de etiqueta repetir en el manifiesto de Smooth Streaming Hola. Para obtener más información, consulte [esta](media-services-deliver-content-overview.md#known-issues) sección.

## <a id="apr_changes16"></a>Versión de abril de 2016
### <a name="azure-media-analytics"></a>Análisis multimedia de Azure
Servicios multimedia de Azure presentó Análisis multimedia de Azure para inteligencia de vídeo eficaz. Para obtener más información, consulte [Información general de análisis de Servicios multimedia de Azure](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (versión preliminar)
Servicios multimedia de Azure ahora permite toodynamically cifrar su HTTP Live Streaming (HLS) de contenido con FairPlay de Apple. También puede utilizar la entrega de licencia AMS servicio toodeliver FairPlay licencias tooclients. Para obtener más información, consulte [tooStream de servicios multimedia de Azure Use su contenido HLS protegido con Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Versión de febrero de 2016
Hola última versión del SDK de servicios multimedia de Azure para .NET (3.5.3) contiene una corrección de errores de Widevine relacionada. Hola problema estaba: AssetDeliveryPolicy no se puede reutilizar para varios recursos cifrados con Widevine. Como parte de este Hola de corrección de errores después de la propiedad se agregó toohello SDK: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Versión de enero de 2016
Unidades reservadas de codificación cambiar el nombre tooreduce confusión con los nombres de codificador.

Hola Basic, Standard y Premium unidades reservadas de codificación son tooS1 cuyo nombre ha cambiado, S2, S3 reservado unidades, respectivamente  Los clientes que usan hoy en día RUs de codificación básicos verán S1 como etiqueta de hello en el Portal de Azure (y en la factura de hello), al estándar y Premium verán las etiquetas de hello S2 y S3 respectivamente. 

## <a id="dec_changes_15"></a>Versión de diciembre de 2015

### <a name="azure-media-encoder-deprecation-announcement"></a>Anuncio de degradación de Azure Media Encoder

El Codificador multimedia de Azure dejará de utilizarse a partir de aproximadamente 12 meses de versión de Hola de Media Encoder estándar.

### <a name="azure-sdk-for-php"></a>SDK de Azure para PHP
equipo de Azure SDK Hola publica una nueva versión de hello [Azure SDK para PHP](http://github.com/Azure/azure-sdk-for-php) paquete que contiene las actualizaciones y nuevas características de servicios multimedia de Microsoft Azure. Hola en particular, SDK de servicios multimedia de Azure para PHP ahora admite más reciente Hola [protección de contenido](media-services-content-protection-overview.md) características: cifrado dinámico con AES y DRM (PlayReady y Widevine) con y sin restricción de Token. También admite el escalado de [unidades de codificación](media-services-dotnet-encoding-units.md).

Para más información, consulte:

* Hola [SDK de servicios de multimedia de Microsoft Azure para PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blog.
* siguiente Hello [ejemplos de código](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp obtener una rápida introducción:
  * **vodworkflow_aes.PHP**: se trata de un archivo PHP que muestra cómo toouse cifrado dinámico AES-128 y el servicio de entrega de clave. Se basa en el ejemplo de Hola .NET explicada en [esto](media-services-protect-with-aes128.md) artículo.
  * **vodworkflow_aes.PHP**: se trata de un archivo PHP que muestra cómo toouse cifrado dinámico PlayReady y del servicio de entrega de licencias. Se basa en el ejemplo de Hola .NET explicada en [esto](media-services-protect-with-drm.md) artículo.
  * **scale_encoding_units.PHP**: se trata de un archivo PHP que muestra cómo tooscale codificación reservado unidad.

## <a id="nov_changes_15"></a>Versión de noviembre de 2015
Servicios multimedia de Azure ahora ofrece el servicio de entrega de licencia de Google Widevine en la nube de Hola. Para obtener más información, consulte demasiado[este blog del anuncio](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Vea también [este tutorial](media-services-protect-with-drm.md) y el [repositorio de GitHub](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Tenga en cuenta que los servicios de entrega de licencias de Widevine proporcionados por Servicios de multimedia de Azure están en vista previa. Para obtener más información, consulte [este blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Versión de octubre de 2015
Servicios de multimedia de Azure (AMS) es ahora en vivo en hello después de centros de datos: sur de Brasil, India occidental, sur de India y India Central. Ahora puede usar Hola portal de Azure[crear cuentas de servicio de medios](media-services-portal-create-account.md) y realizar varias tareas que se describen [aquí](https://azure.microsoft.com/documentation/services/media-services/). Sin embargo, Codificación en directo no está habilitado en estos centros de datos. Además, no todos los tipos de unidades reservadas de codificación están disponibles en estos centros de datos.

* Sur de Brasil: solo están disponibles las unidades reservadas de codificación Estándar y Básica.
* India occidental, Sur de la India e India central: solo están disponibles unidades reservadas de codificación básicas

## <a id="september_changes_15"></a>Versión de septiembre de 2015
* AMS ahora ofrece Hola capacidad tooprotect vídeo bajo demanda (VOD) y secuencias en directo con tecnología DRM Modular de Widevine. Puede usar Hola después toohelp de socios comerciales de servicios de entrega entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    Puede usar [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (a partir de la versión de Hola 3.5.1) o REST API tooconfigure su toouse AssetDeliveryConfiguration Widevine.  
* AMS agregó compatibilidad para vídeos ProRes de Apple. Ahora puede cargar sus archivos de vídeos de origen QuickTime que usan ProRes de Apple u otros códecs. Para más información, vea [este blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* Ahora puede usar medios codificador estándar toodo Sub-recorte y en vivo extracción de archivo. Para más información, vea [este blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* se realizaron Hola después de las actualizaciones de filtrado: 
  
  * Ahora puede usar el formato Apple HTTP Live Streaming (HLS) con filtro solo de audio. Esta actualización permite tooremove solo audio track especificando (solo audio = false) en la dirección URL de Hola.
  * Al definir filtros para los activos, ahora tiene toocombine de capacidad (too3 arriba) varios filtros en una sola dirección URL.
    
    Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) .
* AMS admite ahora I-Frames en HLS v4. La compatibilidad con I-Frames optimiza las operaciones de avance rápido y rebobinado. De forma predeterminada, todas las salidas de HLS v4 incluyen la lista de reproducción de I-Frame (EXT-X-I-FRAME-STREAM-INF).
  
    Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) .

## <a id="august_changes_15"></a>Versión de agosto de 2015
* Ya están disponibles el SDK de Servicios multimedia de Azure para la versión de Java V0.8.0 y nuevos ejemplos. Para más información, consulte:
  
  * [Entrada de blog](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Repositorio de ejemplos de Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Actualización del Reproductor multimedia de Azure con compatibilidad con secuencias de audio múltiples. Para más información, consulte:
  * [Entrada de blog](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Versión de julio de 2015
* Anuncio de disponibilidad general de Hola de Media Encoder estándar. Para más información, vea [esta publicación del blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    Media Encoder Estándar usa valores predefinidos que se describen en [esta](http://go.microsoft.com/fwlink/?LinkId=618336) sección. Tenga en cuenta que cuando se usa un valor preestablecido para codifica de 4k, debería obtener hello **Premium** reservado del tipo de unidad. Para obtener más información, consulte [cómo tooScale codificación](media-services-scale-media-processing-overview.md).
* Subtítulos en tiempo real con Servicios multimedia de Azure y el Reproductor. Para obtener más información, consulte [esta publicación del blog](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/).

### <a name="media-services-net-sdk-updates"></a>Actualizaciones del SDK .NET de Servicios multimedia
Ahora la versión del SDK de Servicios multimedia para .NET de Azure es la 3.4.0.0. Hola después funcionalidad se agregó en esta versión:  

* Se ha implementado la compatibilidad con archivos activos. Tenga en cuenta que no se puede descargar un recurso que contenga un archivo activo.
* Se ha implementado compatibilidad para filtros dinámicos.
* Implementada ninguna funcionalidad que permite que los usuarios tookeep almacenamiento contenedor al eliminar el recurso.
* Correcciones de errores relacionados con las directivas de tooretry de canales.
* **Flujo de trabajo de Codificador multimedia Premium** habilitado.

## <a id="june_changes_15"></a>Versión de junio de 2015
### <a name="media-services-net-sdk-updates"></a>Actualizaciones del SDK .NET de Servicios multimedia
Ahora la versión del SDK .NET de Servicios multimedia de Azure es la 3.3.0.0. Hola después funcionalidad se agregó en esta versión:  

* Compatibilidad con la especificación de detección de OpenId Connect.
* Compatibilidad con el control de sustitución de claves en el lado del proveedor de identidades. 

Si está utilizando un proveedor de identidades que expone el documento de detección de OpenID Connect (como Hola hacen los proveedores siguientes: Azure Active Directory, Google, Salesforce), puede indicar a tooobtain de servicios multimedia de Azure claves para la validación de token JWT de firma OpenID conectar la especificación de detección. 

Para obtener más información, consulte [mediante Json Web las teclas de toowork de especificación de detección de OpenID Connect con JWT símbolo (token) de autenticación en servicios multimedia de Azure](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Versión de mayo de 2015
Anuncio de Hola siguientes nuevas funciones:

* [Una vista previa de codificación en directo con Media Services](media-services-manage-live-encoder-enabled-channels.md)
* [Manifiesto dinámico](media-services-dynamic-manifest-overview.md)
* [Una vista previa del procesador multimedia de Azure Media Hyperlapse](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Versión de abril de 2015
### <a name="general-media-services-updates"></a>Actualizaciones generales de Servicios multimedia
* [Presentación de Reproductor multimedia de Azure](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* A partir de 2.10 de REST de servicios multimedia, los canales que son tooingest configurado un protocolo RTMP, se crean con principal y direcciones URL de entrada de la base de datos secundaria. Para obtener más información, consulte [Configuraciones de ingesta de canales](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Actualizaciones de Azure Media Indexer
* Compatibilidad con el idioma español
* Nuevo formato de xml de configuración

Para obtener más información, consulte [este blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Actualizaciones del SDK .NET de Servicios multimedia
Ahora la versión del SDK .NET de Servicios multimedia de Azure es la versión 3.2.0.0.

siguiente Hola es algunas de a las actualizaciones de nuestros clientes hello:

* **Cambio problemático**: cambiar **TokenRestrictionTemplate.Issuer** y **TokenRestrictionTemplate.Audience** toobe de un tipo de cadena.
* Las actualizaciones relacionadas con directivas de reintento personalizadas toocreating.
* Correcciones de errores relacionados con toouploading/descargar archivos.
* Hola **MediaServicesCredentials** clase ahora acepta tooauthenticate de punto de conexión de control de acceso principal y secundaria en.

## <a id="march_changes_15"></a>Versión de marzo de 2015
### <a name="general-media-services-updates"></a>Actualizaciones generales de Servicios multimedia
* Servicios multimedia ofrece ahora integración de CDN de Azure. Hola toosupport hello integración, **CdnEnabled** propiedad se agregó demasiado**StreamingEndpoint**.  **CdnEnabled** puede utilizarse con las API de REST a partir de la versión 2.9 (para obtener más información, consulte [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** puede utilizarse con el SDK .NET a partir de la versión 3.1.0.2 (para obtener más información, consulte [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Anuncio del **flujo de trabajo Premium de Codificador multimedia**. Para obtener más información, consulte [Introducción de la codificación Premium en Servicios multimedia de Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Versión de febrero de 2015
### <a name="general-media-services-updates"></a>Actualizaciones generales de Servicios multimedia
La versión de la API de REST de Servicios multimedia es ahora la 2.9. A partir de esta versión, puede habilitar la integración de CDN de Azure con extremos de streaming de Hola. Para obtener más información, consulte [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Versión de enero de 2015
### <a name="general-media-services-updates"></a>Actualizaciones generales de Servicios multimedia
Anuncio de disponibilidad General (GA) de protección de contenido con cifrado dinámico. Para más información, consulte [Azure Media Services enhances streaming security with General Availability of DRM technology](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/)(Servicios multimedia de Azure mejoran la seguridad de streaming con la disponibilidad general de tecnología DRM).

### <a name="media-services-net-sdk-updates"></a>Actualizaciones del SDK .NET de Servicios multimedia
Ahora la versión del SDK .NET de Servicios multimedia de Azure es la 3.1.0.1.

Esta versión deja hello Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate un inicializador como obsoleto. Hola nuevo constructor usa TokenType como argumento.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Versión de diciembre de 2014
### <a name="general-media-services-updates"></a>Actualizaciones generales de Servicios multimedia
* Algunas actualizaciones y nuevas características se agregaron toohello Azure indizador procesador multimedia. Para obtener más información, consulte [Azure Media Indexer Version 1.1.6.7 Release Notes](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/)(Notas de la versión de Azure Media Indexer versión 1.1.6.7).
* Agrega una nueva API de REST que permite tooupdate unidades reservadas de codificación: [EncodingReservedUnitType con REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Se agregó compatibilidad con CORS para el servicio de entrega de claves.
* Se realizaron mejoras en el rendimiento de la directiva de autorización de consultas.
* En el centro de datos de China, Hola [dirección URL de entrega de clave](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) es ahora por cliente (igual que en otros centros de datos).
* Se agregó la duración de destino automático de HLS. Cuando se realiza el streaming en vivo, HLS siempre se empaqueta dinámicamente. De forma predeterminada, los servicios multimedia calcula automáticamente empaquetado proporción de segmento HLS (FragmentsPerSegment) en función de hello fotogramas clave intervalo (KeyFrameInterval), también denominado tooas grupo de imágenes: GOP, que se recibe de codificador en directo de Hola. Para obtener más información, consulte [trabajo con el streaming en vivo de Azure Media Services].

### <a name="media-services-net-sdk-updates"></a>Actualizaciones del SDK .NET de Servicios multimedia
* [SDK .NET de Servicios multimedia de Azure](http://www.nuget.org/packages/windowsazure.mediaservices/) es la 3.1.0.0.
* Actualizar Hola .net SDK dependencia too.NET 4.5 Framework.
* Agrega una nueva API que permite tooupdate unidades reservadas de codificación. Para obtener más información, consulte [Actualización del tipo de unidad reservada y aumento de las unidades reservadas de codificación mediante .NET](media-services-dotnet-encoding-units.md).
* Se agregó compatibilidad con JWT (token web de JSON) para la autenticación de token. Para obtener más información, consulte [JWT token Authentication in Azure Media Services and Dynamic Encryption](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)(Autenticación de token JWD en Servicios multimedia y cifrado dinámico de Azure).
* Agregado desplazamientos relativos para BeginDate y ExpirationDate en plantilla de licencia de PlayReady de Hola.

## <a id="november_changes_14"></a>Versión de noviembre de 2014
* Servicios multimedia ahora permite tooingest un activo Smooth Streaming (fmp4 dinámico) contenido en una conexión SSL. tooingest a través de SSL, que seguro Hola de tooupdate tooHTTPS de dirección URL de introducción.  Tenga en cuenta que, actualmente, AMS no admite SSL con dominios personalizados.  Para obtener más información sobre el streaming en vivo, consulte el artículo sobre [trabajo con el streaming en vivo de Azure Media Services].
* En la actualidad, no se puede ingerir un stream en vivo RTMP por una conexión SSL.
* Solo puede transmitir a través de SSL si Hola origen desde el que entrega el contenido se creó después de 10 de septiembre de 2014. Si sus direcciones URL de streaming se basan en hello streaming creados después del 10 de septiembre, dirección URL de hello contiene "streaming.mediaservices.windows.net" (nuevo formato de hello). Direcciones URL de streaming que contienen "origin.mediaservices.windows.net" (formato antiguo de hello) no son compatibles con SSL. Si la dirección URL está en formato antiguo de Hola y desea toobe pueda toostream a través de SSL, [crear un nuevo extremo de streaming](media-services-portal-manage-streaming-endpoints.md). Utilice direcciones URL creadas en hello nuevos streaming extremo toostream su contenido a través de SSL.

## <a id="october_changes_14"></a>Versión de octubre de 2014
### <a id="new_encoder_release"></a>Versión del codificador de Servicios multimedia
Anuncio Hola nueva versión de Media Services Azure Media Encoder. Con hello más reciente Codificador multimedia de Azure solo se le cobra por GB de salida, pero en caso contrario Hola nuevo codificador es una característica compatible con el codificador de hello anterior. Para obtener más información, consulte [Detalles de precios de Servicios multimedia].

### <a id="oct_sdk"></a>SDK .NET de Servicios multimedia
La versión de las extensiones del SDK de Servicios multimedia para .NET es ahora la 2.0.0.3.

La versión del SDK de Servicios multimedia para .NET es ahora la 3.0.0.8.

se realizaron Hola siguientes cambios:

* Refactorización de clases de directivas de reintento.
* Agregar encabezados de solicitud de toohttp de cadena de agente de usuario.
* Adición del paso de compilación de restauración de nuget.
* Corrección de certificado de toouse x509 de pruebas de escenario del repositorio.
* Validación de la configuración al actualizar el canal y extremo de streaming.

### <a name="new-github-repository-toohost-media-services-samples"></a>Nuevos ejemplos de servicios multimedia de toohost de repositorio de GitHub
Hay ejemplos en el [Azure Media Services samples GitHub repository](https://github.com/Azure/Azure-Media-Services-Samples)(repositorio de GitHub de ejemplo de Servicios multimedia de Azure).

## <a id="september_changes_14"></a>Versión de septiembre de 2014
La versión de los metadatos de REST de Servicios multimedia es ahora la 2.7. Para obtener más información acerca de las últimas actualizaciones de REST hello, consulte [Azure Media Services REST API Reference].

El SDK de Servicios multimedia para .NET es ahora la versión 3.0.0.7.

### <a id="sept_14_breaking_changes"></a>Cambios importantes
* **Origen** cambió demasiado[StreamingEndpoint].
* Un cambio de comportamiento predeterminado de hello cuando se usa hello **portal de Azure** tooencode y, a continuación, publicar archivos MP4.

Anteriormente, cuando se usa Hola Portal clásico de Azure toopublish un recurso de vídeo MP4 único archivo una URL de SAS se crearía (direcciones URL de SAS le permiten hello toodownload vídeo desde un almacenamiento de blobs). Actualmente, cuando utilice tooencode de Portal de Azure clásico de hello y, a continuación, publicar un recurso de vídeo MP4 único archivo, Hola genera URL puntos tooan Azure Media Services extremo de streaming.  Este cambio no afecta a los vídeos MP4 que son servicios tooMedia cargado directamente y se publican sin que se está codificando por servicios multimedia de Azure.

Actualmente, tiene Hola después dos opciones toosolve Hola problema.

* Habilitar unidades de streaming y usar activos de empaquetado dinámico toostream Hola. mp4 como una presentación de transmisión por secuencias suave.
* Crear un toodownload de dirección url SAS (o reproducir progresivamente). mp4 Hola. Para obtener más información acerca de cómo toocreate un localizador SAS, consulte [entregar contenido].

### <a id="sept_14_GA_changes"></a>Nuevas características/escenarios que forman parte de la versión GA
* **Procesador multimedia del indizador**. Para obtener más información, consulte [Indización de archivos multimedia con Azure Media Indexer].
* Hola [StreamingEndpoint] entidad ahora permite tooadd los nombres de dominio personalizado (host).
  
    Para un nombre de dominio personalizado toobe usa como nombre del extremo de streaming de servicios de multimedia de Hola, deberá tooyour de nombres de host personalizado tooadd extremo de streaming. Utilice nombres de host personalizado de tooadd de las API de REST de servicios multimedia o .NET SDK Hola.
  
    Hola siguientes consideraciones se aplica:
  
  * Debe tener la propiedad de Hola de nombre de dominio personalizado de Hola.
  * propiedad Hola Hola del nombre de dominio debe ser validada por servicios multimedia de Azure. dominio de hello toovalidate, crear un CName que asigna <MediaServicesAccountId>.<parent domain> tooverifydns. < mediaservices-dns-zone >. 
  * Debe crear otro CName que asigne nombre de host del Hola host personalizado nombre (por ejemplo, sports.contoso.com) tooyour StreamingEndpont de servicios multimedia (por ejemplo, amstest.streaming.mediaservices.windows.net).

    Para obtener más información, vea hello **CustomHostNames** propiedad Hola [StreamingEndpoint] tema.

### <a id="sept_14_preview_changes"></a>Nuevas características/escenarios que forman parte de la versión de vista previa de Hola
* Vista previa de Live Streaming. Para obtener más información, consulte [trabajo con el streaming en vivo de Azure Media Services].
* Servicio de entrega de claves. Para obtener más información, consulte [Uso del cifrado dinámico AES-128 y del servicio de entrega de claves].
* Cifrado dinámico AES. Para obtener más información, consulte [Uso del cifrado dinámico AES-128 y del servicio de entrega de claves].
* Servicio de entrega de licencias PlayReady. Para obtener más información, consulte [Uso del cifrado dinámico de PlayReady y servicio de entrega de licencias].
* Cifrado dinámico PlayReady. Para obtener más información, consulte [Uso del cifrado dinámico de PlayReady y servicio de entrega de licencias].
* Plantilla de licencias PlayReady de Servicios multimedia. Para obtener más información, consulte [Información general de plantillas de licencias de PlayReady de Servicios multimedia].
* Activos cifrados de almacenamiento de streaming. Para obtener más información, consulte [Streaming de contenido cifrado de almacenamiento].

## <a id="august_changes_14"></a>Versión de agosto de 2014
Al codificar un activo, se produce un recurso de salida tras la finalización del trabajo de codificación de Hola. Hasta esta versión, el codificador de Servicios multimedia de Azure producía metadatos sobre activos de salida. A partir de este codificador Hola de versión, también produce metadatos sobre los activos de entrada. Para obtener más información, vea hello [entrada metadatos] y [metadatos de salida] temas.

## <a id="july_changes_14"></a>Versión de julio de 2014
Hola después de correcciones de errores se diseñaron para hello Empaquetador de servicios multimedia de Azure y sistema de cifrado:

* Sólo de audio se reproduce el Streaming en vivo transmultiplexación un tooHTTP de recurso de archivo dinámico: Esto se ha corregido y ahora se reproducen el audio y vídeo.
* Al empaquetar un tooHTTP activo el cifrado de sellado AES de 128 bits y Streaming en vivo, secuencias de hello empaquetada no se reproducen en dispositivos Android: este error se ha corregido y transmisión empaquetada Hola se reproduce en dispositivos Android compatibles con HTTP Live Streaming.

## <a id="may_changes_14"></a>Versión de mayo de 2014
### <a id="may_14_changes"></a>Actualizaciones generales de Servicios multimedia
Ahora puede usar [empaquetado dinámico] toostream HTTP Live Streaming (HLS) v3. toostream HLS v3, agregue Hola siguiendo la ruta de acceso de localizador de origen de formato toohello: * .ism/manifest(format=m3u8-aapl-v3). Para obtener más información, consulte el [blog de Nick Drouin].

El empaquetado dinámico admite ahora también la entrega de HLS (v3 y v4) cifrado con PlayReady basado en Smooth Streaming cifrado estáticamente con PlayReady. Para obtener información acerca de cómo tooencrypt Smooth Streaming con PlayReady, vea [protección de Smooth Streaming con PlayReady].

### <a name="may_14_donnet_changes"></a>Actualizaciones del SDK .NET de Servicios multimedia
Hola siguiendo las mejoras se incluye en hello versión del SDK de .NET de servicios multimedia 3.0.0.5:

* Mayor velocidad y resistencia para cargar/descargar activos multimedia.
* Mejoras en la gestión de excepciones transitorias y la lógica de reintento: 
  
  * La detección de errores transitorios y la lógica de reintento se han mejorado en las excepciones ocasionadas al consultar, guardar cambios y cargar y descargar archivos. 
  * Al recibir excepciones web (por ejemplo, durante una solicitud de token de ACS), observará que ahora se producen con mayor rapidez errores graves.

Para obtener más información, consulte [lógica de reintento en hello SDK de servicios multimedia para .NET].

## <a id="april_changes_14"></a>Versión del codificador de abril de 2014
### <a name="april_14_enocer_changes"></a>Actualizaciones del codificador de Servicios multimedia
* Se agregó compatibilidad para introducir archivos AVI creados mediante el editor no lineal de hello Grass Valley EDIUS, donde es ligeramente Hola vídeo comprimido mediante códec Grass Valley HQ/HQX. Para obtener más información, consulte [Grass Valley anuncia EDIUS 7 Streaming a través de hello en la nube].
* Se agregó compatibilidad para especificar la convención de nomenclatura de Hola para archivos de hello generados por el Codificador multimedia de Hola. Para obtener más información, consulte [Control de nombres de archivo de salida del codificador de Servicios multimedia].
* Se ha agregado compatibilidad con superposiciones de vídeo y/o audio. Para obtener más información, consulte [Creación de superposiciones].
* Se ha agregado compatibilidad con la unión de varios segmentos de vídeo. Para obtener más información, consulte [Unión de segmentos de vídeo].
* Se ha corregido un error relacionado con tootranscoding de MP4s donde audio Hola se ha codificado con MPEG-1 Audio layer 3 (también conocido como MP3).

## <a id="jan_feb_changes_14"></a>Versiones de enero/febrero de 2014
### <a name="jan_fab_14_donnet_changes"></a>SDK .NET de Servicios multimedia de Azure 3.0.0.1, 3.0.0.2 y 3.0.0.3
Hola cambios en las versiones 3.0.0.1 y 3.0.0.2 incluyen:

* Se han corregido problemas relacionados con toousage de las consultas LINQ con instrucciones OrderBy.
* Se han dividido las soluciones de prueba de [GitHub] en pruebas basadas en unidades y pruebas basadas en escenarios.

Para obtener más información acerca de los cambios de hello, consulte: [las versiones de Azure Media Services .NET SDK 3.0.0.1 y 3.0.0.2].

Hola siguientes cambios se realizaron en la versión 3.0.0.3:

* Actualizar toouse versión 3.0.3.0 de almacenamiento de Azure dependencias. 
* Se ha corregido el problema de compatibilidad con versiones posteriores en las versiones 3.0.*.* . 

## <a id="december_changes_13"></a>Versión de diciembre de 2013
### <a name="dec_13_donnet_changes"></a>SDK .NET de Servicios multimedia de Azure 3.0.0.0
> [!NOTE]
> Las versiones 3.0.x.x no son compatibles con las versiones 2.4.x.x.
> 
> 

versión más reciente de Hola de hello SDK de servicios multimedia es ahora la versión 3.0.0.0. Puede descargar el paquete más reciente de Hola de Nuget u obtener bits Hola de [GitHub].

A partir de hello SDK de servicios multimedia versión 3.0.0.0, puede reutilizar hello [Azure Active Directory Access Control Service (ACS)] símbolos (tokens). Para obtener más información, vea Hola "reutilización de Control de servicio de Tokens de acceso" sección Hola [conectar servicios de tooMedia con hello SDK de servicios multimedia para .NET] tema.

### <a name="dec_13_donnet_ext_changes"></a>Extensiones del SDK .NET de Servicios multimedia de Azure 2.0.0.0
Hello Azure Media Services .NET SDK Extensions es un conjunto de métodos de extensión y funciones auxiliares que simplifican el código y que sea más fácil toodevelop con servicios multimedia de Azure. Puede obtener los bits más recientes de hello en [Azure Media Services .NET SDK Extensions].

## <a id="november_changes_13"></a>Versión de noviembre de 2013
### <a name="nov_13_donnet_changes"></a>Cambios en el SDK .NET de Servicios multimedia de Azure
A partir de esta versión, Hola SDK de servicios multimedia para .NET controla los errores transitorios que pueden producirse al realizar la capa de API de REST de servicios multimedia de toohello de llamadas.

## <a id="august_changes_13"></a>Versión de agosto de 2013
### <a name="aug_13_powershell_changes"></a>Cmdlets de PowerShell de Servicios multimedia incluidos en las herramientas del SDK de Azure
Hola siguientes cmdlets de PowerShell de servicios multimedia ahora se incluye en [azure-sdk-tools].

* Get-AzureMediaServices 
  
    Por ejemplo: `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Por ejemplo: `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Por ejemplo: `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Por ejemplo: `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Versión de junio de 2013
### <a name="june_13_general_changes"></a>Cambios en Servicios multimedia de Azure
cambios de Hello mencionados en esta sección son actualizaciones incluidas en hello que libera de servicios multimedia de junio de 2013.

* Capacidad toolink tooa cuenta de servicios multimedia de cuentas de almacenamiento de varios. 
  
    StorageAccount
  
    Asset.StorageAccountName and Asset.StorageAccount
* Capacidad tooupdate Job.Priority. 
* Entidades y propiedades relacionadas con notificaciones: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Trabajo
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Cambios en el SDK .NET de Servicios multimedia de Azure
Hello cambios siguientes se incluyen en junio de 2013 versiones SDK de servicios multimedia. Hello SDK de servicios multimedia más reciente está disponible en GitHub.

* A partir de hello versión 2.3.0.0, Hola SDK de servicios multimedia admite la vinculación tooa varias de las cuentas de almacenamiento cuenta de servicios multimedia. Hello API siguientes admiten esta característica:
  
    Hola IStorageAccount tipo.
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts propiedad.
  
    Hola propiedad StorageAccount.
  
    Hola StorageAccountName propiedad.
  
    Para obtener más información, consulte [Administración de recursos de Servicios multimedia entre varias cuentas de almacenamiento].
* API relacionadas con notificaciones. A partir de hello versión 2.2.0.0 tiene notificaciones de almacenamiento de cola de hello capacidad toolisten tooAzure. Para obtener más información, consulte [Control de notificaciones de trabajo de Servicios multimedia].
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions propiedad.
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint tipo.
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription tipo.
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection tipo.
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType tipo.
  
    Hola Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState tipo.
* Dependencia de hello cliente de almacenamiento de Azure SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Dependencia de OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>Versión de diciembre de 2012
### <a name="dec_12_dotnet_changes"></a>Cambios en el SDK .NET de Servicios multimedia de Azure
* Intellisense: se ha agregado documentación de Intellisense que faltaba para muchos tipos.
* Microsoft.Practices.TransientFaultHandling.Core: se ha corregido un problema donde hello SDK todavía tenía una versión anterior de tooan de dependencia de este ensamblado. Hola SDK ahora referencias versión 5.1.1209.1 de este ensamblado.

Correcciones para problemas encontrados en hello noviembre de 2012 SDK:

* IAsset.Locators.Count: este recuento se notifica ahora correctamente en las nuevas interfaces IAsset después de que todos los localizadores se hayan eliminado.
* IAssetFile.ContentFileSize; este valor está ahora correctamente definido después de una carga por IAssetFile.Upload(filepath).
* IAssetFile.ContentFileSize: esta propiedad se puede establecer ahora al crear un archivo de activo. Anteriormente era de solo lectura.
* Iassetfile.upload (RutaDelArchivo): se ha corregido un problema donde este método carga sincrónica produce Hola tras error al cargar el recurso de toohello de varios archivos. error de Hello es "servidor hello de tooauthenticate solicitudes con error. Compruebe que el valor Hola del encabezado Authorization está formado correctamente incluye firma de Hola".
* IAssetFile.UploadAsync: se ha corregido un problema por el que no más de 5 archivos se podían cargar a la vez.
* IAssetFile.UploadProgressChanged: Hola SDK ahora proporciona este evento.
* IAssetFile.DownloadAsync(string, BlobTransferClient, ILocator, CancellationToken): ahora se proporciona esta sobrecarga del método.
* IAssetFile.DownloadAsync: se ha corregido un problema en el que no más de 5 archivos se podían descargar a la vez.
* Iassetfile.Delete (): Se corrigió un problema donde al llamar a delete puede producir una excepción si no se cargó ningún archivo para hello IAssetFile.
* Trabajos: Se corrigió un problema donde el encadenamiento de una "tarea de secuencias de MP4 tooSmooth" con una "PlayReady Protection tarea" mediante una plantilla de trabajo no creará las tareas en absoluto.
* Encryptionutils.getcertificatefromstore (): Este método ya no produce una excepción de referencia nula debido a errores de tooa buscar certificados de hello en función de los problemas de configuración de certificados.

## <a id="november_changes_12"></a>Versión de noviembre de 2012
Hello cambios mencionados en esta sección eran actualizaciones incluidas en hello noviembre de 2012 (versión 2.0.0.0) SDK. Estos cambios pueden requerir cualquier código escrito de hello junio de 2012 preview SDK versión toobe modificación o reescritura.

* Recursos
  
    IAsset.Create (assetname) es la función de creación de hello sólo activos. IAsset.Create ya no carga archivos como parte de la llamada al método de Hola. Use IAssetFile para cargar.
  
    método IAsset.Publish de Hola y valor de enumeración de hello AssetState.Publish se han quitado de hello SDK de servicios. Todo código que dependa de este valor se debe reescribir.
* FileInfo
  
    Esta clase se ha eliminado y se ha sustituido por IAssetFile.
  
    IAssetFiles
  
    IAssetFile sustituye a FileInfo y tiene un comportamiento diferente. toouse, crear una instancia de objeto de hello IAssetFiles, seguido de una carga de archivo usando Hola SDK de servicios multimedia o hello SDK de almacenamiento de Azure. Hola siguiendo las sobrecargas de IAssetFile.Upload puede utilizarse:
  
  * Iassetfile.upload (RutaDelArchivo): Método sincrónico que bloquea el subproceso de Hola y se recomienda sólo al cargar un único archivo.
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken): un método asincrónico. Este es el mecanismo de carga de hello preferido. 
    
    Problema conocido: usar Hola cancellationToken cancelará carga Hola; Sin embargo, estado de cancelación de Hola de tareas de hello puede ser cualquier número de Estados. Debe capturar y gestionar correctamente las excepciones.
* Localizadores
  
    se han quitado las versiones específicas del origen de Hola. contexto de Hello específico de SAS. Locators.CreateSasLocator (asset, accessPolicy) se marcarán en desuso o se quitan por versión de GA. Vea Hola localizadores sección en nuevas funciones para el comportamiento actualizado.

## <a id="june_changes_12"></a>Versión de vista previa de junio de 2012
Hola después funcionalidad era nuevo en la versión de noviembre de Hola de hello SDK.

* Eliminación de entidades
  
    IAsset, IAssetFile, ILocator, IAccessPolicy y IContentKey objetos se han eliminado en el nivel de objeto de hello, es decir, IObject.Delete (), en lugar de requerir la eliminación en hello colección, que es cloudmediacontext.objCollection.Delete (objinstance).
* Localizadores
  
    Localizadores ahora se debe crear mediante el método de hello CreateLocator y utilizar valores de enumeración LocatorType.SAS o LocatorType.OnDemandOrigin Hola como un argumento de tipo de localizador específico Hola desea toocreate.
  
    Se han agregado nuevas propiedades tooLocators toomake se tooobtain más fácil de URI que puedan usarse para su contenido. Este nuevo diseño de localizadores estaba destinada a tooprovide más flexibilidad para extensibilidad futura de terceros y aumentar la facilidad de uso para aplicaciones cliente multimedia.
* Compatibilidad con el método asincrónico
  
    Se ha agregado compatibilidad asincrónica tooall métodos.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[foro de MSDN de Azure Media Services]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[Azure Media Services REST API Reference]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[Detalles de precios de Servicios multimedia]: http://azure.microsoft.com/pricing/details/media-services/
[entrada metadatos]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[metadatos de salida]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[entregar contenido]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[Indización de archivos multimedia con Azure Media Indexer]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[trabajo con el streaming en vivo de Azure Media Services]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[Uso del cifrado dinámico AES-128 y del servicio de entrega de claves]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[Uso del cifrado dinámico de PlayReady y servicio de entrega de licencias]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Información general de plantillas de licencias de PlayReady de Servicios multimedia]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[Streaming de contenido cifrado de almacenamiento]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[empaquetado dinámico]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[blog de Nick Drouin]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[protección de Smooth Streaming con PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[lógica de reintento en hello SDK de servicios multimedia para .NET]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Grass Valley anuncia EDIUS 7 Streaming a través de hello en la nube]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[Control de nombres de archivo de salida del codificador de Servicios multimedia]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[Creación de superposiciones]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Unión de segmentos de vídeo]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[las versiones de Azure Media Services .NET SDK 3.0.0.1 y 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory Access Control Service (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[conectar servicios de tooMedia con hello SDK de servicios multimedia para .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Azure Media Services .NET SDK Extensions]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Administración de recursos de Servicios multimedia entre varias cuentas de almacenamiento]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[Control de notificaciones de trabajo de Servicios multimedia]: http://msdn.microsoft.com/library/azure/dn261241.aspx

