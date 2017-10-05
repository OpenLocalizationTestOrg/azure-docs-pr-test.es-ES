---
title: Ejemplos de consulta para patrones de uso comunes de Stream Analytics | Microsoft Docs
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
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="ee97c-104">Ejemplos de consulta para patrones de uso comunes de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee97c-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="ee97c-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="ee97c-105">Introduction</span></span>
<span data-ttu-id="ee97c-106">Las consultas de Azure Stream Analytics se expresan en un lenguaje de consulta similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="ee97c-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="ee97c-107">Estas consultas se documentan en la guía [Referencia de lenguaje de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee97c-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="ee97c-108">En este artículo se describen las soluciones para varios patrones de consulta comunes basados en situaciones del mundo real.</span><span class="sxs-lookup"><span data-stu-id="ee97c-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="ee97c-109">Es un trabajo en curso y continúa actualizándose con nuevos patrones de forma continuada.</span><span class="sxs-lookup"><span data-stu-id="ee97c-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="ee97c-110">Ejemplo de consulta: conversión de tipos de datos</span><span class="sxs-lookup"><span data-stu-id="ee97c-110">Query example: Convert data types</span></span>
<span data-ttu-id="ee97c-111">**Descripción**: defina los tipos de propiedades en el flujo de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee97c-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="ee97c-112">Por ejemplo, el peso del vehículo se incorpora al flujo de entrada como cadena y se debe convertir en **INT** para realizar la operación **SUM**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="ee97c-113">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-113">**Input**:</span></span>

| <span data-ttu-id="ee97c-114">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-114">Make</span></span> | <span data-ttu-id="ee97c-115">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-115">Time</span></span> | <span data-ttu-id="ee97c-116">Peso</span><span class="sxs-lookup"><span data-stu-id="ee97c-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-117">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-117">Honda</span></span> |<span data-ttu-id="ee97c-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="ee97c-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="ee97c-119">"1000"</span></span> |
| <span data-ttu-id="ee97c-120">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-120">Honda</span></span> |<span data-ttu-id="ee97c-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="ee97c-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="ee97c-122">"2000"</span></span> |

<span data-ttu-id="ee97c-123">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-123">**Output**:</span></span>

| <span data-ttu-id="ee97c-124">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-124">Make</span></span> | <span data-ttu-id="ee97c-125">Peso</span><span class="sxs-lookup"><span data-stu-id="ee97c-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-126">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-126">Honda</span></span> |<span data-ttu-id="ee97c-127">3000</span><span class="sxs-lookup"><span data-stu-id="ee97c-127">3000</span></span> |

<span data-ttu-id="ee97c-128">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="ee97c-129">**Explicación**: use una instrucción **CAST** en el campo **Weight** (Peso) para especificar su tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="ee97c-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="ee97c-130">Vea la lista de tipos de datos admitidos en [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx) [Tipos de datos (Azure Stream Analytics)].</span><span class="sxs-lookup"><span data-stu-id="ee97c-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="ee97c-131">Ejemplo de consulta: uso de Like/Not like para realizar la coincidencia de patrones</span><span class="sxs-lookup"><span data-stu-id="ee97c-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="ee97c-132">**Descripción**: compruebe que el valor de un campo del evento coincide con un patrón determinado.</span><span class="sxs-lookup"><span data-stu-id="ee97c-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="ee97c-133">Por ejemplo, compruebe que el resultado devuelve las matrículas que empiezan por A y terminan en nueve.</span><span class="sxs-lookup"><span data-stu-id="ee97c-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="ee97c-134">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-134">**Input**:</span></span>

| <span data-ttu-id="ee97c-135">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-135">Make</span></span> | <span data-ttu-id="ee97c-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-136">LicensePlate</span></span> | <span data-ttu-id="ee97c-137">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-138">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-138">Honda</span></span> |<span data-ttu-id="ee97c-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="ee97c-139">ABC-123</span></span> |<span data-ttu-id="ee97c-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-141">Toyota</span></span> |<span data-ttu-id="ee97c-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="ee97c-142">AAA-999</span></span> |<span data-ttu-id="ee97c-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="ee97c-144">Nissan</span></span> |<span data-ttu-id="ee97c-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="ee97c-145">ABC-369</span></span> |<span data-ttu-id="ee97c-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="ee97c-147">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-147">**Output**:</span></span>

