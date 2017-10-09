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
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="357cb-103">Administración de los tipos de contenido en las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="357cb-103">Handle content types in logic apps</span></span>

<span data-ttu-id="357cb-104">Muchos tipos diferentes de contenido pueden pasar a través de una aplicación lógica, como JSON, XML, archivos planos y datos binarios.</span><span class="sxs-lookup"><span data-stu-id="357cb-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="357cb-105">Mientras Hola motor de lógica de aplicaciones es compatible con todos los tipos de contenido, algunos forma nativa pueda entender Hola motor de lógica de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="357cb-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="357cb-106">Otros pueden requerir conversiones.</span><span class="sxs-lookup"><span data-stu-id="357cb-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="357cb-107">Este artículo describe cómo el motor de hello controla varios tipos de contenido y cómo toocorrectly administrar estos tipos cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="357cb-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="357cb-108">Encabezado Content-Type</span><span class="sxs-lookup"><span data-stu-id="357cb-108">Content-Type Header</span></span>

<span data-ttu-id="357cb-109">toostart básicamente, echemos un vistazo a Hola dos `Content-Types` que no requieren conversión o conversión que puede usar en una aplicación lógica: `application/json` y `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="357cb-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="357cb-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="357cb-110">Application/JSON</span></span>

<span data-ttu-id="357cb-111">motor de flujo de trabajo de Hola se basa en hello `Content-Type` encabezado de HTTP llama control adecuado de toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="357cb-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="357cb-112">Cualquier solicitud con el tipo de contenido de hello `application/json` se almacena y se tratan como un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="357cb-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="357cb-113">Además, se puede analizar el contenido JSON de forma predeterminada sin necesidad de conversión.</span><span class="sxs-lookup"><span data-stu-id="357cb-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="357cb-114">Por ejemplo, podría analizar una solicitud que tiene el encabezado content-type de hello `application/json ` en un flujo de trabajo mediante el uso de una expresión como `@body('myAction')['foo'][0]` valor de hello tooget `bar` en este caso:</span><span class="sxs-lookup"><span data-stu-id="357cb-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="357cb-115">No se requieren procesos de conversión adicionales.</span><span class="sxs-lookup"><span data-stu-id="357cb-115">No additional casting is needed.</span></span> <span data-ttu-id="357cb-116">Si está trabajando con datos que es JSON, pero no tenían un encabezado especificado, podrá manualmente convertirlo tooJSON con hello `@json()` funcione, por ejemplo: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="357cb-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="357cb-117">Esquema y generador de esquemas</span><span class="sxs-lookup"><span data-stu-id="357cb-117">Schema and schema generator</span></span>

<span data-ttu-id="357cb-118">Hello solicitud desencadenador le permite tooenter un esquema JSON para carga Hola espera tooreceive.</span><span class="sxs-lookup"><span data-stu-id="357cb-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="357cb-119">Este esquema permite diseñador Hola generar tokens por lo que puede consumir el contenido de saludo de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="357cb-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="357cb-120">Si no tiene un esquema de listo, seleccione **esquema de uso ejemplo carga toogenerate**, por lo que puede generar un esquema JSON de una carga de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="357cb-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Esquema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="357cb-122">Acción "Parse JSON"</span><span class="sxs-lookup"><span data-stu-id="357cb-122">'Parse JSON' action</span></span>

<span data-ttu-id="357cb-123">Hola `Parse JSON` acción le permite analizar el contenido JSON en tokens descriptivos para el consumo de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="357cb-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="357cb-124">Desencadenador de solicitud toohello similar, esta acción le permite especificar o generar un esquema JSON para contenido que desea tooparse Hola.</span><span class="sxs-lookup"><span data-stu-id="357cb-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="357cb-125">Esta herramienta facilita enormemente el consumo de datos de Service Bus, Azure Cosmos DB, etc.</span><span class="sxs-lookup"><span data-stu-id="357cb-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="357cb-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="357cb-127">Text/plain</span></span>

<span data-ttu-id="357cb-128">Similar demasiado`application/json`, mensajes HTTP recibidos con hello `Content-Type` encabezado de `text/plain` se almacenan en formato sin procesar.</span><span class="sxs-lookup"><span data-stu-id="357cb-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="357cb-129">Además, si los mensajes están incluidos en las acciones posteriores sin conversión alguna, las solicitudes salen con el encabezado `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="357cb-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="357cb-130">Por ejemplo, al trabajar con un archivo plano, podría obtener este contenido HTTP como `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="357cb-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="357cb-131">Si en la siguiente acción hello, enviar solicitud hello como cuerpo del mensaje Hola de otra solicitud (`@body('flatfile')`), solicitud de hello tendría un `text/plain` encabezado Content-Type.</span><span class="sxs-lookup"><span data-stu-id="357cb-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="357cb-132">Si está trabajando con datos que es texto sin formato, pero no tenían un encabezado especificado, puede convertir manualmente Hola datos tootext con hello `@string()` funcione, por ejemplo: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="357cb-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="357cb-133">Application/xml, Application/octet-stream y funciones de conversión</span><span class="sxs-lookup"><span data-stu-id="357cb-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="357cb-134">Hola lógica de aplicaciones motor conserva siempre hello `Content-Type` que se ha recibido en la solicitud HTTP de Hola o de respuesta.</span><span class="sxs-lookup"><span data-stu-id="357cb-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="357cb-135">Por tanto, si el motor de hello recibe el contenido con hello `Content-Type` de `application/octet-stream`, e incluyen que contenido en una acción posterior sin conversión alguna solicitud de salida de hello tiene `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="357cb-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="357cb-136">De esta manera, el motor de hello puede garantizar datos no se pierde mientras lo mueve a través del flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="357cb-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="357cb-137">Sin embargo, el estado de acción de hello (entradas y salidas) se almacena en un objeto JSON como Hola se desplaza del estado a través del flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="357cb-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="357cb-138">Por lo que toopreserve convierte algunos tipos de datos, el motor de Hola Hola tooa contenido codificado en base64 binario cadena con los metadatos adecuados que conserva ambos `$content` y `$content-type`, que se automáticamente se convierten.</span><span class="sxs-lookup"><span data-stu-id="357cb-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="357cb-139">`@json()`-Convierte datos demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="357cb-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="357cb-140">`@xml()`-Convierte datos demasiado`application/xml`</span><span class="sxs-lookup"><span data-stu-id="357cb-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="357cb-141">`@binary()`-Convierte datos demasiado`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="357cb-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="357cb-142">`@string()`-Convierte datos demasiado`text/plain`</span><span class="sxs-lookup"><span data-stu-id="357cb-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="357cb-143">`@base64()`-Convierte la cadena de base64 tooa contenido</span><span class="sxs-lookup"><span data-stu-id="357cb-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="357cb-144">`@base64toString()`-Convierte una cadena codificada en base64 demasiado`text/plain`</span><span class="sxs-lookup"><span data-stu-id="357cb-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="357cb-145">`@base64toBinary()`-Convierte una cadena codificada en base64 demasiado`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="357cb-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="357cb-146">`@encodeDataUri()` : codifica una cadena como una matriz de bytes dataUri.</span><span class="sxs-lookup"><span data-stu-id="357cb-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="357cb-147">`@decodeDataUri()` : descodifica dataUri en una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="357cb-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="357cb-148">Por ejemplo, si recibió una solicitud HTTP con `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="357cb-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="357cb-149">Podría convertirla y usarla posteriormente con `@xml(triggerBody())`, por ejemplo, o en una función como `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="357cb-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="357cb-150">Otros tipos de contenido</span><span class="sxs-lookup"><span data-stu-id="357cb-150">Other content types</span></span>

