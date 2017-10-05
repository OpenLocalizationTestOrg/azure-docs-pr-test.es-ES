---
title: Uso del procesamiento por lotes para mejorar el rendimiento de las aplicaciones de Base de datos SQL de Azure
description: "El tema proporciona evidencia de que el procesamiento por lotes de las operaciones de base de datos mejora en gran medida la velocidad y la escalabilidad de las aplicaciones de Base de datos SQL de Azure. Aunque estas técnicas de procesamiento por lotes funcionan para cualquier base de datos de SQL Server, el artículo se centra en Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 22cff47444306e599325ba3035d83a0266d69c72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-batching-to-improve-sql-database-application-performance"></a><span data-ttu-id="cc532-104">Uso del procesamiento por lotes para mejorar el rendimiento de las aplicaciones de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cc532-104">How to use batching to improve SQL Database application performance</span></span>
<span data-ttu-id="cc532-105">El procesamiento de operaciones por lotes para Base de datos SQL de Azure mejora notablemente el rendimiento y la escalabilidad de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span></span> <span data-ttu-id="cc532-106">Para comprender las ventajas, la primera parte de este artículo trata algunos resultados de pruebas de ejemplo que comparan solicitudes por lotes y secuenciales a una base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span></span> <span data-ttu-id="cc532-107">El resto del artículo muestra las técnicas, los escenarios y las consideraciones para ayudarlo a usar el procesamiento por lotes correctamente en las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="cc532-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="cc532-108">¿Por qué es el procesamiento por lotes importante para Base de datos SQL?</span><span class="sxs-lookup"><span data-stu-id="cc532-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="cc532-109">El procesamiento por lotes de las llamadas a un servicio remoto es una estrategia conocida para aumentar el rendimiento y la escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="cc532-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="cc532-110">Existen costos fijos de procesamiento para cualquier interacción con un servicio remoto, como la serialización, la transferencia de red y la deserialización.</span><span class="sxs-lookup"><span data-stu-id="cc532-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="cc532-111">El empaquetado de muchas transacciones diferentes en un único lote minimiza estos costos.</span><span class="sxs-lookup"><span data-stu-id="cc532-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="cc532-112">En este artículo, vamos a examinar las diversas estrategias y escenarios de procesamiento por lotes para Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="cc532-113">Aunque estas estrategias también son importantes para las aplicaciones locales que usan SQL Server, existen varias razones para destacar el uso del procesamiento por lotes para Base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="cc532-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span></span>

* <span data-ttu-id="cc532-114">Potencialmente la latencia de red al acceder a Base de datos SQL es mayor, sobre todo si accede a Base de datos de SQL desde fuera del mismo centro de datos de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc532-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="cc532-115">Las características para varios inquilinos de Base de datos SQL suponen que la eficacia de la capa de acceso a datos se correlacione con la escalabilidad general de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span></span> <span data-ttu-id="cc532-116">Base de datos SQL debe impedir que un solo usuario o inquilino monopolice los recursos de la base de datos en detrimento de los demás inquilinos.</span><span class="sxs-lookup"><span data-stu-id="cc532-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span></span> <span data-ttu-id="cc532-117">En respuesta a un uso superior a las cuotas predefinidas, Base de datos SQL puede reducir el rendimiento o responder con excepciones de limitación.</span><span class="sxs-lookup"><span data-stu-id="cc532-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="cc532-118">Las soluciones eficientes, como el procesamiento por lotes, permiten que haga más trabajo en Base de datos SQL antes de alcanzar estos límites.</span><span class="sxs-lookup"><span data-stu-id="cc532-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="cc532-119">Además, el procesamiento por lotes es efectivo para las arquitecturas que usan varias bases de datos (particionamiento).</span><span class="sxs-lookup"><span data-stu-id="cc532-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="cc532-120">La eficacia de su interacción con cada unidad de base de datos sigue siendo un factor clave para la escalabilidad global.</span><span class="sxs-lookup"><span data-stu-id="cc532-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="cc532-121">Una de las ventajas del uso de Base de datos SQL es que no es necesario administrar los servidores que hospedan la base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span></span> <span data-ttu-id="cc532-122">Sin embargo, esta infraestructura administrada conlleva también que se deban considerar las optimizaciones de la base de datos de manera diferente.</span><span class="sxs-lookup"><span data-stu-id="cc532-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span></span> <span data-ttu-id="cc532-123">Ya no puede intentar mejorar la infraestructura de hardware o de red de la base de datos,</span><span class="sxs-lookup"><span data-stu-id="cc532-123">You can no longer look to improve the database hardware or network infrastructure.</span></span> <span data-ttu-id="cc532-124">porque Microsoft Azure controla esos entornos.</span><span class="sxs-lookup"><span data-stu-id="cc532-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="cc532-125">El principal aspecto que puede controlar es cómo la aplicación interactúa con Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-125">The main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="cc532-126">El procesamiento por lotes es una de estas optimizaciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="cc532-127">En la primera parte del artículo, se examinan diversas técnicas de procesamiento por lotes para aplicaciones .NET que usan Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="cc532-128">En las dos últimas secciones, se explican las instrucciones y los escenarios de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-128">The last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="cc532-129">Estrategias de procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="cc532-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="cc532-130">Nota sobre los tiempos resultantes en este tema</span><span class="sxs-lookup"><span data-stu-id="cc532-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="cc532-131">Los resultados no sirven para pruebas comparativas, sino que están diseñados para mostrar el **rendimiento relativo**.</span><span class="sxs-lookup"><span data-stu-id="cc532-131">Results are not benchmarks but are meant to show **relative performance**.</span></span> <span data-ttu-id="cc532-132">Los tiempos se basan en un promedio de un mínimo de 10 series de pruebas.</span><span class="sxs-lookup"><span data-stu-id="cc532-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="cc532-133">Las operaciones son inserciones en una tabla vacía.</span><span class="sxs-lookup"><span data-stu-id="cc532-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="cc532-134">Estas pruebas se midieron antes de V12 y no se corresponden necesariamente con el rendimiento que podría observar en una base de datos V12 con los nuevos [niveles de servicio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="cc532-134">These tests were measured pre-V12, and they do not necessarily correspond to throughput that you might experience in a V12 database using the new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="cc532-135">La ventaja relativa de la técnica de procesamiento por lotes debería ser semejante.</span><span class="sxs-lookup"><span data-stu-id="cc532-135">The relative benefit of the batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="cc532-136">Transacciones</span><span class="sxs-lookup"><span data-stu-id="cc532-136">Transactions</span></span>
<span data-ttu-id="cc532-137">Parece extraño comenzar una revisión del procesamiento por lotes hablando de transacciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-137">It seems strange to begin a review of batching by discussing transactions.</span></span> <span data-ttu-id="cc532-138">Pero el uso de transacciones del lado cliente surte un sutil efecto de procesamiento por lotes del lado servidor que mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="cc532-139">Además, las transacciones se pueden agregar con unas pocas líneas de código, lo que proporciona una forma rápida de mejorar el rendimiento de las operaciones secuenciales.</span><span class="sxs-lookup"><span data-stu-id="cc532-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span></span>

<span data-ttu-id="cc532-140">Observe el siguiente código C# que contiene una secuencia de operaciones de inserción y actualización en una tabla sencilla.</span><span class="sxs-lookup"><span data-stu-id="cc532-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="cc532-141">El siguiente código ADO.NET realiza estas operaciones de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="cc532-141">The following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="cc532-142">La mejor manera de optimizar este código es implementar algún tipo de procesamiento por lotes del lado cliente para estas llamadas.</span><span class="sxs-lookup"><span data-stu-id="cc532-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span></span> <span data-ttu-id="cc532-143">Pero hay una forma sencilla de aumentar el rendimiento de este código simplemente encapsulando la secuencia de llamadas en una transacción.</span><span class="sxs-lookup"><span data-stu-id="cc532-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span></span> <span data-ttu-id="cc532-144">Este es el mismo código que usa una transacción.</span><span class="sxs-lookup"><span data-stu-id="cc532-144">Here is the same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="cc532-145">Realmente, se usan transacciones en ambos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="cc532-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="cc532-146">En el primer ejemplo, cada llamada individual es una transacción implícita.</span><span class="sxs-lookup"><span data-stu-id="cc532-146">In the first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="cc532-147">En el segundo ejemplo, una transacción explícita encapsula todas las llamadas.</span><span class="sxs-lookup"><span data-stu-id="cc532-147">In the second example, an explicit transaction wraps all of the calls.</span></span> <span data-ttu-id="cc532-148">Según la documentación del [registro de transacciones de escritura anticipada](https://msdn.microsoft.com/library/ms186259.aspx), las entradas del registro se vacían en el disco cuando se confirma la transacción.</span><span class="sxs-lookup"><span data-stu-id="cc532-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span></span> <span data-ttu-id="cc532-149">Por lo tanto, al incluir más llamadas en una transacción, la escritura en el registro de transacciones se puede retrasar hasta que se confirma la transacción.</span><span class="sxs-lookup"><span data-stu-id="cc532-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span></span> <span data-ttu-id="cc532-150">En efecto, está habilitando el procesamiento por lotes para las escrituras en el registro de transacciones del servidor.</span><span class="sxs-lookup"><span data-stu-id="cc532-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span></span>

