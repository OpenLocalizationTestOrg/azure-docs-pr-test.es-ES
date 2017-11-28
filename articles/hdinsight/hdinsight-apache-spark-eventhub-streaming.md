---
title: aaaUse Apache Spark streaming con concentradores de eventos de HDInsight de Azure | Documentos de Microsoft
description: "Compilar un ejemplo de transmisión por secuencias de Apache Spark en cómo toosend datos transmitir tooAzure centro de eventos y, a continuación, recibir los eventos de clúster de HDInsight Spark mediante una aplicación scala."
keywords: apache spark streaming de, streaming de spark, ejemplo de spark, ejemplo de streaming de apache spark, ejemplo de azure event hub, ejemplo de spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="e44a0-104">Streaming de Apache Spark: procesamiento de datos desde Azure Event Hubs con clústeres de Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e44a0-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="e44a0-105">En este artículo, se crea una transmisión por secuencias de ejemplo que implica Hola siguiendo los pasos de Apache Spark:</span><span class="sxs-lookup"><span data-stu-id="e44a0-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="e44a0-106">Un mensaje de tooingest la aplicación independiente que se usa en un centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="e44a0-107">Con dos enfoques diferentes, puede recuperar mensajes de saludo de concentrador de eventos en tiempo real con una aplicación se ejecuta en el clúster de Spark en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="e44a0-108">Compilar canalizaciones de analíticas de transmisión por secuencias sistemas de almacenamiento de toopersist datos toodifferent u obtener información de datos en marcha Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e44a0-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e44a0-109">Prerequisites</span></span>

* <span data-ttu-id="e44a0-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-110">An Azure subscription.</span></span> <span data-ttu-id="e44a0-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e44a0-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="e44a0-112">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e44a0-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e44a0-113">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="e44a0-114">Conceptos de streaming de Spark</span><span class="sxs-lookup"><span data-stu-id="e44a0-114">Spark Streaming concepts</span></span>

