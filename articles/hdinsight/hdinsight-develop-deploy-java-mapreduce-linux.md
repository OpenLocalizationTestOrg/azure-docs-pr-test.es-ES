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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="24e16-103">Desarrollo de programas MapReduce de Java para Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="24e16-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="24e16-104">Obtenga información acerca de cómo toouse aplicación de Apache Maven toocreate basados en Java MapReduce, a continuación, ejecútelo con Hadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="24e16-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="24e16-105">En este ejemplo se probó más recientemente en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="24e16-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="24e16-106"><a name="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="24e16-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="24e16-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o posterior (o un equivalente como OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="24e16-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="24e16-108">Las versiones de HDInsight 3.4 y anteriores usan Java 7.</span><span class="sxs-lookup"><span data-stu-id="24e16-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="24e16-109">HDInsight 3.5 y versiones posteriores usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="24e16-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="24e16-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="24e16-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="24e16-111">Configuración del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="24e16-111">Configure development environment</span></span>

<span data-ttu-id="24e16-112">Hello siguientes variables de entorno pueden establecerse al instalar hello JDK y Java.</span><span class="sxs-lookup"><span data-stu-id="24e16-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="24e16-113">Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.</span><span class="sxs-lookup"><span data-stu-id="24e16-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="24e16-114">`JAVA_HOME`-debe apuntar el directorio toohello donde está instalado Hola de Java runtime environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="24e16-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="24e16-115">Por ejemplo, en un sistema OS X, Unix o Linux, debe tener un valor similar demasiado`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="24e16-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="24e16-116">En Windows, tendría un valor similar demasiado`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="24e16-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="24e16-117">`PATH`-debe contener Hola siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="24e16-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="24e16-118">`JAVA_HOME`(o ruta de acceso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="24e16-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="24e16-119">`JAVA_HOME\bin`(o ruta de acceso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="24e16-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="24e16-120">directorio de Hola donde está instalado Maven</span><span class="sxs-lookup"><span data-stu-id="24e16-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="24e16-121">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="24e16-121">Create a Maven project</span></span>

1. <span data-ttu-id="24e16-122">Desde una sesión de terminal, o la línea de comandos en el entorno de desarrollo, cambiar la ubicación de toohello de directorios que desee toostore este proyecto.</span><span class="sxs-lookup"><span data-stu-id="24e16-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="24e16-123">Hola de uso `mvn` comando, que se instala con Maven, hello toogenerate scaffolding para proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e16-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="24e16-124">Si usa PowerShell, debe encerrar hello `-D` parámetros entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="24e16-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="24e16-125">Este comando crea un directorio con nombre de hello especificado por hello `artifactID` parámetro (**wordcountjava** en este ejemplo.) Este directorio contiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="24e16-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="24e16-126">`pom.xml`-Hola [modelo de objeto de proyecto (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) que contiene información y detalles de configuración utilizan proyectos de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="24e16-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="24e16-127">`src`-directorio de Hola que contiene la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="24e16-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="24e16-128">Eliminar hello `src/test/java/org/apache/hadoop/examples/apptest.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="24e16-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="24e16-129">No lo vamos a usar en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="24e16-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="24e16-130">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="24e16-130">Add dependencies</span></span>

1. <span data-ttu-id="24e16-131">Editar hello `pom.xml` de archivos y agregar Hola después de texto dentro de hello `<dependencies>` sección:</span><span class="sxs-lookup"><span data-stu-id="24e16-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="24e16-132">Esto define las bibliotecas requeridas (enumeradas en &lt;artifactId\>) de una versión específica (enumerada en &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="24e16-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="24e16-133">En tiempo de compilación, estas dependencias se descargan del repositorio de Maven Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="24e16-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="24e16-134">Puede usar hello [búsqueda de repositorio de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview más.</span><span class="sxs-lookup"><span data-stu-id="24e16-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="24e16-135">Hola `<scope>provided</scope>` indica Maven que estas dependencias no se deben empaquetar con la aplicación hello, como se proporcionan por clúster de HDInsight de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="24e16-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="24e16-136">versión de Hola utilizada debe coincidir con versión de Hola de Hadoop presente en el clúster.</span><span class="sxs-lookup"><span data-stu-id="24e16-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="24e16-137">Para obtener más información sobre las versiones, vea hello [versiones de componentes de HDInsight](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="24e16-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="24e16-138">Agregar Hola después toohello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="24e16-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="24e16-139">Este texto debe estar dentro de hello `<project>...</project>` en archivo hello; por ejemplo, entre las etiquetas `</dependencies>` y `</project>`.</span><span class="sxs-lookup"><span data-stu-id="24e16-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="24e16-140">primer complemento Hello configura hello [Maven tono complemento](http://maven.apache.org/plugins/maven-shade-plugin/), que es usado toobuild un uberjar (a veces denominado un fatjar), que contiene las dependencias requeridas por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="24e16-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="24e16-141">También se evita la duplicación de licencias en paquete jar de hello, que pueden causar problemas en algunos sistemas.</span><span class="sxs-lookup"><span data-stu-id="24e16-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="24e16-142">Hola segundo complemento configura versión de Java de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e16-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="24e16-143">HDInsight 3.4 y versiones anteriores utilizan Java 7.</span><span class="sxs-lookup"><span data-stu-id="24e16-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="24e16-144">HDInsight 3.5 y versiones posteriores usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="24e16-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="24e16-145">Guardar hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="24e16-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="24e16-146">Crear aplicación de hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="24e16-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="24e16-147">Vaya toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` Hola de directorio y el nombre `App.java` archivo demasiado`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="24e16-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="24e16-148">Abra hello `WordCount.java` un archivo en un editor de texto y reemplace el contenido de hello con hello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="24e16-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="24e16-149">Nombre del paquete de hello aviso es `org.apache.hadoop.examples` y es el nombre de la clase hello `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="24e16-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="24e16-150">Estos nombres se utilizan cuando se envía el trabajo de MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="24e16-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="24e16-151">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="24e16-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="24e16-152">Compilar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="24e16-152">Build hello application</span></span>

1. <span data-ttu-id="24e16-153">Cambiar toohello `wordcountjava` directory, si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="24e16-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="24e16-154">Usar hello siguiente comando toobuild un archivo JAR de archivos que contienen aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="24e16-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="24e16-155">Este comando limpia los artefactos de compilación anterior, descarga los dependencias que no hayan sido instaladas, y a continuación, compila y empaquetar la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e16-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="24e16-156">Una vez que el comando hello finaliza, hello `wordcountjava/target` directorio contiene un archivo denominado `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="24e16-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="24e16-157">Hola `wordcountjava-1.0-SNAPSHOT.jar` archivo es un uberjar, que contiene no solo el trabajo de WordCount hello, pero también requiere que las dependencias que Hola trabajo en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="24e16-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="24e16-158"><a id="upload"></a>Cargar archivo jar de Hola</span><span class="sxs-lookup"><span data-stu-id="24e16-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="24e16-159">Usar hello después comando tooupload archivo jar hello toohello HDInsight nodo principal:</span><span class="sxs-lookup"><span data-stu-id="24e16-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="24e16-160">Este comando copia los archivos de Hola desde el nodo principal de hello sistema local toohello.</span><span class="sxs-lookup"><span data-stu-id="24e16-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="24e16-161">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="24e16-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="24e16-162"><a name="run"></a>Ejecutar trabajo de MapReduce de hello en Hadoop</span><span class="sxs-lookup"><span data-stu-id="24e16-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="24e16-163">Conectar tooHDInsight mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="24e16-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="24e16-164">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="24e16-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="24e16-165">Desde la sesión de SSH de hello, utilice Hola tras la aplicación de comando toorun Hola MapReduce:</span><span class="sxs-lookup"><span data-stu-id="24e16-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="24e16-166">Este comando inicia Hola aplicación WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="24e16-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="24e16-167">archivo de entrada de Hello es `/example/data/gutenberg/davinci.txt`, y es el directorio de salida de hello `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="24e16-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="24e16-168">Archivo de entrada de Hola y de salida son toohello almacenado predeterminado almacenamiento Hola del clúster.</span><span class="sxs-lookup"><span data-stu-id="24e16-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="24e16-169">Cuando se completa el trabajo de hello, utilice Hola siguiendo los resultados del comando tooview hello:</span><span class="sxs-lookup"><span data-stu-id="24e16-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="24e16-170">Debería recibir una lista de palabras y los recuentos, con valores toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="24e16-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="24e16-171"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24e16-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="24e16-172">En este documento, ha aprendido cómo toodevelop un trabajo de MapReduce de Java.</span><span class="sxs-lookup"><span data-stu-id="24e16-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="24e16-173">Vea Hola después de documentos para otro toowork maneras con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="24e16-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="24e16-174">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="24e16-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="24e16-175">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="24e16-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="24e16-176">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="24e16-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="24e16-177">Para obtener más información, vea también hello [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="24e16-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

