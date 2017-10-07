---
title: conceptos de servicios multimedia de aaaAzure | Documentos de Microsoft
description: "En este tema se proporciona información general sobre los conceptos de Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Conceptos de Azure Media Services
En este tema se ofrece una visión general de conceptos más importantes de servicios multimedia de Hola.

## <a id="assets"></a>Activos y almacenamiento
### <a name="assets"></a>Recursos
Un [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) contiene archivos digitales (como vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y subtítulos) y Hola metadatos acerca de estos archivos. Una vez cargados los archivos digitales de hello en un recurso, se puede usar en los servicios de multimedia de Hola de codificación y streaming flujos de trabajo.

Un recurso es el contenedor de blob de tooa asignada en la cuenta de almacenamiento de Azure de Hola y archivos de hello en activos de Hola se almacenan como blobs en bloques en ese contenedor. Azure Media Services no admite los blobs en páginas.

La hora de decidir qué tooupload contenido multimedia y almacenar en un recurso, se aplica Hola siguientes consideraciones:

* Un recurso debe contener solo una instancia única de contenido multimedia. Por ejemplo, una edición única de un episodio de televisión, una película o un anuncio.
* Un recurso no puede contener varias representaciones o ediciones de un archivo audiovisual. Un ejemplo de uso indebido de un recurso sería el intento toostore más de un episodio de TV, anuncio o varios ángulos de cámara desde una sola producción dentro de un recurso. Almacenar varias representaciones o ediciones de un archivo audiovisual en un recurso puede dar lugar a problemas al enviar trabajos de codificación, transmisión por secuencias y proteger la entrega de Hola de recurso de hello más tarde en el flujo de trabajo de Hola.  

### <a name="asset-file"></a>Archivo de recursos
Un [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa un archivo de vídeo o audio real almacenado en un contenedor de blobs. Un archivo de recursos siempre está asociado con un recurso y un recurso puede contener uno o varios archivos. se produce un error en la tarea de codificador de servicios multimedia de Hello si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.

Hola **AssetFile** instancia y archivo de hello multimedia real son dos objetos diferentes. instancia de AssetFile Hola contiene metadatos sobre archivo multimedia de hello, mientras que el archivo de medios de hello contiene contenido multimedia real de Hola.

No debería intentar toochange contenido de Hola de contenedores de blob generados por los servicios multimedia sin usar las API de servicio de medios.

### <a name="asset-encryption-options"></a>Opciones de cifrado de recursos
Dependiendo del tipo hello de contenido que desee tooupload, la tienda y la entrega, servicios multimedia ofrecen diversas opciones de cifrado en las que puede elegir.

>[!NOTE]
>No se utiliza cifrado. Se trata de un valor predeterminado de Hola. Cuando se utiliza esta opción, el contenido no está protegido en tránsito o en reposo en el almacenamiento.

Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use este tooupload opción su contenido.

**StorageEncrypted** : Use esta opción tooencrypt el contenido no localmente mediante el cifrado de AES 256 bits y, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo. Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo. caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure sitúe los archivos multimedia de entrada de gran calidad con cifrado de alta seguridad en disco. 

En orden toodeliver un recurso cifrado de almacenamiento, debe configurar Directiva de entrega del activo de Hola para que Servicios multimedia sepa cómo desea toodeliver su contenido. Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega (por ejemplo, AES, PlayReady o sin cifrado). 

**CommonEncryptionProtected** -Utilice esta opción si desea que tooencrypt (o carga ya cifrado) contenido con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).

**EnvelopeEncryptionProtected** : Utilice esta opción si desea que tooprotect (o carga ya protegido) HTTP Live Streaming (HLS) cifrado con Advanced Encryption Standard (AES). Si carga HLS ya cifrado con AES, se debe haber cifrado con Transform Manager.

### <a name="access-policy"></a>Directiva de acceso
Un [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) define permisos (como lectura, escritura y lista) y la duración del activo de tooan de acceso. Normalmente pasará un localizador de tooa de objeto de AccessPolicy que, a continuación, se usa tooaccess archivos de hello contenidos en un recurso.

>[!NOTE]
>Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .

### <a name="blob-container"></a>Contenedor de blobs
Un contenedor de blobs proporciona una agrupación de un conjunto de blobs. Los contenedores de blobs se usan en Servicios multimedia como punto limítrofe para el control de acceso y localizadores de firma de acceso compartido (SAS) en los recursos. Una cuenta de almacenamiento de Azure puede contener una cantidad ilimitada de contenedores de blobs. un contenedor puede almacenar un número ilimitado de blobs.

