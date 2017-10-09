---
title: "Guía de programación aaaSCP.NET | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse SCP.NET toocreate. Topologías de Storm basada en la red para usan con Storm en HDInsight."
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
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="0a2ca-103">Guía de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="0a2ca-103">SCP programming guide</span></span>
<span data-ttu-id="0a2ca-104">SCP es una plataforma toobuild en tiempo real, la aplicación de procesamiento de datos confiable, coherente y de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="0a2ca-105">Se genera en la parte superior de [Apache Storm](http://storm.incubator.apache.org/) --una secuencia sistema diseñado por Comunidades de hello OSS de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="0a2ca-106">Storm ha sido diseñado por Nathan Marz con código abierto en Twitter.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="0a2ca-107">Aprovecha [ZooKeeper Apache](http://zookeeper.apache.org/), Apache otro proyecto tooenable altamente confiable distribuida coordinación y administración de Estados.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="0a2ca-108">No sólo proyecto Hola SCP portar Storm en Windows, sino también proyecto Hola agrega personalización ecosistema de Windows hello y extensiones.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="0a2ca-109">extensiones de Hello incluyen experiencia del desarrollador de .NET y las bibliotecas, personalización de hello incluye la implementación basada en Windows.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="0a2ca-110">personalización y extensión de Hola se realiza de forma que no necesitamos proyectos de OSS hello toofork y podríamos aprovechamos derivados ecosistemas creados sobre Storm.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="0a2ca-111">Modelo de procesamiento</span><span class="sxs-lookup"><span data-stu-id="0a2ca-111">Processing model</span></span>
<span data-ttu-id="0a2ca-112">datos de Hello en SCP se modelan como un flujo continuo de tuplas.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="0a2ca-113">Normalmente Hola tuplas fluyen en alguna cola en primer lugar, entonces recoge y transformará lógica de negocios que se hospeda dentro de una topología de Storm, por último salida de hello se canalizan como tuplas tooanother SCP sistema o ser confirmada toostores como sistema de archivos distribuido o las bases de datos, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Un diagrama de una cola que incorpore datos tooprocessing, las fuentes de un almacén de datos](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="0a2ca-115">En Storm, una topología de aplicación define un gráfico de cálculo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="0a2ca-116">Cada nodo de la topología contiene lógica de procesamiento y los vínculos entre nodos indican del flujo de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="0a2ca-117">datos de entrada tooinject de Hello nodos en la topología de Hola se denominan Spouts, que pueden ser utilizados toosequence Hola datos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="0a2ca-118">Hello entradas los datos pueden residir en registros de archivos, bases de datos transaccionales, contador de rendimiento del sistema se denominan nodos de hello etc. con dos flujos de datos de entrada y salida tornillos, que Hola filtrado de datos reales y selecciones y agregación.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="0a2ca-119">SCP admite procesamiento de datos de tipo best-effort, at-least-once y exactly-once.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="0a2ca-120">En una aplicación distribuida de procesamiento de transmisiones se pueden producir varios errores durante el procesamiento de datos, como una interrupción de la red, errores de equipo, errores en el código de usuario, etc. Mínimo: una vez como procesamiento garantiza que se procesarán todos los datos al menos una vez por reproducir automáticamente Hola mismos datos cuando se produce el error.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="0a2ca-121">El procesamiento at-least-once es sencillo y confiable, y es muy adecuado para muchas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="0a2ca-122">Sin embargo, cuando la aplicación hello requiere recuento exacto, por ejemplo, menos de una vez como procesamiento no es suficiente porque hello mismos datos potencialmente se pudieron reproducir en la topología de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="0a2ca-123">En ese caso, exactamente-una vez que se ha diseñado el procesamiento toomake resultado de hello seguro es correcta, aunque se pueden reproducir los datos hello y procesar varias veces.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="0a2ca-124">SCP habilita aplicaciones de proceso de datos de .NET a los desarrolladores toodevelop en tiempo real mientras Aproveche Hola Máquina Virtual Java (JVM) según Storm bajo cubierta Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="0a2ca-125">Hola .NET y JVM comunicarán a través de socket TCP local.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="0a2ca-126">Básicamente cada pitorro/rayo es un par de proceso de .net/Java, donde se ejecuta la lógica de usuario de hello en proceso de .net como un complemento.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="0a2ca-127">toobuild una aplicación en la parte superior SCP de procesamiento de datos, que son necesarios varios pasos:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="0a2ca-128">Diseñar e implementar hello Spouts toopull en los datos de la cola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="0a2ca-129">Diseño e implementación tooprocess tornillos Hola datos de entrada y guardar datos tooexternal se almacena como base de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="0a2ca-130">Diseñar la topología de hello, a continuación, enviar y ejecutar topología Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="0a2ca-131">Hello topología define vértices y los datos de hello flujos entre vértices Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="0a2ca-132">SCP tomará la especificación de topología de Hola y lo implementará en un clúster de Storm, donde cada vértice se ejecuta en un nodo lógico.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="0a2ca-133">conmutación por error de Hola y ajustar la escala nos ocuparemos de programador de tareas de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="0a2ca-134">Este documento va a utilizar algunos toowalk sencillos ejemplos por el proceso de aplicación de procesamiento de datos de toobuild con SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="0a2ca-135">Interfaz de complemento de SCP</span><span class="sxs-lookup"><span data-stu-id="0a2ca-135">SCP Plugin Interface</span></span>
<span data-ttu-id="0a2ca-136">Complementos de SCP (o aplicaciones) son archivos ejecutables independientes que se puedan ejecutar dentro de Visual Studio durante la fase de desarrollo de Hola e incluirse en la canalización de Storm Hola después de la implementación en producción.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="0a2ca-137">Escribir Hola SCP complemento es simplemente Hola igual que escribir cualquier otra aplicación de consola Windows estándar.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="0a2ca-138">Plataforma SCP.NET declara alguna interfaz de pitorro/rayo y código de complemento de hello usuario debería implementar estas interfaces.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="0a2ca-139">propósito principal de Hola de este diseño es que el usuario Hola pueda centrarse en su propia lógica de negocios y dejando otro toobe cosas controlar SCP.NET plataforma.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="0a2ca-140">código de complemento de Hello usuario debería implementar una de las interfaces de hello siguiente, depende de si la topología de hello es transaccional o no transaccional y si el componente de hello es pitorro o rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="0a2ca-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="0a2ca-141">ISCPSpout</span></span>
* <span data-ttu-id="0a2ca-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="0a2ca-142">ISCPBolt</span></span>
* <span data-ttu-id="0a2ca-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="0a2ca-143">ISCPTxSpout</span></span>
* <span data-ttu-id="0a2ca-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="0a2ca-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="0a2ca-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="0a2ca-145">ISCPPlugin</span></span>
<span data-ttu-id="0a2ca-146">ISCPPlugin es la interfaz común de Hola para todos los tipos de complementos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="0a2ca-147">Actualmente es una interfaz ficticia.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="0a2ca-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="0a2ca-148">ISCPSpout</span></span>
<span data-ttu-id="0a2ca-149">ISCPSpout es la interfaz de Hola para pitorro no transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="0a2ca-150">Cuando `NextTuple()` se denomina hello C\# código de usuario puede emitir una o más tuplas.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="0a2ca-151">Si no hay nada tooemit, este método debe devolver sin emitir nada.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="0a2ca-152">Debe señalarse que `NextTuple()`, `Ack()` y `Fail()` se llaman todas en un bucle cerrado en un solo subproceso del proceso de C\#.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="0a2ca-153">Cuando no hay ningún tooemit tuplas, es toohave cortés NextTuple suspensión de un breve período de tiempo (por ejemplo, 10 milisegundos) así como no toowaste demasiada CPU.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="0a2ca-154">`Ack()` y `Fail()` solo se llamarán cuando el mecanismo de confirmación esté habilitado en el archivo de especificación.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="0a2ca-155">Hola `seqId` es tooidentify usado Hola tupla que está realizados o no correctamente.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="0a2ca-156">Por lo que si está habilitada la confirmación de topología no transaccionales, Hola siguen emit función debe usarse en pitorro:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="0a2ca-157">Si no se admite la confirmación de topología no transaccionales, Hola `Ack()` y `Fail()` pueden dejarse como función vacía.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="0a2ca-158">Hola `parms` parámetros de entrada en estas funciones son diccionario vacío, se reservan para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="0a2ca-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="0a2ca-159">ISCPBolt</span></span>
<span data-ttu-id="0a2ca-160">ISCPBolt es la interfaz de Hola para rayo no transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="0a2ca-161">Cuando hay nueva tupla, Hola `Execute()` función llamará tooprocess lo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="0a2ca-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="0a2ca-162">ISCPTxSpout</span></span>
<span data-ttu-id="0a2ca-163">ISCPTxSpout es la interfaz de Hola para pitorro transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="0a2ca-164">Del mismo modo que su contrapartida no transaccional, `NextTx()`, `Ack()` y `Fail()` se llaman todas en un bucle cerrado en un solo subproceso del proceso de C\#.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="0a2ca-165">Cuando no hay ningún tooemit de datos, es toohave cortés `NextTx` suspensión durante un breve período de tiempo (10 milisegundos), así como no toowaste demasiada CPU.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="0a2ca-166">`NextTx()`es importante, toostart una nueva transacción, hello parámetro `seqId` es tooidentify usado Hola transacción, que también se utiliza en `Ack()` y `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="0a2ca-167">En `NextTx()`, usuario puede emitir comandos de tooJava de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="0a2ca-168">Hola datos se almacenarán en reproducción de toosupport ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="0a2ca-169">Porque la capacidad de Hola de ZooKeeper es muy limitada, usuario solo debe emitir metadatos, no los datos de forma masiva en pitorro transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="0a2ca-170">Storm reproducirá automáticamente la transacción en caso de error, por lo que no se debe llamar a `Fail()` en condiciones normales.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="0a2ca-171">Pero si SCP puede comprobar los metadatos de hello emitidos por pitorro transaccional, puede llamar a `Fail()` cuando Hola metadatos no son válida.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="0a2ca-172">Hola `parms` parámetros de entrada en estas funciones son diccionario vacío, se reservan para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="0a2ca-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="0a2ca-173">ISCPBatchBolt</span></span>
<span data-ttu-id="0a2ca-174">ISCPBatchBolt es la interfaz de Hola para rayo transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="0a2ca-175">`Execute()`se llama cuando hay nueva tupla que llegan al rayo Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="0a2ca-176">`FinishBatch()` se llama cuando esta transacción finaliza.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="0a2ca-177">Hola `parms` parámetro de entrada está reservado para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="0a2ca-178">En el caso de una topología transaccional, existe un concepto importante, `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="0a2ca-179">Tiene dos campos, `TxId` y `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="0a2ca-180">`TxId`es tooidentify usa una transacción específica y para una transacción determinada, puede haber varios intento si transacción Hola se produce un error y es volver a reproducir.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="0a2ca-181">SCP.NET nuevo le un diferentes ISCPBatchBolt objeto tooprocess cada `StormTxAttempt`, igual que ¿en qué Storm en lado de Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="0a2ca-182">propósito de Hola de este diseño es toosupport procesamiento de transacciones paralelas.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="0a2ca-183">Usuario debe mantenerlo en cuenta que si finaliza el intento de transacción, se destruirá el objeto ISCPBatchBolt correspondiente de Hola y el recolector.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="0a2ca-184">Modelo de objetos</span><span class="sxs-lookup"><span data-stu-id="0a2ca-184">Object Model</span></span>
<span data-ttu-id="0a2ca-185">SCP.NET también proporciona un sencillo conjunto de objetos de clave para los desarrolladores tooprogram con.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="0a2ca-186">Son **Context**, **StateStore** y **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="0a2ca-187">Se explicará en parte del resto de Hola de esta sección.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="0a2ca-188">Context</span><span class="sxs-lookup"><span data-stu-id="0a2ca-188">Context</span></span>
<span data-ttu-id="0a2ca-189">Contexto proporciona una aplicación en ejecución entorno toohello.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="0a2ca-190">Cada instancia de ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) tiene su correspondiente instancia de Context.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="0a2ca-191">funcionalidad de Hello proporcionada por contexto puede dividirse en dos partes: parte estática (1) Hola que está disponible en Hola todo C\# procesar parte dinámica de hello (2), que solo está disponible para la instancia de contexto específica de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="0a2ca-192">Parte estática</span><span class="sxs-lookup"><span data-stu-id="0a2ca-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="0a2ca-193">`Logger` se proporciona con fines de registro.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="0a2ca-194">`pluginType`es utiliza el tipo de complemento de hello tooindicate de hello C\# proceso.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="0a2ca-195">Si Hola C\# proceso se ejecuta en modo de prueba local (sin Java), el tipo de complemento de hello es `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="0a2ca-196">`Config`se proporciona tooget parámetros de configuración del lado de Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="0a2ca-197">Hola parámetros se pasan desde el lado de Java cuando C\# se inicializa el complemento.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="0a2ca-198">Hola `Config` parámetros se dividen en dos partes: `stormConf` y `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="0a2ca-199">`stormConf`es parámetros definidos por Storm y `pluginConf` es parámetros Hola definidos por el SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="0a2ca-200">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="0a2ca-201">`TopologyContext`es proporcionado por el contexto de topología de hello tooget, es muy útil para los componentes con varios paralelismo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="0a2ca-202">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="0a2ca-203">Parte dinámica</span><span class="sxs-lookup"><span data-stu-id="0a2ca-203">Dynamic Part</span></span>
<span data-ttu-id="0a2ca-204">Hola siguientes interfaces es pertinente tooa cierto instancia de contexto.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="0a2ca-205">instancia de contexto de Hello es creada por plataforma SCP.NET y pasa toohello código de usuario:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="0a2ca-206">Por pitorro no transaccional que admite la confirmación, se proporciona Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="0a2ca-207">Para admitir la confirmación de rayo no transaccionales, lo que debería explícitamente `Ack()` o `Fail()` Hola tupla que recibió.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="0a2ca-208">Y cuando se emiten nueva tupla, también debe especificar delimitadores de Hola de hello nueva tupla.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="0a2ca-209">Hola siguiendo métodos se proporciona.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="0a2ca-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="0a2ca-210">StateStore</span></span>
<span data-ttu-id="0a2ca-211">`StateStore` proporciona servicios de metadatos, generación de secuencias monotónicas y coordinación sin espera.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="0a2ca-212">En `StateStore`, se pueden compilar abstracciones de simultaneidad distribuidas de nivel más alto, como bloqueos distribuidos, colas distribuidas, barreras y servicios de transacciones.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="0a2ca-213">Aplicaciones de SCP pueden utilizar hello `State` objeto toopersist cierta información en ZooKeeper, especialmente para la topología transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="0a2ca-214">Así, si pitorro transaccional se bloquea y se reinicia, puede recuperar la información necesaria de Hola de ZooKeeper y reiniciar canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="0a2ca-215">Hola `StateStore` objeto principalmente tiene estos métodos:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
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
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="0a2ca-216">Hola `State` objeto principalmente tiene estos métodos:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="0a2ca-217">Para hello `Commit()` método, cuando simpleMode se establece tootrue, eliminará simplemente Hola correspondiente ZNode en ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="0a2ca-218">En caso contrario, se eliminarán Hola ZNode actual y agregar un nuevo nodo en hello confirmado\_ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="0a2ca-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="0a2ca-219">SCPRuntime</span></span>
<span data-ttu-id="0a2ca-220">SCPRuntime proporciona Hola siguiendo dos métodos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="0a2ca-221">`Initialize()`es el entorno de runtime de hello SCP de tooinitialize usado.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="0a2ca-222">En este método, Hola C\# proceso conectará toohello lado de Java y obtiene los parámetros de configuración y el contexto de topología.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="0a2ca-223">`LaunchPlugin()`se usa tookick desactivar mensajes de bienvenida del bucle de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="0a2ca-224">En este bucle Hola C\# complemento recibirá mensajes forma parte de Java (incluidas las señales de control y tuplas) y, a continuación, proporcionan mensajes de saludo de proceso, quizás una llamada a método de interfaz de hello mediante código de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="0a2ca-225">parámetro de entrada de Hello para el método `LaunchPlugin()` es un delegado que puede devolver un objeto que implementa la interfaz de ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="0a2ca-226">Para ISCPBatchBolt, podemos obtener `StormTxAttempt` de `parms`y usar toojudge si es un intento de reproducido.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="0a2ca-227">Esto se hace normalmente en rayo de confirmación de Hola y se muestra en hello `HelloWorldTx` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="0a2ca-228">Por lo general, Hola SCP complementos se puede ejecutar en dos modos aquí:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="0a2ca-229">Modo de prueba local: En este modo, Hola SCP complementos (Hola C\# código de usuario) ejecute dentro de Visual Studio durante la fase de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="0a2ca-230">`LocalContext`puede usarse en este modo, que proporciona el método tooserialize Hola genera tuplas toolocal archivos y vuelva toomemory a leerlos.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="0a2ca-231">Modo normal: En este modo, Hola SCP complementos se inician por proceso de java de storm.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="0a2ca-232">A continuación se ofrece un ejemplo de inicio de un complemento de SCP:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="0a2ca-233">Lenguaje de especificación de topologías</span><span class="sxs-lookup"><span data-stu-id="0a2ca-233">Topology Specification Language</span></span>
<span data-ttu-id="0a2ca-234">La especificación de topologías de SCP es un lenguaje específico de dominios para la descripción y configuración de topologías de SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="0a2ca-235">Se basa en Clojure DSL de Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) y se amplía con SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="0a2ca-236">Especificaciones de la topología pueden enviarse directamente toostorm de clúster para la ejecución a través de hello ***runspec*** comando.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="0a2ca-237">SCP.NET ha Agregar seguimiento funciones toodefine Hola topología transaccional:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="0a2ca-238">**Nuevas funciones**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-238">**New Functions**</span></span> | <span data-ttu-id="0a2ca-239">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-239">**Parameters**</span></span> | <span data-ttu-id="0a2ca-240">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a2ca-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-241">**tx-topolopy**</span></span> |<span data-ttu-id="0a2ca-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-242">topology-name</span></span><br /><span data-ttu-id="0a2ca-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="0a2ca-243">spout-map</span></span><br /><span data-ttu-id="0a2ca-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="0a2ca-244">bolt-map</span></span> |<span data-ttu-id="0a2ca-245">Definir una topología transaccional con el nombre de la topología de hello, &nbsp;spouts mapa de definición y mapa de definición de tornillos de Hola</span><span class="sxs-lookup"><span data-stu-id="0a2ca-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="0a2ca-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-246">**scp-tx-spout**</span></span> |<span data-ttu-id="0a2ca-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-247">exec-name</span></span><br /><span data-ttu-id="0a2ca-248">args</span><span class="sxs-lookup"><span data-stu-id="0a2ca-248">args</span></span><br /><span data-ttu-id="0a2ca-249">fields</span><span class="sxs-lookup"><span data-stu-id="0a2ca-249">fields</span></span> |<span data-ttu-id="0a2ca-250">Permite definir un spout transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-250">Define a transactional spout.</span></span> <span data-ttu-id="0a2ca-251">Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="0a2ca-252">Hola ***campos*** es los campos de salida de hello para pitorro</span><span class="sxs-lookup"><span data-stu-id="0a2ca-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="0a2ca-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="0a2ca-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-254">exec-name</span></span><br /><span data-ttu-id="0a2ca-255">args</span><span class="sxs-lookup"><span data-stu-id="0a2ca-255">args</span></span><br /><span data-ttu-id="0a2ca-256">fields</span><span class="sxs-lookup"><span data-stu-id="0a2ca-256">fields</span></span> |<span data-ttu-id="0a2ca-257">Permite definir un bolt de lote.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="0a2ca-258">Se ejecutará la aplicación hello con ***nombre exec*** con ***args.***</span><span class="sxs-lookup"><span data-stu-id="0a2ca-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="0a2ca-259">Hello campos es hello campos de salida para el rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="0a2ca-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="0a2ca-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-261">exec-name</span></span><br /><span data-ttu-id="0a2ca-262">args</span><span class="sxs-lookup"><span data-stu-id="0a2ca-262">args</span></span><br /><span data-ttu-id="0a2ca-263">fields</span><span class="sxs-lookup"><span data-stu-id="0a2ca-263">fields</span></span> |<span data-ttu-id="0a2ca-264">Permite definir un bolt de autor.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="0a2ca-265">Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="0a2ca-266">Hola ***campos*** es los campos de salida de hello de rayo</span><span class="sxs-lookup"><span data-stu-id="0a2ca-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="0a2ca-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-267">**nontx-topolopy**</span></span> |<span data-ttu-id="0a2ca-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-268">topology-name</span></span><br /><span data-ttu-id="0a2ca-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="0a2ca-269">spout-map</span></span><br /><span data-ttu-id="0a2ca-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="0a2ca-270">bolt-map</span></span> |<span data-ttu-id="0a2ca-271">Definir una topología no transaccionales con el nombre de la topología de hello,&nbsp; spouts mapa de definición y mapa de definición de tornillos de Hola</span><span class="sxs-lookup"><span data-stu-id="0a2ca-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="0a2ca-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-272">**scp-spout**</span></span> |<span data-ttu-id="0a2ca-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-273">exec-name</span></span><br /><span data-ttu-id="0a2ca-274">args</span><span class="sxs-lookup"><span data-stu-id="0a2ca-274">args</span></span><br /><span data-ttu-id="0a2ca-275">fields</span><span class="sxs-lookup"><span data-stu-id="0a2ca-275">fields</span></span><br /><span data-ttu-id="0a2ca-276">Parámetros</span><span class="sxs-lookup"><span data-stu-id="0a2ca-276">parameters</span></span> |<span data-ttu-id="0a2ca-277">Permite definir un spout no transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-277">Define a nontransactional spout.</span></span> <span data-ttu-id="0a2ca-278">Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="0a2ca-279">Hola ***campos*** es los campos de salida de hello para pitorro</span><span class="sxs-lookup"><span data-stu-id="0a2ca-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="0a2ca-280">Hola ***parámetros*** es opcional, con toospecify algunos parámetros, como "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="0a2ca-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="0a2ca-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-281">**scp-bolt**</span></span> |<span data-ttu-id="0a2ca-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="0a2ca-282">exec-name</span></span><br /><span data-ttu-id="0a2ca-283">args</span><span class="sxs-lookup"><span data-stu-id="0a2ca-283">args</span></span><br /><span data-ttu-id="0a2ca-284">fields</span><span class="sxs-lookup"><span data-stu-id="0a2ca-284">fields</span></span><br /><span data-ttu-id="0a2ca-285">Parámetros</span><span class="sxs-lookup"><span data-stu-id="0a2ca-285">parameters</span></span> |<span data-ttu-id="0a2ca-286">Permite definir un bolt no transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="0a2ca-287">Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="0a2ca-288">Hola ***campos*** es los campos de salida de hello de rayo</span><span class="sxs-lookup"><span data-stu-id="0a2ca-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="0a2ca-289">Hola ***parámetros*** es opcional, con toospecify algunos parámetros, como "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="0a2ca-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="0a2ca-290">SCP.NET tiene definidas las siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="0a2ca-291">**Palabras clave**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-291">**Key Words**</span></span> | <span data-ttu-id="0a2ca-292">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="0a2ca-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-293">**:name**</span></span> |<span data-ttu-id="0a2ca-294">Definir Hola topología nombre</span><span class="sxs-lookup"><span data-stu-id="0a2ca-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="0a2ca-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-295">**:topology**</span></span> |<span data-ttu-id="0a2ca-296">Definir Hola topología mediante Hola por encima de las funciones y se generan en los que se.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="0a2ca-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-297">**:p**</span></span> |<span data-ttu-id="0a2ca-298">Definir la sugerencia de paralelismo de Hola para cada pitorro o rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="0a2ca-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-299">**:config**</span></span> |<span data-ttu-id="0a2ca-300">Definir parámetro configura o actualización hello las existentes</span><span class="sxs-lookup"><span data-stu-id="0a2ca-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="0a2ca-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-301">**:schema**</span></span> |<span data-ttu-id="0a2ca-302">Definir Hola esquema de secuencia.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="0a2ca-303">Y los parámetros de uso frecuente:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="0a2ca-304">**Parámetro**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-304">**Parameter**</span></span> | <span data-ttu-id="0a2ca-305">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="0a2ca-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-306">**"plugin.name"**</span></span> |<span data-ttu-id="0a2ca-307">nombre de archivo ejecutable de complemento de hello C#</span><span class="sxs-lookup"><span data-stu-id="0a2ca-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="0a2ca-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-308">**"plugin.args"**</span></span> |<span data-ttu-id="0a2ca-309">Argumentos del complemento</span><span class="sxs-lookup"><span data-stu-id="0a2ca-309">plugin args</span></span> |
| <span data-ttu-id="0a2ca-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-310">**"output.schema"**</span></span> |<span data-ttu-id="0a2ca-311">Esquema de salida</span><span class="sxs-lookup"><span data-stu-id="0a2ca-311">Output schema</span></span> |
| <span data-ttu-id="0a2ca-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="0a2ca-313">Indica si se ha habilitado confirmación para una topología no transaccional</span><span class="sxs-lookup"><span data-stu-id="0a2ca-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="0a2ca-314">comando de Hello runspec se implementará junto con los bits de Hola, uso de hello es similar:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="0a2ca-315">Hola ***recursos dir*** parámetro es opcional, deberá toospecify, cuando se desea tooplug una C\# aplicación y este directorio contendrá la aplicación hello, dependencias de Hola y las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="0a2ca-316">Hola ***classpath*** parámetro también es opcional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="0a2ca-317">Es utilizado toospecify Hola Java classpath si archivo especificaciones de hello contiene apetezca charlar Java o rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="0a2ca-318">Características varias</span><span class="sxs-lookup"><span data-stu-id="0a2ca-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="0a2ca-319">Declaración de esquema de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="0a2ca-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="0a2ca-320">usuario de Hello puede emitir la tupla en C\# procesar, hello plataforma necesita tooserialize Hola tupla en byte [], transferencia tooJava lado, y Storm transferirá este destinos de toohello de tupla.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="0a2ca-321">Mientras tanto en el componente de nivel inferior, Hola C\# proceso recibirá tupla desde el lado de java y convertir los tipos originales de toohello por plataforma, todas estas operaciones se ocultan de forma Hola plataforma.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="0a2ca-322">serialización de hello toosupport y la deserialización, el código de usuario debe toodeclare esquema de Hola de hello entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="0a2ca-323">esquema de flujo de entrada/salida de Hello, se definen como un diccionario, clave de hello es hello StreamId y valor hello es Hola tipos de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="0a2ca-324">componente de Hello puede tener varias secuencias declarados.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="0a2ca-325">En el objeto de contexto, tenemos Hola agrega la siguiente API:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="0a2ca-326">Código de usuario debe asegurarse de que tuplas Hola genera obedecen a esquema Hola definido para esa secuencia o sistema Hola producirá una excepción en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="0a2ca-327">Compatibilidad con varias transmisiones</span><span class="sxs-lookup"><span data-stu-id="0a2ca-327">Multi-Stream Support</span></span>
<span data-ttu-id="0a2ca-328">SCP admite usuario código tooemit o recibir mensajes de varias secuencias distintas a Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="0a2ca-329">compatibilidad de Hola se refleja en el objeto de contexto de hello como Hola Emit método toma un parámetro de identificador de secuencia opcional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="0a2ca-330">Se han agregado dos métodos de hello objeto de contexto de SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="0a2ca-331">Únicamente son utilizados tooemit tupla o tuplas toospecify StreamId.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="0a2ca-332">Hola StreamId es una cadena y debe toobe coherentes en ambos C\# y Hola especificación de definición de topología.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="0a2ca-333">secuencia de inexistente emitir de tooa Hola darán lugar a excepciones de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="0a2ca-334">Agrupación de campos</span><span class="sxs-lookup"><span data-stu-id="0a2ca-334">Fields Grouping</span></span>
<span data-ttu-id="0a2ca-335">Hola que compilación en campos de agrupación en Strom no funciona correctamente en SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="0a2ca-336">Hola lado de Proxy de Java, todos los tipos de datos de campos de hello son realmente el byte [] y campos de hello agrupación utilizará Hola byte [] objeto hash tooperform Hola agrupación de código.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="0a2ca-337">código hash de Hello byte [] objeto es la dirección de Hola de este objeto en memoria.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="0a2ca-338">Modo de agrupación Hola serán incorrecto para dos bytes [] objetos ese Hola de recurso compartido mismo contenido pero no Hola la misma dirección.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="0a2ca-339">SCP.NET agrega un método de agrupación personalizada, y va a utilizar contenido Hola de agrupación de hello byte [] toodo Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="0a2ca-340">En **especificación** archivo, la sintaxis de hello es similar:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="0a2ca-341">Aquí,</span><span class="sxs-lookup"><span data-stu-id="0a2ca-341">Here,</span></span>

