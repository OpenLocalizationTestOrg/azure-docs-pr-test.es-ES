---
title: Apache Storm con componentes de Python - Azure HDInsight | Microsoft Docs
description: "Aprenda a crear una topología de Apache Storm que use componentes de Python."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="aa70d-104">Desarrollo de topologías Apache Storm con Python en HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa70d-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="aa70d-105">Aprenda a crear una topología de Apache Storm que use componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="aa70d-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="aa70d-106">Apache Storm admite varios lenguajes, e incluso le permite combinar componentes de varios lenguajes en una topología.</span><span class="sxs-lookup"><span data-stu-id="aa70d-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="aa70d-107">El marco de trabajo de Flux (introducido con Storm 0.10.0) permite crear fácilmente soluciones que usan componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="aa70d-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa70d-108">La información de este documento se probó con Storm en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="aa70d-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="aa70d-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="aa70d-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aa70d-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aa70d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="aa70d-111">El código de este proyecto está disponible en [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="aa70d-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa70d-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa70d-112">Prerequisites</span></span>

* <span data-ttu-id="aa70d-113">Python 2.7 o versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="aa70d-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="aa70d-114">Java JDK 1.8 o versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="aa70d-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="aa70d-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="aa70d-115">Maven 3</span></span>

* <span data-ttu-id="aa70d-116">(Opcional) Un entorno de desarrollo de Storm local.</span><span class="sxs-lookup"><span data-stu-id="aa70d-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="aa70d-117">Un entorno de Storm local solo es necesario si desea ejecutar localmente la topología.</span><span class="sxs-lookup"><span data-stu-id="aa70d-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="aa70d-118">Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo).</span><span class="sxs-lookup"><span data-stu-id="aa70d-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="aa70d-119">Compatibilidad con varios lenguajes de Storm</span><span class="sxs-lookup"><span data-stu-id="aa70d-119">Storm multi-language support</span></span>

<span data-ttu-id="aa70d-120">Apache Storm se ha diseñado para funcionar con componentes escritos con cualquier lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="aa70d-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="aa70d-121">Los componentes deben aprender a trabajar con la [definición Thrift para Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="aa70d-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="aa70d-122">Para Python, se proporciona un módulo como parte del proyecto de Apache Storm que le permite interactuar fácilmente con Storm.</span><span class="sxs-lookup"><span data-stu-id="aa70d-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="aa70d-123">Puede encontrar este módulo en [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="aa70d-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="aa70d-124">Storm es un proceso de Java que se ejecuta en Máquina virtual Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="aa70d-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="aa70d-125">Los componentes escritos en otros lenguajes se ejecutan como subprocesos.</span><span class="sxs-lookup"><span data-stu-id="aa70d-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="aa70d-126">Storm se comunica con estos subprocesos mediante mensajes JSON enviados a través de stdin y stdout.</span><span class="sxs-lookup"><span data-stu-id="aa70d-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="aa70d-127">Se puede encontrar más detalles sobre la comunicación entre los componentes en la documentación de [Multi-lang protocolo](https://storm.apache.org/documentation/Multilang-protocol.html) (Protocolo de varios lenguajes).</span><span class="sxs-lookup"><span data-stu-id="aa70d-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="aa70d-128">Python con el marco de trabajo de Flux</span><span class="sxs-lookup"><span data-stu-id="aa70d-128">Python with the Flux framework</span></span>

