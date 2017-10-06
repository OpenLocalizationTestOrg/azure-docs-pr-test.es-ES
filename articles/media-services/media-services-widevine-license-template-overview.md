---
title: "Introducción a la plantilla licencia aaaWidevine | Documentos de Microsoft"
description: "En este tema se ofrece una visión general de una plantilla de licencias de Widevine que utiliza licencias de Widevine tooconfigure."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Información general sobre las plantillas de licencias de Widevine
## <a name="overview"></a>Información general
Servicios multimedia de Azure le permite ahora licencias de Widevine tooconfigure y solicitud. Cuando el Reproductor del usuario final de hello intente tooplay el contenido de Widevine protegido, una solicitud es tooobtain de servicio de entrega de toohello enviado licencia una licencia. Si el servicio de licencias de hello aprueba la solicitud de hello, que emite la licencia de Hola que es enviado toohello cliente y puede ser usado toodecrypt y play Hola contenido especificado.

La solicitud de licencia de Widevine recibe el formato de un mensaje JSON.  

>[!NOTE]
> Puede elegir toocreate un mensaje vacío con ningún valores simplemente "{}" y se creará una plantilla de licencia con todos los valores predeterminados. valor predeterminado de Hello funciona para la mayoría de los casos. Por ejemplo, en el caso de escenarios de entrega de licencia basados en Microsoft, los valores siempre deberían ser los predeterminados. Si necesita tooset Hola "proveedor" y "content_id" valores, un proveedor debe coincidir con las credenciales de Widevine de Google.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>Mensaje JSON
| Nombre | Valor | Description |
| --- | --- | --- |
| payload |cadena codificada en Base64 |solicitud de licencia de Hello enviado por un cliente. |
| content_id |cadena codificada en Base64 |Identificador usa tooderive KeyId(s) y claves de contenido para cada content_key_specs.track_type. |
| provider |cadena |Toolook usa seguridad de claves de contenido y directivas. En el caso de que se use la entrega de claves de Microsoft para la entrega de licencias de Widevine, este parámetro se omite. |
| policy_name |string |Nombre de una directiva previamente registrada. Opcional |
| allowed_track_types |enum |SD_ONLY o SD_HD. Controla qué claves de contenido deben incluirse en una licencia. |
| content_key_specs |matriz de estructuras JSON, vea **Especificaciones de clave de contenido** a continuación |Un control más preciso sobre el contenido de las claves tooreturn. Vea Especificaciones de clave de contenido para obtener más información.  Solo se puede especificar uno de los valores allowed_track_types y content_key_specs. |
| use_policy_overrides_exclusively |valor booleano. true o false |Utilice atributos de directiva especificados por policy_overrides y omita todas las directivas almacenadas previamente. |
| policy_overrides |Estructura JSON, vea **Invalidaciones de directivas** a continuación |Configuración de directiva para esta licencia.  En caso de hello este recurso tiene una directiva definida previamente, se utilizarán estos valores especificados. |
| session_init |Estructura JSON, vea **Inicialización de la sesión** a continuación |Datos opcionales pasan toolicense. |
| parse_only |valor booleano. true o false |se analiza la solicitud de licencia de Hello pero no se emite ninguna licencia. Sin embargo, la solicitud de licencia de Hola de formato de valores se devuelven en respuesta de Hola. |

## <a name="content-key-specs"></a>Especificaciones de clave de contenido
Si existe una directiva existente, no hay ningún toospecify necesidad alguna de hello valores de hello especificación de clave de contenido.  Directiva de Hello preexistente asociado a este contenido será protección de salida de hello toodetermine usado como HDCP y por CGMS.  Si una directiva existente no está registrada con el servidor de licencias de Widevine hello, proveedor de contenido de Hola puede insertar valores de hello en la solicitud de licencia de Hola.   

Cada content_key_specs debe especificarse para todas las pistas, independientemente de hello opción use_policy_overrides_exclusively. 

| Nombre | Valor | Descripción |
| --- | --- | --- |
| content_key_specs. track_type |string |Un nombre de tipo de pista. Si se especifica content_key_specs en la solicitud de licencia de hello, asegúrese de toospecify seguro que realizar un seguimiento de todos los tipos explícitamente. Error toodo por lo que dará como resultado Error tooplayback últimas 10 segundos. |
| content_key_specs  <br/> security_level |uint32 |Define los requisitos de solidez del cliente para la reproducción. <br/> 1 - Se requiere criptografía white-box basada en software. <br/> 2 - Se requiere criptografía de software y un descodificador de ofuscación. <br/> 3 - operaciones de cifrado y material de clave Hola deben realizarse dentro de un entorno de ejecución con confianza copia de seguridad de hardware. <br/> 4 - Hola cifrado y descodificación de contenido debe realizarse dentro de un entorno de ejecución con confianza copia de seguridad de hardware.  <br/> 5 - Hola cifrado, descodificación y todos los gestionar de medios de hello (comprimir y descomprimir) debe controlarse en un entorno de ejecución con confianza copia de seguridad de hardware. |
| content_key_specs <br/> required_output_protection.hdc |cadena - una de HDCP_NONE, HDCP_V1, HDCP_V2 |Indica si se requiere HDCP. |
| content_key_specs <br/>key |cadena codificada en Base64 <br/>cadena codificada |Contenido toouse clave para esta pista. Si se especifica, Hola track_type o key_id es necesario.  Esta opción permite al proveedor de contenido de hello clave de contenido de hello tooinject para esta pista en lugar de dejar que el servidor de licencias de Widevine generar o buscar una clave. |
| content_key_specs.key_id |Binario de cadena codificada en Base64, 16 bytes |Identificador único para la clave de Hola. |

