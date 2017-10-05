---
title: Procesamiento de eventos desde cEvent Hubs con Storm en HDInsight con Java | Microsoft Docs
description: "Obtenga información sobre cómo procesar los datos de los Centros de eventos con una topología Java de Storm creada con Maven."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="def54-103">Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="def54-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="def54-104">Obtenga información sobre cómo usar Azure Event Hubs con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def54-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="def54-105">Este ejemplo utiliza componentes basados en Java para leer y escribir datos en Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="def54-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="def54-106">Los Centros de eventos de Azure le permiten procesar grandes volúmenes de datos provenientes de sitios web, aplicaciones y dispositivos.</span><span class="sxs-lookup"><span data-stu-id="def54-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="def54-107">El spout de centro de eventos permite que Apache Storm en HDInsight analice fácilmente estos datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="def54-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="def54-108">También es posible escribir datos en Centros de eventos desde Storm usando el bolt de Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="def54-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="def54-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="def54-109">Prerequisites</span></span>

* <span data-ttu-id="def54-110">Una instancia de Apache Storm en un clúster de HDInsight, versión 3.6.</span><span class="sxs-lookup"><span data-stu-id="def54-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="def54-111">Para más información, vea [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md) (Introducción a Storm en clúster de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="def54-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="def54-112">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="def54-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="def54-113">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="def54-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="def54-114">Un [Centro de eventos de Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="def54-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="def54-115">[Oracle Java Developer Kit (JDK) versión 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, como [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="def54-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="def54-116">[Maven](https://maven.apache.org/download.cgi): Maven es un sistema de compilación de proyectos para proyectos de Java.</span><span class="sxs-lookup"><span data-stu-id="def54-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="def54-117">Un editor de texto o un entorno de desarrollo integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="def54-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="def54-118">El editor o IDE puede tener una funcionalidad específica para trabajar con Maven que no se trata en este documento.</span><span class="sxs-lookup"><span data-stu-id="def54-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="def54-119">Para obtener información sobre las capacidades de su entorno de edición, consulte la documentación del producto que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="def54-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="def54-120">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="def54-120">An SSH client.</span></span> <span data-ttu-id="def54-121">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="def54-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="def54-122">Los comandos `ssh` y `scp`,</span><span class="sxs-lookup"><span data-stu-id="def54-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="def54-123">que sirven para copiar archivos en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def54-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="def54-124">En Windows, se obtienen a través de Bash en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="def54-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="def54-125">Descripción del ejemplo</span><span class="sxs-lookup"><span data-stu-id="def54-125">Understanding the example</span></span>

<span data-ttu-id="def54-126">El ejemplo [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) contiene dos topologías:</span><span class="sxs-lookup"><span data-stu-id="def54-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="def54-127">La topología `resources/writer.yaml` escribe datos aleatorios en un centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="def54-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="def54-128">Los datos los genera el componente `DeviceSpout` y son un identificador de dispositivo y un valor de dispositivo aleatorios.</span><span class="sxs-lookup"><span data-stu-id="def54-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="def54-129">Por lo tanto simula un hardware que emite un identificador de cadena y un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="def54-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="def54-130">La topología `resources/reader.yaml` lee los datos del centro de eventos (es decir, los datos que escribe EventHubWriter,) analiza los datos JSON y registra los datos `deviceId` y `deviceValue`.</span><span class="sxs-lookup"><span data-stu-id="def54-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="def54-131">Con el formato de los datos como un documento JSON antes de escribir en el concentrador de eventos y cuando los lee el lector se analiza de JSON a de tuplas.</span><span class="sxs-lookup"><span data-stu-id="def54-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="def54-132">El formato de la dirección JSON es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="def54-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="def54-133">Configuración de proyecto</span><span class="sxs-lookup"><span data-stu-id="def54-133">Project configuration</span></span>

<span data-ttu-id="def54-134">El archivo `POM.xml` contiene información de configuración para este proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="def54-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="def54-135">Las partes interesantes son:</span><span class="sxs-lookup"><span data-stu-id="def54-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="def54-136">Componentes del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="def54-136">Event Hub components</span></span>

<span data-ttu-id="def54-137">El componente que lee y escribe en Azure Event Hubs se encuentra en el [repositorio de HDInsight](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="def54-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="def54-138">En las siguientes secciones del archivo `POM.xml` se cargan los componentes de este repositorio</span><span class="sxs-lookup"><span data-stu-id="def54-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="def54-139">La dependencia de Spout de EventHubs Storm</span><span class="sxs-lookup"><span data-stu-id="def54-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="def54-140">Este xml define una dependencia para el paquete eventhubs, que contiene tanto un spout para la lectura de Event Hubs como un bolt para escribir ahí.</span><span class="sxs-lookup"><span data-stu-id="def54-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="def54-141">Este xml configura el proyecto para generar la salida para Java 8, versión mínima que utiliza HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="def54-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="def54-142">El complemento maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="def54-142">The maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

<span data-ttu-id="def54-143">Este xml configura la solución para empaquetar la salida en un archivo uber jar.</span><span class="sxs-lookup"><span data-stu-id="def54-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="def54-144">El archivo jar contiene el código del proyecto y necesita dependencias.</span><span class="sxs-lookup"><span data-stu-id="def54-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="def54-145">También se usa para:</span><span class="sxs-lookup"><span data-stu-id="def54-145">It is also used to:</span></span>

* <span data-ttu-id="def54-146">Cambiar el nombre de archivos de licencia para las dependencias.</span><span class="sxs-lookup"><span data-stu-id="def54-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="def54-147">Excluir la seguridad y las firmas.</span><span class="sxs-lookup"><span data-stu-id="def54-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="def54-148">Asegúrese de combinar varias implementaciones de la misma interfaz en una sola entrada.</span><span class="sxs-lookup"><span data-stu-id="def54-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="def54-149">Estos valores de configuración evitan errores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="def54-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="def54-150">Definiciones de topología</span><span class="sxs-lookup"><span data-stu-id="def54-150">Topology definitions</span></span>

<span data-ttu-id="def54-151">En este ejemplo se utiliza el marco [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="def54-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="def54-152">El marco usa YAML para definir las topologías.</span><span class="sxs-lookup"><span data-stu-id="def54-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="def54-153">La principal ventaja es que no se codifica la topología de forma rígida en el código de Java.</span><span class="sxs-lookup"><span data-stu-id="def54-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="def54-154">Dado que la definición es YAML, se puede cambiar antes de enviar la topología, sin tener que volver a compilar todo el contenido.</span><span class="sxs-lookup"><span data-stu-id="def54-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="def54-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="def54-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="def54-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="def54-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through the components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="def54-157">Indicación de la topología al centro de eventos</span><span class="sxs-lookup"><span data-stu-id="def54-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="def54-158">En tiempo de ejecución, el archivo `dev.properties` sirve para pasar la configuración del centro de eventos a la topología.</span><span class="sxs-lookup"><span data-stu-id="def54-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="def54-159">El ejemplo siguiente es el contenido predeterminado del archivo:</span><span class="sxs-lookup"><span data-stu-id="def54-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="def54-160">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="def54-160">Configure environment variables</span></span>

<span data-ttu-id="def54-161">Pueden establecer las siguientes variables de entorno al instalar Java y el JDK en la estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="def54-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="def54-162">Sin embargo, debe comprobar que existen y que contienen los valores correctos para su sistema.</span><span class="sxs-lookup"><span data-stu-id="def54-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="def54-163">**JAVA_HOME**: debe apuntar al directorio donde está instalado Java Runtime Environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="def54-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="def54-164">Por ejemplo, en una distribución de Unix o Linux, debe tener un valor similar a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="def54-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="def54-165">En Windows, tendría un valor similar a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="def54-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="def54-166">**PATH** : debe contener las rutas de acceso siguientes:</span><span class="sxs-lookup"><span data-stu-id="def54-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="def54-167">**JAVA_HOME** (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="def54-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="def54-168">**JAVA_HOME\bin** (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="def54-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="def54-169">El directorio donde está instalado Maven</span><span class="sxs-lookup"><span data-stu-id="def54-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="def54-170">Configuración del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="def54-170">Configure Event Hub</span></span>

<span data-ttu-id="def54-171">Centros de eventos es el origen de datos para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="def54-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="def54-172">Use los pasos siguientes para crear un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="def54-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="def54-173">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **NUEVO** > **Service Bus** > **Centro de eventos** > **Creación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="def54-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="def54-174">En la pantalla **Agregar un concentrador de eventos nuevo**, escriba un **Nombre del Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="def54-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="def54-175">Seleccione la **Región** en la que crear el centro y, después, cree un espacio de nombres o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="def54-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="def54-176">Por último, haga clic en la **flecha** para continuar.</span><span class="sxs-lookup"><span data-stu-id="def54-176">Finally, click the **Arrow** to continue.</span></span>

    ![página 1 del asistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="def54-178">Seleccione la misma **Ubicación** de su servidor Storm en HDInsight para disminuir la latencia y los costos.</span><span class="sxs-lookup"><span data-stu-id="def54-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="def54-179">En la pantalla **Configurar el concentrador de eventos**, escriba los valores **Recuento de particiones** y **Retención de mensajes**.</span><span class="sxs-lookup"><span data-stu-id="def54-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="def54-180">En este ejemplo, utilice un recuento de particiones de 10 y una retención de mensajes de 1.</span><span class="sxs-lookup"><span data-stu-id="def54-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="def54-181">Anote el recuento de particiones, porque necesita este valor más adelante.</span><span class="sxs-lookup"><span data-stu-id="def54-181">Note the partition count because you need this value later.</span></span>

    ![página 2 del asistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="def54-183">Una vez se ha creado el concentrador de eventos, seleccione el espacio de nombres, seleccione **Concentradores de eventos**y, después, seleccione el concentrador de eventos que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="def54-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="def54-184">Seleccione **Configurar** y cree dos directivas de acceso con la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="def54-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="def54-185">Nombre</span><span class="sxs-lookup"><span data-stu-id="def54-185">Name</span></span></th><th><span data-ttu-id="def54-186">Permisos</span><span class="sxs-lookup"><span data-stu-id="def54-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="def54-187">Escritor</span><span class="sxs-lookup"><span data-stu-id="def54-187">Writer</span></span></td><td><span data-ttu-id="def54-188">Los métodos Send</span><span class="sxs-lookup"><span data-stu-id="def54-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="def54-189">Lector</span><span class="sxs-lookup"><span data-stu-id="def54-189">Reader</span></span></td><td><span data-ttu-id="def54-190">Escuchar</span><span class="sxs-lookup"><span data-stu-id="def54-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="def54-191">Después de crear los permisos, seleccione el icono **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="def54-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="def54-192">Estas directivas de acceso compartido se usan para leer y escribir en el Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="def54-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![directivas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="def54-194">Después de guardar las directivas, use el **generador de claves de acceso compartido** que se encuentra en la parte inferior de la página para recuperar la clave para las directivas de **escritor** y **lector**.</span><span class="sxs-lookup"><span data-stu-id="def54-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="def54-195">Guarde estas claves.</span><span class="sxs-lookup"><span data-stu-id="def54-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="def54-196">Descarga y compilación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="def54-196">Download and build the project</span></span>

1. <span data-ttu-id="def54-197">Descargue el proyecto de GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="def54-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="def54-198">Puede descargar el paquete como un archivo zip o usar [git](https://git-scm.com/) para clonar el proyecto de forma local.</span><span class="sxs-lookup"><span data-stu-id="def54-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="def54-199">Modifique el archivo `dev.properties` con la configuración del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="def54-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="def54-200">Para compilar y empaquetar el proyecto, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="def54-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="def54-201">Este comando descarga las dependencias requeridas, las compilaciones y, luego, empaqueta el proyecto.</span><span class="sxs-lookup"><span data-stu-id="def54-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="def54-202">La salida se almacena en el directorio **/target** como **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="def54-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="def54-203">Prueba local</span><span class="sxs-lookup"><span data-stu-id="def54-203">Test locally</span></span>

<span data-ttu-id="def54-204">Dado que estas topologías solo leen y escriben en los centros de eventos, puede realizar una prueba local si tiene un [entorno de desarrollo de Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="def54-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="def54-205">Para la ejecución local en el entorno de desarrollo, utilice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="def54-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="def54-206">Ejecute la escritura:</span><span class="sxs-lookup"><span data-stu-id="def54-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="def54-207">Ejecute la lectura:</span><span class="sxs-lookup"><span data-stu-id="def54-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="def54-208">`--local`: ejecuta la topología en modo local (no distribuida).</span><span class="sxs-lookup"><span data-stu-id="def54-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="def54-209">`-R /writer.yaml`: carga la definición de la topología del `resources` empaquetado en el archivo jar.</span><span class="sxs-lookup"><span data-stu-id="def54-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="def54-210">Si la topología es un archivo del sistema de archivos local, especifique su ruta de acceso como último parámetro.</span><span class="sxs-lookup"><span data-stu-id="def54-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="def54-211">`--filter dev.properties`: usa el contenido de `dev.properties` para rellenar los valores de las definiciones de las topologías.</span><span class="sxs-lookup"><span data-stu-id="def54-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="def54-212">Por ejemplo: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="def54-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="def54-213">La salida se registra en la consola cuando se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="def54-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="def54-214">Para detener la topología, use __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="def54-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="def54-215">Implementación de las topologías</span><span class="sxs-lookup"><span data-stu-id="def54-215">Deploy the topologies</span></span>

1. <span data-ttu-id="def54-216">Use SCP para copiar el paquete jar en su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def54-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="def54-217">Reemplace USERNAME con el usuario SSH para el clúster.</span><span class="sxs-lookup"><span data-stu-id="def54-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="def54-218">Reemplace CLUSTERNAME por el nombre del clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="def54-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="def54-219">Si usó una contraseña para la cuenta SSH, se le pedirá que escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="def54-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="def54-220">Si usó una clave SSH con la cuenta, puede que necesite usar el parámetro `-i` para especificar la ruta de acceso al archivo de clave.</span><span class="sxs-lookup"><span data-stu-id="def54-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="def54-221">Por ejemplo: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="def54-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="def54-222">Este comando copia el archivo en el directorio principal del usuario SSH en el clúster.</span><span class="sxs-lookup"><span data-stu-id="def54-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="def54-223">Cuando termine de cargar el archivo, use SSH para conectarse con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def54-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="def54-224">Reemplace **USERNAME** por el nombre de su inicio de sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="def54-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="def54-225">Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def54-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="def54-226">Si usó una contraseña para la cuenta SSH, se le pedirá que escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="def54-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="def54-227">Si usó una clave SSH con la cuenta, puede que necesite usar el parámetro `-i` para especificar la ruta de acceso al archivo de clave.</span><span class="sxs-lookup"><span data-stu-id="def54-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="def54-228">En el ejemplo siguiente se cargará la clave privada desde `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="def54-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="def54-229">Use el comando siguiente para iniciar las topologías.</span><span class="sxs-lookup"><span data-stu-id="def54-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="def54-230">`--remote`: envía la topología al servicio Nimbus, que la inicia en los nodos de trabajo del clúster.</span><span class="sxs-lookup"><span data-stu-id="def54-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="def54-231">Para ver los datos registrados, vaya a https://CLUSTERNAME.azurehdinsight.net/stormui, donde __CLUSTERNAME__ es el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def54-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="def54-232">Seleccione las topologías y profundice hasta los componentes.</span><span class="sxs-lookup"><span data-stu-id="def54-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="def54-233">Seleccione la entrada del __puerto__ para que la instancia de un componente vea la información registrada.</span><span class="sxs-lookup"><span data-stu-id="def54-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="def54-234">Use el comando siguiente para detener las topologías.</span><span class="sxs-lookup"><span data-stu-id="def54-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="def54-235">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="def54-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="def54-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="def54-236">Next steps</span></span>

* [<span data-ttu-id="def54-237">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="def54-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