<span data-ttu-id="aa70d-129">El marco de trabajo de Flux le permite definir las topologías de Storm de forma independiente con respecto a los componentes.</span><span class="sxs-lookup"><span data-stu-id="aa70d-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="aa70d-130">El marco de trabajo de Flux usa YAML para definir la topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="aa70d-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="aa70d-131">El siguiente texto es un ejemplo de cómo se hace referencia a un componente de Python en el documento de YAML:</span><span class="sxs-lookup"><span data-stu-id="aa70d-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="aa70d-132">La clase `FluxShellSpout` se usa para iniciar el script `sentencespout.py` que implementa el spout.</span><span class="sxs-lookup"><span data-stu-id="aa70d-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="aa70d-133">Flux espera que los scripts de Python estén en el directorio `/resources` dentro del archivo jar que contiene la topología.</span><span class="sxs-lookup"><span data-stu-id="aa70d-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="aa70d-134">Por ello, este ejemplo almacena los scripts de Python en el directorio `/multilang/resources`.</span><span class="sxs-lookup"><span data-stu-id="aa70d-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="aa70d-135">El archivo `pom.xml` incluye este archivo mediante el siguiente código XML:</span><span class="sxs-lookup"><span data-stu-id="aa70d-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="aa70d-136">Como se mencionó anteriormente, hay un archivo `storm.py` que implementa la definición de Thrift para Storm.</span><span class="sxs-lookup"><span data-stu-id="aa70d-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="aa70d-137">El marco de trabajo de Flux incluye `storm.py` automáticamente cuando se compila el proyecto, por lo que no tiene que preocuparse de incluirlo.</span><span class="sxs-lookup"><span data-stu-id="aa70d-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="aa70d-138">Compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="aa70d-138">Build the project</span></span>

<span data-ttu-id="aa70d-139">Desde la raíz del proyecto, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="aa70d-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="aa70d-140">Este comando crea un archivo `target/WordCount-1.0-SNAPSHOT.jar` que contiene la topología compilada.</span><span class="sxs-lookup"><span data-stu-id="aa70d-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="aa70d-141">Ejecución de la topología de manera local</span><span class="sxs-lookup"><span data-stu-id="aa70d-141">Run the topology locally</span></span>

<span data-ttu-id="aa70d-142">Para ejecutar la topología de manera local, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="aa70d-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="aa70d-143">Este comando requiere un entorno de desarrollo de Storm local.</span><span class="sxs-lookup"><span data-stu-id="aa70d-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="aa70d-144">Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo).</span><span class="sxs-lookup"><span data-stu-id="aa70d-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="aa70d-145">Una vez que se inicia la topología, esta emite información en la consola local que se parece al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="aa70d-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="aa70d-146">Para detener la topología, use __Ctrl+C__.</span><span class="sxs-lookup"><span data-stu-id="aa70d-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="aa70d-147">Ejecutar la topología de Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa70d-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="aa70d-148">Use el siguiente comando para copiar el archivo `WordCount-1.0-SNAPSHOT.jar` en el clúster de Storm en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="aa70d-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="aa70d-149">Reemplace `sshuser` con el usuario SSH para el clúster.</span><span class="sxs-lookup"><span data-stu-id="aa70d-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="aa70d-150">Reemplace `mycluster` por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="aa70d-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="aa70d-151">Puede que se le solicite que escriba la contraseña del usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="aa70d-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="aa70d-152">Para más información sobre cómo usar SSH y SCP, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aa70d-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aa70d-153">Una vez cargado el archivo, conéctese al clúster mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="aa70d-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="aa70d-154">En la sesión SSH, use el siguiente comando para iniciar la topología en el clúster:</span><span class="sxs-lookup"><span data-stu-id="aa70d-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="aa70d-155">Puede usar la interfaz de usuario de Storm para ver la topología en el clúster.</span><span class="sxs-lookup"><span data-stu-id="aa70d-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="aa70d-156">Esta interfaz de usuario web se encuentra en https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="aa70d-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="aa70d-157">Reemplace `mycluster` por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="aa70d-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="aa70d-158">Cuando se ha iniciado una topología Storm, esta se ejecuta hasta que se detiene.</span><span class="sxs-lookup"><span data-stu-id="aa70d-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="aa70d-159">Para detener la topología, use uno de los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="aa70d-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="aa70d-160">El comando `storm kill TOPOLOGYNAME` desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="aa70d-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="aa70d-161">El botón **Terminar** en la interfaz de usuario de Storm.</span><span class="sxs-lookup"><span data-stu-id="aa70d-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aa70d-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa70d-162">Next steps</span></span>

<span data-ttu-id="aa70d-163">Consulte los siguientes documentos para ver otras maneras de usar Python con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa70d-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="aa70d-164">Uso de Python para la transmisión de trabajos de MapReduce</span><span class="sxs-lookup"><span data-stu-id="aa70d-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="aa70d-165">Uso de funciones definidas por el usuario (UDF) de Python en Pig y Hive</span><span class="sxs-lookup"><span data-stu-id="aa70d-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
