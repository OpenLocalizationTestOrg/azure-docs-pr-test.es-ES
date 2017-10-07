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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Uso de tooAzure de licencias de Widevine Axinom toodeliver servicios multimedia
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Información general
Servicios multimedia de Azure (AMS) agrega protección dinámica de Google Widevine (consulte el [blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) para obtener más información). Además, el Reproductor multimedia de Azure (AMP) también agrega compatibilidad con Widevine (consulte el documento sobre [AMP](http://amp.azure.net/libs/amp/latest/docs/) para obtener más información). Esto es un logro fundamental en el streaming de contenido de DASH protegido por CENC con Multi-native-DRM (PlayReady y Widevine) en los exploradores modernos equipados con MSE y EME.

A partir de Media Services .NET SDK versión 3.5.2 hello, servicios multimedia permite tooconfigure Widevine plantilla de licencia y obtener licencias de Widevine. También puede usar Hola después AMS socios toohelp entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Este artículo describe cómo toointegrate y prueba Widevine licencia de servidor administrado por Axinom. En concreto, trata:  

* Configuración de cifrado común dinámico con Multi-DRM (PlayReady y Widevine) con las direcciones URL de adquisición de licencias correspondientes;
* Generar un token JWT en requisitos del servidor de licencias de orden toomeet Hola;
* Desarrollo de la aplicación Reproductor multimedia de Azure que controla la adquisición de licencias con la autenticación mediante token JWT;

Hola completas del sistema y Hola flujo del contenido de que Hello después diagrama puede describir mejor los Id. de clave, key, de inicialización de clave, el token JTW y sus notificaciones.

![DASH y CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Protección de contenido
Para configurar la protección dinámica y la directiva de entrega de claves, vea el blog de Mingfei: [cómo tooconfigure Widevine empaquetado con servicios multimedia de Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

Puede configurar la protección de CENC dinámica con DRM de múltiples para guión de siguiente Hola de transmisión por secuencias:

1. Protección de PlayReady para MS Edge y IE11, que puede tener restricciones de autorización mediante token. directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS), como Azure Active Directory;
2. Protección de Widevine para Chrome, que puede requerir autenticación mediante token con el token emitido por otro STS. 

Vea la sección [Generación de token JWT](media-services-axinom-integration.md#jwt-token-generation) para saber por qué Azure Active Directory no se puede usar como STS para el servidor de licencias Widevine de Axinom.

### <a name="considerations"></a>Consideraciones
1. Debe usar hello que axinom especifica la inicialización de clave (8888000000000000000000000000000000000000) y su generado seleccionado clave ID toogenerate Hola contenido o la clave para configurar el servicio de entrega de claves. Servidor de licencias de Axinom emitirá todas las licencias que contiene claves de contenido basadas en hello misma clave seed, que es válida para pruebas y producción.
2. URL de adquisición de licencias de Widevine de Hola para las pruebas: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). Se permiten tanto HTTP como HTTS.

## <a name="azure-media-player-preparation"></a>Preparación del Reproductor multimedia de Azure
AMP v1.4.0 es compatible con la reproducción del contenido de AMS que está empaquetado dinámicamente con PlayReady y DRM de Widevine.
Si el servidor de licencias de Widevine no requiere autenticación de token, no hay ninguna acción adicional que necesario toodo tootest un guión contenido protegido por Widevine. Para obtener un ejemplo, equipo de hello AMP proporciona una sencilla [ejemplo](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), donde puede ver que funcione en el borde y IE11 con PlayReady y Chrome con Widevine.
servidor de licencias de Widevine Hola proporcionada por Axinom requiere autenticación de token de JWT. token de JWT de Hello debe toobe enviada con la solicitud de licencia a través de un encabezado HTTP "X-AxDRM-mensaje". Para ello, necesita hello tooadd después de javascript en la página web de hello hospedaje AMP antes de origen de Hola de configuración:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

resto de Hola de código de AMP es una API estándar de AMP como en un documento AMP [aquí](http://amp.azure.net/libs/amp/latest/docs/).

Tenga en cuenta que Hola por encima de javascript para el encabezado de autorización personalizada todavía es un enfoque a corto plazo antes oficial de Hola se libera el enfoque a largo plazo en panel de administración de configuración.

## <a name="jwt-token-generation"></a>Generación de token JWT
El servidor de licencias de Widevine de Axinom para pruebas requiere autenticación mediante token JWT. Además, una de las notificaciones de hello en el token de JWT de hello es de un tipo de objeto complejo en lugar del tipo de datos primitivo.

Lamentablemente, Azure AD solo puede emitir tokens JWT con tipos primitivos. De forma similar, API de .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler y JwtPayload) sólo permite tooinput tipo de objeto complejo como notificaciones. Sin embargo, las demandas de hello todavía se serializan como cadena. Por lo tanto, no podemos usar cualquiera de hello dos para generar token JWT de Hola para solicitud de licencias de Widevine.

De John Sheehan [paquete Nuget de JWT](https://www.nuget.org/packages/JWT) cumple Hola necesidades, por lo que haremos será toouse este paquete de Nuget.

A continuación se muestra código de hello para generar el token de JWT con hello necesita notificaciones tal y como requiere el servidor de licencias de Axinom Widevine para las pruebas:

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

Servidor de licencias de Widevine de Axinom

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Consideraciones
1. Aunque el servicio de entrega de licencias de AMS PlayReady requiere un “Bearer=” que preceda a un token de autenticación, el servidor de licencias de Widevine de Axinom no lo usa.
2. Hola Axinom comunicación se utiliza como clave de firma. Tenga en cuenta que esa clave hello es una cadena hexadecimal, sin embargo, deben tratarse como una serie de bytes no es una cadena al codificar. Esto se logra al método hello ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Recuperación del identificador de clave
Quizás haya observado que en el código de hello para generar un JWT ID de símbolo (token), key se requiere. Puesto que los token de JWT de hello necesita toobe listo antes de cargar el Reproductor de AMP, necesidades de identificador claves toobe recuperado en orden de token de JWT de toogenerate.

Por supuesto que hay varias maneras de clave tooget mantenga identificador. Por ejemplo, se puede almacenar el identificador de clave junto con los metadatos de contenido en una base de datos. O bien recuperar el identificador de clave del archivo DASH MPD (Descripción de presentación de medios). código de Hello siguiente es para hello este último.

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

## <a name="summary"></a>Resumen
Con la incorporación más reciente de soporte de Widevine en la protección de contenido de servicios de multimedia de Azure y Azure Media Player, es posible tooimplement transmisión por secuencias de guión + varios native DRM (PlayReady + Widevine) con ambos servicio de licencias de PlayReady en licencia AMS y Widevine servidor de Axinom para hello siguiendo los exploradores modernos:

* Chrome
* Microsoft Edge en Windows 10
* IE 11 en Windows 8.1 y Windows 10
* (Escritorio) Firefox y Safari en Mac (no iOS) también se admiten a través de Silverlight y Hola la misma dirección URL con el Reproductor de Media de Azure

Hello se requieren los parámetros siguientes en el servidor de licencias de Axinom Widevine sacar provecho de hello solución mínima. Excepto para la clave de Id., rest Hola de parámetros se proporcionan con Axinom según su configuración de servidor Widevine.

| Parámetro | Cómo se utiliza |
| --- | --- |
| Id. de clave de comunicación |Se deben incluir como valor de notificación de Hola "com_key_id" en el token de JWT (vea [esto](media-services-axinom-integration.md#jwt-token-generation) sección). |
| Clave de comunicación |Debe utilizarse como clave de firma de token JWT de Hola (vea [esto](media-services-axinom-integration.md#jwt-token-generation) sección). |
| Inicialización de clave |Clave de contenido toogenerate usadas con cualquier figurarán contenido Id. de clave (vea [esto](media-services-axinom-integration.md#content-protection) sección). |
| Dirección URL de adquisición de licencias de Widevine |Se debe usar en la configuración de la directiva de entrega de activos para el streaming de DASH (vea [esta](media-services-axinom-integration.md#content-protection) sección). |
| Id. de clave de contenido |Se deben incluir como parte del valor de Hola de notificación de mensaje de derechos de token JWT (consulte [esto](media-services-axinom-integration.md#jwt-token-generation) sección). |

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Agradecimientos
Nos gustaría hello tooacknowledge siguientes personas que han contribuido a la creación de este documento: Kristjan Jõgi de Axinom, Mingfei Yan y Amit Rajput.

