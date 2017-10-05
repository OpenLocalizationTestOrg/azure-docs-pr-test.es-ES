---
title: Uso de streaming de Apache Spark con Event Hubs en Azure HDInsight | Microsoft Docs
description: "Compile un ejemplo de streaming de Apache Spark sobre cómo enviar una transmisión de datos a Azure Event Hubs y, luego, recibir esos eventos en un clúster de HDInsight Spark mediante una aplicación de Scala."
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
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="8dc9d-104">Streaming de Apache Spark: procesamiento de datos desde Azure Event Hubs con clústeres de Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8dc9d-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="8dc9d-105">En este artículo, va a crear un ejemplo de streaming de Apache Spark realizando los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="8dc9d-106">Usará una aplicación independiente para ingerir mensajes en un centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="8dc9d-107">Puede usar dos enfoques diferentes para recuperar los mensajes del centro de eventos en tiempo real con una aplicación que se ejecuta en el clúster de Spark en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="8dc9d-108">Creará canalizaciones analíticas de streaming para conservar los datos en diferentes sistemas de almacenamiento u obtener información de datos sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dc9d-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8dc9d-109">Prerequisites</span></span>

* <span data-ttu-id="8dc9d-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-110">An Azure subscription.</span></span> <span data-ttu-id="8dc9d-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="8dc9d-112">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8dc9d-113">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="8dc9d-114">Conceptos de streaming de Spark</span><span class="sxs-lookup"><span data-stu-id="8dc9d-114">Spark Streaming concepts</span></span>

