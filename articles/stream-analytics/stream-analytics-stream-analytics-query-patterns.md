---
title: "ejemplos de patrones de uso comunes de análisis de transmisiones los aaaQuery | Documentos de Microsoft"
description: Patrones de consulta comunes de Azure Stream Analytics
keywords: ejemplos de consultas
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="406ce-104">Ejemplos de consulta para patrones de uso comunes de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="406ce-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="406ce-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="406ce-105">Introduction</span></span>
<span data-ttu-id="406ce-106">Las consultas de Azure Stream Analytics se expresan en un lenguaje de consulta similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="406ce-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="406ce-107">Estas consultas se documentan en hello [referencia del lenguaje de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx) guía.</span><span class="sxs-lookup"><span data-stu-id="406ce-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="406ce-108">Este patrones de consulta común de artículo se describen las soluciones tooseveral, basándose en situaciones del mundo real.</span><span class="sxs-lookup"><span data-stu-id="406ce-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="406ce-109">Es un trabajo en curso y continúa toobe actualizada con nuevos patrones de forma continuada.</span><span class="sxs-lookup"><span data-stu-id="406ce-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="406ce-110">Ejemplo de consulta: conversión de tipos de datos</span><span class="sxs-lookup"><span data-stu-id="406ce-110">Query example: Convert data types</span></span>
<span data-ttu-id="406ce-111">**Descripción**: definir tipos de Hola de propiedades en el flujo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="406ce-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="406ce-112">Por ejemplo, hello automóvil procede en el flujo de entrada de hello como cadenas y la importancia de necesita toobe convertir demasiado**INT** tooperform **suma** , configúrelo.</span><span class="sxs-lookup"><span data-stu-id="406ce-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="406ce-113">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-113">**Input**:</span></span>

| <span data-ttu-id="406ce-114">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-114">Make</span></span> | <span data-ttu-id="406ce-115">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-115">Time</span></span> | <span data-ttu-id="406ce-116">Peso</span><span class="sxs-lookup"><span data-stu-id="406ce-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-117">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-117">Honda</span></span> |<span data-ttu-id="406ce-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="406ce-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="406ce-119">"1000"</span></span> |
| <span data-ttu-id="406ce-120">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-120">Honda</span></span> |<span data-ttu-id="406ce-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="406ce-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="406ce-122">"2000"</span></span> |

<span data-ttu-id="406ce-123">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-123">**Output**:</span></span>

| <span data-ttu-id="406ce-124">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-124">Make</span></span> | <span data-ttu-id="406ce-125">Peso</span><span class="sxs-lookup"><span data-stu-id="406ce-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-126">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-126">Honda</span></span> |<span data-ttu-id="406ce-127">3000</span><span class="sxs-lookup"><span data-stu-id="406ce-127">3000</span></span> |

<span data-ttu-id="406ce-128">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="406ce-129">**Explicación**: Use un **conversión** instrucción Hola **peso** campo toospecify su tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="406ce-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="406ce-130">Ver lista de Hola de tipos de datos compatibles en [tipos de datos (análisis de transmisiones de Azure)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="406ce-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="406ce-131">Ejemplo de consulta: usan Like o Not like toodo coincidencia de patrones</span><span class="sxs-lookup"><span data-stu-id="406ce-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="406ce-132">**Descripción**: Compruebe que el valor de un campo en el evento Hola coincide con un patrón determinado.</span><span class="sxs-lookup"><span data-stu-id="406ce-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="406ce-133">Por ejemplo, compruebe que el resultado de hello devuelve platos de licencia que comience con una letra y terminar por 9.</span><span class="sxs-lookup"><span data-stu-id="406ce-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="406ce-134">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-134">**Input**:</span></span>

| <span data-ttu-id="406ce-135">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-135">Make</span></span> | <span data-ttu-id="406ce-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-136">LicensePlate</span></span> | <span data-ttu-id="406ce-137">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-138">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-138">Honda</span></span> |<span data-ttu-id="406ce-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="406ce-139">ABC-123</span></span> |<span data-ttu-id="406ce-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-141">Toyota</span></span> |<span data-ttu-id="406ce-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="406ce-142">AAA-999</span></span> |<span data-ttu-id="406ce-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="406ce-144">Nissan</span></span> |<span data-ttu-id="406ce-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="406ce-145">ABC-369</span></span> |<span data-ttu-id="406ce-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="406ce-147">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-147">**Output**:</span></span>