## <a name="policy-overrides"></a>Invalidaciones de directivas
| Nombre | Valor | Descripción |
| --- | --- | --- |
| policy_overrides. can_play |valor booleano. true o false |Indica que la reproducción de hello está permitido el contenido. El valor predeterminado es false. |
| policy_overrides. can_persist |valor booleano. true o false |Indica que esa licencia Hola puede ser persistente almacenamiento volátil toonon para su uso sin conexión. El valor predeterminado es false. |
| policy_overrides. can_renew |valor booleano. true o false |Indica que se permite la renovación de la presente licencia. Si es true, se puede ampliar duración Hola de licencia de hello latido. El valor predeterminado es false. |
| policy_overrides. license_duration_seconds |int64 |Indica el período de tiempo de Hola para esta licencia específica. Un valor de 0 indica que no hay ninguna duración toohello de límite. El valor predeterminado es 0. |
| policy_overrides. rental_duration_seconds |int64 |Indica el período de tiempo de hello mientras se permite la reproducción. Un valor de 0 indica que no hay ninguna duración toohello de límite. El valor predeterminado es 0. |
| policy_overrides. playback_duration_seconds |int64 |Hola ver la ventana de tiempo una vez que inicia la reproducción dentro de duración de la licencia de Hola. Un valor de 0 indica que no hay ninguna duración toohello de límite. El valor predeterminado es 0. |
| policy_overrides. renewal_server_url |cadena |Todas las solicitudes de latido (renovación) para esta licencia se destinarán toohello especifica la dirección URL. Este campo solo se utiliza si can_renew es true. |
| policy_overrides. renewal_delay_seconds |int64 |El número de segundos después de license_start_time, antes de intentar la renovación por primera vez. Este campo solo se utiliza si can_renew es true. El valor predeterminado es 0. |
| policy_overrides. renewal_retry_interval_seconds |int64 |Especifica el retraso de hello en segundos entre las solicitudes de renovación de licencias siguientes, en caso de error. Este campo solo se utiliza si can_renew es true. |
| policy_overrides. renewal_recovery_duration_seconds |int64 |ventana Hello de tiempo, en el que la reproducción se permite toocontinue durante la renovación es intento, todavía se realizó correctamente debido a problemas de toobackend con el servidor de licencias de Hola. Un valor de 0 indica que no hay ninguna duración toohello de límite. Este campo solo se utiliza si can_renew es true. |
| policy_overrides. renew_with_usage |valor booleano. true o false |Indica que cuando se inicia el uso, se enviará para la renovación esa licencia Hola. Este campo solo se utiliza si can_renew es true. |

## <a name="session-initialization"></a>Inicialización de la sesión
| Nombre | Valor | Description |
| --- | --- | --- |
| provider_session_token |cadena codificada en Base64 |Este token de sesión se pasa en licencias de Hola y seguirán existiendo en renovaciones posteriores.  no se conservará el token de sesión Hello más allá de las sesiones. |
| provider_client_token |cadena codificada en Base64 |Cliente toosend token en respuesta de la licencia de Hola.  Si la solicitud de licencia de hello contiene un símbolo (token) de cliente, este valor se omite. token de cliente Hello persistan más allá de las sesiones de licencia. |
| override_provider_client_token |valor booleano. true o false |Si la solicitud de licencia de hello y false contiene un símbolo (token) de cliente, usar símbolo (token) de saludo de solicitud de Hola incluso si se especificó un token de cliente en esta estructura.  Si es true, utilice siempre el símbolo (token) de hello especificado en esta estructura. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Configuración de las licencias de Widevine utilizando tipos de .NET
Servicios multimedia proporciona las API de .NET que le permiten configurar sus licencias de Widevine. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Clases tal como se define en hello SDK de .NET de servicios multimedia
siguiente Hola es definiciones de Hola de estos tipos.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Ejemplo
Hola siguiente ejemplo se muestra cómo toouse las API de .NET tooconfigure una licencia de Widevine simple.

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


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte también
[Uso de cifrado dinámico común de PlayReady o Widevine](media-services-protect-with-drm.md)

