---
title: temas de tendencias de aaaTwitter con Apache Storm en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Trident toocreate una topología de Apache Storm que determina los temas tendencias en Twitter basado en hashtags."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="6652e-103">Determinación de las tendencias de Twitter con Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6652e-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="6652e-104">Obtenga información acerca de cómo toouse Trident toocreate una topología de Storm que determina tendencias temas (etiquetas de hash) en Twitter.</span><span class="sxs-lookup"><span data-stu-id="6652e-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="6652e-105">Trident es una abstracción de alto nivel que ofrece herramientas como uniones, agregaciones, agrupaciones, funciones y filtros.</span><span class="sxs-lookup"><span data-stu-id="6652e-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="6652e-106">Además, Trident agrega primitivas para realizar el procesamiento incremental, con estado.</span><span class="sxs-lookup"><span data-stu-id="6652e-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="6652e-107">ejemplo de Hola usado en este documento es una topología de Trident con un pitorro personalizado y una función.</span><span class="sxs-lookup"><span data-stu-id="6652e-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="6652e-108">También usa varias funciones integradas disponibles en Trident.</span><span class="sxs-lookup"><span data-stu-id="6652e-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="6652e-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="6652e-109">Requirements</span></span>

* <span data-ttu-id="6652e-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Hello JDK 1.8 y Java</a></span><span class="sxs-lookup"><span data-stu-id="6652e-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="6652e-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="6652e-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="6652e-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="6652e-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="6652e-113">Una cuenta de desarrollador de Twitter</span><span class="sxs-lookup"><span data-stu-id="6652e-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="6652e-114">Descargar proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="6652e-114">Download hello project</span></span>

<span data-ttu-id="6652e-115">Usar hello después tooclone Hola proyecto de código de forma local.</span><span class="sxs-lookup"><span data-stu-id="6652e-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="6652e-116">Descripción de la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="6652e-116">Understanding hello topology</span></span>

<span data-ttu-id="6652e-117">Hola siguiente diagrama se muestra de cómo fluyen los datos a través de esta topología:</span><span class="sxs-lookup"><span data-stu-id="6652e-117">hello following diagram shows of how data flows through this topology:</span></span>