| <span data-ttu-id="ee97c-148">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-148">Make</span></span> | <span data-ttu-id="ee97c-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-149">LicensePlate</span></span> | <span data-ttu-id="ee97c-150">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-151">Toyota</span></span> |<span data-ttu-id="ee97c-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="ee97c-152">AAA-999</span></span> |<span data-ttu-id="ee97c-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="ee97c-154">Nissan</span></span> |<span data-ttu-id="ee97c-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="ee97c-155">ABC-369</span></span> |<span data-ttu-id="ee97c-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="ee97c-157">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="ee97c-158">**Explicación**: use la instrucción **LIKE** para comprobar el valor del campo **LicensePlate**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="ee97c-159">Debe comenzar con una A, seguida de cualquier cadena de ceros o más caracteres y terminar en nueve.</span><span class="sxs-lookup"><span data-stu-id="ee97c-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="ee97c-160">Ejemplo de consulta: especificación de la lógica para los distintos casos/valores (instrucciones CASE)</span><span class="sxs-lookup"><span data-stu-id="ee97c-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="ee97c-161">**Descripción**: proporcione un cálculo diferente para un campo en función de un criterio concreto.</span><span class="sxs-lookup"><span data-stu-id="ee97c-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="ee97c-162">Por ejemplo, proporcione una descripción de cadena para el número de vehículos que han pasado de la misma marca, con un caso especial para 1.</span><span class="sxs-lookup"><span data-stu-id="ee97c-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="ee97c-163">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-163">**Input**:</span></span>

| <span data-ttu-id="ee97c-164">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-164">Make</span></span> | <span data-ttu-id="ee97c-165">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-166">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-166">Honda</span></span> |<span data-ttu-id="ee97c-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-168">Toyota</span></span> |<span data-ttu-id="ee97c-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-170">Toyota</span></span> |<span data-ttu-id="ee97c-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="ee97c-172">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-172">**Output**:</span></span>

| <span data-ttu-id="ee97c-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="ee97c-173">CarsPassed</span></span> | <span data-ttu-id="ee97c-174">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-175">1 Honda</span></span> |<span data-ttu-id="ee97c-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="ee97c-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="ee97c-177">2 Toyotas</span></span> |<span data-ttu-id="ee97c-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="ee97c-179">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-179">**Solution**:</span></span>

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

<span data-ttu-id="ee97c-180">**Explicación**: la cláusula **CASE** permite proporcionar un cálculo diferente en función de criterios determinados (en nuestro caso, el número de automóviles en la ventana de agregado).</span><span class="sxs-lookup"><span data-stu-id="ee97c-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="ee97c-181">Ejemplo de consulta: envío de datos a varias salidas</span><span class="sxs-lookup"><span data-stu-id="ee97c-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="ee97c-182">**Descripción**: envíe datos a varios destinos de salida desde un único trabajo.</span><span class="sxs-lookup"><span data-stu-id="ee97c-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="ee97c-183">Por ejemplo, analice los datos para una alerta de umbral y archive todos los eventos en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ee97c-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="ee97c-184">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-184">**Input**:</span></span>

| <span data-ttu-id="ee97c-185">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-185">Make</span></span> | <span data-ttu-id="ee97c-186">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-187">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-187">Honda</span></span> |<span data-ttu-id="ee97c-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-189">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-189">Honda</span></span> |<span data-ttu-id="ee97c-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-191">Toyota</span></span> |<span data-ttu-id="ee97c-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-193">Toyota</span></span> |<span data-ttu-id="ee97c-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-195">Toyota</span></span> |<span data-ttu-id="ee97c-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="ee97c-197">**Salida1**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-197">**Output1**:</span></span>

| <span data-ttu-id="ee97c-198">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-198">Make</span></span> | <span data-ttu-id="ee97c-199">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-200">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-200">Honda</span></span> |<span data-ttu-id="ee97c-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-202">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-202">Honda</span></span> |<span data-ttu-id="ee97c-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-204">Toyota</span></span> |<span data-ttu-id="ee97c-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-206">Toyota</span></span> |<span data-ttu-id="ee97c-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-208">Toyota</span></span> |<span data-ttu-id="ee97c-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="ee97c-210">**Salida2**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-210">**Output2**:</span></span>

