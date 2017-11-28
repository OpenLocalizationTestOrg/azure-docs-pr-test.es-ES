---
title: "toouse aaaHow el procesamiento por lotes tooimprove rendimiento de la aplicación de base de datos de SQL Azure"
description: "tema Hello proporciona evidencia de que el procesamiento por lotes de base de datos operaciones en gran medida imroves Hola velocidad y la escalabilidad de las aplicaciones de base de datos de SQL Azure. Aunque estas técnicas de procesamiento por lotes de trabajo para cualquier base de datos de SQL Server, Hola Hola artículo está centrado en Azure."
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
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="84417-104">Cómo toouse tooimprove rendimiento de la aplicación de base de datos SQL de procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="84417-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="84417-105">Procesamiento por lotes operaciones tooAzure base de datos SQL significativamente mejora el rendimiento de Hola y escalabilidad de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="84417-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="84417-106">En ventajas de orden toounderstand hello, primera parte de este artículo de hello cubre algunos resultados de pruebas de ejemplo que comparan solicitudes por lotes y los no secuenciales tooa base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="84417-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="84417-107">Hello resto del artículo hello muestra técnicas de hello, escenarios y consideraciones toohelp toouse procesamiento por lotes correctamente en las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="84417-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="84417-108">¿Por qué es el procesamiento por lotes importante para Base de datos SQL?</span><span class="sxs-lookup"><span data-stu-id="84417-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="84417-109">El servicio remoto tooa llamadas de procesamiento por lotes es una estrategia conocida para aumentar el rendimiento y escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="84417-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="84417-110">Fijos de procesar las interacciones de tooany de costos con un servicio remoto, por ejemplo, la serialización, la transferencia de red y la deserialización.</span><span class="sxs-lookup"><span data-stu-id="84417-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="84417-111">El empaquetado de muchas transacciones diferentes en un único lote minimiza estos costos.</span><span class="sxs-lookup"><span data-stu-id="84417-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="84417-112">En este documento, deseamos tooexamine diversos escenarios y las estrategias de procesamiento por lotes de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="84417-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="84417-113">Aunque estas estrategias también son importantes para las aplicaciones locales que utilizan SQL Server, hay varias razones para resaltar el uso de Hola de procesamiento por lotes para base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="84417-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="84417-114">Hay potencialmente mayor latencia de red al obtener acceso a la base de datos de SQL, especialmente si tiene acceso a base de datos SQL de hello exterior mismo centro de datos de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84417-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="84417-115">características multiempresa de Hola de base de datos SQL decir Hola eficacia de los datos de hello tener acceso a la capa correlaciona toohello escalabilidad global de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="84417-116">Base de datos SQL debe impedir que cualquier inquilino o usuario individual monopolice toohello detrimento de recursos de base de datos de otros inquilinos.</span><span class="sxs-lookup"><span data-stu-id="84417-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="84417-117">En respuesta toousage que superan las cuotas predefinidas, base de datos SQL puede reducir el rendimiento o responder con excepciones de limitación.</span><span class="sxs-lookup"><span data-stu-id="84417-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="84417-118">Las eficiencias, como el procesamiento por lotes, permiten toodo más trabajo en la base de datos SQL antes de alcanzar estos límites.</span><span class="sxs-lookup"><span data-stu-id="84417-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="84417-119">Además, el procesamiento por lotes es efectivo para las arquitecturas que usan varias bases de datos (particionamiento).</span><span class="sxs-lookup"><span data-stu-id="84417-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="84417-120">eficacia de saludo de la interacción con cada unidad de base de datos sigue siendo un factor clave para la escalabilidad global.</span><span class="sxs-lookup"><span data-stu-id="84417-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="84417-121">Una de las ventajas de hello del uso de la base de datos SQL es que no tiene servidores de hello toomanage esa base de datos de Hola de host.</span><span class="sxs-lookup"><span data-stu-id="84417-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="84417-122">Sin embargo, esta infraestructura administrada significa también que haya toothink diferente acerca de las optimizaciones de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="84417-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="84417-123">Ya no se puede buscar la infraestructura de red o de hardware de la base de datos del hello tooimprove.</span><span class="sxs-lookup"><span data-stu-id="84417-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="84417-124">porque Microsoft Azure controla esos entornos.</span><span class="sxs-lookup"><span data-stu-id="84417-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="84417-125">área principal de Hola que puede controlar es cómo interactúa la aplicación con la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="84417-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="84417-126">El procesamiento por lotes es una de estas optimizaciones.</span><span class="sxs-lookup"><span data-stu-id="84417-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="84417-127">primera parte de Hola de papel Hola examina diversas técnicas de procesamiento por lotes para aplicaciones de .NET que usan la base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="84417-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="84417-128">Hola dos últimas secciones tratan instrucciones y escenarios de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="84417-129">Estrategias de procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="84417-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="84417-130">Nota sobre los tiempos resultantes en este tema</span><span class="sxs-lookup"><span data-stu-id="84417-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="84417-131">Resultados no son pruebas comparativas sino que pretenden tooshow **rendimiento relativo**.</span><span class="sxs-lookup"><span data-stu-id="84417-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="84417-132">Los tiempos se basan en un promedio de un mínimo de 10 series de pruebas.</span><span class="sxs-lookup"><span data-stu-id="84417-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="84417-133">Las operaciones son inserciones en una tabla vacía.</span><span class="sxs-lookup"><span data-stu-id="84417-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="84417-134">Estas pruebas se pre-V12 medido, y no corresponde necesariamente toothroughput que pueden producirse en una base de datos de V12 mediante Hola nueva [niveles de servicio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="84417-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="84417-135">beneficio relativo de Hola de hello técnica de procesamiento por lotes debe ser similar.</span><span class="sxs-lookup"><span data-stu-id="84417-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="84417-136">Transacciones</span><span class="sxs-lookup"><span data-stu-id="84417-136">Transactions</span></span>
<span data-ttu-id="84417-137">Parece extraño toobegin una revisión del procesamiento por lotes hablando de transacciones.</span><span class="sxs-lookup"><span data-stu-id="84417-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="84417-138">Pero el uso de Hola de transacciones de cliente tiene un efecto de procesamiento por lotes de servidor sutil que mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84417-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="84417-139">Y las transacciones se pueden agregar con solo unas pocas líneas de código, lo que proporciona un rendimiento de tooimprove de forma más rápida de las operaciones secuenciales.</span><span class="sxs-lookup"><span data-stu-id="84417-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="84417-140">Tenga en cuenta el siguiente código de C# que contiene una secuencia de inserción de Hola y operaciones update en una tabla sencilla.</span><span class="sxs-lookup"><span data-stu-id="84417-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="84417-141">Hola después el código de ADO.NET secuencialmente realiza estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="84417-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="84417-142">Hola toooptimize de manera mejor este código es tooimplement alguna forma de procesamiento por lotes del lado cliente de estas llamadas.</span><span class="sxs-lookup"><span data-stu-id="84417-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="84417-143">Pero hay una manera sencilla tooincrease Hola de rendimiento de este código ajustando simplemente secuencia Hola de llamadas en una transacción.</span><span class="sxs-lookup"><span data-stu-id="84417-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="84417-144">Aquí es Hola mismo código que usa una transacción.</span><span class="sxs-lookup"><span data-stu-id="84417-144">Here is hello same code that uses a transaction.</span></span>

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