>[!NOTE]
> No debería intentar toochange contenido de Hola de contenedores de blob generados por los servicios multimedia sin usar las API de servicio de medios.
> 
> 

### <a id="locators"></a>Localizadores
[Localizador](https://docs.microsoft.com/rest/api/media/operations/locator)s proporcionar un hello tooaccess de punto de entrada a los archivos contenidos en un recurso. Una directiva de acceso es toodefine usado Hola permisos y la duración que un cliente tiene tooa de acceso dada activo. Puede haber una relación de tooone múltiple con una directiva de acceso, por ejemplo, que distintos localizadores pueden proporcionar diferentes horas iniciales y los clientes de toodifferent de tipos de conexión mientras trabaja con todos los Hola mismo permiso y la configuración de duración; Sin embargo, debido a una restricción de directiva de acceso compartido a los servicios de almacenamiento de Azure, no puede tener más de cinco localizadores únicos asociados a un recurso al mismo tiempo. 

Servicios multimedia admite dos tipos de localizadores: localizadores OnDemandOrigin, usó toostream medios (por ejemplo, MPEG DASH, HLS o Smooth Streaming) o descargar progresivamente multimedia y localizadores de URL de SAS, tooupload usado o/de descarga medios archivos desde el almacenamiento de Azure. 

>[!NOTE]
>permiso de lista de Hello (AccessPermissions.List) no debe usarse al crear un localizador OnDemandOrigin. 

### <a name="storage-account"></a>Cuenta de almacenamiento
Todos los tooAzure acceso almacenamiento se realiza a través de una cuenta de almacenamiento. Una cuenta de Servicios multimedia se puede asociar con una o más cuentas de almacenamiento. Una cuenta puede contener una cantidad ilimitada de contenedores, siempre que su tamaño total no supere los 500 TB por cuenta de almacenamiento.  Los servicios multimedia proporcionan herramientas tooallow de nivel SDK toomanage varias cuentas de almacenamiento y carga equilibrar la distribución Hola de sus recursos durante la carga toothese cuentas basadas en métricas y distribución aleatoria. Para obtener más información, consulte Uso de [Almacenamiento de Azure](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Trabajos y tareas
A [trabajo](https://https://docs.microsoft.com/rest/api/media/operations/job) es tooprocess normalmente se usan (por ejemplo, índice o codificar) una presentación de audio/vídeo. Si está procesando varios vídeos, cree un trabajo para cada toobe vídeo codificado.

Un trabajo contiene metadatos sobre toobe de procesamiento de hello realiza. Cada trabajo contiene una o varias [tareas](https://docs.microsoft.com/rest/api/media/operations/task)que especifican una tarea de procesamiento atómica, sus recursos de entrada, recursos de salida, un procesador de multimedia y su configuración asociada. Es posible encadenar tareas dentro de un trabajo, donde se indica el recurso de salida de hello de una tarea como hello toohello siguiente tarea de activos de entrada. De esta manera un trabajo puede contener todo procesamiento Hola necesario para ver una presentación multimedia.

## <a id="encoding"></a>Codificación
Servicios multimedia de Azure proporciona varias opciones para la codificación de Hola de medios en la nube de Hola.

Al iniciar la con los servicios multimedia, es importante toounderstand Hola diferencia entre códecs y formatos de archivo.
Los códecs son software Hola que implementa los algoritmos de compresión y descompresión de hello, mientras que los formatos de archivo son contenedores que alojan el vídeo comprimido de Hola.

Servicios multimedia proporciona empaquetado dinámico que permite toodeliver la velocidad de bits adaptativa MP4 o Smooth Streaming con codificación de contenido de transmisión por secuencias formatos admitidos por los servicios multimedia (MPEG DASH, HLS, Smooth Streaming) sin necesidad de toore-package en estos formatos de transmisión por secuencias.

aprovechar tootake [empaquetado dinámico](media-services-dynamic-packaging-overview.md), necesita tooencode su archivo intermedio (origen) en un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa y tener al menos un extremo de transmisión por secuencias estándar o premium en estado iniciado.

Servicios multimedia admite Hola después de codificadores a petición que se describen en este artículo:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Flujo de trabajo del Codificador multimedia](media-services-encode-asset.md#media-encoder-premium-workflow)

Para obtener información acerca de los codificadores compatibles, consulte [Codificadores](media-services-encode-asset.md).

## <a name="live-streaming"></a>Streaming en directo
En Servicios multimedia de Azure, un canal representa una canalización para procesar contenido de streaming en directo. Los canales reciben el flujo de entrada en directo de dos maneras posibles:

* Un codificador en directo local envía Smooth Streaming (MP4 fragmentado) toohello canal o RTMP de velocidades de bits. Puede usar Hola siguientes codificadores en directo que generan Smooth Streaming de velocidades de bits: MediaExcel, Ateme, Imagine las comunicaciones, Envivio, Cisco y Elemental. Hello siguientes codificadores en directo de salida RTMP: codificadores Adobe Flash Live codificador Telestream Wirecast, Teradek, Haivision y Tricaster. Hello secuencias introducidas pasan a través de canales sin codificación y transcodificación adicionales. Cuando se solicita, servicios multimedia transmite hello secuencia toocustomers.
* Una secuencia de velocidad de bits única (en uno de hello siguientes formatos: RTP (MPEG-TS)), RTMP o Smooth Streaming (MP4 fragmentado)) se envía toohello canal que está habilitado tooperform live codificar con servicios multimedia. Hola canal, a continuación, realiza la codificación en directo de Hola entrante velocidad de bits única secuencia tooa bits múltiple (adaptable) secuencia de vídeo. Cuando se solicita, servicios multimedia transmite hello secuencia toocustomers.

### <a name="channel"></a>Canal
En Servicios multimedia, los [canal](https://docs.microsoft.com/rest/api/media/operations/channel)es son los responsables de procesar el contenido de streaming en vivo. Un canal proporciona un extremo de entrada (URL de introducción) que, a continuación, proporcionar transcodificador tooa. canal de Hello recibe las secuencias de entrada en directo de Transcodificador de Hola y pone a disposición de streaming a través de uno o más StreamingEndpoints. Los canales también proporcionan un extremo de vista previa (URL de vista previa) que use toopreview y validar las secuencias antes del procesamiento y entrega.

Puede obtener Hola introducir la dirección URL y la dirección URL de vista previa de hello al crear el canal de Hola. tooget estas direcciones URL, canal de hello no tiene toobe en estado de hello iniciado. Cuando esté listo toostart insertar datos de un transcodificador en vivo en canal de hello, se debe iniciar el canal de Hola. Una vez Hola transcodificador inicia la introducción de datos, puede obtener una vista previa de la secuencia.

Cada cuenta de Servicios multimedia puede contener varios canales, varios programas y varios StreamingEndpoints. Función de necesidades de ancho de banda y seguridad hello, servicios de StreamingEndpoint pueden ser tooone dedicado o más canales. Puede extraer cualquier StreamingEndpoint de cualquier canal.

### <a name="program-event"></a>Programa (evento)
A [programa (evento)](https://docs.microsoft.com/rest/api/media/operations/program) permite la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo. Los canales administran los programas (eventos). Hello relación de canales y los programas es un medio tootraditional similar donde un canal tiene un flujo constante de contenido y un programa es toosome ámbito ha superado el tiempo de evento en ese canal.
Puede especificar Hola número de horas que quiere tooretain Hola registran contenido de programa Hola, establecer hello **ArchiveWindowLength** propiedad. Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas.

ArchiveWindowLength también determina la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola. Programas pueden ejecutarse durante el período de tiempo especificado de hello, pero se descarta continuamente contenido que queda fuera de la longitud de la ventana de Hola. El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.

Cada programa (evento) está asociado a un recurso. programa de hello toopublish debe crear un localizador para hello asociado activo. Este localizador permitirá toobuild una URL de streaming puede proporcionar a los clientes de tooyour.

Un canal admite hasta toothree programas en ejecución al mismo tiempo para que pueda crear varios archivos de hello mismo flujo entrante. Esto le permite toopublish y archivar diferentes partes de un evento según sea necesario. Por ejemplo, sus necesidades de negocio es tooarchive 6 horas de un programa, pero toobroadcast solo últimos 10 minutos. tooaccomplish, necesita toocreate dos programas en ejecución simultáneos. Un programa se establece tooarchive 6 horas de evento de hello pero no se publica el programa Hola. Hello otro programa es conjunto tooarchive durante 10 minutos y se publica este programa.

Para más información, consulte:

* [Trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md)
* [Uso de canales que reciben streaming en vivo con velocidad de bits múltiple de codificadores locales](media-services-live-streaming-with-onprem-encoders.md)
* [Cuotas y limitaciones](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>Protección del contenido
### <a name="dynamic-encryption"></a>Cifrado dinámico
Servicios multimedia de Azure permite toosecure su media de tiempo de hello sale del equipo a través de almacenamiento, procesamiento y entrega. Servicios multimedia permite toodeliver el contenido cifrado dinámicamente con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits) y el cifrado común (CENC) con PlayReady o Widevine DRM. Servicios multimedia también proporciona un servicio de entrega de claves de AES y los clientes tooauthorized de licencias de PlayReady.

Actualmente, puede cifrar los siguientes formatos de streaming de Hola: HLS, MPEG DASH y Smooth Streaming. No se pueden cifrar las descargas progresivas.

Si desea para servicios multimedia tooencrypt un recurso, es necesario tooassociate una clave de cifrado (CommonEncryption o EnvelopeEncryption) con el recurso y configurar directivas de autorización para la clave de Hola.

Si desea toostream un recurso cifrado de almacenamiento, debe configurar la directiva de entrega del activo de hello en orden toospecify cómo desea toodeliver su activo.

Cuando un Reproductor solicita una secuencia, los servicios multimedia usa Hola especificado toodynamically clave cifrar el contenido con un cifrado de sobre (con AES) o el cifrado común (con PlayReady o Widevine). secuencia de hello toodecrypt, Hola Reproductor solicitará clave Hola del servicio de entrega de claves de Hola. toodecide si es usuario de hello autorizado tooget clave de hello, servicio de hello evalúa las directivas de autorización de Hola que especificó para la clave de Hola.

### <a name="token-restriction"></a>Restricción de token
Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: abra, restricción de tokens o restricción de IP. directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS). Servicios multimedia admite tokens con formato Simple Web Tokens (SWT) de Hola y el formato de JSON Web Token (JWT). Los Servicios multimedia no proporcionan Servicios de tokens seguros. Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue. Hola STS debe estar configurado toocreate un token firmado con hello especificado clave y emitir notificaciones que especificó en la configuración de restricción de token de Hola. Servicios de multimedia de Hello servicio de entrega de claves devolverá Hola solicitado Hola y cliente de toohello (o licencias) de la clave si Hola token es válido notificaciones Hola token coinciden con las configuradas para las claves de hello (o licencias).

Al configurar la directiva restringida de tokens de hello, debe especificar la clave de verificación principal hello, emisor y parámetros de audiencia. clave de verificación principal Hello contiene Hola clave que Hola token se firmó con, el emisor es Hola servicio de token seguro que emite el token de Hola. audiencia de Hello (a veces denominado ámbito) describe intención de hello del token de Hola u Hola recursos Hola token autoriza acceso. Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola.

Para obtener más información, vea Hola siguientes artículos:

[Introducción a la protección de contenido](media-services-content-protection-overview.md)
[Protección con AES-128](media-services-protect-with-aes128.md)
[Protección con DRM](media-services-protect-with-drm.md)

## <a name="delivering"></a>Entrega
### <a id="dynamic_packaging"></a>Empaquetado dinámico
Cuando se trabaja con servicios multimedia, se recomienda tooencode los archivos intermedios en una velocidad de bits adaptativa MP4 establezca y, a continuación, convierta Hola establece toohello formato deseado con hello [empaquetado dinámico](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>punto de conexión de streaming
Un elemento StreamingEndpoint representa un servicio de streaming que puede entregar contenido directamente tooa aplicación de reproducción de cliente o tooa red de entrega de contenido (CDN) para su distribución posterior (servicios multimedia de Azure ahora proporciona integración de Azure CDN Hola.) Hola flujo de salida de un servicio de transmisión de punto de conexión puede ser una secuencia en directo o un recurso de vídeo a petición en su cuenta de servicios multimedia. Los clientes de servicios multimedia eligen un **estándar** streaming extremo o uno o varios **Premium** puntos de conexión, según las necesidades de tootheir de transmisión por secuencias. El punto de conexión de streaming estándar es adecuado para la mayoría de las cargas de trabajo de streaming. 

El punto de conexión de streaming estándar es adecuado para la mayoría de las cargas de trabajo de streaming. Los puntos de conexión estándar de transmisión por secuencias ofrecen Hola flexibilidad toodeliver su contenido toovirtually todos los dispositivos a través de empaquetado dinámico en HLS, MPEG-DASH y Smooth Streaming, así como el cifrado dinámico de Microsoft PlayReady, Google Widevine, Fairplay de Apple y AES128.  También se adaptan desde muy pequeño toovery audiencias grandes con miles de visores simultáneos a través de la integración de CDN de Azure. Si tiene una carga de trabajo avanzada o toostandard objetivos de rendimiento de extremo de transmisión por secuencias no ajustan a sus necesidades de capacidad de transmisión por secuencias o si desea toocontrol capacidad de Hola de hello StreamingEndpoint servicio toohandle cada vez más ancho de banda de es necesario, se recomienda tooallocate unidades de escala (también conocido como premium unidades de streaming).

Se recomienda el empaquetado dinámico toouse o cifrado dinámico.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

Para obtener más información, consulte [este tema](media-services-portal-manage-streaming-endpoints.md) .

De forma predeterminada puede tener hasta los extremos de streaming de too2 en su cuenta de servicios multimedia. toorequest un límite superior, consulte [cuotas y limitaciones](media-services-quotas-and-limitations.md).

Solo se le cobrará cuando StreamingEndpoint esté en estado en ejecución.

### <a name="asset-delivery-policy"></a>Directiva de entrega de recursos
Uno de hello pasos Hola servicios multimedia es la configuración de flujo de trabajo de entrega de contenido [directivas de entrega de activos ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)que desea toobe transmite por secuencias. Directiva de entrega del activo de Hello indica los servicios multimedia cómo desea para su toobe asset entregado: en el protocolo de transmisión por secuencias que debe su activo dinámicamente empaquetarse (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), si no desea toodynamically cifrar un activo y cómo (sobre o cifrado común).

Si tiene un activo cifrado del almacenamiento, antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega. Por ejemplo, toodeliver su activo cifrado con clave de cifrado estándar de cifrado avanzado (AES), tooDynamicEnvelopeEncryption del tipo de directiva de conjunto Hola. cifrado de almacenamiento de tooremove y los activos de hello secuencia de hello claro, establezca tooNoDynamicEncryption de tipo de directiva de Hola.

### <a name="progressive-download"></a>Descarga progresiva
La descarga progresiva permite toostart reproducir contenido multimedia antes de que se ha descargado todo el archivo hello. Solo puede descargar progresivamente un archivo MP4.

>[!NOTE]
>Debe descifrar los recursos cifrados si desea toobe disponible para la descarga progresiva.

los usuarios de tooprovide con progresiva descargar las direcciones URL, primero debe crear un localizador OnDemandOrigin. Creación de hello localizador, proporciona Hola activos de toohello de ruta de acceso base. A continuación, necesita nombre de hello tooappend de archivo MP4. Por ejemplo:

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>Direcciones URL de streaming
Transmisión por secuencias el contenido tooclients. tooprovide usuarios con direcciones URL de streaming, primero debe crear un localizador OnDemandOrigin. Creación de hello localizador, proporciona Hola base asset toohello de ruta de acceso que contiene el contenido de Hola que desee toostream. Sin embargo, toobe toostream capaz de este contenido debe toomodify esta ruta de acceso. tooconstruct una dirección URL completa se toohello transmisión por secuencias de archivo de manifiesto, debe concatenar la ruta de acceso del localizador de hello hello y valor de manifiesto (filename.ism) nombre de archivo. A continuación, anexe/manifest y una ruta de acceso del localizador de toohello de formato apropiado (si es necesario).

También puede transmitir el contenido por una conexión SSL. toodo esto, asegúrese de que la transmisión por secuencias de inicio de las direcciones URL con HTTPS. Actualmente, AMS no admite SSL con dominios personalizados.  

>[!NOTE]
>Solo puede transmitir a través de SSL si Hola origen desde el que entrega el contenido se creó después de 10 de septiembre de 2014. Si sus direcciones URL de streaming se basan en hello streaming creados después del 10 de septiembre, dirección URL de hello contiene "streaming.mediaservices.windows.net" (nuevo formato de hello). Direcciones URL de streaming que contienen "origin.mediaservices.windows.net" (formato antiguo de hello) no son compatibles con SSL. Si la dirección URL está en formato antiguo de Hola y desea toobe pueda toostream a través de SSL, cree un nuevo extremo de transmisión por secuencias. Utilice direcciones URL creadas en hello nuevos streaming extremo toostream su contenido a través de SSL.

Hola lista siguiente describe los diferentes formatos de streaming y proporciona ejemplos:

* Smooth Streaming

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

* MPEG DASH

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

* Apple HTTP Live Streaming (HLS) V4

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

* Apple HTTP Live Streaming (HLS) V3

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

