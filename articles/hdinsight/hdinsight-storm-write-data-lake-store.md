---
title: aaaApache Storm escribir tooStorage/Data Lake Store - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola almacenamiento de Apache Storm toowrite toohello HDFS compatible para HDInsight. Almacén de Azure Data Lake o almacenamiento de Azure proporcionan almacenamiento de hello HDFS comptabile para HDInsight. Este documento y un ejemplo de Hola a asociado, muestran cómo se componente de hello HdfsBolt pueden toowrite usado toohello predeterminado almacenamiento de una tormenta en clúster de HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Escribir tooHDFS desde Apache Storm en HDInsight

Obtenga información acerca de cómo toouse Storm toowrite datos toohello almacenamiento compatible con HDFS utiliza Apache Storm en HDInsight. HDInsight puede usar tanto Azure Storage como Azure Data Lake como almacenamiento compatible con HDFS. Storm proporciona un [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente que escribe datos tooHDFS. Este documento proporciona información sobre cómo escribir tooeither tipo de almacenamiento de hello HdfsBolt. 

> [!IMPORTANT]
> ejemplo de Hola topología utilizada en este documento se basa en los componentes que se incluyen con Storm en HDInsight. Puede requerir toowork modificación con almacén de Azure Data Lake cuando se usa con otros clústeres de Apache Storm.

## <a name="get-hello-code"></a>Obtener el código de hello

proyecto de Hola que contiene esta topología está disponible como una descarga desde [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile este proyecto, deberá Hola siguiente configuración para el entorno de desarrollo:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versiones posteriores. HDInsight 3.5 y versiones posteriores requieren Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Hello siguientes variables de entorno pueden establecerse cuando se instalación Java y Hola JDK en su estación de trabajo de desarrollo. Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.

* `JAVA_HOME`-debe apuntar toohello directorio donde hello JDK está instalado.
* `PATH`-debe contener Hola siguiendo las rutas de acceso:
  
    * `JAVA_HOME`(o la ruta de acceso equivalente hello).
    * `JAVA_HOME\bin`(o la ruta de acceso equivalente hello).
    * directorio de Hola donde está instalado Maven.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>¿Cómo toouse Hola HdfsBolt con HDInsight

> [!IMPORTANT]
> Antes de usar hello HdfsBolt con Storm en HDInsight, primero debe usar un archivos jar de script acción toocopy necesario en hello `extpath` para Storm. Para obtener más información, vea hello [configurar clústeres de hello](#configure) sección.

Hola HdfsBolt utiliza el esquema de archivo de Hola que proporcione cómo toounderstand toowrite tooHDFS. Con HDInsight, utilice uno de hello siguientes esquemas:

* `wasb://`: se usa con una cuenta de Azure Storage.
* `adl://`: se usa con Azure Data Lake Store.

Hello tabla siguiente proporciona ejemplos de uso de archivos de esquema de Hola para diferentes escenarios:

| Esquema | Notas |
| ----- | ----- |
| `wasb:///` | cuenta de almacenamiento predeterminada de Hello es un contenedor de blob en una cuenta de almacenamiento de Azure |
| `adl:///` | cuenta de almacenamiento predeterminada de Hello es un directorio en el almacén de Azure Data Lake. Durante la creación del clúster, debe especificar el directorio de hello en el almacén de Data Lake es Hola raíz HDFS del clúster de hello. Por ejemplo, hello `/clusters/myclustername/` directory. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Una cuenta de almacenamiento de Azure (adicional) no predeterminado asociada con el clúster de Hola. |
| `adl://STORENAME/` | raíz de Hola de hello usa Hola clúster de almacén de Data Lake. Este esquema permite tooaccess datos que se encuentran fuera del directorio de Hola que contiene el sistema de archivos del clúster de Hola. |

Para obtener más información, vea hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) referencia en Apache.org.

### <a name="example-configuration"></a>Configuración de ejemplo

Hola YAML siguiente es un extracto de hello `resources/writetohdfs.yaml` archivo incluido en el ejemplo de Hola. Este archivo define la topología de aluvión de hello mediante hello [flujo](https://storm.apache.org/releases/1.1.0/flux.html) framework para Apache Storm.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Este YAML define Hola siguientes elementos:

* `syncPolicy`: Defina cuándo archivos de sistema de archivos toohello sincronizado/vaciados. En este ejemplo, cada 1000 tuplas.
* `fileNameFormat`: Define toouse de patrón de nombre de ruta de acceso y Hola al escribir archivos. En este ejemplo, se proporciona la ruta de acceso de hello en tiempo de ejecución mediante un filtro y extensión de archivo hello es `.txt`.
* `recordFormat`: Define el formato interno de Hola de archivos de hello escritos. En este ejemplo, los campos están delimitados por hello `|` caracteres.
* `rotationPolicy`: Define cuándo toorotate archivos. En este ejemplo no se realiza ningún giro.
* `hdfs-bolt`: Utiliza Hola componentes anteriores como parámetros de configuración para hello `HdfsBolt` clase.

Para obtener más información sobre el marco de trabajo de un flujo de hello, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Configuración de clúster de Hola

De forma predeterminada, Storm en HDInsight no incluye los componentes de hello HdfsBolt utiliza toocommunicate con almacenamiento de Azure o almacén de Data Lake en classpath del aluvión. Script de uso Hola siguiente acción tooadd estos toohello componentes `extlib` aluvión de directorio en el clúster:

| URI de script | Nodos tooapply a | Parámetros || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |

Para obtener información sobre el uso de esta secuencia de comandos con el clúster, vea hello [HDInsight personalizar clústeres mediante acciones de script](./hdinsight-hadoop-customize-cluster-linux.md) documento.

## <a name="build-and-package-hello-topology"></a>Compilar y empaquetar topología Hola

1. Descargar el proyecto de ejemplo de Hola de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour entorno de desarrollo.

2. Desde un símbolo del sistema, terminal, o una sesión de shell, cambiar directorios toohello raíz de hello descarga proyecto. toobuild y paquete Hola topología, use Hola siguiente comando:
   
        mvn compile package
   
    Una vez que se completa la compilación de Hola y el empaquetado, hay un directorio denominado `target`, que contiene un archivo denominado `StormToHdfs-1.0-SNAPSHOT.jar`. Este archivo contiene la topología de hello compilado.

## <a name="deploy-and-run-hello-topology"></a>Implementar y ejecutar topología Hola

1. Usar hello después de clúster de HDInsight de toohello de topología de comando toocopy Hola. Reemplace **usuario** con el nombre de usuario SSH de Hola que utilizó al crear el clúster de Hola. Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Cuando se le solicite, escriba contraseña de hello usada al crear el usuario SSH de hello para el clúster de Hola. Si utiliza una clave pública en lugar de una contraseña, puede que necesite toouse hello `-i` parámetro toospecify Hola ruta de acceso toohello que coinciden con la clave privada.
   
   > [!NOTE]
   > Para obtener más información sobre cómo usar `scp` con HDInsight, consulte [Conexión a través de SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Una vez completada la carga de hello, utilice Hola después de clúster de HDInsight de toohello tooconnect mediante SSH. Reemplace **usuario** con el nombre de usuario SSH de Hola que utilizó al crear el clúster de Hola. Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Cuando se le solicite, escriba contraseña de hello usada al crear el usuario SSH de hello para el clúster de Hola. Si utiliza una clave pública en lugar de una contraseña, puede que necesite toouse hello `-i` parámetro toospecify Hola ruta de acceso toohello que coinciden con la clave privada.
   
   Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una vez conectado, use Hola comando siguiente toocreate un archivo denominado `dev.properties`:

        nano dev.properties

4. Hola de uso después de texto como contenido de Hola de hello `dev.properties` archivo:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > En este ejemplo se da por supuesto que su clúster usa una cuenta de almacenamiento de Azure como almacenamiento predeterminado de Hola. Si el clúster usa Azure Data Lake Store, use `hdfs.url: adl:///`.
    
    archivo de hello toosave, use __Ctrl + X__, a continuación, __Y__y, finalmente, __ENTRAR__. valores de Hello en este archivo establecen URL de almacén de Data Lake de Hola y el nombre del directorio de Hola que se escriben datos en.

3. Usar hello después de la topología de hello toostart de comando:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Este comando inicia la topología de hello mediante el marco de un flujo de hello mediante el envío de nodo de Nimbus toohello de clúster de Hola. topología de Hello está definida por hello `writetohdfs.yaml` los archivos incluidos en el archivo jar de Hola. Hola `dev.properties` archivo se pasa como un filtro y se leen los valores de hello contenidos en el archivo hello topología Hola.

## <a name="view-output-data"></a>Visualización de datos de salida

datos de hello tooview, usar hello siguiente comando:

    hdfs dfs -ls /stormdata/

Se muestra una lista de archivos de hello creados por esta topología.

Hello lista siguiente es un ejemplo de datos de hello devuelto por los comandos anteriores de hello:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Detener la topología de Hola

Topologías de Storm ejecutan hasta que detenga o se elimina el clúster de Hola. toostop Hola topología, usar hello siguiente comando:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Eliminación del clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toouse Storm toowrite tooAzure almacenamiento y almacén de Azure Data Lake, detectar otros [Storm ejemplos para HDInsight](hdinsight-storm-example-topology.md).

