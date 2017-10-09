---
title: "aaaUsing PlayReady o Widevine comunes cifrado dinámico | Documentos de Microsoft"
description: "Servicios de multimedia de Microsoft Azure permite toodeliver MPEG-DASH, Smooth Streaming y Http-Live-Streaming (HLS) secuencias protegidos con DRM de PlayReady de Microsoft. También permite toodelivery DASH cifrado con Widevine DRM. Este tema muestra cómo cifrar toodynamically con PlayReady y Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>Uso de cifrado dinámico común de PlayReady o Widevine

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Servicios de multimedia de Microsoft Azure le permite toodeliver MPEG-DASH, Smooth Streaming y secuencias de HTTP-Live-Streaming (HLS) protegidas con [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). También permite secuencias de guión toodeliver cifrado con licencias de Widevine DRM. PlayReady y Widevine se cifran por hello especificación de cifrado común (ISO/IEC 23001-7 CENC). Puede usar [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (a partir de la versión de Hola 3.5.1) o REST API tooconfigure su toouse AssetDeliveryConfiguration Widevine.

Servicios multimedia proporciona un servicio para entregar licencias DRM de PlayReady y Widevine. Servicios multimedia también proporcionan API que permiten configurar los derechos de Hola y las restricciones que desea para hello el tooenforce de tiempo de ejecución PlayReady o Widevine DRM cuando un usuario se reproduce contenido protegido. Cuando un usuario solicita un contenido protegido con DRM, aplicación de Reproductor de hello solicitará una licencia de servicio de licencias de hello AMS. servicio de licencias de Hello AMS emitirá un Reproductor de toohello de licencia si está autorizado. Una licencia de PlayReady o Widevine contiene la clave de descifrado de Hola que puede usarse en hello Reproductor toodecrypt y secuencia Hola contenido de cliente.

También puede usar Hola después AMS socios toohelp entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Para obtener más información, consulte: integración con [Axinom](media-services-axinom-integration.md) y [castLabs](media-services-castlabs-integration.md).

Servicios multimedia admite varias formas de autorizar a los usuarios que realizan solicitudes de clave. Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: abrir o símbolo (token) de restricción. directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS). Servicios multimedia admite tokens en hello [Tokens Web simples](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) y [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT). Para obtener más información, vea Directiva de autorización de configurar Hola la clave de contenido.

tootake ventaja del cifrado dinámico, debe toohave un activo que contiene un conjunto de archivos MP4 de velocidad de multibits o archivos de origen Smooth Streaming de velocidades de bits. También necesita las directivas de entrega de hello tooconfigure para activos de hello (descrita más adelante en este tema). A continuación, en función de formato de hello especificado en hello transmisión por secuencias de dirección URL, servidor de Streaming a petición de hello garantizará que esa secuencia Hola se entrega en el protocolo de hello que ha elegido. Como resultado, solo tendrá toostore y pago para los archivos de hello en un formato de almacenamiento único y servicios multimedia creará y proporcionará la respuesta HTTP adecuada hello en función de cada solicitud de un cliente.

En este tema sería útil toodevelopers que funcionan en aplicaciones que ofrecen los medios protegidos con varios DRMs, por ejemplo, PlayReady y Widevine. Hola tema muestra cómo tooconfigure Hola servicio de entrega de licencias de PlayReady con directivas de autorización para que sólo los clientes autorizados puedan recibir licencias de PlayReady o Widevine. También se muestra cómo toouse cifrado dinámico cifrado con PlayReady o Widevine DRM a través de guión.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

## <a name="download-sample"></a>Descarga de un ejemplo
Puede descargar ejemplo Hola se describe en este artículo de [aquí](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Configuración del cifrado dinámico común y el servicio de entrega de licencias DRM

Hola siguientes pasos son generales que tendría tooperform al proteger sus activos con PlayReady, usando el servicio de entrega de licencias de servicios multimedia de Hola y también mediante el cifrado dinámico.

1. Crear un activo y cargar archivos en el recurso de Hola.
2. Codificar Hola asset contenedor Hola archivo toohello velocidad de bits adaptativa que MP4 establecido.
3. Crear una clave de contenido y asociarla a activos de hello codificado. En servicios multimedia, clave de contenido de hello contiene la clave de cifrado del activo de Hola.
4. Configurar la directiva de autorización de la clave de hello contenido. Directiva de autorización de clave de contenido de Hello debe configurarse por parte del usuario y se cumple mediante el cliente de Hola para hello toobe clave contenido entregado toohello cliente.

    Al crear directivas de autorización de clave de contenido de hello, necesita toospecify Hola siguiente: método (PlayReady o Widevine), las restricciones de entrega (abiertas o token) y el tipo de entrega de claves de toohello específico de información que define cómo se entrega clave Hola cliente toohello ([PlayReady](media-services-playready-license-template-overview.md) o [Widevine](media-services-widevine-license-template-overview.md) plantilla de licencia).

5. Configurar directiva de entrega de Hola para un activo. configuración de directiva de entrega de Hello incluye: Hola de protocolo de entrega (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), tipo de cifrado dinámico (por ejemplo, cifrado común), PlayReady o dirección URL de adquisición de licencias de Widevine.

    Podría aplicar protocolo tooeach de directivas diferentes en hello mismo activo. Por ejemplo, podría aplicar PlayReady cifrado tooSmooth/DASH y AES Envelope tooHLS. Todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, se agrega una directiva única que solo especifica HLS como protocolo de Hola) se bloqueará de transmisión por secuencias. Hola toothis de excepción es si no tiene definida en absoluto ninguna directiva de entrega de activos. A continuación, todos los protocolos se permitirá en hello clara.