| <span data-ttu-id="406ce-148">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-148">Make</span></span> | <span data-ttu-id="406ce-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-149">LicensePlate</span></span> | <span data-ttu-id="406ce-150">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-151">Toyota</span></span> |<span data-ttu-id="406ce-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="406ce-152">AAA-999</span></span> |<span data-ttu-id="406ce-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="406ce-154">Nissan</span></span> |<span data-ttu-id="406ce-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="406ce-155">ABC-369</span></span> |<span data-ttu-id="406ce-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="406ce-157">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="406ce-158">**Explicación**: Hola de uso **como** Hola de instrucción toocheck **LicensePlate** valor del campo.</span><span class="sxs-lookup"><span data-stu-id="406ce-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="406ce-159">Debe comenzar con una A, seguida de cualquier cadena de ceros o más caracteres y terminar en nueve.</span><span class="sxs-lookup"><span data-stu-id="406ce-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="406ce-160">Ejemplo de consulta: especificación de la lógica para los distintos casos/valores (instrucciones CASE)</span><span class="sxs-lookup"><span data-stu-id="406ce-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="406ce-161">**Descripción**: proporcione un cálculo diferente para un campo en función de un criterio concreto.</span><span class="sxs-lookup"><span data-stu-id="406ce-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="406ce-162">Por ejemplo, proporcione una descripción de cadena para automóviles cuántos de hello igual que pasan, con un caso especial de 1.</span><span class="sxs-lookup"><span data-stu-id="406ce-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="406ce-163">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-163">**Input**:</span></span>

| <span data-ttu-id="406ce-164">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-164">Make</span></span> | <span data-ttu-id="406ce-165">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-166">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-166">Honda</span></span> |<span data-ttu-id="406ce-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-168">Toyota</span></span> |<span data-ttu-id="406ce-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-170">Toyota</span></span> |<span data-ttu-id="406ce-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="406ce-172">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-172">**Output**:</span></span>

| <span data-ttu-id="406ce-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="406ce-173">CarsPassed</span></span> | <span data-ttu-id="406ce-174">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-175">1 Honda</span></span> |<span data-ttu-id="406ce-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="406ce-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="406ce-177">2 Toyotas</span></span> |<span data-ttu-id="406ce-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="406ce-179">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="406ce-180">**Explicación**: Hola **caso** cláusula nos permite tooprovide un cálculo diferentes, en función de algunos criterios (en nuestro caso, el recuento de Hola de automóviles hello en la ventana agregado de hello).</span><span class="sxs-lookup"><span data-stu-id="406ce-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="406ce-181">Ejemplo de consulta: enviar datos toomultiple genera</span><span class="sxs-lookup"><span data-stu-id="406ce-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="406ce-182">**Descripción**: enviar datos toomultiple destinos desde un único trabajo de salida.</span><span class="sxs-lookup"><span data-stu-id="406ce-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="406ce-183">Por ejemplo, analizar los datos de una alerta basadas en umbrales y todos los eventos tooblob almacenamiento de archivo.</span><span class="sxs-lookup"><span data-stu-id="406ce-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="406ce-184">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-184">**Input**:</span></span>

| <span data-ttu-id="406ce-185">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-185">Make</span></span> | <span data-ttu-id="406ce-186">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-187">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-187">Honda</span></span> |<span data-ttu-id="406ce-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-189">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-189">Honda</span></span> |<span data-ttu-id="406ce-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-191">Toyota</span></span> |<span data-ttu-id="406ce-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-193">Toyota</span></span> |<span data-ttu-id="406ce-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-195">Toyota</span></span> |<span data-ttu-id="406ce-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="406ce-197">**Salida1**:</span><span class="sxs-lookup"><span data-stu-id="406ce-197">**Output1**:</span></span>

