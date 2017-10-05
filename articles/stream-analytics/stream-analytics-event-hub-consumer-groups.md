---
title: "Depuración de Azure Stream Analytics con receptores de Event Hubs | Microsoft Docs"
description: "Prácticas recomendadas de consulta para la consideración de grupos de consumidores de Event Hubs en trabajos de Stream Analytics."
keywords: "límite de centro de eventos, grupo de consumidores"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="eb2d9-104">Depuración de Azure Stream Analytics con receptores de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="eb2d9-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="eb2d9-105">Puede usar Azure Event Hubs en Azure Stream Analytics para ingerir o extraer datos de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="eb2d9-106">Una práctica recomendada para usar Event Hubs es usar varios grupos de consumidor para garantizar la escalabilidad del trabajo.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="eb2d9-107">Una razón es que el número de lectores en el trabajo de Stream Analytics para una entrada específica afecta a la cantidad de lectores en un grupo de consumidores único.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="eb2d9-108">El número exacto de destinatarios se basa en los detalles de implementación interna para la lógica de la topología de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="eb2d9-109">El número de destinatarios no se expone externamente.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="eb2d9-110">El número de lectores puede cambiar a la hora de inicio del trabajo o durante las actualizaciones del trabajo.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="eb2d9-111">Cuando el número de lectores cambia durante una actualización de trabajo, se escriben advertencias transitorias en registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="eb2d9-112">Los trabajos de Stream Analytics se recuperan automáticamente de estos problemas transitorios.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="eb2d9-113">El número de lectores por partición supera el límite de Event Hubs de cinco</span><span class="sxs-lookup"><span data-stu-id="eb2d9-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="eb2d9-114">Los escenarios en los que el número de lectores por partición supera el límite de Event Hubs de cinco incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="eb2d9-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="eb2d9-115">Varias instrucciones SELECT: si usa varias instrucciones SELECT que hacen referencia a la **misma** entrada de centro de eventos, cada instrucción SELECT provoca que se cree un nuevo destinatario.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="eb2d9-116">UNION: cuando se utiliza UNION, es posible tener varias entradas que hacen referencia al **mismo** centro de eventos y grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="eb2d9-117">SELF JOIN: cuando se usa una operación SELF JOIN, es posible hacer referencia al **mismo** centro de eventos varias veces.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="eb2d9-118">Solución</span><span class="sxs-lookup"><span data-stu-id="eb2d9-118">Solution</span></span>

<span data-ttu-id="eb2d9-119">Las siguientes prácticas recomendadas pueden ayudar a reducir los escenarios en los que el número de lectores por partición supera el límite de Event Hubs de cinco.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="eb2d9-120">División de la consulta en varios pasos mediante una cláusula WITH</span><span class="sxs-lookup"><span data-stu-id="eb2d9-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="eb2d9-121">La cláusula WITH especifica un conjunto de resultados con nombre temporal al que se puede hacer referencia mediante una cláusula FROM en la consulta.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="eb2d9-122">Defina la cláusula WITH en el ámbito de ejecución de una única instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="eb2d9-123">Por ejemplo, en lugar de esta consulta:</span><span class="sxs-lookup"><span data-stu-id="eb2d9-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="eb2d9-124">Utilice esta consulta:</span><span class="sxs-lookup"><span data-stu-id="eb2d9-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="eb2d9-125">Asegúrese de que las entradas se enlazan a grupos de consumidores diferentes</span><span class="sxs-lookup"><span data-stu-id="eb2d9-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="eb2d9-126">Para las consultas en las que hay conectadas tres o más entradas al mismo grupo de consumidores de Event Hubs, cree grupos de consumidores independientes.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="eb2d9-127">Esto requiere la creación de entradas de Stream Analytics adicionales.</span><span class="sxs-lookup"><span data-stu-id="eb2d9-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="eb2d9-128">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="eb2d9-128">Get help</span></span>
<span data-ttu-id="eb2d9-129">Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="eb2d9-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb2d9-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb2d9-130">Next steps</span></span>
* [<span data-ttu-id="eb2d9-131">¿Qué es Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="eb2d9-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="eb2d9-132">Introducción a Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb2d9-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="eb2d9-133">Escalado de trabajos de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb2d9-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="eb2d9-134">Referencia de lenguaje de consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb2d9-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="eb2d9-135">Referencia de API de REST de administración de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb2d9-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
