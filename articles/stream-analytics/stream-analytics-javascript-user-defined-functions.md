---
title: "funciones definidas por el usuario de JavaScript de análisis de transmisiones aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="aab79-104">Funciones definidas por el usuario en JavaScript para Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aab79-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="aab79-105">Azure Stream Analytics admite funciones definidas por el usuario escritas en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="aab79-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="aab79-106">Conjunto completo de Hola de **cadena**, **RegExp**, **matemáticas**, **matriz**, y **fecha** métodos que JavaScript proporciona, las transformaciones de datos complejos con trabajos de análisis de transmisiones se convierten en toocreate más fácil.</span><span class="sxs-lookup"><span data-stu-id="aab79-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="aab79-107">Funciones definidas por el usuario en JavaScript</span><span class="sxs-lookup"><span data-stu-id="aab79-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="aab79-108">Las funciones definidas por el usuario en JavaScript admiten funciones escalares de solo cálculo y sin estado, que no requieren conectividad externa.</span><span class="sxs-lookup"><span data-stu-id="aab79-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="aab79-109">Hola devuelve el valor de una función sólo puede ser un valor escalar (único).</span><span class="sxs-lookup"><span data-stu-id="aab79-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="aab79-110">Después de agregar un trabajo de tooa de función definida por el usuario de JavaScript, puede utilizar función hello en cualquier parte en la consulta de hello, como una función escalar integrada.</span><span class="sxs-lookup"><span data-stu-id="aab79-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="aab79-111">Estos son algunos escenarios en los que le podrían resultar útiles las funciones definidas por el usuario en JavaScript:</span><span class="sxs-lookup"><span data-stu-id="aab79-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="aab79-112">Análisis y manipulación de cadenas que incluyen funciones de expresiones regulares, por ejemplo, **Regexp_Replace()** y **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="aab79-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="aab79-113">Descodificación y codificación de datos, por ejemplo, conversión de binario a hexadecimal</span><span class="sxs-lookup"><span data-stu-id="aab79-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="aab79-114">Realización de cálculos matemáticos con funciones **matemáticas** de JavaScript</span><span class="sxs-lookup"><span data-stu-id="aab79-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="aab79-115">Realización de operaciones de matriz como ordenar, combinar, buscar y rellenar</span><span class="sxs-lookup"><span data-stu-id="aab79-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="aab79-116">Aquí se indican algunas operaciones que no se pueden realizar con una función definida por el usuario de JavaScript en Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="aab79-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="aab79-117">Llamar a puntos de conexión de REST externos, por ejemplo, mediante la realización de una búsqueda inversa de direcciones IP o una extracción de datos de referencia de un origen externo</span><span class="sxs-lookup"><span data-stu-id="aab79-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="aab79-118">Realizar la serialización o deserialización de formatos de eventos personalizados en entradas y salidas</span><span class="sxs-lookup"><span data-stu-id="aab79-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="aab79-119">Crear agregados personalizados</span><span class="sxs-lookup"><span data-stu-id="aab79-119">Create custom aggregates</span></span>