| <span data-ttu-id="406ce-198">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-198">Make</span></span> | <span data-ttu-id="406ce-199">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-200">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-200">Honda</span></span> |<span data-ttu-id="406ce-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-202">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-202">Honda</span></span> |<span data-ttu-id="406ce-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-204">Toyota</span></span> |<span data-ttu-id="406ce-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-206">Toyota</span></span> |<span data-ttu-id="406ce-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-208">Toyota</span></span> |<span data-ttu-id="406ce-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="406ce-210">**Salida2**:</span><span class="sxs-lookup"><span data-stu-id="406ce-210">**Output2**:</span></span>

| <span data-ttu-id="406ce-211">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-211">Make</span></span> | <span data-ttu-id="406ce-212">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-212">Time</span></span> | <span data-ttu-id="406ce-213">Recuento</span><span class="sxs-lookup"><span data-stu-id="406ce-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-214">Toyota</span></span> |<span data-ttu-id="406ce-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="406ce-216">3</span><span class="sxs-lookup"><span data-stu-id="406ce-216">3</span></span> |

<span data-ttu-id="406ce-217">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="406ce-218">**Explicación**: Hola **INTO** cláusula indica el análisis de transmisiones que de hello genera toowrite Hola datos toofrom esta instrucción.</span><span class="sxs-lookup"><span data-stu-id="406ce-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="406ce-219">Hola primera consulta es un acceso directo de datos de saludo se recibió una salida tooan que se denomina **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="406ce-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="406ce-220">segunda consulta de Hello realiza algunas agregaciones simples y filtrado y lo envía resultados hello tooa sistema de alertas siguen en la cadena.</span><span class="sxs-lookup"><span data-stu-id="406ce-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="406ce-221">Tenga en cuenta que también puede reutilizar los resultados de Hola de expresiones de tabla común (CTE) de hello (como **WITH** instrucciones) en varias instrucciones de salida.</span><span class="sxs-lookup"><span data-stu-id="406ce-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="406ce-222">Esta opción se Hola ventaja adicional de abrir el origen de entrada de toohello de lectores menos.</span><span class="sxs-lookup"><span data-stu-id="406ce-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="406ce-223">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="406ce-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="406ce-224">Ejemplo de consulta: recuento de valores únicos</span><span class="sxs-lookup"><span data-stu-id="406ce-224">Query example: Count unique values</span></span>
<span data-ttu-id="406ce-225">**Descripción**: contar Hola número único de valores de campo que aparecen en la secuencia de hello dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="406ce-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="406ce-226">Por ejemplo, ¿cuántos único hace que sea de automóviles que se pasan a través de la cabina de peaje hello en una ventana de 2 segundos?</span><span class="sxs-lookup"><span data-stu-id="406ce-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="406ce-227">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-227">**Input**:</span></span>

| <span data-ttu-id="406ce-228">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-228">Make</span></span> | <span data-ttu-id="406ce-229">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-230">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-230">Honda</span></span> |<span data-ttu-id="406ce-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-232">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-232">Honda</span></span> |<span data-ttu-id="406ce-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-234">Toyota</span></span> |<span data-ttu-id="406ce-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-236">Toyota</span></span> |<span data-ttu-id="406ce-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-238">Toyota</span></span> |<span data-ttu-id="406ce-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="406ce-240">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="406ce-240">**Output:**</span></span>

| <span data-ttu-id="406ce-241">Recuento</span><span class="sxs-lookup"><span data-stu-id="406ce-241">Count</span></span> | <span data-ttu-id="406ce-242">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-243">2</span><span class="sxs-lookup"><span data-stu-id="406ce-243">2</span></span> |<span data-ttu-id="406ce-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="406ce-245">1</span><span class="sxs-lookup"><span data-stu-id="406ce-245">1</span></span> |<span data-ttu-id="406ce-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="406ce-247">**Solución:**</span><span class="sxs-lookup"><span data-stu-id="406ce-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="406ce-248">**Explicación:**
**COUNT (DISTINCT hacer)** devuelve Hola número de valores distintos en hello **realizar** columna dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="406ce-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="406ce-249">Ejemplo de consulta: determinar si un valor ha cambiado</span><span class="sxs-lookup"><span data-stu-id="406ce-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="406ce-250">**Descripción**: examine un toodetermine valor anterior si es diferente del valor actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="406ce-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="406ce-251">¿Por ejemplo, está automóvil anterior hello en Hola Hola de carreteras de peaje que misma marca como car actual Hola?</span><span class="sxs-lookup"><span data-stu-id="406ce-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="406ce-252">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-252">**Input**:</span></span>

