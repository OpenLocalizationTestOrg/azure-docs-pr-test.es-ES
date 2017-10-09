---
title: "aaaGet se inició con la entrega de contenido a petición con .NET | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de Hola de implementar una aplicación de entrega de contenido de petición de servicios multimedia de Azure con. NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Introducción a la entrega de contenido a petición mediante .NET SDK
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Este tutorial le guiará por los pasos de saludo de la implementación de un servicio de entrega de contenido de vídeo bajo demanda (VoD) básico con aplicación de servicios de multimedia de Azure (AMS) mediante hello Azure Media Services .NET SDK.

## <a name="prerequisites"></a>Requisitos previos

tutorial de hello toocomplete necesarios son las siguientes de Hello:

* Una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* Una cuenta de Media Services. toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).
* .NET Framework 4.0 o posterior.
* Visual Studio.

Este tutorial incluye Hola siguientes tareas:

1. Iniciar el origen (con hello portal de Azure).
2. Creación y configuración de un proyecto de Visual Studio.
3. Conecte la cuenta de servicios multimedia de toohello.
2. Carga de un archivo de vídeo.
3. Codificar el archivo de código fuente de hello en un conjunto de archivos MP4 de velocidad de bits adaptativa.
4. Publicar los activos de Hola y get de transmisión por secuencias y direcciones URL de descarga progresiva.  
5. Reproduzca el contenido.

## <a name="overview"></a>Información general
Este tutorial le guiará por los pasos de saludo de la implementación de una aplicación de entrega de contenido de vídeo bajo demanda (VoD) mediante servicios de multimedia de Azure (AMS) SDK para. NET.

tutorial de Hello presenta el flujo de trabajo de hello básico de servicios multimedia y objetos de programación más habituales de Hola y las tareas necesarias para el desarrollo de servicios multimedia. Complete Hola tutorial Hola, se le pueda toostream o descargar progresivamente un archivo multimedia de ejemplo que cargar, codificado y descarga.

### <a name="ams-model"></a>Modelo AMS

Hello siguiente imagen muestra algunos de los objetos de hello suelen usada al desarrollar aplicaciones de VoD en modelo de OData de servicios multimedia de Hola.

Haga clic en tooview de imagen de hello tamaño completo.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