| <span data-ttu-id="ee97c-211">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-211">Make</span></span> | <span data-ttu-id="ee97c-212">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-212">Time</span></span> | <span data-ttu-id="ee97c-213">Recuento</span><span class="sxs-lookup"><span data-stu-id="ee97c-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-214">Toyota</span></span> |<span data-ttu-id="ee97c-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="ee97c-216">3</span><span class="sxs-lookup"><span data-stu-id="ee97c-216">3</span></span> |

<span data-ttu-id="ee97c-217">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-217">**Solution**:</span></span>

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

<span data-ttu-id="ee97c-218">**Explicación**: la cláusula **INTO** indica a Stream Analytics en cuál de las salidas se escribirán los datos de esta instrucción.</span><span class="sxs-lookup"><span data-stu-id="ee97c-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="ee97c-219">La primera consulta es una transferencia de los datos que se recibe en una salida que denominamos **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="ee97c-220">La segunda consulta hace una agregación y un filtrado simples y envía los resultados a un sistema de alertas descendente.</span><span class="sxs-lookup"><span data-stu-id="ee97c-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="ee97c-221">Tenga en cuenta que también puede reutilizar los resultados de las expresiones de tabla comunes (CTE), como las instrucciones **WITH**, en varias instrucciones de salida.</span><span class="sxs-lookup"><span data-stu-id="ee97c-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="ee97c-222">Esta opción ofrece el beneficio adicional de la apertura de algunos lectores para el origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee97c-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="ee97c-223">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ee97c-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="ee97c-224">Ejemplo de consulta: recuento de valores únicos</span><span class="sxs-lookup"><span data-stu-id="ee97c-224">Query example: Count unique values</span></span>
<span data-ttu-id="ee97c-225">**Descripción**: cuente el número de valores de campo únicos que aparecen en el flujo durante una ventana de tiempo determinada.</span><span class="sxs-lookup"><span data-stu-id="ee97c-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="ee97c-226">Por ejemplo, ¿cuántas marcas de vehículos únicas pasan a través de la cabina de peaje en un intervalo de dos segundos?</span><span class="sxs-lookup"><span data-stu-id="ee97c-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="ee97c-227">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-227">**Input**:</span></span>

| <span data-ttu-id="ee97c-228">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-228">Make</span></span> | <span data-ttu-id="ee97c-229">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-230">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-230">Honda</span></span> |<span data-ttu-id="ee97c-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-232">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-232">Honda</span></span> |<span data-ttu-id="ee97c-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-234">Toyota</span></span> |<span data-ttu-id="ee97c-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-236">Toyota</span></span> |<span data-ttu-id="ee97c-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-238">Toyota</span></span> |<span data-ttu-id="ee97c-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="ee97c-240">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="ee97c-240">**Output:**</span></span>

| <span data-ttu-id="ee97c-241">Recuento</span><span class="sxs-lookup"><span data-stu-id="ee97c-241">Count</span></span> | <span data-ttu-id="ee97c-242">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-243">2</span><span class="sxs-lookup"><span data-stu-id="ee97c-243">2</span></span> |<span data-ttu-id="ee97c-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="ee97c-245">1</span><span class="sxs-lookup"><span data-stu-id="ee97c-245">1</span></span> |<span data-ttu-id="ee97c-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="ee97c-247">**Solución:**</span><span class="sxs-lookup"><span data-stu-id="ee97c-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="ee97c-248">**Explicación:**
** COUNT(DISTINCT Make)** devuelve la cantidad de valores distintos de la columna **Make** dentro de una ventana de tiempo.</span><span class="sxs-lookup"><span data-stu-id="ee97c-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="ee97c-249">Ejemplo de consulta: determinar si un valor ha cambiado</span><span class="sxs-lookup"><span data-stu-id="ee97c-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="ee97c-250">**Descripción**: busque un valor anterior para determinar si es diferente del valor actual.</span><span class="sxs-lookup"><span data-stu-id="ee97c-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="ee97c-251">Por ejemplo, ¿el vehículo anterior de la autopista de peaje es de la misma marca que el actual?</span><span class="sxs-lookup"><span data-stu-id="ee97c-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="ee97c-252">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-252">**Input**:</span></span>

| <span data-ttu-id="ee97c-253">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-253">Make</span></span> | <span data-ttu-id="ee97c-254">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-255">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-255">Honda</span></span> |<span data-ttu-id="ee97c-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-257">Toyota</span></span> |<span data-ttu-id="ee97c-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="ee97c-259">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-259">**Output**:</span></span>

