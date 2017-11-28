---
title: "Recepción de eventos desde Azure Event Hubs mediante Apache Storm | Microsoft Docs"
description: "Introducción a la recepción de eventos desde Event Hubs mediante Apache Storm"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3e15370c7602276ef323708632b324fe05497f41
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="ace1b-103">Recepción de eventos desde Event Hubs mediante Apache Storm</span><span class="sxs-lookup"><span data-stu-id="ace1b-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="ace1b-104">[Apache Storm](https://storm.incubator.apache.org) es un sistema distribuido de cálculo en tiempo real que simplifica el procesamiento confiable de flujos de datos sin enlazar.</span><span class="sxs-lookup"><span data-stu-id="ace1b-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="ace1b-105">Esta sección muestra cómo utilizar un spout de Storm para Azure Event Hubs a fin de recibir eventos de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ace1b-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="ace1b-106">Con Apache Storm, se pueden dividir los eventos en varios procesos hospedados en distintos nodos.</span><span class="sxs-lookup"><span data-stu-id="ace1b-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="ace1b-107">La integración de los Centros de eventos con Storm simplifica el consumo de eventos al comprobar de forma transparente el progreso mediante la instalación de Zookeeper de Storm, la administración de puntos de comprobación persistentes y las recepciones en paralelo de los Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="ace1b-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="ace1b-108">Para más información sobre los patrones de recepción de Event Hubs, vea la [información general de Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="ace1b-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="ace1b-109">Creación del proyecto y adición de código</span><span class="sxs-lookup"><span data-stu-id="ace1b-109">Create project and add code</span></span>

<span data-ttu-id="ace1b-110">Este tutorial usa una instalación de [HDInsight Storm][HDInsight Storm], que integra el emisor de Event Hubs que ya está disponible.</span><span class="sxs-lookup"><span data-stu-id="ace1b-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="ace1b-111">Siga el procedimiento descrito en [Introducción a HDInsight Storm](../hdinsight/hdinsight-storm-overview.md) para crear un clúster nuevo de HDInsight y conectarlo a través del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ace1b-111">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="ace1b-112">Copie el archivo `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` en su entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="ace1b-112">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="ace1b-113">Contiene events-storm-spout.</span><span class="sxs-lookup"><span data-stu-id="ace1b-113">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="ace1b-114">Utilice el comando siguiente para instalar el paquete en el almacén Maven local.</span><span class="sxs-lookup"><span data-stu-id="ace1b-114">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="ace1b-115">Esto permite agregarlo como referencia en el proyecto de Storm en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="ace1b-115">This enables you to add it as a reference in the Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="ace1b-116">En Eclipse, cree un proyecto Maven nuevo (haga clic en **Archivo**, **Nuevo** y, a continuación, en **Proyecto**).</span><span class="sxs-lookup"><span data-stu-id="ace1b-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="ace1b-117">Seleccione **Usar ubicación del área de trabajo predeterminada** y, a continuación, haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="ace1b-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="ace1b-118">Seleccione el arquetipo **maven-archetype-quickstart** y, a continuación, haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="ace1b-118">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="ace1b-119">Inserte un **GroupId** y **ArtifactId** y, a continuación, haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="ace1b-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="ace1b-120">En **pom.xml**, agregue las siguientes dependencias en el nodo `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="ace1b-120">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. <span data-ttu-id="ace1b-121">En la carpeta **src**, cree un archivo llamado **Config.properties** y copie el siguiente contenido, sustituyendo los valores `receive rule key` y `event hub name`:</span><span class="sxs-lookup"><span data-stu-id="ace1b-121">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:</span></span>

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    <span data-ttu-id="ace1b-122">El valor de **eventhub.receiver.credits** determina cuántos eventos se procesan por lotes antes de liberarlos a la canalización de Storm.</span><span class="sxs-lookup"><span data-stu-id="ace1b-122">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="ace1b-123">Por simplicidad, este ejemplo establece el valor en 10.</span><span class="sxs-lookup"><span data-stu-id="ace1b-123">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="ace1b-124">En producción, se debe normalmente establecer en valores más altos; Por ejemplo, 1024.</span><span class="sxs-lookup"><span data-stu-id="ace1b-124">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="ace1b-125">Cree una clase nueva denominada **LoggerBolt** con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ace1b-125">Create a new class called **LoggerBolt** with the following code:</span></span>
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    <span data-ttu-id="ace1b-126">Este elemento de Storm registra el contenido de los eventos recibidos.</span><span class="sxs-lookup"><span data-stu-id="ace1b-126">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="ace1b-127">Esto se puede ampliar fácilmente para almacenar las tuplas en un servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ace1b-127">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="ace1b-128">El [tutorial de análisis de sensores de HDInsight] usa este mismo enfoque para almacenar datos en HBase.</span><span class="sxs-lookup"><span data-stu-id="ace1b-128">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="ace1b-129">Cree una clase denominada **LogTopology** con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ace1b-129">Create a class called **LogTopology** with the following code:</span></span>
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    <span data-ttu-id="ace1b-130">Esta clase crea un emisor de Event Hubs, utilizando las propiedades del archivo de configuración para crear una instancia.</span><span class="sxs-lookup"><span data-stu-id="ace1b-130">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="ace1b-131">Es importante tener en cuenta que este ejemplo crea tantas tareas de spout como número de particiones hay en el centro de eventos, para poder usar el paralelismo máximo permitido por ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="ace1b-131">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ace1b-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ace1b-132">Next steps</span></span>
<span data-ttu-id="ace1b-133">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ace1b-133">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="ace1b-134">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="ace1b-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="ace1b-135">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="ace1b-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ace1b-136">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ace1b-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
<span data-ttu-id="ace1b-137">[tutorial de análisis de sensores de HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span><span class="sxs-lookup"><span data-stu-id="ace1b-137">[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span></span>

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
