---
title: tipos de contenido de aaaHandle - Azure Logic Apps | Documentos de Microsoft
description: "Administración de Azure Logic Apps de los tipos de contenido en los procesos de diseño y runtime"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Administración de los tipos de contenido en las aplicaciones lógicas

Muchos tipos diferentes de contenido pueden pasar a través de una aplicación lógica, como JSON, XML, archivos planos y datos binarios. Mientras Hola motor de lógica de aplicaciones es compatible con todos los tipos de contenido, algunos forma nativa pueda entender Hola motor de lógica de aplicaciones. Otros pueden requerir conversiones. Este artículo describe cómo el motor de hello controla varios tipos de contenido y cómo toocorrectly administrar estos tipos cuando sea necesario.

## <a name="content-type-header"></a>Encabezado Content-Type

toostart básicamente, echemos un vistazo a Hola dos `Content-Types` que no requieren conversión o conversión que puede usar en una aplicación lógica: `application/json` y `text/plain`.

## <a name="applicationjson"></a>Application/JSON

motor de flujo de trabajo de Hola se basa en hello `Content-Type` encabezado de HTTP llama control adecuado de toodetermine Hola. Cualquier solicitud con el tipo de contenido de hello `application/json` se almacena y se tratan como un objeto JSON. Además, se puede analizar el contenido JSON de forma predeterminada sin necesidad de conversión. 

Por ejemplo, podría analizar una solicitud que tiene el encabezado content-type de hello `application/json ` en un flujo de trabajo mediante el uso de una expresión como `@body('myAction')['foo'][0]` valor de hello tooget `bar` en este caso:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

No se requieren procesos de conversión adicionales. Si está trabajando con datos que es JSON, pero no tenían un encabezado especificado, podrá manualmente convertirlo tooJSON con hello `@json()` funcione, por ejemplo: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Esquema y generador de esquemas

Hello solicitud desencadenador le permite tooenter un esquema JSON para carga Hola espera tooreceive. Este esquema permite diseñador Hola generar tokens por lo que puede consumir el contenido de saludo de solicitud de saludo. Si no tiene un esquema de listo, seleccione **esquema de uso ejemplo carga toogenerate**, por lo que puede generar un esquema JSON de una carga de ejemplo.

![Esquema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Acción "Parse JSON"

Hola `Parse JSON` acción le permite analizar el contenido JSON en tokens descriptivos para el consumo de aplicación lógica. Desencadenador de solicitud toohello similar, esta acción le permite especificar o generar un esquema JSON para contenido que desea tooparse Hola. Esta herramienta facilita enormemente el consumo de datos de Service Bus, Azure Cosmos DB, etc.

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Text/plain

Similar demasiado`application/json`, mensajes HTTP recibidos con hello `Content-Type` encabezado de `text/plain` se almacenan en formato sin procesar. Además, si los mensajes están incluidos en las acciones posteriores sin conversión alguna, las solicitudes salen con el encabezado `Content-Type`: `text/plain`. Por ejemplo, al trabajar con un archivo plano, podría obtener este contenido HTTP como `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

Si en la siguiente acción hello, enviar solicitud hello como cuerpo del mensaje Hola de otra solicitud (`@body('flatfile')`), solicitud de hello tendría un `text/plain` encabezado Content-Type. Si está trabajando con datos que es texto sin formato, pero no tenían un encabezado especificado, puede convertir manualmente Hola datos tootext con hello `@string()` funcione, por ejemplo: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml, Application/octet-stream y funciones de conversión

Hola lógica de aplicaciones motor conserva siempre hello `Content-Type` que se ha recibido en la solicitud HTTP de Hola o de respuesta. Por tanto, si el motor de hello recibe el contenido con hello `Content-Type` de `application/octet-stream`, e incluyen que contenido en una acción posterior sin conversión alguna solicitud de salida de hello tiene `Content-Type`: `application/octet-stream`. De esta manera, el motor de hello puede garantizar datos no se pierde mientras lo mueve a través del flujo de trabajo de Hola. Sin embargo, el estado de acción de hello (entradas y salidas) se almacena en un objeto JSON como Hola se desplaza del estado a través del flujo de trabajo de Hola. Por lo que toopreserve convierte algunos tipos de datos, el motor de Hola Hola tooa contenido codificado en base64 binario cadena con los metadatos adecuados que conserva ambos `$content` y `$content-type`, que se automáticamente se convierten. 

* `@json()`-Convierte datos demasiado`application/json`
* `@xml()`-Convierte datos demasiado`application/xml`
* `@binary()`-Convierte datos demasiado`application/octet-stream`
* `@string()`-Convierte datos demasiado`text/plain`
* `@base64()`-Convierte la cadena de base64 tooa contenido
* `@base64toString()`-Convierte una cadena codificada en base64 demasiado`text/plain`
* `@base64toBinary()`-Convierte una cadena codificada en base64 demasiado`application/octet-stream`
* `@encodeDataUri()` : codifica una cadena como una matriz de bytes dataUri.
* `@decodeDataUri()` : descodifica dataUri en una matriz de bytes.

Por ejemplo, si recibió una solicitud HTTP con `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Podría convertirla y usarla posteriormente con `@xml(triggerBody())`, por ejemplo, o en una función como `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Otros tipos de contenido

Otros tipos de contenido se admiten y trabajar con las aplicaciones lógicas, pero pueden necesitar manualmente al recuperar el cuerpo del mensaje hello mediante la descodificación de hello `$content`. Por ejemplo, suponga que desencadena un `application/x-www-url-formencoded` solicitar where `$content` es la carga de hello codificado como una toopreserve de cadena base64, todos los datos:

```
CustomerName=Frank&Address=123+Avenue
```

Porque la solicitud de hello no es texto sin formato o JSON, solicitud de Hola se almacena en acción Hola como sigue:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Actualmente, no hay una función nativa para los datos de formulario, por lo que puede usar estos datos en un flujo de trabajo accediendo manualmente datos de hello con una función como `@string(body('formdataAction'))`. Si deseara Hola solicitud saliente tooalso tienen hello `application/x-www-url-formencoded` encabezado content-type, podría agregar el cuerpo de acción de hello solicitud toohello sin ninguna conversión como `@body('formdataAction')`. Sin embargo, este método solo funciona si el cuerpo de Hola Hola único parámetro hello `body` entrada. Si intentas toouse `@body('formdataAction')` en un `application/json` solicitar, obtendrá un error en tiempo de ejecución porque cuerpo codificado de Hola se envía.

