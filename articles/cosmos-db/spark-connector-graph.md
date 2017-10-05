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
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="e61e7-103">Azure Cosmos DB: análisis de gráficos mediante Spark y Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="e61e7-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="e61e7-104">[Azure Cosmos DB](introduction.md) es el servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e61e7-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="e61e7-105">Puede crear bases de datos de documentos, de pares clave-valor y de gráficos, y realizar consultas en ellas. Todas las bases de datos se benefician de las funcionalidades de distribución global y escalado horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e61e7-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="e61e7-106">Azure Cosmos DB admite cargas de trabajo gráficas de procesamiento de transacciones en línea (OLTP) que usan [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e61e7-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="e61e7-107">[Spark](http://spark.apache.org/) es un proyecto de Apache Software Foundation que se centra en el procesamiento de datos OLAP (procesamiento analítico en línea) de uso general.</span><span class="sxs-lookup"><span data-stu-id="e61e7-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="e61e7-108">Spark proporciona un modelo híbrido de computación distribuida basado en memoria/disco, similar al modelo de MapReduce de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e61e7-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="e61e7-109">Puede implementar Apache Spark en la nube mediante [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="e61e7-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="e61e7-110">Mediante la combinación de Azure Cosmos DB y Spark, puede ejecutar tanto cargas de trabajo OLTP como OLAP cuando use Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e61e7-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="e61e7-111">En este tutorial se muestra cómo ejecutar consultas de Gremlin en Azure Cosmos DB en un clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e61e7-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e61e7-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e61e7-112">Prerequisites</span></span>

<span data-ttu-id="e61e7-113">Antes de ejecutar este ejemplo, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e61e7-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="e61e7-114">Clúster de Azure HDInsight Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="e61e7-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="e61e7-115">JDK 1.8+ (si no tiene JDK, ejecute `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="e61e7-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="e61e7-116">Maven (si no tiene Maven, ejecute `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="e61e7-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="e61e7-117">Una suscripción de Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="e61e7-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="e61e7-118">Para más información sobre cómo configurar un clúster Spark de Azure HDInsight, consulte [Aprovisionamiento de clústeres de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e61e7-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="e61e7-119">Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e61e7-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="e61e7-120">En primer lugar, cree una cuenta de base de datos con la API Graph siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e61e7-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="e61e7-121">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="e61e7-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="e61e7-122">Obtención de Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="e61e7-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="e61e7-123">Obtenga Apache TinkerPop mediante estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e61e7-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="e61e7-124">Conéctese en remoto al nodo principal del clúster de HDInsight `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="e61e7-125">Clone el código fuente de TinkerPop3, compílelo localmente e instálelo en la caché de Maven.</span><span class="sxs-lookup"><span data-stu-id="e61e7-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="e61e7-126">Instale el complemento Spark-Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e61e7-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="e61e7-127">a.</span><span class="sxs-lookup"><span data-stu-id="e61e7-127">a.</span></span> <span data-ttu-id="e61e7-128">La instalación del complemento se administra mediante Grape.</span><span class="sxs-lookup"><span data-stu-id="e61e7-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="e61e7-129">Rellene la información de los repositorios de Grape para poder descargar el complemento y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="e61e7-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="e61e7-130">Cree el archivo de configuración de Grape si no está en `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="e61e7-131">Use la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="e61e7-131">Use the following settings:</span></span>

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

    <span data-ttu-id="e61e7-132">b.</span><span class="sxs-lookup"><span data-stu-id="e61e7-132">b.</span></span> <span data-ttu-id="e61e7-133">Inicie la consola de Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="e61e7-134">c.</span><span class="sxs-lookup"><span data-stu-id="e61e7-134">c.</span></span> <span data-ttu-id="e61e7-135">Instale el complemento Spark-Gremlin, versión 3.3.0-SNAPSHOT, que generó en los pasos anteriores:</span><span class="sxs-lookup"><span data-stu-id="e61e7-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
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

4. <span data-ttu-id="e61e7-136">Compruebe si `Hadoop-Gremlin` está activado con `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="e61e7-137">Deshabilite este complemento, ya que podría interferir con el complemento Spark-Gremlin `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="e61e7-138">Preparación de las dependencias de TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="e61e7-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="e61e7-139">Cuando se compiló TinkerPop3 en el paso anterior, el proceso también extrajo todas las dependencias de archivos JAR para Spark y Hadoop en el directorio de destino.</span><span class="sxs-lookup"><span data-stu-id="e61e7-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="e61e7-140">Use lo archivos JAR anteriormente instalados con HDI y extraiga las dependencias adicionales solo si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e61e7-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="e61e7-141">Vaya al directorio de destino de la consola de Gremlin en `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="e61e7-142">Mueva todos los archivos JAR que hay en `ext/` a `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="e61e7-143">Quite todas las bibliotecas JAR que aparezcan en `lib/` que no estén en la siguiente lista:</span><span class="sxs-lookup"><span data-stu-id="e61e7-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

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

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="e61e7-144">Obtención del conector de Spark para Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e61e7-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="e61e7-145">Obtenga el conector de Spark para Azure Cosmos DB `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` y el SDK de Java para Cosmos DB `azure-documentdb-1.10.0.jar` en la página del [conector de Spark para Azure Cosmos DB en Github](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="e61e7-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="e61e7-146">También puede compilarlo localmente.</span><span class="sxs-lookup"><span data-stu-id="e61e7-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="e61e7-147">Dado que la versión más reciente de Spark-Gremlin se generó con Spark 1.6.1 y no es compatible con la versión Spark 2.0.2 que actualmente se usa en el conector de Spark para Azure Cosmos DB, puede compilar el código de TinkerPop3 más reciente e instalar manualmente los archivos JAR.</span><span class="sxs-lookup"><span data-stu-id="e61e7-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="e61e7-148">Haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e61e7-148">Do the following:</span></span>

    <span data-ttu-id="e61e7-149">a.</span><span class="sxs-lookup"><span data-stu-id="e61e7-149">a.</span></span> <span data-ttu-id="e61e7-150">Clone el conector de Spark para Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e61e7-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="e61e7-151">b.</span><span class="sxs-lookup"><span data-stu-id="e61e7-151">b.</span></span> <span data-ttu-id="e61e7-152">Compile TinkerPop3 (ya se hizo en pasos anteriores).</span><span class="sxs-lookup"><span data-stu-id="e61e7-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="e61e7-153">Instale todos los archivos JAR de TinkerPop 3.3.0-SNAPSHOT localmente.</span><span class="sxs-lookup"><span data-stu-id="e61e7-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="e61e7-154">c.</span><span class="sxs-lookup"><span data-stu-id="e61e7-154">c.</span></span> <span data-ttu-id="e61e7-155">Actualice `tinkerpop.version` `azure-documentdb-spark/pom.xml` a `3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="e61e7-156">d.</span><span class="sxs-lookup"><span data-stu-id="e61e7-156">d.</span></span> <span data-ttu-id="e61e7-157">Compile con Maven.</span><span class="sxs-lookup"><span data-stu-id="e61e7-157">Build with Maven.</span></span> <span data-ttu-id="e61e7-158">Los archivos JAR necesarios están ubicados en `target` y `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="e61e7-159">Copie los archivos JAR mencionados anteriormente en un directorio local en ~/azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="e61e7-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="e61e7-160">Distribuya las dependencias en los nodos de trabajo de Spark</span><span class="sxs-lookup"><span data-stu-id="e61e7-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="e61e7-161">Puesto que la transformación de datos de gráficos depende de TinkerPop3, debe distribuir las dependencias relacionadas a todos los nodos de trabajo de Spark.</span><span class="sxs-lookup"><span data-stu-id="e61e7-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="e61e7-162">Copie las dependencias de Gremlin mencionadas anteriormente, los archivos JAR del conector de Spark para CosmosDB y el SDK de Java para CosmosDB en los nodos de trabajo. Para ello, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e61e7-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="e61e7-163">a.</span><span class="sxs-lookup"><span data-stu-id="e61e7-163">a.</span></span> <span data-ttu-id="e61e7-164">Copie todos los archivos JAR en `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="e61e7-165">b.</span><span class="sxs-lookup"><span data-stu-id="e61e7-165">b.</span></span> <span data-ttu-id="e61e7-166">Obtenga la lista de todos los nodos de trabajo de Spark, que se encuentra en el panel de Ambari, en la lista `Spark2 Clients` de la sección `Spark2`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="e61e7-167">c.</span><span class="sxs-lookup"><span data-stu-id="e61e7-167">c.</span></span> <span data-ttu-id="e61e7-168">Copie ese directorio en cada uno de los nodos.</span><span class="sxs-lookup"><span data-stu-id="e61e7-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="e61e7-169">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="e61e7-169">Set up the environment variables</span></span>

1. <span data-ttu-id="e61e7-170">Busque la versión HDP del clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="e61e7-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="e61e7-171">Es el nombre del directorio en `/usr/hdp/` (por ejemplo, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="e61e7-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="e61e7-172">Establezca hdp.version para todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="e61e7-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="e61e7-173">En el panel de Ambari, vaya a la **sección de YARN** > **Configs** (Configuraciones)  > **Advanced** (Avanzadas) y luego haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e61e7-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="e61e7-174">a.</span><span class="sxs-lookup"><span data-stu-id="e61e7-174">a.</span></span> <span data-ttu-id="e61e7-175">En `Custom yarn-site`, agregue una nueva propiedad `hdp.version` con el valor de la versión de HDP en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="e61e7-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="e61e7-176">b.</span><span class="sxs-lookup"><span data-stu-id="e61e7-176">b.</span></span> <span data-ttu-id="e61e7-177">Guarde las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="e61e7-177">Save the configurations.</span></span> <span data-ttu-id="e61e7-178">Aparecen advertencias, pero puede ignorarlas.</span><span class="sxs-lookup"><span data-stu-id="e61e7-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="e61e7-179">c.</span><span class="sxs-lookup"><span data-stu-id="e61e7-179">c.</span></span> <span data-ttu-id="e61e7-180">Reinicie los servicios YARN y Oozie tal y como indican los iconos de notificación.</span><span class="sxs-lookup"><span data-stu-id="e61e7-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="e61e7-181">Establezca las siguientes variables de entorno en el nodo principal (reemplace los valores según corresponda):</span><span class="sxs-lookup"><span data-stu-id="e61e7-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="e61e7-182">Preparación de la configuración de grafos</span><span class="sxs-lookup"><span data-stu-id="e61e7-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="e61e7-183">Cree un archivo de configuración con los parámetros de conexión de Azure Cosmos DB y la configuración de Spark, y colóquelo en `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for the driver and executors
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

2. <span data-ttu-id="e61e7-184">Actualice `spark.driver.extraClassPath` y `spark.executor.extraClassPath` para incluir el directorio de los archivos JAR que se han distribuido en el paso anterior; en este caso, `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="e61e7-185">Proporcione los detalles siguientes para Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="e61e7-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="e61e7-186">Carga del gráfico de TinkerPop y su almacenamiento en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e61e7-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="e61e7-187">Para demostrar cómo se conserva un gráfico en Azure Cosmos DB, en este ejemplo se usa el gráfico moderno TinkerPop predefinido por TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="e61e7-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="e61e7-188">El gráfico se almacena en formato de Kryo y se proporciona en el repositorio de TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="e61e7-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="e61e7-189">Como está ejecutando Gremlin en modo YARN, debe permitir que los datos del gráfico estén disponibles en el sistema de archivos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e61e7-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="e61e7-190">Use los comandos siguientes para crear un directorio y copiar en él el archivo de gráficos local.</span><span class="sxs-lookup"><span data-stu-id="e61e7-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="e61e7-191">Actualice temporalmente el archivo `gremlin-spark.properties` para que use `GryoInputFormat` para leer el gráfico.</span><span class="sxs-lookup"><span data-stu-id="e61e7-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="e61e7-192">También indique `inputLocation` como el directorio creado, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e61e7-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="e61e7-193">Inicie la consola de Gremlin y, a continuación, cree los siguientes pasos de cálculo para conservar los datos en la colección de Azure Cosmos DB configurada:</span><span class="sxs-lookup"><span data-stu-id="e61e7-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="e61e7-194">a.</span><span class="sxs-lookup"><span data-stu-id="e61e7-194">a.</span></span> <span data-ttu-id="e61e7-195">Cree el gráfico `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="e61e7-196">b.</span><span class="sxs-lookup"><span data-stu-id="e61e7-196">b.</span></span> <span data-ttu-id="e61e7-197">Use SparkGraphComputer para escribir: `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="e61e7-198">Desde el Explorador de datos, puede comprobar que los datos se han conservado en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e61e7-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="e61e7-199">Carga del gráfico desde Azure Cosmos DB y ejecución de las consultas de Gremlin</span><span class="sxs-lookup"><span data-stu-id="e61e7-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="e61e7-200">Para cargar el gráfico, edite `gremlin-spark.properties` para establecer `graphReader` en `DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="e61e7-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="e61e7-201">Cargue el gráfico, recorra los datos y ejecute con ellos consultas de Gremlin siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e61e7-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="e61e7-202">a.</span><span class="sxs-lookup"><span data-stu-id="e61e7-202">a.</span></span> <span data-ttu-id="e61e7-203">Inicie la consola de Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="e61e7-204">b.</span><span class="sxs-lookup"><span data-stu-id="e61e7-204">b.</span></span> <span data-ttu-id="e61e7-205">Cree el gráfico con la configuración `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="e61e7-206">c.</span><span class="sxs-lookup"><span data-stu-id="e61e7-206">c.</span></span> <span data-ttu-id="e61e7-207">Cree un recorrido de gráfico con SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="e61e7-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="e61e7-208">d.</span><span class="sxs-lookup"><span data-stu-id="e61e7-208">d.</span></span> <span data-ttu-id="e61e7-209">Ejecute las siguientes consultas de gráfico de Gremlin:</span><span class="sxs-lookup"><span data-stu-id="e61e7-209">Run the following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="e61e7-210">Para ver un registro más detallado, configure el nivel de registro de `conf/log4j-console.properties` en un nivel más detallado.</span><span class="sxs-lookup"><span data-stu-id="e61e7-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="e61e7-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e61e7-211">Next steps</span></span>

<span data-ttu-id="e61e7-212">En este artículo de inicio rápido, ha aprendido cómo trabajar con gráficos mediante la combinación de Azure Cosmos DB y Spark.</span><span class="sxs-lookup"><span data-stu-id="e61e7-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
