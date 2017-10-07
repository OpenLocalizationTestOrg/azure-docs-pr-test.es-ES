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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight (Java)

Obtenga información acerca de cómo toouse centros de eventos de Azure con Storm en HDInsight. Este ejemplo utiliza componentes basados en Java tooread y escribir datos en los centros de eventos de Azure.

Centros de eventos de Azure permite tooprocess grandes cantidades de datos de sitios Web, aplicaciones y dispositivos. Hello pitorro de concentrador de eventos resulta fácil toouse Apache Storm en HDInsight tooanalyze estos datos en tiempo real. También puede escribir tooEvent centros de datos de Storm mediante Hola tornillo de centros de eventos.

## <a name="prerequisites"></a>Requisitos previos

* Una instancia de Apache Storm en un clúster de HDInsight, versión 3.6. Para más información, vea [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md) (Introducción a Storm en clúster de HDInsight).

    > [!IMPORTANT]
    > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un [Centro de eventos de Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Oracle Java Developer Kit (JDK) versión 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, como [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): Maven es un sistema de compilación de proyectos para proyectos de Java.

* Un editor de texto o un entorno de desarrollo integrado (IDE).

    > [!NOTE]
    > El editor o IDE puede tener una funcionalidad específica para trabajar con Maven que no se trata en este documento. Para obtener información acerca de las capacidades de Hola de su entorno de edición, consulte la documentación de hello para el producto de Hola que usa.

    * Un cliente SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Hola `ssh` y `scp` comandos. Se trata de un clúster de HDInsight de toocopy usa archivos toohello. En Windows, se obtienen a través de Bash en Windows 10.

## <a name="understanding-hello-example"></a>Ejemplo de Hola de descripción

Hola [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) ejemplo contiene dos topologías:

Hola `resources/writer.yaml` topología escribe datos aleatorios tooan concentrador de eventos de Azure. generan datos de Hola Hola `DeviceSpout` componente, y es un Id. de dispositivo aleatorio y el valor del dispositivo. Por lo tanto simula un hardware que emite un identificador de cadena y un valor numérico.

Tres `resources/reader.yaml` topología lee datos desde el centro de eventos (datos de hello escritos por EventHubWriter,) analiza los datos JSON de hello y, a continuación, registra hello `deviceId` y `deviceValue` datos.

Hola datos tienen el formato como un documento JSON antes de escribir tooEvent concentrador y, cuando lee el lector de Hola se analiza de JSON y pasarlo al tuplas. formato JSON de Hello es como sigue:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Configuración de proyecto

Hola `POM.xml` archivo contiene información de configuración para este proyecto de Maven. información interesante Hola es:

#### <a name="event-hub-components"></a>Componentes del centro de eventos

componente de Hola que lee y escribe los concentradores de eventos de tooAzure está ubicado en hello [HDInsight repositorio](https://github.com/hdinsight/mvn-rep). Hola siguientes secciones de hello `POM.xml` componentes de Hola de carga de archivos desde este repositorio

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Hola EventHubs apetezca charlar un aluvión de dependencia

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Este código xml define una dependencia para el paquete de eventhubs de hello, que contiene tanto un pitorro para leer desde los centros de eventos como un rayo para escribir tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Este código xml configura la salida de hello proyecto toogenerate para Java 8, que se usa en HDInsight 3.5 o posterior.

#### <a name="hello-maven-shade-plugin"></a>Hola maven complemento de sombra

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

Este código xml configura la salida de hello solución toopackage hello en un archivo jar de la misma. jar de Hello contiene el código del proyecto de Hola y dependencias necesarias. También se usa para:

* Cambiar el nombre de los archivos de licencia para las dependencias de Hola.
* Excluir la seguridad y las firmas.
* Asegúrese de que varias implementaciones de Hola misma interfaz se combinan en una entrada.

Estos valores de configuración evitan errores en tiempo de ejecución.

#### <a name="topology-definitions"></a>Definiciones de topología

Este ejemplo utiliza hello [flujo](https://storm.apache.org/releases/1.1.0/flux.html) framework. Este marco de trabajo usa las topologías YAML toodefine Hola. Hola principales ventajas es que no sean difíciles de codificación topología hello en el código de Java. Dado que la definición de hello es YAML, se puede cambiar antes de enviar la topología de hello, sin necesidad de toorecompile todo.

__writer.yaml__:

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

__reader.yaml__:

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

#### <a name="tell-hello-topology-about-event-hub"></a>Explíquenos topología Hola concentrador de eventos

En tiempo de ejecución Hola `dev.properties` archivo es toopass usado Hola concentrador de eventos configuración toohello topología. Hello en el ejemplo siguiente se es contenido de hello predeterminado del archivo hello:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Configuración de las variables de entorno

Hello siguientes variables de entorno pueden establecerse cuando se instalación Java y Hola JDK en su estación de trabajo de desarrollo. Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.

* **JAVA_HOME** -debe apuntar el directorio toohello donde está instalado Hola de Java runtime environment (JRE). Por ejemplo, en una distribución de Unix o Linux, debe tener un valor similar demasiado`/usr/lib/jvm/java-7-oracle`. En Windows, tendría un valor similar demasiado`c:\Program Files (x86)\Java\jre1.7`
* **Ruta de acceso** -debe contener Hola siguiendo las rutas de acceso:

  * **JAVA_HOME** (o ruta de acceso equivalente hello)
  * **JAVA_HOME\bin** (o ruta de acceso equivalente hello)
  * directorio de Hola donde está instalado Maven

## <a name="configure-event-hub"></a>Configuración del centro de eventos

Centros de eventos es el origen de datos de Hola para este ejemplo. Usar hello siguiendo los pasos toocreate un concentrador de eventos.

1. De hello [Portal clásico de Azure](https://manage.windowsazure.com), seleccione **NEW** > **Service Bus** > **concentrador de eventos**  >  **Creación personalizada**.

2. En hello **agregar un nuevo centro de eventos** pantalla, escriba un **nombre centro de eventos**. Seleccione hello **región** toocreate Hola concentrador y, a continuación, crear un espacio de nombres o seleccione uno existente. Por último, haga clic en hello **flecha** toocontinue.

    ![página 1 del asistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Seleccione Hola mismo **ubicación** como el aluvión de latencia de tooreduce del servidor de HDInsight y los costos.

3. En hello **Configurar centro de eventos** pantalla, escriba Hola **número de partición** y **retención de mensajes** valores. En este ejemplo, utilice un recuento de particiones de 10 y una retención de mensajes de 1. Tenga en cuenta el recuento de particiones de Hola porque necesita este valor más adelante.

    ![página 2 del asistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Después de concentrador de eventos de Hola Hola creado, seleccione espacio de nombres, seleccione **centros de eventos**y, a continuación, seleccione el concentrador de eventos de Hola que creó anteriormente.
5. Seleccione **configurar**, a continuación, cree dos nuevas directivas de acceso mediante el uso de hello siguiente información:

    <table>
    <tr><th>Nombre</th><th>Permisos</th></tr>
    <tr><td>Escritor</td><td>Los métodos Send</td></tr>
    <tr><td>Lector</td><td>Escuchar</td></tr>
    </table>

    Después de crear permisos de hello, seleccione hello **guardar** situado en la parte inferior de Hola de página de Hola. Estas directivas de acceso compartido son tooread usado y escribir tooEvent concentrador.

    ![directivas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Después de guardar las directivas de hello, usar hello **generador de claves de acceso compartido** final Hola de hello página tooretrieve Hola clave hello **escritor** y **lector** directivas. Guarde estas claves.

## <a name="download-and-build-hello-project"></a>Descargar y compile el proyecto de Hola

1. Descargar proyecto Hola de GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Puede descargar el paquete de Hola como un archivo zip o usar [git](https://git-scm.com/) tooclone proyecto de hello localmente.

2. Modificar hello `dev.properties` archivo con la configuración de hello para el centro de eventos.

3. Usar hello después toobuild y paquete en el proyecto hello:

        mvn package

    Este comando descarga las dependencias necesarias, compilaciones, y, a continuación, paquetes Hola proyecto. salida de Hello se almacena en hello **/target** directorio como **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Prueba local

Dado que estas topologías simplemente leerán y escribir tooEvent concentradores, puede probarlas localmente si tienes un [entorno de desarrollo de Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Usar hello siguiendo los pasos toorun localmente en el entorno de desarrollo de hello:

1. Ejecute el sistema de escritura de hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Ejecute lector hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Topología de hello ejecución en modo local (no distribuidas).
> * `-R /writer.yaml`: Cargar la definición de la topología de Hola de hello `resources` empaquetados en jar Hola. Si la topología de hello es un archivo en el sistema de archivos local de hello, especificar hello tooit de ruta de acceso como último parámetro de Hola en su lugar.
> * `--filter dev.properties`: Se usa contenido Hola de `dev.properties` toofill en valores de hello en definiciones de topología de Hola. Por ejemplo: `${eventhub.read.policy.name}`.

Salida es la consola de toohello registrados cuando se ejecuta localmente. Use __Ctrl + C__ topología de hello toostop.

## <a name="deploy-hello-topologies"></a>Implementar topologías de Hola

1. Use SCP toocopy Hola jar paquete tooyour clúster de HDInsight. Reemplace el nombre de usuario por usuario SSH de hello para el clúster. Reemplace CLUSTERNAME por nombre de Hola de su clúster de HDInsight:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Si utiliza una contraseña para su cuenta SSH, son contraseña de hello tooenter solicitadas. Si utiliza una clave SSH con cuenta de hello, puede que necesite toouse hello `-i` archivo de la clave de toohello toospecify Hola ruta de acceso de parámetro. Por ejemplo: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Este comando copia Hola archivo toohello directorio particular de su usuario SSH en clúster de Hola.

2. Una vez que ha finalizado la carga del archivo hello, use el clúster de HDInsight SSH tooconnect toohello. Reemplace **nombre de usuario** nombre hello del inicio de sesión SSH. Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Si utiliza una contraseña para su cuenta SSH, son contraseña de hello tooenter solicitadas. Si utiliza una clave SSH con cuenta de hello, puede que necesite toouse hello `-i` archivo de la clave de toohello toospecify Hola ruta de acceso de parámetro. Hello en el ejemplo siguiente se carga la clave privada Hola de `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Usar hello siguientes topologías de hello toostart de comando:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Hola topología toohello servicio Nimbus, que se inicia en nodos de trabajador de hello en clúster de Hola se envía.

4. datos de hello registran tooview, vaya a toohttps://CLUSTERNAME.azurehdinsight.net/stormui, donde __CLUSTERNAME__ es Hola nombre de su clúster de HDInsight. Seleccione las topologías de Hola y explorar en profundidad toohello componentes. Seleccione hello __puerto__ entrada para una instancia de un componente tooview la información registrada.

5. Usar hello siguientes topologías de hello toostop de comandos:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Eliminación del clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Pasos siguientes

* [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md)
