---
title: Trabajo con desencadenadores y enlaces de Azure Functions | Microsoft Docs
description: "Obtenga información sobre cómo usar desencadenadores y enlaces en Azure Functions para conectar la ejecución del código a los eventos en línea y servicios basados en la nube."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="bce79-104">Conceptos básicos sobre los enlaces y desencadenadores de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bce79-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="bce79-105">Azure Functions le permite escribir código en respuesta a eventos en Azure y otros servicios mediante *desencadenadores* y *enlaces*.</span><span class="sxs-lookup"><span data-stu-id="bce79-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="bce79-106">En este artículo, se ofrece una introducción conceptual a los desencadenadores y enlaces de todos los lenguajes de programación compatibles.</span><span class="sxs-lookup"><span data-stu-id="bce79-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="bce79-107">Aquí se describen características comunes de todos los enlaces.</span><span class="sxs-lookup"><span data-stu-id="bce79-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="bce79-108">Información general</span><span class="sxs-lookup"><span data-stu-id="bce79-108">Overview</span></span>

<span data-ttu-id="bce79-109">Los desencadenadores y enlaces permiten definir de forma declarativa cómo se invoca una función y con qué datos funcionará.</span><span class="sxs-lookup"><span data-stu-id="bce79-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="bce79-110">Los *desencadenadores* establecen el modo de invocar una función.</span><span class="sxs-lookup"><span data-stu-id="bce79-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="bce79-111">Cada función debe tener exactamente un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="bce79-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="bce79-112">Los desencadenadores tienen datos asociados, que suelen ser la carga que desencadenó la función.</span><span class="sxs-lookup"><span data-stu-id="bce79-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="bce79-113">Los *enlaces* de entrada y de salida permiten conectarse de manera declarativa a datos desde el código.</span><span class="sxs-lookup"><span data-stu-id="bce79-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="bce79-114">De forma similar a los desencadenadores, se pueden especificar las cadenas de conexión y otras propiedades en la configuración de la función.</span><span class="sxs-lookup"><span data-stu-id="bce79-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="bce79-115">Los enlaces son opcionales y cada función puede tener varios enlaces de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="bce79-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="bce79-116">Mediante los desencadenadores y enlaces, puede escribir código más genérico sin codificar de forma rígida los detalles de los servicios con los que interactúa.</span><span class="sxs-lookup"><span data-stu-id="bce79-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="bce79-117">Los datos procedentes de los servicios se convierten simplemente en valores de entrada para el código de función.</span><span class="sxs-lookup"><span data-stu-id="bce79-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="bce79-118">Si desea enviar datos a otro servicio (por ejemplo, para crear una fila nueva en Azure Table Storage), utilice el valor devuelto por el método.</span><span class="sxs-lookup"><span data-stu-id="bce79-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="bce79-119">O bien, si necesita enviar varios valores, use un objeto auxiliar.</span><span class="sxs-lookup"><span data-stu-id="bce79-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="bce79-120">Los desencadenadores y los enlaces cuentan con una propiedad denominada **name**, un identificador que se emplea en el código para acceder al enlace.</span><span class="sxs-lookup"><span data-stu-id="bce79-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="bce79-121">Puede configurar desencadenadores y enlaces en la pestaña **Integrar** del portal de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="bce79-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="bce79-122">Entre bastidores, la interfaz de usuario modifica un archivo llamado *function.json* en el directorio de la función.</span><span class="sxs-lookup"><span data-stu-id="bce79-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="bce79-123">Este archivo puede editarse cambiando a la opción **Editor avanzado**.</span><span class="sxs-lookup"><span data-stu-id="bce79-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="bce79-124">En la siguiente tabla, se muestran los desencadenadores y enlaces compatibles con Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="bce79-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="bce79-125">Ejemplo: desencadenador de colas y enlace de salida de tablas</span><span class="sxs-lookup"><span data-stu-id="bce79-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="bce79-126">Supongamos que quiere escribir una fila nueva en Azure Table Storage cada vez que aparezca un nuevo mensaje en Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="bce79-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="bce79-127">Este escenario puede implementarse mediante un desencadenador de colas de Azure y un enlace de salida de tablas.</span><span class="sxs-lookup"><span data-stu-id="bce79-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="bce79-128">Los desencadenadores de colas precisan de la siguiente información en la pestaña **Integrar**:</span><span class="sxs-lookup"><span data-stu-id="bce79-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="bce79-129">El nombre del valor de configuración de la aplicación que contiene la cadena de conexión de la cuenta de almacenamiento para la cola</span><span class="sxs-lookup"><span data-stu-id="bce79-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="bce79-130">El nombre de la cola</span><span class="sxs-lookup"><span data-stu-id="bce79-130">The queue name</span></span>
* <span data-ttu-id="bce79-131">El identificador del código que leerá el contenido del mensaje de la cola, como, por ejemplo, `order`</span><span class="sxs-lookup"><span data-stu-id="bce79-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="bce79-132">Para escribir en Azure Table Storage, utilice un enlace de salida con estos datos:</span><span class="sxs-lookup"><span data-stu-id="bce79-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="bce79-133">El nombre del valor de configuración de la aplicación que contiene la cadena de conexión de la cuenta de almacenamiento para la tabla</span><span class="sxs-lookup"><span data-stu-id="bce79-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="bce79-134">El nombre de la tabla</span><span class="sxs-lookup"><span data-stu-id="bce79-134">The table name</span></span>
* <span data-ttu-id="bce79-135">El identificador del código que creará los elementos de salida o el valor devuelto por la función</span><span class="sxs-lookup"><span data-stu-id="bce79-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="bce79-136">Los enlaces se sirven de los valores de configuración de la aplicación para que las cadenas de conexión apliquen el procedimiento recomendado de que *function.json* no contenga secretos de los servicios.</span><span class="sxs-lookup"><span data-stu-id="bce79-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="bce79-137">A continuación, utilice los identificadores que facilitó para posibilitar la integración con Azure Storage en el código.</span><span class="sxs-lookup"><span data-stu-id="bce79-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="bce79-138">Esta es la función *function.json* correspondiente al código anterior.</span><span class="sxs-lookup"><span data-stu-id="bce79-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="bce79-139">Tenga en cuenta que se puede emplear la misma configuración, con independencia del lenguaje de la implementación de la función.</span><span class="sxs-lookup"><span data-stu-id="bce79-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="bce79-140">Para ver y editar el contenido de *function.json* en el portal de Azure, haga clic en la opción **Editor avanzado** en la pestaña **Integrar** de la función.</span><span class="sxs-lookup"><span data-stu-id="bce79-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="bce79-141">Para obtener más ejemplos de código e información sobre la integración con Azure Storage, consulte el artículo sobre [desencadenadores y enlaces de Azure Functions para Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bce79-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="bce79-142">Dirección de los enlaces</span><span class="sxs-lookup"><span data-stu-id="bce79-142">Binding direction</span></span>

<span data-ttu-id="bce79-143">Todos los desencadenadores y enlaces tienen la propiedad `direction`:</span><span class="sxs-lookup"><span data-stu-id="bce79-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="bce79-144">En el caso de los desencadenadores, esta propiedad siempre aparece como `in`</span><span class="sxs-lookup"><span data-stu-id="bce79-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="bce79-145">Los enlaces de entrada y de salida usan `in` y `out`</span><span class="sxs-lookup"><span data-stu-id="bce79-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="bce79-146">Algunos enlaces admiten la dirección especial `inout`.</span><span class="sxs-lookup"><span data-stu-id="bce79-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="bce79-147">Si utiliza `inout`, solo estará disponible la opción **Editor avanzado** en la pestaña **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="bce79-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="bce79-148">Uso del tipo de valor devuelto por la función para devolver un resultado único</span><span class="sxs-lookup"><span data-stu-id="bce79-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="bce79-149">En el ejemplo anterior, se muestra cómo utilizar el valor devuelto por la función para proporcionar la salida a un enlace, lo cual se consigue mediante el parámetro de nombre especial `$return`.</span><span class="sxs-lookup"><span data-stu-id="bce79-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="bce79-150">(Esto solo se admite en los lenguajes que presenten un valor devuelto, como C#, JavaScript y F#). Si una función tiene varios enlaces de salida, emplee `$return` para únicamente uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="bce79-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="bce79-151">En los ejemplos siguientes, puede ver cómo se usan los tipos de valores devueltos con los enlaces de salida en C#, JavaScript y F#.</span><span class="sxs-lookup"><span data-stu-id="bce79-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in the second parameter to context.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="bce79-152">Enlace de la propiedad DataType</span><span class="sxs-lookup"><span data-stu-id="bce79-152">Binding dataType property</span></span>

<span data-ttu-id="bce79-153">En .NET, use los tipos para definir el tipo de datos de los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="bce79-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="bce79-154">Por ejemplo, use `string` para enlazar al texto de un desencadenador de cola y una matriz de bytes que se lee como binaria.</span><span class="sxs-lookup"><span data-stu-id="bce79-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="bce79-155">Para los idiomas que se escriben dinámicamente, como JavaScript, use la propiedad `dataType` en la definición de enlace.</span><span class="sxs-lookup"><span data-stu-id="bce79-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="bce79-156">Por ejemplo, para leer el contenido de una solicitud HTTP en formato binario, use el tipo `binary`:</span><span class="sxs-lookup"><span data-stu-id="bce79-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="bce79-157">Otras opciones para `dataType` son `stream` y `string`.</span><span class="sxs-lookup"><span data-stu-id="bce79-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="bce79-158">Resolver la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bce79-158">Resolving app settings</span></span>
<span data-ttu-id="bce79-159">Como procedimiento recomendado, los secretos y las cadenas de conexión deberían administrarse mediante los ajustes de la aplicación, en lugar de archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="bce79-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="bce79-160">De este modo, se limita el acceso a estos secretos y resulta seguro almacenar *function.json* en un repositorio de control de código fuente público.</span><span class="sxs-lookup"><span data-stu-id="bce79-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="bce79-161">Los ajustes de la aplicación también son útiles cuando se desea cambiar la configuración en función del entorno.</span><span class="sxs-lookup"><span data-stu-id="bce79-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="bce79-162">Por ejemplo, en un entorno de prueba, es posible que quiera supervisar una cola o un contenedor de almacenamiento de blobs diferente.</span><span class="sxs-lookup"><span data-stu-id="bce79-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="bce79-163">Los ajustes de la aplicación se resuelven cuando un valor aparece entre símbolos de porcentaje; por ejemplo `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="bce79-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="bce79-164">Tenga en cuenta que la propiedad `connection` de los desencadenadores y los enlaces es un caso especial y resuelve automáticamente los valores como ajustes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bce79-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="bce79-165">En el ejemplo siguiente, aparece un desencadenador de colas que se sirve del valor de configuración de la aplicación `%input-queue-name%` para definir la cola que se desencadenará.</span><span class="sxs-lookup"><span data-stu-id="bce79-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="bce79-166">Propiedades de metadatos de los desencadenadores</span><span class="sxs-lookup"><span data-stu-id="bce79-166">Trigger metadata properties</span></span>

<span data-ttu-id="bce79-167">Además de la carga de datos que proporciona un desencadenador (como el mensaje de la cola que desencadenó una función), muchos desencadenadores facilitan valores de metadatos adicionales.</span><span class="sxs-lookup"><span data-stu-id="bce79-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="bce79-168">Estos valores pueden usarse como parámetros de entrada en C# y F# o como propiedades en el objeto `context.bindings` de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bce79-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="bce79-169">Por ejemplo, los desencadenadores de colas admiten las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="bce79-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="bce79-170">QueueTrigger (desencadena el contenido del mensaje si hay una cadena válida)</span><span class="sxs-lookup"><span data-stu-id="bce79-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="bce79-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="bce79-171">DequeueCount</span></span>
* <span data-ttu-id="bce79-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="bce79-172">ExpirationTime</span></span>
* <span data-ttu-id="bce79-173">Id</span><span class="sxs-lookup"><span data-stu-id="bce79-173">Id</span></span>
* <span data-ttu-id="bce79-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="bce79-174">InsertionTime</span></span>
* <span data-ttu-id="bce79-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="bce79-175">NextVisibleTime</span></span>
* <span data-ttu-id="bce79-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="bce79-176">PopReceipt</span></span>

<span data-ttu-id="bce79-177">Los detalles sobre las propiedades de metadatos de cada desencadenador se describen en el tema de referencia correspondiente.</span><span class="sxs-lookup"><span data-stu-id="bce79-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="bce79-178">También podrá encontrar documentación en la pestaña **Integrar** del portal, en la sección **Documentación**, debajo del área de configuración de enlaces.</span><span class="sxs-lookup"><span data-stu-id="bce79-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="bce79-179">Por ejemplo, debido a que los desencadenadores de blobs tienen algunos retrasos, puede utilizar un desencadenador de colas para ejecutar la función (consulte el artículo relativo al [desencadenador de Blob Storage](functions-bindings-storage-blob.md#storage-blob-trigger)).</span><span class="sxs-lookup"><span data-stu-id="bce79-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="bce79-180">El mensaje de la cola contendría el nombre de archivo del blob que se desencadenará.</span><span class="sxs-lookup"><span data-stu-id="bce79-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="bce79-181">Mediante la propiedad de metadatos `queueTrigger`, puede especificar este comportamiento en la configuración, en lugar del código.</span><span class="sxs-lookup"><span data-stu-id="bce79-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="bce79-182">Las propiedades de metadatos de los desencadenadores también se pueden usar en una *expresión de enlace* para otro enlace, tal y como se describe en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="bce79-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="bce79-183">Patrones y expresiones de enlace</span><span class="sxs-lookup"><span data-stu-id="bce79-183">Binding expressions and patterns</span></span>

<span data-ttu-id="bce79-184">Una de las características más eficaces de los desencadenadores y los enlaces son las *expresiones de enlace*.</span><span class="sxs-lookup"><span data-stu-id="bce79-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="bce79-185">En el enlace, puede definir expresiones de patrón que, después, podrán emplearse en otros enlaces o en el código.</span><span class="sxs-lookup"><span data-stu-id="bce79-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="bce79-186">Asimismo, los metadatos de los desencadenadores pueden utilizarse en expresiones de enlace, tal y como aparece en la muestra de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="bce79-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="bce79-187">Por ejemplo, imagine que desea cambiar el tamaño de unas imágenes en un contenedor de almacenamiento de blobs concreto, similar a la plantilla **Image Resizer** (Cambio de tamaño de imágenes) de la página **Nueva función**.</span><span class="sxs-lookup"><span data-stu-id="bce79-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="bce79-188">Vaya a **Nueva función** -> lenguaje **C#** -> escenario **Samples** (Muestras) -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="bce79-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="bce79-189">Esta es la definición de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="bce79-189">Here is the *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="bce79-190">Observe que el parámetro `filename` se usa tanto en la definición del desencadenador de blobs como en el enlace de salida de blobs.</span><span class="sxs-lookup"><span data-stu-id="bce79-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="bce79-191">Este parámetro también puede incluirse en el código de la función.</span><span class="sxs-lookup"><span data-stu-id="bce79-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="bce79-192">GUID aleatorios</span><span class="sxs-lookup"><span data-stu-id="bce79-192">Random GUIDs</span></span>
<span data-ttu-id="bce79-193">Azure Functions facilita una práctica sintaxis para generar GUID en los enlaces por medio de la expresión de enlace `{rand-guid}`.</span><span class="sxs-lookup"><span data-stu-id="bce79-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="bce79-194">En el ejemplo siguiente, se usa dicha expresión para crear un nombre de blob único:</span><span class="sxs-lookup"><span data-stu-id="bce79-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="bce79-195">Hora actual</span><span class="sxs-lookup"><span data-stu-id="bce79-195">Current time</span></span>

<span data-ttu-id="bce79-196">Puede usar la expresión de enlace `DateTime`, que se resuelve en `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="bce79-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="bce79-197">Enlace a propiedades de entrada personalizadas en una expresión de enlace</span><span class="sxs-lookup"><span data-stu-id="bce79-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="bce79-198">Las expresiones de enlace también pueden hacer referencia a propiedades definidas en la propia carga de los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="bce79-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="bce79-199">Por ejemplo, es posible que quiera establecer un enlace de forma dinámica a un archivo de almacenamiento de blobs a partir de un nombre de archivo proporcionado en un webhook.</span><span class="sxs-lookup"><span data-stu-id="bce79-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="bce79-200">Por ejemplo, la función *function.json* siguiente recurre a una propiedad denominada `BlobName` en la carga del desencadenador:</span><span class="sxs-lookup"><span data-stu-id="bce79-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="bce79-201">Para realizar esto en C# y F#, debe definir un POCO que establezca los campos que se deserializarán en la carga del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="bce79-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="bce79-202">En JavaScript, la deserialización de JSON se lleva a cabo de manera automática y el usuario puede usar directamente las propiedades.</span><span class="sxs-lookup"><span data-stu-id="bce79-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="bce79-203">Configuración de datos de enlace en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="bce79-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="bce79-204">En C# y otros lenguajes .NET, puede usar un patrón de enlace imperativo, en contraposición a los enlaces declarativos de *function.json*.</span><span class="sxs-lookup"><span data-stu-id="bce79-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="bce79-205">Los enlaces imperativos resultan útiles cuando los parámetros de enlace tienen que calcularse en tiempo de ejecución, en lugar de en el tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="bce79-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="bce79-206">Para obtener más información, vea [Enlace en tiempo de ejecución a través de enlaces imperativos](functions-reference-csharp.md#imperative-bindings) en la Referencia para desarrolladores de C#.</span><span class="sxs-lookup"><span data-stu-id="bce79-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bce79-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bce79-207">Next steps</span></span>
<span data-ttu-id="bce79-208">Para obtener más información sobre un tipo de enlace concreto, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="bce79-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="bce79-209">HTTP y webhooks</span><span class="sxs-lookup"><span data-stu-id="bce79-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="bce79-210">Temporizador</span><span class="sxs-lookup"><span data-stu-id="bce79-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="bce79-211">Queue storage</span><span class="sxs-lookup"><span data-stu-id="bce79-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="bce79-212">Blob storage</span><span class="sxs-lookup"><span data-stu-id="bce79-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="bce79-213">Almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="bce79-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="bce79-214">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bce79-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="bce79-215">Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="bce79-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="bce79-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bce79-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="bce79-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="bce79-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="bce79-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="bce79-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="bce79-219">Centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="bce79-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="bce79-220">Aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="bce79-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="bce79-221">Archivo externo</span><span class="sxs-lookup"><span data-stu-id="bce79-221">External file</span></span>](functions-bindings-external-file.md)
