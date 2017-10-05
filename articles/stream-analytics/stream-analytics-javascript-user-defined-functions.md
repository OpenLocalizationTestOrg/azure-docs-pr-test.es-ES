---
title: Funciones definidas por el usuario en JavaScript para Azure Stream Analytics | Microsoft Docs
description: "Realizar mecánica de consultas avanzadas con funciones definidas por el usuario en JavaScript"
keywords: javascript, funciones definidas por el usuario, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="1e1f4-104">Funciones definidas por el usuario en JavaScript para Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="1e1f4-105">Azure Stream Analytics admite funciones definidas por el usuario escritas en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="1e1f4-106">Con el conjunto completo de métodos **String**, **RegExp**, **Math**, **Array** y **Date** que proporciona JavaScript, las transformaciones de datos complejas con trabajos de Stream Analytics son más fáciles de crear.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="1e1f4-107">Funciones definidas por el usuario en JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e1f4-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="1e1f4-108">Las funciones definidas por el usuario en JavaScript admiten funciones escalares de solo cálculo y sin estado, que no requieren conectividad externa.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="1e1f4-109">El valor devuelto de una función solo puede ser un valor escalar (único).</span><span class="sxs-lookup"><span data-stu-id="1e1f4-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="1e1f4-110">Después de agregar una función definida por el usuario en JavaScript a un trabajo, puede usar la función en cualquier parte de la consulta, como una función escalar integrada.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="1e1f4-111">Estos son algunos escenarios en los que le podrían resultar útiles las funciones definidas por el usuario en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="1e1f4-112">Análisis y manipulación de cadenas que incluyen funciones de expresiones regulares, por ejemplo, **Regexp_Replace()** y **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="1e1f4-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="1e1f4-113">Descodificación y codificación de datos, por ejemplo, conversión de binario a hexadecimal</span><span class="sxs-lookup"><span data-stu-id="1e1f4-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="1e1f4-114">Realización de cálculos matemáticos con funciones **matemáticas** de JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e1f4-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="1e1f4-115">Realización de operaciones de matriz como ordenar, combinar, buscar y rellenar</span><span class="sxs-lookup"><span data-stu-id="1e1f4-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="1e1f4-116">Aquí se indican algunas operaciones que no se pueden realizar con una función definida por el usuario de JavaScript en Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="1e1f4-117">Llamar a puntos de conexión de REST externos, por ejemplo, mediante la realización de una búsqueda inversa de direcciones IP o una extracción de datos de referencia de un origen externo</span><span class="sxs-lookup"><span data-stu-id="1e1f4-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="1e1f4-118">Realizar la serialización o deserialización de formatos de eventos personalizados en entradas y salidas</span><span class="sxs-lookup"><span data-stu-id="1e1f4-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="1e1f4-119">Crear agregados personalizados</span><span class="sxs-lookup"><span data-stu-id="1e1f4-119">Create custom aggregates</span></span>

