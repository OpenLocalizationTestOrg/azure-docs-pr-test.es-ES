---
title: "Azure Cosmos DB: análisis de gráficos mediante Spark y Apache TinkerPop Gremlin | Microsoft Docs"
description: "Este artículo presenta instrucciones para configurar y ejecutar análisis de gráficos y cálculos en paralelo en Azure Cosmos DB con Spark y TinkerPop SparkGraphComputer."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="87311-103">Azure Cosmos DB: análisis de gráficos mediante Spark y Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="87311-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="87311-104">[Base de datos de Azure Cosmos](introduction.md) es Hola servicio de base de datos distribuidos globalmente, varios modelos de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87311-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="87311-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todas ellas beneficiarán de las capacidades de distribución global y escalado horizontal de hello en núcleo de hello de la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="87311-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="87311-106">Azure Cosmos DB admite cargas de trabajo gráficas de procesamiento de transacciones en línea (OLTP) que usan [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87311-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="87311-107">[Spark](http://spark.apache.org/) es un proyecto de Apache Software Foundation que se centra en el procesamiento de datos OLAP (procesamiento analítico en línea) de uso general.</span><span class="sxs-lookup"><span data-stu-id="87311-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="87311-108">Spark proporciona un híbrido en memoria/disco basada en modelo informático distribuido que sea similar toohello Hadoop MapReduce modelo.</span><span class="sxs-lookup"><span data-stu-id="87311-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="87311-109">Puede implementar Apache Spark en nube de hello mediante [HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="87311-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="87311-110">Mediante la combinación de Azure Cosmos DB y Spark, puede ejecutar tanto cargas de trabajo OLTP como OLAP cuando use Gremlin.</span><span class="sxs-lookup"><span data-stu-id="87311-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="87311-111">Este artículo de inicio rápido muestra cómo toorun Gremlin consultas en base de datos de Azure Cosmos en un clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="87311-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87311-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="87311-112">Prerequisites</span></span>