| <span data-ttu-id="ee97c-260">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-260">Make</span></span> | <span data-ttu-id="ee97c-261">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-262">Toyota</span></span> |<span data-ttu-id="ee97c-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="ee97c-264">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="ee97c-265">**Explicación**: use **LAG** para revisar en el flujo de entrada de un evento anterior y obtener el valor **Marca**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="ee97c-266">A continuación, compárelo con el de la **marca** del evento actual y genere la salida del evento si son distintos.</span><span class="sxs-lookup"><span data-stu-id="ee97c-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="ee97c-267">Ejemplo de consulta: búsqueda del primer evento en una ventana</span><span class="sxs-lookup"><span data-stu-id="ee97c-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="ee97c-268">**Descripción**: ¿desea buscar el primer vehículo en un intervalo de cada diez minutos?</span><span class="sxs-lookup"><span data-stu-id="ee97c-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="ee97c-269">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-269">**Input**:</span></span>

| <span data-ttu-id="ee97c-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-270">LicensePlate</span></span> | <span data-ttu-id="ee97c-271">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-271">Make</span></span> | <span data-ttu-id="ee97c-272">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="ee97c-273">DXE 5291</span></span> |<span data-ttu-id="ee97c-274">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-274">Honda</span></span> |<span data-ttu-id="ee97c-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="ee97c-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="ee97c-276">YZK 5704</span></span> |<span data-ttu-id="ee97c-277">Ford</span><span class="sxs-lookup"><span data-stu-id="ee97c-277">Ford</span></span> |<span data-ttu-id="ee97c-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="ee97c-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="ee97c-279">RMV 8282</span></span> |<span data-ttu-id="ee97c-280">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-280">Honda</span></span> |<span data-ttu-id="ee97c-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="ee97c-282">YHN 6970</span></span> |<span data-ttu-id="ee97c-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-283">Toyota</span></span> |<span data-ttu-id="ee97c-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="ee97c-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="ee97c-285">VFE 1616</span></span> |<span data-ttu-id="ee97c-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-286">Toyota</span></span> |<span data-ttu-id="ee97c-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="ee97c-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="ee97c-288">QYF 9358</span></span> |<span data-ttu-id="ee97c-289">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-289">Honda</span></span> |<span data-ttu-id="ee97c-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="ee97c-291">MDR 6128</span></span> |<span data-ttu-id="ee97c-292">BMW</span><span class="sxs-lookup"><span data-stu-id="ee97c-292">BMW</span></span> |<span data-ttu-id="ee97c-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="ee97c-294">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-294">**Output**:</span></span>

| <span data-ttu-id="ee97c-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-295">LicensePlate</span></span> | <span data-ttu-id="ee97c-296">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-296">Make</span></span> | <span data-ttu-id="ee97c-297">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="ee97c-298">DXE 5291</span></span> |<span data-ttu-id="ee97c-299">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-299">Honda</span></span> |<span data-ttu-id="ee97c-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="ee97c-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="ee97c-301">QYF 9358</span></span> |<span data-ttu-id="ee97c-302">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-302">Honda</span></span> |<span data-ttu-id="ee97c-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="ee97c-304">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="ee97c-305">Ahora se va a cambiar el problema y se va a buscar el primer vehículo de una marca concreta en un intervalo de cada diez minutos.</span><span class="sxs-lookup"><span data-stu-id="ee97c-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="ee97c-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-306">LicensePlate</span></span> | <span data-ttu-id="ee97c-307">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-307">Make</span></span> | <span data-ttu-id="ee97c-308">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="ee97c-309">DXE 5291</span></span> |<span data-ttu-id="ee97c-310">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-310">Honda</span></span> |<span data-ttu-id="ee97c-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="ee97c-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="ee97c-312">YZK 5704</span></span> |<span data-ttu-id="ee97c-313">Ford</span><span class="sxs-lookup"><span data-stu-id="ee97c-313">Ford</span></span> |<span data-ttu-id="ee97c-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="ee97c-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="ee97c-315">YHN 6970</span></span> |<span data-ttu-id="ee97c-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-316">Toyota</span></span> |<span data-ttu-id="ee97c-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="ee97c-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="ee97c-318">QYF 9358</span></span> |<span data-ttu-id="ee97c-319">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-319">Honda</span></span> |<span data-ttu-id="ee97c-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="ee97c-321">MDR 6128</span></span> |<span data-ttu-id="ee97c-322">BMW</span><span class="sxs-lookup"><span data-stu-id="ee97c-322">BMW</span></span> |<span data-ttu-id="ee97c-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="ee97c-324">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="ee97c-325">Ejemplo de consulta: búsqueda del último evento en una ventana</span><span class="sxs-lookup"><span data-stu-id="ee97c-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="ee97c-326">**Descripción**: busque el último vehículo en un intervalo de cada diez minutos.</span><span class="sxs-lookup"><span data-stu-id="ee97c-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="ee97c-327">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-327">**Input**:</span></span>