1. <span data-ttu-id="0a2ca-342">"scp-field-group" significa "Agrupación personalizada de campos implementada mediante SCP".</span><span class="sxs-lookup"><span data-stu-id="0a2ca-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="0a2ca-343">":tx" o ":non-tx" indica si se trata de una topología transaccional.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="0a2ca-344">Necesitamos esta información desde Hola índice de inicio es diferente en tx frente a topologías no tx.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="0a2ca-345">[0,1] indica un hashset de campos de identificadores, a partir de 0.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="0a2ca-346">Topologías híbridas</span><span class="sxs-lookup"><span data-stu-id="0a2ca-346">Hybrid topology</span></span>
<span data-ttu-id="0a2ca-347">Hola que Storm nativo se escribe en Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="0a2ca-348">Y SCP.Net ha mejorado tooenable nuestro toowrite aduaneras C\# código toohandle su lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="0a2ca-349">Pero también admitimos topologías híbridas que no solo contengan spouts y bolts de C\#, sino también spouts y bolts de Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="0a2ca-350">Especificación de spout o bolt de Java en el archivo de especificación</span><span class="sxs-lookup"><span data-stu-id="0a2ca-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="0a2ca-351">En el archivo de especificación, "scp pitorro" y "scp rayo" también pueden ser usado toospecify Java Spouts y tornillos, este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="0a2ca-352">Aquí `microsoft.scp.example.HybridTopology.Generator` es nombre Hola de hello clase apetezca charlar Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="0a2ca-353">Especificación de classpath de Java en el comando runSpec</span><span class="sxs-lookup"><span data-stu-id="0a2ca-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="0a2ca-354">Si desea que la topología toosubmit que contiene Spouts Java o tornillos, es necesario toofirst compilación hello Spouts Java o tornillos y obtener los archivos Jar de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="0a2ca-355">A continuación, debe especificar Hola classpath de java que contiene los archivos Jar de hello al enviar la topología.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="0a2ca-356">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="0a2ca-357">Aquí **ejemplos\\HybridTopology\\java\\destino\\**  es Hola carpeta que contiene archivos Jar de Java pitorro/rayo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="0a2ca-358">Serialización y deserialización entre Java y C\\</span><span class="sxs-lookup"><span data-stu-id="0a2ca-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="0a2ca-359">El componente de SCP incluye Java y C\#.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="0a2ca-360">En orden toointeract con Spouts/tornillos de Java nativo, serialización/deserialización debe llevarse a cabo entre el lado de Java y C\# en paralelo, como se muestra en hello después de gráfico.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![diagrama de componente de java enviar componente tooSCP enviar tooJava componente](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="0a2ca-362">**Serialización en Java y deserialización en C\#**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="0a2ca-363">En primer lugar, proporcionamos la implementación predeterminada de serialización en la parte Java y deserialización en la parte C\#.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="0a2ca-364">método de serialización de Hello en el lado de Java puede especificarse en el archivo de especificación:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="0a2ca-365">Hola método de deserialización en C\# lado debe especificarse en C\# código de usuario:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="0a2ca-366">Esta implementación predeterminada debe controlar la mayoría de los casos si el tipo de datos de hello no es demasiado complejo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="0a2ca-367">En ciertos casos, ya sea porque hello tipo de datos de usuario es demasiado complejo o porque hello resultados de la implementación predeterminada no satisfacen Hola a requisito del usuario, el complemento de usuario pueden su propia implementación.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="0a2ca-368">Hola serializar la interfaz en java lado se define como:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="0a2ca-369">Hola deserializar interfaz en C\# lado se define como:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="0a2ca-370">public interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="0a2ca-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="0a2ca-371">**Serialización en C\# y deserialización en Java**</span><span class="sxs-lookup"><span data-stu-id="0a2ca-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="0a2ca-372">método de serialización de C de Hola\# lado debe especificarse en C\# código de usuario:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="0a2ca-373">Hola método de deserialización en el lado de Java debe especificarse en el archivo de especificación:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="0a2ca-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="0a2ca-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="0a2ca-375">Aquí "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" es el nombre de hello del deserializador, y "microsoft.scp.example.HybridTopology.Person" es se deserializan datos de Hola de clase de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="0a2ca-376">El usuario también puede usar su propia implementación de serializador de C\# y deserializador de Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="0a2ca-377">Se trata de interfaz de Hola para C\# serializador:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="0a2ca-378">Ésta es la interfaz de Hola para deserializador de Java:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="0a2ca-379">Modo host de SCP</span><span class="sxs-lookup"><span data-stu-id="0a2ca-379">SCP Host Mode</span></span>
<span data-ttu-id="0a2ca-380">En este modo, usuario puede compilar su tooDLL de códigos y usar SCPHost.exe proporcionada por la topología de toosubmit SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="0a2ca-381">archivo de especificación de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="0a2ca-382">En este caso, `plugin.name` se especifica como `SCPHost.exe` proporcionado por el SDK de SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="0a2ca-383">SCPHost.exe que acepta exactamente tres parámetros:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="0a2ca-384">Hello primero uno es nombre de la DLL de hello, que es `"HelloWorld.dll"` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="0a2ca-385">segunda Hello es nombre de clase de hello, que es `"Scp.App.HelloWorld.Generator"` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="0a2ca-386">Hello en tercer lugar uno es Hola nombre de un método estático público, que puede ser invocado tooget una instancia de ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="0a2ca-387">En modo host, el código de usuario se compila como DLL y lo invoca la plataforma SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="0a2ca-388">Por lo que plataforma SCP puede obtener el control completo de la lógica de procesamiento completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="0a2ca-389">Por lo que recomendamos a nuestros clientes toosubmit topología en modo de host de SCP ya que puede simplificar la experiencia de desarrollo de Hola y traiga más flexibilidad y mejor compatibilidad con versiones anteriores para versiones posteriores también.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="0a2ca-390">Ejemplos de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="0a2ca-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="0a2ca-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="0a2ca-391">HelloWorld</span></span>
<span data-ttu-id="0a2ca-392">**HelloWorld** es un ejemplo muy sencillo tooshow un sabor de SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="0a2ca-393">Se usa una topología no transaccional, con un spout llamado **generator** y dos bolts llamados **splitter** y **counter**.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="0a2ca-394">pitorro Hello **generador** aleatoriamente generará algunas frases y emitir estas frases demasiado**divisor**.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="0a2ca-395">tornillo de Hello **divisor** se divide Hola frases toowords y emitir estas palabras demasiado**contador** rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="0a2ca-396">Hola rayo "counter" usa un número de aparición de diccionario toorecord Hola de cada palabra.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="0a2ca-397">En este ejemplo, hay dos archivos de especificación, **HelloWorld.spec** y **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="0a2ca-398">Hola C\# código, puede averiguar si está habilitada la confirmación obteniendo hello pluginConf de lado de Java.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="0a2ca-399">En pitorro hello, si está habilitada la confirmación, un diccionario es toocache usado Hola tuplas que no han sido realizados.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="0a2ca-400">Si se llama a Fail(), hello error tupla se reproduzca:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="0a2ca-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="0a2ca-401">HelloWorldTx</span></span>
<span data-ttu-id="0a2ca-402">Hola **HelloWorldTx** en el ejemplo se muestra cómo tooimplement transaccional topología.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="0a2ca-403">Incluye un spout denominado **generator**, un bolt de lote denominado **partial-count** y un bolt de confirmación denominado **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="0a2ca-404">Existen también tres archivos txt creados previamente: **DataSource0.txt**, **DataSource1.txt** y **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="0a2ca-405">En cada transacción, Hola pitorro **generador** aleatoriamente se elija dos archivos de hello previamente creado tres archivos y emitir toohello de nombres de archivo de hello dos **parcial recuento** rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="0a2ca-406">tornillo de Hello **parcial recuento** primero obtendrá el nombre del archivo de hello de la tupla de hello recibido, Hola abrir archivo y recuento Hola el número de palabras en este archivo y finalmente emitir hello word número toohello **desumaderecuento**rayo.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="0a2ca-407">Hola **recuento suma** rayo mostrará un resumen de recuento total de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="0a2ca-408">tooachieve **exactamente una vez** semántica, rayo de confirmación de hello **recuento suma** necesita toojudge si es una transacción reproducida.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="0a2ca-409">En este ejemplo se incluye una variable de miembro estática:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="0a2ca-410">Cuando se crea una instancia de ISCPBatchBolt, obtendrá hello `txAttempt` de parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
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