<span data-ttu-id="cc532-151">En la tabla siguiente se muestran algunos resultados de pruebas ad hoc.</span><span class="sxs-lookup"><span data-stu-id="cc532-151">The following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="cc532-152">En las pruebas se realizaron las mismas inserciones secuenciales con y sin transacciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-152">The tests performed the same sequential inserts with and without transactions.</span></span> <span data-ttu-id="cc532-153">Para obtener más perspectiva, el primer conjunto de pruebas se ejecutó de forma remota de un equipo portátil a la base de datos de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc532-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span></span> <span data-ttu-id="cc532-154">El segundo conjunto de pruebas se ejecutó de un servicio en la nube y una base de datos que residían en el mismo centro de datos de Microsoft Azure (Oeste de EE. UU.).</span><span class="sxs-lookup"><span data-stu-id="cc532-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="cc532-155">En la tabla siguiente se muestra la duración en milisegundos de las inserciones secuenciales con y sin transacciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="cc532-156">**De local a Azure**:</span><span class="sxs-lookup"><span data-stu-id="cc532-156">**On-Premises to Azure**:</span></span>

| <span data-ttu-id="cc532-157">Operaciones</span><span class="sxs-lookup"><span data-stu-id="cc532-157">Operations</span></span> | <span data-ttu-id="cc532-158">Ninguna transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-158">No Transaction (ms)</span></span> | <span data-ttu-id="cc532-159">Transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc532-160">1</span><span class="sxs-lookup"><span data-stu-id="cc532-160">1</span></span> |<span data-ttu-id="cc532-161">130</span><span class="sxs-lookup"><span data-stu-id="cc532-161">130</span></span> |<span data-ttu-id="cc532-162">402</span><span class="sxs-lookup"><span data-stu-id="cc532-162">402</span></span> |
| <span data-ttu-id="cc532-163">10</span><span class="sxs-lookup"><span data-stu-id="cc532-163">10</span></span> |<span data-ttu-id="cc532-164">1208</span><span class="sxs-lookup"><span data-stu-id="cc532-164">1208</span></span> |<span data-ttu-id="cc532-165">1226</span><span class="sxs-lookup"><span data-stu-id="cc532-165">1226</span></span> |
| <span data-ttu-id="cc532-166">100</span><span class="sxs-lookup"><span data-stu-id="cc532-166">100</span></span> |<span data-ttu-id="cc532-167">12662</span><span class="sxs-lookup"><span data-stu-id="cc532-167">12662</span></span> |<span data-ttu-id="cc532-168">10395</span><span class="sxs-lookup"><span data-stu-id="cc532-168">10395</span></span> |
| <span data-ttu-id="cc532-169">1000</span><span class="sxs-lookup"><span data-stu-id="cc532-169">1000</span></span> |<span data-ttu-id="cc532-170">128852</span><span class="sxs-lookup"><span data-stu-id="cc532-170">128852</span></span> |<span data-ttu-id="cc532-171">102917</span><span class="sxs-lookup"><span data-stu-id="cc532-171">102917</span></span> |

<span data-ttu-id="cc532-172">**De Azure a Azure (mismo centro de datos)**:</span><span class="sxs-lookup"><span data-stu-id="cc532-172">**Azure to Azure (same datacenter)**:</span></span>

| <span data-ttu-id="cc532-173">Operaciones</span><span class="sxs-lookup"><span data-stu-id="cc532-173">Operations</span></span> | <span data-ttu-id="cc532-174">Ninguna transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-174">No Transaction (ms)</span></span> | <span data-ttu-id="cc532-175">Transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc532-176">1</span><span class="sxs-lookup"><span data-stu-id="cc532-176">1</span></span> |<span data-ttu-id="cc532-177">21</span><span class="sxs-lookup"><span data-stu-id="cc532-177">21</span></span> |<span data-ttu-id="cc532-178">26</span><span class="sxs-lookup"><span data-stu-id="cc532-178">26</span></span> |
| <span data-ttu-id="cc532-179">10</span><span class="sxs-lookup"><span data-stu-id="cc532-179">10</span></span> |<span data-ttu-id="cc532-180">220</span><span class="sxs-lookup"><span data-stu-id="cc532-180">220</span></span> |<span data-ttu-id="cc532-181">56</span><span class="sxs-lookup"><span data-stu-id="cc532-181">56</span></span> |
| <span data-ttu-id="cc532-182">100</span><span class="sxs-lookup"><span data-stu-id="cc532-182">100</span></span> |<span data-ttu-id="cc532-183">2145</span><span class="sxs-lookup"><span data-stu-id="cc532-183">2145</span></span> |<span data-ttu-id="cc532-184">341</span><span class="sxs-lookup"><span data-stu-id="cc532-184">341</span></span> |
| <span data-ttu-id="cc532-185">1000</span><span class="sxs-lookup"><span data-stu-id="cc532-185">1000</span></span> |<span data-ttu-id="cc532-186">21479</span><span class="sxs-lookup"><span data-stu-id="cc532-186">21479</span></span> |<span data-ttu-id="cc532-187">2756</span><span class="sxs-lookup"><span data-stu-id="cc532-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="cc532-188">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="cc532-188">Results are not benchmarks.</span></span> <span data-ttu-id="cc532-189">Consulte la [nota sobre los tiempos resultantes en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="cc532-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cc532-190">A partir de los resultados de las pruebas anteriores, encapsular una única operación en una transacción en realidad reduce el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="cc532-191">Pero a medida que aumente el número de operaciones dentro de una única transacción, la mejora del rendimiento se vuelve más marcada.</span><span class="sxs-lookup"><span data-stu-id="cc532-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span></span> <span data-ttu-id="cc532-192">La diferencia de rendimiento también es más apreciable cuando todas las operaciones se producen dentro del centro de datos de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc532-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span></span> <span data-ttu-id="cc532-193">La mayor latencia existente cuando se usa Base de datos de SQL desde fuera del centro de datos de Microsoft Azure contrarresta la ganancia de rendimiento por el uso de transacciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span></span>

