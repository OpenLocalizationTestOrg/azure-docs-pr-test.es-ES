---
title: "Guía de programación de SCP.NET | Microsoft Docs"
description: "Aprenda a usar SCP.NET para crear. topologías de Storm basadas en .NET para usarlas con Storm en HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="1173d-103">Guía de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="1173d-103">SCP programming guide</span></span>
<span data-ttu-id="1173d-104">SCP es una plataforma para compilar aplicaciones de procesamiento de datos confiables, coherentes y de alto rendimiento en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="1173d-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="1173d-105">Se basa en [Apache Storm](http://storm.incubator.apache.org/) , un sistema de procesamiento de transmisiones diseñado por las comunidades de OSS.</span><span class="sxs-lookup"><span data-stu-id="1173d-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="1173d-106">Storm ha sido diseñado por Nathan Marz con código abierto en Twitter.</span><span class="sxs-lookup"><span data-stu-id="1173d-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="1173d-107">Usa [Apache ZooKeeper](http://zookeeper.apache.org/), otro proyecto de Apache que permite una coordinación distribuida muy confiable y la administración de estados.</span><span class="sxs-lookup"><span data-stu-id="1173d-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="1173d-108">El proyecto SCP no solo trasladó Storm a Windows sino que también agregó las extensiones y la personalización del ecosistema Windows.</span><span class="sxs-lookup"><span data-stu-id="1173d-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="1173d-109">Entre las extensiones se incluye la experiencia de desarrolladores de .NET y las bibliotecas; la personalización incluye implementación basada en Windows.</span><span class="sxs-lookup"><span data-stu-id="1173d-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="1173d-110">La extensión y la personalización se ha realizado de tal forma que no necesitamos bifurcar los proyectos de OSS y pudimos aprovechar los ecosistemas derivados basados en Storm.</span><span class="sxs-lookup"><span data-stu-id="1173d-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="1173d-111">Modelo de procesamiento</span><span class="sxs-lookup"><span data-stu-id="1173d-111">Processing model</span></span>
<span data-ttu-id="1173d-112">Los datos de SCP se han modelado como secuencias continuas de tuplas.</span><span class="sxs-lookup"><span data-stu-id="1173d-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="1173d-113">Normalmente, las tuplas se introducen en primer lugar en alguna consulta, luego se seleccionan y se transforman mediante la lógica de negocios hospedada en una topología Storm, para finalmente poder canalizar el resultado como tuplas a otro sistema SCP o se confirma en almacenes como un sistema de archivos distribuidos o bases de datos como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1173d-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Diagrama de una cola que alimenta de datos a un procesamiento, lo que alimenta un almacén de datos](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="1173d-115">En Storm, una topología de aplicación define un gráfico de cálculo.</span><span class="sxs-lookup"><span data-stu-id="1173d-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="1173d-116">Cada nodo de la topología contiene lógica de procesamiento y los vínculos entre nodos indican del flujo de datos.</span><span class="sxs-lookup"><span data-stu-id="1173d-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="1173d-117">Los nodos que inyectan los datos de entrada en la topología se denominan spouts, que pueden usarse para secuenciar los datos.</span><span class="sxs-lookup"><span data-stu-id="1173d-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="1173d-118">Los datos de entrada pueden residir en registros de archivo, en bases de datos transaccionales, en contadores de rendimiento de sistema, etc. Los nodos con flujos de datos tanto de entrada como de salida se denominan bolts, que son los que realmente realizan el filtrado de datos, las selecciones y las agregaciones.</span><span class="sxs-lookup"><span data-stu-id="1173d-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="1173d-119">SCP admite procesamiento de datos de tipo best-effort, at-least-once y exactly-once.</span><span class="sxs-lookup"><span data-stu-id="1173d-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="1173d-120">En una aplicación distribuida de procesamiento de transmisiones se pueden producir varios errores durante el procesamiento de datos, como una interrupción de la red, errores de equipo, errores en el código de usuario, etc. El procesamiento por lo menos una vez garantiza que todos los datos se van a procesar al menos una vez, para lo cual se reproducen automáticamente los mismos datos en caso de error.</span><span class="sxs-lookup"><span data-stu-id="1173d-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="1173d-121">El procesamiento at-least-once es sencillo y confiable, y es muy adecuado para muchas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1173d-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="1173d-122">Sin embargo, cuando, por ejemplo, la aplicación requiere un recuento exacto, el procesamiento at-least-once es insuficiente ya que existe la posibilidad de que los mismos datos se reproduzcan en la topología de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1173d-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="1173d-123">En este caso, el procesamiento exactly-once se ha diseñado para asegurar que el resultados sea correcto aunque los datos se puedan reproducir y procesar varias veces.</span><span class="sxs-lookup"><span data-stu-id="1173d-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="1173d-124">SCP permite a los desarrolladores de .NET desarrollar aplicaciones de proceso en tiempo real y, al mismo tiempo, usar Storm basado en Máquina virtual Java (JVM) de forma encubierta.</span><span class="sxs-lookup"><span data-stu-id="1173d-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="1173d-125">.NET y JVM se comunican a través del socket local de TCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="1173d-126">Básicamente, cada spout/bolt es un par de procesos .Net/Java, donde la lógica del usuario se ejecuta en el proceso .Net como complemento.</span><span class="sxs-lookup"><span data-stu-id="1173d-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="1173d-127">Para compilar una aplicación de procesamiento de datos encima de SCP, se requieren varios pasos:</span><span class="sxs-lookup"><span data-stu-id="1173d-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="1173d-128">Diseño e implementación de los spouts para extraer datos de la cola.</span><span class="sxs-lookup"><span data-stu-id="1173d-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="1173d-129">Diseño e implementación de bolts para procesar los datos de entrada y guardado de los datos en almacenes externos como, por ejemplo, Base de datos.</span><span class="sxs-lookup"><span data-stu-id="1173d-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="1173d-130">Diseño de la topología y posterior envío y ejecución de la misma.</span><span class="sxs-lookup"><span data-stu-id="1173d-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="1173d-131">La topología define vértices y los datos fluyen entre los vértices.</span><span class="sxs-lookup"><span data-stu-id="1173d-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="1173d-132">SCP tomará la especificación de topología y la implementa en un clúster de Storm, en el que cada vértice ejecuta un nodo lógico.</span><span class="sxs-lookup"><span data-stu-id="1173d-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="1173d-133">El programador de tareas de Storm se encargará de la conmutación por error y el escalado.</span><span class="sxs-lookup"><span data-stu-id="1173d-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="1173d-134">En este documento se usarán algunos ejemplos sencillos para examinar cómo se compila una aplicación de procesamiento de datos con SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="1173d-135">Interfaz de complemento de SCP</span><span class="sxs-lookup"><span data-stu-id="1173d-135">SCP Plugin Interface</span></span>
<span data-ttu-id="1173d-136">Los complementos (o aplicaciones) de SCP son EXE independientes que pueden ejecutarse en Visual Studio durante la fase de desarrollo y conectarse al proceso de Storm tras su implementación en producción.</span><span class="sxs-lookup"><span data-stu-id="1173d-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="1173d-137">La escritura del complemento de SCP es exactamente igual que la escritura de las demás aplicaciones estándar de consola de Windows.</span><span class="sxs-lookup"><span data-stu-id="1173d-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="1173d-138">La plataforma SCP.NET declara alguna interfaz de spout/bolt y el código de complemento del usuario se debe implementar en estas interfaces.</span><span class="sxs-lookup"><span data-stu-id="1173d-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="1173d-139">El objetivo principal de este diseño es que el usuario pueda centrarse en su propia lógica del negocio y dejar que la plataforma SCP.NET controle otras cosas.</span><span class="sxs-lookup"><span data-stu-id="1173d-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="1173d-140">El código de complemento del usuario debe implementar una de las siguientes interfaces, en función de que la topología sea transaccional o no transaccional y de que el componentes sea un spout o un bolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="1173d-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="1173d-141">ISCPSpout</span></span>
* <span data-ttu-id="1173d-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="1173d-142">ISCPBolt</span></span>
* <span data-ttu-id="1173d-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="1173d-143">ISCPTxSpout</span></span>
* <span data-ttu-id="1173d-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="1173d-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="1173d-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="1173d-145">ISCPPlugin</span></span>
<span data-ttu-id="1173d-146">ISCPPlugin es la interfaz común para todos los tipos de complementos.</span><span class="sxs-lookup"><span data-stu-id="1173d-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="1173d-147">Actualmente es una interfaz ficticia.</span><span class="sxs-lookup"><span data-stu-id="1173d-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="1173d-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="1173d-148">ISCPSpout</span></span>
<span data-ttu-id="1173d-149">ISCPSpout es la interfaz del spout no transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="1173d-150">Cuando se llama a `NextTuple()`, el código C\# del usuario puede emitir una o más tuplas.</span><span class="sxs-lookup"><span data-stu-id="1173d-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="1173d-151">Si no hay nada que emitir, este método se debe devolver sin emitir nada.</span><span class="sxs-lookup"><span data-stu-id="1173d-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="1173d-152">Debe señalarse que `NextTuple()`, `Ack()` y `Fail()` se llaman todas en un bucle cerrado en un solo subproceso del proceso de C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="1173d-153">Cuando no hay tuplas que emitir, lo correcto es mantener inactiva NextTuple durante una breve cantidad de tiempo (como, por ejemplo, 10 milisegundos) para que no se desperdicie demasiada CPU.</span><span class="sxs-lookup"><span data-stu-id="1173d-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="1173d-154">`Ack()` y `Fail()` solo se llamarán cuando el mecanismo de confirmación esté habilitado en el archivo de especificación.</span><span class="sxs-lookup"><span data-stu-id="1173d-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="1173d-155">`seqId` se usa para identificar la tupla que se confirma o que contiene errores.</span><span class="sxs-lookup"><span data-stu-id="1173d-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="1173d-156">Por lo que si la confirmación se habilita en una topología no transaccional, se debe usar la siguiente función de emisión en spout:</span><span class="sxs-lookup"><span data-stu-id="1173d-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="1173d-157">Si la confirmación no se admite en la topología no transaccional, `Ack()` y `Fail()` se pueden dejar como funciones vacías.</span><span class="sxs-lookup"><span data-stu-id="1173d-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="1173d-158">Los parámetros de entrada `parms` de estas funciones son solo un diccionario vacío y se reservan para su uso en el futuro.</span><span class="sxs-lookup"><span data-stu-id="1173d-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="1173d-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="1173d-159">ISCPBolt</span></span>
<span data-ttu-id="1173d-160">ISCPBolt es la interfaz del bolt no transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="1173d-161">Cuando hay una nueva tupla disponible, se llamará a la función `Execute()` para procesarla.</span><span class="sxs-lookup"><span data-stu-id="1173d-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="1173d-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="1173d-162">ISCPTxSpout</span></span>
<span data-ttu-id="1173d-163">ISCPTxSpout es la interfaz del spout transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="1173d-164">Del mismo modo que su contrapartida no transaccional, `NextTx()`, `Ack()` y `Fail()` se llaman todas en un bucle cerrado en un solo subproceso del proceso de C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="1173d-165">Cuando no hay datos que emitir, lo correcto es mantener inactiva `NextTx` durante una breve cantidad de tiempo (10 milisegundos) para que no se desperdicie demasiada CPU.</span><span class="sxs-lookup"><span data-stu-id="1173d-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="1173d-166">`NextTx()` se llama para iniciar una nueva transacción, el parámetro de salida `seqId` se usa para identificar la transacción, que también se usa en `Ack()` y `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="1173d-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="1173d-167">En `NextTx()`, el usuario puede emitir datos a la parte Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="1173d-168">Los datos se almacenarán en ZooKeeper para admitir la reproducción.</span><span class="sxs-lookup"><span data-stu-id="1173d-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="1173d-169">Puesto que la capacidad de ZooKeeper es muy limitada, el usuario solo debe emitir metadatos, no datos masivos en un spout transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="1173d-170">Storm reproducirá automáticamente la transacción en caso de error, por lo que no se debe llamar a `Fail()` en condiciones normales.</span><span class="sxs-lookup"><span data-stu-id="1173d-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="1173d-171">Pero, si SCP puede comprobar los datos emitidos por el spout transaccional, puede llamar a `Fail()` cuando los metadatos no son válidos.</span><span class="sxs-lookup"><span data-stu-id="1173d-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="1173d-172">Los parámetros de entrada `parms` de estas funciones son solo un diccionario vacío y se reservan para su uso en el futuro.</span><span class="sxs-lookup"><span data-stu-id="1173d-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="1173d-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="1173d-173">ISCPBatchBolt</span></span>
<span data-ttu-id="1173d-174">ISCPBatchBolt es la interfaz del bolt transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="1173d-175">`Execute()` se llama cuando una nueva tupla llega al bolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="1173d-176">`FinishBatch()` se llama cuando esta transacción finaliza.</span><span class="sxs-lookup"><span data-stu-id="1173d-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="1173d-177">El parámetro de entrada `parms` se reserva para su uso en el futuro.</span><span class="sxs-lookup"><span data-stu-id="1173d-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="1173d-178">En el caso de una topología transaccional, existe un concepto importante, `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="1173d-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="1173d-179">Tiene dos campos, `TxId` y `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="1173d-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="1173d-180">`TxId` se usa para identificar una transacción específica y, en una transacción determinada, puede que haya varios intentos si la transacción tiene errores y se vuelve a reproducir.</span><span class="sxs-lookup"><span data-stu-id="1173d-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="1173d-181">SCP.NET usará otro objeto ISCPBatchBolt para procesar cada `StormTxAttempt`, del mismo modo que hace Storm en la parte Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="1173d-182">La finalidad de este diseño es admitir el procesamiento en paralelo de transacciones.</span><span class="sxs-lookup"><span data-stu-id="1173d-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="1173d-183">El usuario no debe olvidar que cuando un intento de transacción finaliza, el objeto ISCPBatchBolt correspondiente se destruirá y se recopilará como no utilizado.</span><span class="sxs-lookup"><span data-stu-id="1173d-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="1173d-184">Modelo de objetos</span><span class="sxs-lookup"><span data-stu-id="1173d-184">Object Model</span></span>
<span data-ttu-id="1173d-185">SCP.NET también proporciona un conjunto sencillo de objetos clave para que los desarrolladores programen con ellos.</span><span class="sxs-lookup"><span data-stu-id="1173d-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="1173d-186">Son **Context**, **StateStore** y **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="1173d-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="1173d-187">Se tratarán en la parte restante de esta sección.</span><span class="sxs-lookup"><span data-stu-id="1173d-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="1173d-188">Context</span><span class="sxs-lookup"><span data-stu-id="1173d-188">Context</span></span>
<span data-ttu-id="1173d-189">Context proporciona un entorno de ejecución para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1173d-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="1173d-190">Cada instancia de ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) tiene su correspondiente instancia de Context.</span><span class="sxs-lookup"><span data-stu-id="1173d-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="1173d-191">La función suministrada por Context se puede dividir en dos partes: (1) la parte estática, que está disponible en todo el proceso de C\#, y (2) la parte dinámica, que solo está disponible para la instancia concreta de Context.</span><span class="sxs-lookup"><span data-stu-id="1173d-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="1173d-192">Parte estática</span><span class="sxs-lookup"><span data-stu-id="1173d-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="1173d-193">`Logger` se proporciona con fines de registro.</span><span class="sxs-lookup"><span data-stu-id="1173d-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="1173d-194">`pluginType` se usa para indicar el tipo de complemento del proceso de C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="1173d-195">Si el proceso de C\# se ejecuta en modo de prueba local (sin Java), el tipo de complemento es `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="1173d-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="1173d-196">`Config` se proporciona para obtener parámetros de configuración de la parte Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="1173d-197">Los parámetros se pasan desde la parte Java al inicializar el complemento de C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="1173d-198">Los parámetros `Config` se dividen en dos partes: `stormConf` y `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="1173d-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="1173d-199">`stormConf` corresponde a los parámetros definidos por Storm y `pluginConf`, a los parámetros definidos por SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="1173d-200">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1173d-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="1173d-201">`TopologyContext` se proporciona para obtener el contexto de la topología, resulta más útil en el caso de componentes con paralelismo múltiple.</span><span class="sxs-lookup"><span data-stu-id="1173d-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="1173d-202">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1173d-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="1173d-203">Parte dinámica</span><span class="sxs-lookup"><span data-stu-id="1173d-203">Dynamic Part</span></span>
<span data-ttu-id="1173d-204">Las siguientes interfaces son adecuadas para una instancia determinada de Context.</span><span class="sxs-lookup"><span data-stu-id="1173d-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="1173d-205">La instancia de Context se crea con la plataforma SCP.NET y se pasa al código de usuario:</span><span class="sxs-lookup"><span data-stu-id="1173d-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="1173d-206">Para un spout no transaccional que admita confirmación, se proporciona el siguiente método:</span><span class="sxs-lookup"><span data-stu-id="1173d-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="1173d-207">Para un bolt no transaccional que admita confirmación, se debe aplicar `Ack()` o `Fail()` explícitamente a la tupla que recibe.</span><span class="sxs-lookup"><span data-stu-id="1173d-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="1173d-208">Además, al emitir una nueva tupla, también se deben especificar los delimitadores de la nueva tupla.</span><span class="sxs-lookup"><span data-stu-id="1173d-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="1173d-209">Se proporcionan los siguientes métodos.</span><span class="sxs-lookup"><span data-stu-id="1173d-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="1173d-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="1173d-210">StateStore</span></span>
<span data-ttu-id="1173d-211">`StateStore` proporciona servicios de metadatos, generación de secuencias monotónicas y coordinación sin espera.</span><span class="sxs-lookup"><span data-stu-id="1173d-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="1173d-212">En `StateStore`, se pueden compilar abstracciones de simultaneidad distribuidas de nivel más alto, como bloqueos distribuidos, colas distribuidas, barreras y servicios de transacciones.</span><span class="sxs-lookup"><span data-stu-id="1173d-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="1173d-213">Las aplicaciones de SCP pueden usar el objeto `State` para conservar información en ZooKeeper, sobre todo en el caso de una topología transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="1173d-214">Al hacerlo, si un spout transaccional tiene errores y se reinicia, puede recuperar la información necesaria de ZooKeeper y reiniciar del proceso.</span><span class="sxs-lookup"><span data-stu-id="1173d-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="1173d-215">El objeto `StateStore` tiene estos métodos principalmente:</span><span class="sxs-lookup"><span data-stu-id="1173d-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="1173d-216">El objeto `State` tiene estos métodos principalmente:</span><span class="sxs-lookup"><span data-stu-id="1173d-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="1173d-217">En el caso del método `Commit()` , cuando simpleMode se establece en "true", simplemente eliminará el ZNode correspondiente de ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="1173d-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="1173d-218">De lo contrario, eliminará el ZNode actual y agregará un nuevo nodo en COMMITTED\_PATH.</span><span class="sxs-lookup"><span data-stu-id="1173d-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="1173d-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="1173d-219">SCPRuntime</span></span>
<span data-ttu-id="1173d-220">SCPRuntime proporciona los dos métodos siguientes.</span><span class="sxs-lookup"><span data-stu-id="1173d-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="1173d-221">`Initialize()` se usa para inicializar el entorno de tiempo de ejecución de SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="1173d-222">En este método, el proceso de C\# se conectará a la parte Java, y obtiene los parámetros de configuración y el contexto de la topología.</span><span class="sxs-lookup"><span data-stu-id="1173d-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="1173d-223">`LaunchPlugin()` se usa para iniciar el bucle de procesamiento de mensajes.</span><span class="sxs-lookup"><span data-stu-id="1173d-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="1173d-224">En este bucle, el complemento de C\# recibe mensajes de la parte Java (incluidas las tuplas y las señales de control) y luego procesa los mensajes, tal vez llamando al método de la interfaz proporcionado por el código de usuario.</span><span class="sxs-lookup"><span data-stu-id="1173d-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="1173d-225">El parámetro de entrada del método `LaunchPlugin()` es un delegado que puede devolver un objeto que implemente la interfaz ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="1173d-226">En el caso de ISCPBatchBolt, podemos obtener `StormTxAttempt` de `parms` y usarlo para decidir si se trata de un intento reproducido.</span><span class="sxs-lookup"><span data-stu-id="1173d-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="1173d-227">Esto suele realizarse en el bolt de confirmación y se muestra en el ejemplo de `HelloWorldTx` .</span><span class="sxs-lookup"><span data-stu-id="1173d-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="1173d-228">En términos generales, los complementos de SCP pueden ejecutarse aquí en dos modos:</span><span class="sxs-lookup"><span data-stu-id="1173d-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="1173d-229">Modo de prueba local: en este modo, los complementos de SCP (el código C\# de usuario) se ejecutan en Visual Studio durante la fase de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="1173d-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="1173d-230">`LocalContext` se puede usar en este modo, lo que proporciona un método para serializar las tuplas emitidas a archivos locales y leerlas de nuevo en la memoria.</span><span class="sxs-lookup"><span data-stu-id="1173d-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="1173d-231">Modo regular: en este modo, los complementos de SCP se inician con el proceso Java de Storm.</span><span class="sxs-lookup"><span data-stu-id="1173d-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="1173d-232">A continuación se ofrece un ejemplo de inicio de un complemento de SCP:</span><span class="sxs-lookup"><span data-stu-id="1173d-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="1173d-233">Lenguaje de especificación de topologías</span><span class="sxs-lookup"><span data-stu-id="1173d-233">Topology Specification Language</span></span>
<span data-ttu-id="1173d-234">La especificación de topologías de SCP es un lenguaje específico de dominios para la descripción y configuración de topologías de SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="1173d-235">Se basa en Clojure DSL de Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) y se amplía con SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="1173d-236">Las especificaciones de topologías se pueden enviar directamente a un clúster de Storm para su ejecución a través del comando ***runspec***.</span><span class="sxs-lookup"><span data-stu-id="1173d-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="1173d-237">SCP.NET ha agregado las siguientes funciones para definir la topología transaccional:</span><span class="sxs-lookup"><span data-stu-id="1173d-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="1173d-238">**Nuevas funciones**</span><span class="sxs-lookup"><span data-stu-id="1173d-238">**New Functions**</span></span> | <span data-ttu-id="1173d-239">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="1173d-239">**Parameters**</span></span> | <span data-ttu-id="1173d-240">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1173d-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1173d-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="1173d-241">**tx-topolopy**</span></span> |<span data-ttu-id="1173d-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="1173d-242">topology-name</span></span><br /><span data-ttu-id="1173d-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="1173d-243">spout-map</span></span><br /><span data-ttu-id="1173d-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="1173d-244">bolt-map</span></span> |<span data-ttu-id="1173d-245">Permite definir una topología transaccional con el nombre de la topología, el mapa de definición de &nbsp;spouts y el mapa de definición de bolts.</span><span class="sxs-lookup"><span data-stu-id="1173d-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="1173d-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="1173d-246">**scp-tx-spout**</span></span> |<span data-ttu-id="1173d-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="1173d-247">exec-name</span></span><br /><span data-ttu-id="1173d-248">args</span><span class="sxs-lookup"><span data-stu-id="1173d-248">args</span></span><br /><span data-ttu-id="1173d-249">fields</span><span class="sxs-lookup"><span data-stu-id="1173d-249">fields</span></span> |<span data-ttu-id="1173d-250">Permite definir un spout transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-250">Define a transactional spout.</span></span> <span data-ttu-id="1173d-251">La aplicación se ejecutará con ***exec-name*** mediante ***args***.</span><span class="sxs-lookup"><span data-stu-id="1173d-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1173d-252">***fields*** corresponde a los campos de salida del spout.</span><span class="sxs-lookup"><span data-stu-id="1173d-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="1173d-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="1173d-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="1173d-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="1173d-254">exec-name</span></span><br /><span data-ttu-id="1173d-255">args</span><span class="sxs-lookup"><span data-stu-id="1173d-255">args</span></span><br /><span data-ttu-id="1173d-256">fields</span><span class="sxs-lookup"><span data-stu-id="1173d-256">fields</span></span> |<span data-ttu-id="1173d-257">Permite definir un bolt de lote.</span><span class="sxs-lookup"><span data-stu-id="1173d-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="1173d-258">La aplicación se ejecutará con ***exec-name*** mediante ***args***.</span><span class="sxs-lookup"><span data-stu-id="1173d-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="1173d-259">Fields corresponde a los campos de salida del bolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="1173d-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="1173d-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="1173d-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="1173d-261">exec-name</span></span><br /><span data-ttu-id="1173d-262">args</span><span class="sxs-lookup"><span data-stu-id="1173d-262">args</span></span><br /><span data-ttu-id="1173d-263">fields</span><span class="sxs-lookup"><span data-stu-id="1173d-263">fields</span></span> |<span data-ttu-id="1173d-264">Permite definir un bolt de autor.</span><span class="sxs-lookup"><span data-stu-id="1173d-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="1173d-265">La aplicación se ejecutará con ***exec-name*** mediante ***args***.</span><span class="sxs-lookup"><span data-stu-id="1173d-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1173d-266">***fields*** corresponde a los campos de salida del bolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="1173d-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="1173d-267">**nontx-topolopy**</span></span> |<span data-ttu-id="1173d-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="1173d-268">topology-name</span></span><br /><span data-ttu-id="1173d-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="1173d-269">spout-map</span></span><br /><span data-ttu-id="1173d-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="1173d-270">bolt-map</span></span> |<span data-ttu-id="1173d-271">Permite definir una topología no transaccional con el nombre de la topología,&nbsp; el mapa de definición de spouts y el mapa de definición de bolts.</span><span class="sxs-lookup"><span data-stu-id="1173d-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="1173d-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="1173d-272">**scp-spout**</span></span> |<span data-ttu-id="1173d-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="1173d-273">exec-name</span></span><br /><span data-ttu-id="1173d-274">args</span><span class="sxs-lookup"><span data-stu-id="1173d-274">args</span></span><br /><span data-ttu-id="1173d-275">fields</span><span class="sxs-lookup"><span data-stu-id="1173d-275">fields</span></span><br /><span data-ttu-id="1173d-276">Parámetros</span><span class="sxs-lookup"><span data-stu-id="1173d-276">parameters</span></span> |<span data-ttu-id="1173d-277">Permite definir un spout no transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-277">Define a nontransactional spout.</span></span> <span data-ttu-id="1173d-278">La aplicación se ejecutará con ***exec-name*** mediante ***args***.</span><span class="sxs-lookup"><span data-stu-id="1173d-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1173d-279">***fields*** corresponde a los campos de salida del spout.</span><span class="sxs-lookup"><span data-stu-id="1173d-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="1173d-280">***parameters*** es opcional, se usa para especificar algunos parámetros como, por ejemplo, "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="1173d-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="1173d-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="1173d-281">**scp-bolt**</span></span> |<span data-ttu-id="1173d-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="1173d-282">exec-name</span></span><br /><span data-ttu-id="1173d-283">args</span><span class="sxs-lookup"><span data-stu-id="1173d-283">args</span></span><br /><span data-ttu-id="1173d-284">fields</span><span class="sxs-lookup"><span data-stu-id="1173d-284">fields</span></span><br /><span data-ttu-id="1173d-285">Parámetros</span><span class="sxs-lookup"><span data-stu-id="1173d-285">parameters</span></span> |<span data-ttu-id="1173d-286">Permite definir un bolt no transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="1173d-287">La aplicación se ejecutará con ***exec-name*** mediante ***args***.</span><span class="sxs-lookup"><span data-stu-id="1173d-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1173d-288">***fields*** corresponde a los campos de salida del bolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="1173d-289">***parameters*** es opcional, se usa para especificar algunos parámetros como, por ejemplo, "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="1173d-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="1173d-290">SCP.NET tiene definidas las siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="1173d-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="1173d-291">**Palabras clave**</span><span class="sxs-lookup"><span data-stu-id="1173d-291">**Key Words**</span></span> | <span data-ttu-id="1173d-292">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1173d-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1173d-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="1173d-293">**:name**</span></span> |<span data-ttu-id="1173d-294">Permite definir el nombre de la topología</span><span class="sxs-lookup"><span data-stu-id="1173d-294">Define the Topology Name</span></span> |
| <span data-ttu-id="1173d-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="1173d-295">**:topology**</span></span> |<span data-ttu-id="1173d-296">Permite definir la topología con las funciones anteriores e incorporar otras.</span><span class="sxs-lookup"><span data-stu-id="1173d-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="1173d-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="1173d-297">**:p**</span></span> |<span data-ttu-id="1173d-298">Permite definir la sugerencia de paralelismo para cada spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="1173d-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="1173d-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="1173d-299">**:config**</span></span> |<span data-ttu-id="1173d-300">Permite definir un parámetro de configuración o actualizar los existentes.</span><span class="sxs-lookup"><span data-stu-id="1173d-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="1173d-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="1173d-301">**:schema**</span></span> |<span data-ttu-id="1173d-302">Permite definir el esquema de la secuencia.</span><span class="sxs-lookup"><span data-stu-id="1173d-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="1173d-303">Y los parámetros de uso frecuente:</span><span class="sxs-lookup"><span data-stu-id="1173d-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="1173d-304">**Parámetro**</span><span class="sxs-lookup"><span data-stu-id="1173d-304">**Parameter**</span></span> | <span data-ttu-id="1173d-305">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="1173d-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1173d-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="1173d-306">**"plugin.name"**</span></span> |<span data-ttu-id="1173d-307">Nombre del archivo exe del complemento de C#</span><span class="sxs-lookup"><span data-stu-id="1173d-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="1173d-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="1173d-308">**"plugin.args"**</span></span> |<span data-ttu-id="1173d-309">Argumentos del complemento</span><span class="sxs-lookup"><span data-stu-id="1173d-309">plugin args</span></span> |
| <span data-ttu-id="1173d-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="1173d-310">**"output.schema"**</span></span> |<span data-ttu-id="1173d-311">Esquema de salida</span><span class="sxs-lookup"><span data-stu-id="1173d-311">Output schema</span></span> |
| <span data-ttu-id="1173d-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="1173d-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="1173d-313">Indica si se ha habilitado confirmación para una topología no transaccional</span><span class="sxs-lookup"><span data-stu-id="1173d-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="1173d-314">El comando runspec se implementará junto con los bits, el uso es similar a:</span><span class="sxs-lookup"><span data-stu-id="1173d-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="1173d-315">El parámetro ***resource-dir*** es opcional, es necesario especificarlo cuando se desea conectar una aplicación de C\#. Este directorio contendrá la aplicación, las dependencias y las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="1173d-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="1173d-316">El parámetro ***classpath*** también es opcional.</span><span class="sxs-lookup"><span data-stu-id="1173d-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="1173d-317">Se usa para especificar el classpath de Java si el archivo de especificación contiene un spout o un bolt de Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="1173d-318">Características varias</span><span class="sxs-lookup"><span data-stu-id="1173d-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="1173d-319">Declaración de esquema de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="1173d-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="1173d-320">El usuario puede emitir una tupla de un proceso de C\#, la plataforma necesita serializar la tupla en byte, transferirla a la parte Java y Storm transferirá esta tupla a los destinos.</span><span class="sxs-lookup"><span data-stu-id="1173d-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="1173d-321">Mientras tanto, en el componente de bajada, el proceso de C\# recibirá de nuevo la tupla de la parte Java y la convierte a los tipos originales por plataforma; todas estas operaciones quedan ocultas por la plataforma.</span><span class="sxs-lookup"><span data-stu-id="1173d-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="1173d-322">Para que admita la serialización y la deserialización, es necesario que el código de usuario declare el esquema de las entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="1173d-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="1173d-323">El esquema de secuencias de entrada y salida se define como diccionario, la clave es el StreamId y el valor corresponde a los tipos de la columnas.</span><span class="sxs-lookup"><span data-stu-id="1173d-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="1173d-324">El componente puede tener declaradas multisecuencias.</span><span class="sxs-lookup"><span data-stu-id="1173d-324">The component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="1173d-325">En el objeto Context, hemos agregado la siguiente API:</span><span class="sxs-lookup"><span data-stu-id="1173d-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="1173d-326">El código de usuario debe comprobar que las tuplas emitidas siguen el esquema definido para la secuencia o el sistema lanzará una excepción en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1173d-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="1173d-327">Compatibilidad con varias transmisiones</span><span class="sxs-lookup"><span data-stu-id="1173d-327">Multi-Stream Support</span></span>
<span data-ttu-id="1173d-328">SCP admite que el código de usuario emita o reciba desde varias secuencias distintas a la vez.</span><span class="sxs-lookup"><span data-stu-id="1173d-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="1173d-329">La compatibilidad se refleja en el objeto Context cuando el método Emit adopta un parámetro de identificador de secuencia opcional.</span><span class="sxs-lookup"><span data-stu-id="1173d-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="1173d-330">Se han agregado dos métodos al objeto Context de SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="1173d-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="1173d-331">Se usan para emitir una tupla o tuplas para especificar StreamId.</span><span class="sxs-lookup"><span data-stu-id="1173d-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="1173d-332">StreamId es una cadena y debe ser coherente en C\# y en la especificación de definición de la topología.</span><span class="sxs-lookup"><span data-stu-id="1173d-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="1173d-333">La emisión a una secuencia inexistente provocará excepciones en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1173d-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="1173d-334">Agrupación de campos</span><span class="sxs-lookup"><span data-stu-id="1173d-334">Fields Grouping</span></span>
<span data-ttu-id="1173d-335">La agrupación de campos integrada de Strom no funciona correctamente en SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="1173d-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="1173d-336">En la parte de proxy Java, todos los tipos de datos de campos son en realidad byte[] y la agrupación de campos usa el código hash del objeto byte[] para realizar la agrupación.</span><span class="sxs-lookup"><span data-stu-id="1173d-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="1173d-337">El código hash del objeto byte[] es la dirección de este objeto en la memoria.</span><span class="sxs-lookup"><span data-stu-id="1173d-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="1173d-338">Por lo que la agrupación será incorrecta para dos objetos byte[] que compartan el mismo contenido pero no la misma dirección.</span><span class="sxs-lookup"><span data-stu-id="1173d-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="1173d-339">SCP.NET agrega un método de agrupación personalizado y usará el contenido del objeto byte[] para realizar la agrupación.</span><span class="sxs-lookup"><span data-stu-id="1173d-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="1173d-340">En el archivo **SPEC** , la sintaxis es similar a:</span><span class="sxs-lookup"><span data-stu-id="1173d-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="1173d-341">Aquí,</span><span class="sxs-lookup"><span data-stu-id="1173d-341">Here,</span></span>

