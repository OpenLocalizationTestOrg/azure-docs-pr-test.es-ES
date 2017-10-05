---
title: "Administración de los tipos de contenido: Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="0c331-103">Administración de los tipos de contenido en las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="0c331-103">Handle content types in logic apps</span></span>

<span data-ttu-id="0c331-104">Muchos tipos diferentes de contenido pueden pasar a través de una aplicación lógica, como JSON, XML, archivos planos y datos binarios.</span><span class="sxs-lookup"><span data-stu-id="0c331-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="0c331-105">Aunque el motor de Logic App admite todos los tipos de contenido, algunos los entiende de manera inherente.</span><span class="sxs-lookup"><span data-stu-id="0c331-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="0c331-106">Otros pueden requerir conversiones.</span><span class="sxs-lookup"><span data-stu-id="0c331-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="0c331-107">En este artículo se describe cómo administra el motor distintos tipos de contenido y cómo se administran correctamente estos tipos cuando proceda.</span><span class="sxs-lookup"><span data-stu-id="0c331-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="0c331-108">Encabezado Content-Type</span><span class="sxs-lookup"><span data-stu-id="0c331-108">Content-Type Header</span></span>

<span data-ttu-id="0c331-109">Para empezar por lo básico, echemos un vistazo a los dos `Content-Types` que no requieren conversión para usarlos en una aplicación lógica: `application/json` y `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="0c331-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="0c331-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="0c331-110">Application/JSON</span></span>

<span data-ttu-id="0c331-111">El motor de flujo de trabajo se basa en el encabezado `Content-Type` de las llamadas HTTP para determinar el control adecuado.</span><span class="sxs-lookup"><span data-stu-id="0c331-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="0c331-112">Cualquier solicitud con el tipo de contenido `application/json` se almacena y administra como objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="0c331-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="0c331-113">Además, se puede analizar el contenido JSON de forma predeterminada sin necesidad de conversión.</span><span class="sxs-lookup"><span data-stu-id="0c331-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="0c331-114">Por ejemplo, podría analizar una solicitud con el encabezado de tipo de contenido `application/json ` en un flujo de trabajo con una expresión como `@body('myAction')['foo'][0]` para obtener el valor `bar` en este caso:</span><span class="sxs-lookup"><span data-stu-id="0c331-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="0c331-115">No se requieren procesos de conversión adicionales.</span><span class="sxs-lookup"><span data-stu-id="0c331-115">No additional casting is needed.</span></span> <span data-ttu-id="0c331-116">Si trabaja con datos JSON, pero no tienen especificado un encabezado, puede convertirlos manualmente a JSON mediante la función `@json()`, por ejemplo, `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="0c331-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="0c331-117">Esquema y generador de esquemas</span><span class="sxs-lookup"><span data-stu-id="0c331-117">Schema and schema generator</span></span>

<span data-ttu-id="0c331-118">El desencadenador de solicitud le permite incorporar un esquema JSON para la carga útil que espera recibir.</span><span class="sxs-lookup"><span data-stu-id="0c331-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="0c331-119">Este esquema permite al diseñador generar tokens para ayudar al usuario a consumir el contenido de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0c331-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="0c331-120">Si no tiene listo un esquema, seleccione **Usar una carga de ejemplo para generar el esquema** para generar un esquema de JSON a partir de una carga de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0c331-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![SCHEMA (ESQUEMA)](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="0c331-122">Acción "Parse JSON"</span><span class="sxs-lookup"><span data-stu-id="0c331-122">'Parse JSON' action</span></span>

<span data-ttu-id="0c331-123">La acción `Parse JSON` le permite analizar el contenido JSON en tokens descriptivos para el consumo de las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="0c331-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="0c331-124">Al igual que el desencadenador de solicitud, esta acción le permite especificar o generar un esquema JSON para el contenido que desee analizar.</span><span class="sxs-lookup"><span data-stu-id="0c331-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="0c331-125">Esta herramienta facilita enormemente el consumo de datos de Service Bus, Azure Cosmos DB, etc.</span><span class="sxs-lookup"><span data-stu-id="0c331-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="0c331-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="0c331-127">Text/plain</span></span>