| <span data-ttu-id="406ce-253">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-253">Make</span></span> | <span data-ttu-id="406ce-254">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-255">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-255">Honda</span></span> |<span data-ttu-id="406ce-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-257">Toyota</span></span> |<span data-ttu-id="406ce-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="406ce-259">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-259">**Output**:</span></span>

| <span data-ttu-id="406ce-260">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-260">Make</span></span> | <span data-ttu-id="406ce-261">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-262">Toyota</span></span> |<span data-ttu-id="406ce-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="406ce-264">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="406ce-265">**Explicación**: Use **LAG** toopeek en hello secuencia un evento nuevo de entrada y obtener hello **realizar** valor.</span><span class="sxs-lookup"><span data-stu-id="406ce-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="406ce-266">A continuación, compárela toohello **realizar** el valor en hello actual y evento salida Hola si son diferentes.</span><span class="sxs-lookup"><span data-stu-id="406ce-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="406ce-267">Ejemplo de consulta: primer evento de Hola de búsqueda en una ventana</span><span class="sxs-lookup"><span data-stu-id="406ce-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="406ce-268">**Descripción**: primer coche de Hola de búsqueda en cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="406ce-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="406ce-269">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-269">**Input**:</span></span>

| <span data-ttu-id="406ce-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-270">LicensePlate</span></span> | <span data-ttu-id="406ce-271">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-271">Make</span></span> | <span data-ttu-id="406ce-272">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="406ce-273">DXE 5291</span></span> |<span data-ttu-id="406ce-274">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-274">Honda</span></span> |<span data-ttu-id="406ce-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="406ce-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="406ce-276">YZK 5704</span></span> |<span data-ttu-id="406ce-277">Ford</span><span class="sxs-lookup"><span data-stu-id="406ce-277">Ford</span></span> |<span data-ttu-id="406ce-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="406ce-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="406ce-279">RMV 8282</span></span> |<span data-ttu-id="406ce-280">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-280">Honda</span></span> |<span data-ttu-id="406ce-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="406ce-282">YHN 6970</span></span> |<span data-ttu-id="406ce-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-283">Toyota</span></span> |<span data-ttu-id="406ce-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="406ce-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="406ce-285">VFE 1616</span></span> |<span data-ttu-id="406ce-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-286">Toyota</span></span> |<span data-ttu-id="406ce-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="406ce-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="406ce-288">QYF 9358</span></span> |<span data-ttu-id="406ce-289">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-289">Honda</span></span> |<span data-ttu-id="406ce-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="406ce-291">MDR 6128</span></span> |<span data-ttu-id="406ce-292">BMW</span><span class="sxs-lookup"><span data-stu-id="406ce-292">BMW</span></span> |<span data-ttu-id="406ce-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="406ce-294">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-294">**Output**:</span></span>

| <span data-ttu-id="406ce-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-295">LicensePlate</span></span> | <span data-ttu-id="406ce-296">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-296">Make</span></span> | <span data-ttu-id="406ce-297">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="406ce-298">DXE 5291</span></span> |<span data-ttu-id="406ce-299">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-299">Honda</span></span> |<span data-ttu-id="406ce-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="406ce-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="406ce-301">QYF 9358</span></span> |<span data-ttu-id="406ce-302">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-302">Honda</span></span> |<span data-ttu-id="406ce-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="406ce-304">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="406ce-305">Ahora vamos a hacer el cambio Hola problema y buscar Hola primer coche de una determinada en cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="406ce-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="406ce-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-306">LicensePlate</span></span> | <span data-ttu-id="406ce-307">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-307">Make</span></span> | <span data-ttu-id="406ce-308">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="406ce-309">DXE 5291</span></span> |<span data-ttu-id="406ce-310">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-310">Honda</span></span> |<span data-ttu-id="406ce-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="406ce-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="406ce-312">YZK 5704</span></span> |<span data-ttu-id="406ce-313">Ford</span><span class="sxs-lookup"><span data-stu-id="406ce-313">Ford</span></span> |<span data-ttu-id="406ce-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="406ce-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="406ce-315">YHN 6970</span></span> |<span data-ttu-id="406ce-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-316">Toyota</span></span> |<span data-ttu-id="406ce-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="406ce-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="406ce-318">QYF 9358</span></span> |<span data-ttu-id="406ce-319">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-319">Honda</span></span> |<span data-ttu-id="406ce-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="406ce-321">MDR 6128</span></span> |<span data-ttu-id="406ce-322">BMW</span><span class="sxs-lookup"><span data-stu-id="406ce-322">BMW</span></span> |<span data-ttu-id="406ce-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="406ce-324">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="406ce-325">Ejemplo de consulta: último evento de Hola de búsqueda en una ventana</span><span class="sxs-lookup"><span data-stu-id="406ce-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="406ce-326">**Descripción**: último automóvil de Hola de búsqueda en cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="406ce-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="406ce-327">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-327">**Input**:</span></span>