1. <span data-ttu-id="1173d-342">"scp-field-group" significa "Agrupación personalizada de campos implementada mediante SCP".</span><span class="sxs-lookup"><span data-stu-id="1173d-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="1173d-343">":tx" o ":non-tx" indica si se trata de una topología transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="1173d-344">Necesitamos esta información porque el índice inicial es diferente en las topologías tx y non-tx.</span><span class="sxs-lookup"><span data-stu-id="1173d-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="1173d-345">[0,1] indica un hashset de campos de identificadores, a partir de 0.</span><span class="sxs-lookup"><span data-stu-id="1173d-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="1173d-346">Topologías híbridas</span><span class="sxs-lookup"><span data-stu-id="1173d-346">Hybrid topology</span></span>
<span data-ttu-id="1173d-347">El Storm nativo se escribe en Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-347">The native Storm is written in Java.</span></span> <span data-ttu-id="1173d-348">SCP.NET lo ha mejorado para permitir que nuestros clientes escriban código C\# para tratar su lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="1173d-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="1173d-349">Pero también admitimos topologías híbridas que no solo contengan spouts y bolts de C\#, sino también spouts y bolts de Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="1173d-350">Especificación de spout o bolt de Java en el archivo de especificación</span><span class="sxs-lookup"><span data-stu-id="1173d-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="1173d-351">En el archivo de especificación, también pueden usarse "scp-spout" y "scp-bolt" para especificar spouts o bolts de Java; a continuación se ofrece un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1173d-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="1173d-352">Aquí, `microsoft.scp.example.HybridTopology.Generator` es el nombre de la clase Spout de Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="1173d-353">Especificación de classpath de Java en el comando runSpec</span><span class="sxs-lookup"><span data-stu-id="1173d-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="1173d-354">Si quiere enviar una topología que contenga spouts o bolts de Java, es necesario compilar primero los spouts o bolts de Java y obtener los archivos Jar.</span><span class="sxs-lookup"><span data-stu-id="1173d-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="1173d-355">Tras ello, hay que especificar el classpath de Java que contiene los archivos Jar al enviar la topología.</span><span class="sxs-lookup"><span data-stu-id="1173d-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="1173d-356">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1173d-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="1173d-357">Aquí, **examples\\HybridTopology\\java\\target\\** es la carpeta que contiene el archivo Jar de spout o bolt de Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="1173d-358">Serialización y deserialización entre Java y C\\</span><span class="sxs-lookup"><span data-stu-id="1173d-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="1173d-359">El componente de SCP incluye Java y C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="1173d-360">Para interactuar con spouts o bolts nativos de Java, se deben llevar a cabo tareas de serialización y deserialización entre Java y C\#, como se muestra en el siguiente gráfico.</span><span class="sxs-lookup"><span data-stu-id="1173d-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Diagrama de un componente de Java que envía a un componente SCP que envía al componente de Java](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="1173d-362">**Serialización en Java y deserialización en C\#**</span><span class="sxs-lookup"><span data-stu-id="1173d-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="1173d-363">En primer lugar, proporcionamos la implementación predeterminada de serialización en la parte Java y deserialización en la parte C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="1173d-364">El método de serialización de la parte Java se puede especificar en el archivo SPEC:</span><span class="sxs-lookup"><span data-stu-id="1173d-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="1173d-365">El método de deserialización de la parte C\# debe especificarse en el código de usuario de C\#:</span><span class="sxs-lookup"><span data-stu-id="1173d-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="1173d-366">Esta implementación predeterminada debe tratar la mayoría de los casos si el tipo de datos no es demasiado complejo.</span><span class="sxs-lookup"><span data-stu-id="1173d-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="1173d-367">En determinados casos, bien porque el tipo de datos del usuario sea demasiado complejo o porque el rendimiento de nuestra implementación predeterminada no satisfaga los requisitos del cliente, el usuario puede conectar su propia implementación.</span><span class="sxs-lookup"><span data-stu-id="1173d-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="1173d-368">La interfaz de serialización en la parte Java se define de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="1173d-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="1173d-369">La interfaz de deserialización en la parte C\# se define de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="1173d-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="1173d-370">public interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="1173d-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="1173d-371">**Serialización en C\# y deserialización en Java**</span><span class="sxs-lookup"><span data-stu-id="1173d-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="1173d-372">El método de serialización de la parte C\# se debe especificar en el código C\# del usuario:</span><span class="sxs-lookup"><span data-stu-id="1173d-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="1173d-373">El método de deserialización de la parte Java se debe especificar en el archivo SPEC:</span><span class="sxs-lookup"><span data-stu-id="1173d-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="1173d-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="1173d-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="1173d-375">Aquí, "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" es el nombre del deserializador y "microsoft.scp.example.HybridTopology.Person", la clase de destino en la que los datos se deserializan.</span><span class="sxs-lookup"><span data-stu-id="1173d-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="1173d-376">El usuario también puede usar su propia implementación de serializador de C\# y deserializador de Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="1173d-377">Esta es la interfaz del serializador de C\#:</span><span class="sxs-lookup"><span data-stu-id="1173d-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="1173d-378">Esta es la interfaz del deserializador de Java:</span><span class="sxs-lookup"><span data-stu-id="1173d-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="1173d-379">Modo host de SCP</span><span class="sxs-lookup"><span data-stu-id="1173d-379">SCP Host Mode</span></span>
<span data-ttu-id="1173d-380">En este modo, el usuario puede compilar sus códigos en DLL y usar el SCPHost.exe proporcionado por SCP para enviar la topología.</span><span class="sxs-lookup"><span data-stu-id="1173d-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="1173d-381">El archivo de especificación es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="1173d-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="1173d-382">En este caso, `plugin.name` se especifica como `SCPHost.exe` proporcionado por el SDK de SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="1173d-383">SCPHost.exe que acepta exactamente tres parámetros:</span><span class="sxs-lookup"><span data-stu-id="1173d-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="1173d-384">El primero es el nombre del archivo DLL que, en este ejemplo, es `"HelloWorld.dll"` .</span><span class="sxs-lookup"><span data-stu-id="1173d-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="1173d-385">El segundo es el nombre de clase que, en este ejemplo, es `"Scp.App.HelloWorld.Generator"` .</span><span class="sxs-lookup"><span data-stu-id="1173d-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="1173d-386">El tercero es el nombre de un método estático público, que se puede invocar para obtener una instancia de ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="1173d-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="1173d-387">En modo host, el código de usuario se compila como DLL y lo invoca la plataforma SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="1173d-388">Por consiguiente, la plataforma SCP puede obtener el control completo de toda la lógica de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="1173d-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="1173d-389">Por consiguiente, recomendamos a nuestros clientes que envíen la topología en modo host de SCP, ya que puede simplificar la experiencia de desarrollo y proporcionarnos mayor flexibilidad y también mejor compatibilidad con versiones anteriores para una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="1173d-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="1173d-390">Ejemplos de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="1173d-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="1173d-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="1173d-391">HelloWorld</span></span>
<span data-ttu-id="1173d-392">**HelloWorld** resulta un ejemplo muy sencillo para dar una idea de SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="1173d-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="1173d-393">Se usa una topología no transaccional, con un spout llamado **generator** y dos bolts llamados **splitter** y **counter**.</span><span class="sxs-lookup"><span data-stu-id="1173d-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="1173d-394">El spout **generator** generará aleatoriamente algunas oraciones y emitirá estas oraciones a **splitter**.</span><span class="sxs-lookup"><span data-stu-id="1173d-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="1173d-395">El bolt **splitter** dividirá las oraciones en palabras y emitirá estas palabras al bolt **counter**.</span><span class="sxs-lookup"><span data-stu-id="1173d-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="1173d-396">El bolt "counter" usa un diccionario para registrar el número de repeticiones de cada palabra.</span><span class="sxs-lookup"><span data-stu-id="1173d-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="1173d-397">En este ejemplo, hay dos archivos de especificación, **HelloWorld.spec** y **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="1173d-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="1173d-398">En el código C\#, se puede descubrir si se ha habilitado confirmación obteniendo pluginConf de la parte Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="1173d-399">En el spout, si se ha habilitado confirmación, se usa un diccionario para almacenar en caché las tuplas que no se han confirmado.</span><span class="sxs-lookup"><span data-stu-id="1173d-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="1173d-400">Si llama a Fail(), la tupla con errores se reproducirá:</span><span class="sxs-lookup"><span data-stu-id="1173d-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="1173d-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="1173d-401">HelloWorldTx</span></span>
<span data-ttu-id="1173d-402">El ejemplo **HelloWorldTx** muestra cómo implementar la topología transaccional.</span><span class="sxs-lookup"><span data-stu-id="1173d-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="1173d-403">Incluye un spout denominado **generator**, un bolt de lote denominado **partial-count** y un bolt de confirmación denominado **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="1173d-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="1173d-404">Existen también tres archivos txt creados previamente: **DataSource0.txt**, **DataSource1.txt** y **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="1173d-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="1173d-405">En cada transacción, el spout **generator** elegirá aleatoriamente dos de los tres archivos creados previamente y emitirá los nombres de estos dos archivos al bolt **partial-count**.</span><span class="sxs-lookup"><span data-stu-id="1173d-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="1173d-406">El bolt **partial-count** obtendrá primero el nombre de archivo de la tupla recibida, luego abrirá el archivo y contará el número de palabras que hay en el mismo y, por último, emitirá el número de palabras al bolt **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="1173d-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="1173d-407">El bolt **count-sum** resumirá el recuento total.</span><span class="sxs-lookup"><span data-stu-id="1173d-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="1173d-408">Para obtener la semántica **exactly once**, es necesario que el bolt de confirmación **count-sum** decida si se trata de una transacción reproducida.</span><span class="sxs-lookup"><span data-stu-id="1173d-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="1173d-409">En este ejemplo se incluye una variable de miembro estática:</span><span class="sxs-lookup"><span data-stu-id="1173d-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="1173d-410">Una vez creada una instancia ISCPBatchBolt, obtendrá `txAttempt` de los parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="1173d-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="1173d-411">Cuando se llame a `FinishBatch()`, `lastCommittedTxId` se actualizará si no se trata de una transacción reproducida.</span><span class="sxs-lookup"><span data-stu-id="1173d-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="1173d-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="1173d-412">HybridTopology</span></span>
<span data-ttu-id="1173d-413">Esta topología contiene un spout de Java y un bolt de C\#.</span><span class="sxs-lookup"><span data-stu-id="1173d-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="1173d-414">Usa la implementación predeterminada de serialización y deserialización que proporciona la plataforma SCP.</span><span class="sxs-lookup"><span data-stu-id="1173d-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="1173d-415">Consulte **HybridTopology.spec** en la carpeta **examples\\HybridTopology** para obtener los detalles del archivo spec y **SubmitTopology.bat** para saber cómo se especifica un classpath de Java.</span><span class="sxs-lookup"><span data-stu-id="1173d-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="1173d-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="1173d-416">SCPHostDemo</span></span>
<span data-ttu-id="1173d-417">Este ejemplo es, básicamente, igual a HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="1173d-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="1173d-418">La única diferencia es que el código de usuario se compila como DLL y la topología se envía mediante SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="1173d-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="1173d-419">Consulte la sección "Modo host de SCP" para ver una explicación más detallada.</span><span class="sxs-lookup"><span data-stu-id="1173d-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1173d-420">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1173d-420">Next Steps</span></span>
<span data-ttu-id="1173d-421">Para ver ejemplos de topologías de Storm creados con SCP, consulte lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1173d-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="1173d-422">Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1173d-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="1173d-423">Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1173d-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="1173d-424">Creación de varios flujos de datos en una topología de Storm en C#</span><span class="sxs-lookup"><span data-stu-id="1173d-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="1173d-425">Uso de Power BI para visualizar datos desde la topología de Storm</span><span class="sxs-lookup"><span data-stu-id="1173d-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="1173d-426">Procesamiento de los datos de sensor del vehículo desde Centros de eventos usando Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1173d-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="1173d-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span><span class="sxs-lookup"><span data-stu-id="1173d-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="1173d-428">Poner en correlación eventos con Storm y HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1173d-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