<span data-ttu-id="0a2ca-411">Cuando `FinishBatch()` se llama, hello `lastCommittedTxId` será la actualización si no es una transacción reproducida.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="0a2ca-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="0a2ca-412">HybridTopology</span></span>
<span data-ttu-id="0a2ca-413">Esta topología contiene un spout de Java y un bolt de C\#.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="0a2ca-414">Utiliza la implementación de serialización y deserialización de la predeterminada de hello proporcionada por la plataforma de SCP.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="0a2ca-415">Inicie Hola ref **HybridTopology.spec** en **ejemplos\\HybridTopology** carpeta para obtener detalles de especificación de archivo de hello, y **SubmitTopology.bat** para saber cómo toospecify Java classpath.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="0a2ca-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="0a2ca-416">SCPHostDemo</span></span>
<span data-ttu-id="0a2ca-417">En este ejemplo se Hola igual que HelloWorld en esencia.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="0a2ca-418">Hello la única diferencia es que se compila código de usuario de hello como DLL y topología de Hola se envía mediante SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="0a2ca-419">Realice una sección de hello ref "Modo de Host de SCP" para ver una explicación más detallada.</span><span class="sxs-lookup"><span data-stu-id="0a2ca-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a2ca-420">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a2ca-420">Next Steps</span></span>
<span data-ttu-id="0a2ca-421">Para obtener ejemplos de topologías de Storm siguieron SCP, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a2ca-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="0a2ca-422">Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0a2ca-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="0a2ca-423">Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a2ca-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="0a2ca-424">Creación de varios flujos de datos en una topología de Storm en C#</span><span class="sxs-lookup"><span data-stu-id="0a2ca-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="0a2ca-425">Usar datos de Power Bi toovisualize de una topología de Storm</span><span class="sxs-lookup"><span data-stu-id="0a2ca-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="0a2ca-426">Procesamiento de los datos de sensor del vehículo desde Centros de eventos usando Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a2ca-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="0a2ca-427">Extracción, transformación y carga (ETL) de los centros de eventos de Azure tooHBase</span><span class="sxs-lookup"><span data-stu-id="0a2ca-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="0a2ca-428">Poner en correlación eventos con Storm y HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a2ca-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