| <span data-ttu-id="ee97c-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-328">LicensePlate</span></span> | <span data-ttu-id="ee97c-329">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-329">Make</span></span> | <span data-ttu-id="ee97c-330">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="ee97c-331">DXE 5291</span></span> |<span data-ttu-id="ee97c-332">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-332">Honda</span></span> |<span data-ttu-id="ee97c-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="ee97c-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="ee97c-334">YZK 5704</span></span> |<span data-ttu-id="ee97c-335">Ford</span><span class="sxs-lookup"><span data-stu-id="ee97c-335">Ford</span></span> |<span data-ttu-id="ee97c-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="ee97c-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="ee97c-337">RMV 8282</span></span> |<span data-ttu-id="ee97c-338">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-338">Honda</span></span> |<span data-ttu-id="ee97c-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="ee97c-340">YHN 6970</span></span> |<span data-ttu-id="ee97c-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-341">Toyota</span></span> |<span data-ttu-id="ee97c-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="ee97c-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="ee97c-343">VFE 1616</span></span> |<span data-ttu-id="ee97c-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-344">Toyota</span></span> |<span data-ttu-id="ee97c-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="ee97c-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="ee97c-346">QYF 9358</span></span> |<span data-ttu-id="ee97c-347">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-347">Honda</span></span> |<span data-ttu-id="ee97c-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="ee97c-349">MDR 6128</span></span> |<span data-ttu-id="ee97c-350">BMW</span><span class="sxs-lookup"><span data-stu-id="ee97c-350">BMW</span></span> |<span data-ttu-id="ee97c-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="ee97c-352">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-352">**Output**:</span></span>

| <span data-ttu-id="ee97c-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-353">LicensePlate</span></span> | <span data-ttu-id="ee97c-354">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-354">Make</span></span> | <span data-ttu-id="ee97c-355">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="ee97c-356">VFE 1616</span></span> |<span data-ttu-id="ee97c-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-357">Toyota</span></span> |<span data-ttu-id="ee97c-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="ee97c-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="ee97c-359">MDR 6128</span></span> |<span data-ttu-id="ee97c-360">BMW</span><span class="sxs-lookup"><span data-stu-id="ee97c-360">BMW</span></span> |<span data-ttu-id="ee97c-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="ee97c-362">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-362">**Solution**:</span></span>

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

<span data-ttu-id="ee97c-363">**Explicación**: hay dos pasos en la consulta.</span><span class="sxs-lookup"><span data-stu-id="ee97c-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="ee97c-364">El primero consiste en buscar la última marca de tiempo en ventanas de diez minutos.</span><span class="sxs-lookup"><span data-stu-id="ee97c-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="ee97c-365">El segundo paso combina los resultados de la primera consulta con el flujo original para buscar eventos que coinciden con las últimas marcas de tiempo en cada ventana.</span><span class="sxs-lookup"><span data-stu-id="ee97c-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="ee97c-366">Ejemplo de consulta: detectar la ausencia de eventos</span><span class="sxs-lookup"><span data-stu-id="ee97c-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="ee97c-367">**Descripción**: compruebe que un flujo no tiene ningún valor que cumpla un criterio determinado.</span><span class="sxs-lookup"><span data-stu-id="ee97c-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="ee97c-368">Por ejemplo, ¿han entrado dos vehículos consecutivos de la misma marca en la autopista de peaje durante los últimos noventa segundos?</span><span class="sxs-lookup"><span data-stu-id="ee97c-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="ee97c-369">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-369">**Input**:</span></span>

