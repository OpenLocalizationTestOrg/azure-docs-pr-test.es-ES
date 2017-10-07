---
title: "aaaUsing AES-128 dinámicos cifrado y la clave de servicio de entrega | Documentos de Microsoft"
description: "Servicios de multimedia de Microsoft Azure permite toodeliver el contenido cifrado con las claves de cifrado de AES de 128 bits. Servicios multimedia también ofrecen servicio de entrega de claves de Hola que ofrece a los usuarios de tooauthorized de claves de cifrado. Este tema muestra cómo toodynamically cifrar con AES-128 y usar el servicio de entrega de claves de Hola."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>Uso del cifrado dinámico AES-128 y del servicio de entrega de claves
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Información general
> [!NOTE]
> Vea [esto](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) vídeo para obtener información general de cómo tooprotect los medios de contenido con cifrado de AES.
> 
> 

Servicios de multimedia de Microsoft Azure le permite toodeliver Http Live Streaming (HLS) y Smooth Streams cifrado con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits). Servicios multimedia también ofrecen servicio de entrega de claves de Hola que ofrece a los usuarios de tooauthorized de claves de cifrado. Si desea para servicios multimedia tooencrypt un recurso, es necesario tooassociate una clave de cifrado con asset hello y configurar directivas de autorización para la clave de Hola. Cuando un Reproductor solicita una secuencia, los servicios multimedia usa Hola especificado toodynamically clave cifrar el contenido con cifrado de AES. secuencia de hello toodecrypt, Hola Reproductor solicitará clave Hola del servicio de entrega de claves de Hola. toodecide si es usuario de hello autorizado tooget clave de hello, servicio de hello evalúa las directivas de autorización de Hola que especificó para la clave de Hola.

Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave. Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: abrir o símbolo (token) de restricción. directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS). Servicios multimedia admite tokens en hello [Tokens Web simples](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) y [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT). Para obtener más información, consulte [configurar Directiva de autorización de la clave de hello contenido](media-services-protect-with-aes128.md#configure_key_auth_policy).

tootake ventaja del cifrado dinámico, debe toohave un activo que contiene un conjunto de archivos MP4 de velocidad de multibits o archivos de origen Smooth Streaming de velocidades de bits. También necesita directiva de entrega de hello tooconfigure para activos de hello (descrita más adelante en este tema). A continuación, en función de formato de hello especificado en hello transmisión por secuencias de dirección URL, servidor de Streaming a petición de hello garantizará que esa secuencia Hola se entrega en el protocolo de hello que ha elegido. Como resultado, solo tendrá toostore y pago para los archivos de hello en formato de almacenamiento único y el servicio de servicios multimedia creará y proporcionará la respuesta adecuada Hola según las solicitudes de un cliente.

En este tema sería útil toodevelopers que trabajan en aplicaciones que ofrecen contenido multimedia protegido. Hola tema muestra cómo tooconfigure Hola servicio de entrega de clave con directivas de autorización para que sólo los clientes autorizados reciban las claves de cifrado de Hola. También muestra cómo cifrado dinámico toouse.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>Flujo de trabajo de cifrado dinámico AES-128 y del servicio de entrega de claves

Hola siguientes pasos son generales que tendría tooperform para cifrar los recursos con AES, utilizando el servicio de entrega de claves de servicios multimedia de Hola y también cifrado dinámico.

1. [Crear un activo y cargar archivos en el recurso de hello](media-services-protect-with-aes128.md#create_asset).
2. [Codificar el activo de Hola que contiene Hola archivo toohello velocidad de bits adaptativa MP4 conjunto](media-services-protect-with-aes128.md#encode_asset).
3. [Crear una clave de contenido y asociarla a activos de hello codificado](media-services-protect-with-aes128.md#create_contentkey). En servicios multimedia, clave de contenido de hello contiene la clave de cifrado del activo de Hola.
4. [Configurar directiva de autorización de la clave de hello contenido](media-services-protect-with-aes128.md#configure_key_auth_policy). Directiva de autorización de clave de contenido de Hello debe configurarse por parte del usuario y se cumple mediante el cliente de Hola para hello toobe clave contenido entregado toohello cliente.
5. [Configurar directiva de entrega de Hola para un activo](media-services-protect-with-aes128.md#configure_asset_delivery_policy). incluye la configuración de directiva de entrega de Hello: clave de dirección URL de adquisición y el Vector de inicialización (IV) (AES-128 requiere Hola mismo toobe IV proporcionado al cifrar y descifrar), protocolo de entrega (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), Hola tipo de cifrado dinámico (por ejemplo, sobre o sin cifrado dinámico).

    Podría aplicar protocolo tooeach de directivas diferentes en hello mismo activo. Por ejemplo, podría aplicar PlayReady cifrado tooSmooth/DASH y AES Envelope tooHLS. Todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, se agrega una directiva única que solo especifica HLS como protocolo de Hola) se bloqueará de transmisión por secuencias. Hola toothis de excepción es si no tiene definida en absoluto ninguna directiva de entrega de activos. A continuación, todos los protocolos se permitirá en hello clara.

6. [Crear un localizador OnDemand](media-services-protect-with-aes128.md#create_locator) en orden tooget una URL de streaming.

También muestra el tema de Hello [cómo una aplicación cliente puede solicitar una clave de servicio de entrega de claves de hello](media-services-protect-with-aes128.md#client_request).

Encontrará un .NET completo [ejemplo](media-services-protect-with-aes128.md#example) final Hola de tema de Hola.

Hola después de la imagen muestra el flujo de trabajo de Hola que se ha descrito anteriormente. Aquí se utiliza el token de hello para la autenticación.

![Protección con AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

resto Hola de este tema ofrece explicaciones detalladas, ejemplos de código y tootopics de vínculos que le muestran cómo tooachieve Hola tareas descritas anteriormente.

## <a name="current-limitations"></a>Limitaciones actuales
Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.

## <a id="create_asset"></a>Crear un activo y cargar archivos en el recurso de Hola
En orden toomanage, codificar y transmitir sus vídeos, debe cargar primero su contenido en los servicios de multimedia de Microsoft Azure. Una vez cargado, el contenido se almacena de forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias. 

Para obtener información detallada, consulte [Carga de archivos en una cuenta de Servicios multimedia](media-services-dotnet-upload-files.md).

## <a id="encode_asset"></a>Codificar Hola asset contenedor Hola archivo toohello velocidad de bits adaptativa que MP4 establecer
Con cifrado dinámico todo lo que necesita es toocreate un activo que contiene un conjunto de archivos MP4 de velocidad de multibits o archivos de origen Smooth Streaming de velocidades de bits. A continuación, según Hola formato especificado en el manifiesto de Hola o fragmentar la solicitud, Hola servidor se asegurará de que recibe Hola transmisión por secuencias de protocolo de Hola que ha elegido el Streaming a petición. Como resultado, solo tendrá toostore y pago para los archivos de hello en formato de almacenamiento único y el servicio de servicios multimedia creará y proporcionará la respuesta adecuada Hola según las solicitudes de un cliente. Para obtener más información, vea hello [Introducción al empaquetado dinámico](media-services-dynamic-packaging-overview.md) tema.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 
>
>Además, puede toouse toobe el empaquetado dinámico y cifrado dinámico su activo debe contener un conjunto de velocidad de bits adaptativa MP4s o archivos de Smooth Streaming de velocidad de bits adaptativa.

Para obtener instrucciones sobre cómo tooencode, consulte [cómo tooencode un activo con Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Crear una clave de contenido y asociarla a activos de hello codificado
En los servicios multimedia, clave de contenido de hello contiene clave de Hola que desea tooencrypt un activo con.

Para obtener más información, consulte [Creación de la clave de contenido](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurar directiva de autorización de la clave de hello contenido
Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave. Directiva de autorización de clave de contenido de Hello debe configurarse por parte del usuario y cumplir Hola cliente (Reproductor) en orden para hello toobe clave entregado a toohello cliente. Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: abra, restricción de tokens o restricción de IP.

Para obtener información detallada, consulte [Configuración de la directiva de autorización de claves de contenido](media-services-dotnet-configure-content-key-auth-policy.md).

## <a id="configure_asset_delivery_policy"></a>Configuración de directivas de entrega de recursos
Configurar directiva de entrega de hello para el activo. Algunas cosas que Hola configuración de directiva de entrega de activos incluye:

* dirección URL de adquisición de clave de Hola. 
* Hola toouse de Vector de inicialización (IV) para el cifrado de sellado Hola. AES-128 requiere Hola mismo toobe IV proporcionado al cifrar y descifrar. 
* Hola asset protocolo de entrega (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos).
* tipo de Hola de cifrado dinámico (por ejemplo, de sobre AES) o sin cifrado dinámico. 

Para obtener más información, consulte [Configuración de la directiva de entrega de recursos ](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Crear un localizador en orden tooget una URL de streaming de transmisión por secuencias a petición
Deberá tooprovide el usuario con hello transmisión por secuencias de dirección URL para Smooth, DASH o HLS.

> [!NOTE]
> Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.
> 
> 

Para obtener instrucciones sobre cómo toopublish un activo y generar una dirección URL de streaming, vea [generar una dirección URL de streaming](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Obtención de un token de prueba
Obtenga una prueba de token en función de la restricción de token de Hola que se usó para la directiva de autorización de claves de Hola.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

Puede usar hello [AMS Reproductor](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest la secuencia.

## <a id="client_request"></a>¿Cómo el cliente puede solicitar una clave de servicio de entrega de claves de hello?
En el paso anterior de hello, construyen Hola URL que apunta el archivo de manifiesto de tooa. El cliente debe información necesaria de hello tooextract de hello transmisión por secuencias de archivos de manifiesto en orden toomake un servicio de entrega de claves toohello de solicitud.

### <a name="manifest-files"></a>Archivos de manifiesto
cliente de Hello necesita tooextract Hola URL (que también contiene el identificador (kid) de clave) valor de archivo de manifiesto de Hola. cliente de Hello, a continuación, intentará clave de cifrado de hello tooget del servicio de entrega de claves de Hola. Hello cliente también necesita tooextract Hola IV valor y que descifrar stream.hello Hola siguiente fragmento de código se muestra hello <Protection> elemento del manifiesto de Smooth Streaming de Hola.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

En caso de hello de HLS, el manifiesto de la raíz de Hola se divide en archivos de segmento. 

Por ejemplo, es el manifiesto de la raíz de hello: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) que contiene una lista de nombres de archivo de segmento.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

Si abre uno de los archivos de segmento de hello en el editor de texto (por ejemplo, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contiene #EXT-X-clave que indica que ese archivo hello está cifrado.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>Si tiene previsto tooplay un AES cifrado HLS en Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Solicitar una clave de hello del servicio de entrega de claves de Hola

Hello código siguiente muestra cómo toosend una toohello de solicitud servicios multimedia de clave con una Uri (que se extrajo del manifiesto de hello) de la entrega de clave de servicio de entrega y un token (en este tema no trata sobre cómo tooget Simple Web Tokens de un servicio de Token seguro).

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>Protección del contenido con AES-128 mediante .NET

### <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

1. Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 
2. Agregar Hola después elementos demasiado**appSettings** definido en el archivo app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>Ejemplo

Sobrescribir el código de hello en el archivo Program.cs con el código de hello que se muestra en esta sección.
 
>[!NOTE]
>Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .

Seguro tooupdate que las variables sean toopoint toofolders donde se encuentran los archivos de entrada.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file. 
            return originLocator.Path + assetFile.Name;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