<span data-ttu-id="1e1f4-120">Aunque haya funciones como **Date.GetDate()** o **Math.random()** que no están bloqueadas en la definición de funciones, debe evitar su uso.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="1e1f4-121">Estas funciones **no** devuelven el mismo resultado cada vez que las llama y el servicio Azure Stream Analytics no mantiene un diario de las llamadas a funciones y los resultados devueltos.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="1e1f4-122">Si una función devuelve resultados diferentes en los mismos eventos, la repetibilidad no se garantizará cuando el usuario o el servicio Stream Analytics reinicie un trabajo.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="1e1f4-123">Incorporación de una función definida por el usuario de JavaScript en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1e1f4-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="1e1f4-124">Para crear una función definida por el usuario de JavaScript en un trabajo de Stream Analytics existente, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="1e1f4-125">En Azure Portal, busque el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="1e1f4-126">En **TOPOLOGÍA DE TRABAJO**, seleccione la función.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="1e1f4-127">Aparece una lista vacía de funciones.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="1e1f4-128">Para crear una nueva función definida por el usuario, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="1e1f4-129">En la hoja **Nueva función**, en **Tipo de función**, seleccione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="1e1f4-130">Aparecerá una plantilla de función predeterminada en el editor.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="1e1f4-131">Como **alias de la función definida por el usuario** escriba **hex2Int** y cambie la implementación de la función como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="1e1f4-132">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-132">Select **Save**.</span></span> <span data-ttu-id="1e1f4-133">La función aparece en la lista de funciones.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="1e1f4-134">Seleccione la nueva función **hex2Int** y compruebe la definición de función.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="1e1f4-135">Todas las funciones tienen un prefijo **UDF** agregado al alias de la función.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="1e1f4-136">Debe *incluir el prefijo* cuando llama a la función en la consulta de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="1e1f4-137">En este caso, debe llamar a **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="1e1f4-138">Llamada a una función definida por el usuario de JavaScript en una consulta</span><span class="sxs-lookup"><span data-stu-id="1e1f4-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="1e1f4-139">En el editor de consultas, en **TOPOLOGÍA DE CONSULTA**, seleccione **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="1e1f4-140">Edite la consulta y, a continuación, llame a la función definida por el usuario, de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="1e1f4-141">Haga clic con el botón derecho en la entrada del trabajo para cargar el archivo de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="1e1f4-142">Para probar la consulta, seleccione **Probar**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="1e1f4-143">Objetos de JavaScript compatibles</span><span class="sxs-lookup"><span data-stu-id="1e1f4-143">Supported JavaScript objects</span></span>
<span data-ttu-id="1e1f4-144">Las funciones definidas por el usuario en JavaScript para Azure Stream Analytics admiten objetos de JavaScript estándar e integrados.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="1e1f4-145">Para obtener una lista de estos objetos, consulte [Objetos globales](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="1e1f4-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="1e1f4-146">Conversión de tipos de Stream Analytics y JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e1f4-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="1e1f4-147">Hay diferencias entre los tipos admitidos en el lenguaje de consultas de Stream Analytics y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="1e1f4-148">En esta tabla se muestran las asignaciones de conversión entre los dos:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="1e1f4-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-149">Stream Analytics</span></span> | <span data-ttu-id="1e1f4-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e1f4-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="1e1f4-151">bigint</span><span class="sxs-lookup"><span data-stu-id="1e1f4-151">bigint</span></span> | <span data-ttu-id="1e1f4-152">Number (JavaScript solamente puede representar enteros hasta 2^53 con precisión)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="1e1f4-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="1e1f4-153">DateTime</span></span> | <span data-ttu-id="1e1f4-154">Date (JavaScript solo admite milisegundos)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="1e1f4-155">double</span><span class="sxs-lookup"><span data-stu-id="1e1f4-155">double</span></span> | <span data-ttu-id="1e1f4-156">Number</span><span class="sxs-lookup"><span data-stu-id="1e1f4-156">Number</span></span>
<span data-ttu-id="1e1f4-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-157">nvarchar(MAX)</span></span> | <span data-ttu-id="1e1f4-158">String</span><span class="sxs-lookup"><span data-stu-id="1e1f4-158">String</span></span>
<span data-ttu-id="1e1f4-159">Registro</span><span class="sxs-lookup"><span data-stu-id="1e1f4-159">Record</span></span> | <span data-ttu-id="1e1f4-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="1e1f4-160">Object</span></span>
<span data-ttu-id="1e1f4-161">Matriz</span><span class="sxs-lookup"><span data-stu-id="1e1f4-161">Array</span></span> | <span data-ttu-id="1e1f4-162">Matriz</span><span class="sxs-lookup"><span data-stu-id="1e1f4-162">Array</span></span>
<span data-ttu-id="1e1f4-163">NULL</span><span class="sxs-lookup"><span data-stu-id="1e1f4-163">NULL</span></span> | <span data-ttu-id="1e1f4-164">Null</span><span class="sxs-lookup"><span data-stu-id="1e1f4-164">Null</span></span>


<span data-ttu-id="1e1f4-165">Estas son las conversiones de JavaScript a Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="1e1f4-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="1e1f4-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e1f4-166">JavaScript</span></span> | <span data-ttu-id="1e1f4-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="1e1f4-168">Number</span><span class="sxs-lookup"><span data-stu-id="1e1f4-168">Number</span></span> | <span data-ttu-id="1e1f4-169">Bigint (si el número es round y entre long.MinValue y long.MaxValue, double en caso contrario)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="1e1f4-170">Date</span><span class="sxs-lookup"><span data-stu-id="1e1f4-170">Date</span></span> | <span data-ttu-id="1e1f4-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="1e1f4-171">DateTime</span></span>
<span data-ttu-id="1e1f4-172">String</span><span class="sxs-lookup"><span data-stu-id="1e1f4-172">String</span></span> | <span data-ttu-id="1e1f4-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-173">nvarchar(MAX)</span></span>
<span data-ttu-id="1e1f4-174">Objeto</span><span class="sxs-lookup"><span data-stu-id="1e1f4-174">Object</span></span> | <span data-ttu-id="1e1f4-175">Registro</span><span class="sxs-lookup"><span data-stu-id="1e1f4-175">Record</span></span>
<span data-ttu-id="1e1f4-176">Matriz</span><span class="sxs-lookup"><span data-stu-id="1e1f4-176">Array</span></span> | <span data-ttu-id="1e1f4-177">Matriz</span><span class="sxs-lookup"><span data-stu-id="1e1f4-177">Array</span></span>
<span data-ttu-id="1e1f4-178">Null, sin definir</span><span class="sxs-lookup"><span data-stu-id="1e1f4-178">Null, Undefined</span></span> | <span data-ttu-id="1e1f4-179">NULL</span><span class="sxs-lookup"><span data-stu-id="1e1f4-179">NULL</span></span>
<span data-ttu-id="1e1f4-180">Cualquier otro tipo (por ejemplo, una función o un error)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="1e1f4-181">No admitido (da lugar a un error en tiempo de ejecución)</span><span class="sxs-lookup"><span data-stu-id="1e1f4-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1e1f4-182">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="1e1f4-182">Troubleshooting</span></span>
<span data-ttu-id="1e1f4-183">Los errores en tiempo de ejecución de JavaScript se consideran graves y se presentan en el registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="1e1f4-184">Para recuperar el registro, en Azure Portal, vaya al trabajo y seleccione **Registro de actividad**.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="1e1f4-185">Otros patrones de función definida por el usuario de JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e1f4-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="1e1f4-186">Escritura de JSON anidado en la salida</span><span class="sxs-lookup"><span data-stu-id="1e1f4-186">Write nested JSON to output</span></span>
<span data-ttu-id="1e1f4-187">Si tiene un paso de procesamiento de seguimiento que usa la salida del trabajo de Stream Analytics como entrada y requiere un formato JSON, puede escribir una cadena JSON en la salida.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="1e1f4-188">El ejemplo siguiente llama a la función **JSON.stringify()** para empaquetar todos los pares nombre-valor de la entrada y escribirlos como un único valor de cadena en la salida.</span><span class="sxs-lookup"><span data-stu-id="1e1f4-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="1e1f4-189">**Definición de funciones definidas por el usuario en JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="1e1f4-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="1e1f4-190">**Consulta de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="1e1f4-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="1e1f4-191">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="1e1f4-191">Get help</span></span>
<span data-ttu-id="1e1f4-192">Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1e1f4-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e1f4-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e1f4-193">Next steps</span></span>
* [<span data-ttu-id="1e1f4-194">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1e1f4-195">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1e1f4-196">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="1e1f4-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1e1f4-197">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1e1f4-198">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1e1f4-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