| <span data-ttu-id="ee97c-370">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-370">Make</span></span> | <span data-ttu-id="ee97c-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-371">LicensePlate</span></span> | <span data-ttu-id="ee97c-372">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-373">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-373">Honda</span></span> |<span data-ttu-id="ee97c-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="ee97c-374">ABC-123</span></span> |<span data-ttu-id="ee97c-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="ee97c-376">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-376">Honda</span></span> |<span data-ttu-id="ee97c-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="ee97c-377">AAA-999</span></span> |<span data-ttu-id="ee97c-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="ee97c-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-379">Toyota</span></span> |<span data-ttu-id="ee97c-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="ee97c-380">DEF-987</span></span> |<span data-ttu-id="ee97c-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="ee97c-382">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-382">Honda</span></span> |<span data-ttu-id="ee97c-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="ee97c-383">GHI-345</span></span> |<span data-ttu-id="ee97c-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="ee97c-385">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-385">**Output**:</span></span>

| <span data-ttu-id="ee97c-386">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-386">Make</span></span> | <span data-ttu-id="ee97c-387">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-387">Time</span></span> | <span data-ttu-id="ee97c-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="ee97c-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="ee97c-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="ee97c-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="ee97c-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ee97c-391">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-391">Honda</span></span> |<span data-ttu-id="ee97c-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="ee97c-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="ee97c-393">AAA-999</span></span> |<span data-ttu-id="ee97c-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="ee97c-394">ABC-123</span></span> |<span data-ttu-id="ee97c-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="ee97c-396">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-396">**Solution**:</span></span>

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

<span data-ttu-id="ee97c-397">**Explicación**: use **LAG** para revisar en el flujo de entrada de un evento anterior y obtener el valor **Marca**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="ee97c-398">Compárelo con el valor **MARCA** del evento actual y después genere la salida del evento en caso de que los valores sean los mismos.</span><span class="sxs-lookup"><span data-stu-id="ee97c-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="ee97c-399">También puede usar **LAG** para obtener datos sobre el vehículo anterior.</span><span class="sxs-lookup"><span data-stu-id="ee97c-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="ee97c-400">Ejemplo de consulta: detección de la duración entre eventos</span><span class="sxs-lookup"><span data-stu-id="ee97c-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="ee97c-401">**Descripción**: busque la duración de un evento determinado.</span><span class="sxs-lookup"><span data-stu-id="ee97c-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="ee97c-402">Por ejemplo, dada una secuencia de clics de web, determine el tiempo invertido en una característica.</span><span class="sxs-lookup"><span data-stu-id="ee97c-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="ee97c-403">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-403">**Input**:</span></span>  

| <span data-ttu-id="ee97c-404">Usuario</span><span class="sxs-lookup"><span data-stu-id="ee97c-404">User</span></span> | <span data-ttu-id="ee97c-405">Característica</span><span class="sxs-lookup"><span data-stu-id="ee97c-405">Feature</span></span> | <span data-ttu-id="ee97c-406">Evento</span><span class="sxs-lookup"><span data-stu-id="ee97c-406">Event</span></span> | <span data-ttu-id="ee97c-407">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="ee97c-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="ee97c-408">RightMenu</span></span> |<span data-ttu-id="ee97c-409">Iniciar</span><span class="sxs-lookup"><span data-stu-id="ee97c-409">Start</span></span> |<span data-ttu-id="ee97c-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="ee97c-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="ee97c-411">RightMenu</span></span> |<span data-ttu-id="ee97c-412">End</span><span class="sxs-lookup"><span data-stu-id="ee97c-412">End</span></span> |<span data-ttu-id="ee97c-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="ee97c-414">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-414">**Output**:</span></span>  

| <span data-ttu-id="ee97c-415">Usuario</span><span class="sxs-lookup"><span data-stu-id="ee97c-415">User</span></span> | <span data-ttu-id="ee97c-416">Característica</span><span class="sxs-lookup"><span data-stu-id="ee97c-416">Feature</span></span> | <span data-ttu-id="ee97c-417">Duración</span><span class="sxs-lookup"><span data-stu-id="ee97c-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="ee97c-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="ee97c-418">RightMenu</span></span> |<span data-ttu-id="ee97c-419">7</span><span class="sxs-lookup"><span data-stu-id="ee97c-419">7</span></span> |