Puede ver todo el modelo de hello [aquí](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Iniciar la transmisión de los extremos que usan Hola portal de Azure

Cuando se trabaja con uno de los escenarios más comunes de hello es entregar vídeo a través de la velocidad de bits de transmisión por secuencias adaptativa de servicios de multimedia de Azure. Servicios multimedia proporciona empaquetado dinámico, lo que permite toodeliver la velocidad de bits adaptativa MP4 codificados contenido de transmisión por secuencias formatos admitidos por servicios multimedia (MPEG DASH, HLS, Smooth Streaming) just-in-time, sin necesidad de toostore preempaquetado versiones de cada uno de estos formatos de transmisión por secuencias.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.

toostart Hola extremo de streaming, Hola siguientes:

1. Inicie sesión en hello [portal de Azure](https://portal.azure.com/).
2. En la ventana de configuración de hello, haga clic en los puntos de conexión de la transmisión por secuencias.
3. Haga clic en predeterminada Hola extremo de streaming.

    Aparecerá la ventana de detalles predeterminada del extremo de transmisión por secuencias de Hola.

4. Haga clic en el icono de inicio de Hola.
5. Haga clic en botón toosave de hello guardar los cambios.

## <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

1. Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 
2. Cree una nueva carpeta (carpeta puede estar en cualquier parte en la unidad local) y copie un archivo. mp4 que se desean tooencode y el flujo o descarga progresiva. En este ejemplo, se utiliza la ruta de acceso de Hola "C:\VideoFiles".

## <a name="connect-toohello-media-services-account"></a>Conectar la cuenta de servicios multimedia de toohello

Al utilizar los servicios multimedia con. NET, debe utilizar hello **CloudMediaContext** clase para la mayoría de los servicios multimedia tareas de programación: conexión de cuenta de servicios de tooMedia; crear, actualizar, obtener acceso a y eliminar siguiente Hola objetos: activos, los archivos de recursos, trabajos, las directivas de acceso, localizadores y etcetera.

Sobrescribir clase de programa Hola predeterminada con el siguiente código de hello. Hello código se muestra cómo la conexión de hello tooread los valores del archivo App.config de hello y cómo hello toocreate **CloudMediaContext** de servicios de objeto en orden tooconnect tooMedia. Para obtener más información, consulte [toohello API de servicios multimedia de conexión](media-services-use-aad-auth-to-access-ams-api.md).

Asegúrese de que tooupdate Hola archivo nombre y ruta de acceso toowhere que tiene el archivo multimedia.

Hola **Main** función llama a métodos que se definirá más adelante en esta sección.

> [!NOTE]
> Hasta que agregue las definiciones para todas las funciones de saludo se está recibiendo errores de compilación.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Creación de un nuevo recurso y carga de un archivo de vídeo

En Media Services, cargará (o especificará) los archivos digitales en un recurso. Hola **Asset** entidad puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.)  Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias. se denominan archivos Hello en activos de hello **archivos de recursos**.

Hola **UploadFile** método definido por debajo de las llamadas **CreateFromFile** (definido en las extensiones de SDK. NET). **CreateFromFile** crea un nuevo recurso en qué Hola se carga el archivo de origen especificado.

Hola **CreateFromFile** método toma **AssetCreationOptions** que le permite especificar una de las siguientes opciones de creación de activos de Hola:

* **Ninguno** : no se utiliza cifrado. Se trata de un valor predeterminado de Hola. Tenga en cuenta que al usar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.
  Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use esta opción.
* **StorageEncrypted** -Utilice esta opción tooencrypt el contenido no localmente mediante cifrado de bits-256. estándar de cifrado avanzado (AES), que, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo. Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo. caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure los archivos multimedia de entrada de alta calidad con cifrado de alta seguridad en reposo en el disco.
* **CommonEncryptionProtected** : use esta opción si va a cargar contenido que ya se cifró y protegió con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).
* **EnvelopeEncryptionProtected** : use esta opción si va a cargar HLS cifrado con AES. Tenga en cuenta que deben ha codificado y cifrado con Transform Manager archivos Hola.

Hola **CreateFromFile** método también le permite especificar una devolución de llamada en orden tooreport Hola progreso de la carga de archivo hello.

En el siguiente ejemplo de Hola, especificamos **ninguno** para opciones de hello activos.

Agregar Hola después de la clase de método toohello Program.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Codificar el archivo de código fuente de hello en un conjunto de archivos MP4 de velocidad de bits adaptativa
Después de la introducción de activos en los servicios multimedia, medios puede realizarse en codificar, transmultiplexar, marca de agua y así sucesivamente, antes de que se entregue tooclients. Estas actividades se programen y se ejecutarán varias fondo rol instancias tooensure alto rendimiento y disponibilidad. Estas actividades se denominan trabajos y cada trabajo está compuesto de tareas atómicas que Hola trabajo real en el archivo de recursos de Hola.

Tal y como se mencionó anteriormente, cuando se trabaja con servicios multimedia de Azure, uno de los escenarios más comunes de hello está proporcionando la velocidad de bits adaptativa tooyour clientes de transmisión por secuencias. Servicios multimedia dinámicamente puede empaquetar un conjunto de archivos MP4 de velocidad de bits adaptativa en uno de hello siguientes formatos: HTTP Live Streaming (HLS), Smooth Streaming y MPEG DASH.

tootake ventaja de los paquetes dinámicos, necesitará tooencode o transcodificar el archivo mezzanine (origen) en un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa.  

