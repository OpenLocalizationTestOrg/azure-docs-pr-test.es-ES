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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB: análisis de gráficos mediante Spark y Apache TinkerPop Gremlin

[Base de datos de Azure Cosmos](introduction.md) es Hola servicio de base de datos distribuidos globalmente, varios modelos de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todas ellas beneficiarán de las capacidades de distribución global y escalado horizontal de hello en núcleo de hello de la base de datos de Azure Cosmos. Azure Cosmos DB admite cargas de trabajo gráficas de procesamiento de transacciones en línea (OLTP) que usan [Apache TinkerPop Gremlin](graph-introduction.md).

[Spark](http://spark.apache.org/) es un proyecto de Apache Software Foundation que se centra en el procesamiento de datos OLAP (procesamiento analítico en línea) de uso general. Spark proporciona un híbrido en memoria/disco basada en modelo informático distribuido que sea similar toohello Hadoop MapReduce modelo. Puede implementar Apache Spark en nube de hello mediante [HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Mediante la combinación de Azure Cosmos DB y Spark, puede ejecutar tanto cargas de trabajo OLTP como OLAP cuando use Gremlin. Este artículo de inicio rápido muestra cómo toorun Gremlin consultas en base de datos de Azure Cosmos en un clúster de Azure HDInsight Spark.

## <a name="prerequisites"></a>Requisitos previos

Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:
* Clúster de Azure HDInsight Spark 2.0
* JDK 1.8+ (si no tiene JDK, ejecute `apt-get install default-jdk`.)
* Maven (si no tiene Maven, ejecute `apt-get install maven`.)
* Una suscripción de Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

Para obtener información acerca de cómo tooset de un clúster de Azure HDInsight Spark, consulte [clústeres de HDInsight de aprovisionamiento](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Creación de una cuenta de base de datos de Azure Cosmos DB

En primer lugar, cree una cuenta de base de datos con API Graph hello haciendo Hola siguiente:

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Incorporación de una colección

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Obtención de Apache TinkerPop

Obtener Apache TinkerPop haciendo Hola siguiente:

1. Nodo principal de toohello remoto hello del clúster de HDInsight `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Clonar el código fuente de hello TinkerPop3, genérelo localmente e instálelo tooMaven caché.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Instalar Hola Spark-Gremlin complemento 

    a. instalación de Hola de hello complemento administra uva. Rellenar la información de los repositorios de Hola de uva para poder descargar Hola complemento y sus dependencias. 

      Crear archivo de configuración uva hello si no está presente en `~/.groovy/grapeConfig.xml`. Usar hello después de configuración:

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

    b. Inicie la consola de Gremlin `bin/gremlin.sh`.
        
    c. Instalar Hola Spark-Gremlin complemento con versión 3.3.0-SNAPSHOT, que basa en los pasos anteriores de hello:

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

4. Compruebe si toosee `Hadoop-Gremlin` se activa con `:plugin list`. Deshabilitar este complemento, ya que podría interferir con hello Spark Gremlin complemento `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>Preparación de las dependencias de TinkerPop3

Al generar TinkerPop3 en el paso anterior de hello, proceso hello también extrajo todas las dependencias de archivo jar para Spark y Hadoop en el directorio de destino de Hola. Usar archivos JAR Hola que previamente se instala con HDI y extracción en dependencias adicionales solo según sea necesario.

1. Directorio de destino de Gremlin consola vaya toohello en `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Mover todos los archivos JAR en `ext/` demasiado`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Quitar todos los jar de bibliotecas en `lib/` que es hello no en lista siguiente:

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Obtener el conector de Azure Cosmos DB Spark Hola

1. Obtener el conector de Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` y el SDK de Java de Cosmos DB `azure-documentdb-1.10.0.jar` de [Cosmos DB Spark conector de Azure en GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. También puede compilarlo localmente. Porque la versión más reciente de Hola de Spark Gremlin se ha generado con Spark 1.6.1 y no es compatible con Spark 2.0.2, que se utiliza actualmente en el conector de Azure Cosmos DB Spark hello, puede compilar código de hello más reciente TinkerPop3 e instalar archivos JAR Hola manualmente. Hola siguientes:

    a. Clonación de conector de Azure Cosmos DB Spark Hola.

    b. Compile TinkerPop3 (ya se hizo en pasos anteriores). Instale todos los archivos JAR de TinkerPop 3.3.0-SNAPSHOT localmente.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Actualización `tinkerpop.version` `azure-documentdb-spark/pom.xml` demasiado`3.3.0-SNAPSHOT`.
    
    d. Compile con Maven. Hello archivos JAR necesario se colocan en `target` y `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Hola de copia se ha mencionado previamente directorio local de archivos JAR tooa en ~ / spark de documentos de azure:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Distribuir los nodos de trabajador de hello dependencias toohello Spark 

1. Como transformación Hola de datos del gráfico depende de TinkerPop3, debe distribuir Hola relacionados con nodos de trabajador de dependencias tooall Spark.

2. Hola de copia mencionó anteriormente Gremlin dependencias, Hola jar de conector CosmosDB Spark y nodos de trabajador de SDK de Java CosmosDB toohello haciendo Hola siguiente:

    a. Copie todos los archivos JAR hello en `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Obtener lista de Hola de todos los nodos de trabajador de Spark, que encontrará en el panel de Ambari, Hola `Spark2 Clients` lista Hola `Spark2` sección.

    c. Copie ese tooeach del directorio de nodos de Hola.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Establecer las variables de entorno de Hola

1. Encontrar Hola HDP versión de clúster de Spark Hola. Se trata de nombre de directorio de hello en `/usr/hdp/` (por ejemplo, 2.5.4.2-7).

2. Establezca hdp.version para todos los nodos. En el panel de Ambari, vaya demasiado**sección YARN** > **configuraciones** > **avanzadas**y, a continuación, Hola siguientes: 
 
    a. En `Custom yarn-site`, agregar una nueva propiedad `hdp.version` con el valor de Hola de versión HDP hello en el nodo principal de Hola. 
     
    b. Guardar las configuraciones de Hola. Aparecen advertencias, pero puede ignorarlas. 
     
    c. Reinicie los servicios YARN y Oozie de hello como iconos de notificación de hello indican.

3. Hola de conjunto después de las variables de entorno en el nodo principal de hello (reemplazar valores de hello según corresponda):

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Preparar la configuración del gráfico de Hola

1. Cree un archivo de configuración con hello parámetros de conexión de base de datos de Azure Cosmos e inspirará configuración y colóquelo en `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

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

2. Hola de actualización `spark.driver.extraClassPath` y `spark.executor.extraClassPath` tooinclude directorio de Hola de archivos JAR Hola distribuido en el paso anterior de hello, en este caso `/home/sshuser/azure-documentdb-spark/*`.

3. Proporcionar Hola siga detalles para la base de datos de Azure Cosmos:

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Cargar hello TinkerPop gráfico y guardar tooAzure Cosmos DB
toodemonstrate cómo toopersist un gráfico en la base de datos de Azure Cosmos, este ejemplo utiliza Hola TinkerPop predefinidos TinkerPop moderna gráfico. gráfico de Hola se almacena en formato de Kryo y se proporciona en el repositorio de TinkerPop Hola.

1. Porque se está ejecutando Gremlin en modo YARN, debe realizar datos de gráfico de hello disponibles en el sistema de archivos Hadoop Hola. Siguiente de hello use comandos toomake un directorio y archivo de copia hello gráfico local en él. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Actualizar temporalmente hello `gremlin-spark.properties` archivo toouse `GryoInputFormat` gráfico de hello tooread. También indicar `inputLocation` como directorio de hello crea, como en el siguiente hello:

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Inicie la consola de Gremlin y, a continuación, crear Hola después de cálculo pasos toopersist datos toohello Configurar base de datos de Azure Cosmos colección:  

    a. Crear el gráfico de hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. Use SparkGraphComputer para escribir: `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

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

4. Desde el Explorador de datos, puede comprobar que Hola ha sido datos persistentes tooAzure Cosmos DB.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Gráfico de Hola de carga de base de datos de Azure Cosmos y ejecutar consultas de Gremlin

1. gráfico de hello tooload, editar `gremlin-spark.properties` tooset `graphReader` demasiado`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. Gráfico de Hola de carga, recorrer datos hello y ejecutar consultas de Gremlin con él haciendo Hola siguiente:

    a. Iniciar hello Gremlin consola `bin/gremlin.sh`.

    b. Crear el gráfico de hello con la configuración de hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Cree un recorrido de gráfico con SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Ejecute hello las siguientes consultas de gráfico Gremlin:

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
> toosee más detallada de registro, Establece el nivel de registro de hello `conf/log4j-console.properties` tooa nivel más detallado.
>

## <a name="next-steps"></a>Pasos siguientes

En este artículo de inicio rápido, ha aprendido cómo toowork con gráficos mediante la combinación de base de datos de Azure Cosmos y Spark.

> [!div class="nextstepaction"]