<span data-ttu-id="ee97c-420">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="ee97c-421">**Explicación**: use la función **LAST** para recuperar el último valor **TIME** en el que el tipo de evento era **Start**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="ee97c-422">La función **LAST** usa **PARTITION BY [user]** para indicar que el resultado se calcula por usuario único.</span><span class="sxs-lookup"><span data-stu-id="ee97c-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="ee97c-423">La consulta tiene un umbral máximo de una hora para el intervalo de tiempo entre eventos **Start** y **Stop**, pero se puede configurar según sea necesario **(LIMIT DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="ee97c-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="ee97c-424">Ejemplo de consulta: detección de la duración de una condición</span><span class="sxs-lookup"><span data-stu-id="ee97c-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="ee97c-425">**Descripción**: averigüe la duración de una condición.</span><span class="sxs-lookup"><span data-stu-id="ee97c-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="ee97c-426">Por ejemplo, supongamos que, por error, todos los vehículos tienen un peso incorrecto (por encima de 20 000 libras).</span><span class="sxs-lookup"><span data-stu-id="ee97c-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="ee97c-427">Queremos calcular la duración del error.</span><span class="sxs-lookup"><span data-stu-id="ee97c-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="ee97c-428">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-428">**Input**:</span></span>

| <span data-ttu-id="ee97c-429">Asegúrese</span><span class="sxs-lookup"><span data-stu-id="ee97c-429">Make</span></span> | <span data-ttu-id="ee97c-430">Hora</span><span class="sxs-lookup"><span data-stu-id="ee97c-430">Time</span></span> | <span data-ttu-id="ee97c-431">Peso</span><span class="sxs-lookup"><span data-stu-id="ee97c-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-432">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-432">Honda</span></span> |<span data-ttu-id="ee97c-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="ee97c-434">2000</span><span class="sxs-lookup"><span data-stu-id="ee97c-434">2000</span></span> |
| <span data-ttu-id="ee97c-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-435">Toyota</span></span> |<span data-ttu-id="ee97c-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="ee97c-437">25000</span><span class="sxs-lookup"><span data-stu-id="ee97c-437">25000</span></span> |
| <span data-ttu-id="ee97c-438">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-438">Honda</span></span> |<span data-ttu-id="ee97c-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="ee97c-440">26000</span><span class="sxs-lookup"><span data-stu-id="ee97c-440">26000</span></span> |
| <span data-ttu-id="ee97c-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-441">Toyota</span></span> |<span data-ttu-id="ee97c-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="ee97c-443">25000</span><span class="sxs-lookup"><span data-stu-id="ee97c-443">25000</span></span> |
| <span data-ttu-id="ee97c-444">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-444">Honda</span></span> |<span data-ttu-id="ee97c-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="ee97c-446">26000</span><span class="sxs-lookup"><span data-stu-id="ee97c-446">26000</span></span> |
| <span data-ttu-id="ee97c-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-447">Toyota</span></span> |<span data-ttu-id="ee97c-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="ee97c-449">25000</span><span class="sxs-lookup"><span data-stu-id="ee97c-449">25000</span></span> |
| <span data-ttu-id="ee97c-450">Honda</span><span class="sxs-lookup"><span data-stu-id="ee97c-450">Honda</span></span> |<span data-ttu-id="ee97c-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="ee97c-452">26000</span><span class="sxs-lookup"><span data-stu-id="ee97c-452">26000</span></span> |
| <span data-ttu-id="ee97c-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="ee97c-453">Toyota</span></span> |<span data-ttu-id="ee97c-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="ee97c-455">2000</span><span class="sxs-lookup"><span data-stu-id="ee97c-455">2000</span></span> |

<span data-ttu-id="ee97c-456">**Salida**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-456">**Output**:</span></span>

| <span data-ttu-id="ee97c-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="ee97c-457">StartFault</span></span> | <span data-ttu-id="ee97c-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="ee97c-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="ee97c-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="ee97c-461">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-461">**Solution**:</span></span>

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

<span data-ttu-id="ee97c-462">**Explicación**: use **LAG** para ver el flujo de entrada que se produjo durante veinticuatro horas y busque instancias donde**StartFault** y **StopFault** superan el peso de <20 000.</span><span class="sxs-lookup"><span data-stu-id="ee97c-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="ee97c-463">Ejemplo de consulta: rellenar los valores que faltan</span><span class="sxs-lookup"><span data-stu-id="ee97c-463">Query example: Fill missing values</span></span>
<span data-ttu-id="ee97c-464">**Descripción**: para la transmisión de eventos con valores que faltan, genere una transmisión de eventos con intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="ee97c-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="ee97c-465">Por ejemplo, genere un evento cada cinco segundos que notifique el punto de datos visto más recientemente.</span><span class="sxs-lookup"><span data-stu-id="ee97c-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="ee97c-466">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-466">**Input**:</span></span>