<span data-ttu-id="357cb-151">Otros tipos de contenido se admiten y trabajar con las aplicaciones lógicas, pero pueden necesitar manualmente al recuperar el cuerpo del mensaje hello mediante la descodificación de hello `$content`.</span><span class="sxs-lookup"><span data-stu-id="357cb-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="357cb-152">Por ejemplo, suponga que desencadena un `application/x-www-url-formencoded` solicitar where `$content` es la carga de hello codificado como una toopreserve de cadena base64, todos los datos:</span><span class="sxs-lookup"><span data-stu-id="357cb-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="357cb-153">Porque la solicitud de hello no es texto sin formato o JSON, solicitud de Hola se almacena en acción Hola como sigue:</span><span class="sxs-lookup"><span data-stu-id="357cb-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Actualmente, no hay una función nativa para los datos de formulario, por lo que puede usar estos datos en un flujo de trabajo accediendo manualmente datos de hello con una función como `@string(body('formdataAction'))`. Si deseara Hola solicitud saliente tooalso tienen hello `application/x-www-url-formencoded` encabezado content-type, podría agregar el cuerpo de acción de hello solicitud toohello sin ninguna conversión como `@body('formdataAction')`. Sin embargo, este método solo funciona si el cuerpo de Hola Hola único parámetro hello `body` entrada. <span data-ttu-id="357cb-157">Si intentas toouse `@body('formdataAction')` en un `application/json` solicitar, obtendrá un error en tiempo de ejecución porque cuerpo codificado de Hola se envía.</span><span class="sxs-lookup"><span data-stu-id="357cb-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

