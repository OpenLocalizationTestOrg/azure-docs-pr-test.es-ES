---
title: "API del recopilador de datos de análisis HTTP aaaLog | Documentos de Microsoft"
description: "Puede usar el repositorio de análisis de registros de hello API de recopilador de datos de análisis de registros HTTP tooadd POST JSON datos toohello desde cualquier cliente que puede llamar a la API de REST de Hola. Este artículo describe cómo toouse Hola API y tiene algunos ejemplos de cómo toopublish datos mediante el uso de diferentes lenguajes de programación."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Enviar datos tooLog análisis con hello API de recopilador de datos HTTP
Este artículo muestra cómo toouse Hola API de recopilador de datos HTTP toosend datos tooLog análisis desde un cliente de la API de REST.  Se describe cómo incluir en una solicitud de datos tooformat recopilados por el script o la aplicación y tiene esa solicitud autorizada por análisis de registros.  Se proporcionan ejemplos de PowerShell, C# y Python.

## <a name="concepts"></a>Conceptos
Puede usar Hola API de recopilador de datos HTTP toosend datos tooLog análisis desde cualquier cliente que puede llamar a una API de REST.  Podría tratarse de un runbook en automatización de Azure que recopila la administración de datos de Azure u otra nube o se podrían formar parte de un sistema de administración alternativo que usa el análisis de registros tooconsolidate y analizar datos.

Todos los datos en el repositorio de análisis de registros de Hola se almacena como un registro con un tipo de registro concreto.  Dar formato a su toohello de toosend de datos API de recopilador de datos HTTP como varios registros en JSON.  Al enviar datos de hello, se crea un registro individual en el repositorio de Hola para cada registro de carga de la solicitud de Hola.