| <span data-ttu-id="406ce-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-328">LicensePlate</span></span> | <span data-ttu-id="406ce-329">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-329">Make</span></span> | <span data-ttu-id="406ce-330">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="406ce-331">DXE 5291</span></span> |<span data-ttu-id="406ce-332">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-332">Honda</span></span> |<span data-ttu-id="406ce-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="406ce-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="406ce-334">YZK 5704</span></span> |<span data-ttu-id="406ce-335">Ford</span><span class="sxs-lookup"><span data-stu-id="406ce-335">Ford</span></span> |<span data-ttu-id="406ce-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="406ce-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="406ce-337">RMV 8282</span></span> |<span data-ttu-id="406ce-338">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-338">Honda</span></span> |<span data-ttu-id="406ce-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="406ce-340">YHN 6970</span></span> |<span data-ttu-id="406ce-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-341">Toyota</span></span> |<span data-ttu-id="406ce-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="406ce-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="406ce-343">VFE 1616</span></span> |<span data-ttu-id="406ce-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-344">Toyota</span></span> |<span data-ttu-id="406ce-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="406ce-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="406ce-346">QYF 9358</span></span> |<span data-ttu-id="406ce-347">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-347">Honda</span></span> |<span data-ttu-id="406ce-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="406ce-349">MDR 6128</span></span> |<span data-ttu-id="406ce-350">BMW</span><span class="sxs-lookup"><span data-stu-id="406ce-350">BMW</span></span> |<span data-ttu-id="406ce-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="406ce-352">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-352">**Output**:</span></span>

| <span data-ttu-id="406ce-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-353">LicensePlate</span></span> | <span data-ttu-id="406ce-354">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-354">Make</span></span> | <span data-ttu-id="406ce-355">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="406ce-356">VFE 1616</span></span> |<span data-ttu-id="406ce-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-357">Toyota</span></span> |<span data-ttu-id="406ce-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="406ce-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="406ce-359">MDR 6128</span></span> |<span data-ttu-id="406ce-360">BMW</span><span class="sxs-lookup"><span data-stu-id="406ce-360">BMW</span></span> |<span data-ttu-id="406ce-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="406ce-362">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="406ce-363">**Explicación**: hay dos pasos en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="406ce-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="406ce-364">Hola primera busca una hello más reciente marca de tiempo en las ventanas de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="406ce-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="406ce-365">las combinaciones de Hello segundo paso Hola resultados de Hola la primera consulta con hello original flujo toofind Hola eventos que coinciden con marcas de tiempo último hello en cada ventana.</span><span class="sxs-lookup"><span data-stu-id="406ce-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="406ce-366">Ejemplo de consulta: detectar Hola ausencia de eventos</span><span class="sxs-lookup"><span data-stu-id="406ce-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="406ce-367">**Descripción**: compruebe que un flujo no tiene ningún valor que cumpla un criterio determinado.</span><span class="sxs-lookup"><span data-stu-id="406ce-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="406ce-368">¿Por ejemplo, han 2 automóviles consecutivas de la misma marca de hello escrito carreteras de peaje hello en hello últimos 90 segundos?</span><span class="sxs-lookup"><span data-stu-id="406ce-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="406ce-369">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-369">**Input**:</span></span>