<span data-ttu-id="aab79-120">Aunque las funciones como **Date.GetDate()** o **Math.random()** no están bloqueados en la definición de funciones de hello, debería evitar su uso.</span><span class="sxs-lookup"><span data-stu-id="aab79-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="aab79-121">Estas funciones **no** devuelto Hola mismo resultado cada vez que llamarlas y Hola servicio Azure Stream Analytics no mantiene un diario de las llamadas a funciones y devuelve resultados.</span><span class="sxs-lookup"><span data-stu-id="aab79-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="aab79-122">Si una función devuelve un resultado diferente en hello mismos eventos, repetibilidad no se garantiza que cuando se reinicia un trabajo por usted o por el servicio de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="aab79-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="aab79-123">Agregar una función definida por el usuario de JavaScript en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="aab79-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="aab79-124">toocreate una función definida por el usuario simple de JavaScript en un trabajo de análisis de transmisiones existente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="aab79-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="aab79-125">En hello portal de Azure, busque el trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="aab79-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="aab79-126">En **TOPOLOGÍA DE TRABAJO**, seleccione la función.</span><span class="sxs-lookup"><span data-stu-id="aab79-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="aab79-127">Aparece una lista vacía de funciones.</span><span class="sxs-lookup"><span data-stu-id="aab79-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="aab79-128">toocreate una nueva función definida por el usuario, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="aab79-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="aab79-129">En hello **nueva función** hoja, para **tipo de función**, seleccione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="aab79-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="aab79-130">Una plantilla de función predeterminado aparece en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="aab79-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="aab79-131">Para hello **alias UDF**, escriba **hex2Int**y cambiar la implementación de la función de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="aab79-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="aab79-132">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="aab79-132">Select **Save**.</span></span> <span data-ttu-id="aab79-133">La función aparece en la lista de Hola de funciones.</span><span class="sxs-lookup"><span data-stu-id="aab79-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="aab79-134">Seleccione Hola de nuevo **hex2Int** función y comprobar la definición de función de Hola.</span><span class="sxs-lookup"><span data-stu-id="aab79-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="aab79-135">Todas las funciones tienen un **UDF** alias de prefijo de función de agregado toohello.</span><span class="sxs-lookup"><span data-stu-id="aab79-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="aab79-136">Necesita demasiado*incluir el prefijo de hello* cuando se llama a función hello en la consulta de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="aab79-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="aab79-137">En este caso, debe llamar a **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="aab79-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="aab79-138">Llamada a una función definida por el usuario de JavaScript en una consulta</span><span class="sxs-lookup"><span data-stu-id="aab79-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="aab79-139">Hola editor de consultas, en **trabajo topología**, seleccione **consulta**.</span><span class="sxs-lookup"><span data-stu-id="aab79-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="aab79-140">Editar la consulta y, a continuación, llame a función definida por el usuario de hello, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="aab79-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="aab79-141">archivo de datos de ejemplo de Hola tooupload, entrada de trabajo de Hola de menú contextual.</span><span class="sxs-lookup"><span data-stu-id="aab79-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="aab79-142">tootest la consulta, seleccione **prueba**.</span><span class="sxs-lookup"><span data-stu-id="aab79-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="aab79-143">Objetos de JavaScript compatibles</span><span class="sxs-lookup"><span data-stu-id="aab79-143">Supported JavaScript objects</span></span>
<span data-ttu-id="aab79-144">Las funciones definidas por el usuario en JavaScript para Azure Stream Analytics admiten objetos de JavaScript estándar e integrados.</span><span class="sxs-lookup"><span data-stu-id="aab79-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="aab79-145">Para obtener una lista de estos objetos, consulte [Objetos globales](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="aab79-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="aab79-146">Conversión de tipos de Stream Analytics y JavaScript</span><span class="sxs-lookup"><span data-stu-id="aab79-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="aab79-147">Existen diferencias en los tipos de Hola que admiten el lenguaje de consultas de análisis de transmisiones de Hola y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="aab79-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="aab79-148">Esta tabla enumeran las asignaciones de conversión de hello entre Hola dos:</span><span class="sxs-lookup"><span data-stu-id="aab79-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="aab79-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aab79-149">Stream Analytics</span></span> | <span data-ttu-id="aab79-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="aab79-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="aab79-151">bigint</span><span class="sxs-lookup"><span data-stu-id="aab79-151">bigint</span></span> | <span data-ttu-id="aab79-152">Número (JavaScript solo puede representar enteros seguridad tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="aab79-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="aab79-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="aab79-153">DateTime</span></span> | <span data-ttu-id="aab79-154">Date (JavaScript solo admite milisegundos)</span><span class="sxs-lookup"><span data-stu-id="aab79-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="aab79-155">double</span><span class="sxs-lookup"><span data-stu-id="aab79-155">double</span></span> | <span data-ttu-id="aab79-156">Number</span><span class="sxs-lookup"><span data-stu-id="aab79-156">Number</span></span>
<span data-ttu-id="aab79-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="aab79-157">nvarchar(MAX)</span></span> | <span data-ttu-id="aab79-158">String</span><span class="sxs-lookup"><span data-stu-id="aab79-158">String</span></span>
<span data-ttu-id="aab79-159">Registro</span><span class="sxs-lookup"><span data-stu-id="aab79-159">Record</span></span> | <span data-ttu-id="aab79-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="aab79-160">Object</span></span>
<span data-ttu-id="aab79-161">Matriz</span><span class="sxs-lookup"><span data-stu-id="aab79-161">Array</span></span> | <span data-ttu-id="aab79-162">Matriz</span><span class="sxs-lookup"><span data-stu-id="aab79-162">Array</span></span>
<span data-ttu-id="aab79-163">NULL</span><span class="sxs-lookup"><span data-stu-id="aab79-163">NULL</span></span> | <span data-ttu-id="aab79-164">Null</span><span class="sxs-lookup"><span data-stu-id="aab79-164">Null</span></span>