![Información general del recopilador de datos HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Creación de una solicitud
API de recopilador de datos de toouse Hola HTTP, cree una solicitud POST que incluye Hola datos toosend en JavaScript Object Notation (JSON).  Hola siguientes tres tablas lista Hola atributos que son necesarios para cada solicitud. Se describe cada atributo con más detalle más adelante en el artículo de Hola.

### <a name="request-uri"></a>URI de solicitud
| Atributo | Propiedad |
|:--- |:--- |
| Método |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Tipo de contenido |application/json |

### <a name="request-uri-parameters"></a>Parámetros de URI de solicitud
| Parámetro | Descripción |
|:--- |:--- |
| CustomerID |Identificador único de Hello para el área de trabajo de hello Microsoft Operations Management Suite. |
| Recurso |nombre del recurso Hola API: / api/logs. |
| Versión de API |versión de Hola de hello API toouse a esta solicitud. Actualmente, es 2016-04-01. |

### <a name="request-headers"></a>Encabezados de solicitud
| Encabezado | Descripción |
|:--- |:--- |
| Autorización |firma de autorización de Hola. Más adelante en el artículo de hello, puede leer acerca de cómo toocreate un HMAC-SHA256 encabezado. |
| Log-Type |Especifique el tipo de registro de hello de datos de Hola que se está enviando. Actualmente, el tipo de registro de hello es compatible con solo caracteres alfabéticos. No admite valores numéricos ni caracteres especiales. |
| x-ms-date |fecha de Hola se procesó la solicitud hello, en formato RFC 1123. |
| time-generated-field |nombre de Hola de un campo de datos de Hola que contiene la marca de tiempo de Hola Hola del elemento de datos. Si especifica un campo, su contenido se usa para **TimeGenerated**. Si no se especifica este campo, Hola predeterminado para **TimeGenerated** es hora de Hola que hello es ingestión mensaje. contenido de Hello del campo de mensaje de Hola debe seguir el formato de hello ISO 8601 aaaa-MM-ddTHH. |

## <a name="authorization"></a>Autorización
Las API de recopilador de datos de análisis de registro HTTP de solicitud toohello debe incluir un encabezado de autorización. tooauthenticate una solicitud, debe firmar solicitud de hello con hello principal o clave secundaria de Hola de área de trabajo de Hola que está realizando la solicitud de saludo. A continuación, pasar esa firma como parte de la solicitud de saludo.   

Este es el formato hello para el encabezado de autorización de Hola:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* es Hola identificador único para el área de trabajo de hello Operations Management Suite. *Firma* es un [código de autenticación de mensajes basado en Hash (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que está construido a partir de la solicitud de hello y, a continuación, se calcula mediante hello [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Luego se codifica con la codificación Base64.

Utilice este Hola de tooencode formato **SharedKey** cadena de firma:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Este es un ejemplo de una cadena de firma:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Cuando haya cadena de firma de hello, codificar mediante Hola algoritmo HMAC-SHA256 en hello cadena codificada mediante UTF-8 y, a continuación, codificar el resultado de hello como Base64. Use este formato:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

ejemplos de Hello en las secciones siguientes se Hola tienen toohelp de código de ejemplo se crea un encabezado de autorización.

## <a name="request-body"></a>Request body
cuerpo de Hola de mensaje de bienvenida debe estar en JSON. Debe incluir uno o más registros con pares de nombre y valor de propiedad de hello en este formato:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Puede procesar por lotes varios registros en una única solicitud mediante Hola siguiendo el formato. Todos los registros de hello deben estar Hola mismo tipo de registro.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Propiedades y tipo de registro
Definir un tipo de registro personalizado al enviar datos a través de la API de recopilador de datos de análisis de registros HTTP Hola. Actualmente, no se puede escribir datos tooexisting tipos de registro creados por otros tipos de datos y soluciones. Análisis de registros leen los datos entrantes de hello y, a continuación, crea propiedades que coinciden con los tipos de datos de Hola de valores de hello que especifique.

Cada toohello de solicitud API de análisis de registros debe incluir un **tipo de registro** encabezado con el nombre de hello para el tipo de registro de hello. sufijo de Hello **_CL** es nombre automáticamente anexados toohello escriba toodistinguish desde el registro de otro tipos como un registro personalizado. Por ejemplo, si escribe el nombre de hello **MyNewRecordType**, análisis de registros, se crea un registro con el tipo de hello **MyNewRecordType_CL**. Esto ayuda a garantizar que no haya conflictos entre los nombres de tipo creados por el usuario y los incluidos en las soluciones de Microsoft actuales o futuras.

de tipo de datos de la propiedad tooidentify, análisis de registros agrega un nombre de propiedad toohello de sufijo. Si una propiedad contiene un valor null, no se incluye la propiedad hello en ese registro. Esta tabla enumera el tipo de datos de propiedad de Hola y el sufijo correspondiente:

| Tipo de datos de la propiedad | Sufijo |
|:--- |:--- |
| Cadena |_s |
| Booleano |_b |
| Double |_d |
| Fecha/hora |_t |
| GUID |_g |

tipo de datos de Hola que utiliza el análisis de registros para cada propiedad depende de si tipo de registro de hello para el nuevo registro de hello ya existe.

* Si no existe el tipo de registro de hello, análisis de registros crea uno nuevo. Análisis de registros usa Hola JSON inferencia toodetermine Hola tipo de datos para cada propiedad para el nuevo registro de hello.
* Si existe el tipo de registro de hello, análisis de registros intenta toocreate un nuevo registro en función de las propiedades existentes. Si hello tipo de datos para una propiedad en el nuevo registro de hello no coincide con y no se puede convertir toohello existente de tipo o si hello registro incluye una propiedad que no existe, análisis de registros crea una nueva propiedad que tiene el sufijo relevante Hola.

Por ejemplo, esta entrada de envío crearía un registro con tres propiedades **number_d**, **boolean_b** y **string_s**:

![Registro de ejemplo 1](media/log-analytics-data-collector-api/record-01.png)

Si, a continuación, envía la entrada siguiente con todos los valores con formato como cadenas, no debería cambiar propiedades de Hola. Estos valores pueden ser tooexisting convertir tipos de datos:

![Registro de ejemplo 2](media/log-analytics-data-collector-api/record-02.png)

Pero, si, a continuación, ha realizado este envío siguiente, análisis de registros crearía Hola nuevas propiedades **boolean_d** y **string_d**. Estos valores no se pueden convertir:

![Registro de ejemplo 3](media/log-analytics-data-collector-api/record-03.png)

Si, a continuación, envían Hola siguiente entrada, antes de que se creó el tipo de registro de hello, análisis de registros crearía un registro con tres propiedades **número**, **boolean_s**, y **string_s**. En esta entrada, cada uno de los valores iniciales de hello formato es como una cadena:

![Registro de ejemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Límites de datos
Hay algunas restricciones sobre los datos de hello registrados toohello API de recopilación de datos de análisis de registro.

* Máximo de 30 MB por post tooLog API de recopilador de datos de análisis. Se trata de un límite de tamaño para una sola publicación. Si datos Hola desde un solo elemento para exponer que supera los 30 MB, debe dividir Hola datos seguridad toosmaller tamaño fragmentos y envían al mismo tiempo.
* Límite de 32 kB para los valores de campo. Si el valor del campo de hello es mayor que 32 KB, se truncará datos Hola.
* El número máximo recomendado de campos para un tipo determinado es 50. Se trata de un límite práctico desde una perspectiva de la experiencia de búsqueda y la facilidad de uso.  

## <a name="return-codes"></a>Códigos de retorno
Hola código de estado HTTP 200 significa que se ha recibido esa solicitud de hello para el procesamiento. Esto indica que esa operación Hola que se completó correctamente.

Esta tabla muestra hello conjunto completo de códigos de estado que podría devolver el servicio de hello:

| Código | Estado | Código de error | Descripción |
|:--- |:--- |:--- |:--- |
| 200 |OK | |correctamente se aceptó la solicitud de saludo. |
| 400 |Solicitud incorrecta |InactiveCustomer |se ha cerrado el área de trabajo de Hola. |
| 400 |Solicitud incorrecta |InvalidApiVersion |versión de Hola API que especificó no se reconoció por servicio Hola. |
| 400 |Solicitud incorrecta |InvalidCustomerId |Id. de área de trabajo de Hello especificado no es válido. |
| 400 |Solicitud incorrecta |InvalidDataFormat |No envió un formato JSON no válido. cuerpo de respuesta de Hello podría contener más información acerca de cómo tooresolve Hola error. |
| 400 |Solicitud incorrecta |InvalidLogType |tipo de registro de Hello había especificado contiene caracteres especiales o valores numéricos. |
| 400 |Solicitud incorrecta |MissingApiVersion |no se especificó la versión de la API de Hola. |
| 400 |Solicitud incorrecta |MissingContentType |no se especificó el tipo de contenido de Hola. |
| 400 |Solicitud incorrecta |MissingLogType |Hola necesarios no se especificó el tipo de valor de registro. |
| 400 |Solicitud incorrecta |UnsupportedContentType |tipo de contenido de Hello no se estableció demasiado**application/json**. |
| 403 |Prohibido |InvalidAuthorization |servicio de Hola Hola de tooauthenticate solicitudes con error. Compruebe que esa clave de conexión y el Id. de área de trabajo de hello son válidos. |
| 404 |No encontrado | | Dirección URL de hello proporcionada no es correcto, u Hola solicitud es demasiado grande. |
| 429 |Demasiadas solicitudes | | servicio de Hello está experimentando un gran volumen de datos de su cuenta. Vuelva a intentar la solicitud de hello más tarde. |
| 500 |Internal Server Error |UnspecifiedError |servicio de Hello encontró un error interno. Vuelva a intentar la solicitud de saludo. |
| 503 |Servicio no disponible |ServiceUnavailable |servicio de Hello es actualmente las solicitudes de tooreceive disponible. Vuelva a intentar realizar la solicitud. |

## <a name="query-data"></a>Datos de consulta
datos de tooquery enviados por hello API de recopilador de datos de HTTP de análisis de registros, búsqueda de registros con **tipo** que es igual toohello **LogType** valor que ha especificado, se anexa con **_CL**. Por ejemplo, si utilizó **MyCustomLog**, se devolverán todos los registros cuyo **Type= MyCustomLog_CL**.

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de la consulta cambiaría toohello siguiente.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Solicitudes de ejemplo
En las secciones siguientes de hello, encontrará ejemplos de cómo toosubmit datos toohello API de recopilador de datos de análisis de registros HTTP mediante el uso de diferentes lenguajes de programación.

Para cada ejemplo, realice estos pasos tooset variables de hello para el encabezado de autorización de hello:

1. En el portal de Operations Management Suite hello, seleccione hello **configuración** icono y, a continuación, seleccione hello **orígenes conectados** ficha.
2. toohello derecha de **Id. de área de trabajo**, seleccione el icono de copiar de Hola y, a continuación, pegue el identificador hello como valor de Hola de hello **Id. de cliente** variable.
3. toohello derecha de **Primary Key**, seleccione el icono de copiar de Hola y, a continuación, pegue el identificador hello como valor de Hola de hello **Shared Key** variable.

Como alternativa, puede cambiar las variables de hello para el tipo de registro de hello y datos JSON.

### <a name="powershell-sample"></a>Ejemplo de PowerShell
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>Ejemplo de C#
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Ejemplo de Python
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Pasos siguientes
- Hola de uso [API de búsqueda de registros](log-analytics-log-search-api.md) tooretrieve datos del repositorio de análisis de registros de Hola.
