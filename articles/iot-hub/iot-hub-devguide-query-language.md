---
title: Hola aaaUnderstand lenguaje de consultas del centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - descripción del lenguaje de consulta similar a SQL centro de IoT hello usa tooretrieve saber: los gemelos de dispositivo y los trabajos desde el centro de IoT."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes

Centro de IoT proporciona una información de tooretrieve eficaz lenguaje similar a SQL con respecto a [: los gemelos de dispositivo] [ lnk-twins] y [trabajos][lnk-jobs]y [enrutamiento de mensajes][lnk-devguide-messaging-routes]. Este artículo presenta:

* Una introducción toohello principales las funciones de lenguaje de consultas del centro de IoT, hello y
* Hola descripción detallada del lenguaje de Hola.

## <a name="get-started-with-device-twin-queries"></a>Introducción a las consultas de dispositivos gemelos
Los [dispositivos gemelos][lnk-twins] pueden contener objetos JSON arbitrarios como etiquetas y propiedades. Centro de IoT permite: los gemelos de tooquery dispositivo como un solo documento JSON que contiene toda la información de dispositivo gemelas.
Da por supuesto, por ejemplo, que su: los gemelos de IoT hub dispositivo Hola siguiente estructura:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

Centro de IoT expone: los gemelos de hello dispositivo como una colección de documentos denominada **dispositivos**.
Por lo que Hola después de consulta recupera el conjunto completo de Hola de: los gemelos de dispositivo:

```sql
SELECT * FROM devices
```

> [!NOTE]
> Los [SDK IoT de Azure][lnk-hub-sdks] admiten la paginación de resultados de gran tamaño.

Centro de IoT le permite filtrar con condiciones arbitrarias de: los gemelos de tooretrieve dispositivo. Por ejemplo,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

Recupera Hola: los gemelos de dispositivo con hello **location.region** etiqueta establecido demasiado**US**.
También se admiten operadores booleanos y comparaciones aritméticas, por ejemplo,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

Recupera todos los gemelos de dispositivo ubicados en hello nos configurado toosend telemetría menor frecuencia que cada minuto. Para su comodidad, también es posible toouse constantes de matriz con hello **IN** y **NEN** operadores (no en). Por ejemplo,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

recupera todos los dispositivos gemelos que notificaron conectividad WiFi o con cable. Es a menudo necesario tooidentify todos los gemelos de dispositivo que contienen una propiedad concreta. Centro de IoT es compatible con la función de hello `is_defined()` para este propósito. Por ejemplo,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

recuperar todos los gemelos de dispositivo que definen hello `connectivity` informa de la propiedad. Consulte toohello [cláusula WHERE] [ lnk-query-where] sección de referencia completa de Hola de hello capacidades de filtrado.

También se admiten la agrupación y las agregaciones. Por ejemplo,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Devuelve el recuento de Hola de dispositivos de hello en cada estado de la configuración de telemetría.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Hello en el ejemplo anterior se muestra una situación donde tres dispositivos notifican una configuración correcta, dos se sigue aplicando configuración hello y uno informó de un error.