<span data-ttu-id="0c331-128">De forma similar a `application/json`, los mensajes HTTP recibidos con el encabezado `Content-Type` de `text/plain` se almacenan en formato sin procesar.</span><span class="sxs-lookup"><span data-stu-id="0c331-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="0c331-129">Además, si los mensajes están incluidos en las acciones posteriores sin conversión alguna, las solicitudes salen con el encabezado `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="0c331-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="0c331-130">Por ejemplo, al trabajar con un archivo plano, podría obtener este contenido HTTP como `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="0c331-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="0c331-131">Si en la siguiente acción, envía la solicitud como cuerpo de otra solicitud (`@body('flatfile')`), esta tendría un encabezado Content-Type `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="0c331-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="0c331-132">Si trabaja con datos de texto sin formato, pero no tienen un encabezado especificado, puede convertirlos manualmente a texto mediante la función `@string()`, por ejemplo, `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="0c331-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="0c331-133">Application/xml, Application/octet-stream y funciones de conversión</span><span class="sxs-lookup"><span data-stu-id="0c331-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="0c331-134">El motor de Logic Apps siempre conserva el encabezado `Content-Type` que se recibiera en la solicitud o respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="0c331-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="0c331-135">Por tanto, si el motor recibe el contenido con `Content-Type` `application/octet-stream` y el usuario incluye ese contenido en una acción posterior sin conversión alguna, la solicitud de salida tiene `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="0c331-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="0c331-136">De esta manera, el motor puede garantizar que no se pierden datos al pasar por el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0c331-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="0c331-137">Sin embargo, el estado de la acción (entradas y salidas) se almacena en un objeto JSON cuando este pasa por el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0c331-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="0c331-138">Por lo tanto, para conservar algunos tipos de datos, el motor convierte el contenido en una cadena con codificación binaria base64 con los metadatos adecuados que conserva `$content` y `$content-type`, que se convierten automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0c331-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="0c331-139">`@json()`: convierte los datos a `application/json`.</span><span class="sxs-lookup"><span data-stu-id="0c331-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="0c331-140">`@xml()`: convierte los datos a `application/xml`.</span><span class="sxs-lookup"><span data-stu-id="0c331-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="0c331-141">`@binary()`: convierte los datos a `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="0c331-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="0c331-142">`@string()`: convierte los datos a `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="0c331-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="0c331-143">`@base64()` : convierte el contenido a una cadena base64.</span><span class="sxs-lookup"><span data-stu-id="0c331-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="0c331-144">`@base64toString()`: convierte una cadena codificada en base64 a `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="0c331-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="0c331-145">`@base64toBinary()`: convierte una cadena codificada en base64 a `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="0c331-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="0c331-146">`@encodeDataUri()` : codifica una cadena como una matriz de bytes dataUri.</span><span class="sxs-lookup"><span data-stu-id="0c331-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="0c331-147">`@decodeDataUri()` : descodifica dataUri en una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="0c331-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="0c331-148">Por ejemplo, si recibió una solicitud HTTP con `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="0c331-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="0c331-149">Podría convertirla y usarla posteriormente con `@xml(triggerBody())`, por ejemplo, o en una función como `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="0c331-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="0c331-150">Otros tipos de contenido</span><span class="sxs-lookup"><span data-stu-id="0c331-150">Other content types</span></span>

<span data-ttu-id="0c331-151">Otros tipos de contenido son compatibles con las aplicaciones lógicas, pero es posible que haya que descodificar `$content` para recuperar manualmente el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="0c331-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="0c331-152">Por ejemplo, supongamos que desencadena una solicitud `application/x-www-url-formencoded` donde `$content` es la carga codificada como cadena base64 para conservar todos los datos:</span><span class="sxs-lookup"><span data-stu-id="0c331-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="0c331-153">Como la solicitud no es texto sin formato o JSON, se almacena en la acción como sigue:</span><span class="sxs-lookup"><span data-stu-id="0c331-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Actualmente no hay una función nativa para datos de formulario, por lo que puede seguir usando estos datos en un flujo de trabajo al acceder a ellos manualmente con una función como `@string(body('formdataAction'))`. Si quisiéramos que la solicitud saliente tuviera también el encabezado content type `application/x-www-url-formencoded`, solo tendría que agregarla al cuerpo de la acción sin realizar ninguna conversión como `@body('formdataAction')`. Sin embargo, este método solo funciona si el cuerpo es el único parámetro de la entrada `body`. <span data-ttu-id="0c331-157">Si intenta usar `@body('formdataAction')` en una solicitud `application/json`, obtendrá un error en tiempo de ejecución, ya que se envía el cuerpo codificado.</span><span class="sxs-lookup"><span data-stu-id="0c331-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

