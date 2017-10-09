---
title: "aaaApache Storm topología de ejemplo Java - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las topologías de Apache Storm toocreate mediante la creación de una palabra de ejemplo en Java contar topología."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm,ejemplo de apache storm,storm java,ejemplo de topología de storm"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Crear una topología de Apache Storm en Java

Obtenga información acerca de cómo toocreate una topología basada en Java para Apache Storm. Vamos a crear una topología de Storm que implemente una aplicación de recuento de palabras. Utilice Maven toobuild y paquete hello en el proyecto. A continuación, aprenderá cómo toodefine Hola topología utilizando Hola framework de un flujo.

> [!NOTE]
> marco de trabajo de un flujo de Hello está disponible en Storm 0.10.0 o posterior. Storm 0.10.0 está disponible con HDInsight 3.3 y 3.4.

Después de completar los pasos de hello en este documento, puede implementar Hola topología tooApache Storm en HDInsight.

> [!NOTE]
> Una versión completa de ejemplos de topología de Storm Hola creado en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Requisitos previos

* [Kit de desarrolladores de Java (JDK) versión 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven es un sistema de compilación de proyectos para proyectos de Java.

* Un editor de texto o IDE.

## <a name="configure-environment-variables"></a>Configuración de las variables de entorno

Hello siguientes variables de entorno pueden establecerse al instalar hello JDK y Java. Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.

* **JAVA_HOME** -debe apuntar el directorio toohello donde está instalado Hola de Java runtime environment (JRE). Por ejemplo, en una distribución de Unix o Linux, debe tener un valor similar demasiado`/usr/lib/jvm/java-7-oracle`. En Windows, tendría un valor similar demasiado`c:\Program Files (x86)\Java\jre1.7`

* **Ruta de acceso** -debe contener Hola siguiendo las rutas de acceso:

  * **JAVA_HOME** (o ruta de acceso equivalente hello)

  * **JAVA_HOME\bin** (o ruta de acceso equivalente hello)

  * directorio de Hola donde está instalado Maven

## <a name="create-a-maven-project"></a>Creación de un proyecto de Maven

Desde la línea de comandos de hello, use Hola siguiente comando toocreate un proyecto de Maven **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> Si va a usar PowerShell, deberá poner comillas dobles alrededor de los parámetros `-D`.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Este comando crea un directorio denominado `WordCount` en la ubicación actual de hello, que contiene un proyecto básico de Maven. Hola `WordCount` directorio contiene Hola siguientes elementos:

* `pom.xml`: Contiene la configuración para proyectos de Maven Hola.
* `src\main\java\com\microsoft\example`: Contiene el código de la aplicación.
* `src\test\java\com\microsoft\example`: Contiene pruebas para la aplicación. 

### <a name="remove-hello-generated-example-code"></a>Quitar el código de ejemplo de Hola generado

Eliminar pruebas Hola generado y archivos de la aplicación hello:

* **src\test\java\com\microsoft\example\AppTest.java**
* **src\main\java\com\microsoft\example\App.java**

## <a name="add-maven-repositories"></a>Agregar repositorios de Maven

HDInsight se basa en hello Hortonworks Data Platform (HDP), por lo que se recomienda utilizar las dependencias de hello Hortonworks repositorio toodownload para los proyectos de Apache Storm. Hola __pom.xml__ , agregue Hola continuación de XML después de hello `<url>http://maven.apache.org</url>` línea:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Agregar propiedades

Maven permite valores de nivel de proyecto de toodefine denominados propiedades. Hola __pom.xml__, agregar Hola después texto después de hello `</repositories>` línea:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

Ahora puede usar este valor en otras secciones de hello `pom.xml`. Por ejemplo, al especificar la versión de Hola de componentes de Storm, puede utilizar `${storm.version}` en lugar de codificar de forma rígida un valor.

## <a name="add-dependencies"></a>Adición de dependencias

Agregue una dependencia para componentes de Storm. Abra hello `pom.xml` de archivos y agregar Hola después el código de hello `<dependencies>` sección:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

En tiempo de compilación, Maven Utilice esta información toolook `storm-core` en el repositorio de Maven Hola. Primero busca en el repositorio de hello en el equipo local. Si archivos hello no existe, experto en descarga de repositorio público de Maven de Hola y almacenarlos en el repositorio local de Hola.

> [!NOTE]
> Hola aviso `<scope>provided</scope>` línea en esta sección. Esta configuración le comunica Maven tooexclude **aluvión de núcleo** de ningún archivo JAR que se crea, dado que se proporciona al sistema de Hola.

## <a name="build-configuration"></a>Configuración de compilación

Complementos de maven le permiten fases de compilación de hello toocustomize del proyecto de Hola. Por ejemplo, cómo se compila el proyecto de Hola o cómo toopackage en un archivo JAR. Abra hello `pom.xml` de archivos y agregar Hola después el código directamente encima de hello `</project>` línea.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Esta sección es tooadd usa complementos, los recursos y otras opciones de configuración de compilación. Para obtener una referencia completa de hello **pom.xml** de archivos, consulte [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Agregar complementos

Para las topologías de Apache Storm implementadas en Java, Hola [Exec Maven complemento](http://www.mojohaus.org/exec-maven-plugin/) es útil porque permite tooeasily ejecuta topología Hola localmente en el entorno de desarrollo. Agregar Hola después toohello `<plugins>` sección de hello `pom.xml` archivo tooinclude Hola Exec Maven complemento:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Otro útil es complemento hello [Apache Maven compilador complemento](http://maven.apache.org/plugins/maven-compiler-plugin/), que es usado toochange opciones de compilación. cambios de Hola Hola versión de Java que Maven se usa para el origen de Hola y de destino para la aplicación.

* Para HDInsight __3.4 o una versión anterior__, establezca Hola origen y destino too__1.7__ de versión de Java.

* Para HDInsight __3.5__, establezca Hola origen y destino too__1.8__ de versión de Java.

Agregar Hola después texto Hola `<plugins>` sección de hello `pom.xml` tooinclude Hola Apache Maven compilador complemento de archivos. Este ejemplo especifica 1.8, por lo que la versión de HDInsight de destino de hello es 3.5.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Configure resources

sección de recursos de Hello permite tooinclude recursos de código como archivos de configuración necesarios para componentes de topología de Hola. En este ejemplo, agregar Hola después texto Hola `<resources>` sección de hello ' archivo pom.xml.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

En este ejemplo agrega el directorio de recursos de hello en raíz de Hola de proyecto de hello (`${basedir}`) como una ubicación que contiene recursos e incluye el archivo hello denominado `log4j2.xml`. Este archivo es tooconfigure usado topología Hola registra la información.

## <a name="create-hello-topology"></a>Crear topología de Hola

Una topología de Apache Storm basada en Java consta de tres componentes que debe crear (o hacer referencia) como una dependencia.

* **Spouts**: lee los orígenes de datos desde externo y emite flujos de datos en la topología de Hola.

* **Bolts**: realiza el procesamiento en flujos que emite spouts u otros bolts, y emite uno o varios flujos.

* **Topología**: define el modo spouts hello y tornillos se organizan y proporciona el punto de entrada de hello para la topología de Hola.

### <a name="create-hello-spout"></a>Crear pitorro Hola

requisitos de tooreduce para configurar orígenes de datos externos, Hola siguiendo pitorro simplemente emite frases aleatorias. Es una versión modificada de un pitorro que se proporciona con hello [ejemplos de Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Para obtener un ejemplo de un pitorro que lee de un origen de datos externo, consulte uno de hello en los ejemplos siguientes:
>
> * [TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): un spout de ejemplo que lee desde Twitter.
> * [Storm Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): un spout que lee desde Kafka.

Para pitorro hello, cree un archivo denominado `RandomSentenceSpout.java` en hello `src\main\java\com\microsoft\example` Hola directorio y use después el código Java como contenido de hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Aunque esta topología usa sola pitorro, otros usuarios pueden tener varios que introducir datos de orígenes diferentes en la topología de Hola.

### <a name="create-hello-bolts"></a>Crear Hola tornillos

Tornillos controlen el procesamiento de datos de Hola. Esta topología utiliza dos bolts:

* **SplitSentence**: divide las frases de hello emitidas por **RandomSentenceSpout** en palabras individuales.

* **WordCount**: cuenta cuántas veces se ha repetido cada palabra.

> [!NOTE]
> Tornillos pueden hacer cualquier cosa, por ejemplo, cálculo, persistencia o hablar tooexternal componentes.

Cree dos nuevos archivos, `SplitSentence.java` y `WordCount.java` en hello `src\main\java\com\microsoft\example` directory. Usar hello después de texto como contenido de Hola para archivos de hello:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Definir la topología de Hola

topología de Hello une spouts hello y los tornillos juntos en un gráfico, que define cómo fluyen los datos entre los componentes de Hola. También proporciona sugerencias de paralelismo que Storm utiliza al crear instancias de componentes de hello en clúster de Hola.

Hello imagen siguiente es un diagrama básico de gráfico de Hola de componentes para esta topología.

![Hola de diagrama que muestra spouts y los tornillos de organización](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement Hola topología, cree un archivo denominado `WordCountTopology.java` en hello `src\main\java\com\microsoft\example` directory. Usar hello después el código Java como contenido de Hola de archivo hello:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>registro

Storm utiliza Apache Log4j toolog información. Si no configura el registro, la topología de hello emite información de diagnóstico. toocontrol lo que se registra, cree un archivo denominado `log4j2.xml` en hello `resources` directory. Usar hello continuación de XML como contenido de Hola de archivo hello.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Este código XML configura un nuevo registrador para hello `com.microsoft.example` (clase), que incluye componentes de hello en esta topología de ejemplo. nivel de Hola se establece tootrace para este registrador, que captura la información de registro de emitidos por componentes en esta topología.

Hola `<Root level="error">` sección configura el nivel de raíz de Hola de registro (todo lo que no está en `com.microsoft.example`) tooonly información de error de registro.

Para obtener más información sobre la configuración de registro de Log4j, consulte [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> La versión 0.10.0 y superiores de Storm utilizan Log4j 2.x. Las versiones anteriores de Storm usaban Log4j 1.x, que empleaba otro formato de configuración del registro. Para obtener información sobre la configuración anterior de hello, consulte [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Topología de hello pruebas localmente

Después de guardar los archivos de hello, utilice Hola después topología localmente de comando tootest Hola.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Mientras se ejecuta, topología hello muestra información de inicio. Hello texto siguiente es un ejemplo de salida de recuento de hello word:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Este registro de ejemplo indica esa palabra Hola ' y ' se emitió 113 veces. Hello recuento continúa toogo hasta como topología Hola se ejecuta porque pitorro Hola continuamente emite Hola mismas frases.

Hay un intervalo de 5 segundos entre la emisión de las palabras y los recuentos. Hola **WordCount** componente está configurado tooonly emitir información cuando llega una tupla de graduación. Solicita que esas tuplas se entreguen solo cada cinco segundos.

## <a name="convert-hello-topology-tooflux"></a>Convertir Hola topología tooFlux

Un flujo es un nuevo marco disponible con Storm 0.10.0 y versiones posterior, lo que permite tooseparate configuración de implementación. Los componentes aún están definidos en Java, pero topología Hola se define utilizando un archivo YAML. Puede empaquetar una definición de topología de manera predeterminada con el proyecto, o usar un archivo independiente al enviar la topología de Hola. Al enviar Hola topología tooStorm, puede utilizar variables de entorno o valores de toopopulate de archivos de configuración en la definición de la topología YAML Hola.

archivo de Hello YAML define Hola componentes toouse de topología de Hola y Hola de flujo de datos entre ellos. Puede incluir un archivo YAML como parte del archivo jar de Hola o puede usar un archivo YAML externo.

Para más información sobre Flux, vea este documento sobre el [marco de trabajo de Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Due tooa [error (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) con Storm 1.0.1, puede que necesite tooinstall una [entorno de desarrollo de Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) localmente las topologías de un flujo de toorun.

1. Mover hello `WordCountTopology.java` archivo fuera del proyecto de Hola. Anteriormente, este archivo define la topología de hello, pero no es necesario con un flujo.

2. Hola `resources` directorio, cree un archivo denominado `topology.yaml`. Usar hello después de texto como contenido de Hola de este archivo.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Realizar Hola después cambios toohello `pom.xml` archivo.
   
   * Agregar Hola después nuevas dependencias en hello `<dependencies>` sección:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Agregar Hola después complemento toohello `<plugins>` sección. Este complemento controla la creación de hello de un paquete (archivo jar) para el proyecto de Hola y aplica algunos tooFlux específico de transformaciones al crear paquetes de saludo.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * Hola **exec-maven-plugin** `<configuration>` sección, cambie el valor de Hola para `<mainClass>` demasiado`org.apache.storm.flux.Flux`. Esta configuración permite toohandle flujo ejecuta topología Hola localmente en el desarrollo.

   * Hola `<resources>` sección, agregue Hola después toohello `<includes>`. Este código XML incluye el archivo hello YAML que define la topología de hello como parte del proyecto de Hola.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Topología de un flujo de Hola de prueba localmente

1. Use Hola después toocompile y ejecute la topología de un flujo de hello mediante Maven:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Si usa PowerShell, use Hola siguiente comando:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Este comando produce un error si la topología usa bits de Storm 1.0.1. Este error se debe a [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). En su lugar, [instalar Storm en su entorno de desarrollo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) y use Hola siguiendo la información.

    Si tiene [instalado Storm en el entorno de desarrollo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), puede usar Hola siguientes comandos en su lugar:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Hola `--local` parámetro topología Hola ejecuta en modo local en el entorno de desarrollo. Hola `-R /topology.yaml` parámetro utiliza hello `topology.yaml` recursos de archivos de topología de hello jar archivo toodefine Hola.

    Mientras se ejecuta, topología hello muestra información de inicio. Hola después de texto es un ejemplo de salida de hello:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Hay un retraso de 10 segundos entre los distintos lotes de la información registrada.

2. Realizar una copia de hello `topology.yaml` archivo de proyecto de Hola. Nuevo archivo de nombre hello `newtopology.yaml`. Hola `newtopology.yaml` de archivos, busque la siguiente Hola sección y cambie el valor Hola de `10` demasiado`5`. Este intervalo de saludo de modificación cambios entre la emisión de lotes de word cuenta de too5 de 10 segundos.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    También puede hacer lo siguiente si tiene Storm en el entorno de desarrollo:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Hola de cambio `/path/to/newtopology.yaml` toohello ruta toohello newtopology.yaml archivo creado en el paso anterior de Hola. Este comando usa hello newtopology.yaml como definición de topología de Hola. Puesto que no incluimos hello `compile` parámetro, Maven utiliza Hola versión de Hola proyecto creado en los pasos anteriores.

    Una vez Hola topología se inicia, debe tener en cuenta que tiempo Hola entre los distintos lotes emitidos ha cambiado el valor de Hola de tooreflect en newtopology.yaml. Para que pueda ver que puede cambiar la configuración a través de un archivo YAML sin necesidad de topología de hello toorecompile.

Para obtener más información sobre estas y otras características del marco de trabajo de un flujo de hello, consulte [flujo (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident es una abstracción de alto nivel que ofrece Storm. Admite el procesamiento con estado. Hola principal ventaja de Trident es que puede garantizar que cada mensaje que entra en la topología de Hola se procesa solo una vez. Si no se usa Trident, la topología solo puede garantizar que los mensajes se procesan al menos una vez. También hay otras diferencias, como los componentes integrados que se pueden usar en lugar de crear bolts. De hecho, los bolts se reemplazan por componentes menos genéricos, como filtros, proyecciones y funciones.

Las aplicaciones de Trident se pueden crear mediante proyectos de Maven. Usar hello basic mismo pasos tal como se presenta anteriormente en este artículo, solo el código de hello es diferente. Trident también no (actualmente) puede utilizarse con marco de trabajo de un flujo de Hola.

Para obtener más información acerca de Trident, vea hello [Introducción a la API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).

Para ver un ejemplo de una aplicación de Trident, consulte [Tendencias de Twitter con Apache Storm en HDInsight](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Pasos siguientes

Ha aprendido cómo toocreate una topología Storm con Java. Ahora obtenga información sobre:

* [Implementación y administración de topologías de Apache Storm en HDInsight](hdinsight-storm-deploy-monitor-topology.md)

* [Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Puede encontrar más topologías de ejemplo de Storm en [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).

