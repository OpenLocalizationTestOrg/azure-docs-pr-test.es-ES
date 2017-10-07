---
title: aaaApache Storm con los componentes de Python - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una topología de Apache Storm que usa componentes de Python."
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
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="c21be-104">Desarrollo de topologías Apache Storm con Python en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c21be-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="c21be-105">Obtenga información acerca de cómo toocreate una topología de Apache Storm que usa componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="c21be-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="c21be-106">Apache Storm admite varios idiomas, incluso permitiendo que toocombine componentes de varios idiomas en una topología.</span><span class="sxs-lookup"><span data-stu-id="c21be-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="c21be-107">Hello flujo marco de trabajo (que se introdujo con Storm 0.10.0) permite tooeasily crear soluciones que usan componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="c21be-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c21be-108">información de Hello en este documento se probó con Storm en 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c21be-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="c21be-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="c21be-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c21be-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c21be-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c21be-111">código de Hello para este proyecto está disponible en [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="c21be-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c21be-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c21be-112">Prerequisites</span></span>

* <span data-ttu-id="c21be-113">Python 2.7 o versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="c21be-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="c21be-114">Java JDK 1.8 o versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="c21be-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="c21be-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="c21be-115">Maven 3</span></span>

* <span data-ttu-id="c21be-116">(Opcional) Un entorno de desarrollo de Storm local.</span><span class="sxs-lookup"><span data-stu-id="c21be-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="c21be-117">Un entorno de Storm local solo es necesario si desea que la topología de hello toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="c21be-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="c21be-118">Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo).</span><span class="sxs-lookup"><span data-stu-id="c21be-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="c21be-119">Compatibilidad con varios lenguajes de Storm</span><span class="sxs-lookup"><span data-stu-id="c21be-119">Storm multi-language support</span></span>

<span data-ttu-id="c21be-120">Apache Storm era toowork diseñada con componentes escritos mediante cualquier lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="c21be-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="c21be-121">componentes de Hello deben entender cómo toowork con hello [definición Thrift para Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="c21be-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="c21be-122">Para Python, un módulo se proporciona como parte del proyecto de Apache Storm Hola que le permite tooeasily interfaz con Storm.</span><span class="sxs-lookup"><span data-stu-id="c21be-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="c21be-123">Puede encontrar este módulo en [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="c21be-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="c21be-124">Storm es un proceso de Java que se ejecuta en hello Máquina Virtual Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="c21be-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="c21be-125">Los componentes escritos en otros lenguajes se ejecutan como subprocesos.</span><span class="sxs-lookup"><span data-stu-id="c21be-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="c21be-126">Hola Storm se comunica con estos subprocesos con mensajes JSON enviados a través de stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="c21be-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="c21be-127">Encontrará más detalles sobre la comunicación entre componentes en hello [Multi-lang protocolo](https://storm.apache.org/documentation/Multilang-protocol.html) documentación.</span><span class="sxs-lookup"><span data-stu-id="c21be-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="c21be-128">Python con el marco de trabajo de un flujo de Hola</span><span class="sxs-lookup"><span data-stu-id="c21be-128">Python with hello Flux framework</span></span>

<span data-ttu-id="c21be-129">marco de trabajo de un flujo de Hello permite topologías de Storm toodefine por separado de los componentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c21be-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="c21be-130">marco de trabajo de un flujo de Hello usa topología aluvión YAML toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="c21be-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="c21be-131">Hola texto siguiente es un ejemplo de cómo un componente de Python en el documento de hello YAML tooreference:</span><span class="sxs-lookup"><span data-stu-id="c21be-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="c21be-132">Hola clase `FluxShellSpout` es toostart usado hello `sentencespout.py` secuencia de comandos que implementa pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="c21be-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="c21be-133">Un flujo espera toobe de scripts de Python Hola Hola `/resources` directorio dentro de archivo jar de Hola que contenga Hola topología.</span><span class="sxs-lookup"><span data-stu-id="c21be-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="c21be-134">Por lo que este ejemplo almacena scripts de Python Hola Hola `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="c21be-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="c21be-135">Hola `pom.xml` incluye este archivo mediante Hola continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="c21be-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="c21be-136">Como se mencionó anteriormente, hay un `storm.py` archivo que implementa la definición de Thrift de Hola para Storm.</span><span class="sxs-lookup"><span data-stu-id="c21be-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="c21be-137">marco de trabajo de un flujo de Hello incluye `storm.py` cuando proyecto Hola se genera automáticamente, por lo que no tiene tooworry de incluirlo.</span><span class="sxs-lookup"><span data-stu-id="c21be-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="c21be-138">Compile el proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="c21be-138">Build hello project</span></span>

<span data-ttu-id="c21be-139">Desde la raíz de hello del proyecto de hello, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c21be-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="c21be-140">Este comando crea un `target/WordCount-1.0-SNAPSHOT.jar` archivo que contiene Hola compila topología.</span><span class="sxs-lookup"><span data-stu-id="c21be-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="c21be-141">Ejecutar topología Hola localmente</span><span class="sxs-lookup"><span data-stu-id="c21be-141">Run hello topology locally</span></span>

<span data-ttu-id="c21be-142">topología de hello toorun localmente, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c21be-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="c21be-143">Este comando requiere un entorno de desarrollo de Storm local.</span><span class="sxs-lookup"><span data-stu-id="c21be-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="c21be-144">Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo).</span><span class="sxs-lookup"><span data-stu-id="c21be-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="c21be-145">Una vez Hola topología inicia, emite información toohello consola local similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="c21be-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="c21be-146">topología de hello toostop, use __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="c21be-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="c21be-147">Ejecutar topología aluvión de hello en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c21be-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="c21be-148">Siguiente Hola de uso del comando hello toocopy `WordCount-1.0-SNAPSHOT.jar` archivo tooyour Storm en clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c21be-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c21be-149">Reemplace `sshuser` con el usuario SSH de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="c21be-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="c21be-150">Reemplace `mycluster` con el nombre del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c21be-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="c21be-151">Es posible que la contraseña de hello tooenter solicitada para el usuario SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="c21be-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="c21be-152">Para más información sobre cómo usar SSH y SCP, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c21be-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c21be-153">Una vez que se ha cargado el archivo hello, conectar clúster toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="c21be-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="c21be-154">Desde la sesión de SSH de hello, utilice Hola después de topología de comando toostart hello en clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="c21be-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="c21be-155">Puede usar topología de hello Storm UI tooview hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c21be-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="c21be-156">Hola aluvión de interfaz de usuario se encuentra en https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="c21be-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="c21be-157">Reemplace `mycluster` por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="c21be-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="c21be-158">Cuando se ha iniciado una topología Storm, esta se ejecuta hasta que se detiene.</span><span class="sxs-lookup"><span data-stu-id="c21be-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="c21be-159">topología de hello toostop, utilice uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="c21be-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="c21be-160">Hola `storm kill TOPOLOGYNAME` comando desde la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="c21be-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="c21be-161">Hola **Kill** botón Hola aluvión de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="c21be-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c21be-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c21be-162">Next steps</span></span>

<span data-ttu-id="c21be-163">Vea Hola después de documentos para otro toouse maneras de Python con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c21be-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="c21be-164">¿Cómo toouse Python para los trabajos MapReduce de streaming</span><span class="sxs-lookup"><span data-stu-id="c21be-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="c21be-165">¿Cómo toouse Python usuario definida por las funciones (UDF) en Pig y Hive</span><span class="sxs-lookup"><span data-stu-id="c21be-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
