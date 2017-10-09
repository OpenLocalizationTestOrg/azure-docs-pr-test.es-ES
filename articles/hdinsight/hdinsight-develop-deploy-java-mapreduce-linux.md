---
title: aaaCreate MapReduce de Java para Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse aplicación de Apache Maven toocreate basados en Java MapReduce, a continuación, ejecútelo con Hadoop en HDInsight de Azure."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Desarrollo de programas MapReduce de Java para Hadoop en HDInsight

Obtenga información acerca de cómo toouse aplicación de Apache Maven toocreate basados en Java MapReduce, a continuación, ejecútelo con Hadoop en HDInsight de Azure.

> [!NOTE]
> En este ejemplo se probó más recientemente en HDInsight 3.6.

## <a name="prerequisites"></a>Requisitos previos

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o posterior (o un equivalente como OpenJDK).
    
    > [!NOTE]
    > Las versiones de HDInsight 3.4 y anteriores usan Java 7. HDInsight 3.5 y versiones posteriores usa Java 8.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Configuración del entorno de desarrollo

Hello siguientes variables de entorno pueden establecerse al instalar hello JDK y Java. Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.

* `JAVA_HOME`-debe apuntar el directorio toohello donde está instalado Hola de Java runtime environment (JRE). Por ejemplo, en un sistema OS X, Unix o Linux, debe tener un valor similar demasiado`/usr/lib/jvm/java-7-oracle`. En Windows, tendría un valor similar demasiado`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-debe contener Hola siguiendo las rutas de acceso:
  
  * `JAVA_HOME`(o ruta de acceso equivalente hello)

  * `JAVA_HOME\bin`(o ruta de acceso equivalente hello)

  * directorio de Hola donde está instalado Maven

## <a name="create-a-maven-project"></a>Creación de un proyecto de Maven

1. Desde una sesión de terminal, o la línea de comandos en el entorno de desarrollo, cambiar la ubicación de toohello de directorios que desee toostore este proyecto.

2. Hola de uso `mvn` comando, que se instala con Maven, hello toogenerate scaffolding para proyecto de Hola.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Si usa PowerShell, debe encerrar hello `-D` parámetros entre comillas dobles.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Este comando crea un directorio con nombre de hello especificado por hello `artifactID` parámetro (**wordcountjava** en este ejemplo.) Este directorio contiene Hola siguientes elementos:

   * `pom.xml`-Hola [modelo de objeto de proyecto (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) que contiene información y detalles de configuración utilizan proyectos de hello toobuild.

   * `src`-directorio de Hola que contiene la aplicación hello.

3. Eliminar hello `src/test/java/org/apache/hadoop/examples/apptest.java` archivo. No lo vamos a usar en este ejemplo.

## <a name="add-dependencies"></a>Adición de dependencias

1. Editar hello `pom.xml` de archivos y agregar Hola después de texto dentro de hello `<dependencies>` sección:
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    Esto define las bibliotecas requeridas (enumeradas en &lt;artifactId\>) de una versión específica (enumerada en &lt;version\>). En tiempo de compilación, estas dependencias se descargan del repositorio de Maven Hola predeterminado. Puede usar hello [búsqueda de repositorio de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview más.
   
    Hola `<scope>provided</scope>` indica Maven que estas dependencias no se deben empaquetar con la aplicación hello, como se proporcionan por clúster de HDInsight de hello en tiempo de ejecución.

    > [!IMPORTANT]
    > versión de Hola utilizada debe coincidir con versión de Hola de Hadoop presente en el clúster. Para obtener más información sobre las versiones, vea hello [versiones de componentes de HDInsight](hdinsight-component-versioning.md) documento.

2. Agregar Hola después toohello `pom.xml` archivo. Este texto debe estar dentro de hello `<project>...</project>` en archivo hello; por ejemplo, entre las etiquetas `</dependencies>` y `</project>`.

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    primer complemento Hello configura hello [Maven tono complemento](http://maven.apache.org/plugins/maven-shade-plugin/), que es usado toobuild un uberjar (a veces denominado un fatjar), que contiene las dependencias requeridas por la aplicación hello. También se evita la duplicación de licencias en paquete jar de hello, que pueden causar problemas en algunos sistemas.

    Hola segundo complemento configura versión de Java de destino de Hola.

    > [!NOTE]
    > HDInsight 3.4 y versiones anteriores utilizan Java 7. HDInsight 3.5 y versiones posteriores usa Java 8.

3. Guardar hello `pom.xml` archivo.

## <a name="create-hello-mapreduce-application"></a>Crear aplicación de hello MapReduce

1. Vaya toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` Hola de directorio y el nombre `App.java` archivo demasiado`WordCount.java`.

2. Abra hello `WordCount.java` un archivo en un editor de texto y reemplace el contenido de hello con hello siguiente texto:
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    Nombre del paquete de hello aviso es `org.apache.hadoop.examples` y es el nombre de la clase hello `WordCount`. Estos nombres se utilizan cuando se envía el trabajo de MapReduce Hola.

3. Guarde el archivo hello.

## <a name="build-hello-application"></a>Compilar la aplicación hello

1. Cambiar toohello `wordcountjava` directory, si no está ya no existe.

2. Usar hello siguiente comando toobuild un archivo JAR de archivos que contienen aplicación hello:

   ```
   mvn clean package
   ```

    Este comando limpia los artefactos de compilación anterior, descarga los dependencias que no hayan sido instaladas, y a continuación, compila y empaquetar la aplicación de Hola.

3. Una vez que el comando hello finaliza, hello `wordcountjava/target` directorio contiene un archivo denominado `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Hola `wordcountjava-1.0-SNAPSHOT.jar` archivo es un uberjar, que contiene no solo el trabajo de WordCount hello, pero también requiere que las dependencias que Hola trabajo en tiempo de ejecución.

## <a id="upload"></a>Cargar archivo jar de Hola

Usar hello después comando tooupload archivo jar hello toohello HDInsight nodo principal:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Este comando copia los archivos de Hola desde el nodo principal de hello sistema local toohello. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Ejecutar trabajo de MapReduce de hello en Hadoop

1. Conectar tooHDInsight mediante SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Desde la sesión de SSH de hello, utilice Hola tras la aplicación de comando toorun Hola MapReduce:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Este comando inicia Hola aplicación WordCount MapReduce. archivo de entrada de Hello es `/example/data/gutenberg/davinci.txt`, y es el directorio de salida de hello `/example/data/wordcountout`. Archivo de entrada de Hola y de salida son toohello almacenado predeterminado almacenamiento Hola del clúster.

3. Cuando se completa el trabajo de hello, utilice Hola siguiendo los resultados del comando tooview hello:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Debería recibir una lista de palabras y los recuentos, con valores toohello similar siguiente texto:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Pasos siguientes

En este documento, ha aprendido cómo toodevelop un trabajo de MapReduce de Java. Vea Hola después de documentos para otro toowork maneras con HDInsight.

* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)

Para obtener más información, vea también hello [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