<span data-ttu-id="87311-113">Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="87311-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="87311-114">Clúster de Azure HDInsight Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="87311-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="87311-115">JDK 1.8+ (si no tiene JDK, ejecute `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="87311-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="87311-116">Maven (si no tiene Maven, ejecute `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="87311-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="87311-117">Una suscripción de Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="87311-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="87311-118">Para obtener información acerca de cómo tooset de un clúster de Azure HDInsight Spark, consulte [clústeres de HDInsight de aprovisionamiento](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="87311-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="87311-119">Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="87311-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="87311-120">En primer lugar, cree una cuenta de base de datos con API Graph hello haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="87311-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="87311-121">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="87311-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="87311-122">Obtención de Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="87311-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="87311-123">Obtener Apache TinkerPop haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="87311-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="87311-124">Nodo principal de toohello remoto hello del clúster de HDInsight `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="87311-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="87311-125">Clonar el código fuente de hello TinkerPop3, genérelo localmente e instálelo tooMaven caché.</span><span class="sxs-lookup"><span data-stu-id="87311-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="87311-126">Instalar Hola Spark-Gremlin complemento</span><span class="sxs-lookup"><span data-stu-id="87311-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="87311-127">a.</span><span class="sxs-lookup"><span data-stu-id="87311-127">a.</span></span> <span data-ttu-id="87311-128">instalación de Hola de hello complemento administra uva.</span><span class="sxs-lookup"><span data-stu-id="87311-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="87311-129">Rellenar la información de los repositorios de Hola de uva para poder descargar Hola complemento y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="87311-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="87311-130">Crear archivo de configuración uva hello si no está presente en `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="87311-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="87311-131">Usar hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="87311-131">Use hello following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="87311-132">b.</span><span class="sxs-lookup"><span data-stu-id="87311-132">b.</span></span> <span data-ttu-id="87311-133">Inicie la consola de Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="87311-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="87311-134">c.</span><span class="sxs-lookup"><span data-stu-id="87311-134">c.</span></span> <span data-ttu-id="87311-135">Instalar Hola Spark-Gremlin complemento con versión 3.3.0-SNAPSHOT, que basa en los pasos anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="87311-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="87311-136">Compruebe si toosee `Hadoop-Gremlin` se activa con `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="87311-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="87311-137">Deshabilitar este complemento, ya que podría interferir con hello Spark Gremlin complemento `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="87311-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="87311-138">Preparación de las dependencias de TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="87311-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="87311-139">Al generar TinkerPop3 en el paso anterior de hello, proceso hello también extrajo todas las dependencias de archivo jar para Spark y Hadoop en el directorio de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="87311-140">Usar archivos JAR Hola que previamente se instala con HDI y extracción en dependencias adicionales solo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="87311-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="87311-141">Directorio de destino de Gremlin consola vaya toohello en `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="87311-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="87311-142">Mover todos los archivos JAR en `ext/` demasiado`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="87311-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="87311-143">Quitar todos los jar de bibliotecas en `lib/` que es hello no en lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="87311-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="87311-144">Obtener el conector de Azure Cosmos DB Spark Hola</span><span class="sxs-lookup"><span data-stu-id="87311-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="87311-145">Obtener el conector de Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` y el SDK de Java de Cosmos DB `azure-documentdb-1.10.0.jar` de [Cosmos DB Spark conector de Azure en GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="87311-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="87311-146">También puede compilarlo localmente.</span><span class="sxs-lookup"><span data-stu-id="87311-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="87311-147">Porque la versión más reciente de Hola de Spark Gremlin se ha generado con Spark 1.6.1 y no es compatible con Spark 2.0.2, que se utiliza actualmente en el conector de Azure Cosmos DB Spark hello, puede compilar código de hello más reciente TinkerPop3 e instalar archivos JAR Hola manualmente.</span><span class="sxs-lookup"><span data-stu-id="87311-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="87311-148">Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="87311-148">Do hello following:</span></span>

    <span data-ttu-id="87311-149">a.</span><span class="sxs-lookup"><span data-stu-id="87311-149">a.</span></span> <span data-ttu-id="87311-150">Clonación de conector de Azure Cosmos DB Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="87311-151">b.</span><span class="sxs-lookup"><span data-stu-id="87311-151">b.</span></span> <span data-ttu-id="87311-152">Compile TinkerPop3 (ya se hizo en pasos anteriores).</span><span class="sxs-lookup"><span data-stu-id="87311-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="87311-153">Instale todos los archivos JAR de TinkerPop 3.3.0-SNAPSHOT localmente.</span><span class="sxs-lookup"><span data-stu-id="87311-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="87311-154">c.</span><span class="sxs-lookup"><span data-stu-id="87311-154">c.</span></span> <span data-ttu-id="87311-155">Actualización `tinkerpop.version` `azure-documentdb-spark/pom.xml` demasiado`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="87311-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="87311-156">d.</span><span class="sxs-lookup"><span data-stu-id="87311-156">d.</span></span> <span data-ttu-id="87311-157">Compile con Maven.</span><span class="sxs-lookup"><span data-stu-id="87311-157">Build with Maven.</span></span> <span data-ttu-id="87311-158">Hello archivos JAR necesario se colocan en `target` y `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="87311-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="87311-159">Hola de copia se ha mencionado previamente directorio local de archivos JAR tooa en ~ / spark de documentos de azure:</span><span class="sxs-lookup"><span data-stu-id="87311-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="87311-160">Distribuir los nodos de trabajador de hello dependencias toohello Spark</span><span class="sxs-lookup"><span data-stu-id="87311-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="87311-161">Como transformación Hola de datos del gráfico depende de TinkerPop3, debe distribuir Hola relacionados con nodos de trabajador de dependencias tooall Spark.</span><span class="sxs-lookup"><span data-stu-id="87311-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="87311-162">Hola de copia mencionó anteriormente Gremlin dependencias, Hola jar de conector CosmosDB Spark y nodos de trabajador de SDK de Java CosmosDB toohello haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="87311-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="87311-163">a.</span><span class="sxs-lookup"><span data-stu-id="87311-163">a.</span></span> <span data-ttu-id="87311-164">Copie todos los archivos JAR hello en `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="87311-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="87311-165">b.</span><span class="sxs-lookup"><span data-stu-id="87311-165">b.</span></span> <span data-ttu-id="87311-166">Obtener lista de Hola de todos los nodos de trabajador de Spark, que encontrará en el panel de Ambari, Hola `Spark2 Clients` lista Hola `Spark2` sección.</span><span class="sxs-lookup"><span data-stu-id="87311-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="87311-167">c.</span><span class="sxs-lookup"><span data-stu-id="87311-167">c.</span></span> <span data-ttu-id="87311-168">Copie ese tooeach del directorio de nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="87311-169">Establecer las variables de entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="87311-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="87311-170">Encontrar Hola HDP versión de clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="87311-171">Se trata de nombre de directorio de hello en `/usr/hdp/` (por ejemplo, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="87311-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="87311-172">Establezca hdp.version para todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="87311-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="87311-173">En el panel de Ambari, vaya demasiado**sección YARN** > **configuraciones** > **avanzadas**y, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="87311-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="87311-174">a.</span><span class="sxs-lookup"><span data-stu-id="87311-174">a.</span></span> <span data-ttu-id="87311-175">En `Custom yarn-site`, agregar una nueva propiedad `hdp.version` con el valor de Hola de versión HDP hello en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="87311-176">b.</span><span class="sxs-lookup"><span data-stu-id="87311-176">b.</span></span> <span data-ttu-id="87311-177">Guardar las configuraciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-177">Save hello configurations.</span></span> <span data-ttu-id="87311-178">Aparecen advertencias, pero puede ignorarlas.</span><span class="sxs-lookup"><span data-stu-id="87311-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="87311-179">c.</span><span class="sxs-lookup"><span data-stu-id="87311-179">c.</span></span> <span data-ttu-id="87311-180">Reinicie los servicios YARN y Oozie de hello como iconos de notificación de hello indican.</span><span class="sxs-lookup"><span data-stu-id="87311-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="87311-181">Hola de conjunto después de las variables de entorno en el nodo principal de hello (reemplazar valores de hello según corresponda):</span><span class="sxs-lookup"><span data-stu-id="87311-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="87311-182">Preparar la configuración del gráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="87311-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="87311-183">Cree un archivo de configuración con hello parámetros de conexión de base de datos de Azure Cosmos e inspirará configuración y colóquelo en `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="87311-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for hello driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="87311-184">Hola de actualización `spark.driver.extraClassPath` y `spark.executor.extraClassPath` tooinclude directorio de Hola de archivos JAR Hola distribuido en el paso anterior de hello, en este caso `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="87311-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="87311-185">Proporcionar Hola siga detalles para la base de datos de Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="87311-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="87311-186">Cargar hello TinkerPop gráfico y guardar tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="87311-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="87311-187">toodemonstrate cómo toopersist un gráfico en la base de datos de Azure Cosmos, este ejemplo utiliza Hola TinkerPop predefinidos TinkerPop moderna gráfico.</span><span class="sxs-lookup"><span data-stu-id="87311-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="87311-188">gráfico de Hola se almacena en formato de Kryo y se proporciona en el repositorio de TinkerPop Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="87311-189">Porque se está ejecutando Gremlin en modo YARN, debe realizar datos de gráfico de hello disponibles en el sistema de archivos Hadoop Hola.</span><span class="sxs-lookup"><span data-stu-id="87311-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="87311-190">Siguiente de hello use comandos toomake un directorio y archivo de copia hello gráfico local en él.</span><span class="sxs-lookup"><span data-stu-id="87311-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="87311-191">Actualizar temporalmente hello `gremlin-spark.properties` archivo toouse `GryoInputFormat` gráfico de hello tooread.</span><span class="sxs-lookup"><span data-stu-id="87311-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="87311-192">También indicar `inputLocation` como directorio de hello crea, como en el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="87311-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="87311-193">Inicie la consola de Gremlin y, a continuación, crear Hola después de cálculo pasos toopersist datos toohello Configurar base de datos de Azure Cosmos colección:</span><span class="sxs-lookup"><span data-stu-id="87311-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="87311-194">a.</span><span class="sxs-lookup"><span data-stu-id="87311-194">a.</span></span> <span data-ttu-id="87311-195">Crear el gráfico de hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="87311-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="87311-196">b.</span><span class="sxs-lookup"><span data-stu-id="87311-196">b.</span></span> <span data-ttu-id="87311-197">Use SparkGraphComputer para escribir: `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="87311-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="87311-198">Desde el Explorador de datos, puede comprobar que Hola ha sido datos persistentes tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="87311-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="87311-199">Gráfico de Hola de carga de base de datos de Azure Cosmos y ejecutar consultas de Gremlin</span><span class="sxs-lookup"><span data-stu-id="87311-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="87311-200">gráfico de hello tooload, editar `gremlin-spark.properties` tooset `graphReader` demasiado`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="87311-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="87311-201">Gráfico de Hola de carga, recorrer datos hello y ejecutar consultas de Gremlin con él haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="87311-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="87311-202">a.</span><span class="sxs-lookup"><span data-stu-id="87311-202">a.</span></span> <span data-ttu-id="87311-203">Iniciar hello Gremlin consola `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="87311-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="87311-204">b.</span><span class="sxs-lookup"><span data-stu-id="87311-204">b.</span></span> <span data-ttu-id="87311-205">Crear el gráfico de hello con la configuración de hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="87311-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="87311-206">c.</span><span class="sxs-lookup"><span data-stu-id="87311-206">c.</span></span> <span data-ttu-id="87311-207">Cree un recorrido de gráfico con SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="87311-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="87311-208">d.</span><span class="sxs-lookup"><span data-stu-id="87311-208">d.</span></span> <span data-ttu-id="87311-209">Ejecute hello las siguientes consultas de gráfico Gremlin:</span><span class="sxs-lookup"><span data-stu-id="87311-209">Run hello following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="87311-210">toosee más detallada de registro, Establece el nivel de registro de hello `conf/log4j-console.properties` tooa nivel más detallado.</span><span class="sxs-lookup"><span data-stu-id="87311-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="87311-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87311-211">Next steps</span></span>

<span data-ttu-id="87311-212">En este artículo de inicio rápido, ha aprendido cómo toowork con gráficos mediante la combinación de base de datos de Azure Cosmos y Spark.</span><span class="sxs-lookup"><span data-stu-id="87311-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