![Topología](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="6652e-119">Este diagrama es una vista simplificada de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="6652e-120">Varias instancias de componentes de Hola se distribuyen en nodos de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="6652e-121">Hola código Trident que implementa la topología de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="6652e-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="6652e-122">Este código realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="6652e-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="6652e-123">Crea una secuencia de pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="6652e-124">pitorro Hola recupera tweets de Twitter y los filtros de palabras clave específicas (amor, música y coffee en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="6652e-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="6652e-125">HashtagExtractor, una función personalizada, es tooextract usa hash etiquetas de cada tweet.</span><span class="sxs-lookup"><span data-stu-id="6652e-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="6652e-126">Hola hash distinguen flujo toohello emitido.</span><span class="sxs-lookup"><span data-stu-id="6652e-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="6652e-127">secuencia de Hello es había agrupado por etiqueta de hash y pasa tooan agregador.</span><span class="sxs-lookup"><span data-stu-id="6652e-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="6652e-128">Este agregador crea un recuento de cuántas veces se ha repetido cada hashtag.</span><span class="sxs-lookup"><span data-stu-id="6652e-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="6652e-129">Estos datos se conservan en memoria.</span><span class="sxs-lookup"><span data-stu-id="6652e-129">This data is persisted in memory.</span></span> <span data-ttu-id="6652e-130">Por último, se genera una nueva secuencia que contiene la etiqueta de hash de Hola y recuento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="6652e-131">Hola **FirstN** ensamblado es tooreturn aplicado solo Hola 10 valores más altos, tomando como base el campo de recuento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="6652e-132">Para obtener más información sobre cómo trabajar con Trident, vea hello [Introducción a la API de Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) documento.</span><span class="sxs-lookup"><span data-stu-id="6652e-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="6652e-133">pitorro Hola</span><span class="sxs-lookup"><span data-stu-id="6652e-133">hello spout</span></span>

<span data-ttu-id="6652e-134">pitorro Hello, **TwitterSpout**, usa [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets de Twitter.</span><span class="sxs-lookup"><span data-stu-id="6652e-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="6652e-135">Se crea un filtro para palabras hello __le encanta__, **música**, y **café**.</span><span class="sxs-lookup"><span data-stu-id="6652e-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="6652e-136">Tweets entrantes (status) que coinciden con el filtro de Hola se almacenan en una cola bloqueo vinculada.</span><span class="sxs-lookup"><span data-stu-id="6652e-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="6652e-137">Por último, elementos se saca de la cola de Hola y genera la topología de toohello.</span><span class="sxs-lookup"><span data-stu-id="6652e-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="6652e-138">Hola HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="6652e-138">hello HashtagExtractor</span></span>

<span data-ttu-id="6652e-139">etiquetas de hash tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) es tooretrieve usado todas las etiquetas de hash que se encuentran en tweet Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="6652e-140">Estos artículos pasan a secuencia toohello emitido.</span><span class="sxs-lookup"><span data-stu-id="6652e-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="6652e-141">Configuración de Twitter</span><span class="sxs-lookup"><span data-stu-id="6652e-141">Configure Twitter</span></span>

<span data-ttu-id="6652e-142">Usar hello siguiendo los pasos tooregister una nueva aplicación de Twitter y obtener tooread de necesita la información del token de acceso y el consumidor Hola de Twitter:</span><span class="sxs-lookup"><span data-stu-id="6652e-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="6652e-143">Vaya demasiado[aplicaciones Twitter](https://apps.twitter.com) y haga clic en hello **crear nueva aplicación** botón.</span><span class="sxs-lookup"><span data-stu-id="6652e-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="6652e-144">Al rellenar el formulario de hello, deje hello **dirección URL de devolución de llamada** campo vacío.</span><span class="sxs-lookup"><span data-stu-id="6652e-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="6652e-145">Cuando se crea la aplicación hello, haga clic en hello **claves y Tokens de acceso** ficha.</span><span class="sxs-lookup"><span data-stu-id="6652e-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="6652e-146">Hola copia **clave de consumidor** y **secreto de consumidor** información.</span><span class="sxs-lookup"><span data-stu-id="6652e-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="6652e-147">En hello parte inferior de la página de hello, seleccione **crear mi token de acceso** si no existen tokens.</span><span class="sxs-lookup"><span data-stu-id="6652e-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="6652e-148">Cuando se han creado los tokens de hello, Hola copia **Token de acceso** y **secreto del Token de acceso** información.</span><span class="sxs-lookup"><span data-stu-id="6652e-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="6652e-149">Hola **TwitterSpoutTopology** proyecto Hola clonado anteriormente, abra **resources/twitter4j.properties** de archivos, agregar información de Hola que recopiló en los pasos anteriores de hello y, a continuación, guarde el archivo hello .</span><span class="sxs-lookup"><span data-stu-id="6652e-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="6652e-150">Crear topología de Hola</span><span class="sxs-lookup"><span data-stu-id="6652e-150">Build hello topology</span></span>

<span data-ttu-id="6652e-151">Usar hello siguiendo el proyecto de código toobuild hello:</span><span class="sxs-lookup"><span data-stu-id="6652e-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="6652e-152">Topología de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="6652e-152">Test hello topology</span></span>

<span data-ttu-id="6652e-153">Usar hello después topología localmente de comando tootest hello:</span><span class="sxs-lookup"><span data-stu-id="6652e-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="6652e-154">Una vez iniciada la topología de hello, debería ver información de depuración que contiene el hash de hello etiquetas y recuentos de emitido por la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="6652e-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="6652e-155">salida de Hello debe aparecer toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="6652e-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="6652e-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6652e-156">Next steps</span></span>

<span data-ttu-id="6652e-157">Ahora que ha probado localmente la topología de hello, descubrir cómo toodeploy Hola topología: [implementar y administrar topologías de Apache Storm en HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6652e-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="6652e-158">También es posible que interesa Hola Storm temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="6652e-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="6652e-159">Desarrollo de las topologías de Java para Storm en HDInsight con Maven</span><span class="sxs-lookup"><span data-stu-id="6652e-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="6652e-160">Desarrollo de las topologías de C# para Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6652e-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="6652e-161">Para obtener más ejemplos de Storm para HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6652e-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="6652e-162">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6652e-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

