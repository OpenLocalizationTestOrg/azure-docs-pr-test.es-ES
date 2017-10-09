---
title: aaaWork con desencadenadores y los enlaces de funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse desencadenadores y los enlaces de funciones de Azure tooconnect los eventos de tooonline de ejecución de código y servicios en la nube."
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
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="3dedc-104">Conceptos básicos sobre los enlaces y desencadenadores de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3dedc-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="3dedc-105">Las funciones de Azure permite toowrite código de respuesta tooevents en Azure y otros servicios a través de *desencadenadores* y *enlaces*.</span><span class="sxs-lookup"><span data-stu-id="3dedc-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="3dedc-106">En este artículo, se ofrece una introducción conceptual a los desencadenadores y enlaces de todos los lenguajes de programación compatibles.</span><span class="sxs-lookup"><span data-stu-id="3dedc-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="3dedc-107">Características que son comunes enlaces tooall se describen aquí.</span><span class="sxs-lookup"><span data-stu-id="3dedc-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="3dedc-108">Información general</span><span class="sxs-lookup"><span data-stu-id="3dedc-108">Overview</span></span>

<span data-ttu-id="3dedc-109">Desencadenadores y los enlaces son un toodefine de manera declarativa cómo se invoca una función y los datos que funciona con.</span><span class="sxs-lookup"><span data-stu-id="3dedc-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="3dedc-110">Los *desencadenadores* establecen el modo de invocar una función.</span><span class="sxs-lookup"><span data-stu-id="3dedc-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="3dedc-111">Cada función debe tener exactamente un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="3dedc-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="3dedc-112">Los desencadenadores tienen asociados datos, que suele ser carga Hola que desencadenó la función hello.</span><span class="sxs-lookup"><span data-stu-id="3dedc-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="3dedc-113">Entrada y salida *enlaces* proporcionan un toodata de tooconnect de manera declarativa desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="3dedc-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="3dedc-114">Tootriggers similar, puede especificar las cadenas de conexión y otras propiedades en la configuración de la función.</span><span class="sxs-lookup"><span data-stu-id="3dedc-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="3dedc-115">Los enlaces son opcionales y cada función puede tener varios enlaces de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="3dedc-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="3dedc-116">Mediante enlaces y desencadenadores, puede escribir código que es más genérico y no codificar los detalles de hello de servicios de hello con la que interactúa.</span><span class="sxs-lookup"><span data-stu-id="3dedc-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="3dedc-117">Los datos procedentes de los servicios se convierten simplemente en valores de entrada para el código de función.</span><span class="sxs-lookup"><span data-stu-id="3dedc-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="3dedc-118">servicio de tooanother de datos toooutput (por ejemplo, para crear una nueva fila en el almacenamiento de tabla de Azure), utilice valor devuelto de hello del método hello.</span><span class="sxs-lookup"><span data-stu-id="3dedc-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="3dedc-119">O bien, si necesita toooutput varios valores, use un objeto auxiliar.</span><span class="sxs-lookup"><span data-stu-id="3dedc-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="3dedc-120">Desencadenadores y los enlaces tienen un **nombre** propiedad, que es un identificador que se utiliza en el enlace de Hola de tooaccess de código.</span><span class="sxs-lookup"><span data-stu-id="3dedc-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="3dedc-121">Puede configurar los desencadenadores y los enlaces de hello **integrar** ficha en el portal de Azure funciones hello.</span><span class="sxs-lookup"><span data-stu-id="3dedc-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="3dedc-122">Tras bastidores de hello, Hola interfaz de usuario modifica un archivo denominado *function.json* archivo en el directorio de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="3dedc-123">Este archivo se puede modificar cambiando toohello **editor avanzado**.</span><span class="sxs-lookup"><span data-stu-id="3dedc-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="3dedc-124">Hello tabla siguiente muestran los desencadenadores de Hola y enlaces que son compatibles con las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dedc-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="3dedc-125">Ejemplo: desencadenador de colas y enlace de salida de tablas</span><span class="sxs-lookup"><span data-stu-id="3dedc-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="3dedc-126">Imagine que desea toowrite una tooAzure fila nueva tabla de almacenamiento cada vez que un mensaje nuevo aparece en el almacenamiento de la cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dedc-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="3dedc-127">Este escenario puede implementarse mediante un desencadenador de colas de Azure y un enlace de salida de tablas.</span><span class="sxs-lookup"><span data-stu-id="3dedc-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="3dedc-128">Un desencadenador de cola requiere Hola siguiendo la información de hello **integrar** ficha:</span><span class="sxs-lookup"><span data-stu-id="3dedc-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="3dedc-129">nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de cuenta de almacenamiento de Hola para cola de Hola</span><span class="sxs-lookup"><span data-stu-id="3dedc-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="3dedc-130">nombre de la cola de Hola</span><span class="sxs-lookup"><span data-stu-id="3dedc-130">hello queue name</span></span>
* <span data-ttu-id="3dedc-131">Hola identificador en el contenido del código tooread Hola Hola del mensaje de cola, como `order`.</span><span class="sxs-lookup"><span data-stu-id="3dedc-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="3dedc-132">toowrite tooAzure almacenamiento de tabla, utilice un enlace de salida con hello detalles siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dedc-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="3dedc-133">nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de cuenta de almacenamiento de hello para la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="3dedc-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="3dedc-134">nombre de la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="3dedc-134">hello table name</span></span>
* <span data-ttu-id="3dedc-135">identificador Hello en su toocreate de código de salida elementos u Hola de valor devuelto de función hello.</span><span class="sxs-lookup"><span data-stu-id="3dedc-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="3dedc-136">Enlaces de usan la configuración de aplicación para Hola de tooenforce de cadenas de conexión mejor práctica que *function.json* no contiene secretos de servicio.</span><span class="sxs-lookup"><span data-stu-id="3dedc-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="3dedc-137">A continuación, usar identificadores de hello proporcionados toointegrate con el almacenamiento de Azure en el código.</span><span class="sxs-lookup"><span data-stu-id="3dedc-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
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

