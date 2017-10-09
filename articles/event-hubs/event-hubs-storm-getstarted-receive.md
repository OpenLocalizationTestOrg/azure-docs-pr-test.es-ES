---
title: aaaReceive eventos desde los centros de eventos de Azure con Apache Storm | Documentos de Microsoft
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
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="8e75a-103">Recepción de eventos desde Event Hubs mediante Apache Storm</span><span class="sxs-lookup"><span data-stu-id="8e75a-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="8e75a-104">[Apache Storm](https://storm.incubator.apache.org) es un sistema distribuido de cálculo en tiempo real que simplifica el procesamiento confiable de flujos de datos sin enlazar.</span><span class="sxs-lookup"><span data-stu-id="8e75a-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="8e75a-105">Esta sección muestra cómo toouse un aluvión de concentradores de eventos de Azure apetezca charlar tooreceive eventos desde los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="8e75a-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="8e75a-106">Con Apache Storm, se pueden dividir los eventos en varios procesos hospedados en distintos nodos.</span><span class="sxs-lookup"><span data-stu-id="8e75a-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="8e75a-107">Hola integración de los centros de eventos con Storm simplifica el consumo de eventos por puntos de forma transparente su progreso mediante una instalación de Zookeeper del aluvión, administrar los puntos de control persistentes y paralelo recibe de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="8e75a-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="8e75a-108">Para obtener más información acerca de los centros de eventos de recepción patrones, vea hello [información general de los centros de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="8e75a-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="8e75a-109">Creación del proyecto y adición de código</span><span class="sxs-lookup"><span data-stu-id="8e75a-109">Create project and add code</span></span>

<span data-ttu-id="8e75a-110">Este tutorial se usa un [aluvión de HDInsight] [ HDInsight Storm] instalación, que se incluye con hello apetezca charlar centros de eventos ya disponible.</span><span class="sxs-lookup"><span data-stu-id="8e75a-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="8e75a-111">Siga hello [HDInsight Storm - Introducción](../hdinsight/hdinsight-storm-overview.md) procedimiento toocreate un nuevo HDInsight del clúster y conecte tooit a través de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="8e75a-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="8e75a-112">Hola copia `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` entorno de desarrollo local tooyour de archivo.</span><span class="sxs-lookup"><span data-stu-id="8e75a-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="8e75a-113">Esto contiene Hola eventos-storm-pitorro.</span><span class="sxs-lookup"><span data-stu-id="8e75a-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="8e75a-114">Usar hello siguiente paquete de comando tooinstall hello en el almacén local de Maven de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e75a-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="8e75a-115">Esto le permite tooadd como una referencia en hello aluvión de proyecto en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="8e75a-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="8e75a-116">En Eclipse, cree un proyecto Maven nuevo (haga clic en **Archivo**, **Nuevo** y, a continuación, en **Proyecto**).</span><span class="sxs-lookup"><span data-stu-id="8e75a-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="8e75a-117">Seleccione **Usar ubicación del área de trabajo predeterminada** y, a continuación, haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="8e75a-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="8e75a-118">Seleccione hello **maven-Arquetipo-inicio rápido** Arquetipo, a continuación, haga clic en **siguiente**</span><span class="sxs-lookup"><span data-stu-id="8e75a-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="8e75a-119">Inserte un **GroupId** y **ArtifactId** y, a continuación, haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="8e75a-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="8e75a-120">En **pom.xml**, agregar Hola siguiendo las dependencias en hello `<dependency>` nodo.</span><span class="sxs-lookup"><span data-stu-id="8e75a-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

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

9. <span data-ttu-id="8e75a-121">Hola **src** carpeta, cree un archivo denominado **Config.properties** copia hello siguen contenido, sustituyendo hello y `receive rule key` y `event hub name` valores:</span><span class="sxs-lookup"><span data-stu-id="8e75a-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="8e75a-122">Hola valor para **eventhub.receiver.credits** determina cuántos eventos se procesan por lotes antes de liberarlos canalización aluvión de toohello.</span><span class="sxs-lookup"><span data-stu-id="8e75a-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="8e75a-123">Para simplificar Hola simplicidad, este ejemplo establece este valor too10.</span><span class="sxs-lookup"><span data-stu-id="8e75a-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="8e75a-124">En producción, normalmente se debe establecer valores de toohigher; Por ejemplo, 1024.</span><span class="sxs-lookup"><span data-stu-id="8e75a-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="8e75a-125">Crear una nueva clase denominada **LoggerBolt** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8e75a-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
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
    
    <span data-ttu-id="8e75a-126">Este rayo Storm registra contenido Hola de eventos de hello recibido.</span><span class="sxs-lookup"><span data-stu-id="8e75a-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="8e75a-127">Esto se puede ampliar fácilmente toostore tuplas en un servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8e75a-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="8e75a-128">Hola [tutorial de analysis del sensor de HDInsight] utiliza estos mismos datos toostore de enfoque en HBase.</span><span class="sxs-lookup"><span data-stu-id="8e75a-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="8e75a-129">Cree una clase denominada **LogTopology** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8e75a-129">Create a class called **LogTopology** with hello following code:</span></span>
    
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
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
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

    <span data-ttu-id="8e75a-130">Esta clase crea un nuevo pitorro centros de eventos, mediante las propiedades de hello en tooinstantiate de archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e75a-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="8e75a-131">Es importante toonote que este ejemplo se crea tantos spouts tareas como número de Hola de particiones en el centro de eventos de hello, en orden toouse Hola máximo paralelismo permitido por ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8e75a-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e75a-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e75a-132">Next steps</span></span>
<span data-ttu-id="8e75a-133">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="8e75a-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="8e75a-134">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="8e75a-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="8e75a-135">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="8e75a-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8e75a-136">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8e75a-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[tutorial de analysis del sensor de HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
