---
title: Uso de Servicios multimedia de Azure para entregar licencias de DRM a claves de AES
description: "Este artículo describe cómo puede utilizar Servicios de multimedia de Azure (AMS) para proporcionar licencias de PlayReady y Widevine y claves de AES, pero realizar el resto (codificación, cifrado y streaming) con los servidores locales."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 263a381dc72105eea60ad9b39434599ff04a4531
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-services-to-deliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="501d1-103">Uso de Servicios multimedia de Azure para entregar licencias de DRM a claves de AES</span><span class="sxs-lookup"><span data-stu-id="501d1-103">Use Azure Media Services to deliver DRM licenses or AES keys</span></span>
<span data-ttu-id="501d1-104">Servicios de multimedia de Azure (AMS) le permite introducir, codificar, agregar protección de contenido y transmitir el contenido (consulte [este](media-services-protect-with-drm.md) artículo para ver los detalles).</span><span class="sxs-lookup"><span data-stu-id="501d1-104">Azure Media Services (AMS) enables you to ingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="501d1-105">Sin embargo, hay clientes que solo desean usar AMS para entregar licencias y claves, y realizar la codificación, el cifrado y el streaming mediante sus servidores locales.</span><span class="sxs-lookup"><span data-stu-id="501d1-105">However, there are customers who only want to use AMS to deliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="501d1-106">Este artículo describe cómo puede usar AMS para entregar licencias de PlayReady y Widevine, pero realizar el resto con los servidores locales.</span><span class="sxs-lookup"><span data-stu-id="501d1-106">This article describes how you can use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="501d1-107">Información general</span><span class="sxs-lookup"><span data-stu-id="501d1-107">Overview</span></span>
<span data-ttu-id="501d1-108">Media Services proporciona un servicio para entregar licencias DRM de PlayReady y Widevine y claves de AES-128.</span><span class="sxs-lookup"><span data-stu-id="501d1-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="501d1-109">Servicios multimedia también proporciona API que permiten configurar los derechos y las restricciones que desee aplicar en tiempo de ejecución de DRM cuando un usuario reproduzca contenido protegido de DRM.</span><span class="sxs-lookup"><span data-stu-id="501d1-109">Media Services also provides APIs that let you configure the rights and restrictions that you want for the DRM runtime to enforce when a user plays back the DRM protected content.</span></span> <span data-ttu-id="501d1-110">Cuando un usuario solicita contenido protegido, la aplicación del reproductor solicitará una licencia del servicio de licencias de AMS.</span><span class="sxs-lookup"><span data-stu-id="501d1-110">When a user requests the protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="501d1-111">El servicio de licencias de AMS emitirá la licencia al reproductor, si está autorizado.</span><span class="sxs-lookup"><span data-stu-id="501d1-111">The AMS license service will issue the license to the player (if it is authorized).</span></span> <span data-ttu-id="501d1-112">Las licencias de PlayReady y Widevine contienen la clave de descifrado que puede usar el reproductor cliente para descifrar y transmitir el contenido.</span><span class="sxs-lookup"><span data-stu-id="501d1-112">The PlayReady and Widevine licenses contain the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="501d1-113">Servicios multimedia admite varias formas de autorizar a los usuarios que realizan solicitudes de licencias o claves.</span><span class="sxs-lookup"><span data-stu-id="501d1-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="501d1-114">Puede configurar la directiva de autorización de claves de acceso, que podría tener una o más restricciones: abrir o restricción de token.</span><span class="sxs-lookup"><span data-stu-id="501d1-114">You configure the content key's authorization policy and the policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="501d1-115">La directiva con restricción token debe ir acompañada de un token emitido por un Servicio de tokens seguros (STS).</span><span class="sxs-lookup"><span data-stu-id="501d1-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="501d1-116">Servicios multimedia admite tokens en formato Token de web simple (SWT) y en formato Token de web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="501d1-116">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="501d1-117">El siguiente diagrama muestra los pasos principales que debe llevar a cabo con el fin de usar AMS para entregar licencias de PlayReady y Widevine, pero realizar el resto con los servidores locales.</span><span class="sxs-lookup"><span data-stu-id="501d1-117">The following diagram shows the main steps you need to take to use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span>