| <span data-ttu-id="406ce-370">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-370">Make</span></span> | <span data-ttu-id="406ce-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-371">LicensePlate</span></span> | <span data-ttu-id="406ce-372">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-373">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-373">Honda</span></span> |<span data-ttu-id="406ce-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="406ce-374">ABC-123</span></span> |<span data-ttu-id="406ce-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="406ce-376">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-376">Honda</span></span> |<span data-ttu-id="406ce-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="406ce-377">AAA-999</span></span> |<span data-ttu-id="406ce-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="406ce-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-379">Toyota</span></span> |<span data-ttu-id="406ce-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="406ce-380">DEF-987</span></span> |<span data-ttu-id="406ce-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="406ce-382">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-382">Honda</span></span> |<span data-ttu-id="406ce-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="406ce-383">GHI-345</span></span> |<span data-ttu-id="406ce-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="406ce-385">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-385">**Output**:</span></span>

| <span data-ttu-id="406ce-386">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-386">Make</span></span> | <span data-ttu-id="406ce-387">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-387">Time</span></span> | <span data-ttu-id="406ce-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="406ce-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="406ce-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="406ce-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="406ce-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="406ce-391">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-391">Honda</span></span> |<span data-ttu-id="406ce-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="406ce-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="406ce-393">AAA-999</span></span> |<span data-ttu-id="406ce-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="406ce-394">ABC-123</span></span> |<span data-ttu-id="406ce-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="406ce-396">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="406ce-397">**Explicación**: Use **LAG** toopeek en hello secuencia un evento nuevo de entrada y obtener hello **realizar** valor.</span><span class="sxs-lookup"><span data-stu-id="406ce-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="406ce-398">Comparar toohello **realizar** valor en el evento actual hello y, a continuación, evento de Hola de salida si están Hola igual.</span><span class="sxs-lookup"><span data-stu-id="406ce-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="406ce-399">También puede usar **LAG** tooget datos acerca de automóvil anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="406ce-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="406ce-400">Ejemplo de consulta: detectar Hola duración del intervalo entre eventos</span><span class="sxs-lookup"><span data-stu-id="406ce-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="406ce-401">**Descripción**: buscar duración Hola de un evento determinado.</span><span class="sxs-lookup"><span data-stu-id="406ce-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="406ce-402">Por ejemplo, dada una secuencia de clics de web, determine tiempo de hello invertido en una característica.</span><span class="sxs-lookup"><span data-stu-id="406ce-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="406ce-403">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-403">**Input**:</span></span>  

| <span data-ttu-id="406ce-404">Usuario</span><span class="sxs-lookup"><span data-stu-id="406ce-404">User</span></span> | <span data-ttu-id="406ce-405">Característica</span><span class="sxs-lookup"><span data-stu-id="406ce-405">Feature</span></span> | <span data-ttu-id="406ce-406">Evento</span><span class="sxs-lookup"><span data-stu-id="406ce-406">Event</span></span> | <span data-ttu-id="406ce-407">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="406ce-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="406ce-408">RightMenu</span></span> |<span data-ttu-id="406ce-409">Iniciar</span><span class="sxs-lookup"><span data-stu-id="406ce-409">Start</span></span> |<span data-ttu-id="406ce-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="406ce-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="406ce-411">RightMenu</span></span> |<span data-ttu-id="406ce-412">End</span><span class="sxs-lookup"><span data-stu-id="406ce-412">End</span></span> |<span data-ttu-id="406ce-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="406ce-414">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-414">**Output**:</span></span>  

| <span data-ttu-id="406ce-415">Usuario</span><span class="sxs-lookup"><span data-stu-id="406ce-415">User</span></span> | <span data-ttu-id="406ce-416">Característica</span><span class="sxs-lookup"><span data-stu-id="406ce-416">Feature</span></span> | <span data-ttu-id="406ce-417">Duración</span><span class="sxs-lookup"><span data-stu-id="406ce-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="406ce-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="406ce-418">RightMenu</span></span> |<span data-ttu-id="406ce-419">7</span><span class="sxs-lookup"><span data-stu-id="406ce-419">7</span></span> |

