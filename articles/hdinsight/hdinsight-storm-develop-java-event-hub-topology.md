---
title: aaaProcess eventos desde los centros de eventos con Storm en HDInsight con Java | Documentos de Microsoft
description: "Obtenga información acerca de cómo se crean tooprocess datos de los centros de eventos con una topología de Java Storm con Maven."
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
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="767c6-103">Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="767c6-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="767c6-104">Obtenga información acerca de cómo toouse centros de eventos de Azure con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="767c6-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="767c6-105">Este ejemplo utiliza componentes basados en Java tooread y escribir datos en los centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="767c6-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="767c6-106">Centros de eventos de Azure permite tooprocess grandes cantidades de datos de sitios Web, aplicaciones y dispositivos.</span><span class="sxs-lookup"><span data-stu-id="767c6-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="767c6-107">Hello pitorro de concentrador de eventos resulta fácil toouse Apache Storm en HDInsight tooanalyze estos datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="767c6-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="767c6-108">También puede escribir tooEvent centros de datos de Storm mediante Hola tornillo de centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="767c6-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="767c6-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="767c6-109">Prerequisites</span></span>

* <span data-ttu-id="767c6-110">Una instancia de Apache Storm en un clúster de HDInsight, versión 3.6.</span><span class="sxs-lookup"><span data-stu-id="767c6-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="767c6-111">Para más información, vea [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md) (Introducción a Storm en clúster de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="767c6-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="767c6-112">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="767c6-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="767c6-113">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="767c6-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="767c6-114">Un [Centro de eventos de Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="767c6-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="767c6-115">[Oracle Java Developer Kit (JDK) versión 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, como [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="767c6-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="767c6-116">[Maven](https://maven.apache.org/download.cgi): Maven es un sistema de compilación de proyectos para proyectos de Java.</span><span class="sxs-lookup"><span data-stu-id="767c6-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="767c6-117">Un editor de texto o un entorno de desarrollo integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="767c6-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="767c6-118">El editor o IDE puede tener una funcionalidad específica para trabajar con Maven que no se trata en este documento.</span><span class="sxs-lookup"><span data-stu-id="767c6-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="767c6-119">Para obtener información acerca de las capacidades de Hola de su entorno de edición, consulte la documentación de hello para el producto de Hola que usa.</span><span class="sxs-lookup"><span data-stu-id="767c6-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="767c6-120">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="767c6-120">An SSH client.</span></span> <span data-ttu-id="767c6-121">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="767c6-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="767c6-122">Hola `ssh` y `scp` comandos.</span><span class="sxs-lookup"><span data-stu-id="767c6-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="767c6-123">Se trata de un clúster de HDInsight de toocopy usa archivos toohello.</span><span class="sxs-lookup"><span data-stu-id="767c6-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="767c6-124">En Windows, se obtienen a través de Bash en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="767c6-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="767c6-125">Ejemplo de Hola de descripción</span><span class="sxs-lookup"><span data-stu-id="767c6-125">Understanding hello example</span></span>

<span data-ttu-id="767c6-126">Hola [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) ejemplo contiene dos topologías:</span><span class="sxs-lookup"><span data-stu-id="767c6-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="767c6-127">Hola `resources/writer.yaml` topología escribe datos aleatorios tooan concentrador de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="767c6-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="767c6-128">generan datos de Hola Hola `DeviceSpout` componente, y es un Id. de dispositivo aleatorio y el valor del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="767c6-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="767c6-129">Por lo tanto simula un hardware que emite un identificador de cadena y un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="767c6-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="767c6-130">Tres `resources/reader.yaml` topología lee datos desde el centro de eventos (datos de hello escritos por EventHubWriter,) analiza los datos JSON de hello y, a continuación, registra hello `deviceId` y `deviceValue` datos.</span><span class="sxs-lookup"><span data-stu-id="767c6-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="767c6-131">Hola datos tienen el formato como un documento JSON antes de escribir tooEvent concentrador y, cuando lee el lector de Hola se analiza de JSON y pasarlo al tuplas.</span><span class="sxs-lookup"><span data-stu-id="767c6-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="767c6-132">formato JSON de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="767c6-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="767c6-133">Configuración de proyecto</span><span class="sxs-lookup"><span data-stu-id="767c6-133">Project configuration</span></span>

<span data-ttu-id="767c6-134">Hola `POM.xml` archivo contiene información de configuración para este proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="767c6-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="767c6-135">información interesante Hola es:</span><span class="sxs-lookup"><span data-stu-id="767c6-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="767c6-136">Componentes del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="767c6-136">Event Hub components</span></span>

<span data-ttu-id="767c6-137">componente de Hola que lee y escribe los concentradores de eventos de tooAzure está ubicado en hello [HDInsight repositorio](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="767c6-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="767c6-138">Hola siguientes secciones de hello `POM.xml` componentes de Hola de carga de archivos desde este repositorio</span><span class="sxs-lookup"><span data-stu-id="767c6-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="767c6-139">Hola EventHubs apetezca charlar un aluvión de dependencia</span><span class="sxs-lookup"><span data-stu-id="767c6-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="767c6-140">Este código xml define una dependencia para el paquete de eventhubs de hello, que contiene tanto un pitorro para leer desde los centros de eventos como un rayo para escribir tooit.</span><span class="sxs-lookup"><span data-stu-id="767c6-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="767c6-141">Este código xml configura la salida de hello proyecto toogenerate para Java 8, que se usa en HDInsight 3.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="767c6-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="767c6-142">Hola maven complemento de sombra</span><span class="sxs-lookup"><span data-stu-id="767c6-142">hello maven-shade-plugin</span></span>

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

<span data-ttu-id="767c6-143">Este código xml configura la salida de hello solución toopackage hello en un archivo jar de la misma.</span><span class="sxs-lookup"><span data-stu-id="767c6-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="767c6-144">jar de Hello contiene el código del proyecto de Hola y dependencias necesarias.</span><span class="sxs-lookup"><span data-stu-id="767c6-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="767c6-145">También se usa para:</span><span class="sxs-lookup"><span data-stu-id="767c6-145">It is also used to:</span></span>

* <span data-ttu-id="767c6-146">Cambiar el nombre de los archivos de licencia para las dependencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="767c6-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="767c6-147">Excluir la seguridad y las firmas.</span><span class="sxs-lookup"><span data-stu-id="767c6-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="767c6-148">Asegúrese de que varias implementaciones de Hola misma interfaz se combinan en una entrada.</span><span class="sxs-lookup"><span data-stu-id="767c6-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="767c6-149">Estos valores de configuración evitan errores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="767c6-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="767c6-150">Definiciones de topología</span><span class="sxs-lookup"><span data-stu-id="767c6-150">Topology definitions</span></span>

<span data-ttu-id="767c6-151">Este ejemplo utiliza hello [flujo](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="767c6-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="767c6-152">Este marco de trabajo usa las topologías YAML toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="767c6-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="767c6-153">Hola principales ventajas es que no sean difíciles de codificación topología hello en el código de Java.</span><span class="sxs-lookup"><span data-stu-id="767c6-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="767c6-154">Dado que la definición de hello es YAML, se puede cambiar antes de enviar la topología de hello, sin necesidad de toorecompile todo.</span><span class="sxs-lookup"><span data-stu-id="767c6-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="767c6-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="767c6-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
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
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
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

<span data-ttu-id="767c6-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="767c6-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
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
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
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

# How data flows through hello components
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

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="767c6-157">Explíquenos topología Hola concentrador de eventos</span><span class="sxs-lookup"><span data-stu-id="767c6-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="767c6-158">En tiempo de ejecución Hola `dev.properties` archivo es toopass usado Hola concentrador de eventos configuración toohello topología.</span><span class="sxs-lookup"><span data-stu-id="767c6-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="767c6-159">Hello en el ejemplo siguiente se es contenido de hello predeterminado del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="767c6-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="767c6-160">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="767c6-160">Configure environment variables</span></span>

<span data-ttu-id="767c6-161">Hello siguientes variables de entorno pueden establecerse cuando se instalación Java y Hola JDK en su estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="767c6-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="767c6-162">Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.</span><span class="sxs-lookup"><span data-stu-id="767c6-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="767c6-163">**JAVA_HOME** -debe apuntar el directorio toohello donde está instalado Hola de Java runtime environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="767c6-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="767c6-164">Por ejemplo, en una distribución de Unix o Linux, debe tener un valor similar demasiado`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="767c6-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="767c6-165">En Windows, tendría un valor similar demasiado`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="767c6-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="767c6-166">**Ruta de acceso** -debe contener Hola siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="767c6-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="767c6-167">**JAVA_HOME** (o ruta de acceso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="767c6-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="767c6-168">**JAVA_HOME\bin** (o ruta de acceso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="767c6-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="767c6-169">directorio de Hola donde está instalado Maven</span><span class="sxs-lookup"><span data-stu-id="767c6-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="767c6-170">Configuración del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="767c6-170">Configure Event Hub</span></span>

<span data-ttu-id="767c6-171">Centros de eventos es el origen de datos de Hola para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="767c6-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="767c6-172">Usar hello siguiendo los pasos toocreate un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="767c6-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="767c6-173">De hello [Portal clásico de Azure](https://manage.windowsazure.com), seleccione **NEW** > **Service Bus** > **concentrador de eventos**  >  **Creación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="767c6-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="767c6-174">En hello **agregar un nuevo centro de eventos** pantalla, escriba un **nombre centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="767c6-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="767c6-175">Seleccione hello **región** toocreate Hola concentrador y, a continuación, crear un espacio de nombres o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="767c6-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="767c6-176">Por último, haga clic en hello **flecha** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="767c6-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![página 1 del asistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="767c6-178">Seleccione Hola mismo **ubicación** como el aluvión de latencia de tooreduce del servidor de HDInsight y los costos.</span><span class="sxs-lookup"><span data-stu-id="767c6-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="767c6-179">En hello **Configurar centro de eventos** pantalla, escriba Hola **número de partición** y **retención de mensajes** valores.</span><span class="sxs-lookup"><span data-stu-id="767c6-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="767c6-180">En este ejemplo, utilice un recuento de particiones de 10 y una retención de mensajes de 1.</span><span class="sxs-lookup"><span data-stu-id="767c6-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="767c6-181">Tenga en cuenta el recuento de particiones de Hola porque necesita este valor más adelante.</span><span class="sxs-lookup"><span data-stu-id="767c6-181">Note hello partition count because you need this value later.</span></span>

    ![página 2 del asistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="767c6-183">Después de concentrador de eventos de Hola Hola creado, seleccione espacio de nombres, seleccione **centros de eventos**y, a continuación, seleccione el concentrador de eventos de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="767c6-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="767c6-184">Seleccione **configurar**, a continuación, cree dos nuevas directivas de acceso mediante el uso de hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="767c6-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="767c6-185">Nombre</span><span class="sxs-lookup"><span data-stu-id="767c6-185">Name</span></span></th><th><span data-ttu-id="767c6-186">Permisos</span><span class="sxs-lookup"><span data-stu-id="767c6-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="767c6-187">Escritor</span><span class="sxs-lookup"><span data-stu-id="767c6-187">Writer</span></span></td><td><span data-ttu-id="767c6-188">Los métodos Send</span><span class="sxs-lookup"><span data-stu-id="767c6-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="767c6-189">Lector</span><span class="sxs-lookup"><span data-stu-id="767c6-189">Reader</span></span></td><td><span data-ttu-id="767c6-190">Escuchar</span><span class="sxs-lookup"><span data-stu-id="767c6-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="767c6-191">Después de crear permisos de hello, seleccione hello **guardar** situado en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="767c6-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="767c6-192">Estas directivas de acceso compartido son tooread usado y escribir tooEvent concentrador.</span><span class="sxs-lookup"><span data-stu-id="767c6-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![directivas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="767c6-194">Después de guardar las directivas de hello, usar hello **generador de claves de acceso compartido** final Hola de hello página tooretrieve Hola clave hello **escritor** y **lector** directivas.</span><span class="sxs-lookup"><span data-stu-id="767c6-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="767c6-195">Guarde estas claves.</span><span class="sxs-lookup"><span data-stu-id="767c6-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="767c6-196">Descargar y compile el proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="767c6-196">Download and build hello project</span></span>

1. <span data-ttu-id="767c6-197">Descargar proyecto Hola de GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="767c6-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="767c6-198">Puede descargar el paquete de Hola como un archivo zip o usar [git](https://git-scm.com/) tooclone proyecto de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="767c6-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="767c6-199">Modificar hello `dev.properties` archivo con la configuración de hello para el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="767c6-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="767c6-200">Usar hello después toobuild y paquete en el proyecto hello:</span><span class="sxs-lookup"><span data-stu-id="767c6-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="767c6-201">Este comando descarga las dependencias necesarias, compilaciones, y, a continuación, paquetes Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="767c6-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="767c6-202">salida de Hello se almacena en hello **/target** directorio como **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="767c6-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="767c6-203">Prueba local</span><span class="sxs-lookup"><span data-stu-id="767c6-203">Test locally</span></span>

<span data-ttu-id="767c6-204">Dado que estas topologías simplemente leerán y escribir tooEvent concentradores, puede probarlas localmente si tienes un [entorno de desarrollo de Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="767c6-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="767c6-205">Usar hello siguiendo los pasos toorun localmente en el entorno de desarrollo de hello:</span><span class="sxs-lookup"><span data-stu-id="767c6-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="767c6-206">Ejecute el sistema de escritura de hello:</span><span class="sxs-lookup"><span data-stu-id="767c6-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="767c6-207">Ejecute lector hello:</span><span class="sxs-lookup"><span data-stu-id="767c6-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="767c6-208">`--local`: Topología de hello ejecución en modo local (no distribuidas).</span><span class="sxs-lookup"><span data-stu-id="767c6-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="767c6-209">`-R /writer.yaml`: Cargar la definición de la topología de Hola de hello `resources` empaquetados en jar Hola.</span><span class="sxs-lookup"><span data-stu-id="767c6-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="767c6-210">Si la topología de hello es un archivo en el sistema de archivos local de hello, especificar hello tooit de ruta de acceso como último parámetro de Hola en su lugar.</span><span class="sxs-lookup"><span data-stu-id="767c6-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="767c6-211">`--filter dev.properties`: Se usa contenido Hola de `dev.properties` toofill en valores de hello en definiciones de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="767c6-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="767c6-212">Por ejemplo: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="767c6-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="767c6-213">Salida es la consola de toohello registrados cuando se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="767c6-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="767c6-214">Use __Ctrl + C__ topología de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="767c6-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="767c6-215">Implementar topologías de Hola</span><span class="sxs-lookup"><span data-stu-id="767c6-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="767c6-216">Use SCP toocopy Hola jar paquete tooyour clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="767c6-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="767c6-217">Reemplace el nombre de usuario por usuario SSH de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="767c6-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="767c6-218">Reemplace CLUSTERNAME por nombre de Hola de su clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="767c6-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="767c6-219">Si utiliza una contraseña para su cuenta SSH, son contraseña de hello tooenter solicitadas.</span><span class="sxs-lookup"><span data-stu-id="767c6-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="767c6-220">Si utiliza una clave SSH con cuenta de hello, puede que necesite toouse hello `-i` archivo de la clave de toohello toospecify Hola ruta de acceso de parámetro.</span><span class="sxs-lookup"><span data-stu-id="767c6-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="767c6-221">Por ejemplo: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="767c6-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="767c6-222">Este comando copia Hola archivo toohello directorio particular de su usuario SSH en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="767c6-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="767c6-223">Una vez que ha finalizado la carga del archivo hello, use el clúster de HDInsight SSH tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="767c6-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="767c6-224">Reemplace **nombre de usuario** nombre hello del inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="767c6-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="767c6-225">Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="767c6-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="767c6-226">Si utiliza una contraseña para su cuenta SSH, son contraseña de hello tooenter solicitadas.</span><span class="sxs-lookup"><span data-stu-id="767c6-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="767c6-227">Si utiliza una clave SSH con cuenta de hello, puede que necesite toouse hello `-i` archivo de la clave de toohello toospecify Hola ruta de acceso de parámetro.</span><span class="sxs-lookup"><span data-stu-id="767c6-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="767c6-228">Hello en el ejemplo siguiente se carga la clave privada Hola de `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="767c6-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="767c6-229">Usar hello siguientes topologías de hello toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="767c6-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="767c6-230">`--remote`: Hola topología toohello servicio Nimbus, que se inicia en nodos de trabajador de hello en clúster de Hola se envía.</span><span class="sxs-lookup"><span data-stu-id="767c6-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="767c6-231">datos de hello registran tooview, vaya a toohttps://CLUSTERNAME.azurehdinsight.net/stormui, donde __CLUSTERNAME__ es Hola nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="767c6-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="767c6-232">Seleccione las topologías de Hola y explorar en profundidad toohello componentes.</span><span class="sxs-lookup"><span data-stu-id="767c6-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="767c6-233">Seleccione hello __puerto__ entrada para una instancia de un componente tooview la información registrada.</span><span class="sxs-lookup"><span data-stu-id="767c6-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="767c6-234">Usar hello siguientes topologías de hello toostop de comandos:</span><span class="sxs-lookup"><span data-stu-id="767c6-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="767c6-235">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="767c6-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="767c6-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="767c6-236">Next steps</span></span>

* [<span data-ttu-id="767c6-237">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="767c6-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