<span data-ttu-id="aab79-165">Estas son las conversiones de JavaScript a Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="aab79-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="aab79-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="aab79-166">JavaScript</span></span> | <span data-ttu-id="aab79-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aab79-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="aab79-168">Number</span><span class="sxs-lookup"><span data-stu-id="aab79-168">Number</span></span> | <span data-ttu-id="aab79-169">Bigint (si el número de hello es round y entre larga. MinValue y long. MaxValue; en caso contrario, es double)</span><span class="sxs-lookup"><span data-stu-id="aab79-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="aab79-170">Date</span><span class="sxs-lookup"><span data-stu-id="aab79-170">Date</span></span> | <span data-ttu-id="aab79-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="aab79-171">DateTime</span></span>
<span data-ttu-id="aab79-172">String</span><span class="sxs-lookup"><span data-stu-id="aab79-172">String</span></span> | <span data-ttu-id="aab79-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="aab79-173">nvarchar(MAX)</span></span>
<span data-ttu-id="aab79-174">Objeto</span><span class="sxs-lookup"><span data-stu-id="aab79-174">Object</span></span> | <span data-ttu-id="aab79-175">Registro</span><span class="sxs-lookup"><span data-stu-id="aab79-175">Record</span></span>
<span data-ttu-id="aab79-176">Matriz</span><span class="sxs-lookup"><span data-stu-id="aab79-176">Array</span></span> | <span data-ttu-id="aab79-177">Matriz</span><span class="sxs-lookup"><span data-stu-id="aab79-177">Array</span></span>
<span data-ttu-id="aab79-178">Null, sin definir</span><span class="sxs-lookup"><span data-stu-id="aab79-178">Null, Undefined</span></span> | <span data-ttu-id="aab79-179">NULL</span><span class="sxs-lookup"><span data-stu-id="aab79-179">NULL</span></span>
<span data-ttu-id="aab79-180">Cualquier otro tipo (por ejemplo, una función o un error)</span><span class="sxs-lookup"><span data-stu-id="aab79-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="aab79-181">No admitido (da lugar a un error en tiempo de ejecución)</span><span class="sxs-lookup"><span data-stu-id="aab79-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="aab79-182">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="aab79-182">Troubleshooting</span></span>
<span data-ttu-id="aab79-183">Errores de tiempo de ejecución de JavaScript se consideran muy negativos y se exponen a través del registro de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="aab79-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="aab79-184">registro de hello tooretrieve, expresada en hello portal de Azure, vaya tooyour trabajo y seleccione **registro de actividad**.</span><span class="sxs-lookup"><span data-stu-id="aab79-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="aab79-185">Otros patrones de función definida por el usuario de JavaScript</span><span class="sxs-lookup"><span data-stu-id="aab79-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="aab79-186">Escribir anidada toooutput JSON</span><span class="sxs-lookup"><span data-stu-id="aab79-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="aab79-187">Si tiene un paso del procesamiento de seguimiento que utiliza un trabajo de análisis de transmisiones de salida como entrada, y requiere un formato JSON, puede escribir una toooutput de cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="aab79-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="aab79-188">el ejemplo siguiente se Hola llama hello **JSON.stringify()** toopack todos los pares de nombre/valor de hello de entrada y, a continuación, escriben como un único valor de cadena en la salida de función.</span><span class="sxs-lookup"><span data-stu-id="aab79-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="aab79-189">**Definición de funciones definidas por el usuario en JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="aab79-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="aab79-190">**Consulta de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="aab79-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="aab79-191">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="aab79-191">Get help</span></span>
<span data-ttu-id="aab79-192">Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="aab79-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aab79-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aab79-193">Next steps</span></span>
* [<span data-ttu-id="aab79-194">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="aab79-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="aab79-195">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aab79-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="aab79-196">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="aab79-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="aab79-197">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aab79-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="aab79-198">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aab79-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
