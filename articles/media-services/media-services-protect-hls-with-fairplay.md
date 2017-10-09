---
title: aaaProtect de contenido HLS con Microsoft PlayReady o Apple FairPlay - Azure | Documentos de Microsoft
description: "Este tema proporciona información general y muestra cómo toouse servicios multimedia de Azure toodynamically cifrar el contenido HTTP Live Streaming (HLS) con FairPlay de Apple. También muestra cómo toouse Hola servicios multimedia de licencia toodeliver de servicio de entrega tooclients de licencias FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Protección del contenido HLS con Apple FairPlay o Microsoft PlayReady
Azure Media Services permite toodynamically cifrar el contenido de HTTP Live Streaming (HLS) mediante el uso de hello siguientes formatos:  

* **Clave sin cifrado de sobre AES-128**

    Hello fragmento completo se cifra con hello **AES-128 CBC** modo. descifrado de Hola de secuencia de hello es compatible con iOS y el Reproductor de OS X de la forma nativa. Para más información, consulte [Uso del cifrado dinámico AES-128 y del servicio de entrega de claves](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    Hola individual vídeo y muestras de audio se cifran mediante el uso de hello **AES-128 CBC** modo. **Transmisión por secuencias de FairPlay** (FPS) se integra en hello sistemas operativos de dispositivos, con compatibilidad nativa en iOS y Apple TV. Safari en OS X permite FPS utilizando el soporte de interfaz de hello las extensiones de medios de cifrado (EME).
* **Microsoft PlayReady**

Hello siguiente imagen muestra hello **HLS + FairPlay o PlayReady cifrado dinámico** flujo de trabajo.

![Diagrama de flujo de trabajo de cifrado dinámico](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

Este tema muestra cómo toouse servicios multimedia toodynamically cifrar el contenido HLS con FairPlay de Apple. También muestra cómo toouse Hola servicios multimedia de licencia toodeliver de servicio de entrega tooclients de licencias FairPlay.

> [!NOTE]
> Si también desea tooencrypt su HLS contenido con PlayReady, es necesario toocreate una clave de contenido común y asociarlo con el recurso. También deberá directiva de autorización de tooconfigure Hola la clave de contenido, tal y como se describe en [cifrado dinámico comunes de usar PlayReady](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Requisitos y consideraciones

Hola se necesita siguiente al usar toodeliver de servicios multimedia que HLS cifrado con FairPlay y toodeliver FairPlay licencias:

  * Una cuenta de Azure. Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Una cuenta de Media Services. toocreate uno, vea [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de hello](media-services-portal-create-account.md).
  * Suscríbase al [programa de desarrollo de Apple](https://developer.apple.com/).
  * Apple requiere Hola de hello propietario del contenido tooobtain [paquete de implementación](https://developer.apple.com/contact/fps/). Estado que ya se ha implementado módulo de seguridad de clave (KSM) con servicios multimedia, por lo que está solicitando paquete FPS final de Hola. Hay instrucciones de hello FPS final toogenerate certificación del paquete y obtener Hola clave de secreto de aplicación (consulte). Utilice ASK tooconfigure FairPlay.
  * Versión **3.6.0** del SDK .NET de Servicios multimedia de Azure.

Hola después cosas debe establecerse en el lado de la entrega de claves de servicios multimedia:

  * **Aplicación de certificados (CA)**: se trata de un archivo .pfx que contiene la clave privada de Hola. Puede crear este archivo y cifrarlo con una contraseña.

       Cuando se configura una directiva de entrega de claves, debe proporcionar ese archivo .pfx hello y la contraseña en formato Base64.

      Hola pasos describe cómo archivo toogenerate un certificado .pfx para FairPlay:

    1. Instalación de OpenSSL desde https://slproweb.com/products/Win32OpenSSL.html.

        Vaya a carpeta de toohello donde se certificado FairPlay de Hola y otros archivos entregados por Apple.
    2. Ejecute hello siguiente comando desde la línea de comandos de Hola. Esto convierte el archivo PEM tooa de hello .cer archivo.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Ejecute hello siguiente comando desde la línea de comandos de Hola. Esto convierte el archivo .pfx tooa de hello PEM archivo con clave privada de Hola. contraseña de Hola para archivo hello, a continuación, se pide al OpenSSL.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **Contraseña del certificado de la aplicación**: contraseña de Hola para crear el archivo .pfx de Hola.
  * **Id. de la contraseña de certificado de la aplicación**: debe cargar contraseña hello, toohow similar cargan otras claves de servicios multimedia. Hola de uso **ContentKeyType.FairPlayPfxPassword** Hola de tooget valor enum identificador de Media Services. Esto es lo necesitan toouse dentro de la opción de directiva de entrega de claves de Hola.
  * **iv**: se trata de un valor aleatorio de 16 bytes. Debe coincidir con Hola iv en directiva de entrega de hello activo. Generar Hola iv y colóquelo en ambos lugares: directiva de entrega del activo de Hola y la opción de directiva de entrega de claves de Hola.
  * **PIDA**: esta clave se recibe cuando genere certificación hello mediante portal para desarrolladores de Apple Hola. Cada equipo de desarrollo recibirá una única ASK. Guardar una copia del programa Hola a FORMULAR y almacenarlo en un lugar seguro. Más adelante necesitará tooconfigure ASK como FairPlayAsk tooMedia servicios.
  * **Identificador de ASK**: este identificador se obtiene cuando se carga la ASK en Media Services. Debe cargar ASK mediante hello **ContentKeyType.FairPlayAsk** valor enum. Como resultado de hello, se devuelve el Id. de servicios multimedia de Hola y esto es lo que se debe usar al establecer la opción de directiva de entrega de claves de Hola.

Hello lo siguiente debe establecerse por hello cliente FPS:

  * **Aplicación de certificados (CA)**: se trata de un archivo.cer/.der que contiene la clave pública de hello, sistema operativo hello usa tooencrypt algunos carga. Servicios multimedia debe tooknow sobre él porque es necesaria para el Reproductor de Hola. servicio de entrega de claves de Hello descifra mediante la clave privada correspondiente de Hola.

tooplay hacer copia de una secuencia cifrada FairPlay, obtener primero un ASK real y, a continuación, generar un certificado real. Este proceso crea todas las tres partes:

  * archivo .der
  * archivo .pfx
  * contraseña de hello .pfx

Hello siguientes clientes admiten HLS con **AES-128 CBC** cifrado: Safari en OS X, Apple TV, iOS.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Configuración del cifrado dinámico y los servicios de entrega de licencias de FairPlay
Hola siguientes pasos son generales para proteger sus activos con FairPlay mediante servicio de entrega de licencias de servicios multimedia de hello y también mediante el uso de cifrado dinámico.

1. Crear un activo y cargar archivos en el recurso de Hola.
2. Codificar el activo de Hola que contenga Hola archivo toohello velocidad de bits adaptativa que MP4 establecido.
3. Crear una clave de contenido y asociarla a activos de hello codificado.  
4. Configurar la directiva de autorización de la clave de hello contenido. Especifique Hola siguientes:

   * método de entrega de Hello (en este caso, FairPlay).
   * Configuración de opciones de directiva de FairPlay. Para obtener más información acerca de cómo tooconfigure FairPlay, vea hello **ConfigureFairPlayPolicyOptions()** método en el siguiente ejemplo de Hola.

     > [!NOTE]
     > Por lo general, sería aconsejable tooconfigure FairPlay directiva opciones sólo una vez, ya que sólo tendrá un conjunto de una entidad y un ASK.
     >
     >
   * Restricciones (abiertas o token).
   * Tipo de la entrega de claves de toohello específico información que define cómo clave Hola se entrega a toohello cliente.
5. Configurar directiva de entrega de hello activo. configuración de directiva de entrega de Hello incluye:

   * Protocolo de entrega de Hello (HLS).
   * tipo de Hola de cifrado dinámico (cifrado CBC común).
   * dirección URL de adquisición de licencias de Hola.

     > [!NOTE]
     > Si desea toodeliver una secuencia que se cifra con FairPlay y otro sistema de administración de derechos digitales (DRM), tienen directivas de entrega diferente de tooconfigure:
     >
     > * Una tooconfigure IAssetDeliveryPolicy dinámica transmisión por secuencias adaptativa sobre HTTP (guión) con CENC (Common Encryption) (PlayReady + Widevine) y suave con PlayReady
     > * Otro IAssetDeliveryPolicy tooconfigure FairPlay para HLS
     >
     >
6. Crear un tooget de localizador OnDemand una URL de streaming.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Uso de la entrega de la clave FairPlay por aplicaciones reproductor
Puede desarrollar aplicaciones de Reproductor mediante el uso de SDK de iOS de Hola. tooplay toobe capaz de FairPlay contenido, tendrá protocolo de intercambio de licencias de tooimplement Hola. Apple no especifica este protocolo. Es la aplicación de tooeach cómo solicita toosend entrega de claves. Hola servicio de entrega de clave de Media Services FairPlay espera Hola SPC toocome como un mensaje de post codificados www-form-url, Hola siguiente forma:

    spc=<Base64 encoded SPC>

> [!NOTE]
> El Reproductor multimedia de Azure no admita la reproducción de FairPlay fuera del cuadro de Hola. reproducción de FairPlay tooget en MAC OS X para obtenerlo Reproductor de ejemplo de Hola Hola cuenta de desarrollador de Apple.
>
>

## <a name="streaming-urls"></a>Direcciones URL de streaming
Si el recurso se cifró con DRM de más de una, debe usar una etiqueta de cifrado en hello transmisión por secuencias de dirección URL: (formato = 'm3u8-aapl' cifrado = 'xxx').

Hola siguientes consideraciones se aplica:

* Se puede especificar solo un tipo de cifrado o ninguno.
* tipo de cifrado de Hello no tiene toobe especificado en dirección URL de hello si solo un cifrado estaba activo toohello aplicada.
* tipo de cifrado de Hello distingue mayúsculas de minúsculas.
* Hola siguientes tipos de cifrado se puede especificar:  
  * **cenc**: cifrado común (PlayReady o Widevine)
  * **cbcs-aapl**: FairPlay
  * **cbc**: cifrado de sobre AES

## <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

1. Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 
2. Agregar Hola después elementos demasiado**appSettings** definido en el archivo app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Ejemplo

Hola siguiente ejemplo muestra hello capacidad toouse toodeliver de servicios multimedia el contenido cifrado con FairPlay. Esta funcionalidad se introdujo en hello SDK de servicios multimedia de Azure para .NET versión 3.6.0. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>Siguientes pasos: Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