<span data-ttu-id="406ce-420">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="406ce-421">**Explicación**: Hola de uso **última** función hello tooretrieve última **tiempo** valor al tipo de evento de hello era **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="406ce-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="406ce-422">Hola **última** función utiliza **PARTITION BY [user]** tooindicate que Hola resultado se calcula por usuario único.</span><span class="sxs-lookup"><span data-stu-id="406ce-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="406ce-423">consulta de Hello tiene un umbral máximo de 1 hora de diferencia de tiempo de hello entre **iniciar** y **detener** eventos, pero se puede configurar según sea necesario **(límite DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="406ce-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="406ce-424">Ejemplo de consulta: detectar una condición de tiempo que dure Hola</span><span class="sxs-lookup"><span data-stu-id="406ce-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="406ce-425">**Descripción**: averigüe la duración de una condición.</span><span class="sxs-lookup"><span data-stu-id="406ce-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="406ce-426">Por ejemplo, supongamos que, por error, todos los vehículos tienen un peso incorrecto (por encima de 20 000 libras).</span><span class="sxs-lookup"><span data-stu-id="406ce-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="406ce-427">Queremos que la duración de hello toocompute de los errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="406ce-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="406ce-428">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-428">**Input**:</span></span>

| <span data-ttu-id="406ce-429">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="406ce-429">Make</span></span> | <span data-ttu-id="406ce-430">Hora</span><span class="sxs-lookup"><span data-stu-id="406ce-430">Time</span></span> | <span data-ttu-id="406ce-431">Peso</span><span class="sxs-lookup"><span data-stu-id="406ce-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-432">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-432">Honda</span></span> |<span data-ttu-id="406ce-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="406ce-434">2000</span><span class="sxs-lookup"><span data-stu-id="406ce-434">2000</span></span> |
| <span data-ttu-id="406ce-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-435">Toyota</span></span> |<span data-ttu-id="406ce-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="406ce-437">25000</span><span class="sxs-lookup"><span data-stu-id="406ce-437">25000</span></span> |
| <span data-ttu-id="406ce-438">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-438">Honda</span></span> |<span data-ttu-id="406ce-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="406ce-440">26000</span><span class="sxs-lookup"><span data-stu-id="406ce-440">26000</span></span> |
| <span data-ttu-id="406ce-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-441">Toyota</span></span> |<span data-ttu-id="406ce-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="406ce-443">25000</span><span class="sxs-lookup"><span data-stu-id="406ce-443">25000</span></span> |
| <span data-ttu-id="406ce-444">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-444">Honda</span></span> |<span data-ttu-id="406ce-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="406ce-446">26000</span><span class="sxs-lookup"><span data-stu-id="406ce-446">26000</span></span> |
| <span data-ttu-id="406ce-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-447">Toyota</span></span> |<span data-ttu-id="406ce-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="406ce-449">25000</span><span class="sxs-lookup"><span data-stu-id="406ce-449">25000</span></span> |
| <span data-ttu-id="406ce-450">Honda</span><span class="sxs-lookup"><span data-stu-id="406ce-450">Honda</span></span> |<span data-ttu-id="406ce-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="406ce-452">26000</span><span class="sxs-lookup"><span data-stu-id="406ce-452">26000</span></span> |
| <span data-ttu-id="406ce-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="406ce-453">Toyota</span></span> |<span data-ttu-id="406ce-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="406ce-455">2000</span><span class="sxs-lookup"><span data-stu-id="406ce-455">2000</span></span> |

<span data-ttu-id="406ce-456">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="406ce-456">**Output**:</span></span>

| <span data-ttu-id="406ce-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="406ce-457">StartFault</span></span> | <span data-ttu-id="406ce-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="406ce-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="406ce-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="406ce-461">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="406ce-462">**Explicación**: Use **LAG** instancias de flujo de entrada de hello tooview durante 24 horas y buscar dónde **StartFault** y **StopFault** se extienden por hello peso < 20000.</span><span class="sxs-lookup"><span data-stu-id="406ce-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="406ce-463">Ejemplo de consulta: rellenar los valores que faltan</span><span class="sxs-lookup"><span data-stu-id="406ce-463">Query example: Fill missing values</span></span>
<span data-ttu-id="406ce-464">**Descripción**: para el flujo de Hola de eventos que tienen valores que faltan, generar un flujo de eventos con intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="406ce-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="406ce-465">Por ejemplo, generar un evento cada 5 segundos que indica el punto de datos de hello visto más recientemente.</span><span class="sxs-lookup"><span data-stu-id="406ce-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="406ce-466">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="406ce-466">**Input**:</span></span>

| <span data-ttu-id="406ce-467">t</span><span class="sxs-lookup"><span data-stu-id="406ce-467">t</span></span> | <span data-ttu-id="406ce-468">value</span><span class="sxs-lookup"><span data-stu-id="406ce-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="406ce-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="406ce-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="406ce-470">1</span><span class="sxs-lookup"><span data-stu-id="406ce-470">1</span></span> |
| <span data-ttu-id="406ce-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="406ce-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="406ce-472">2</span><span class="sxs-lookup"><span data-stu-id="406ce-472">2</span></span> |
| <span data-ttu-id="406ce-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="406ce-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="406ce-474">3</span><span class="sxs-lookup"><span data-stu-id="406ce-474">3</span></span> |
| <span data-ttu-id="406ce-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="406ce-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="406ce-476">4</span><span class="sxs-lookup"><span data-stu-id="406ce-476">4</span></span> |
| <span data-ttu-id="406ce-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="406ce-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="406ce-478">5</span><span class="sxs-lookup"><span data-stu-id="406ce-478">5</span></span> |
| <span data-ttu-id="406ce-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="406ce-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="406ce-480">6</span><span class="sxs-lookup"><span data-stu-id="406ce-480">6</span></span> |

<span data-ttu-id="406ce-481">**Salida (10 primeras filas)**:</span><span class="sxs-lookup"><span data-stu-id="406ce-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="406ce-482">windowend</span><span class="sxs-lookup"><span data-stu-id="406ce-482">windowend</span></span> | <span data-ttu-id="406ce-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="406ce-483">lastevent.t</span></span> | <span data-ttu-id="406ce-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="406ce-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="406ce-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="406ce-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="406ce-487">1</span><span class="sxs-lookup"><span data-stu-id="406ce-487">1</span></span> |
| <span data-ttu-id="406ce-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="406ce-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="406ce-490">2</span><span class="sxs-lookup"><span data-stu-id="406ce-490">2</span></span> |
| <span data-ttu-id="406ce-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="406ce-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="406ce-493">3</span><span class="sxs-lookup"><span data-stu-id="406ce-493">3</span></span> |
| <span data-ttu-id="406ce-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="406ce-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="406ce-496">4</span><span class="sxs-lookup"><span data-stu-id="406ce-496">4</span></span> |
| <span data-ttu-id="406ce-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="406ce-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="406ce-499">4</span><span class="sxs-lookup"><span data-stu-id="406ce-499">4</span></span> |
| <span data-ttu-id="406ce-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="406ce-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="406ce-502">4</span><span class="sxs-lookup"><span data-stu-id="406ce-502">4</span></span> |
| <span data-ttu-id="406ce-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="406ce-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="406ce-505">5</span><span class="sxs-lookup"><span data-stu-id="406ce-505">5</span></span> |
| <span data-ttu-id="406ce-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="406ce-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="406ce-508">6</span><span class="sxs-lookup"><span data-stu-id="406ce-508">6</span></span> |
| <span data-ttu-id="406ce-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="406ce-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="406ce-511">6</span><span class="sxs-lookup"><span data-stu-id="406ce-511">6</span></span> |
| <span data-ttu-id="406ce-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="406ce-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="406ce-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="406ce-514">6</span><span class="sxs-lookup"><span data-stu-id="406ce-514">6</span></span> |

<span data-ttu-id="406ce-515">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="406ce-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="406ce-516">**Explicación**: esta consulta genera eventos de cada 5 segundos y salidas Hola último evento que se recibió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="406ce-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="406ce-517">Hola [Hopping ventana](https://msdn.microsoft.com/library/dn835041.aspx "Hopping ventana: análisis de transmisiones de Azure") duración determina hasta qué punto Hola atrás consulta presenta un aspecto toofind evento más reciente de hello (300 segundos en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="406ce-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="406ce-518">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="406ce-518">Get help</span></span>
<span data-ttu-id="406ce-519">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="406ce-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="406ce-520">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="406ce-520">Next steps</span></span>
* [<span data-ttu-id="406ce-521">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="406ce-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="406ce-522">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="406ce-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="406ce-523">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="406ce-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="406ce-524">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="406ce-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="406ce-525">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="406ce-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