### <a name="c-example"></a>Ejemplo de C#
funcionalidad de consulta de Hola se expone mediante hello [C# SDK del servicio] [ lnk-hub-sdks] en hello **RegistryManager** clase.
Este ejemplo corresponde a una consulta simple:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Tenga en cuenta cómo Hola **consulta** se crea una instancia de objeto con un tamaño de página (arriba too1000) y, a continuación, se pueden recuperar varias páginas que realiza la llamada hello **GetNextAsTwinAsync** métodos varias veces.
Tenga en cuenta ese objeto de consulta de hello expone varios **siguiente\***, dependiendo de opción de deserialización Hola requeridos por la consulta de hello, como objetos de trabajo o gemelas del dispositivo, o sin formato toobe JSON que usar cuando se empleen las proyecciones.

### <a name="nodejs-example"></a>Ejemplo de Node.js
funcionalidad de consulta de Hola se expone mediante hello [servicio IoT de Azure SDK para Node.js] [ lnk-hub-sdks] en hello **registro** objeto.
Este ejemplo corresponde a una consulta simple:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Tenga en cuenta cómo Hola **consulta** se crea una instancia de objeto con un tamaño de página (arriba too1000) y, a continuación, se pueden recuperar varias páginas que realiza la llamada hello **nextAsTwin** métodos varias veces.
Tenga en cuenta ese objeto de consulta de hello expone varios **siguiente\***, dependiendo de opción de deserialización Hola requeridos por la consulta de hello, como objetos de trabajo o gemelas del dispositivo, o sin formato toobe JSON que usar cuando se empleen las proyecciones.

### <a name="limitations"></a>Limitaciones
> [!IMPORTANT]
> Resultados de la consulta pueden tener unos minutos de retraso con valores más recientes de respeto toohello en: los gemelos de dispositivo. Si consulta: los gemelos de dispositivos individuales por Id., siempre es preferible toouse Hola recuperar dispositivo gemelas API, que siempre contiene valores más recientes de Hola y tiene el límite superior de límites.

Actualmente, las comparaciones solo se admiten entre tipos primitivos (no objetos), por ejemplo `... WHERE properties.desired.config = properties.reported.config` solo se admite si esas propiedades tienen valores primitivos.

## <a name="get-started-with-jobs-queries"></a>Introducción a las consultas de trabajos
[Trabajos] [ lnk-jobs] proporcionan una manera tooexecute operaciones en conjuntos de dispositivos. Cada gemelas dispositivo contiene información de Hola de trabajos de hello del cual forma parte de una colección denominada **trabajos**.
Lógicamente,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Actualmente, esta colección es consultable como **devices.jobs** Hola lenguaje de consultas del centro de IoT.

> [!IMPORTANT]
> Actualmente, la propiedad de trabajos de hello nunca se devuelve al consultar a: los gemelos de dispositivo (es decir, las consultas que contiene 'desde dispositivos'). Solo es accesible directamente con las consultas que utilizan `FROM devices.jobs`.
>
>

Por ejemplo, tooget todos los trabajos (pasados y programados) que afectan a un único dispositivo, puede usar Hola después de consulta:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Tenga en cuenta cómo esta consulta proporciona el estado específico del dispositivo de hello (y posiblemente Hola método directo respuesta) de cada trabajo que se devuelve.
También es posible toofilter con condiciones booleanas arbitrarias en todas las propiedades de objeto de hello **devices.jobs** colección.
Por ejemplo, Hola consulta siguiente:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

recupera todos los trabajos de actualización de dispositivos gemelos completados para el dispositivo **myDeviceId** que se crearon después de septiembre de 2016.

También es posible tooretrieve resultados de por dispositivo de Hola de un único trabajo.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Limitaciones
Actualmente, las consultas en **devices.jobs** no admiten:

* proyecciones, por lo tanto, solo `SELECT *` es posible.
* Condiciones que hacen referencia a toohello gemelas de dispositivo en las propiedades de toojob de suma (vea la sección anterior de hello).
* realizar agregaciones, como count, avg, group by.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Introducción a expresiones de consulta de rutas de mensajes de dispositivo a la nube

Usar [rutas de dispositivo para la nube][lnk-devguide-messaging-routes], puede configurar centro de IoT toodispatch dispositivo a la nube mensajes extremos de toodifferent basados en expresiones evaluadas en mensajes individuales.

ruta de Hello [condición] [ lnk-query-expressions] usa Hola mismo lenguaje de consultas del centro de IoT como condiciones en las consultas gemelas y trabajo. Condiciones de ruta se evalúan en los encabezados de mensaje de Hola y cuerpo. La expresión de consulta de enrutamiento puede implicar sólo los encabezados de mensaje, sólo cuerpo del mensaje hello, o ambos encabezados de mensaje y cuerpo del mensaje. Centro de IoT se da por supuesto un esquema específico para los encabezados de Hola y el cuerpo del mensaje en mensajes de pedido tooroute y hello las secciones siguientes describe lo que se requiere para la ruta de centro de IoT tooproperly:

### <a name="routing-on-message-headers"></a>Enrutamiento en los encabezados del mensaje

Centro de IoT se da por supuesto Hola después de la representación JSON de encabezados de mensaje para enrutar el mensaje:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Propiedades de sistema de mensajes tienen el prefijo hello `'$'` símbolos.
Siempre se accede a las propiedades de usuario con su nombre. Si un nombre de propiedad de usuario produce toocoincide con una propiedad del sistema (como `$to`), se recuperará la propiedad de usuario de hello con hello `$to` expresión.
Siempre puede tener acceso a propiedad de sistema de hello mediante corchetes `{}`: por ejemplo, puede utilizar la expresión de hello `{$to}` tooaccess Hola propiedad del sistema `to`. Nombres de propiedad entre corchetes siempre recuperan la propiedad del sistema correspondiente Hola.

Recuerde que los nombres de propiedad no distinguen mayúsculas de minúsculas.

> [!NOTE]
> Todas las propiedades de mensaje son cadenas. Propiedades del sistema, como se describe en hello [Guía del desarrollador][lnk-devguide-messaging-format], no están actualmente disponible toouse en las consultas.
>

Por ejemplo, si utiliza un `messageType` propiedad, puede que desee tooroute todos los extremos de tooone de telemetría y el punto de conexión de todas las alertas tooanother. Puede escribir Hola después de telemetría de hello tooroute de expresión:

```sql
messageType = 'telemetry'
```

Y Hola siguiendo los mensajes de alerta Hola expresión tooroute:

```sql
messageType = 'alert'
```

También se admiten las funciones y expresiones booleanas. Esta característica permite toodistinguish entre el nivel de gravedad, por ejemplo:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Consulte toohello [expresiones y condiciones] [ lnk-query-expressions] sección de la lista completa de Hola de funciones y operadores compatibles.

### <a name="routing-on-message-bodies"></a>Enrutamiento en los cuerpos del mensaje

Centro de IoT solamente puede enrutar basado en el cuerpo del mensaje contenido si el cuerpo del mensaje Hola esté correctamente formado JSON codificado en UTF-8, UTF-16 o UTF-32. Debe establecer el tipo de contenido de Hola de mensaje de saludo demasiado`application/json` y Hola contenido tooone de codificación de hello admite las codificaciones UTF en tooallow de encabezados de mensaje de Hola mensajes de bienvenida del centro de IoT tooroute según el contenido del cuerpo de Hola. Si no se especifica cualquiera de los encabezados de hello, centro de IoT no intentará tooevaluate cualquier expresión de consulta que contenga cuerpo hello en el mensaje de bienvenida. Si el mensaje no es un mensaje JSON, o si no especifica mensajes de bienvenida del tipo de contenido de Hola y codificación de contenido, puede seguir utilizando tooroute mensaje de saludo en función de los encabezados de mensaje de Hola el enrutamiento de mensajes.

Puede usar `$body` en el mensaje de saludo de tooroute de expresión de consulta de Hola. Puede usar una referencia de cuerpo simple, referencia de la matriz de cuerpo o varias referencias de cuerpo en la expresión de consulta de Hola. La expresión de consulta también puede combinar una referencia al cuerpo con una referencia al encabezado del mensaje. Por ejemplo, la siguiente Hola es todas las expresiones de consulta válida:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Conceptos básicos de una consulta de IoT Hub
Cada consulta de IoT Hub consta de cláusulas SELECT y FROM, y de cláusulas WHERE y GROUP BY opcionales. Cada consulta se ejecuta en una colección de documentos JSON, por ejemplo, dispositivos gemelos. cláusula FROM de Hello indica Hola documento colección toobe recorren en iteración en (**dispositivos** o **devices.jobs**). A continuación, Hola filtro Hola donde se aplica la cláusula. Con agregaciones, se agrupan los resultados de Hola de este paso como se especifica en Hola de cláusula GROUP BY y, para cada grupo, se genera una fila según se haya especificado en la cláusula SELECT Hola.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>Cláusula FROM
Hola **de < from_specification >** cláusula puede asumir solo dos valores: **desde dispositivos**, tooquery: los gemelos de dispositivo, o **de devices.jobs**, trabajo tooquery por dispositivo detalles.

## <a name="where-clause"></a>Cláusula WHERE
Hola **donde < filter_condition >** cláusula es opcional. Especifica una o varias condiciones que deben satisfacer los documentos JSON de hello en la colección de hello FROM toobe incluido como parte del resultado de hello. Se debe evaluar cualquier documento JSON Hola especifica condiciones demasiado "true" toobe incluida en el resultado de hello.

Hola permite condiciones se describen en la sección [expresiones y condiciones][lnk-query-expressions].

## <a name="select-clause"></a>Cláusula SELECT
cláusula SELECT Hello (**seleccione < select_list >**) es obligatorio y especifica qué valores se recuperan de la consulta de Hola. Especifica Hola JSON valores toobe utiliza toogenerate nuevos objetos JSON.
Para cada elemento de Hola subconjunto filtrado (y, opcionalmente, agrupado) del conjunto de FROM de hello, fase de proyección de hello genera un nuevo objeto JSON, construido con valores de hello especificados en la cláusula SELECT Hola.

Aquí te mostramos gramática Hola de cláusula SELECT hello:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

donde **attribute_name** hace referencia la propiedad tooany del documento JSON de hello en la colección de hello FROM. Algunos ejemplos de las cláusulas SELECT pueden encontrarse en hello [Introducción a las consultas de dispositivo gemelas] [ lnk-query-getstarted] sección.

Actualmente, las cláusulas de selección distintas a **SELECT \*** solo se admiten en las consultas agregadas de dispositivos gemelos.

## <a name="group-by-clause"></a>Cláusula GROUP BY
Hola **GROUP BY < group_specification >** cláusula es un paso opcional que se puede ejecutar después de filtro de hello especificado Hola de cláusula WHERE y antes de la proyección de hello especificada en hello seleccione. Agrupa documentos basados en el valor de Hola de un atributo. Estos grupos son utilizados toogenerate agregado valores tal como se especifica en la cláusula SELECT Hola.

Un ejemplo de consulta con GROUP BY es:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

sintaxis formal de Hola de GROUP BY es:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

donde **attribute_name** hace referencia la propiedad tooany del documento JSON de hello en la colección de hello FROM.

Actualmente, solo se admite la cláusula GROUP BY Hola al consultar a: los gemelos de dispositivo.

## <a name="expressions-and-conditions"></a>Expresiones y condiciones
Brevemente, una *expresión*:

* Se evalúa como instancia de tooan de un tipo JSON (por ejemplo, un valor booleano, número, cadena, matriz u objeto), y
* Se define mediante la manipulación de datos procedentes de documento JSON de dispositivo de Hola y constantes que se utilizan funciones y operadores integrados.

*Condiciones* son expresiones que se evalúan tooa un valor booleano. Cualquier constante diferente a un valor booleano **true** se considera como **false** (incluidos **null**, **indefinido**, cualquier instancia de objeto o matriz, cualquier cadena, claramente hello y un valor booleano **false**).

sintaxis de Hola de expresiones es:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

donde:

| Símbolo | Definición |
| --- | --- |
| attribute_name | Cualquier propiedad de documento JSON de Hola Hola **FROM** colección. |
| binary_operator | Cualquier operador binario enumerados en hello [operadores](#operators) sección. |
| function_name| Cualquier función que se muestra en hello [funciones](#functions) sección. |
| decimal_literal |Un valor float expresado en notación decimal. |
| hexadecimal_literal |Un número expresado por cadena hello '0 x' seguido por una cadena de dígitos hexadecimales. |
| string_literal |Los literales de cadena son cadenas Unicode representadas por una secuencia de cero o varios caracteres Unicode o secuencias de escape. Los literales de cadena se encierran entre comillas simples (apóstrofo: ') o comillas dobles (comillas: "). Caracteres de escape permitidos: `\'`, `\"`, `\\`, `\uXXXX` para los caracteres Unicode definidos con 4 dígitos hexadecimales. |

### <a name="operators"></a>Operadores
se admite Hola siguientes operadores:

| Familia | Operadores |
| --- | --- |
| Aritméticos |+,-,*,/,% |
| Lógicos |AND, OR, NOT |
| De comparación |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Functions
Cuando se consultan hello: los gemelos y los trabajos solo admitido la función es:

| Función | Descripción |
| -------- | ----------- |
| IS_DEFINED(property) | Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor (incluido `null`). |

En condiciones de rutas, se admite Hola siguientes funciones matemáticas:

| Función | Descripción |
| -------- | ----------- |
| ABS(x) | Devuelve Hola valor absoluto (positivo) de hello especifica la expresión numérica. |
| EXP(x) | Devuelve Hola valor exponencial de hello especifica la expresión numérica (e ^ x). |
| POWER(x,y) | Devuelve Hola valo Hola especificado expresión toohello potencia especificada (x ^ y).|
| SQUARE(x) | Hola devuelve cuadrado de hello especifica el valor numérico. |
| CEILING(x) | Devuelve Hola valor entero más pequeño mayor o igual a, Hola expresión numérica especificada. |
| FLOOR(x) | Devuelve Hola mayor entero menor o igual toohello especifica la expresión numérica. |
| SIGN(x) | Devuelve Hola positivo (+ 1), cero (0), o signo negativo (-1) de hello especificado expresión numérica.|
| SQRT(x) | Hola devuelve cuadrado de hello especifica el valor numérico. |

En condiciones de rutas, se admite Hola después el tipo de comprobación y las funciones de conversión:

| Función | Descripción |
| -------- | ----------- |
| AS_NUMBER | Convierte el número de tooa de cadena de entrada de Hola. `noop` si la entrada es un número; `Undefined` si la cadena no representa un número.|
| IS_ARRAY | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una matriz. |
| IS_BOOL | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un valor booleano. |
| IS_DEFINED | Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor. |
| IS_NULL | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es null. |
| IS_NUMBER | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un número. |
| IS_OBJECT | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un objeto JSON. |
| IS_PRIMITIVE | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un tipo primitivo (cadena, booleano, numérico o `null`). |
| IS_STRING | Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una cadena. |

En condiciones de rutas, se admite Hola siguiendo las funciones de cadena:

| Función | Descripción |
| -------- | ----------- |
| CONCAT(x, …) | Devuelve una cadena que es el resultado de hello de concatenar dos o más valores de cadena. |
| LENGTH(x) | Devuelve el número de caracteres de Hola Hola especificado expresión de cadena.|
| LOWER(x) | Devuelve una expresión de cadena después de convertir toolowercase de datos de caracteres en mayúsculas. |
| UPPER(x) | Devuelve una expresión de cadena después de convertir toouppercase de datos de carácter en minúscula. |
| SUBSTRING(string, start [, length]) | Devuelve parte de una expresión de cadena a partir de hello especifica la posición de base cero del carácter y continúa toohello especifica la longitud o toohello final de cadena de Hola. |
| INDEX_OF(string, fragment) | Devuelve Hola a partir de la posición de la primera aparición de hello de la segunda expresión de cadena Hola dentro de la primera expresión de cadena especificada de hello, o -1 si no se encuentra la cadena de Hola.|
| STARTS_WITH(x, y) | Devuelve un valor booleano que indica si primera expresión de cadena Hola empieza por hello en segundo lugar. |
| ENDS_WITH(x, y) | Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar. |
| CONTAINS(x,y) | Devuelve un valor booleano que indica si primera expresión de cadena hello contiene hello en segundo lugar. |

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo tooexecute las consultas en sus aplicaciones usando [SDK de Azure IoT][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
