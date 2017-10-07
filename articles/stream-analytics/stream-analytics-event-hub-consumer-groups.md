---
title: "aaaDebug análisis de transmisiones de Azure con receptores de eventos de base de datos central | Documentos de Microsoft"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="69f5a-104">Depuración de Azure Stream Analytics con receptores de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="69f5a-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="69f5a-105">Puede usar los centros de eventos de Azure en los datos de análisis de transmisiones de Azure tooingest o la salida de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="69f5a-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="69f5a-106">Una práctica recomendada para el uso de los centros de eventos es toouse varios grupos de consumidores, escalabilidad de trabajo tooensure.</span><span class="sxs-lookup"><span data-stu-id="69f5a-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="69f5a-107">Una razón es que número Hola de lectores en el trabajo de análisis de transmisiones de Hola para una entrada específica afecta al número de Hola de lectores en un grupo único consumidor.</span><span class="sxs-lookup"><span data-stu-id="69f5a-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="69f5a-108">número exacto de Hola de destinatarios se basa en los detalles de implementación internos para la lógica de la topología de ampliación de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f5a-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="69f5a-109">número de Hola de destinatarios no se expone externamente.</span><span class="sxs-lookup"><span data-stu-id="69f5a-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="69f5a-110">número de Hola de lectores puede cambiar en tiempo de inicio del trabajo de Hola o durante las actualizaciones del trabajo.</span><span class="sxs-lookup"><span data-stu-id="69f5a-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="69f5a-111">Cuando se cambia el número de Hola de lectores durante la actualización del trabajo, las advertencias transitorias se escriben registros tooaudit.</span><span class="sxs-lookup"><span data-stu-id="69f5a-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="69f5a-112">Los trabajos de Stream Analytics se recuperan automáticamente de estos problemas transitorios.</span><span class="sxs-lookup"><span data-stu-id="69f5a-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="69f5a-113">El número de lectores por partición supera el límite de Event Hubs de cinco</span><span class="sxs-lookup"><span data-stu-id="69f5a-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="69f5a-114">Escenarios de en qué Hola número de lectores por partición supera el límite de los centros de eventos de Hola de cinco Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="69f5a-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="69f5a-115">Varias instrucciones SELECT: si usa varias instrucciones SELECT que hacen referencia demasiado**mismo** concentrador de eventos de entrada, cada instrucción SELECT hace que un nuevo toobe de receptor creado.</span><span class="sxs-lookup"><span data-stu-id="69f5a-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="69f5a-116">Unión: Cuando se utiliza una unión, es posible toohave varias entradas que hacen referencia toohello **mismo** grupo de concentrador y consumidor de eventos.</span><span class="sxs-lookup"><span data-stu-id="69f5a-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="69f5a-117">AUTOCOMBINACIÓN: Cuando se usa una operación JOIN de AUTOSERVICIO, es posible toorefer toohello **mismo** concentrador de eventos varias veces.</span><span class="sxs-lookup"><span data-stu-id="69f5a-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="69f5a-118">Solución</span><span class="sxs-lookup"><span data-stu-id="69f5a-118">Solution</span></span>

<span data-ttu-id="69f5a-119">Hello siguientes prácticas recomendadas pueden ayudar a mitigar escenarios en qué Hola número de lectores por partición supera el límite de los centros de eventos de Hola de cinco.</span><span class="sxs-lookup"><span data-stu-id="69f5a-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="69f5a-120">División de la consulta en varios pasos mediante una cláusula WITH</span><span class="sxs-lookup"><span data-stu-id="69f5a-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="69f5a-121">cláusula WITH de Hello especifica un conjunto de resultados temporal indicado que puede hacer referencia a una cláusula FROM en consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="69f5a-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="69f5a-122">Definir cláusula WITH de hello en el ámbito de ejecución de Hola de una sola instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="69f5a-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="69f5a-123">Por ejemplo, en lugar de esta consulta:</span><span class="sxs-lookup"><span data-stu-id="69f5a-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="69f5a-124">Utilice esta consulta:</span><span class="sxs-lookup"><span data-stu-id="69f5a-124">Use this query:</span></span>

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="69f5a-125">Asegúrese de que las entradas enlazan grupos de consumidores toodifferent</span><span class="sxs-lookup"><span data-stu-id="69f5a-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="69f5a-126">Para las consultas en el que tres o más entradas están conectado toohello mismo consumidor de los centros de eventos de grupo, cree grupos de consumidores independientes.</span><span class="sxs-lookup"><span data-stu-id="69f5a-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="69f5a-127">Esto requiere la creación de hello de entradas de análisis de transmisiones adicionales.</span><span class="sxs-lookup"><span data-stu-id="69f5a-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="69f5a-128">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="69f5a-128">Get help</span></span>
<span data-ttu-id="69f5a-129">Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="69f5a-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69f5a-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69f5a-130">Next steps</span></span>
* [<span data-ttu-id="69f5a-131">Introducción tooStream análisis</span><span class="sxs-lookup"><span data-stu-id="69f5a-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="69f5a-132">Introducción a Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="69f5a-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="69f5a-133">Escalado de trabajos de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="69f5a-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="69f5a-134">Referencia de lenguaje de consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="69f5a-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="69f5a-135">Referencia de API de REST de administración de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="69f5a-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