<span data-ttu-id="84417-145">Realmente, se usan transacciones en ambos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="84417-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="84417-146">En el primer ejemplo de Hola, cada llamada individual es una transacción implícita.</span><span class="sxs-lookup"><span data-stu-id="84417-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="84417-147">En el segundo ejemplo de Hola, una transacción explícita ajusta todas las llamadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="84417-148">Por documentación Hola Hola [registro de transacciones de escritura anticipada](https://msdn.microsoft.com/library/ms186259.aspx), entradas de registro son toohello vaciado disco cuando se confirma la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="84417-149">Por lo que al incluir más llamadas en una transacción, hello registro de transacciones de escritura toohello puede retrasar hasta que se confirma la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="84417-150">En efecto, va a habilitar el procesamiento por lotes para el registro de transacciones del servidor de hello escrituras toohello.</span><span class="sxs-lookup"><span data-stu-id="84417-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="84417-151">Hello en la tabla siguiente muestra algunos resultados de pruebas ad hoc.</span><span class="sxs-lookup"><span data-stu-id="84417-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="84417-152">pruebas de Hello realizan Hola que mismo secuencial inserta con y sin transacciones.</span><span class="sxs-lookup"><span data-stu-id="84417-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="84417-153">Para tener más perspectiva, primer conjunto de pruebas de hello ejecutó remotamente desde una base de datos de toohello portátil en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84417-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="84417-154">Hello segundo conjunto de pruebas se ejecutaba desde un servicio en la nube y la base de datos que residían en hello mismo centro de datos de Microsoft Azure (US occidental).</span><span class="sxs-lookup"><span data-stu-id="84417-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="84417-155">Hello siguiente tabla muestra hello duración en milisegundos de inserciones secuenciales con y sin transacciones.</span><span class="sxs-lookup"><span data-stu-id="84417-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="84417-156">**TooAzure local**:</span><span class="sxs-lookup"><span data-stu-id="84417-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="84417-157">Operaciones</span><span class="sxs-lookup"><span data-stu-id="84417-157">Operations</span></span> | <span data-ttu-id="84417-158">Ninguna transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-158">No Transaction (ms)</span></span> | <span data-ttu-id="84417-159">Transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84417-160">1</span><span class="sxs-lookup"><span data-stu-id="84417-160">1</span></span> |<span data-ttu-id="84417-161">130</span><span class="sxs-lookup"><span data-stu-id="84417-161">130</span></span> |<span data-ttu-id="84417-162">402</span><span class="sxs-lookup"><span data-stu-id="84417-162">402</span></span> |
| <span data-ttu-id="84417-163">10</span><span class="sxs-lookup"><span data-stu-id="84417-163">10</span></span> |<span data-ttu-id="84417-164">1208</span><span class="sxs-lookup"><span data-stu-id="84417-164">1208</span></span> |<span data-ttu-id="84417-165">1226</span><span class="sxs-lookup"><span data-stu-id="84417-165">1226</span></span> |
| <span data-ttu-id="84417-166">100</span><span class="sxs-lookup"><span data-stu-id="84417-166">100</span></span> |<span data-ttu-id="84417-167">12662</span><span class="sxs-lookup"><span data-stu-id="84417-167">12662</span></span> |<span data-ttu-id="84417-168">10395</span><span class="sxs-lookup"><span data-stu-id="84417-168">10395</span></span> |
| <span data-ttu-id="84417-169">1000</span><span class="sxs-lookup"><span data-stu-id="84417-169">1000</span></span> |<span data-ttu-id="84417-170">128852</span><span class="sxs-lookup"><span data-stu-id="84417-170">128852</span></span> |<span data-ttu-id="84417-171">102917</span><span class="sxs-lookup"><span data-stu-id="84417-171">102917</span></span> |

<span data-ttu-id="84417-172">**Azure tooAzure (mismo centro de datos)**:</span><span class="sxs-lookup"><span data-stu-id="84417-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="84417-173">Operaciones</span><span class="sxs-lookup"><span data-stu-id="84417-173">Operations</span></span> | <span data-ttu-id="84417-174">Ninguna transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-174">No Transaction (ms)</span></span> | <span data-ttu-id="84417-175">Transacción (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84417-176">1</span><span class="sxs-lookup"><span data-stu-id="84417-176">1</span></span> |<span data-ttu-id="84417-177">21</span><span class="sxs-lookup"><span data-stu-id="84417-177">21</span></span> |<span data-ttu-id="84417-178">26</span><span class="sxs-lookup"><span data-stu-id="84417-178">26</span></span> |
| <span data-ttu-id="84417-179">10</span><span class="sxs-lookup"><span data-stu-id="84417-179">10</span></span> |<span data-ttu-id="84417-180">220</span><span class="sxs-lookup"><span data-stu-id="84417-180">220</span></span> |<span data-ttu-id="84417-181">56</span><span class="sxs-lookup"><span data-stu-id="84417-181">56</span></span> |
| <span data-ttu-id="84417-182">100</span><span class="sxs-lookup"><span data-stu-id="84417-182">100</span></span> |<span data-ttu-id="84417-183">2145</span><span class="sxs-lookup"><span data-stu-id="84417-183">2145</span></span> |<span data-ttu-id="84417-184">341</span><span class="sxs-lookup"><span data-stu-id="84417-184">341</span></span> |
| <span data-ttu-id="84417-185">1000</span><span class="sxs-lookup"><span data-stu-id="84417-185">1000</span></span> |<span data-ttu-id="84417-186">21479</span><span class="sxs-lookup"><span data-stu-id="84417-186">21479</span></span> |<span data-ttu-id="84417-187">2756</span><span class="sxs-lookup"><span data-stu-id="84417-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="84417-188">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="84417-188">Results are not benchmarks.</span></span> <span data-ttu-id="84417-189">Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="84417-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="84417-190">En función de los resultados de pruebas anteriores hello, ajustar una única operación en una transacción reduce realmente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84417-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="84417-191">Pero medida que aumenta el número de Hola de operaciones en una única transacción, la mejora del rendimiento Hola se vuelve más marcada.</span><span class="sxs-lookup"><span data-stu-id="84417-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="84417-192">diferencia de rendimiento de Hello también es más destacable cuando todas las operaciones se producen en el centro de datos de hello Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84417-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="84417-193">Hello mayor latencia del uso de base de datos SQL desde el centro de datos de Microsoft Azure Hola exterior oculta mejora del rendimiento Hola de utilizar transacciones.</span><span class="sxs-lookup"><span data-stu-id="84417-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="84417-194">Aunque el uso de Hola de transacciones puede aumentar el rendimiento, continuar demasiado[observando las prácticas recomendadas para las conexiones y transacciones](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="84417-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="84417-195">Mantener transacciones hello más corta como conexión de base de datos de hello posible y, a continuación, cierre después de que el trabajo de hello completa.</span><span class="sxs-lookup"><span data-stu-id="84417-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="84417-196">Hola utilizando la instrucción en el ejemplo anterior de hello garantiza que se cierra la conexión de hello cuando finaliza el bloque de código siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="84417-197">ejemplo de Hola anterior muestra que puede agregar un código de ADO.NET de transacción local tooany con dos líneas.</span><span class="sxs-lookup"><span data-stu-id="84417-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="84417-198">Las transacciones ofrecen una forma rápida de rendimiento de hello tooimprove del código que realiza secuencial inserciones, actualizaciones y las operaciones de eliminación.</span><span class="sxs-lookup"><span data-stu-id="84417-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="84417-199">Sin embargo, para lograr rendimiento hello, considere la posibilidad de cambiar Hola código tootake ventaja adicional de procesamiento por lotes de cliente, como los parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="84417-200">Para obtener más información acerca de las transacciones en ADO.NET, consulte [Transacciones locales](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="84417-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="84417-201">Parámetros con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="84417-201">Table-valued parameters</span></span>
<span data-ttu-id="84417-202">Los parámetros con valores de tabla admiten tipos de tabla definidos por el usuario como parámetros en instrucciones Transact-SQL, procedimientos almacenados y funciones.</span><span class="sxs-lookup"><span data-stu-id="84417-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="84417-203">Esta técnica de procesamiento por lotes del lado cliente permite toosend varias filas de datos de parámetro con valores de tabla de hello.</span><span class="sxs-lookup"><span data-stu-id="84417-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="84417-204">parámetros con valores de tabla toouse, definir un tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="84417-205">Hola después de la instrucción Transact-SQL crea un tipo de tabla denominado **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="84417-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="84417-206">En código, cree un **DataTable** con hello exactamente los mismos nombres y tipos de tipo de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="84417-207">Pase este **DataTable** en un parámetro de una consulta de texto o una llamada de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="84417-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="84417-208">Hello en el ejemplo siguiente se muestra esta técnica:</span><span class="sxs-lookup"><span data-stu-id="84417-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
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

<span data-ttu-id="84417-209">En el ejemplo anterior de hello, Hola **SqlCommand** objeto inserta filas de un parámetro con valores de tabla,  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="84417-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="84417-210">Hola creado anteriormente **DataTable** se asigna al objeto parámetro toothis con hello **SqlCommand.Parameters.Add** método.</span><span class="sxs-lookup"><span data-stu-id="84417-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="84417-211">Procesamiento por lotes inserciones de hello en uno llamar a significativamente aumenta Hola de rendimiento a través de las inserciones secuenciales.</span><span class="sxs-lookup"><span data-stu-id="84417-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="84417-212">tooimprove Hola ejemplo anterior aún más, utilice un procedimiento almacenado en lugar de un comando basado en texto.</span><span class="sxs-lookup"><span data-stu-id="84417-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="84417-213">Hola siguiente comando de Transact-SQL crea un procedimiento almacenado que toma hello **SimpleTestTableType** parámetro con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="84417-214">A continuación, cambie hello **SqlCommand** declaración en siguiente para toohello de ejemplo anterior código de hello del objeto.</span><span class="sxs-lookup"><span data-stu-id="84417-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="84417-215">En la mayoría de los casos, los parámetros con valores de tabla tienen un rendimiento equivalente o mejor que otras técnicas de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="84417-216">Los parámetros con valores de tabla son a menudo preferibles, ya que son más flexibles que otras opciones.</span><span class="sxs-lookup"><span data-stu-id="84417-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="84417-217">Por ejemplo, otras técnicas como la copia masiva de SQL sólo permiten inserción Hola de filas nuevas.</span><span class="sxs-lookup"><span data-stu-id="84417-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="84417-218">Pero con parámetros con valores de tabla, puede usar lógica en toodetermine de procedimiento almacenado de hello qué filas son actualizaciones y que son inserciones.</span><span class="sxs-lookup"><span data-stu-id="84417-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="84417-219">tipo de tabla de Hello también puede ser modificado toocontain una columna "Operación" que indica si Hola especifica fila debe insertarlos, actualizarlos o eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="84417-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="84417-220">Hello en la tabla siguiente muestra los resultados de pruebas ad hoc para su uso de Hola de parámetros con valores de tabla en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="84417-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="84417-221">Operaciones</span><span class="sxs-lookup"><span data-stu-id="84417-221">Operations</span></span> | <span data-ttu-id="84417-222">TooAzure local (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="84417-223">Azure en el mismo centro de datos (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84417-224">1</span><span class="sxs-lookup"><span data-stu-id="84417-224">1</span></span> |<span data-ttu-id="84417-225">124</span><span class="sxs-lookup"><span data-stu-id="84417-225">124</span></span> |<span data-ttu-id="84417-226">32</span><span class="sxs-lookup"><span data-stu-id="84417-226">32</span></span> |
| <span data-ttu-id="84417-227">10</span><span class="sxs-lookup"><span data-stu-id="84417-227">10</span></span> |<span data-ttu-id="84417-228">131</span><span class="sxs-lookup"><span data-stu-id="84417-228">131</span></span> |<span data-ttu-id="84417-229">25</span><span class="sxs-lookup"><span data-stu-id="84417-229">25</span></span> |
| <span data-ttu-id="84417-230">100</span><span class="sxs-lookup"><span data-stu-id="84417-230">100</span></span> |<span data-ttu-id="84417-231">338</span><span class="sxs-lookup"><span data-stu-id="84417-231">338</span></span> |<span data-ttu-id="84417-232">51</span><span class="sxs-lookup"><span data-stu-id="84417-232">51</span></span> |
| <span data-ttu-id="84417-233">1000</span><span class="sxs-lookup"><span data-stu-id="84417-233">1000</span></span> |<span data-ttu-id="84417-234">2615</span><span class="sxs-lookup"><span data-stu-id="84417-234">2615</span></span> |<span data-ttu-id="84417-235">382</span><span class="sxs-lookup"><span data-stu-id="84417-235">382</span></span> |
| <span data-ttu-id="84417-236">10000</span><span class="sxs-lookup"><span data-stu-id="84417-236">10000</span></span> |<span data-ttu-id="84417-237">23830</span><span class="sxs-lookup"><span data-stu-id="84417-237">23830</span></span> |<span data-ttu-id="84417-238">3586</span><span class="sxs-lookup"><span data-stu-id="84417-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="84417-239">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="84417-239">Results are not benchmarks.</span></span> <span data-ttu-id="84417-240">Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="84417-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="84417-241">Hola mejora del rendimiento de procesamiento por lotes es evidente inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="84417-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="84417-242">En la prueba secuencial anterior hello, 1000 operaciones tardaban 129 segundos fuera Hola datacenter y 21 segundos dentro del centro de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="84417-243">Pero con los parámetros con valores de tabla, 1000 operaciones aprovechar solo 2,6 segundos fuera del centro de datos de Hola y 0,4 segundos dentro del centro de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="84417-244">Para obtener más información sobre los parámetros con valores de tabla, consulte [Usar parámetros con valores de tabla (motor de base de datos)](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="84417-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="84417-245">Copia masiva de SQL</span><span class="sxs-lookup"><span data-stu-id="84417-245">SQL bulk copy</span></span>
<span data-ttu-id="84417-246">Copia masiva de SQL es otra manera tooinsert grandes cantidades de datos en una base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="84417-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="84417-247">Las aplicaciones .NET pueden utilizar hello **SqlBulkCopy** operaciones de inserción masiva de tooperform de clase.</span><span class="sxs-lookup"><span data-stu-id="84417-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="84417-248">**SqlBulkCopy** es similar en la herramienta de línea de comandos de función toohello, **Bcp.exe**, o instrucción de Transact-SQL, hello **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="84417-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="84417-249">Hello ejemplo de código siguiente muestra cómo toobulk Hola de copiar filas de origen de hello **DataTable**, tabla, tabla de destino toohello en SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="84417-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

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

<span data-ttu-id="84417-250">Hay algunos casos en que la copia masiva es preferible a los parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="84417-251">Vea la tabla de comparación de Hola de parámetros con valores de tabla frente a las operaciones BULK INSERT en el tema de hello [parámetros con valores de tabla](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="84417-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="84417-252">Hello resultados de pruebas ad hoc siguientes muestran rendimiento de Hola de procesamiento por lotes con **SqlBulkCopy** en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="84417-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="84417-253">Operaciones</span><span class="sxs-lookup"><span data-stu-id="84417-253">Operations</span></span> | <span data-ttu-id="84417-254">TooAzure local (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="84417-255">Azure en el mismo centro de datos (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84417-256">1</span><span class="sxs-lookup"><span data-stu-id="84417-256">1</span></span> |<span data-ttu-id="84417-257">433</span><span class="sxs-lookup"><span data-stu-id="84417-257">433</span></span> |<span data-ttu-id="84417-258">57</span><span class="sxs-lookup"><span data-stu-id="84417-258">57</span></span> |
| <span data-ttu-id="84417-259">10</span><span class="sxs-lookup"><span data-stu-id="84417-259">10</span></span> |<span data-ttu-id="84417-260">441</span><span class="sxs-lookup"><span data-stu-id="84417-260">441</span></span> |<span data-ttu-id="84417-261">32</span><span class="sxs-lookup"><span data-stu-id="84417-261">32</span></span> |
| <span data-ttu-id="84417-262">100</span><span class="sxs-lookup"><span data-stu-id="84417-262">100</span></span> |<span data-ttu-id="84417-263">636</span><span class="sxs-lookup"><span data-stu-id="84417-263">636</span></span> |<span data-ttu-id="84417-264">53</span><span class="sxs-lookup"><span data-stu-id="84417-264">53</span></span> |
| <span data-ttu-id="84417-265">1000</span><span class="sxs-lookup"><span data-stu-id="84417-265">1000</span></span> |<span data-ttu-id="84417-266">2535</span><span class="sxs-lookup"><span data-stu-id="84417-266">2535</span></span> |<span data-ttu-id="84417-267">341</span><span class="sxs-lookup"><span data-stu-id="84417-267">341</span></span> |
| <span data-ttu-id="84417-268">10000</span><span class="sxs-lookup"><span data-stu-id="84417-268">10000</span></span> |<span data-ttu-id="84417-269">21605</span><span class="sxs-lookup"><span data-stu-id="84417-269">21605</span></span> |<span data-ttu-id="84417-270">2737</span><span class="sxs-lookup"><span data-stu-id="84417-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="84417-271">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="84417-271">Results are not benchmarks.</span></span> <span data-ttu-id="84417-272">Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="84417-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="84417-273">En tamaños de lote menores, parámetros con valores de tabla de uso de hello superó hello **SqlBulkCopy** clase.</span><span class="sxs-lookup"><span data-stu-id="84417-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="84417-274">Sin embargo, **SqlBulkCopy** realiza 12-31% más rápido que los parámetros con valores de tabla para las pruebas de Hola de 1.000 y 10.000 filas.</span><span class="sxs-lookup"><span data-stu-id="84417-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="84417-275">Como los parámetros con valores de tabla, **SqlBulkCopy** es una buena opción para las inserciones por lotes, especialmente cuando se comparan toohello rendimiento de operaciones por lotes no.</span><span class="sxs-lookup"><span data-stu-id="84417-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="84417-276">Para obtener más información sobre la copia masiva en ADO.NET, consulte [Operaciones de copia masiva en SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="84417-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="84417-277">Instrucciones INSERT con parámetros de varias filas</span><span class="sxs-lookup"><span data-stu-id="84417-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="84417-278">Una alternativa para los lotes pequeños es tooconstruct una gran parametrizar la instrucción INSERT que inserta varias filas.</span><span class="sxs-lookup"><span data-stu-id="84417-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="84417-279">Hola, ejemplo de código siguiente muestra esta técnica.</span><span class="sxs-lookup"><span data-stu-id="84417-279">hello following code example demonstrates this technique.</span></span>

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


<span data-ttu-id="84417-280">Este ejemplo está pensado concepto básico de tooshow Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="84417-281">Un escenario más realista se recorre en bucle Hola necesario entidades tooconstruct Hola cadena de consulta y parámetros de comando de hello simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="84417-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="84417-282">Está limitado tooa total de 2100 parámetros de consulta, lo que se limita el número total de Hola de filas que se pueden procesar de esta manera.</span><span class="sxs-lookup"><span data-stu-id="84417-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="84417-283">Hola tras la ejecución ad hoc prueba resultados mostrar hello de este tipo de instrucción de inserción en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="84417-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="84417-284">Operaciones</span><span class="sxs-lookup"><span data-stu-id="84417-284">Operations</span></span> | <span data-ttu-id="84417-285">Parámetros con valores de tabla (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="84417-286">Instrucción INSERT única (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84417-287">1</span><span class="sxs-lookup"><span data-stu-id="84417-287">1</span></span> |<span data-ttu-id="84417-288">32</span><span class="sxs-lookup"><span data-stu-id="84417-288">32</span></span> |<span data-ttu-id="84417-289">20</span><span class="sxs-lookup"><span data-stu-id="84417-289">20</span></span> |
| <span data-ttu-id="84417-290">10</span><span class="sxs-lookup"><span data-stu-id="84417-290">10</span></span> |<span data-ttu-id="84417-291">30</span><span class="sxs-lookup"><span data-stu-id="84417-291">30</span></span> |<span data-ttu-id="84417-292">25</span><span class="sxs-lookup"><span data-stu-id="84417-292">25</span></span> |
| <span data-ttu-id="84417-293">100</span><span class="sxs-lookup"><span data-stu-id="84417-293">100</span></span> |<span data-ttu-id="84417-294">33</span><span class="sxs-lookup"><span data-stu-id="84417-294">33</span></span> |<span data-ttu-id="84417-295">51</span><span class="sxs-lookup"><span data-stu-id="84417-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="84417-296">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="84417-296">Results are not benchmarks.</span></span> <span data-ttu-id="84417-297">Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="84417-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="84417-298">Este enfoque puede ser algo más rápido para los lotes de menos de 100 filas.</span><span class="sxs-lookup"><span data-stu-id="84417-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="84417-299">Aunque Hola mejora es pequeña, esta técnica es otra opción que podría funcionar bien en el escenario de aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="84417-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="84417-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="84417-300">DataAdapter</span></span>
<span data-ttu-id="84417-301">Hola **DataAdapter** clase le permite toomodify una **conjunto de datos** de objeto y, a continuación, enviar cambios de hello como operaciones INSERT, UPDATE y DELETE.</span><span class="sxs-lookup"><span data-stu-id="84417-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="84417-302">Si usas hello **DataAdapter** de esta manera, es importante toonote que separan las llamadas se realizan para cada operación.</span><span class="sxs-lookup"><span data-stu-id="84417-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="84417-303">tooimprove rendimiento, use hello **UpdateBatchSize** número de toohello de propiedad de las operaciones que deben procesarse por lotes a la vez.</span><span class="sxs-lookup"><span data-stu-id="84417-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="84417-304">Para obtener más información, consulte [Realizar operaciones por lotes mediante DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="84417-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="84417-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="84417-305">Entity framework</span></span>
<span data-ttu-id="84417-306">Actualmente, Entity Framework no admite el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="84417-307">Varios desarrolladores de la Comunidad de hello han intentado toodemonstrate las soluciones alternativas, como invalidación hello **SaveChanges** método.</span><span class="sxs-lookup"><span data-stu-id="84417-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="84417-308">Pero Hola soluciones suelen ser complejas y personalizadas toohello aplicación y el modelo de datos.</span><span class="sxs-lookup"><span data-stu-id="84417-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="84417-309">proyecto de codeplex de Entity Framework Hola actualmente tiene una página de conversación en esta solicitud de característica.</span><span class="sxs-lookup"><span data-stu-id="84417-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="84417-310">tooview esta explicación, consulte [notas de la reunión de diseño - 2 de agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="84417-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="84417-311">XML</span><span class="sxs-lookup"><span data-stu-id="84417-311">XML</span></span>
<span data-ttu-id="84417-312">Por integridad, creemos que es importante tootalk sobre XML como una estrategia de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="84417-313">Sin embargo, el uso de Hola de XML tiene ningún ventajas sobre otros métodos y varias desventajas.</span><span class="sxs-lookup"><span data-stu-id="84417-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="84417-314">Hola consiste parámetros con valores de tootable similares, pero un archivo XML o una cadena se pasa el procedimiento almacenado de tooa en lugar de una tabla definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="84417-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="84417-315">procedimiento almacenado de Hello analiza los comandos de hello en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="84417-316">Hay varias desventajas toothis enfoque:</span><span class="sxs-lookup"><span data-stu-id="84417-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="84417-317">El trabajo con XML puede resultar tedioso y propenso a errores.</span><span class="sxs-lookup"><span data-stu-id="84417-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="84417-318">Hola análisis XML en la base de datos de hello puede usar mucha CPU.</span><span class="sxs-lookup"><span data-stu-id="84417-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="84417-319">En la mayoría de los casos, este método es más lento que los parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="84417-320">Por estos motivos, no se recomienda el uso de Hola de XML para las consultas del lote.</span><span class="sxs-lookup"><span data-stu-id="84417-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="84417-321">Consideraciones sobre el procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="84417-321">Batching considerations</span></span>
<span data-ttu-id="84417-322">Hola las secciones siguientes proporciona más instrucciones para el uso de Hola de procesamiento por lotes en las aplicaciones de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="84417-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="84417-323">Compromisos</span><span class="sxs-lookup"><span data-stu-id="84417-323">Tradeoffs</span></span>
<span data-ttu-id="84417-324">Según la arquitectura, el procesamiento por lotes puede suponer un compromiso entre el rendimiento y la resistencia.</span><span class="sxs-lookup"><span data-stu-id="84417-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="84417-325">Por ejemplo, considere el escenario de Hola donde su rol deja de funcionar inesperadamente.</span><span class="sxs-lookup"><span data-stu-id="84417-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="84417-326">Si pierde una fila de datos, impacto hello es menor que el impacto de Hola de perder un lote grande de filas sin enviar.</span><span class="sxs-lookup"><span data-stu-id="84417-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="84417-327">Hay un riesgo mayor cuando almacena filas en búfer antes de enviarlos toohello base de datos en un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="84417-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="84417-328">Debido a esta contrapartida, evalúe el tipo de Hola de operaciones que procesa por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="84417-329">Intensifique el procesamiento por lotes (con lotes y períodos de tiempo mayores) con aquellos datos que sean menos críticos.</span><span class="sxs-lookup"><span data-stu-id="84417-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="84417-330">Tamaño de lote</span><span class="sxs-lookup"><span data-stu-id="84417-330">Batch size</span></span>
<span data-ttu-id="84417-331">En nuestras pruebas, normalmente no había ningún lote grande de toobreaking ventaja en fragmentos menores.</span><span class="sxs-lookup"><span data-stu-id="84417-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="84417-332">De hecho, esta subdivisión produjo a menudo un rendimiento más lento que el envío de un único lote grande.</span><span class="sxs-lookup"><span data-stu-id="84417-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="84417-333">Por ejemplo, considere un escenario donde desea tooinsert 1000 filas.</span><span class="sxs-lookup"><span data-stu-id="84417-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="84417-334">Hello siguiente tabla muestra el tiempo que tarda parámetros con valores de tabla de toouse tooinsert 1000 filas cuando se divide en lotes más pequeños.</span><span class="sxs-lookup"><span data-stu-id="84417-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="84417-335">Tamaño de lote</span><span class="sxs-lookup"><span data-stu-id="84417-335">Batch size</span></span> | <span data-ttu-id="84417-336">Iteraciones</span><span class="sxs-lookup"><span data-stu-id="84417-336">Iterations</span></span> | <span data-ttu-id="84417-337">Parámetros con valores de tabla (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84417-338">1000</span><span class="sxs-lookup"><span data-stu-id="84417-338">1000</span></span> |<span data-ttu-id="84417-339">1</span><span class="sxs-lookup"><span data-stu-id="84417-339">1</span></span> |<span data-ttu-id="84417-340">347</span><span class="sxs-lookup"><span data-stu-id="84417-340">347</span></span> |
| <span data-ttu-id="84417-341">500</span><span class="sxs-lookup"><span data-stu-id="84417-341">500</span></span> |<span data-ttu-id="84417-342">2</span><span class="sxs-lookup"><span data-stu-id="84417-342">2</span></span> |<span data-ttu-id="84417-343">355</span><span class="sxs-lookup"><span data-stu-id="84417-343">355</span></span> |
| <span data-ttu-id="84417-344">100</span><span class="sxs-lookup"><span data-stu-id="84417-344">100</span></span> |<span data-ttu-id="84417-345">10</span><span class="sxs-lookup"><span data-stu-id="84417-345">10</span></span> |<span data-ttu-id="84417-346">465</span><span class="sxs-lookup"><span data-stu-id="84417-346">465</span></span> |
| <span data-ttu-id="84417-347">50</span><span class="sxs-lookup"><span data-stu-id="84417-347">50</span></span> |<span data-ttu-id="84417-348">20</span><span class="sxs-lookup"><span data-stu-id="84417-348">20</span></span> |<span data-ttu-id="84417-349">630</span><span class="sxs-lookup"><span data-stu-id="84417-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="84417-350">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="84417-350">Results are not benchmarks.</span></span> <span data-ttu-id="84417-351">Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="84417-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="84417-352">Puede ver el que obtener el mejor rendimiento para 1000 filas de hello toosubmit ellos a la vez.</span><span class="sxs-lookup"><span data-stu-id="84417-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="84417-353">En otras pruebas (no mostradas aquí) hubo una toobreak de ganancia de rendimiento de pequeñas un lote de 10.000 filas en dos lotes de 5000.</span><span class="sxs-lookup"><span data-stu-id="84417-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="84417-354">Pero el esquema de la tabla de Hola para estas pruebas es relativamente simple, por lo que debe realizar pruebas en los datos específicos y tooverify de tamaños de lote estos hallazgos.</span><span class="sxs-lookup"><span data-stu-id="84417-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="84417-355">Tooconsider de otro factor es que si el lote total de hello es demasiado grande, base de datos SQL puede limitar y rechazar por lotes de hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="84417-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="84417-356">Para obtener mejores resultados de hello, probar su escenario concreto toodetermine si hay un tamaño de lote ideal.</span><span class="sxs-lookup"><span data-stu-id="84417-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="84417-357">Hacer que el tamaño del lote de hello configurable en tiempo de ejecución tooenable ajustes rápidos en función del rendimiento o de errores.</span><span class="sxs-lookup"><span data-stu-id="84417-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="84417-358">Por último, sopese tamaño Hola de lote de Hola y riesgos de hello asociados al procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="84417-359">Si hay errores transitorios o se produce un error en la función hello, considere la posibilidad de consecuencias de Hola de volver a intentar la operación de Hola o de pérdida de datos de hello en lote Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="84417-360">Procesamiento en paralelo</span><span class="sxs-lookup"><span data-stu-id="84417-360">Parallel processing</span></span>
<span data-ttu-id="84417-361">¿Qué ocurre si tardó enfoque Hola de reducir el tamaño del lote de hello pero utiliza varios subprocesos tooexecute Hola trabajo?</span><span class="sxs-lookup"><span data-stu-id="84417-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="84417-362">Una vez más, nuestras pruebas mostraron que varios lotes multiproceso más pequeños presentaban normalmente un rendimiento peor que un único lote más grande.</span><span class="sxs-lookup"><span data-stu-id="84417-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="84417-363">Hello prueba siguiente intenta tooinsert 1000 filas en uno o varios lotes paralelos.</span><span class="sxs-lookup"><span data-stu-id="84417-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="84417-364">Esta prueba muestra cómo el uso de más lotes simultáneos realmente reduce el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84417-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="84417-365">Tamaño de lote [iteraciones]</span><span class="sxs-lookup"><span data-stu-id="84417-365">Batch size [Iterations]</span></span> | <span data-ttu-id="84417-366">Dos subprocesos (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-366">Two threads (ms)</span></span> | <span data-ttu-id="84417-367">Cuatro subprocesos (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-367">Four threads (ms)</span></span> | <span data-ttu-id="84417-368">Seis subprocesos (ms)</span><span class="sxs-lookup"><span data-stu-id="84417-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="84417-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="84417-369">1000 [1]</span></span> |<span data-ttu-id="84417-370">277</span><span class="sxs-lookup"><span data-stu-id="84417-370">277</span></span> |<span data-ttu-id="84417-371">315</span><span class="sxs-lookup"><span data-stu-id="84417-371">315</span></span> |<span data-ttu-id="84417-372">266</span><span class="sxs-lookup"><span data-stu-id="84417-372">266</span></span> |
| <span data-ttu-id="84417-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="84417-373">500 [2]</span></span> |<span data-ttu-id="84417-374">548</span><span class="sxs-lookup"><span data-stu-id="84417-374">548</span></span> |<span data-ttu-id="84417-375">278</span><span class="sxs-lookup"><span data-stu-id="84417-375">278</span></span> |<span data-ttu-id="84417-376">256</span><span class="sxs-lookup"><span data-stu-id="84417-376">256</span></span> |
| <span data-ttu-id="84417-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="84417-377">250 [4]</span></span> |<span data-ttu-id="84417-378">405</span><span class="sxs-lookup"><span data-stu-id="84417-378">405</span></span> |<span data-ttu-id="84417-379">329</span><span class="sxs-lookup"><span data-stu-id="84417-379">329</span></span> |<span data-ttu-id="84417-380">265</span><span class="sxs-lookup"><span data-stu-id="84417-380">265</span></span> |
| <span data-ttu-id="84417-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="84417-381">100 [10]</span></span> |<span data-ttu-id="84417-382">488</span><span class="sxs-lookup"><span data-stu-id="84417-382">488</span></span> |<span data-ttu-id="84417-383">439</span><span class="sxs-lookup"><span data-stu-id="84417-383">439</span></span> |<span data-ttu-id="84417-384">391</span><span class="sxs-lookup"><span data-stu-id="84417-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="84417-385">Los resultados no sirven para pruebas comparativas.</span><span class="sxs-lookup"><span data-stu-id="84417-385">Results are not benchmarks.</span></span> <span data-ttu-id="84417-386">Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="84417-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="84417-387">Hay varias razones posibles para la degradación de hello en rendimiento due tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="84417-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="84417-388">Se realizan varias llamadas de red simultáneas en lugar de una.</span><span class="sxs-lookup"><span data-stu-id="84417-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="84417-389">Varias operaciones en una sola tabla pueden conllevar contención y bloqueo.</span><span class="sxs-lookup"><span data-stu-id="84417-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="84417-390">Hay sobrecargas asociadas con el subprocesamiento múltiple.</span><span class="sxs-lookup"><span data-stu-id="84417-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="84417-391">gastos de Hello supone abrir varias conexiones supera con creces las ventajas de Hola de procesamiento en paralelo.</span><span class="sxs-lookup"><span data-stu-id="84417-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="84417-392">Si elige como destino diferentes tablas o bases de datos, es posible toosee el aumento del rendimiento con esta estrategia.</span><span class="sxs-lookup"><span data-stu-id="84417-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="84417-393">Un escenario de particionamiento de base de datos o de federaciones sería adecuado para este enfoque.</span><span class="sxs-lookup"><span data-stu-id="84417-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="84417-394">Particionamiento utiliza varias bases de datos y base de datos de tooeach de datos diferentes de las rutas.</span><span class="sxs-lookup"><span data-stu-id="84417-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="84417-395">Si cada lote pequeño va tooa otra base de datos, puede ser más eficaz, a continuación, realizar operaciones de hello en paralelo.</span><span class="sxs-lookup"><span data-stu-id="84417-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="84417-396">Sin embargo, ganancia de rendimiento de hello no es toouse suficientemente importante como base de Hola para un particionamiento de base de datos de toouse de decisión de la solución.</span><span class="sxs-lookup"><span data-stu-id="84417-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="84417-397">En algunos diseños, la ejecución en paralelo de lotes más pequeños podría mejorar el rendimiento de las solicitudes en un sistema con mucha carga.</span><span class="sxs-lookup"><span data-stu-id="84417-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="84417-398">En este caso, aunque es más rápido tooprocess un único lote mayor, procesamiento de varios lotes en paralelo puede ser más eficaz.</span><span class="sxs-lookup"><span data-stu-id="84417-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="84417-399">Si usa la ejecución en paralelo, considere la posibilidad de controlar número máximo de Hola de subprocesos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="84417-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="84417-400">Un número menor podría causar menos contención y un tiempo de ejecución más rápido.</span><span class="sxs-lookup"><span data-stu-id="84417-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="84417-401">Además, considere la posibilidad de una carga adicional Hola que esto impone sobre la base de datos de destino de hello tanto en las conexiones y transacciones.</span><span class="sxs-lookup"><span data-stu-id="84417-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="84417-402">Factores de rendimiento relacionados</span><span class="sxs-lookup"><span data-stu-id="84417-402">Related performance factors</span></span>
<span data-ttu-id="84417-403">Las instrucciones típicas sobre el rendimiento de la base de datos también afectan al procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="84417-404">Por ejemplo, el rendimiento de inserción se reduce para aquellas tablas que tengan una clave principal grande o varios índices no agrupados.</span><span class="sxs-lookup"><span data-stu-id="84417-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="84417-405">Si los parámetros con valores de tabla utilizan un procedimiento almacenado, puede usar el comando hello **SET NOCOUNT ON** al principio de hello del procedimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="84417-406">Esta instrucción suprime la devolución de hello del recuento de Hola de filas de hello afectado en el procedimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="84417-407">Sin embargo, en nuestras pruebas, Hola uso de **SET NOCOUNT ON** no tiene ningún efecto o disminución del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84417-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="84417-408">Hello procedimiento almacenado de prueba era simple con una sola **insertar** comando de parámetro con valores de tabla de hello.</span><span class="sxs-lookup"><span data-stu-id="84417-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="84417-409">Es posible que los procedimientos almacenados más complejos se beneficien de esta instrucción.</span><span class="sxs-lookup"><span data-stu-id="84417-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="84417-410">Pero no suponga que agregar **SET NOCOUNT ON** procedimiento tooyour almacenado mejora automáticamente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84417-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="84417-411">toounderstand Hola efecto, pruebe el procedimiento almacenado con y sin hello **SET NOCOUNT ON** instrucción.</span><span class="sxs-lookup"><span data-stu-id="84417-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="84417-412">Escenarios de procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="84417-412">Batching scenarios</span></span>
<span data-ttu-id="84417-413">Hello siguientes secciones se describen cómo parámetros con valores de tabla de toouse en tres escenarios de aplicación.</span><span class="sxs-lookup"><span data-stu-id="84417-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="84417-414">Hola primer escenario muestra cómo almacenar en búfer y el procesamiento por lotes pueden trabajar juntos.</span><span class="sxs-lookup"><span data-stu-id="84417-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="84417-415">segundo escenario de Hello mejora el rendimiento mediante la realización de operaciones de maestro y detalles en una llamada a procedimiento almacenado único.</span><span class="sxs-lookup"><span data-stu-id="84417-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="84417-416">Hola último escenario muestra cómo toouse con valores de tabla de parámetros en una operación "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="84417-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="84417-417">Almacenamiento en búfer</span><span class="sxs-lookup"><span data-stu-id="84417-417">Buffering</span></span>
<span data-ttu-id="84417-418">Aunque hay algunos escenarios que son candidatos obvios para el procesamiento por lotes, muchos otros podrían beneficiarse del procesamiento por lotes difiriendo el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="84417-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="84417-419">Sin embargo, también el procesamiento diferida conlleva un riesgo mayor de que se pueden perder datos de hello en caso de hello de un error inesperado.</span><span class="sxs-lookup"><span data-stu-id="84417-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="84417-420">Es importante toounderstand este riesgo y tenga en cuenta las consecuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="84417-421">Por ejemplo, considere una aplicación web que realiza un seguimiento del historial de navegación de Hola de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="84417-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="84417-422">En cada solicitud de página, aplicación hello podría realizar la vista de página de base de datos llamada toorecord Hola de un usuario.</span><span class="sxs-lookup"><span data-stu-id="84417-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="84417-423">Pero se consigue un mayor rendimiento y escalabilidad: el almacenamiento en búfer las actividades de navegación de los usuarios de hello y, a continuación, enviar esta base de datos de toohello datos en lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="84417-424">Puede desencadenar la actualización de la base de datos de Hola por tiempo transcurrido o el tamaño de búfer.</span><span class="sxs-lookup"><span data-stu-id="84417-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="84417-425">Por ejemplo, una regla podría especificar que ese lote Hola debe procesarse después de 20 segundos o al búfer de hello llegue a tener 1000 elementos.</span><span class="sxs-lookup"><span data-stu-id="84417-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="84417-426">siguiente Hola código de ejemplo utiliza [extensiones reactivas - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess almacenado en búfer los eventos generados por una clase de supervisión.</span><span class="sxs-lookup"><span data-stu-id="84417-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="84417-427">Cuando Hola rellenos de búfer o se alcanza un tiempo de espera, se envía el lote de Hola de datos de usuario de base de datos de toohello con un parámetro con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="84417-428">Hola NavHistoryData clase modelos Hola usuario navegación detalles siguientes.</span><span class="sxs-lookup"><span data-stu-id="84417-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="84417-429">Contiene información básica como el identificador de usuario de hello, tiene acceso a la dirección URL de Hola y Hola hora de acceso.</span><span class="sxs-lookup"><span data-stu-id="84417-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="84417-430">Hola NavHistoryDataMonitor clase es responsable de hello usuario navegación toohello de datos de almacenamiento en búfer.</span><span class="sxs-lookup"><span data-stu-id="84417-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="84417-431">Contiene un método, RecordUserNavigationEntry, que responde generando un evento **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="84417-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="84417-432">Hello código siguiente muestra la lógica del constructor Hola que utiliza Rx toocreate una colección observable basada en un evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="84417-433">A continuación, se suscribe colección observable toothis con método de búfer de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="84417-434">sobrecarga de Hello especifica que dicho búfer Hola se debe enviar cada 20 segundos o 1000 entradas.</span><span class="sxs-lookup"><span data-stu-id="84417-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="84417-435">controlador de Hello convierte todos los elementos almacenados en búfer de hello en un tipo con valores de tabla y, a continuación, pasa este procedimiento tooa almacenado de tipo ese lote Hola de procesos.</span><span class="sxs-lookup"><span data-stu-id="84417-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="84417-436">Hello código siguiente muestra toda la definición para las clases de NavHistoryDataMonitor de Hola y Hola NavHistoryDataEventArgs Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

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

<span data-ttu-id="84417-437">toouse esta clase de almacenamiento en búfer, aplicación hello crea un objeto de NavHistoryDataMonitor estático.</span><span class="sxs-lookup"><span data-stu-id="84417-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="84417-438">Cada vez que un usuario tiene acceso a una página de la aplicación hello llama método NavHistoryDataMonitor.RecordUserNavigationEntry de hello.</span><span class="sxs-lookup"><span data-stu-id="84417-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="84417-439">Hola lógica de almacenamiento en búfer continúa tootake atención enviando estas bases de datos de toohello de entradas en lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="84417-440">Maestro/detalle</span><span class="sxs-lookup"><span data-stu-id="84417-440">Master detail</span></span>
<span data-ttu-id="84417-441">Los parámetros con valores de tabla son útiles en escenarios INSERT sencillos.</span><span class="sxs-lookup"><span data-stu-id="84417-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="84417-442">Sin embargo, puede ser más difíciles inserciones toobatch que implican más de una tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="84417-443">escenario de "maestro y detalles" Hello es un buen ejemplo.</span><span class="sxs-lookup"><span data-stu-id="84417-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="84417-444">tabla maestra Hola identifica la entidad primaria Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="84417-445">Una o varias tablas de detalle almacenen más datos sobre la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="84417-446">En este escenario, las relaciones de clave externas Exigir relación Hola de entidad principal de detalles tooa única.</span><span class="sxs-lookup"><span data-stu-id="84417-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="84417-447">Considere una versión simplificada de una tabla PurchaseOrder y su tabla OrderDetail asociada.</span><span class="sxs-lookup"><span data-stu-id="84417-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="84417-448">Hola después de Transact-SQL crea la tabla de PurchaseOrder de hello con cuatro columnas: OrderID, OrderDate, CustomerID y estado.</span><span class="sxs-lookup"><span data-stu-id="84417-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="84417-449">Cada pedido contiene una o más compras de productos.</span><span class="sxs-lookup"><span data-stu-id="84417-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="84417-450">Esta información se captura en la tabla PurchaseOrderDetail de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="84417-451">Hola después de Transact-SQL crea la tabla PurchaseOrderDetail de hello con cinco columnas: OrderID, OrderDetailID, ProductID, UnitPrice y OrderQty.</span><span class="sxs-lookup"><span data-stu-id="84417-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="84417-452">columna OrderID de Hello en la tabla PurchaseOrderDetail de hello debe hacer referencia a un pedido de la tabla de PurchaseOrder Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="84417-453">Hola después de la definición de una clave externa aplica esta restricción.</span><span class="sxs-lookup"><span data-stu-id="84417-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="84417-454">Parámetros con valores de tabla orden toouse, debe tener un tipo de tabla definido por el usuario para cada tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="84417-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

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

<span data-ttu-id="84417-455">Después, defina un procedimiento almacenado que acepte tablas de estos tipos.</span><span class="sxs-lookup"><span data-stu-id="84417-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="84417-456">Este procedimiento permite a un lote de solicitudes de toolocally un conjunto de pedidos y detalles de pedido en una sola llamada.</span><span class="sxs-lookup"><span data-stu-id="84417-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="84417-457">Hello Transact-SQL siguiente proporciona declaración completa del procedimiento almacenado de hello en este ejemplo de pedido de compra.</span><span class="sxs-lookup"><span data-stu-id="84417-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="84417-458">En este ejemplo, Hola definidas localmente @IdentityLink tabla almacena valores de hello reales OrderID de las filas de hello recién insertado.</span><span class="sxs-lookup"><span data-stu-id="84417-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="84417-459">Estos identificadores de pedidos son diferentes de los valores de OrderID temporales Hola Hola @orders y @details parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="84417-460">Por esta razón, Hola @IdentityLink tabla, a continuación, conecta a valores de hello OrderID de hello @orders toohello real OrderID valores de parámetro para las nuevas filas en la tabla de PurchaseOrder Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="84417-461">Después de este paso, Hola @IdentityLink tabla puede facilitar Insertar detalles de pedido de hello con hello OrderID real que satisface la restricción de clave externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="84417-462">Este procedimiento almacenado puede usarse desde el código o desde otras llamadas Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="84417-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="84417-463">Vea la sección de parámetros con valores de tabla de Hola de este documento para obtener un ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="84417-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="84417-464">Hola después de Transact-SQL muestra cómo toocall Hola sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="84417-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

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

<span data-ttu-id="84417-465">Esta solución permite que cada toouse por lotes un conjunto de valores de OrderID que empiezan en 1.</span><span class="sxs-lookup"><span data-stu-id="84417-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="84417-466">Estos valores temporales de OrderID describen relaciones de hello en el lote de hello, pero los valores reales de OrderID de Hola se determinan en tiempo de Hola de operación de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="84417-467">Puede ejecutar Hola mismas instrucciones en el ejemplo anterior de hello repetidamente y generar pedidos únicos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="84417-468">Por este motivo, podría agregar más lógica de base de datos o código que evite la duplicación de pedidos cuando se usa esta técnica de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="84417-469">Este ejemplo demuestra que las operaciones de base de datos más complejas, como las operaciones maestro/detalle, se pueden procesar por lotes con parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="84417-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="84417-470">UPSERT</span></span>
<span data-ttu-id="84417-471">Otro escenario de procesamiento por lotes supone la actualización de filas existentes y la inserción de nuevas filas de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="84417-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="84417-472">A veces, esta operación es tooas que se hace referencia una operación "UPSERT" (actualización + inserción).</span><span class="sxs-lookup"><span data-stu-id="84417-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="84417-473">En lugar de realizar llamadas independientes tooINSERT y UPDATE, instrucción MERGE de hello es mejor adecuado toothis tarea.</span><span class="sxs-lookup"><span data-stu-id="84417-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="84417-474">Hola instrucción MERGE puede realizar ambas insert y las operaciones en una única llamada de actualización.</span><span class="sxs-lookup"><span data-stu-id="84417-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="84417-475">Parámetros con valores de tabla pueden utilizarse con hello mezcla instrucción tooperform actualizaciones e inserciones.</span><span class="sxs-lookup"><span data-stu-id="84417-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="84417-476">Por ejemplo, considere una tabla de empleados simplificada que contiene Hola siguientes columnas: EmployeeID, FirstName, LastName, NúmeroSeguridadSocial:</span><span class="sxs-lookup"><span data-stu-id="84417-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="84417-477">En este ejemplo, puede usar la ausencia de Hola que Hola NúmeroSeguridadSocial único tooperform una combinación de varios empleados.</span><span class="sxs-lookup"><span data-stu-id="84417-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="84417-478">En primer lugar, cree el tipo de tabla definido por el usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="84417-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="84417-479">A continuación, crear un procedimiento almacenado o escribir código que usa Hola actualización de Hola de tooperform de instrucción de combinación e insert.</span><span class="sxs-lookup"><span data-stu-id="84417-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="84417-480">Hello en el ejemplo siguiente se utiliza Hola instrucción MERGE en un parámetro con valores de tabla, @employees, del tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="84417-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="84417-481">Hola contenido de hello @employees tabla no se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="84417-481">hello contents of hello @employees table are not shown here.</span></span>

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

<span data-ttu-id="84417-482">Para obtener más información, vea Hola documentación y ejemplos para la instrucción de combinación Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="84417-483">Aunque Hola se pudo realizar el mismo trabajo en varios pasos almacena la llamada al procedimiento con operaciones INSERT y UPDATE independientes, Hola instrucción MERGE es más eficaz.</span><span class="sxs-lookup"><span data-stu-id="84417-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="84417-484">Código de la base de datos también puede construir llamadas de Transact-SQL que utilizan la instrucción MERGE de hello directamente sin necesidad de dos llamadas de base de datos para INSERT y UPDATE.</span><span class="sxs-lookup"><span data-stu-id="84417-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="84417-485">Resumen de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="84417-485">Recommendation summary</span></span>
<span data-ttu-id="84417-486">Hello lista siguiente proporciona un resumen de hello procesamiento por lotes las recomendaciones que se describen en este tema:</span><span class="sxs-lookup"><span data-stu-id="84417-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="84417-487">Usar almacenamiento en búfer y rendimiento de hello tooincrease y la escalabilidad de las aplicaciones de base de datos SQL de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="84417-488">Comprender el equilibrio de hello entre el procesamiento por lotes o el almacenamiento en búfer y resistencia.</span><span class="sxs-lookup"><span data-stu-id="84417-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="84417-489">Error en un rol, riesgo de Hola de perder un lote sin procesar de los datos empresariales críticos puede contrarrestar ventaja de rendimiento de Hola de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="84417-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="84417-490">Intente tookeep todas las bases de datos de toohello llamadas dentro de una latencia de tooreduce único centro de datos.</span><span class="sxs-lookup"><span data-stu-id="84417-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="84417-491">Si elige una única técnica de procesamiento por lotes, los parámetros con valores de tabla proporcionan flexibilidad y un rendimiento óptimo Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="84417-492">Para hello más rápido rendimiento de inserción, siga estas directrices generales y pruebe su escenario:</span><span class="sxs-lookup"><span data-stu-id="84417-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="84417-493">Para < 100 filas, use un único comando INSERT con parámetros.</span><span class="sxs-lookup"><span data-stu-id="84417-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="84417-494">Para < 1000 filas, use parámetros con valores de tabla.</span><span class="sxs-lookup"><span data-stu-id="84417-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="84417-495">Para > = 1000 filas, use SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="84417-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="84417-496">Para actualizar y eliminar operaciones, usar parámetros con valores de tabla con lógica de procedimiento almacenado que determina el funcionamiento correcto de hello en cada fila de parámetro de tabla de hello.</span><span class="sxs-lookup"><span data-stu-id="84417-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="84417-497">Instrucciones para el tamaño de lote:</span><span class="sxs-lookup"><span data-stu-id="84417-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="84417-498">Utilice Hola tamaños de lote mayores que tengan sentido para su aplicación y los requisitos empresariales.</span><span class="sxs-lookup"><span data-stu-id="84417-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="84417-499">Aumento del rendimiento de Hola de equilibrio de lotes de gran tamaño con los riesgos de Hola de errores temporales o catastróficos.</span><span class="sxs-lookup"><span data-stu-id="84417-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="84417-500">¿Qué es consecuencia de Hola de reintentos o pérdida de datos de hello en lote Hola?</span><span class="sxs-lookup"><span data-stu-id="84417-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="84417-501">Probar Hola mayor lote tamaño tooverify que base de datos SQL no lo rechaza.</span><span class="sxs-lookup"><span data-stu-id="84417-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="84417-502">Cree la configuración ese control procesamiento por lotes, como el tamaño de lote de Hola o período de tiempo de almacenamiento en búfer de Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="84417-503">Estas configuraciones proporcionan flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="84417-503">These settings provide flexibility.</span></span> <span data-ttu-id="84417-504">Puede cambiar Hola procesamiento por lotes de comportamiento en producción sin volver a implementar el servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="84417-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="84417-505">Evite la ejecución en paralelo de lotes que operan en una sola tabla en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="84417-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="84417-506">Si elige toodivide un único lote a través de varios subprocesos de trabajo, ejecute pruebas toodetermine Hola número ideal de subprocesos.</span><span class="sxs-lookup"><span data-stu-id="84417-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="84417-507">Después de traspasar un umbral no especificado, el aumento del número de subprocesos hará que el rendimiento disminuya en lugar de mejorarlo.</span><span class="sxs-lookup"><span data-stu-id="84417-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="84417-508">Considere la posibilidad de almacenar en búfer por tamaño y hora como una manera de implementar el procesamiento por lotes para más escenarios.</span><span class="sxs-lookup"><span data-stu-id="84417-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84417-509">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84417-509">Next steps</span></span>
<span data-ttu-id="84417-510">En este artículo se centra en cómo el diseño de la base de datos y técnicas de codificación relacionan toobatching puede mejorar el rendimiento de la aplicación y la escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="84417-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="84417-511">Sin embargo, esto es solamente un factor en la estrategia global.</span><span class="sxs-lookup"><span data-stu-id="84417-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="84417-512">Para obtener más formas tooimprove rendimiento y la escalabilidad, vea [Guía de rendimiento de base de datos de SQL Azure para las bases de datos únicos](sql-database-performance-guidance.md) y [consideraciones de precio y el rendimiento para un grupo elástico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="84417-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

