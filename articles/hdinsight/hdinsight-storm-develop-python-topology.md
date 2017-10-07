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
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Desarrollo de topologías Apache Storm con Python en HDInsight

Obtenga información acerca de cómo toocreate una topología de Apache Storm que usa componentes de Python. Apache Storm admite varios idiomas, incluso permitiendo que toocombine componentes de varios idiomas en una topología. Hello flujo marco de trabajo (que se introdujo con Storm 0.10.0) permite tooeasily crear soluciones que usan componentes de Python.

> [!IMPORTANT]
> información de Hello en este documento se probó con Storm en 3.6 de HDInsight. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

código de Hello para este proyecto está disponible en [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Requisitos previos

* Python 2.7 o versiones posteriores

* Java JDK 1.8 o versiones posteriores

* Maven 3

* (Opcional) Un entorno de desarrollo de Storm local. Un entorno de Storm local solo es necesario si desea que la topología de hello toorun localmente. Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo).

## <a name="storm-multi-language-support"></a>Compatibilidad con varios lenguajes de Storm

Apache Storm era toowork diseñada con componentes escritos mediante cualquier lenguaje de programación. componentes de Hello deben entender cómo toowork con hello [definición Thrift para Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Para Python, un módulo se proporciona como parte del proyecto de Apache Storm Hola que le permite tooeasily interfaz con Storm. Puede encontrar este módulo en [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Storm es un proceso de Java que se ejecuta en hello Máquina Virtual Java (JVM). Los componentes escritos en otros lenguajes se ejecutan como subprocesos. Hola Storm se comunica con estos subprocesos con mensajes JSON enviados a través de stdin/stdout. Encontrará más detalles sobre la comunicación entre componentes en hello [Multi-lang protocolo](https://storm.apache.org/documentation/Multilang-protocol.html) documentación.

## <a name="python-with-hello-flux-framework"></a>Python con el marco de trabajo de un flujo de Hola

marco de trabajo de un flujo de Hello permite topologías de Storm toodefine por separado de los componentes de Hola. marco de trabajo de un flujo de Hello usa topología aluvión YAML toodefine Hola. Hola texto siguiente es un ejemplo de cómo un componente de Python en el documento de hello YAML tooreference:

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

Hola clase `FluxShellSpout` es toostart usado hello `sentencespout.py` secuencia de comandos que implementa pitorro Hola.

Un flujo espera toobe de scripts de Python Hola Hola `/resources` directorio dentro de archivo jar de Hola que contenga Hola topología. Por lo que este ejemplo almacena scripts de Python Hola Hola `/multilang/resources` directory. Hola `pom.xml` incluye este archivo mediante Hola continuación de XML:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Como se mencionó anteriormente, hay un `storm.py` archivo que implementa la definición de Thrift de Hola para Storm. marco de trabajo de un flujo de Hello incluye `storm.py` cuando proyecto Hola se genera automáticamente, por lo que no tiene tooworry de incluirlo.

## <a name="build-hello-project"></a>Compile el proyecto de Hola

Desde la raíz de hello del proyecto de hello, use Hola siguiente comando:

```bash
mvn clean compile package
```

Este comando crea un `target/WordCount-1.0-SNAPSHOT.jar` archivo que contiene Hola compila topología.

## <a name="run-hello-topology-locally"></a>Ejecutar topología Hola localmente

topología de hello toorun localmente, utilice Hola siguiente comando:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Este comando requiere un entorno de desarrollo de Storm local. Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo).

Una vez Hola topología inicia, emite información toohello consola local similar toohello siguiente texto:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


topología de hello toostop, use __Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Ejecutar topología aluvión de hello en HDInsight

1. Siguiente Hola de uso del comando hello toocopy `WordCount-1.0-SNAPSHOT.jar` archivo tooyour Storm en clúster de HDInsight:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Reemplace `sshuser` con el usuario SSH de hello para el clúster. Reemplace `mycluster` con el nombre del clúster de Hola. Es posible que la contraseña de hello tooenter solicitada para el usuario SSH Hola.

    Para más información sobre cómo usar SSH y SCP, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Una vez que se ha cargado el archivo hello, conectar clúster toohello mediante SSH:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Desde la sesión de SSH de hello, utilice Hola después de topología de comando toostart hello en clúster de hello:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. Puede usar topología de hello Storm UI tooview hello en clúster de Hola. Hola aluvión de interfaz de usuario se encuentra en https://mycluster.azurehdinsight.net/stormui. Reemplace `mycluster` por el nombre del clúster.

> [!NOTE]
> Cuando se ha iniciado una topología Storm, esta se ejecuta hasta que se detiene. topología de hello toostop, utilice uno de los siguientes métodos de hello:
>
> * Hola `storm kill TOPOLOGYNAME` comando desde la línea de comandos de Hola
> * Hola **Kill** botón Hola aluvión de interfaz de usuario.


## <a name="next-steps"></a>Pasos siguientes

Vea Hola después de documentos para otro toouse maneras de Python con HDInsight:

* [¿Cómo toouse Python para los trabajos MapReduce de streaming](hdinsight-hadoop-streaming-python.md)
* [¿Cómo toouse Python usuario definida por las funciones (UDF) en Pig y Hive](hdinsight-python.md)