<span data-ttu-id="e44a0-115">Para obtener una explicación detallada del streaming de Spark consulte la [información general sobre el streaming de Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="e44a0-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="e44a0-116">HDInsight aporta hello tooa de características de transmisión por secuencias mismo Spark de Cluster Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="e44a0-117">¿Cómo funciona la solución?</span><span class="sxs-lookup"><span data-stu-id="e44a0-117">What does this solution do?</span></span>

<span data-ttu-id="e44a0-118">En este artículo, toocreate un ejemplo de transmisión por secuencias de Spark, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e44a0-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="e44a0-119">Cree un Centro de eventos de Azure, que será el que reciba una transmisión de eventos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="e44a0-120">Ejecutar una aplicación local independiente que genera eventos y lo inserta toohello concentrador de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="e44a0-121">se publica la aplicación de ejemplo de Hola que lo haga en [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="e44a0-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="e44a0-122">Ejecute una aplicación de streaming de forma remota en un clúster de Spark que lea los eventos de streaming desde el centro de eventos de Azure y lleve a cabo varios análisis y procesamientos de datos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="e44a0-123">Crear un centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="e44a0-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="e44a0-124">Inicie sesión en toohello [Portal de Azure](https://ms.portal.azure.com)y haga clic en **New** en hello parte superior izquierda de la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="e44a0-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="e44a0-125">Haga clic en **Internet de las cosas** y en **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="e44a0-126">![Creación de un centro de eventos para un ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="e44a0-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="e44a0-127">Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="e44a0-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="e44a0-128">Elija Hola tarifa (básico o estándar).</span><span class="sxs-lookup"><span data-stu-id="e44a0-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="e44a0-129">Además, elija una suscripción de Azure, el grupo de recursos y la ubicación en el recurso que hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e44a0-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="e44a0-130">Haga clic en **crear** el espacio de nombres de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="e44a0-131">![Aportación de un nombre de centro de evento para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="e44a0-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="e44a0-132">Debe seleccionar Hola mismo **ubicación** como el clúster de Apache Spark en HDInsight tooreduce latencia y los costos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="e44a0-133">En la lista de espacio de nombres de los centros de eventos de hello, haga clic en el espacio de nombres de hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="e44a0-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="e44a0-134">En la hoja de espacio de nombres de hello, haga clic en **centros de eventos**y, a continuación, haga clic en **+ concentrador de eventos** toocreate un nuevo centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="e44a0-135">![Creación de un centro de eventos para un ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="e44a0-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="e44a0-136">Escriba un nombre para el concentrador de eventos, conjunto Hola partición recuento too10 y too1 de retención de mensajes.</span><span class="sxs-lookup"><span data-stu-id="e44a0-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="e44a0-137">No nos estamos archivar los mensajes de Hola en esta solución para que pueda dejar resto hello como valor predeterminado y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="e44a0-138">![Aportación de detalles del centro de evento para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="e44a0-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="e44a0-139">Hola recién creado concentrador de eventos se muestra en la hoja de concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="e44a0-140">![Ver centro de eventos de ejemplo de Hola Spark streaming](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "concentrador de eventos de vista para hello inspirará ejemplo de transmisión por secuencias")</span><span class="sxs-lookup"><span data-stu-id="e44a0-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="e44a0-141">En la hoja de espacio de nombres de hello (no Hola específico concentrador de eventos hoja), haga clic en **directivas de acceso compartido**y, a continuación, haga clic en **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="e44a0-142">![Establecer directivas de concentrador de eventos de ejemplo de Hola Spark streaming](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "directivas de concentrador de eventos establecido para hello inspirará ejemplo de transmisión por secuencias")</span><span class="sxs-lookup"><span data-stu-id="e44a0-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="e44a0-143">Haga clic en Hola de hello copia botón toocopy **RootManageSharedAccessKey** principal Portapapeles de toohello de cadena de conexión y la clave.</span><span class="sxs-lookup"><span data-stu-id="e44a0-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="e44a0-144">Guardar estas toouse más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="e44a0-145">![Ver claves de directiva de centro de eventos de ejemplo de Hola Spark streaming](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "claves de directiva de centro de eventos de vista para hello inspirará ejemplo de transmisión por secuencias")</span><span class="sxs-lookup"><span data-stu-id="e44a0-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="e44a0-146">Enviar mensajes tooAzure centro de eventos mediante una aplicación de ejemplo Scala</span><span class="sxs-lookup"><span data-stu-id="e44a0-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="e44a0-147">En esta sección utiliza local Scala aplicación independiente que se genera una secuencia de eventos y lo envía tooAzure concentrador de eventos que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e44a0-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="e44a0-148">Esta aplicación está disponible en GitHub en [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="e44a0-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="e44a0-149">Hola aquí da por sentado que ya ha bifurcado este repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="e44a0-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="e44a0-150">Asegúrese de que tiene los siguientes Hola instalados en el equipo de Hola donde se ejecuta esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="e44a0-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="e44a0-151">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="e44a0-151">Oracle Java Development kit.</span></span> <span data-ttu-id="e44a0-152">Puede instalarlo desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="e44a0-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="e44a0-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="e44a0-153">Apache Maven.</span></span> <span data-ttu-id="e44a0-154">Puede descargarla [aquí](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="e44a0-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="e44a0-155">Existen instrucciones tooinstall Maven [aquí](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="e44a0-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="e44a0-156">Abra un símbolo del sistema, navegue ubicación toohello clonar el repositorio de GitHub de Hola para aplicación de Scala de ejemplo de Hola y ejecute hello tras la aplicación de comando toobuild Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="e44a0-157">Hola jar de salida para la aplicación hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, se crea en **/target** directory.</span><span class="sxs-lookup"><span data-stu-id="e44a0-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="e44a0-158">Utilice este JAR más adelante en esta solución completa de artículo tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="e44a0-159">Crear mensajes de tooreceive la aplicación de centro de eventos en un clúster de Spark</span><span class="sxs-lookup"><span data-stu-id="e44a0-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="e44a0-160">Tenemos dos tooconnect enfoques Spark transmisión por secuencias y centros de eventos de Azure, conexión basada en el receptor y conexión directa basada en DStream.</span><span class="sxs-lookup"><span data-stu-id="e44a0-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="e44a0-161">Direct-DStream-based se introdujo en enero de 2017, en la versión de Hola 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="e44a0-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="e44a0-162">Se suponía que conexión basada en el receptor de tooreplace Hola original sea más eficiente y eficaz de los recursos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="e44a0-163">Encontrará más información en [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="e44a0-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="e44a0-164">Direct DStream solo admite Spark 2.0+.</span><span class="sxs-lookup"><span data-stu-id="e44a0-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="e44a0-165">Compilar aplicaciones con el conector de hello dependencia toospark eventhubs</span><span class="sxs-lookup"><span data-stu-id="e44a0-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="e44a0-166">También publicaremos Hola versión de Spark EventHubs en GitHub de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="e44a0-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="e44a0-167">versión de almacenamiento provisional de Hola de toouse de Spark EventHubs, Hola primer paso es tooindicate GitHub como Hola repositorio de origen mediante la adición de hello después toopom.xml de entrada:</span><span class="sxs-lookup"><span data-stu-id="e44a0-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="e44a0-168">A continuación, puede agregar Hola después de la versión preliminar de dependencia tooyour proyecto tootake Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="e44a0-169">Dependencia de Maven</span><span class="sxs-lookup"><span data-stu-id="e44a0-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="e44a0-170">Dependencia de SBT</span><span class="sxs-lookup"><span data-stu-id="e44a0-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="e44a0-171">Conexión de Direct DStream</span><span class="sxs-lookup"><span data-stu-id="e44a0-171">Direct DStream Connection</span></span>

<span data-ttu-id="e44a0-172">En [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) se puede descargar un archivo JAR pregenerado que contiene ejemplos en los que se usa Direct DStream.</span><span class="sxs-lookup"><span data-stu-id="e44a0-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="e44a0-173">archivo jar de Hello contiene tres ejemplos cuyo código fuente está disponible en [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="e44a0-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="e44a0-174">Si tomamos [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e44a0-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="e44a0-175">Hola por encima de ejemplo, `eventhubParameters` instancia única de EventHubs de hello parámetros tooa específico y tienen toopass se toohello `createDirectStreams` API que crea un espacio de nombres de los centros de eventos de DStream directo objeto asignación tooa.</span><span class="sxs-lookup"><span data-stu-id="e44a0-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="e44a0-176">A través de objeto de hello DStream directa, puede llamar a cualquier API DStream proporcionada por marco API de transmisión por secuencias de Spark.</span><span class="sxs-lookup"><span data-stu-id="e44a0-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="e44a0-177">En este ejemplo, calculamos frecuencia Hola de cada palabra en intervalos de hello último lote micro 3.</span><span class="sxs-lookup"><span data-stu-id="e44a0-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="e44a0-178">Conexión basada en un receptor</span><span class="sxs-lookup"><span data-stu-id="e44a0-178">Receiver-based Connection</span></span>

<span data-ttu-id="e44a0-179">Está disponible en una aplicación de ejemplo escrita en Scala, que recibe eventos y destinos de enrutamiento hello toodifferent, de transmisión por secuencias de Spark [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="e44a0-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="e44a0-180">Siga los pasos de Hola por debajo de la aplicación de hello tooupdate para la configuración del centro de eventos y cree Hola jar de salida.</span><span class="sxs-lookup"><span data-stu-id="e44a0-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="e44a0-181">Inicie la IDEA de IntelliJ y de hello iniciar pantalla Seleccione **desproteger del Control de versiones** y, a continuación, haga clic en **Git**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="e44a0-182">![Ejemplo de streaming de Apache Spark: obtener orígenes de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span><span class="sxs-lookup"><span data-stu-id="e44a0-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="e44a0-183">Hola **clon repositorio** cuadro de diálogo, proporcionar tooclone del repositorio de Git Hola URL toohello desde, especifique Hola directory tooclone a y, a continuación, haga clic en **clon**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="e44a0-184">![Ejemplo de streaming de Apache Spark: clonar de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span><span class="sxs-lookup"><span data-stu-id="e44a0-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="e44a0-185">Siga las indicaciones de hello hasta que el proyecto de hello completamente se clona.</span><span class="sxs-lookup"><span data-stu-id="e44a0-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="e44a0-186">Presione **Alt + 1** tooopen hello **vista proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="e44a0-187">Debe parecerse al siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="e44a0-188">![Ejemplo de streaming de Apache Spark: vista de proyecto](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span><span class="sxs-lookup"><span data-stu-id="e44a0-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="e44a0-189">Asegúrese de que se compila código de la aplicación hello con Java8.</span><span class="sxs-lookup"><span data-stu-id="e44a0-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="e44a0-190">tooensure, haga clic en **archivo**, haga clic en **estructura del proyecto**y en hello **proyecto** ficha, asegúrese de que el nivel de lenguaje de proyecto se establece demasiado**8 - las expresiones lambda, tipo las anotaciones, etc.**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="e44a0-191">![Ejemplo de streaming de Apache Spark: establecer compilador](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span><span class="sxs-lookup"><span data-stu-id="e44a0-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="e44a0-192">Abra hello **pom.xml** y asegúrese de que la versión de Hola Spark es correcta.</span><span class="sxs-lookup"><span data-stu-id="e44a0-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="e44a0-193">En `<properties>` nodo, busque el siguiente fragmento de código de hello y comprobar la versión de Hola Spark.</span><span class="sxs-lookup"><span data-stu-id="e44a0-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="e44a0-194">aplicación Hello requiere un archivo jar de dependencia llama **jar del controlador JDBC**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="e44a0-195">Se trata de mensajes de saludo de toowrite necesario recibidos del concentrador de eventos en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="e44a0-196">Puede descargar este archivo jar (versión 4.1, o las versiones posteriores) desde [aquí](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="e44a0-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="e44a0-197">Agregar referencia toothis jar en la biblioteca de proyectos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="e44a0-198">Lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e44a0-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="e44a0-199">En la ventana de IDEA IntelliJ donde hay aplicación hello abierta, haga clic en **archivo**, haga clic en **estructura del proyecto**y, a continuación, haga clic en **bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="e44a0-200">Haga clic en hello agregar icono (![agregar icono](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), haga clic en **Java**y, a continuación, navegue ubicación toohello donde descargó jar de controlador JDBC de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="e44a0-201">Siga Hola indicaciones tooadd Hola jar archivo toohello biblioteca de proyectos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="e44a0-202">![agregar dependencias que faltan](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Agregar archivos jar de dependencias que faltan")</span><span class="sxs-lookup"><span data-stu-id="e44a0-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="e44a0-203">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-203">Click **Apply**.</span></span>

7. <span data-ttu-id="e44a0-204">Crear archivo jar de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="e44a0-204">Create hello output jar file.</span></span> <span data-ttu-id="e44a0-205">Realizar pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="e44a0-206">Hola **estructura del proyecto** cuadro de diálogo, haga clic en **artefactos** y, a continuación, haga clic en hello además de símbolos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="e44a0-207">En el cuadro de diálogo emergente de hello, haga clic en **JAR**y, a continuación, haga clic en **de módulos con dependencias**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="e44a0-208">![Ejemplo de streaming de Apache Spark: crear archivo JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span><span class="sxs-lookup"><span data-stu-id="e44a0-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="e44a0-209">Hola **crear JAR de módulos** diálogo cuadro, haga clic en el botón de puntos suspensivos hello (![puntos suspensivos](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) contra Hola **clase principal**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="e44a0-210">Hola **seleccionar clase de Main** diálogo cuadro, seleccione cualquiera de las clases disponibles de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="e44a0-211">![Ejemplo de streaming de Apache Spark: seleccionar clase para el archivo jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span><span class="sxs-lookup"><span data-stu-id="e44a0-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="e44a0-212">Hola **crear JAR de módulos** diálogo cuadro, asegúrese de que esa opción Hola demasiado**extraer toohello destino JAR** está seleccionada y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="e44a0-213">Así se crea un archivo JAR único con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="e44a0-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="e44a0-214">![Ejemplo de streaming de Apache Spark: crear archivo jar desde módulos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span><span class="sxs-lookup"><span data-stu-id="e44a0-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="e44a0-215">Hola **salida diseño** ficha enumera todos los archivos JAR Hola que se incluyen como parte del proyecto de Maven Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="e44a0-216">Puede seleccionar y Hola delete aquellos en los que Hola Scala aplicación no tiene ninguna dependencia directa.</span><span class="sxs-lookup"><span data-stu-id="e44a0-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="e44a0-217">Para la aplicación hello vamos a crear a continuación, puede quitar todos menos Hola último (**spark-transmisión por secuencias de datos-persistencia-ejemplos compilan salida**).</span><span class="sxs-lookup"><span data-stu-id="e44a0-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="e44a0-218">Seleccione toodelete de archivos JAR de hello y, a continuación, haga clic en hello **eliminar** icono (![icono Eliminar](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="e44a0-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="e44a0-219">![Ejemplo de streaming de Apache Spark: eliminar archivos jar extraídos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span><span class="sxs-lookup"><span data-stu-id="e44a0-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="e44a0-220">Asegúrese de que **compilar en hacer** casilla está activada, lo que garantiza que jar Hola se crea cada vez proyecto Hola se compila o se actualiza.</span><span class="sxs-lookup"><span data-stu-id="e44a0-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="e44a0-221">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="e44a0-222">Hola **salida diseño** ficha, en parte inferior de Hola de Hola **elementos disponibles** cuadro, tiene que agregar biblioteca de proyectos de toohello anterior archivo jar JDBC de SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="e44a0-223">Debe agregar esta toohello **salida diseño** ficha. Haga clic en archivo jar de hello y, a continuación, haga clic en **extraer en la raíz de salida**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="e44a0-224">![Ejemplo de streaming de Apache Spark: extraer archivo jar de dependencia](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span><span class="sxs-lookup"><span data-stu-id="e44a0-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="e44a0-225">Hola **salida diseño** ficha debe tener el siguiente aspecto.</span><span class="sxs-lookup"><span data-stu-id="e44a0-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="e44a0-226">![Ejemplo de streaming de Apache Spark: pestaña de salida final](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span><span class="sxs-lookup"><span data-stu-id="e44a0-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="e44a0-227">Hola **estructura del proyecto** cuadro de diálogo, haga clic en **aplicar** y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="e44a0-228">En la barra de menús de hello, haga clic en **generar**y, a continuación, haga clic en **proyecto realizar**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="e44a0-229">También puede hacer clic en **Generar artefactos** jar de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e44a0-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="e44a0-230">jar de salida Hello se crea una en **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="e44a0-231">![Ejemplo de streaming de Apache Spark: salida de archivo JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span><span class="sxs-lookup"><span data-stu-id="e44a0-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="e44a0-232">Ejecutar aplicación hello de forma remota en un clúster de Spark mediante Livio</span><span class="sxs-lookup"><span data-stu-id="e44a0-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="e44a0-233">En este artículo se utiliza Livio toorun Hola Apache Spark streaming aplicación remotamente en un clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="e44a0-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="e44a0-234">Para obtener información detallada sobre cómo agrupar toouse Livio con HDInsight Spark, consulte [enviar trabajos remotamente clúster tooan Apache Spark en HDInsight de Azure](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="e44a0-235">Antes de que puede empezar a ejecutar la aplicación de transmisión por secuencias de Spark hello, hay un par de cosas que debe hacer:</span><span class="sxs-lookup"><span data-stu-id="e44a0-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="e44a0-236">Iniciar aplicación toogenerate eventos de hello local independiente y envían tooEvent concentrador.</span><span class="sxs-lookup"><span data-stu-id="e44a0-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="e44a0-237">El comando siguiente de Hola de uso toodo así:</span><span class="sxs-lookup"><span data-stu-id="e44a0-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="e44a0-238">Hola copia jar de transmisión por secuencias (**spark archivo-transmisión por secuencias de datos-persistencia-examples.jar**) toohello asociada Hola clúster de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="e44a0-239">Esto hace que Hola jar accesible tooLivy.</span><span class="sxs-lookup"><span data-stu-id="e44a0-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="e44a0-240">Puede usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), por lo que utilidad, toodo un comando de línea.</span><span class="sxs-lookup"><span data-stu-id="e44a0-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="e44a0-241">Hay mucho de otros clientes puede usar datos de tooupload.</span><span class="sxs-lookup"><span data-stu-id="e44a0-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="e44a0-242">Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="e44a0-243">Instalar CURL en donde se ejecuta estas aplicaciones desde el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="e44a0-244">Utilizamos CURL tooinvoke Hola Hola de Livio extremos toorun trabajos de forma remota.</span><span class="sxs-lookup"><span data-stu-id="e44a0-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="e44a0-245">Hola ejecución Spark streaming tooreceive Hola eventos de aplicación en un Blob de almacenamiento de Azure como texto</span><span class="sxs-lookup"><span data-stu-id="e44a0-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="e44a0-246">Abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute hello siguiente comando (reemplazar nombre de usuario/contraseña y clúster nombre):</span><span class="sxs-lookup"><span data-stu-id="e44a0-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="e44a0-247">Hola parámetros en el archivo hello **inputBlob.txt** se definen como sigue:</span><span class="sxs-lookup"><span data-stu-id="e44a0-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="e44a0-248">Vamos a explicar cuáles son los parámetros de hello en el archivo de entrada de hello:</span><span class="sxs-lookup"><span data-stu-id="e44a0-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="e44a0-249">**archivo** es Hola el archivo jar de ruta de acceso toohello aplicación hello Azure cuenta de almacenamiento asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="e44a0-250">**className** es Hola nombre de clase de hello en jar Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="e44a0-251">**args** es Hola lista de argumentos requeridos por la clase hello</span><span class="sxs-lookup"><span data-stu-id="e44a0-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="e44a0-252">**numExecutors** es Hola número de núcleos usados por Hola de Spark toorun transmisión por secuencias la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e44a0-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="e44a0-253">Siempre debería ser al menos dos veces el número de Hola de particiones de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e44a0-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="e44a0-254">**executorMemory**, **executorCores**, **driverMemory** son parámetros utilizados tooassign requerido recursos toohello de transmisión por secuencias la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e44a0-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="e44a0-255">No es necesario toocreate Hola carpetas de salida (EventCheckpoint, conteo de eventos/EventCount10) que se utilizan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="e44a0-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="e44a0-256">Hola streaming aplicación creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e44a0-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="e44a0-257">Al ejecutar el comando de hello, debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e44a0-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="e44a0-258">Tome nota del identificador de lote de hello en la última línea de saludo del resultado de hello (en este ejemplo es '1').</span><span class="sxs-lookup"><span data-stu-id="e44a0-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="e44a0-259">tooverify que Hola aplicación se ejecuta correctamente, puede mirar la cuenta de almacenamiento de Azure asociada con el clúster de Hola y debería ver Hola **/conteo de eventos/EventCount10** carpeta creado.</span><span class="sxs-lookup"><span data-stu-id="e44a0-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="e44a0-260">Esta carpeta debe contener blobs que captura Hola número de eventos procesados en hello período de tiempo especificado para el parámetro hello **lote intervalo en segundos**.</span><span class="sxs-lookup"><span data-stu-id="e44a0-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="e44a0-261">aplicación de transmisión por secuencias de Hello Spark continuará toorun hasta que la elimine.</span><span class="sxs-lookup"><span data-stu-id="e44a0-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="e44a0-262">toodo por lo tanto, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e44a0-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="e44a0-263">Ejecutar aplicaciones de hello tooreceive eventos de hello en un Blob de almacenamiento de Azure como JSON</span><span class="sxs-lookup"><span data-stu-id="e44a0-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="e44a0-264">Abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute hello siguiente comando (reemplazar nombre de usuario/contraseña y clúster nombre):</span><span class="sxs-lookup"><span data-stu-id="e44a0-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="e44a0-265">Hola parámetros en el archivo hello **inputJSON.txt** se definen como sigue:</span><span class="sxs-lookup"><span data-stu-id="e44a0-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="e44a0-266">parámetros de Hello son toowhat similar que especificó para la salida de texto hello, en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="e44a0-267">Una vez más, no es necesario toocreate Hola carpetas de salida (EventCheckpoint, conteo de eventos/EventCount10) que se utilizan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="e44a0-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="e44a0-268">Hola streaming aplicación creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e44a0-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="e44a0-269">Después de ejecutar el comando de hello, puede mirar la cuenta de almacenamiento de Azure asociada con el clúster de Hola y debería ver Hola **/EventStore10** carpeta creado.</span><span class="sxs-lookup"><span data-stu-id="e44a0-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="e44a0-270">Abra cualquier archivo con el prefijo **parte -** y debería ver los eventos de hello procesados en un formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e44a0-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="e44a0-271">Ejecutar aplicaciones de hello tooreceive eventos de hello en una tabla de Hive</span><span class="sxs-lookup"><span data-stu-id="e44a0-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="e44a0-272">Hola toorun aplicación de streaming de Spark que la tabla eventos de secuencias en un subárbol necesita algunos componentes adicionales.</span><span class="sxs-lookup"><span data-stu-id="e44a0-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="e44a0-273">Dichos componentes son:</span><span class="sxs-lookup"><span data-stu-id="e44a0-273">These are:</span></span>

* <span data-ttu-id="e44a0-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="e44a0-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="e44a0-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="e44a0-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="e44a0-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="e44a0-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="e44a0-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="e44a0-277">hive-site.xml</span></span>

<span data-ttu-id="e44a0-278">Hola **.jar** archivos están disponibles en el clúster de HDInsight Spark en `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="e44a0-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="e44a0-279">Hola **hive-site.xml** está disponible en `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="e44a0-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="e44a0-280">Puede usar [WinScp](http://winscp.net/eng/download.php) toocopy a través de estos archivos del equipo local de hello clúster tooyour.</span><span class="sxs-lookup"><span data-stu-id="e44a0-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="e44a0-281">A continuación, puede usar toocopy herramientas estos archivos a través de la cuenta de almacenamiento de tooyour asociados a clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="e44a0-282">Para obtener más información sobre cómo se tooupload archivos toohello cuenta de almacenamiento, consulte [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="e44a0-283">Una vez que migraron Hola archivos tooyour cuenta de almacenamiento de Azure, abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute hello siguiente comando (reemplazar nombre de usuario/contraseña y clúster nombre):</span><span class="sxs-lookup"><span data-stu-id="e44a0-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="e44a0-284">Hola parámetros en el archivo hello **inputHive.txt** se definen como sigue:</span><span class="sxs-lookup"><span data-stu-id="e44a0-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="e44a0-285">parámetros de Hello son toowhat similar que especificó para la salida de texto hello, en los pasos anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="e44a0-286">Una vez más, no es necesario salida de hello toocreate carpetas (EventCheckpoint, conteo de eventos/EventCount10) o hello de la tabla de Hive (EventHiveTable10) que se utilizan como parámetros de salida.</span><span class="sxs-lookup"><span data-stu-id="e44a0-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="e44a0-287">Hola streaming aplicación creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e44a0-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="e44a0-288">Tenga en cuenta que hello **archivos JAR** y **archivos** opción incluye archivos .jar de rutas de acceso toohello y Hola hive-site.xml que copió toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e44a0-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="e44a0-289">tooverify que Hola tabla de hive se creó correctamente, puede SSH en clúster de Hola y ejecución de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="e44a0-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="e44a0-290">Para obtener instrucciones, consulte [Uso de Hive con Hadoop en HDInsight con SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="e44a0-291">Una vez que están conectados a través de SSH, puede ejecutar Hola después comando tooverify esa tabla de Hive hello, **EventHiveTable10**, se crea.</span><span class="sxs-lookup"><span data-stu-id="e44a0-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="e44a0-292">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="e44a0-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="e44a0-293">También puede ejecutar una consulta SELECT tooview contenido de Hola de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="e44a0-294">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e44a0-294">You should see an output like hello following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="e44a0-295">Ejecutar aplicaciones de hello tooreceive eventos de hello en una tabla de base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e44a0-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="e44a0-296">Antes de realizar este paso, asegúrese de que ha creado una Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e44a0-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="e44a0-297">Para instrucciones, consulte el artículo sobre la [creación de una base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="e44a0-298">toocomplete esta sección, necesita valores de nombre de base de datos, el nombre del servidor de base de datos y credenciales de administrador de base de datos de hello como parámetros.</span><span class="sxs-lookup"><span data-stu-id="e44a0-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="e44a0-299">No es necesario aunque la tabla de base de datos de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="e44a0-300">Hola aplicación de streaming de Spark crea para usted.</span><span class="sxs-lookup"><span data-stu-id="e44a0-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="e44a0-301">Abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e44a0-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="e44a0-302">Hola parámetros en el archivo hello **inputSQL.txt** se definen como sigue:</span><span class="sxs-lookup"><span data-stu-id="e44a0-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="e44a0-303">tooverify que Hola aplicación se ejecuta correctamente, puede conectarse toohello de base de datos de SQL Azure con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e44a0-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="e44a0-304">Para obtener instrucciones sobre cómo toodo que vea [conectar tooSQL base de datos con SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="e44a0-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="e44a0-305">Una vez que esté conectado toohello base de datos, puede navegar toohello **EventContent** tabla creada por hello transmisión por secuencias la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e44a0-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="e44a0-306">Puede ejecutar una consulta rápida tooget Hola de datos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e44a0-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="e44a0-307">Ejecute hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="e44a0-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="e44a0-308">Debería ver resultados similares toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="e44a0-308">You should see output similar toohello following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="e44a0-309"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e44a0-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e44a0-310">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e44a0-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* <span data-ttu-id="e44a0-311">[Design of Receiver-based Connection and Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317) (Diseño de conexiones basadas en receptor y Direct DStream)</span><span class="sxs-lookup"><span data-stu-id="e44a0-311">[Design of Receiver-based Connection and Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)</span></span>

### <a name="scenarios"></a><span data-ttu-id="e44a0-312">Escenarios</span><span class="sxs-lookup"><span data-stu-id="e44a0-312">Scenarios</span></span>
* [<span data-ttu-id="e44a0-313">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="e44a0-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e44a0-314">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e44a0-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e44a0-315">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="e44a0-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e44a0-316">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e44a0-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e44a0-317">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e44a0-317">Create and run applications</span></span>
* [<span data-ttu-id="e44a0-318">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="e44a0-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e44a0-319">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="e44a0-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e44a0-320">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="e44a0-320">Tools and extensions</span></span>
* [<span data-ttu-id="e44a0-321">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e44a0-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e44a0-322">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="e44a0-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e44a0-323">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e44a0-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e44a0-324">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e44a0-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e44a0-325">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="e44a0-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e44a0-326">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e44a0-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e44a0-327">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="e44a0-327">Manage resources</span></span>
* [<span data-ttu-id="e44a0-328">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e44a0-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e44a0-329">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="e44a0-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