6. Crear un localizador OnDemand en orden tooget una URL de streaming.

Encontrará un ejemplo completo de .NET final Hola de tema de Hola.

Hola después de la imagen muestra el flujo de trabajo de Hola que se ha descrito anteriormente. Aquí se utiliza el token de hello para la autenticación.

![Protección con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

resto Hola de este tema ofrece explicaciones detalladas, ejemplos de código y tootopics de vínculos que le muestran cómo tooachieve Hola tareas descritas anteriormente.

## <a name="current-limitations"></a>Limitaciones actuales
Si agrega o actualiza una directiva de entrega de activos, debe eliminar el localizador de hello asociado (si existe) y crear un localizador nuevo.

Limitación cuando se cifra con Widevine con Servicios multimedia de Azure: actualmente, no se admiten varias claves de contenido.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Crear un activo y cargar archivos en el recurso de Hola
En orden toomanage, codificar y transmitir sus vídeos, debe cargar primero su contenido en los servicios de multimedia de Microsoft Azure. Una vez cargado, el contenido se almacena de forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.

Para obtener información detallada, consulte [Carga de archivos en una cuenta de Servicios multimedia](media-services-dotnet-upload-files.md).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Codificar Hola asset contenedor Hola archivo toohello velocidad de bits adaptativa que MP4 establecer
Con cifrado dinámico todo lo que necesita es toocreate un activo que contiene un conjunto de archivos MP4 de velocidad de multibits o archivos de origen Smooth Streaming de velocidades de bits. A continuación, según Hola formato especificado en el manifiesto de Hola y fragmentar la solicitud, Hola servidor se asegurará de que recibe Hola transmisión por secuencias de protocolo de Hola que ha elegido el Streaming a petición. Como resultado, solo tendrá toostore y pago para los archivos de hello en formato de almacenamiento único y el servicio de servicios multimedia creará y proporcionará la respuesta adecuada Hola según las solicitudes de un cliente. Para obtener más información, vea hello [Introducción al empaquetado dinámico](media-services-dynamic-packaging-overview.md) tema.

Para obtener instrucciones sobre cómo tooencode, consulte [cómo tooencode un activo con Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Crear una clave de contenido y asociarla a activos de hello codificado
En los servicios multimedia, clave de contenido de hello contiene clave de Hola que desea tooencrypt un activo con.

Para obtener más información, consulte [Creación de la clave de contenido](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurar directiva de autorización de la clave de hello contenido
Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave. Directiva de autorización de clave de contenido de Hello debe configurarse por parte del usuario y cumplir Hola cliente (Reproductor) en orden para hello toobe clave entregado a toohello cliente. Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: abrir o símbolo (token) de restricción.

Para obtener información detallada, consulte [Configuración de la directiva de autorización de claves de contenido](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).

## <a id="configure_asset_delivery_policy"></a>Configuración de directivas de entrega de recursos
Configurar directiva de entrega de hello para el activo. Algunas cosas que Hola configuración de directiva de entrega de activos incluye:

* dirección URL de adquisición de licencias de Hello DRM.
* Hola asset protocolo de entrega (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos).
* tipo de Hola de cifrado dinámico (en este caso, cifrado común).

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

## <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

1. Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 
2. Agregar Hola después elementos demasiado**appSettings** definido en el archivo app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente muestra la funcionalidad que se introdujo en el SDK de servicios multimedia de Azure para .net-versión 3.5.2 (específicamente, Hola capacidad toodefine un Widevine plantilla de licencia y solicitan una licencia de Widevine de servicios multimedia de Azure).

Sobrescribir el código de hello en el archivo Program.cs con el código de hello que se muestra en esta sección.

>[!NOTE]
>Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .

Seguro tooupdate que las variables sean toopoint toofolders donde se encuentran los archivos de entrada.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
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

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
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

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[CENC with Multi-DRM and Access Control (CENC con DRM múltiple y Control de acceso)](media-services-cenc-with-multidrm-access-control.md)

[Configuración del empaquetado Widevine con AMS](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Anuncio de los servicios de entrega de licencias de Google Widevine en Servicios multimedia de Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