| <span data-ttu-id="ee97c-467">t</span><span class="sxs-lookup"><span data-stu-id="ee97c-467">t</span></span> | <span data-ttu-id="ee97c-468">value</span><span class="sxs-lookup"><span data-stu-id="ee97c-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="ee97c-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="ee97c-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="ee97c-470">1</span><span class="sxs-lookup"><span data-stu-id="ee97c-470">1</span></span> |
| <span data-ttu-id="ee97c-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="ee97c-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="ee97c-472">2</span><span class="sxs-lookup"><span data-stu-id="ee97c-472">2</span></span> |
| <span data-ttu-id="ee97c-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="ee97c-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="ee97c-474">3</span><span class="sxs-lookup"><span data-stu-id="ee97c-474">3</span></span> |
| <span data-ttu-id="ee97c-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="ee97c-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="ee97c-476">4</span><span class="sxs-lookup"><span data-stu-id="ee97c-476">4</span></span> |
| <span data-ttu-id="ee97c-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="ee97c-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="ee97c-478">5</span><span class="sxs-lookup"><span data-stu-id="ee97c-478">5</span></span> |
| <span data-ttu-id="ee97c-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="ee97c-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="ee97c-480">6</span><span class="sxs-lookup"><span data-stu-id="ee97c-480">6</span></span> |

<span data-ttu-id="ee97c-481">**Salida (10 primeras filas)**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="ee97c-482">windowend</span><span class="sxs-lookup"><span data-stu-id="ee97c-482">windowend</span></span> | <span data-ttu-id="ee97c-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="ee97c-483">lastevent.t</span></span> | <span data-ttu-id="ee97c-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="ee97c-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee97c-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="ee97c-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="ee97c-487">1</span><span class="sxs-lookup"><span data-stu-id="ee97c-487">1</span></span> |
| <span data-ttu-id="ee97c-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="ee97c-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="ee97c-490">2</span><span class="sxs-lookup"><span data-stu-id="ee97c-490">2</span></span> |
| <span data-ttu-id="ee97c-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="ee97c-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="ee97c-493">3</span><span class="sxs-lookup"><span data-stu-id="ee97c-493">3</span></span> |
| <span data-ttu-id="ee97c-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="ee97c-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="ee97c-496">4</span><span class="sxs-lookup"><span data-stu-id="ee97c-496">4</span></span> |
| <span data-ttu-id="ee97c-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="ee97c-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="ee97c-499">4</span><span class="sxs-lookup"><span data-stu-id="ee97c-499">4</span></span> |
| <span data-ttu-id="ee97c-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="ee97c-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="ee97c-502">4</span><span class="sxs-lookup"><span data-stu-id="ee97c-502">4</span></span> |
| <span data-ttu-id="ee97c-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="ee97c-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="ee97c-505">5</span><span class="sxs-lookup"><span data-stu-id="ee97c-505">5</span></span> |
| <span data-ttu-id="ee97c-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="ee97c-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="ee97c-508">6</span><span class="sxs-lookup"><span data-stu-id="ee97c-508">6</span></span> |
| <span data-ttu-id="ee97c-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="ee97c-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="ee97c-511">6</span><span class="sxs-lookup"><span data-stu-id="ee97c-511">6</span></span> |
| <span data-ttu-id="ee97c-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="ee97c-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="ee97c-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="ee97c-514">6</span><span class="sxs-lookup"><span data-stu-id="ee97c-514">6</span></span> |

<span data-ttu-id="ee97c-515">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="ee97c-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="ee97c-516">**Explicación**: esta consulta genera eventos cada cinco segundos y genera como resultado el último evento que se recibió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ee97c-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="ee97c-517">La duración de la [ventana de salto](https://msdn.microsoft.com/library/dn835041.aspx "ventana de salto - Azure Stream Analytics") determina hasta cuándo se remontará la consulta para encontrar el evento más reciente (en este ejemplo, trescientos segundos).</span><span class="sxs-lookup"><span data-stu-id="ee97c-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="ee97c-518">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="ee97c-518">Get help</span></span>
<span data-ttu-id="ee97c-519">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ee97c-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee97c-520">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee97c-520">Next steps</span></span>
* [<span data-ttu-id="ee97c-521">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee97c-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ee97c-522">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee97c-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ee97c-523">Escalación de trabajos de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee97c-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ee97c-524">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee97c-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ee97c-525">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee97c-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