<span data-ttu-id="3dedc-138">Aquí es hello *function.json* que corresponde toohello anterior el código.</span><span class="sxs-lookup"><span data-stu-id="3dedc-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="3dedc-139">Tenga en cuenta que Hola misma configuración puede utilizarse, independientemente del lenguaje de Hola de implementación de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="3dedc-140">tooview y editar contenido de Hola de *function.json* en hello portal de Azure, haga clic en hello **editor avanzado** opción en hello **integrar** pestaña de la función.</span><span class="sxs-lookup"><span data-stu-id="3dedc-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="3dedc-141">Para obtener más ejemplos de código e información sobre la integración con Azure Storage, consulte el artículo sobre [desencadenadores y enlaces de Azure Functions para Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3dedc-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="3dedc-142">Dirección de los enlaces</span><span class="sxs-lookup"><span data-stu-id="3dedc-142">Binding direction</span></span>

<span data-ttu-id="3dedc-143">Todos los desencadenadores y enlaces tienen la propiedad `direction`:</span><span class="sxs-lookup"><span data-stu-id="3dedc-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="3dedc-144">Para los desencadenadores, dirección de hello es siempre`in`</span><span class="sxs-lookup"><span data-stu-id="3dedc-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="3dedc-145">Los enlaces de entrada y de salida usan `in` y `out`</span><span class="sxs-lookup"><span data-stu-id="3dedc-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="3dedc-146">Algunos enlaces admiten la dirección especial `inout`.</span><span class="sxs-lookup"><span data-stu-id="3dedc-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="3dedc-147">Si usa `inout`, solo Hola **editor avanzado** está disponible en hello **integrar** ficha.</span><span class="sxs-lookup"><span data-stu-id="3dedc-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="3dedc-148">Uso de tooreturn de tipo de valor devuelto de función hello una salida única</span><span class="sxs-lookup"><span data-stu-id="3dedc-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="3dedc-149">Hello en el ejemplo anterior se muestra cómo tooprovide de valor devuelto de función de hello toouse salida tooa enlace, que se consigue mediante el parámetro de nombre especial de hello `$return`.</span><span class="sxs-lookup"><span data-stu-id="3dedc-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="3dedc-150">(Esto solo se admite en los lenguajes que presenten un valor devuelto, como C#, JavaScript y F#). Si una función tiene varios enlaces de salida, use `$return` para una sola Hola de enlaces de salida.</span><span class="sxs-lookup"><span data-stu-id="3dedc-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="3dedc-151">ejemplos de Hello siguientes se muestra cómo devolución tipos se utilizan con enlaces de salida en C#, JavaScript y F #.</span><span class="sxs-lookup"><span data-stu-id="3dedc-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in hello second parameter toocontext.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="3dedc-152">Enlace de la propiedad DataType</span><span class="sxs-lookup"><span data-stu-id="3dedc-152">Binding dataType property</span></span>

<span data-ttu-id="3dedc-153">En. NET, utilice tipos Hola Hola tipos toodefine para datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="3dedc-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="3dedc-154">Por ejemplo, usar `string` toobind toohello texto de un desencadenador de cola y una tooread de matriz de bytes como binario.</span><span class="sxs-lookup"><span data-stu-id="3dedc-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="3dedc-155">Para los idiomas que se escriben dinámicamente, como JavaScript, usar hello `dataType` propiedad en la definición de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="3dedc-156">Por ejemplo, tooread Hola contenido de una solicitud HTTP en formato binario, usar tipo hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="3dedc-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="3dedc-157">Otras opciones para `dataType` son `stream` y `string`.</span><span class="sxs-lookup"><span data-stu-id="3dedc-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="3dedc-158">Resolver la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3dedc-158">Resolving app settings</span></span>
<span data-ttu-id="3dedc-159">Como procedimiento recomendado, los secretos y las cadenas de conexión deberían administrarse mediante los ajustes de la aplicación, en lugar de archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="3dedc-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="3dedc-160">Esto limita el acceso toothese secretos y resulta seguro toostore *function.json* en un repositorio de control de código fuente pública.</span><span class="sxs-lookup"><span data-stu-id="3dedc-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="3dedc-161">Configuración de la aplicación también es útil cuando lo desee configuración toochange según el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="3dedc-162">Por ejemplo, en un entorno de prueba, puede que desee toomonitor otro contenedor de almacenamiento cola o un blob.</span><span class="sxs-lookup"><span data-stu-id="3dedc-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="3dedc-163">Los ajustes de la aplicación se resuelven cuando un valor aparece entre símbolos de porcentaje; por ejemplo `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="3dedc-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="3dedc-164">Tenga en cuenta que hello `connection` propiedad de desencadenadores y enlaces es un caso especial y soluciona automáticamente los valores de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dedc-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="3dedc-165">el ejemplo siguiente se Hello es un desencadenador de cola que usa una configuración de aplicación `%input-queue-name%` toodefine Hola cola tootrigger en.</span><span class="sxs-lookup"><span data-stu-id="3dedc-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="3dedc-166">Propiedades de metadatos de los desencadenadores</span><span class="sxs-lookup"><span data-stu-id="3dedc-166">Trigger metadata properties</span></span>

<span data-ttu-id="3dedc-167">En la carga de datos de adición toohello proporcionada por un desencadenador (por ejemplo, el mensaje de cola de Hola que desencadenó una función), desencadenadores muchos proporcionan valores de metadatos adicionales.</span><span class="sxs-lookup"><span data-stu-id="3dedc-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="3dedc-168">Estos valores se pueden usar como parámetros de entrada en C# y F # o propiedades en hello `context.bindings` objetos en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3dedc-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="3dedc-169">Por ejemplo, un desencadenador de cola admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dedc-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="3dedc-170">QueueTrigger (desencadena el contenido del mensaje si hay una cadena válida)</span><span class="sxs-lookup"><span data-stu-id="3dedc-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="3dedc-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="3dedc-171">DequeueCount</span></span>
* <span data-ttu-id="3dedc-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="3dedc-172">ExpirationTime</span></span>
* <span data-ttu-id="3dedc-173">Id</span><span class="sxs-lookup"><span data-stu-id="3dedc-173">Id</span></span>
* <span data-ttu-id="3dedc-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="3dedc-174">InsertionTime</span></span>
* <span data-ttu-id="3dedc-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="3dedc-175">NextVisibleTime</span></span>
* <span data-ttu-id="3dedc-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="3dedc-176">PopReceipt</span></span>

<span data-ttu-id="3dedc-177">Detalles de propiedades de metadatos para cada desencadenador se describen en el tema de referencia correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="3dedc-178">Documentación también está disponible en hello **integrar** ficha del portal Hola Hola **documentación** sección por debajo del área de configuración de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="3dedc-179">Por ejemplo, dado que los desencadenadores de blob tienen algunos retrasos, puede usar un toorun de desencadenador de cola la función (vea [desencadenador de almacenamiento Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="3dedc-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="3dedc-180">mensaje de la cola de Hello contendría tootrigger de nombre de archivo de blob de hello en.</span><span class="sxs-lookup"><span data-stu-id="3dedc-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="3dedc-181">Con hello `queueTrigger` propiedad de metadatos, este comportamiento se puede especificar en la configuración, en lugar de su código.</span><span class="sxs-lookup"><span data-stu-id="3dedc-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="3dedc-182">Propiedades de metadatos de un desencadenador también se pueden usar en un *expresión de enlace* para otro enlace, como se describe en hello pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="3dedc-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="3dedc-183">Patrones y expresiones de enlace</span><span class="sxs-lookup"><span data-stu-id="3dedc-183">Binding expressions and patterns</span></span>

<span data-ttu-id="3dedc-184">Una de las características más eficaces de Hola de desencadenadores y enlaces es *expresiones de enlace*.</span><span class="sxs-lookup"><span data-stu-id="3dedc-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="3dedc-185">En el enlace, puede definir expresiones de patrón que, después, podrán emplearse en otros enlaces o en el código.</span><span class="sxs-lookup"><span data-stu-id="3dedc-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="3dedc-186">Metadatos de desencadenador también pueden utilizarse para enlazar las expresiones, como se muestra en el ejemplo de Hola Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="3dedc-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="3dedc-187">Por ejemplo, imagine que desea tooresize imágenes de contenedor de almacenamiento de blob determinado, toohello similar **tamaño de imagen** plantilla Hola **nueva función** página.</span><span class="sxs-lookup"><span data-stu-id="3dedc-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="3dedc-188">Vaya demasiado**nueva función** -> lenguaje **C#** -> escenario **ejemplos** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="3dedc-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="3dedc-189">Aquí es hello *function.json* definición:</span><span class="sxs-lookup"><span data-stu-id="3dedc-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="3dedc-190">Tenga en cuenta que hello `filename` parámetro se utiliza en la definición del desencadenador Hola blob así como blob de hello el enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="3dedc-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="3dedc-191">Este parámetro también puede incluirse en el código de la función.</span><span class="sxs-lookup"><span data-stu-id="3dedc-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="3dedc-192">GUID aleatorios</span><span class="sxs-lookup"><span data-stu-id="3dedc-192">Random GUIDs</span></span>
<span data-ttu-id="3dedc-193">Las funciones de Azure proporciona una sintaxis de conveniencia para generar GUID en sus enlaces a través de hello `{rand-guid}` expresión de enlace.</span><span class="sxs-lookup"><span data-stu-id="3dedc-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="3dedc-194">Hello en el ejemplo siguiente se utiliza este toogenerate un nombre de blob único:</span><span class="sxs-lookup"><span data-stu-id="3dedc-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="3dedc-195">Hora actual</span><span class="sxs-lookup"><span data-stu-id="3dedc-195">Current time</span></span>

<span data-ttu-id="3dedc-196">Puede utilizar la expresión de enlace de hello `DateTime`, que se resuelve demasiado`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="3dedc-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="3dedc-197">Enlazar las propiedades de entrada toocustom en una expresión de enlace</span><span class="sxs-lookup"><span data-stu-id="3dedc-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="3dedc-198">Expresiones de enlace pueden hacer referencia a propiedades que se definen en la carga de desencadenador de hello propio.</span><span class="sxs-lookup"><span data-stu-id="3dedc-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="3dedc-199">Por ejemplo, puede que desee toodynamically enlace tooa: archivo de almacenamiento blob de un nombre de archivo proporcionado en un webhook.</span><span class="sxs-lookup"><span data-stu-id="3dedc-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="3dedc-200">Por ejemplo, Hola después *function.json* utiliza una propiedad denominada `BlobName` de carga de desencadenador de hello:</span><span class="sxs-lookup"><span data-stu-id="3dedc-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="3dedc-201">tooaccomplish este en C# y F #, debe definir un POCO que define los campos de Hola que se va a deserializar carga de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dedc-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="3dedc-202">En JavaScript, automáticamente se realiza la deserialización de JSON y puede usar las propiedades de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="3dedc-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="3dedc-203">Configuración de datos de enlace en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="3dedc-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="3dedc-204">En C# y otros lenguajes. NET, puede utilizar un patrón de enlace imperativo, como opuestos toohello enlaces declarativos en *function.json*.</span><span class="sxs-lookup"><span data-stu-id="3dedc-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="3dedc-205">Enlace imperativa es útil cuando los parámetros de enlace necesitan toobe calcula en tiempo de ejecución en lugar de diseño.</span><span class="sxs-lookup"><span data-stu-id="3dedc-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="3dedc-206">más información, consulte toolearn [enlace en tiempo de ejecución a través de enlaces imperativos](functions-reference-csharp.md#imperative-bindings) en referencia del programador de hello C#.</span><span class="sxs-lookup"><span data-stu-id="3dedc-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dedc-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3dedc-207">Next steps</span></span>
<span data-ttu-id="3dedc-208">Para obtener más información sobre un enlace específico, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="3dedc-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="3dedc-209">HTTP y webhooks</span><span class="sxs-lookup"><span data-stu-id="3dedc-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="3dedc-210">Temporizador</span><span class="sxs-lookup"><span data-stu-id="3dedc-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="3dedc-211">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="3dedc-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="3dedc-212">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="3dedc-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="3dedc-213">Table storage</span><span class="sxs-lookup"><span data-stu-id="3dedc-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="3dedc-214">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3dedc-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="3dedc-215">Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="3dedc-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="3dedc-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3dedc-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="3dedc-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="3dedc-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="3dedc-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="3dedc-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="3dedc-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="3dedc-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="3dedc-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="3dedc-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="3dedc-221">Archivo externo</span><span class="sxs-lookup"><span data-stu-id="3dedc-221">External file</span></span>](functions-bindings-external-file.md)