<span data-ttu-id="cc532-194">Aunque el uso de transacciones puede aumentar el rendimiento, siga [respetando las prácticas recomendadas para las transacciones y las conexiones](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc532-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="cc532-195">Mantenga la transacción lo más corta posible y cierre la conexión con la base de datos una vez finalizado el trabajo.</span><span class="sxs-lookup"><span data-stu-id="cc532-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span></span> <span data-ttu-id="cc532-196">La instrucción using del ejemplo anterior garantiza que la conexión se cierre cuando finalice el bloque de código subsiguiente.</span><span class="sxs-lookup"><span data-stu-id="cc532-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span></span>

<span data-ttu-id="cc532-197">El ejemplo anterior muestra que puede agregar una transacción local a cualquier código ADO.NET con dos líneas.</span><span class="sxs-lookup"><span data-stu-id="cc532-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span></span> <span data-ttu-id="cc532-198">Las transacciones ofrecen una forma rápida de mejorar el rendimiento del código que realiza operaciones secuenciales de inserción, actualización y eliminación.</span><span class="sxs-lookup"><span data-stu-id="cc532-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="cc532-199">Sin embargo, para lograr el máximo rendimiento, podría cambiar aún más el código para aprovechar las ventajas del procesamiento por lotes del lado cliente, como los parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="cc532-200">Para obtener más información acerca de las transacciones en ADO.NET, consulte [Transacciones locales](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="cc532-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="cc532-201">Parámetros con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="cc532-201">Table-valued parameters</span></span>
<span data-ttu-id="cc532-202">Los parámetros con valores de tabla admiten tipos de tabla definidos por el usuario como parámetros en instrucciones Transact-SQL, procedimientos almacenados y funciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="cc532-203">Esta técnica de procesamiento por lotes del lado cliente permite enviar varias filas de datos dentro del parámetro con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span></span> <span data-ttu-id="cc532-204">Para usar parámetros con valores de tabla, primero debe definir un tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-204">To use table-valued parameters, first define a table type.</span></span> <span data-ttu-id="cc532-205">La siguiente instrucción Transact-SQL crea un tipo de tabla denominado **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="cc532-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="cc532-206">En el código, se crea un **DataTable** con los mismos nombres y tipos exactos del tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span></span> <span data-ttu-id="cc532-207">Pase este **DataTable** en un parámetro de una consulta de texto o una llamada de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="cc532-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="cc532-208">En el siguiente ejemplo se muestra esta técnica:</span><span class="sxs-lookup"><span data-stu-id="cc532-208">The following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. The following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="cc532-209">En el ejemplo anterior, el objeto **SqlCommand** inserta filas desde un parámetro con valores de tabla, **@TestTvp**.</span><span class="sxs-lookup"><span data-stu-id="cc532-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="cc532-210">El objeto **DataTable** creado antes se asigna a este parámetro con el método **SqlCommand.Parameters.Add**.</span><span class="sxs-lookup"><span data-stu-id="cc532-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="cc532-211">El procesamiento por lotes de las inserciones en una llamada aumenta notablemente el rendimiento en comparación con las inserciones secuenciales.</span><span class="sxs-lookup"><span data-stu-id="cc532-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span></span>

<span data-ttu-id="cc532-212">Para mejorar aún más el ejemplo anterior, use un procedimiento almacenado en lugar de un comando de texto.</span><span class="sxs-lookup"><span data-stu-id="cc532-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="cc532-213">El siguiente comando Transact-SQL crea un procedimiento almacenado que acepta el parámetro con valores de tabla **SimpleTestTableType** .</span><span class="sxs-lookup"><span data-stu-id="cc532-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="cc532-214">Después, cambie la declaración del objeto **SqlCommand** en el ejemplo de código anterior a lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cc532-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="cc532-215">En la mayoría de los casos, los parámetros con valores de tabla tienen un rendimiento equivalente o mejor que otras técnicas de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="cc532-216">Los parámetros con valores de tabla son a menudo preferibles, ya que son más flexibles que otras opciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="cc532-217">Por ejemplo, otras técnicas, como la copia masiva de SQL, solo permiten la inserción de filas nuevas.</span><span class="sxs-lookup"><span data-stu-id="cc532-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span></span> <span data-ttu-id="cc532-218">Sin embargo, con los parámetros con valores de tabla, puede usar lógica en el procedimiento almacenado para determinar qué filas son actualizaciones y cuáles son inserciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span></span> <span data-ttu-id="cc532-219">También se puede modificar el tipo de tabla para que contenga una columna "Operación" que indica si la fila especificada se debe insertar, actualizar o eliminar.</span><span class="sxs-lookup"><span data-stu-id="cc532-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="cc532-220">En la tabla siguiente se muestran los resultados de pruebas ad hoc para el uso de parámetros con valores de tabla, expresados en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="cc532-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="cc532-221">Operaciones</span><span class="sxs-lookup"><span data-stu-id="cc532-221">Operations</span></span> | <span data-ttu-id="cc532-222">De local a Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-222">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="cc532-223">Azure en el mismo centro de datos (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc532-224">1</span><span class="sxs-lookup"><span data-stu-id="cc532-224">1</span></span> |<span data-ttu-id="cc532-225">124</span><span class="sxs-lookup"><span data-stu-id="cc532-225">124</span></span> |<span data-ttu-id="cc532-226">32</span><span class="sxs-lookup"><span data-stu-id="cc532-226">32</span></span> |
| <span data-ttu-id="cc532-227">10</span><span class="sxs-lookup"><span data-stu-id="cc532-227">10</span></span> |<span data-ttu-id="cc532-228">131</span><span class="sxs-lookup"><span data-stu-id="cc532-228">131</span></span> |<span data-ttu-id="cc532-229">25</span><span class="sxs-lookup"><span data-stu-id="cc532-229">25</span></span> |
| <span data-ttu-id="cc532-230">100</span><span class="sxs-lookup"><span data-stu-id="cc532-230">100</span></span> |<span data-ttu-id="cc532-231">338</span><span class="sxs-lookup"><span data-stu-id="cc532-231">338</span></span> |<span data-ttu-id="cc532-232">51</span><span class="sxs-lookup"><span data-stu-id="cc532-232">51</span></span> |
| <span data-ttu-id="cc532-233">1000</span><span class="sxs-lookup"><span data-stu-id="cc532-233">1000</span></span> |<span data-ttu-id="cc532-234">2615</span><span class="sxs-lookup"><span data-stu-id="cc532-234">2615</span></span> |<span data-ttu-id="cc532-235">382</span><span class="sxs-lookup"><span data-stu-id="cc532-235">382</span></span> |
| <span data-ttu-id="cc532-236">10000</span><span class="sxs-lookup"><span data-stu-id="cc532-236">10000</span></span> |<span data-ttu-id="cc532-237">23830</span><span class="sxs-lookup"><span data-stu-id="cc532-237">23830</span></span> |<span data-ttu-id="cc532-238">3586</span><span class="sxs-lookup"><span data-stu-id="cc532-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="cc532-239">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="cc532-239">Results are not benchmarks.</span></span> <span data-ttu-id="cc532-240">Consulte la [nota sobre los tiempos resultantes en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="cc532-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cc532-241">El aumento del rendimiento gracias al procesamiento por lotes es evidente de inmediato.</span><span class="sxs-lookup"><span data-stu-id="cc532-241">The performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="cc532-242">En la prueba secuencial anterior, 1000 operaciones tardaban 129 segundos fuera del centro de datos y 21 segundos dentro del centro de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span></span> <span data-ttu-id="cc532-243">Pero con parámetros con valores de tabla, 1000 operaciones solo tardan 2,6 segundos fuera del centro de datos y 0,4 segundos dentro del centro de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span></span>

<span data-ttu-id="cc532-244">Para obtener más información sobre los parámetros con valores de tabla, consulte [Usar parámetros con valores de tabla (motor de base de datos)](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc532-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="cc532-245">Copia masiva de SQL</span><span class="sxs-lookup"><span data-stu-id="cc532-245">SQL bulk copy</span></span>
<span data-ttu-id="cc532-246">La copia masiva de SQL es otra forma de insertar grandes cantidades de datos en una base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="cc532-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span></span> <span data-ttu-id="cc532-247">Las aplicaciones .NET pueden usar la clase **SqlBulkCopy** para realizar operaciones de inserción masiva.</span><span class="sxs-lookup"><span data-stu-id="cc532-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span></span> <span data-ttu-id="cc532-248">**SqlBulkCopy** desempeña una función similar a la herramienta de línea de comandos **Bcp.exe** o la instrucción Transact-SQL **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="cc532-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="cc532-249">En el ejemplo de código siguiente se muestra cómo realizar una copia masiva de las filas de la tabla de origen **DataTable**en la tabla de destino en SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="cc532-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="cc532-250">Hay algunos casos en que la copia masiva es preferible a los parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="cc532-251">Consulte la tabla de comparación de parámetros con valores de tabla frente a las operaciones BULK INSERT en el tema [Usar parámetros con valores de tabla (motor de base de datos)](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc532-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="cc532-252">Los resultados de pruebas ad hoc siguientes muestran el rendimiento del procesamiento por lotes con **SqlBulkCopy** en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="cc532-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="cc532-253">Operaciones</span><span class="sxs-lookup"><span data-stu-id="cc532-253">Operations</span></span> | <span data-ttu-id="cc532-254">De local a Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-254">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="cc532-255">Azure en el mismo centro de datos (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc532-256">1</span><span class="sxs-lookup"><span data-stu-id="cc532-256">1</span></span> |<span data-ttu-id="cc532-257">433</span><span class="sxs-lookup"><span data-stu-id="cc532-257">433</span></span> |<span data-ttu-id="cc532-258">57</span><span class="sxs-lookup"><span data-stu-id="cc532-258">57</span></span> |
| <span data-ttu-id="cc532-259">10</span><span class="sxs-lookup"><span data-stu-id="cc532-259">10</span></span> |<span data-ttu-id="cc532-260">441</span><span class="sxs-lookup"><span data-stu-id="cc532-260">441</span></span> |<span data-ttu-id="cc532-261">32</span><span class="sxs-lookup"><span data-stu-id="cc532-261">32</span></span> |
| <span data-ttu-id="cc532-262">100</span><span class="sxs-lookup"><span data-stu-id="cc532-262">100</span></span> |<span data-ttu-id="cc532-263">636</span><span class="sxs-lookup"><span data-stu-id="cc532-263">636</span></span> |<span data-ttu-id="cc532-264">53</span><span class="sxs-lookup"><span data-stu-id="cc532-264">53</span></span> |
| <span data-ttu-id="cc532-265">1000</span><span class="sxs-lookup"><span data-stu-id="cc532-265">1000</span></span> |<span data-ttu-id="cc532-266">2535</span><span class="sxs-lookup"><span data-stu-id="cc532-266">2535</span></span> |<span data-ttu-id="cc532-267">341</span><span class="sxs-lookup"><span data-stu-id="cc532-267">341</span></span> |
| <span data-ttu-id="cc532-268">10000</span><span class="sxs-lookup"><span data-stu-id="cc532-268">10000</span></span> |<span data-ttu-id="cc532-269">21605</span><span class="sxs-lookup"><span data-stu-id="cc532-269">21605</span></span> |<span data-ttu-id="cc532-270">2737</span><span class="sxs-lookup"><span data-stu-id="cc532-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="cc532-271">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="cc532-271">Results are not benchmarks.</span></span> <span data-ttu-id="cc532-272">Consulte la [nota sobre los tiempos resultantes en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="cc532-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cc532-273">En lotes más pequeños, el uso de parámetros con valores de tabla superó el rendimiento de la clase **SqlBulkCopy** .</span><span class="sxs-lookup"><span data-stu-id="cc532-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span></span> <span data-ttu-id="cc532-274">Sin embargo, el rendimiento con**SqlBulkCopy** fue entre un 12 % y un 31 % mayor que los parámetros con valores de tabla en las pruebas de 1000 y 10,000 filas.</span><span class="sxs-lookup"><span data-stu-id="cc532-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="cc532-275">Como los parámetros con valores de tabla, **SqlBulkCopy** es una buena opción para las inserciones por lotes, especialmente cuando se compara con el rendimiento de las operaciones sin lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span></span>

<span data-ttu-id="cc532-276">Para obtener más información sobre la copia masiva en ADO.NET, consulte [Operaciones de copia masiva en SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc532-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="cc532-277">Instrucciones INSERT con parámetros de varias filas</span><span class="sxs-lookup"><span data-stu-id="cc532-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="cc532-278">Una alternativa para los lotes pequeños es construir una instrucción INSERT con parámetros grande que inserte varias filas.</span><span class="sxs-lookup"><span data-stu-id="cc532-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="cc532-279">En el siguiente ejemplo de código se muestra esta técnica.</span><span class="sxs-lookup"><span data-stu-id="cc532-279">The following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="cc532-280">Este ejemplo está pensado para demostrar el concepto básico.</span><span class="sxs-lookup"><span data-stu-id="cc532-280">This example is meant to show the basic concept.</span></span> <span data-ttu-id="cc532-281">En un escenario más realista, se recorrerían las entidades necesarias para construir la cadena de consulta y los parámetros del comando simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="cc532-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span></span> <span data-ttu-id="cc532-282">Está limitado a un total de 2100 parámetros de consulta, lo que restringe el número total de filas que pueden procesarse de esta manera.</span><span class="sxs-lookup"><span data-stu-id="cc532-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="cc532-283">Los resultados de pruebas ad hoc siguientes muestran el rendimiento de este tipo de instrucción de inserción en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="cc532-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="cc532-284">Operaciones</span><span class="sxs-lookup"><span data-stu-id="cc532-284">Operations</span></span> | <span data-ttu-id="cc532-285">Parámetros con valores de tabla (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="cc532-286">Instrucción INSERT única (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc532-287">1</span><span class="sxs-lookup"><span data-stu-id="cc532-287">1</span></span> |<span data-ttu-id="cc532-288">32</span><span class="sxs-lookup"><span data-stu-id="cc532-288">32</span></span> |<span data-ttu-id="cc532-289">20</span><span class="sxs-lookup"><span data-stu-id="cc532-289">20</span></span> |
| <span data-ttu-id="cc532-290">10</span><span class="sxs-lookup"><span data-stu-id="cc532-290">10</span></span> |<span data-ttu-id="cc532-291">30</span><span class="sxs-lookup"><span data-stu-id="cc532-291">30</span></span> |<span data-ttu-id="cc532-292">25</span><span class="sxs-lookup"><span data-stu-id="cc532-292">25</span></span> |
| <span data-ttu-id="cc532-293">100</span><span class="sxs-lookup"><span data-stu-id="cc532-293">100</span></span> |<span data-ttu-id="cc532-294">33</span><span class="sxs-lookup"><span data-stu-id="cc532-294">33</span></span> |<span data-ttu-id="cc532-295">51</span><span class="sxs-lookup"><span data-stu-id="cc532-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="cc532-296">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="cc532-296">Results are not benchmarks.</span></span> <span data-ttu-id="cc532-297">Consulte la [nota sobre los tiempos resultantes en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="cc532-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cc532-298">Este enfoque puede ser algo más rápido para los lotes de menos de 100 filas.</span><span class="sxs-lookup"><span data-stu-id="cc532-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="cc532-299">Aunque la mejora es pequeña, esta técnica es otra opción que podría funcionar bien en su escenario de aplicaciones específico.</span><span class="sxs-lookup"><span data-stu-id="cc532-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="cc532-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="cc532-300">DataAdapter</span></span>
<span data-ttu-id="cc532-301">La clase **DataAdapter** le permite modificar un objeto **DataSet** y después enviar los cambios como operaciones INSERT, UPDATE y DELETE.</span><span class="sxs-lookup"><span data-stu-id="cc532-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="cc532-302">Si está usando la clase **DataAdapter** de esta manera, es importante tener en cuenta que se realizan llamadas independientes para cada operación distinta.</span><span class="sxs-lookup"><span data-stu-id="cc532-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="cc532-303">Para mejorar el rendimiento, use la propiedad **UpdateBatchSize** con el número de operaciones que deben procesarse por lotes a la vez.</span><span class="sxs-lookup"><span data-stu-id="cc532-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span></span> <span data-ttu-id="cc532-304">Para obtener más información, consulte [Realizar operaciones por lotes mediante DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc532-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="cc532-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="cc532-305">Entity framework</span></span>
<span data-ttu-id="cc532-306">Actualmente, Entity Framework no admite el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="cc532-307">Varios desarrolladores de la comunidad intentaron demostrar soluciones alternativas, como invalidar el método **SaveChanges** .</span><span class="sxs-lookup"><span data-stu-id="cc532-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span></span> <span data-ttu-id="cc532-308">Pero las soluciones suelen ser complejas y personalizadas para la aplicación y el modelo de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-308">But the solutions are typically complex and customized to the application and data model.</span></span> <span data-ttu-id="cc532-309">El proyecto Entity Framework de CodePlex actualmente cuenta con una página de debate sobre esta solicitud de característica.</span><span class="sxs-lookup"><span data-stu-id="cc532-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="cc532-310">Para ver este debate, consulte las [notas de la reunión de diseño del 2 de agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="cc532-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="cc532-311">XML</span><span class="sxs-lookup"><span data-stu-id="cc532-311">XML</span></span>
<span data-ttu-id="cc532-312">Por exhaustividad, creemos que es importante hablar de XML como estrategia de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span></span> <span data-ttu-id="cc532-313">Sin embargo, el uso de XML no supone ninguna ventaja respecto a otros métodos, pero sí varias desventajas.</span><span class="sxs-lookup"><span data-stu-id="cc532-313">However, the use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="cc532-314">El enfoque es similar a los parámetros con valores de tabla, excepto en que se pasa una cadena o un archivo XML a un procedimiento almacenado en lugar de una tabla definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="cc532-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="cc532-315">El procedimiento almacenado analiza los comandos en el procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="cc532-315">The stored procedure parses the commands in the stored procedure.</span></span>

<span data-ttu-id="cc532-316">Existen varias desventajas con este enfoque:</span><span class="sxs-lookup"><span data-stu-id="cc532-316">There are several disadvantages to this approach:</span></span>

* <span data-ttu-id="cc532-317">El trabajo con XML puede resultar tedioso y propenso a errores.</span><span class="sxs-lookup"><span data-stu-id="cc532-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="cc532-318">Analizar el XML en la base de datos puede consumir bastantes recursos de la CPU.</span><span class="sxs-lookup"><span data-stu-id="cc532-318">Parsing the XML on the database can be CPU-intensive.</span></span>
* <span data-ttu-id="cc532-319">En la mayoría de los casos, este método es más lento que los parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="cc532-320">Por estas razones, no se recomienda el uso de XML para las consultas por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-320">For these reasons, the use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="cc532-321">Consideraciones sobre el procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="cc532-321">Batching considerations</span></span>
<span data-ttu-id="cc532-322">Las secciones siguientes proporcionan más instrucciones para el uso del procesamiento por lotes en las aplicaciones de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="cc532-323">Compromisos</span><span class="sxs-lookup"><span data-stu-id="cc532-323">Tradeoffs</span></span>
<span data-ttu-id="cc532-324">Según la arquitectura, el procesamiento por lotes puede suponer un compromiso entre el rendimiento y la resistencia.</span><span class="sxs-lookup"><span data-stu-id="cc532-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="cc532-325">Por ejemplo, piense en un escenario en que su rol deja de funcionar inesperadamente.</span><span class="sxs-lookup"><span data-stu-id="cc532-325">For example, consider the scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="cc532-326">Si pierde una fila de datos, el efecto es menor que si pierde un lote grande de filas sin enviar.</span><span class="sxs-lookup"><span data-stu-id="cc532-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="cc532-327">Existe un riesgo mayor cuando almacena filas en búfer antes de enviarlas a la base de datos en un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="cc532-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span></span>

<span data-ttu-id="cc532-328">Debido a este compromiso, evalúe el tipo de operaciones que procese por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-328">Because of this tradeoff, evaluate the type of operations that you batch.</span></span> <span data-ttu-id="cc532-329">Intensifique el procesamiento por lotes (con lotes y períodos de tiempo mayores) con aquellos datos que sean menos críticos.</span><span class="sxs-lookup"><span data-stu-id="cc532-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="cc532-330">Tamaño de lote</span><span class="sxs-lookup"><span data-stu-id="cc532-330">Batch size</span></span>
<span data-ttu-id="cc532-331">En nuestras pruebas, normalmente dividir los lotes grandes en fragmentos menores no supuso ninguna ventaja.</span><span class="sxs-lookup"><span data-stu-id="cc532-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span></span> <span data-ttu-id="cc532-332">De hecho, esta subdivisión produjo a menudo un rendimiento más lento que el envío de un único lote grande.</span><span class="sxs-lookup"><span data-stu-id="cc532-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="cc532-333">Por ejemplo, considere un escenario en el que desea insertar 1000 filas.</span><span class="sxs-lookup"><span data-stu-id="cc532-333">For example, consider a scenario where you want to insert 1000 rows.</span></span> <span data-ttu-id="cc532-334">La siguiente tabla muestra cuánto tiempo se tarda usando parámetros con valores de tabla para insertar 1000 filas cuando se dividen en lotes más pequeños.</span><span class="sxs-lookup"><span data-stu-id="cc532-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="cc532-335">Tamaño de lote</span><span class="sxs-lookup"><span data-stu-id="cc532-335">Batch size</span></span> | <span data-ttu-id="cc532-336">Iteraciones</span><span class="sxs-lookup"><span data-stu-id="cc532-336">Iterations</span></span> | <span data-ttu-id="cc532-337">Parámetros con valores de tabla (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc532-338">1000</span><span class="sxs-lookup"><span data-stu-id="cc532-338">1000</span></span> |<span data-ttu-id="cc532-339">1</span><span class="sxs-lookup"><span data-stu-id="cc532-339">1</span></span> |<span data-ttu-id="cc532-340">347</span><span class="sxs-lookup"><span data-stu-id="cc532-340">347</span></span> |
| <span data-ttu-id="cc532-341">500</span><span class="sxs-lookup"><span data-stu-id="cc532-341">500</span></span> |<span data-ttu-id="cc532-342">2</span><span class="sxs-lookup"><span data-stu-id="cc532-342">2</span></span> |<span data-ttu-id="cc532-343">355</span><span class="sxs-lookup"><span data-stu-id="cc532-343">355</span></span> |
| <span data-ttu-id="cc532-344">100</span><span class="sxs-lookup"><span data-stu-id="cc532-344">100</span></span> |<span data-ttu-id="cc532-345">10</span><span class="sxs-lookup"><span data-stu-id="cc532-345">10</span></span> |<span data-ttu-id="cc532-346">465</span><span class="sxs-lookup"><span data-stu-id="cc532-346">465</span></span> |
| <span data-ttu-id="cc532-347">50</span><span class="sxs-lookup"><span data-stu-id="cc532-347">50</span></span> |<span data-ttu-id="cc532-348">20</span><span class="sxs-lookup"><span data-stu-id="cc532-348">20</span></span> |<span data-ttu-id="cc532-349">630</span><span class="sxs-lookup"><span data-stu-id="cc532-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="cc532-350">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="cc532-350">Results are not benchmarks.</span></span> <span data-ttu-id="cc532-351">Consulte la [nota sobre los tiempos resultantes en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="cc532-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cc532-352">Es obvio que el mejor rendimiento para 1000 filas es enviarlas todas a la vez.</span><span class="sxs-lookup"><span data-stu-id="cc532-352">You can see that the best performance for 1000 rows is to submit them all at once.</span></span> <span data-ttu-id="cc532-353">En otras pruebas (no mostradas aquí) hubo una pequeña mejora de rendimiento al dividir un lote de 10.000 filas en dos lotes de 5000.</span><span class="sxs-lookup"><span data-stu-id="cc532-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="cc532-354">Pero el esquema de tabla para estas pruebas es relativamente simple, por lo que debería realizar pruebas con sus datos y tamaños de lote específicos para verificar estos hallazgos.</span><span class="sxs-lookup"><span data-stu-id="cc532-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span></span>

<span data-ttu-id="cc532-355">Otro factor que se debe considerar es que, si el lote total es demasiado grande, es posible que Base de datos SQL imponga limitaciones y no confirme el lote.</span><span class="sxs-lookup"><span data-stu-id="cc532-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span></span> <span data-ttu-id="cc532-356">Para obtener resultados óptimos, pruebe su escenario concreto para determinar si existe un tamaño de lote ideal.</span><span class="sxs-lookup"><span data-stu-id="cc532-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span></span> <span data-ttu-id="cc532-357">Haga que el tamaño de lote sea configurable en tiempo de ejecución para permitir ajustes rápidos en función del rendimiento o la presencia de errores.</span><span class="sxs-lookup"><span data-stu-id="cc532-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="cc532-358">Por último, sopese el tamaño del lote y los riesgos asociados con el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-358">Finally, balance the size of the batch with the risks associated with batching.</span></span> <span data-ttu-id="cc532-359">Si se producen errores transitorios o de rol, considere las consecuencias de reintentar la operación o de perder los datos en el lote.</span><span class="sxs-lookup"><span data-stu-id="cc532-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="cc532-360">Procesamiento en paralelo</span><span class="sxs-lookup"><span data-stu-id="cc532-360">Parallel processing</span></span>
<span data-ttu-id="cc532-361">¿Qué pasa si adopta el enfoque de reducir el tamaño del lote pero usa varios subprocesos para ejecutar el trabajo?</span><span class="sxs-lookup"><span data-stu-id="cc532-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span></span> <span data-ttu-id="cc532-362">Una vez más, nuestras pruebas mostraron que varios lotes multiproceso más pequeños presentaban normalmente un rendimiento peor que un único lote más grande.</span><span class="sxs-lookup"><span data-stu-id="cc532-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="cc532-363">La siguiente prueba intenta insertar 1000 filas en uno o varios lotes paralelos.</span><span class="sxs-lookup"><span data-stu-id="cc532-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="cc532-364">Esta prueba muestra cómo el uso de más lotes simultáneos realmente reduce el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="cc532-365">Tamaño de lote [iteraciones]</span><span class="sxs-lookup"><span data-stu-id="cc532-365">Batch size [Iterations]</span></span> | <span data-ttu-id="cc532-366">Dos subprocesos (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-366">Two threads (ms)</span></span> | <span data-ttu-id="cc532-367">Cuatro subprocesos (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-367">Four threads (ms)</span></span> | <span data-ttu-id="cc532-368">Seis subprocesos (ms)</span><span class="sxs-lookup"><span data-stu-id="cc532-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cc532-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="cc532-369">1000 [1]</span></span> |<span data-ttu-id="cc532-370">277</span><span class="sxs-lookup"><span data-stu-id="cc532-370">277</span></span> |<span data-ttu-id="cc532-371">315</span><span class="sxs-lookup"><span data-stu-id="cc532-371">315</span></span> |<span data-ttu-id="cc532-372">266</span><span class="sxs-lookup"><span data-stu-id="cc532-372">266</span></span> |
| <span data-ttu-id="cc532-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="cc532-373">500 [2]</span></span> |<span data-ttu-id="cc532-374">548</span><span class="sxs-lookup"><span data-stu-id="cc532-374">548</span></span> |<span data-ttu-id="cc532-375">278</span><span class="sxs-lookup"><span data-stu-id="cc532-375">278</span></span> |<span data-ttu-id="cc532-376">256</span><span class="sxs-lookup"><span data-stu-id="cc532-376">256</span></span> |
| <span data-ttu-id="cc532-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="cc532-377">250 [4]</span></span> |<span data-ttu-id="cc532-378">405</span><span class="sxs-lookup"><span data-stu-id="cc532-378">405</span></span> |<span data-ttu-id="cc532-379">329</span><span class="sxs-lookup"><span data-stu-id="cc532-379">329</span></span> |<span data-ttu-id="cc532-380">265</span><span class="sxs-lookup"><span data-stu-id="cc532-380">265</span></span> |
| <span data-ttu-id="cc532-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="cc532-381">100 [10]</span></span> |<span data-ttu-id="cc532-382">488</span><span class="sxs-lookup"><span data-stu-id="cc532-382">488</span></span> |<span data-ttu-id="cc532-383">439</span><span class="sxs-lookup"><span data-stu-id="cc532-383">439</span></span> |<span data-ttu-id="cc532-384">391</span><span class="sxs-lookup"><span data-stu-id="cc532-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="cc532-385">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="cc532-385">Results are not benchmarks.</span></span> <span data-ttu-id="cc532-386">Consulte la [nota sobre los tiempos resultantes en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="cc532-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cc532-387">Hay varias razones posibles para la degradación del rendimiento debido al paralelismo:</span><span class="sxs-lookup"><span data-stu-id="cc532-387">There are several potential reasons for the degradation in performance due to parallelism:</span></span>

* <span data-ttu-id="cc532-388">Se realizan varias llamadas de red simultáneas en lugar de una.</span><span class="sxs-lookup"><span data-stu-id="cc532-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="cc532-389">Varias operaciones en una sola tabla pueden conllevar contención y bloqueo.</span><span class="sxs-lookup"><span data-stu-id="cc532-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="cc532-390">Hay sobrecargas asociadas con el subprocesamiento múltiple.</span><span class="sxs-lookup"><span data-stu-id="cc532-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="cc532-391">El gasto que supone abrir varias conexiones sobrepasa las ventajas del procesamiento en paralelo.</span><span class="sxs-lookup"><span data-stu-id="cc532-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span></span>

<span data-ttu-id="cc532-392">Si elige como destino diferentes tablas o bases de datos, es posible que observe alguna mejora de rendimiento con esta estrategia.</span><span class="sxs-lookup"><span data-stu-id="cc532-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span></span> <span data-ttu-id="cc532-393">Un escenario de particionamiento de base de datos o de federaciones sería adecuado para este enfoque.</span><span class="sxs-lookup"><span data-stu-id="cc532-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="cc532-394">El particionamiento usa varias bases de datos y enruta distintos datos a cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-394">Sharding uses multiple databases and routes different data to each database.</span></span> <span data-ttu-id="cc532-395">Si cada lote pequeño va a una base de datos diferente, puede ser más eficaz realizar las operaciones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="cc532-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span></span> <span data-ttu-id="cc532-396">Sin embargo, la mejora de rendimiento no es lo bastante importante como para usarla como base para tomar la decisión de emplear el particionamiento de base de datos en la solución.</span><span class="sxs-lookup"><span data-stu-id="cc532-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span></span>

<span data-ttu-id="cc532-397">En algunos diseños, la ejecución en paralelo de lotes más pequeños podría mejorar el rendimiento de las solicitudes en un sistema con mucha carga.</span><span class="sxs-lookup"><span data-stu-id="cc532-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="cc532-398">En este caso, aunque es más rápido procesar un único lote más grande, es posible que el procesamiento de varios lotes en paralelo sea más eficaz.</span><span class="sxs-lookup"><span data-stu-id="cc532-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="cc532-399">Si usa la ejecución en paralelo, considere la posibilidad de controlar el número máximo de subprocesos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cc532-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span></span> <span data-ttu-id="cc532-400">Un número menor podría causar menos contención y un tiempo de ejecución más rápido.</span><span class="sxs-lookup"><span data-stu-id="cc532-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="cc532-401">Además, tenga en cuenta la carga adicional sobre la base de datos de destino tanto en conexiones como en transacciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="cc532-402">Factores de rendimiento relacionados</span><span class="sxs-lookup"><span data-stu-id="cc532-402">Related performance factors</span></span>
<span data-ttu-id="cc532-403">Las instrucciones típicas sobre el rendimiento de la base de datos también afectan al procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="cc532-404">Por ejemplo, el rendimiento de inserción se reduce para aquellas tablas que tengan una clave principal grande o varios índices no agrupados.</span><span class="sxs-lookup"><span data-stu-id="cc532-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="cc532-405">Si los parámetros con valores de tabla usan un procedimiento almacenado, puede emplear el comando **SET NOCOUNT ON** al principio del procedimiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span></span> <span data-ttu-id="cc532-406">Esta instrucción suprime la devolución del recuento de las filas afectadas en el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-406">This statement suppresses the return of the count of the affected rows in the procedure.</span></span> <span data-ttu-id="cc532-407">Sin embargo, en nuestras pruebas, el uso de **SET NOCOUNT ON** no tiene ningún efecto sobre el rendimiento o lo disminuye.</span><span class="sxs-lookup"><span data-stu-id="cc532-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="cc532-408">El procedimiento almacenado de la prueba era simple, con un solo comando **INSERT** desde el parámetro con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span></span> <span data-ttu-id="cc532-409">Es posible que los procedimientos almacenados más complejos se beneficien de esta instrucción.</span><span class="sxs-lookup"><span data-stu-id="cc532-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="cc532-410">Pero no dé por supuesto que agregar **SET NOCOUNT ON** al procedimiento almacenado mejora automáticamente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span></span> <span data-ttu-id="cc532-411">Para entender el efecto, pruebe el procedimiento almacenado con y sin la instrucción **SET NOCOUNT ON** .</span><span class="sxs-lookup"><span data-stu-id="cc532-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="cc532-412">Escenarios de procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="cc532-412">Batching scenarios</span></span>
<span data-ttu-id="cc532-413">En las secciones siguientes, se describe cómo usar parámetros con valores de tabla en tres escenarios de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-413">The following sections describe how to use table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="cc532-414">El primer escenario muestra cómo el almacenamiento en búfer y el procesamiento por lotes funcionan juntos.</span><span class="sxs-lookup"><span data-stu-id="cc532-414">The first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="cc532-415">El segundo escenario mejora el rendimiento al realizar operaciones maestro/detalle en una sola llamada a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="cc532-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="cc532-416">El último escenario muestra cómo usar parámetros con valores de tabla en una operación "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="cc532-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="cc532-417">Almacenamiento en búfer</span><span class="sxs-lookup"><span data-stu-id="cc532-417">Buffering</span></span>
<span data-ttu-id="cc532-418">Aunque hay algunos escenarios que son candidatos obvios para el procesamiento por lotes, muchos otros podrían beneficiarse del procesamiento por lotes difiriendo el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="cc532-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="cc532-419">Sin embargo, el procesamiento diferido también plantea un mayor riesgo de que los datos se pierdan si se produce un error inesperado.</span><span class="sxs-lookup"><span data-stu-id="cc532-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span></span> <span data-ttu-id="cc532-420">Es importante comprender este riesgo y tener en cuenta las consecuencias.</span><span class="sxs-lookup"><span data-stu-id="cc532-420">It is important to understand this risk and consider the consequences.</span></span>

<span data-ttu-id="cc532-421">Por ejemplo, piense en una aplicación web que registra el historial de navegación de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="cc532-421">For example, consider a web application that tracks the navigation history of each user.</span></span> <span data-ttu-id="cc532-422">Con cada solicitud de página, la aplicación podría llamar a una base de datos para registrar la vista de página del usuario.</span><span class="sxs-lookup"><span data-stu-id="cc532-422">On each page request, the application could make a database call to record the user’s page view.</span></span> <span data-ttu-id="cc532-423">Pero se pueden conseguir mayor rendimiento y escalabilidad si se almacenan las actividades de navegación de los usuarios en el búfer y después se envían estos datos a la base de datos en lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span></span> <span data-ttu-id="cc532-424">Puede desencadenar la actualización de la base de datos según el tiempo transcurrido o el tamaño de búfer.</span><span class="sxs-lookup"><span data-stu-id="cc532-424">You can trigger the database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="cc532-425">Por ejemplo, una regla podría especificar que se debería procesar el lote después de 20 segundos o cuando el búfer alcance los 1000 elementos.</span><span class="sxs-lookup"><span data-stu-id="cc532-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span></span>

<span data-ttu-id="cc532-426">El siguiente ejemplo de código usa [extensiones reactivas - Rx](https://msdn.microsoft.com/data/gg577609) para procesar los eventos almacenados en búfer generados por una clase de supervisión.</span><span class="sxs-lookup"><span data-stu-id="cc532-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span></span> <span data-ttu-id="cc532-427">Cuando el búfer se llena o se alcanza el tiempo de espera, se envía el lote de datos de usuarios a la base de datos con un parámetro con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span></span>

<span data-ttu-id="cc532-428">La siguiente clase NavHistoryData modela los detalles de navegación de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cc532-428">The following NavHistoryData class models the user navigation details.</span></span> <span data-ttu-id="cc532-429">Contiene información básica como el identificador de usuario, la dirección URL visitada y el tiempo de acceso.</span><span class="sxs-lookup"><span data-stu-id="cc532-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="cc532-430">La clase NavHistoryDataMonitor se encarga de almacenar los datos de navegación de los usuarios en búfer en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span></span> <span data-ttu-id="cc532-431">Contiene un método, RecordUserNavigationEntry, que responde generando un evento **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="cc532-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="cc532-432">El código siguiente muestra la lógica del constructor que usa Rx para crear una colección observable basada en el evento.</span><span class="sxs-lookup"><span data-stu-id="cc532-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span></span> <span data-ttu-id="cc532-433">Después, se suscribe a esta colección observable con el método Buffer.</span><span class="sxs-lookup"><span data-stu-id="cc532-433">It then subscribes to this observable collection with the Buffer method.</span></span> <span data-ttu-id="cc532-434">La sobrecarga especifica que el búfer se debe enviar cada 20 segundos o 1000 entradas.</span><span class="sxs-lookup"><span data-stu-id="cc532-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="cc532-435">El controlador convierte todos los elementos almacenados en búfer en un tipo con valores de tabla y después pasa este tipo a un procedimiento almacenado que procesa el lote.</span><span class="sxs-lookup"><span data-stu-id="cc532-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span></span> <span data-ttu-id="cc532-436">El código siguiente muestra la definición completa de las clases NavHistoryDataEventArgs y NavHistoryDataMonitor.</span><span class="sxs-lookup"><span data-stu-id="cc532-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="cc532-437">Para usar esta clase de almacenamiento en búfer, la aplicación crea un objeto NavHistoryDataMonitor estático.</span><span class="sxs-lookup"><span data-stu-id="cc532-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="cc532-438">Cada vez que un usuario accede a una página, la aplicación llama al método NavHistoryDataMonitor.RecordUserNavigationEntry.</span><span class="sxs-lookup"><span data-stu-id="cc532-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="cc532-439">La lógica de almacenamiento en búfer procede a enviar estas entradas a la base de datos en lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="cc532-440">Maestro/detalle</span><span class="sxs-lookup"><span data-stu-id="cc532-440">Master detail</span></span>
<span data-ttu-id="cc532-441">Los parámetros con valores de tabla son útiles en escenarios INSERT sencillos.</span><span class="sxs-lookup"><span data-stu-id="cc532-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="cc532-442">Sin embargo, puede ser más difícil procesar por lotes aquellas inserciones para más de una tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-442">However, it can be more challenging to batch inserts that involve more than one table.</span></span> <span data-ttu-id="cc532-443">El escenario de "maestro/detalle" es un buen ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cc532-443">The “master/detail” scenario is a good example.</span></span> <span data-ttu-id="cc532-444">La tabla maestra identifica la entidad principal.</span><span class="sxs-lookup"><span data-stu-id="cc532-444">The master table identifies the primary entity.</span></span> <span data-ttu-id="cc532-445">Una o varias tablas de detalle almacenan más datos sobre la entidad.</span><span class="sxs-lookup"><span data-stu-id="cc532-445">One or more detail tables store more data about the entity.</span></span> <span data-ttu-id="cc532-446">En este escenario, las relaciones de clave externa aplican la relación de los detalles con una entidad maestra única.</span><span class="sxs-lookup"><span data-stu-id="cc532-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span></span> <span data-ttu-id="cc532-447">Considere una versión simplificada de una tabla PurchaseOrder y su tabla OrderDetail asociada.</span><span class="sxs-lookup"><span data-stu-id="cc532-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="cc532-448">El siguiente código Transact-SQL crea la tabla PurchaseOrder con cuatro columnas: OrderID, OrderDate, CustomerID y Status.</span><span class="sxs-lookup"><span data-stu-id="cc532-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="cc532-449">Cada pedido contiene una o más compras de productos.</span><span class="sxs-lookup"><span data-stu-id="cc532-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="cc532-450">Esta información se captura en la tabla PurchaseOrderDetail.</span><span class="sxs-lookup"><span data-stu-id="cc532-450">This information is captured in the PurchaseOrderDetail table.</span></span> <span data-ttu-id="cc532-451">El siguiente código Transact-SQL crea la tabla PurchaseOrderDetail con cinco columnas: OrderID, OrderDetailID, ProductID, UnitPrice y OrderQty.</span><span class="sxs-lookup"><span data-stu-id="cc532-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="cc532-452">La columna OrderID de la tabla PurchaseOrderDetail debe hacer referencia a un pedido de la tabla PurchaseOrder.</span><span class="sxs-lookup"><span data-stu-id="cc532-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span></span> <span data-ttu-id="cc532-453">La siguiente definición de una clave externa aplica esta restricción.</span><span class="sxs-lookup"><span data-stu-id="cc532-453">The following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="cc532-454">Para poder usar parámetros con valores de tabla, debe tener un tipo de tabla definido por el usuario para cada tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="cc532-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="cc532-455">Después, defina un procedimiento almacenado que acepte tablas de estos tipos.</span><span class="sxs-lookup"><span data-stu-id="cc532-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="cc532-456">Este procedimiento permite que una aplicación procese un conjunto de pedidos y detalles de pedido por lotes localmente en una sola llamada.</span><span class="sxs-lookup"><span data-stu-id="cc532-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="cc532-457">El siguiente código Transact-SQL proporciona la declaración completa del procedimiento almacenado para este ejemplo de pedido de compra.</span><span class="sxs-lookup"><span data-stu-id="cc532-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects the order identifiers in the @orders
    -- table with the actual order identifiers in the PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders to the PurchaseOrder table, storing the actual
    -- order identifiers in the @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match the passed-in order identifiers with the actual identifiers
    -- and complete the @IdentityLink table for use with inserting the details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert the order details into the PurchaseOrderDetail table, 
          -- using the actual order identifiers of the master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="cc532-458">En este ejemplo, la tabla @IdentityLink definida localmente almacena los valores de OrderID reales de las filas recién insertadas.</span><span class="sxs-lookup"><span data-stu-id="cc532-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span></span> <span data-ttu-id="cc532-459">Estos identificadores de pedidos son diferentes de los valores de OrderID temporales de los parámetros con valores de tabla @orders y @details.</span><span class="sxs-lookup"><span data-stu-id="cc532-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span></span> <span data-ttu-id="cc532-460">Por este motivo, la tabla @IdentityLink conecta después los valores de OrderID del parámetro @orders a los valores de OrderID reales para las nuevas filas de la tabla PurchaseOrder.</span><span class="sxs-lookup"><span data-stu-id="cc532-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span></span> <span data-ttu-id="cc532-461">Después de este paso, la tabla @IdentityLink puede facilitar la inserción de los detalles del pedido con el OrderID real que cumple la restricción de clave externa.</span><span class="sxs-lookup"><span data-stu-id="cc532-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span></span>

<span data-ttu-id="cc532-462">Este procedimiento almacenado puede usarse desde el código o desde otras llamadas Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="cc532-463">Consulte la sección Parámetros con valores de tabla de este artículo para obtener un ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="cc532-463">See the table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="cc532-464">El siguiente código Transact-SQL muestra cómo llamar a sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="cc532-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="cc532-465">Esta solución permite que cada lote use un conjunto de valores de OrderID que empiezan en 1.</span><span class="sxs-lookup"><span data-stu-id="cc532-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="cc532-466">Estos valores temporales de OrderID describen las relaciones en el lote, pero los valores de OrderID reales se determinan en el momento de la operación de inserción.</span><span class="sxs-lookup"><span data-stu-id="cc532-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span></span> <span data-ttu-id="cc532-467">Puede ejecutar las mismas instrucciones en el ejemplo anterior repetidamente y generar pedidos únicos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span></span> <span data-ttu-id="cc532-468">Por este motivo, podría agregar más lógica de base de datos o código que evite la duplicación de pedidos cuando se usa esta técnica de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="cc532-469">Este ejemplo demuestra que las operaciones de base de datos más complejas, como las operaciones maestro/detalle, se pueden procesar por lotes con parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="cc532-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="cc532-470">UPSERT</span></span>
<span data-ttu-id="cc532-471">Otro escenario de procesamiento por lotes supone la actualización de filas existentes y la inserción de nuevas filas de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="cc532-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="cc532-472">Esta operación se conoce a veces como operación "UPSERT" (actualización + inserción).</span><span class="sxs-lookup"><span data-stu-id="cc532-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="cc532-473">En lugar de realizar llamadas independientes para insertar (INSERT) y actualizar (UPDATE), la instrucción MERGE es más adecuada para esta tarea.</span><span class="sxs-lookup"><span data-stu-id="cc532-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span></span> <span data-ttu-id="cc532-474">La instrucción MERGE puede realizar ambas operaciones en una sola llamada.</span><span class="sxs-lookup"><span data-stu-id="cc532-474">The MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="cc532-475">Los parámetros con valores de tabla pueden usarse con la instrucción MERGE para realizar actualizaciones e inserciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span></span> <span data-ttu-id="cc532-476">Por ejemplo, piense en una tabla Employee simplificada que contiene las siguientes columnas: EmployeeID, FirstName, LastName y SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="cc532-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="cc532-477">En este ejemplo, puede aprovechar el hecho de que SocialSecurityNumber (número del seguro social) sea único para realizar una operación MERGE de varios empleados.</span><span class="sxs-lookup"><span data-stu-id="cc532-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span></span> <span data-ttu-id="cc532-478">En primer lugar, cree el tipo de tabla definido por el usuario:</span><span class="sxs-lookup"><span data-stu-id="cc532-478">First, create the user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="cc532-479">Después, cree un procedimiento almacenado o escriba código que use la instrucción MERGE para realizar la actualización y la inserción.</span><span class="sxs-lookup"><span data-stu-id="cc532-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span></span> <span data-ttu-id="cc532-480">En el ejemplo siguiente, se usa la instrucción MERGE en un parámetro con valores de tabla, @employees, del tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="cc532-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="cc532-481">El contenido de la tabla @employees no se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="cc532-481">The contents of the @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="cc532-482">Para obtener más información, consulte la documentación y los ejemplos de la instrucción MERGE.</span><span class="sxs-lookup"><span data-stu-id="cc532-482">For more information, see the documentation and examples for the MERGE statement.</span></span> <span data-ttu-id="cc532-483">Aunque se podría realizar el mismo trabajo en una llamada a procedimiento almacenado de varios pasos con operaciones INSERT y UPDATE separadas, la instrucción MERGE es más eficaz.</span><span class="sxs-lookup"><span data-stu-id="cc532-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span></span> <span data-ttu-id="cc532-484">Además, el código de la base de datos puede construir llamadas Transact-SQL que usen la instrucción MERGE directamente sin necesidad de realizar dos llamadas de base de datos para INSERT y UPDATE.</span><span class="sxs-lookup"><span data-stu-id="cc532-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="cc532-485">Resumen de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="cc532-485">Recommendation summary</span></span>
<span data-ttu-id="cc532-486">En la lista siguiente, se proporciona un resumen de las recomendaciones de procesamiento por lotes tratadas en este tema:</span><span class="sxs-lookup"><span data-stu-id="cc532-486">The following list provides a summary of the batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="cc532-487">Use el almacenamiento en búfer y el procesamiento por lotes para aumentar el rendimiento y la escalabilidad de las aplicaciones de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cc532-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="cc532-488">Comprenda los compromisos entre el procesamiento por lotes o el almacenamiento en búfer y la resistencia.</span><span class="sxs-lookup"><span data-stu-id="cc532-488">Understand the tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="cc532-489">Durante un error de rol, el riesgo de perder un lote sin procesar de datos esenciales para la empresa podría sobrepasar las ventajas de rendimiento del procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="cc532-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span></span>
* <span data-ttu-id="cc532-490">Intente mantener todas las llamadas a la base de datos dentro de un único centro de datos para reducir la latencia.</span><span class="sxs-lookup"><span data-stu-id="cc532-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span></span>
* <span data-ttu-id="cc532-491">Si elige una técnica de procesamiento con un solo lote, los parámetros con valores de tabla ofrecen el mejor rendimiento y flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="cc532-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span></span>
* <span data-ttu-id="cc532-492">Para lograr el rendimiento de inserción de mayor velocidad, siga estas instrucciones generales y pruebe su escenario:</span><span class="sxs-lookup"><span data-stu-id="cc532-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="cc532-493">Para < 100 filas, use un único comando INSERT con parámetros.</span><span class="sxs-lookup"><span data-stu-id="cc532-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="cc532-494">Para < 1000 filas, use parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="cc532-495">Para > = 1000 filas, use SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="cc532-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="cc532-496">Para las operaciones de actualización y eliminación, use parámetros con valores de tabla con lógica de procedimiento almacenado que determine la operación correcta en cada fila en el parámetro de la tabla.</span><span class="sxs-lookup"><span data-stu-id="cc532-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span></span>
* <span data-ttu-id="cc532-497">Instrucciones para el tamaño de lote:</span><span class="sxs-lookup"><span data-stu-id="cc532-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="cc532-498">Use los tamaños de lote más grandes que tengan sentido para los requisitos de la aplicación y de la empresa.</span><span class="sxs-lookup"><span data-stu-id="cc532-498">Use the largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="cc532-499">Equilibre la ganancia en rendimiento de los lotes grandes con el riesgo de los errores temporales o catastróficos.</span><span class="sxs-lookup"><span data-stu-id="cc532-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="cc532-500">¿Cuál es la consecuencia de los reintentos o la pérdida de datos en el lote?</span><span class="sxs-lookup"><span data-stu-id="cc532-500">What is the consequence of retries or loss of the data in the batch?</span></span> 
  * <span data-ttu-id="cc532-501">Pruebe el tamaño de lote más grande para verificar que Base de datos de SQL no lo rechace.</span><span class="sxs-lookup"><span data-stu-id="cc532-501">Test the largest batch size to verify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="cc532-502">Cree parámetros de configuración que controlen el procesamiento por lotes, como el tamaño del lote o el período de tiempo de almacenamiento en búfer.</span><span class="sxs-lookup"><span data-stu-id="cc532-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span></span> <span data-ttu-id="cc532-503">Estas configuraciones proporcionan flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="cc532-503">These settings provide flexibility.</span></span> <span data-ttu-id="cc532-504">Puede cambiar el comportamiento de procesamiento por lotes en producción sin volver a implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="cc532-504">You can change the batching behavior in production without redeploying the cloud service.</span></span>
* <span data-ttu-id="cc532-505">Evite la ejecución en paralelo de lotes que operan en una sola tabla en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc532-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="cc532-506">Si decide dividir un único lote entre varios subprocesos de trabajo, ejecute pruebas para determinar el número ideal de subprocesos.</span><span class="sxs-lookup"><span data-stu-id="cc532-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span></span> <span data-ttu-id="cc532-507">Después de traspasar un umbral no especificado, el aumento del número de subprocesos hará que el rendimiento disminuya en lugar de mejorarlo.</span><span class="sxs-lookup"><span data-stu-id="cc532-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="cc532-508">Considere la posibilidad de almacenar en búfer por tamaño y hora como una manera de implementar el procesamiento por lotes para más escenarios.</span><span class="sxs-lookup"><span data-stu-id="cc532-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc532-509">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc532-509">Next steps</span></span>
<span data-ttu-id="cc532-510">Este artículo se centra en cómo el diseño de base de datos y las técnicas de codificado relacionadas con el procesamiento por lotes pueden mejorar el rendimiento y la escalabilidad de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cc532-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span></span> <span data-ttu-id="cc532-511">Sin embargo, esto es solamente un factor en la estrategia global.</span><span class="sxs-lookup"><span data-stu-id="cc532-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="cc532-512">Para conocer más formas de mejorar el rendimiento y la escalabilidad, consulte [Guía de rendimiento de Azure SQL Database para bases de datos únicas](sql-database-performance-guidance.md) y [Consideraciones de precio y rendimiento para un grupo elástico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="cc532-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