![Protección con PlayReady](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="501d1-119">Descarga de un ejemplo</span><span class="sxs-lookup"><span data-stu-id="501d1-119">Download sample</span></span>
<span data-ttu-id="501d1-120">Puede descargar el ejemplo descrito en este artículo [aquí](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span><span class="sxs-lookup"><span data-stu-id="501d1-120">You can download the sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="501d1-121">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="501d1-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="501d1-122">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="501d1-122">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="501d1-123">Agregue los siguientes elementos al elemento **appSettings** definido en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="501d1-123">Add the following elements to **appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="501d1-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="501d1-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="501d1-125">Ejemplo de código .NET</span><span class="sxs-lookup"><span data-stu-id="501d1-125">.NET code example</span></span>

<span data-ttu-id="501d1-126">El ejemplo de código siguiente muestra cómo crear una clave de contenido común y obtener direcciones URL de adquisición de licencias de PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="501d1-126">The following code example shows how to create a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="501d1-127">Necesitará obtener los siguientes fragmentos de información de AMS y configurar el servidor local: **clave de contenido**, **identificador de clave**, **URL de adquisición de licencias**.</span><span class="sxs-lookup"><span data-stu-id="501d1-127">You need to get the following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="501d1-128">Una vez que configure su servidor local, podría transmitir desde su propio servidor de streaming.</span><span class="sxs-lookup"><span data-stu-id="501d1-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="501d1-129">Puesto que la transmisión cifrada apunta al servidor de licencias de AMS, el reproductor solicitará una licencia de AMS.</span><span class="sxs-lookup"><span data-stu-id="501d1-129">Since the encrypted stream points to AMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="501d1-130">Si elige la autenticación de token, el servidor de licencias de AMS validará el token enviado a través de HTTPS y, si es válido, devolverá la licencia a su reproductor.</span><span class="sxs-lookup"><span data-stu-id="501d1-130">If you choose token authentication, the AMS license server will validate the token you sent through HTTPS and (if valid) will deliver the license back to your player.</span></span> <span data-ttu-id="501d1-131">(El ejemplo de código solo muestra cómo crear una clave de contenido común y obtener direcciones URL de adquisición de licencias PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="501d1-131">(The code example only shows how to create a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="501d1-132">Si desea proporcionar las claves de AES-128, debe crear una clave de contenido del sobre y obtener una dirección URL de adquisición de claves; en [este](media-services-protect-with-aes128.md) artículo se muestra cómo hacerlo).</span><span class="sxs-lookup"><span data-stu-id="501d1-132">If you want to delivery AES-128 keys, you need to create an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how to do it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from the App.config file.
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

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out the key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
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
                // Associate the content key authorization policy with the content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
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

                // Associate the content key authorization policy with the content key
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
                // The following code configures PlayReady License Template using .NET classes
                // and returns the XML string.

                //The PlayReadyLicenseResponseTemplate class represents the template 
                //for the response sent back to the end user. 
                //It contains a field for a custom data string between the license server 
                //and the application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // The PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // to be returned to the end users. 
                // It contains the data on the content key in the license 
                // and any rights or restrictions to be 
                // enforced by the PlayReady DRM runtime when using the content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether the license is persistent 
                // (saved in persistent storage on the client) 
                // or non-persistent (only held in memory while the player is using the license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use the license or not.  
                // If true, the MinimumSecurityLevel property of the license
                // is set to 150.  If false (the default), 
                // the MinimumSecurityLevel property of the license is set to 2000.
                licenseTemplate.AllowTestDevices = true;

                // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
                // It grants the user the ability to playback the content subject to the zero or more restrictions 
                // configured in the license and on the PlayRight itself (for playback specific policy). 
                // Much of the policy on the PlayRight has to do with output restrictions 
                // which control the types of outputs that the content can be played over and 
                // any restrictions that must be put in place when using a given output.
                // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
                //then the DRM runtime will only allow the video to be displayed over digital outputs 
                //(analog video outputs won’t be allowed to pass the content).

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect the consumer experience. 
                // If the output protections are configured too restrictive, 
                // the content might be unplayable on some clients. 
                // For more information, see the PlayReady Compliance Rules document.

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
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="501d1-133">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="501d1-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="501d1-134">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="501d1-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="501d1-135">Consulte también</span><span class="sxs-lookup"><span data-stu-id="501d1-135">See also</span></span>
[<span data-ttu-id="501d1-136">Uso de cifrado dinámico común de PlayReady o Widevine</span><span class="sxs-lookup"><span data-stu-id="501d1-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="501d1-137">Uso del cifrado dinámico AES-128 y del servicio de entrega de claves</span><span class="sxs-lookup"><span data-stu-id="501d1-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="501d1-138">Uso de partners para entregar licencias de Widevine a Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="501d1-138">Using partners to deliver Widevine licenses to Azure Media Services</span></span>](media-services-licenses-partner-integration.md)