Hola siguiente código muestra cómo toosubmit una codificación de trabajo. trabajo Hello contiene una tarea que especifica el archivo mezzanine de tootranscode hello en un conjunto de velocidad de bits adaptativa MP4s utilizando **Media Encoder estándar**. código de Hello envía trabajo hello y espera hasta que se complete.

Una vez que se complete el trabajo de hello, podría ser capaz de toostream su activo o descargar progresivamente archivos MP4 creados como resultado de transcodificación.

Agregar Hola después de la clase de método toohello Program.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Publicar el recurso de Hola y obtener las direcciones URL de descarga progresiva y transmisión por secuencias

toostream o descarga un recurso, primero necesita demasiado "publicar", mediante la creación de un localizador. Los localizadores proporcionan toofiles de acceso que contiene el recurso de Hola. Servicios multimedia admite dos tipos de localizadores: OnDemandOrigin localizadores, toostream usa medios (por ejemplo, MPEG DASH, HLS o Smooth Streaming) y localizadores de Access Signature (SAS), los archivos de medios de toodownload (para obtener más información sobre, consulte localizadores SAS utilizan[esto](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).

### <a name="some-details-about-url-formats"></a>Algunos detalles sobre los formatos de direcciones URL

Después de crear los localizadores de hello, puede crear direcciones URL de Hola que estaría toostream usado o descargar los archivos. ejemplo de Hola en este tutorial darán como resultado las direcciones URL que puede pegar en exploradores adecuados. En esta sección se incluyen breves ejemplos del aspecto de los diferentes formatos.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>Una dirección URL de streaming de MPEG DASH tiene Hola siguiendo el formato:

{nombre del punto de conexión de streaming-nombre de la cuenta de media services}.streaming.mediaservices.windows.net/{id. de localizador}/{nombre del archivo}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>Una dirección URL de streaming para HLS tiene Hola siguiendo el formato:

{nombre del punto de conexión de streaming-nombre de la cuenta de media services}.streaming.mediaservices.windows.net/{id. de localizador}/{nombre del archivo}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Una dirección URL de streaming para Smooth Streaming tiene Hola siguiendo el formato:

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Archivos de toodownload de una dirección URL de SAS utilizada tiene Hola siguiendo el formato:

{nombre del contenedor de blobs}/{nombre del recurso}/{nombre del archivo}/{firma de SAS}

Extensiones de SDK de .NET de servicios multimedia proporcionan métodos auxiliares útiles que devuelven un formato direcciones URL para hello activo publican.

Hello código siguiente usa localizadores toocreate de extensiones del SDK para .NET y las direcciones URL de descarga de tooget de transmisión por secuencias y progresiva. código de Hello también muestra cómo toodownload archivos tooa de carpeta local.

Agregar Hola después de la clase de método toohello Program.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>Prueba mediante la reproducción de contenido

Una vez que ejecute el programa Hola definido en la sección anterior de hello, Hola direcciones URL similar siguiente toohello se mostrará en la ventana de la consola de Hola.

Direcciones URL de streaming adaptable:

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

Direcciones URL de descarga progresiva (audio y vídeo).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream el vídeo, pegue la dirección URL en el cuadro de texto de dirección URL de Hola Hola [Reproductor de servicios multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progresiva descargar, pegue una dirección URL en un explorador (por ejemplo, Internet Explorer, Chrome o Safari).

Para obtener más información, vea Hola temas siguientes:

- [Reproducir contenido con reproductores existentes](media-services-playback-content-with-existing-players.md)
- [Desarrollo de aplicaciones para reproductor de vídeo](media-services-develop-video-players.md)
- [Incrustación de un vídeo de transmisión por secuencias adaptativa MPEG-DASH en una aplicación HTML5 con DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Descarga de un ejemplo
ejemplo de código siguiente Hello contiene código de hello que creó en este tutorial: [ejemplo](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