<span data-ttu-id="8dc9d-115">Para obtener una explicación detallada del streaming de Spark consulte la [información general sobre el streaming de Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="8dc9d-116">HDInsight ofrece las mismas funciones de streaming para un clúster de Spark en Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="8dc9d-117">¿Cómo funciona la solución?</span><span class="sxs-lookup"><span data-stu-id="8dc9d-117">What does this solution do?</span></span>

<span data-ttu-id="8dc9d-118">En este artículo, para crear un ejemplo de streaming, siga los pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="8dc9d-119">Cree un Centro de eventos de Azure, que será el que reciba una transmisión de eventos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="8dc9d-120">Ejecute una aplicación local independiente que genere eventos y los inserte en el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="8dc9d-121">La aplicación de ejemplo que lo hace se publica en [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="8dc9d-122">Ejecute una aplicación de streaming de forma remota en un clúster de Spark que lea los eventos de streaming desde el centro de eventos de Azure y lleve a cabo varios análisis y procesamientos de datos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="8dc9d-123">Crear un centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc9d-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="8dc9d-124">Inicie sesión en [Azure Portal](https://ms.portal.azure.com) y haga clic en **Nuevo** en la parte superior izquierda de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="8dc9d-125">Haga clic en **Internet de las cosas** y en **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="8dc9d-126">![Creación de un centro de eventos para un ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="8dc9d-127">En la hoja **Crear espacio de nombres** , especifique el nombre del espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="8dc9d-128">Elija el plan de tarifa (Básico o Estándar).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="8dc9d-129">Elija también una suscripción de Azure, un grupo de recursos y la ubicación en la que se va a crear el recurso.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="8dc9d-130">Haga clic en **Crear** para crear el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="8dc9d-131">![Aportación de un nombre de centro de evento para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="8dc9d-132">Para reducir la latencia y los costos, debe seleccionar la misma **ubicación** que la del clúster Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="8dc9d-133">En la lista de espacios de nombres de los Centros de eventos, haga clic en el espacio de nombres recién creado.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="8dc9d-134">En la hoja de espacio de nombres, haga clic en **Event Hubs** y luego en **+ Centro de eventos** para crear un nuevo centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="8dc9d-135">![Creación de un centro de eventos para un ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="8dc9d-136">Escriba un nombre para el centro de eventos, establezca el recuento de partición en 10 y la retención de mensajes en 1.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="8dc9d-137">En esta solución no vamos a archivar los mensajes, así que puede dejar el resto con los valores predeterminados y hacer clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="8dc9d-138">![Aportación de detalles del centro de evento para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="8dc9d-139">El centro de eventos recién creado aparece en la hoja Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="8dc9d-140">![Vista de Event Hub para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="8dc9d-141">En la hoja del espacio de nombres (no en la hoja del Centro de eventos específico), haga clic en **Directivas de acceso compartido** y, luego, en **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="8dc9d-142">![Establecimiento de directivas de Event Hub para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="8dc9d-143">Haga clic en el botón Copiar para copiar la clave principal **RootManageSharedAccessKey** y la cadena de conexión en el portapapeles.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="8dc9d-144">Guárdelas, ya que las necesitará más tarde en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="8dc9d-145">![Vista de las claves de directiva de Event Hub para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="8dc9d-146">Envío de mensajes a Azure Event Hub mediante una aplicación de Scala</span><span class="sxs-lookup"><span data-stu-id="8dc9d-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="8dc9d-147">En esta sección se usa una aplicación de Scala local independiente que genera una secuencia de eventos y la envía al centro de Azure Event Hub que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="8dc9d-148">Esta aplicación está disponible en GitHub en [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="8dc9d-149">En los siguientes pasos se asume que ya ha bifurcado este repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="8dc9d-150">Asegúrese de tener instalados los siguientes elementos en el equipo donde se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="8dc9d-151">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-151">Oracle Java Development kit.</span></span> <span data-ttu-id="8dc9d-152">Puede instalarlo desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="8dc9d-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-153">Apache Maven.</span></span> <span data-ttu-id="8dc9d-154">Puede descargarla [aquí](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="8dc9d-155">Las instrucciones para instalar Maven están disponibles [aquí](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="8dc9d-156">Abra un símbolo del sistema y desplácese a la ubicación en la que clonó el repositorio de GitHub para la aplicación de ejemplo de Scala y ejecute el siguiente comando para compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="8dc9d-157">El archivo JAR de salida de la aplicación, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, se crea en el directorio **/target**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="8dc9d-158">Usará este archivo JAR más adelante en este artículo para probar la solución completa.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="8dc9d-159">Creación de una aplicación para recibir mensajes de Event Hub en un clúster de Spark</span><span class="sxs-lookup"><span data-stu-id="8dc9d-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="8dc9d-160">Tenemos dos enfoques para conectar Spark Streaming y los centros de eventos de Azure, una conexión basada en un receptor y una conexión basada en Direct DStream.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="8dc9d-161">La conexión basada en Direct DStream se introdujo en enero de 2017 en la versión 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="8dc9d-162">Supuestamente reemplaza la conexión original basada en un receptor, ya que es más eficiente y eficaz de cara a los recursos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="8dc9d-163">Encontrará más información en [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="8dc9d-164">Direct DStream solo admite Spark 2.0+.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="8dc9d-165">Compilación de aplicaciones con la dependencia al conector spark-eventhubs</span><span class="sxs-lookup"><span data-stu-id="8dc9d-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="8dc9d-166">También publicaremos la versión de almacenamiento provisional de Spark-EventHubs en GitHub.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="8dc9d-167">Para usar la versión de almacenamiento provisional de Spark-EventHubs, el primer paso consiste en establecer GitHub como repositorio de origen; para ello, debe agregar la siguiente entrada al archivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

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

<span data-ttu-id="8dc9d-168">Luego podrá agregar la siguiente dependencia al proyecto para tomar la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="8dc9d-169">Dependencia de Maven</span><span class="sxs-lookup"><span data-stu-id="8dc9d-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="8dc9d-170">Dependencia de SBT</span><span class="sxs-lookup"><span data-stu-id="8dc9d-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="8dc9d-171">Conexión de Direct DStream</span><span class="sxs-lookup"><span data-stu-id="8dc9d-171">Direct DStream Connection</span></span>

<span data-ttu-id="8dc9d-172">En [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) se puede descargar un archivo JAR pregenerado que contiene ejemplos en los que se usa Direct DStream.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="8dc9d-173">El archivo jar contiene tres ejemplos cuyo código fuente está disponible en [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="8dc9d-174">Si tomamos [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="8dc9d-175">En el ejemplo anterior, `eventhubParameters` son los parámetros específicos de una sola instancia de EventHubs y tiene que pasarlos a la API `createDirectStreams`, que construye una asignación de objeto de Direct DStream a un espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="8dc9d-176">Mediante el objeto de Direct DStream puede llamar a cualquier API de DStream proporcionada por el marco de la API de Spark Streaming.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="8dc9d-177">En este ejemplo se calcula la frecuencia de cada palabra dentro de los 3 últimos microintervalos por lotes.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="8dc9d-178">Conexión basada en un receptor</span><span class="sxs-lookup"><span data-stu-id="8dc9d-178">Receiver-based Connection</span></span>

<span data-ttu-id="8dc9d-179">En [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples) está disponible una aplicación de streaming de Spark de ejemplo escrita en Scala que recibe eventos y los enruta a diferentes destinos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="8dc9d-180">Siga los pasos que se indican a continuación para actualizar la aplicación para su configuración de Event Hub y crear el archivo JAR de salida.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="8dc9d-181">Inicie IntelliJ IDEA y en la pantalla de inicio, seleccione **Check out from Version Control** (Extraer del repositorio de control de versiones) y haga clic en **Git**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="8dc9d-182">![Ejemplo de streaming de Apache Spark: obtener orígenes de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="8dc9d-183">En el cuadro de diálogo **Clone Repository** (Clonar repositorio), indique la dirección URL del repositorio de Git de origen y el directorio de destino de la clonación, y haga clic en **Clone** (Clonar).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="8dc9d-184">![Ejemplo de streaming de Apache Spark: clonar de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="8dc9d-185">Siga las indicaciones hasta que el proyecto se haya clonado completamente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="8dc9d-186">Presione **Alt + 1** para abrir la **Project View** (Vista de proyecto).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="8dc9d-187">Debería ser similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="8dc9d-188">![Ejemplo de streaming de Apache Spark: vista de proyecto](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="8dc9d-189">Asegúrese de que el código de aplicación se compila con Java8.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="8dc9d-190">Para asegurarse de esto, haga clic en **File** (Archivo), **Project Structure** (Estructura del proyecto) y la **Project** (Proyecto), asegúrese de que el nivel de lenguaje del proyecto se establece en **8 - Expresiones lambda, anotaciones de tipo, etc**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="8dc9d-191">![Ejemplo de streaming de Apache Spark: establecer compilador](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="8dc9d-192">Abra **pom.xml** y asegúrese de que la versión de Spark es correcta.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="8dc9d-193">En el `<properties>` nodo, busque el siguiente fragmento y compruebe la versión de Spark.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="8dc9d-194">La aplicación requiere un archivo jar de dependencia llamado **jar del controlador JDBC**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="8dc9d-195">Se requiere para escribir los mensajes recibidos desde el Centro de eventos en una Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="8dc9d-196">Puede descargar este archivo jar (versión 4.1, o las versiones posteriores) desde [aquí](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="8dc9d-197">Agregue referencia a este archivo jar en la biblioteca de proyectos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="8dc9d-198">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="8dc9d-199">En la ventana de IntelliJ IDEA en la que la aplicación está abierta, haga clic en **File** (Archivo), **Project Structure** (Estructura de proyecto) y en **Libraries** (Bibliotecas).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="8dc9d-200">Haga clic en el icono de agregar (![icono Agregar](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), haga clic en **Java**, y luego navegue hasta la ubicación en que descargó el archivo jar del controlador de JDBC.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="8dc9d-201">Siga las indicaciones para agregar el archivo JAR a la biblioteca de proyectos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="8dc9d-202">![agregar dependencias que faltan](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Agregar archivos jar de dependencias que faltan")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="8dc9d-203">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-203">Click **Apply**.</span></span>

7. <span data-ttu-id="8dc9d-204">Cree el archivo JAR de salida.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-204">Create the output jar file.</span></span> <span data-ttu-id="8dc9d-205">Lleve a cabo los siguiente pasos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="8dc9d-206">En el cuadro de diálogo **Project Structure** (Estructura de proyecto), haga clic en **Artifacts** (Artefactos) y en el signo más.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="8dc9d-207">En el cuadro de diálogo emergente, haga clic en **JAR** y en **From modules with dependencies** (Desde módulos con dependencias).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="8dc9d-208">![Ejemplo de streaming de Apache Spark: crear archivo JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="8dc9d-209">En el cuadro de diálogo **Create JAR** from Modules (Crear archivo JAR desde módulos), haga clic en el botón de puntos suspensivos (![puntos suspensivos](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) en la **clase principal**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="8dc9d-210">En el cuadro de diálogo **Select Main Class** (Seleccionar clase principal), seleccione cualquiera de las clases disponibles y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="8dc9d-211">![Ejemplo de streaming de Apache Spark: seleccionar clase para el archivo jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="8dc9d-212">En el cuadro de diálogo **Create JAR from Modules** (Crear archivo JAR desde módulos), asegúrese de que está seleccionada la opción para **extraer al archivo JAR de destino** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="8dc9d-213">Así se crea un archivo JAR único con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="8dc9d-214">![Ejemplo de streaming de Apache Spark: crear archivo jar desde módulos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="8dc9d-215">La pestaña **Output Layout** (Diseño de salida) enumera todos los archivos JAR que forman parte del proyecto Maven.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="8dc9d-216">Puede seleccionar y eliminar aquellos de los que la aplicación de Scala no tenga ninguna dependencia directa.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="8dc9d-217">En el caso de la aplicación que creamos aquí, puede quitar todos los archivos menos el último (**spark-streaming-data-persistence-examples compile output**).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="8dc9d-218">Seleccione los archivos JAR que va a eliminar y haga clic en el icono **Eliminar** (![icono eliminar](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="8dc9d-219">![Ejemplo de streaming de Apache Spark: eliminar archivos jar extraídos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="8dc9d-220">Asegúrese de que la casilla **Build on make** (Compilar al crear) está activada, lo que garantiza que el archivo jar se crea cada vez que el proyecto se compila o actualiza.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="8dc9d-221">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="8dc9d-222">En la ficha **Output Layout** (Diseño de salida), en la parte inferior del cuadro **Available Elements** (Elementos disponibles), tendrá los dos archivos jar de SQL JDBC que agregó anteriormente a la biblioteca de proyectos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="8dc9d-223">Debe agregarlos a la pestaña **Output Layout** (Diseño de salida). Haga clic con el botón derecho en el archivo jar y, después, haga clic en **Extract Into Output Root**(Extraer en raíz de salida).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="8dc9d-224">![Ejemplo de streaming de Apache Spark: extraer archivo jar de dependencia](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="8dc9d-225">La pestaña **Output Layout** (Diseño de salida) debe ser como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="8dc9d-226">![Ejemplo de streaming de Apache Spark: pestaña de salida final](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="8dc9d-227">En el cuadro de diálogo **Project Structure** (Estructura de proyecto), haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="8dc9d-228">En la barra de menús, haga clic en **Build** (Compilar) y en **Make Project** (Crear proyecto).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="8dc9d-229">También puede hacer clic en **Build Artifacts** (Compilar artefactos) para crear el archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="8dc9d-230">El archivo jar de salida se crea en **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="8dc9d-231">![Ejemplo de streaming de Apache Spark: salida de archivo JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span><span class="sxs-lookup"><span data-stu-id="8dc9d-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="8dc9d-232">Ejecución remota de aplicaciones en un clúster Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="8dc9d-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="8dc9d-233">En este artículo usaremos Livy para ejecutar la aplicación de streaming de Apache Spark de forma remota en un clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="8dc9d-234">Para obtener una explicación detallada sobre cómo usar Livy con un clúster de HDInsight Spark, consulte [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight (Linux)](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="8dc9d-235">Antes de empezar a ejecutar la aplicación de streaming de Spark, tiene que hacer un par de cosas:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="8dc9d-236">Inicie la aplicación autónoma local para generar eventos y enviarlos al Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="8dc9d-237">Utilice el siguiente comando para hacerlo:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="8dc9d-238">Copie el archivo jar de streaming (**spark-streaming-data-persistence-examples.jar**) en la instancia de Azure Blob Storage asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="8dc9d-239">Esto permite que Livy pueda acceder al archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="8dc9d-240">Puede usar [**AzCopy**](../storage/common/storage-use-azcopy.md), una utilidad de línea de comandos, para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="8dc9d-241">Hay muchos otros clientes que se pueden utilizar para cargar datos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="8dc9d-242">Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="8dc9d-243">Instale CURL en el equipo desde el que se ejecutan estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="8dc9d-244">CURL se usa para invocar los puntos de conexión de Livy para ejecutar los trabajos de forma remota.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="8dc9d-245">Ejecución de la aplicación de streaming de Spark para recibir los eventos en una instancia de Azure Storage Blob como texto</span><span class="sxs-lookup"><span data-stu-id="8dc9d-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="8dc9d-246">Abra un símbolo del sistema, navegue al directorio en que instaló CURL y ejecute el siguiente comando (reemplace el nombre de usuario y la contraseña, y el nombre del clúster):</span><span class="sxs-lookup"><span data-stu-id="8dc9d-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="8dc9d-247">A continuación se definen los parámetros del archivo **inputBlob.txt** :</span><span class="sxs-lookup"><span data-stu-id="8dc9d-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="8dc9d-248">Estos son los parámetros del archivo de entrada:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="8dc9d-249">**file** es la ruta de acceso al archivo JAR de la aplicación en la cuenta de Almacenamiento de Azure asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="8dc9d-250">**className** es el nombre de la clase en el archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="8dc9d-251">**args** es la lista de argumentos requeridos por la clase</span><span class="sxs-lookup"><span data-stu-id="8dc9d-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="8dc9d-252">**numExecutors** es el número de núcleos que usa Spark para ejecutar la aplicación de streaming.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="8dc9d-253">Siempre debe ser al menos dos veces el número de particiones del Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="8dc9d-254">**executorMemory**, **executorCores** y **driverMemory** son los parámetros que se usan para asignar los recursos necesarios a la aplicación de streaming.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="8dc9d-255">No es preciso crear las carpetas de salida (EventCheckpoint, EventCount/EventCount10) que se usan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="8dc9d-256">La aplicación de streaming las crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="8dc9d-257">Al ejecutar el comando, debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="8dc9d-258">Anote el identificador de lote de la última línea de la salida (en este ejemplo es '1').</span><span class="sxs-lookup"><span data-stu-id="8dc9d-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="8dc9d-259">Para comprobar que la aplicación se ejecuta correctamente, puede examinar la cuenta de Almacenamiento de Azure asociada con el clúster, donde debería ver que se ha creado la carpeta **/EventCount/EventCount10** .</span><span class="sxs-lookup"><span data-stu-id="8dc9d-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="8dc9d-260">Dicha carpeta debe contener blobs que capturen el número de eventos procesados en el período especificado para el parámetro **batch-interval-in-seconds**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="8dc9d-261">La aplicación de streaming de Spark seguirá ejecutándose hasta que la termine.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="8dc9d-262">Para ello, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="8dc9d-263">Ejecución de las aplicaciones para recibir los eventos en un blob de Almacenamiento de Azure como JSON</span><span class="sxs-lookup"><span data-stu-id="8dc9d-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="8dc9d-264">Abra un símbolo del sistema, navegue al directorio en que instaló CURL y ejecute el siguiente comando (reemplace el nombre de usuario y la contraseña, y el nombre del clúster):</span><span class="sxs-lookup"><span data-stu-id="8dc9d-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="8dc9d-265">A continuación se definen los parámetros del archivo **inputJSON.txt** :</span><span class="sxs-lookup"><span data-stu-id="8dc9d-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="8dc9d-266">Los parámetros son similares a los que especificó para la salida de texto en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="8dc9d-267">Una vez más, no es preciso crear las carpetas de salida (EventCheckpoint, EventCount/EventCount10) que se usan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="8dc9d-268">La aplicación de streaming las crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="8dc9d-269">Tras ejecutar el comando puede examinar la cuenta de Almacenamiento de Azure asociada con el clúster, donde debería ver que se ha creado la carpeta **/EventStore10** .</span><span class="sxs-lookup"><span data-stu-id="8dc9d-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="8dc9d-270">Si abre cualquier archivo con el prefijo **part-** , debería ver los eventos procesados en un formato JSON.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="8dc9d-271">Ejecución de las aplicaciones para recibir los eventos en una tabla de Hive</span><span class="sxs-lookup"><span data-stu-id="8dc9d-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="8dc9d-272">Para ejecutar la aplicación de streaming de Spark que transmite los eventos a una tabla de Hive se necesitan varios componentes adicionales.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="8dc9d-273">Dichos componentes son:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-273">These are:</span></span>

* <span data-ttu-id="8dc9d-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="8dc9d-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="8dc9d-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="8dc9d-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="8dc9d-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="8dc9d-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="8dc9d-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="8dc9d-277">hive-site.xml</span></span>

<span data-ttu-id="8dc9d-278">Los archivos **.jar** están disponibles en el clúster de HDInsight Spark en `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="8dc9d-279">El archivo **hive-site.xml** está disponible en `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="8dc9d-280">Puede usar [WinScp](http://winscp.net/eng/download.php) para copiar estos archivos desde el clúster al equipo local.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="8dc9d-281">A continuación, puede usan herramientas para copiar estos archivos en su cuenta de almacenamiento asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="8dc9d-282">Para más información acerca de cómo cargar archivos en la cuenta de almacenamiento, consulte [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="8dc9d-283">Una vez que haya copiado los archivos a la cuenta de Almacenamiento de Azure, abra un símbolo del sistema, navegue al directorio en que instaló CURL y ejecute el siguiente comando (reemplace el nombre de usuario y la contraseña, y el nombre del clúster):</span><span class="sxs-lookup"><span data-stu-id="8dc9d-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="8dc9d-284">A continuación se definen los parámetros del archivo **inputHive.txt** :</span><span class="sxs-lookup"><span data-stu-id="8dc9d-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="8dc9d-285">Los parámetros son similares a los que especificó para la salida de texto en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="8dc9d-286">Una vez más, no es preciso crear las carpetas de salida (EventCheckpoint, EventCount/EventCount10) ni la tabla de Hive de salida (EventHiveTable10) que se usan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="8dc9d-287">La aplicación de streaming las crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-287">The streaming application creates them for you.</span></span> <span data-ttu-id="8dc9d-288">Tenga en cuenta que la opción **jars** y **files** incluye rutas de acceso a los archivos .jar y hive-site.xml que copió a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="8dc9d-289">Para comprobar que la tabla de Hive se ha creado correctamente, puede usar SSH en el clúster y ejecutar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="8dc9d-290">Para obtener instrucciones, consulte [Uso de Hive con Hadoop en HDInsight con SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="8dc9d-291">Una vez que se haya conectado mediante SSH, puede ejecutar el comando siguiente para comprobar que se ha creado la tabla de Hive, **EventHiveTable10**.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="8dc9d-292">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="8dc9d-293">También puede ejecutar una consulta SELECT para ver el contenido de la tabla.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="8dc9d-294">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-294">You should see an output like the following:</span></span>

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


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="8dc9d-295">Ejecución de las aplicaciones para recibir los eventos en una tabla de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc9d-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="8dc9d-296">Antes de realizar este paso, asegúrese de que ha creado una Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="8dc9d-297">Para instrucciones, consulte el artículo sobre la [creación de una base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="8dc9d-298">Para completar esta acción, necesitará valores para el nombre de la base de datos, el nombre del servidor de la base de datos y las credenciales del administrador de la base de datos como parámetros.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="8dc9d-299">Sin embargo, no es preciso crear la tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-299">You do not need to create the database table though.</span></span> <span data-ttu-id="8dc9d-300">La aplicación de streaming de Spark la crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="8dc9d-301">Abra un símbolo del sistema, navegue al directorio en que instaló CURL y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="8dc9d-302">A continuación se definen los parámetros del archivo **inputSQL.txt** :</span><span class="sxs-lookup"><span data-stu-id="8dc9d-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="8dc9d-303">Para comprobar que la aplicación se ejecuta correctamente, puede conectarse a la Base de datos SQL de Azure mediante SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="8dc9d-304">Para obtener instrucciones sobre cómo hacerlo, consulte [Conexión a la Base de datos SQL con SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="8dc9d-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="8dc9d-305">Una vez que se haya conectado a la base de datos, puede navegar a la tabla **EventContent** que creó la aplicación de streaming.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="8dc9d-306">Para obtener los datos de la tabla, puede ejecutar una consulta rápida.</span><span class="sxs-lookup"><span data-stu-id="8dc9d-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="8dc9d-307">Ejecute la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="8dc9d-308">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="8dc9d-308">You should see output similar to the following:</span></span>

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


## <span data-ttu-id="8dc9d-309"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8dc9d-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8dc9d-310">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc9d-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* <span data-ttu-id="8dc9d-311">[Design of Receiver-based Connection and Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317) (Diseño de conexiones basadas en receptor y Direct DStream)</span><span class="sxs-lookup"><span data-stu-id="8dc9d-311">[Design of Receiver-based Connection and Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)</span></span>

### <a name="scenarios"></a><span data-ttu-id="8dc9d-312">Escenarios</span><span class="sxs-lookup"><span data-stu-id="8dc9d-312">Scenarios</span></span>
* [<span data-ttu-id="8dc9d-313">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="8dc9d-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8dc9d-314">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc9d-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8dc9d-315">Spark con Aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="8dc9d-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8dc9d-316">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8dc9d-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8dc9d-317">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8dc9d-317">Create and run applications</span></span>
* [<span data-ttu-id="8dc9d-318">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="8dc9d-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8dc9d-319">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="8dc9d-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8dc9d-320">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="8dc9d-320">Tools and extensions</span></span>
* [<span data-ttu-id="8dc9d-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones Scala Spark)</span><span class="sxs-lookup"><span data-stu-id="8dc9d-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8dc9d-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="8dc9d-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8dc9d-323">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8dc9d-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8dc9d-324">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="8dc9d-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8dc9d-325">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="8dc9d-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8dc9d-326">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc9d-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8dc9d-327">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="8dc9d-327">Manage resources</span></span>
* [<span data-ttu-id="8dc9d-328">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8dc9d-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8dc9d-329">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8dc9d-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
