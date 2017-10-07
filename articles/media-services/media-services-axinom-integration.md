---
title: aaaUsing Axinom toodeliver Widevine licencias de servicios de multimedia de tooAzure | Documentos de Microsoft
description: "Este artículo describe cómo puede usar servicios de multimedia de Azure (AMS) toodeliver una secuencia que se cifra dinámicamente por AMS con PlayReady y Widevine DRMs. licencia de PlayReady Hola procede del servidor de licencias de PlayReady de servicios multimedia y licencias de Widevine enviada por el servidor de licencias de Axinom."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="9f6f0-104">Uso de tooAzure de licencias de Widevine Axinom toodeliver servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9f6f0-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f6f0-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="9f6f0-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="9f6f0-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="9f6f0-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9f6f0-107">Información general</span><span class="sxs-lookup"><span data-stu-id="9f6f0-107">Overview</span></span>
<span data-ttu-id="9f6f0-108">Servicios multimedia de Azure (AMS) agrega protección dinámica de Google Widevine (consulte el [blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="9f6f0-109">Además, el Reproductor multimedia de Azure (AMP) también agrega compatibilidad con Widevine (consulte el documento sobre [AMP](http://amp.azure.net/libs/amp/latest/docs/) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="9f6f0-110">Esto es un logro fundamental en el streaming de contenido de DASH protegido por CENC con Multi-native-DRM (PlayReady y Widevine) en los exploradores modernos equipados con MSE y EME.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="9f6f0-111">A partir de Media Services .NET SDK versión 3.5.2 hello, servicios multimedia permite tooconfigure Widevine plantilla de licencia y obtener licencias de Widevine.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="9f6f0-112">También puede usar Hola después AMS socios toohelp entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="9f6f0-113">Este artículo describe cómo toointegrate y prueba Widevine licencia de servidor administrado por Axinom.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="9f6f0-114">En concreto, trata:</span><span class="sxs-lookup"><span data-stu-id="9f6f0-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="9f6f0-115">Configuración de cifrado común dinámico con Multi-DRM (PlayReady y Widevine) con las direcciones URL de adquisición de licencias correspondientes;</span><span class="sxs-lookup"><span data-stu-id="9f6f0-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="9f6f0-116">Generar un token JWT en requisitos del servidor de licencias de orden toomeet Hola;</span><span class="sxs-lookup"><span data-stu-id="9f6f0-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="9f6f0-117">Desarrollo de la aplicación Reproductor multimedia de Azure que controla la adquisición de licencias con la autenticación mediante token JWT;</span><span class="sxs-lookup"><span data-stu-id="9f6f0-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="9f6f0-118">Hola completas del sistema y Hola flujo del contenido de que Hello después diagrama puede describir mejor los Id. de clave, key, de inicialización de clave, el token JTW y sus notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH y CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="9f6f0-120">Protección de contenido</span><span class="sxs-lookup"><span data-stu-id="9f6f0-120">Content Protection</span></span>
<span data-ttu-id="9f6f0-121">Para configurar la protección dinámica y la directiva de entrega de claves, vea el blog de Mingfei: [cómo tooconfigure Widevine empaquetado con servicios multimedia de Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="9f6f0-122">Puede configurar la protección de CENC dinámica con DRM de múltiples para guión de siguiente Hola de transmisión por secuencias:</span><span class="sxs-lookup"><span data-stu-id="9f6f0-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="9f6f0-123">Protección de PlayReady para MS Edge y IE11, que puede tener restricciones de autorización mediante token.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="9f6f0-124">directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS), como Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="9f6f0-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="9f6f0-125">Protección de Widevine para Chrome, que puede requerir autenticación mediante token con el token emitido por otro STS.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="9f6f0-126">Vea la sección [Generación de token JWT](media-services-axinom-integration.md#jwt-token-generation) para saber por qué Azure Active Directory no se puede usar como STS para el servidor de licencias Widevine de Axinom.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="9f6f0-127">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="9f6f0-127">Considerations</span></span>
1. <span data-ttu-id="9f6f0-128">Debe usar hello que axinom especifica la inicialización de clave (8888000000000000000000000000000000000000) y su generado seleccionado clave ID toogenerate Hola contenido o la clave para configurar el servicio de entrega de claves.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="9f6f0-129">Servidor de licencias de Axinom emitirá todas las licencias que contiene claves de contenido basadas en hello misma clave seed, que es válida para pruebas y producción.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="9f6f0-130">URL de adquisición de licencias de Widevine de Hola para las pruebas: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="9f6f0-131">Se permiten tanto HTTP como HTTS.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="9f6f0-132">Preparación del Reproductor multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="9f6f0-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="9f6f0-133">AMP v1.4.0 es compatible con la reproducción del contenido de AMS que está empaquetado dinámicamente con PlayReady y DRM de Widevine.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="9f6f0-134">Si el servidor de licencias de Widevine no requiere autenticación de token, no hay ninguna acción adicional que necesario toodo tootest un guión contenido protegido por Widevine.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="9f6f0-135">Para obtener un ejemplo, equipo de hello AMP proporciona una sencilla [ejemplo](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), donde puede ver que funcione en el borde y IE11 con PlayReady y Chrome con Widevine.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="9f6f0-136">servidor de licencias de Widevine Hola proporcionada por Axinom requiere autenticación de token de JWT.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="9f6f0-137">token de JWT de Hello debe toobe enviada con la solicitud de licencia a través de un encabezado HTTP "X-AxDRM-mensaje".</span><span class="sxs-lookup"><span data-stu-id="9f6f0-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="9f6f0-138">Para ello, necesita hello tooadd después de javascript en la página web de hello hospedaje AMP antes de origen de Hola de configuración:</span><span class="sxs-lookup"><span data-stu-id="9f6f0-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="9f6f0-139">resto de Hola de código de AMP es una API estándar de AMP como en un documento AMP [aquí](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="9f6f0-140">Tenga en cuenta que Hola por encima de javascript para el encabezado de autorización personalizada todavía es un enfoque a corto plazo antes oficial de Hola se libera el enfoque a largo plazo en panel de administración de configuración.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="9f6f0-141">Generación de token JWT</span><span class="sxs-lookup"><span data-stu-id="9f6f0-141">JWT Token Generation</span></span>
<span data-ttu-id="9f6f0-142">El servidor de licencias de Widevine de Axinom para pruebas requiere autenticación mediante token JWT.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="9f6f0-143">Además, una de las notificaciones de hello en el token de JWT de hello es de un tipo de objeto complejo en lugar del tipo de datos primitivo.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="9f6f0-144">Lamentablemente, Azure AD solo puede emitir tokens JWT con tipos primitivos.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="9f6f0-145">De forma similar, API de .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler y JwtPayload) sólo permite tooinput tipo de objeto complejo como notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="9f6f0-146">Sin embargo, las demandas de hello todavía se serializan como cadena.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="9f6f0-147">Por lo tanto, no podemos usar cualquiera de hello dos para generar token JWT de Hola para solicitud de licencias de Widevine.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="9f6f0-148">De John Sheehan [paquete Nuget de JWT](https://www.nuget.org/packages/JWT) cumple Hola necesidades, por lo que haremos será toouse este paquete de Nuget.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="9f6f0-149">A continuación se muestra código de hello para generar el token de JWT con hello necesita notificaciones tal y como requiere el servidor de licencias de Axinom Widevine para las pruebas:</span><span class="sxs-lookup"><span data-stu-id="9f6f0-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="9f6f0-150">Servidor de licencias de Widevine de Axinom</span><span class="sxs-lookup"><span data-stu-id="9f6f0-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="9f6f0-151">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="9f6f0-151">Considerations</span></span>
1. <span data-ttu-id="9f6f0-152">Aunque el servicio de entrega de licencias de AMS PlayReady requiere un “Bearer=” que preceda a un token de autenticación, el servidor de licencias de Widevine de Axinom no lo usa.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="9f6f0-153">Hola Axinom comunicación se utiliza como clave de firma.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="9f6f0-154">Tenga en cuenta que esa clave hello es una cadena hexadecimal, sin embargo, deben tratarse como una serie de bytes no es una cadena al codificar.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="9f6f0-155">Esto se logra al método hello ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="9f6f0-156">Recuperación del identificador de clave</span><span class="sxs-lookup"><span data-stu-id="9f6f0-156">Retrieving Key ID</span></span>
<span data-ttu-id="9f6f0-157">Quizás haya observado que en el código de hello para generar un JWT ID de símbolo (token), key se requiere.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="9f6f0-158">Puesto que los token de JWT de hello necesita toobe listo antes de cargar el Reproductor de AMP, necesidades de identificador claves toobe recuperado en orden de token de JWT de toogenerate.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="9f6f0-159">Por supuesto que hay varias maneras de clave tooget mantenga identificador.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="9f6f0-160">Por ejemplo, se puede almacenar el identificador de clave junto con los metadatos de contenido en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="9f6f0-161">O bien recuperar el identificador de clave del archivo DASH MPD (Descripción de presentación de medios).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="9f6f0-162">código de Hello siguiente es para hello este último.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-162">hello code below is for hello latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="9f6f0-163">Resumen</span><span class="sxs-lookup"><span data-stu-id="9f6f0-163">Summary</span></span>
<span data-ttu-id="9f6f0-164">Con la incorporación más reciente de soporte de Widevine en la protección de contenido de servicios de multimedia de Azure y Azure Media Player, es posible tooimplement transmisión por secuencias de guión + varios native DRM (PlayReady + Widevine) con ambos servicio de licencias de PlayReady en licencia AMS y Widevine servidor de Axinom para hello siguiendo los exploradores modernos:</span><span class="sxs-lookup"><span data-stu-id="9f6f0-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="9f6f0-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="9f6f0-165">Chrome</span></span>
* <span data-ttu-id="9f6f0-166">Microsoft Edge en Windows 10</span><span class="sxs-lookup"><span data-stu-id="9f6f0-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="9f6f0-167">IE 11 en Windows 8.1 y Windows 10</span><span class="sxs-lookup"><span data-stu-id="9f6f0-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="9f6f0-168">(Escritorio) Firefox y Safari en Mac (no iOS) también se admiten a través de Silverlight y Hola la misma dirección URL con el Reproductor de Media de Azure</span><span class="sxs-lookup"><span data-stu-id="9f6f0-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="9f6f0-169">Hello se requieren los parámetros siguientes en el servidor de licencias de Axinom Widevine sacar provecho de hello solución mínima.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="9f6f0-170">Excepto para la clave de Id., rest Hola de parámetros se proporcionan con Axinom según su configuración de servidor Widevine.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="9f6f0-171">Parámetro</span><span class="sxs-lookup"><span data-stu-id="9f6f0-171">Parameter</span></span> | <span data-ttu-id="9f6f0-172">Cómo se utiliza</span><span class="sxs-lookup"><span data-stu-id="9f6f0-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="9f6f0-173">Id. de clave de comunicación</span><span class="sxs-lookup"><span data-stu-id="9f6f0-173">Communication key ID</span></span> |<span data-ttu-id="9f6f0-174">Se deben incluir como valor de notificación de Hola "com_key_id" en el token de JWT (vea [esto](media-services-axinom-integration.md#jwt-token-generation) sección).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="9f6f0-175">Clave de comunicación</span><span class="sxs-lookup"><span data-stu-id="9f6f0-175">Communication key</span></span> |<span data-ttu-id="9f6f0-176">Debe utilizarse como clave de firma de token JWT de Hola (vea [esto](media-services-axinom-integration.md#jwt-token-generation) sección).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="9f6f0-177">Inicialización de clave</span><span class="sxs-lookup"><span data-stu-id="9f6f0-177">Key seed</span></span> |<span data-ttu-id="9f6f0-178">Clave de contenido toogenerate usadas con cualquier figurarán contenido Id. de clave (vea [esto](media-services-axinom-integration.md#content-protection) sección).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="9f6f0-179">Dirección URL de adquisición de licencias de Widevine</span><span class="sxs-lookup"><span data-stu-id="9f6f0-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="9f6f0-180">Se debe usar en la configuración de la directiva de entrega de activos para el streaming de DASH (vea [esta](media-services-axinom-integration.md#content-protection) sección).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="9f6f0-181">Id. de clave de contenido</span><span class="sxs-lookup"><span data-stu-id="9f6f0-181">Content Key ID</span></span> |<span data-ttu-id="9f6f0-182">Se deben incluir como parte del valor de Hola de notificación de mensaje de derechos de token JWT (consulte [esto](media-services-axinom-integration.md#jwt-token-generation) sección).</span><span class="sxs-lookup"><span data-stu-id="9f6f0-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="9f6f0-183">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9f6f0-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9f6f0-184">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9f6f0-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="9f6f0-185">Agradecimientos</span><span class="sxs-lookup"><span data-stu-id="9f6f0-185">Acknowledgments</span></span>
<span data-ttu-id="9f6f0-186">Nos gustaría hello tooacknowledge siguientes personas que han contribuido a la creación de este documento: Kristjan Jõgi de Axinom, Mingfei Yan y Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="9f6f0-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

