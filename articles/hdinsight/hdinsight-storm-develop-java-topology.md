---
title: "Ejemplo de topología de Apache Storm en Java - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear topologías de Apache Storm en Java al crear una topología de recuento de palabras de ejemplo."
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
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="b71df-104">Crear una topología de Apache Storm en Java</span><span class="sxs-lookup"><span data-stu-id="b71df-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="b71df-105">Aprenda a crear una topología de Apache Storm basada en Java.</span><span class="sxs-lookup"><span data-stu-id="b71df-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="b71df-106">Vamos a crear una topología de Storm que implemente una aplicación de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="b71df-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="b71df-107">Para compilar y empaquetar el proyecto, usaremos Maven.</span><span class="sxs-lookup"><span data-stu-id="b71df-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="b71df-108">Después, aprende a definir la topología con el marco de trabajo Flux.</span><span class="sxs-lookup"><span data-stu-id="b71df-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="b71df-109">El marco de trabajo Flux está disponible en Storm 0.10.0 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="b71df-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="b71df-110">Storm 0.10.0 está disponible con HDInsight 3.3 y 3.4.</span><span class="sxs-lookup"><span data-stu-id="b71df-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="b71df-111">Después de completar los pasos descritos en este documento, puede implementar la topología en Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b71df-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="b71df-112">En [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount) encontrará una versión completa de los ejemplos de topologías de Storm creadas en este documento.</span><span class="sxs-lookup"><span data-stu-id="b71df-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b71df-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b71df-113">Prerequisites</span></span>

* [<span data-ttu-id="b71df-114">Kit de desarrolladores de Java (JDK) versión 7</span><span class="sxs-lookup"><span data-stu-id="b71df-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="b71df-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven es un sistema de compilación de proyectos para proyectos de Java.</span><span class="sxs-lookup"><span data-stu-id="b71df-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="b71df-116">Un editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="b71df-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="b71df-117">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="b71df-117">Configure environment variables</span></span>

<span data-ttu-id="b71df-118">Pueden establecer las siguientes variables de entorno al instalar Java y el JDK.</span><span class="sxs-lookup"><span data-stu-id="b71df-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="b71df-119">Sin embargo, debe comprobar que existen y que contienen los valores correctos para su sistema.</span><span class="sxs-lookup"><span data-stu-id="b71df-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="b71df-120">**JAVA_HOME**: debe apuntar al directorio donde está instalado Java Runtime Environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="b71df-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="b71df-121">Por ejemplo, en una distribución de Unix o Linux, debe tener un valor similar a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="b71df-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="b71df-122">En Windows, tendría un valor similar a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="b71df-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="b71df-123">**PATH** : debe contener las rutas de acceso siguientes:</span><span class="sxs-lookup"><span data-stu-id="b71df-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="b71df-124">**JAVA_HOME** (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="b71df-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="b71df-125">**JAVA_HOME\bin** (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="b71df-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="b71df-126">El directorio donde está instalado Maven</span><span class="sxs-lookup"><span data-stu-id="b71df-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="b71df-127">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="b71df-127">Create a Maven project</span></span>

<span data-ttu-id="b71df-128">En la línea de comandos, use el siguiente comando para crear un proyecto de Maven llamado **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="b71df-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="b71df-129">Si va a usar PowerShell, deberá poner comillas dobles alrededor de los parámetros `-D`.</span><span class="sxs-lookup"><span data-stu-id="b71df-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="b71df-130">Este comando crea un directorio denominado `WordCount` en la ubicación actual, que contiene un proyecto de Maven básico.</span><span class="sxs-lookup"><span data-stu-id="b71df-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="b71df-131">El directorio `WordCount` contiene los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b71df-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="b71df-132">`pom.xml`: Contiene la configuración del proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="b71df-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="b71df-133">`src\main\java\com\microsoft\example`: Contiene el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b71df-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="b71df-134">`src\test\java\com\microsoft\example`: Contiene pruebas para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b71df-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="b71df-135">Eliminar el código de ejemplo generado</span><span class="sxs-lookup"><span data-stu-id="b71df-135">Remove the generated example code</span></span>

<span data-ttu-id="b71df-136">Elimine la prueba generada y los archivos de aplicación:</span><span class="sxs-lookup"><span data-stu-id="b71df-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="b71df-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="b71df-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="b71df-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="b71df-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="b71df-139">Agregar repositorios de Maven</span><span class="sxs-lookup"><span data-stu-id="b71df-139">Add Maven repositories</span></span>

<span data-ttu-id="b71df-140">HDInsight se basa en Hortonworks Data Platform (HDP), por lo que se recomienda usar el repositorio de Hortonworks para descargar las dependencias correspondientes a los proyectos de Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="b71df-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="b71df-141">En el archivo __pom.xml__, agregue el siguiente texto XML después de la línea `<url>http://maven.apache.org</url>`:</span><span class="sxs-lookup"><span data-stu-id="b71df-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="b71df-142">Agregar propiedades</span><span class="sxs-lookup"><span data-stu-id="b71df-142">Add properties</span></span>

<span data-ttu-id="b71df-143">Maven permite definir los valores de nivel de proyecto llamados propiedades.</span><span class="sxs-lookup"><span data-stu-id="b71df-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="b71df-144">En __pom.xml__, agregue el siguiente texto después de la línea `</repositories>`:</span><span class="sxs-lookup"><span data-stu-id="b71df-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="b71df-145">Ahora puede usar este valor en otras secciones de `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="b71df-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="b71df-146">Por ejemplo, al especificar la versión de los componentes de Storm, puede usar `${storm.version}` en lugar de codificar un valor de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="b71df-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="b71df-147">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="b71df-147">Add dependencies</span></span>

<span data-ttu-id="b71df-148">Agregue una dependencia para componentes de Storm.</span><span class="sxs-lookup"><span data-stu-id="b71df-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="b71df-149">Abra el archivo `pom.xml` y agregue el código siguiente en la sección `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="b71df-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="b71df-150">En tiempo de compilación, Maven usa esta información para buscar `storm-core` en el repositorio de Maven.</span><span class="sxs-lookup"><span data-stu-id="b71df-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="b71df-151">Busca primero en el repositorio del equipo local.</span><span class="sxs-lookup"><span data-stu-id="b71df-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="b71df-152">Si los archivos no están allí, Maven los descarga desde el repositorio de Maven público y los almacena en el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="b71df-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b71df-153">Observe la línea `<scope>provided</scope>` en esta sección.</span><span class="sxs-lookup"><span data-stu-id="b71df-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="b71df-154">Esta opción indica a Maven que excluya **storm-core** de los archivos JAR creados, ya que el sistema lo proporciona.</span><span class="sxs-lookup"><span data-stu-id="b71df-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="b71df-155">Configuración de compilación</span><span class="sxs-lookup"><span data-stu-id="b71df-155">Build configuration</span></span>

<span data-ttu-id="b71df-156">Los complementos de Maven permiten personalizar las fases de compilación del proyecto,</span><span class="sxs-lookup"><span data-stu-id="b71df-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="b71df-157">por ejemplo, cómo se compila el proyecto o cómo este se empaqueta en un archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="b71df-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="b71df-158">Abra el archivo `pom.xml` y agregue el código siguiente directamente encima de la línea `</project>`.</span><span class="sxs-lookup"><span data-stu-id="b71df-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="b71df-159">Esta sección se usa para agregar complementos, recursos y otras opciones de configuración de compilación.</span><span class="sxs-lookup"><span data-stu-id="b71df-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="b71df-160">Para obtener una referencia completa del archivo **pom.xml**, consulte [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="b71df-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="b71df-161">Agregar complementos</span><span class="sxs-lookup"><span data-stu-id="b71df-161">Add plug-ins</span></span>

<span data-ttu-id="b71df-162">En el caso de las topologías de Apache Storm implementadas en Java, el [Complemento Exec Maven](http://www.mojohaus.org/exec-maven-plugin/) es útil porque le permite ejecutar fácilmente la topología de manera local en su entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b71df-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="b71df-163">Agregue lo siguiente a la sección `<plugins>` del archivo `pom.xml` para incluir el complemento Exec Maven:</span><span class="sxs-lookup"><span data-stu-id="b71df-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

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

<span data-ttu-id="b71df-164">Otro complemento útil es el [Complemento Apache Maven Compiler](http://maven.apache.org/plugins/maven-compiler-plugin/), que se usa para cambiar las opciones de compilación.</span><span class="sxs-lookup"><span data-stu-id="b71df-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="b71df-165">Se cambia la versión de Java que usa Maven para el origen y destino de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b71df-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="b71df-166">Para HDInsight __3.4 o una versión anterior__, establezca la versión de origen y destino de Java en __1.7__.</span><span class="sxs-lookup"><span data-stu-id="b71df-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="b71df-167">Para HDInsight __3.5__, establezca la versión de origen y destino de Java en __1.8__.</span><span class="sxs-lookup"><span data-stu-id="b71df-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="b71df-168">Agregue el siguiente texto en la sección `<plugins>` del archivo `pom.xml` para incluir el complemento Apache Maven Compiler.</span><span class="sxs-lookup"><span data-stu-id="b71df-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="b71df-169">Este ejemplo especifica 1.8, por lo que la versión de HDInsight de destino es 3.5.</span><span class="sxs-lookup"><span data-stu-id="b71df-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="b71df-170">Configure resources</span><span class="sxs-lookup"><span data-stu-id="b71df-170">Configure resources</span></span>

<span data-ttu-id="b71df-171">Gracias a la sección de recursos, podrá incluir recursos no basados en códigos, como los archivos de configuración que necesitan los componentes de la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="b71df-172">En este ejemplo, agregue el texto siguiente en la sección `<resources>` del archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="b71df-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="b71df-173">Este ejemplo agrega el directorio de recursos en la raíz del proyecto (`${basedir}`) como una ubicación que contiene recursos e incluye el archivo denominado `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="b71df-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="b71df-174">Este archivo se utiliza para configurar la información que registra la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="b71df-175">Creación de la topología</span><span class="sxs-lookup"><span data-stu-id="b71df-175">Create the topology</span></span>

<span data-ttu-id="b71df-176">Una topología de Apache Storm basada en Java consta de tres componentes que debe crear (o hacer referencia) como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="b71df-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="b71df-177">**Spouts**: lee datos de orígenes externos y emite flujos de datos a la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="b71df-178">**Bolts**: realiza el procesamiento en flujos que emite spouts u otros bolts, y emite uno o varios flujos.</span><span class="sxs-lookup"><span data-stu-id="b71df-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="b71df-179">**Topology**: define cómo se organizan los spouts y bolts, y proporciona el punto de entrada de la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="b71df-180">Creación del spout</span><span class="sxs-lookup"><span data-stu-id="b71df-180">Create the spout</span></span>

<span data-ttu-id="b71df-181">Para reducir los requisitos de la configuración de los orígenes de datos externos, el spout siguiente simplemente emite frases aleatorias.</span><span class="sxs-lookup"><span data-stu-id="b71df-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="b71df-182">Se trata de una versión modificada de un spout que se proporciona con los [ejemplos de Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="b71df-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="b71df-183">Para ver un ejemplo de un spout que lee desde un origen de datos externos, consulte uno de los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="b71df-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="b71df-184">[TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): un spout de ejemplo que lee desde Twitter.</span><span class="sxs-lookup"><span data-stu-id="b71df-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="b71df-185">[Storm Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): un spout que lee desde Kafka.</span><span class="sxs-lookup"><span data-stu-id="b71df-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="b71df-186">Para spout, cree un archivo llamado `RandomSentenceSpout.java` en el directorio `src\main\java\com\microsoft\example` y use el siguiente código Java como contenido:</span><span class="sxs-lookup"><span data-stu-id="b71df-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

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
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
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

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="b71df-187">Aunque esta topología solo usa un spout, otras pueden tener varios que alimenten datos desde orígenes distintos en la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="b71df-188">Creación de los bolts</span><span class="sxs-lookup"><span data-stu-id="b71df-188">Create the bolts</span></span>

<span data-ttu-id="b71df-189">Los bolts controlan el procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="b71df-189">Bolts handle the data processing.</span></span> <span data-ttu-id="b71df-190">Esta topología utiliza dos bolts:</span><span class="sxs-lookup"><span data-stu-id="b71df-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="b71df-191">**SplitSentence**: divide las frases que emite **RandomSentenceSpout** en palabras individuales.</span><span class="sxs-lookup"><span data-stu-id="b71df-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="b71df-192">**WordCount**: cuenta cuántas veces se ha repetido cada palabra.</span><span class="sxs-lookup"><span data-stu-id="b71df-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="b71df-193">Los bolts pueden hacer cualquier cosa; por ejemplo, cálculo, persistencia o hablar con componentes externos.</span><span class="sxs-lookup"><span data-stu-id="b71df-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="b71df-194">Cree dos nuevos archivos, `SplitSentence.java` y `WordCount.java` en el directorio `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="b71df-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="b71df-195">Use el siguiente texto como contenido para los archivos:</span><span class="sxs-lookup"><span data-stu-id="b71df-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="b71df-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="b71df-196">SplitSentence</span></span>

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

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
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

#### <a name="wordcount"></a><span data-ttu-id="b71df-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="b71df-197">WordCount</span></span>

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
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
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
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
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

### <a name="define-the-topology"></a><span data-ttu-id="b71df-198">Definición de la topología</span><span class="sxs-lookup"><span data-stu-id="b71df-198">Define the topology</span></span>

<span data-ttu-id="b71df-199">La topología vincula los spouts y los bolts juntos en un gráfico, que define cómo fluyen los datos entre los componentes.</span><span class="sxs-lookup"><span data-stu-id="b71df-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="b71df-200">También proporciona sugerencias de paralelismos que utiliza Storm al crear instancias de los componentes dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="b71df-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="b71df-201">La siguiente imagen es un diagrama básico del gráfico de componentes para esta topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![diagrama que muestra la disposición de los spouts y bolts](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="b71df-203">Para implementar la topología, cree un archivo llamado `WordCountTopology.java` en el directorio `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="b71df-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="b71df-204">Use el siguiente código Java como contenido del archivo:</span><span class="sxs-lookup"><span data-stu-id="b71df-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="b71df-205">registro</span><span class="sxs-lookup"><span data-stu-id="b71df-205">Configure logging</span></span>

<span data-ttu-id="b71df-206">Storm utiliza Apache Log4j para registrar información.</span><span class="sxs-lookup"><span data-stu-id="b71df-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="b71df-207">Si no configura el registro, la topología emite información de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b71df-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="b71df-208">Para controlar lo que se registra, cree un archivo denominado `log4j2.xml` en el directorio `resources`.</span><span class="sxs-lookup"><span data-stu-id="b71df-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="b71df-209">Use el siguiente XML como contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="b71df-209">Use the following XML as the contents of the file.</span></span>

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

<span data-ttu-id="b71df-210">Este XML configura un nuevo registrador para la clase `com.microsoft.example`, que incluye los componentes de esta topología de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b71df-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="b71df-211">El nivel está establecido para realizar un seguimiento de este registrador, que captura cualquier información de registro que generen los componentes de esta topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="b71df-212">La sección `<Root level="error">` configura el nivel de registro raíz (todo lo que no esté en `com.microsoft.example`) para registrar solo la información de los errores.</span><span class="sxs-lookup"><span data-stu-id="b71df-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="b71df-213">Para obtener más información sobre la configuración de registro de Log4j, consulte [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="b71df-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="b71df-214">La versión 0.10.0 y superiores de Storm utilizan Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="b71df-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="b71df-215">Las versiones anteriores de Storm usaban Log4j 1.x, que empleaba otro formato de configuración del registro.</span><span class="sxs-lookup"><span data-stu-id="b71df-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="b71df-216">Para obtener información sobre la configuración anterior, consulte [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="b71df-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="b71df-217">Prueba de la topología de manera local</span><span class="sxs-lookup"><span data-stu-id="b71df-217">Test the topology locally</span></span>

<span data-ttu-id="b71df-218">Después de guardar los archivos, use el comando siguiente para probar localmente la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="b71df-219">Mientras se ejecuta, la topología muestra información de inicio.</span><span class="sxs-lookup"><span data-stu-id="b71df-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="b71df-220">El siguiente texto es un ejemplo de la salida del recuento de palabras:</span><span class="sxs-lookup"><span data-stu-id="b71df-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="b71df-221">Este registro de ejemplo indica que la palabra «and» se ha emitido 113 veces.</span><span class="sxs-lookup"><span data-stu-id="b71df-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="b71df-222">El recuento continúa aumentando mientras se ejecute la topología porque el spout emite continuamente las mismas frases.</span><span class="sxs-lookup"><span data-stu-id="b71df-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="b71df-223">Hay un intervalo de 5 segundos entre la emisión de las palabras y los recuentos.</span><span class="sxs-lookup"><span data-stu-id="b71df-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="b71df-224">El componente **WordCount** está configurado para emitir la información solo cuando llegue una tupla de marca.</span><span class="sxs-lookup"><span data-stu-id="b71df-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="b71df-225">Solicita que esas tuplas se entreguen solo cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="b71df-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="b71df-226">Conversión de la topología a Flux</span><span class="sxs-lookup"><span data-stu-id="b71df-226">Convert the topology to Flux</span></span>

<span data-ttu-id="b71df-227">Flux es un nuevo marco de trabajo disponible con Storm 0.10.0 y versiones superiores que permite separar la configuración de la implementación.</span><span class="sxs-lookup"><span data-stu-id="b71df-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="b71df-228">Los componentes se siguen definiendo en Java, pero la topología se define con un archivo YAML.</span><span class="sxs-lookup"><span data-stu-id="b71df-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="b71df-229">Puede empaquetar una definición de topología predeterminada con el proyecto, o bien usar un archivo independiente al enviar la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="b71df-230">Al enviar la topología a Storm, puede usar variables de entorno o archivos de configuración para rellenar los valores de la definición de la topología de YAML.</span><span class="sxs-lookup"><span data-stu-id="b71df-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="b71df-231">El archivo YAML define los componentes que se usarán para la topología y el flujo de datos entre ellos.</span><span class="sxs-lookup"><span data-stu-id="b71df-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="b71df-232">Puede incluir un archivo YAML como parte del archivo jar o puede usar un archivo YAML externo.</span><span class="sxs-lookup"><span data-stu-id="b71df-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="b71df-233">Para más información sobre Flux, vea este documento sobre el [marco de trabajo de Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b71df-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="b71df-234">Debido a un [error (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) con Storm 1.0.1, es posible que deba instalar un [entorno de desarrollo de Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) para ejecutar topologías de un flujo de forma local.</span><span class="sxs-lookup"><span data-stu-id="b71df-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="b71df-235">Saque el archivo `WordCountTopology.java` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="b71df-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="b71df-236">Anteriormente, este archivo definía la topología, pero no es necesario con Flux.</span><span class="sxs-lookup"><span data-stu-id="b71df-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="b71df-237">En el directorio `resources`, cree un archivo denominado `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="b71df-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="b71df-238">Use el siguiente texto como contenido de este archivo.</span><span class="sxs-lookup"><span data-stu-id="b71df-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
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
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="b71df-239">Realice los siguientes cambios en el archivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="b71df-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="b71df-240">Agregue la siguiente dependencia nueva en la sección `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="b71df-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="b71df-241">Agregue el complemento siguiente a la sección `<plugins>` .</span><span class="sxs-lookup"><span data-stu-id="b71df-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="b71df-242">Este complemento administra la creación de un paquete (archivo jar) para el proyecto y aplica algunas transformaciones específicas a Flux cuando se crea el paquete.</span><span class="sxs-lookup"><span data-stu-id="b71df-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
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
                    <!-- We're using Flux, so refer to it as main -->
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

   * <span data-ttu-id="b71df-243">En la sección **exec-maven-plugin**`<configuration>`, cambie el valor de `<mainClass>` por `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="b71df-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="b71df-244">Esta opción permite a Flux controlar la ejecución de la topología localmente en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b71df-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="b71df-245">En la sección `<resources>`, agregue lo siguiente a `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="b71df-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="b71df-246">Este XML incluye el archivo YAML que define la topología como parte del proyecto.</span><span class="sxs-lookup"><span data-stu-id="b71df-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="b71df-247">Prueba local de la topología</span><span class="sxs-lookup"><span data-stu-id="b71df-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="b71df-248">Use lo siguiente para compilar y ejecutar la topología de Flux con Maven:</span><span class="sxs-lookup"><span data-stu-id="b71df-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="b71df-249">Si usa PowerShell, utilice el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b71df-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="b71df-250">Este comando produce un error si la topología usa bits de Storm 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="b71df-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="b71df-251">Este error se debe a [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="b71df-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="b71df-252">En su lugar, [instale Storm en su entorno de desarrollo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) y emplee la siguiente información.</span><span class="sxs-lookup"><span data-stu-id="b71df-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="b71df-253">Si tiene [instalado Storm en el entorno de desarrollo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), puede usar en su lugar los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b71df-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="b71df-254">El parámetro `--local` ejecuta la topología en modo local en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b71df-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="b71df-255">El parámetro `-R /topology.yaml` usa el recurso de archivo `topology.yaml` del archivo jar para definir la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="b71df-256">Mientras se ejecuta, la topología muestra información de inicio.</span><span class="sxs-lookup"><span data-stu-id="b71df-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="b71df-257">El siguiente texto es un ejemplo de la salida:</span><span class="sxs-lookup"><span data-stu-id="b71df-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="b71df-258">Hay un retraso de 10 segundos entre los distintos lotes de la información registrada.</span><span class="sxs-lookup"><span data-stu-id="b71df-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="b71df-259">Realice una copia del archivo `topology.yaml` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="b71df-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="b71df-260">Asigne el nombre `newtopology.yaml` al archivo nuevo.</span><span class="sxs-lookup"><span data-stu-id="b71df-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="b71df-261">En el archivo `newtopology.yaml`, busque la siguiente sección y cambie el valor de `10` por `5`.</span><span class="sxs-lookup"><span data-stu-id="b71df-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="b71df-262">Esta modificación altera el intervalo entre la emisión de lotes de recuentos de palabras de 10 segundos a 5.</span><span class="sxs-lookup"><span data-stu-id="b71df-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="b71df-263">También puede hacer lo siguiente si tiene Storm en el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="b71df-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="b71df-264">Cambie `/path/to/newtopology.yaml` por la ruta de acceso al archivo newtopology.yaml que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="b71df-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="b71df-265">Este comando usa newtopology.yaml como definición de la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="b71df-266">Puesto que no se incluyó el parámetro `compile`, Maven usa la versión del proyecto compilada en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="b71df-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="b71df-267">Una vez iniciada la topología, observará que el tiempo entre los lotes emitidos ha cambiado y ahora refleja el valor de newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="b71df-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="b71df-268">Esto demuestra que puede cambiar la configuración a través de un archivo YAML sin tener que volver a compilar la topología.</span><span class="sxs-lookup"><span data-stu-id="b71df-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="b71df-269">Para más información sobre estas y otras características del marco de trabajo Flux, consulte [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b71df-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="b71df-270">Trident</span><span class="sxs-lookup"><span data-stu-id="b71df-270">Trident</span></span>

<span data-ttu-id="b71df-271">Trident es una abstracción de alto nivel que ofrece Storm.</span><span class="sxs-lookup"><span data-stu-id="b71df-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="b71df-272">Admite el procesamiento con estado.</span><span class="sxs-lookup"><span data-stu-id="b71df-272">It supports stateful processing.</span></span> <span data-ttu-id="b71df-273">La principal ventaja de Trident es que puede garantizar que todos los mensajes que entran en la topología se procesan una sola vez.</span><span class="sxs-lookup"><span data-stu-id="b71df-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="b71df-274">Si no se usa Trident, la topología solo puede garantizar que los mensajes se procesan al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="b71df-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="b71df-275">También hay otras diferencias, como los componentes integrados que se pueden usar en lugar de crear bolts.</span><span class="sxs-lookup"><span data-stu-id="b71df-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="b71df-276">De hecho, los bolts se reemplazan por componentes menos genéricos, como filtros, proyecciones y funciones.</span><span class="sxs-lookup"><span data-stu-id="b71df-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="b71df-277">Las aplicaciones de Trident se pueden crear mediante proyectos de Maven.</span><span class="sxs-lookup"><span data-stu-id="b71df-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="b71df-278">Siga los mismos pasos básicos que se mostraron anteriormente en este artículo; lo único diferente es el código.</span><span class="sxs-lookup"><span data-stu-id="b71df-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="b71df-279">Actualmente, tampoco puede usarse Trident con el marco de trabajo Flux.</span><span class="sxs-lookup"><span data-stu-id="b71df-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="b71df-280">Para obtener más información sobre Trident, consulte [Información general sobre la API de Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="b71df-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="b71df-281">Para ver un ejemplo de una aplicación de Trident, consulte [Tendencias de Twitter con Apache Storm en HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="b71df-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b71df-282">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b71df-282">Next Steps</span></span>

<span data-ttu-id="b71df-283">Ha aprendido a crear una topología de Storm con Java.</span><span class="sxs-lookup"><span data-stu-id="b71df-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="b71df-284">Ahora obtenga información sobre:</span><span class="sxs-lookup"><span data-stu-id="b71df-284">Now learn how to:</span></span>

* [<span data-ttu-id="b71df-285">Implementación y administración de topologías de Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b71df-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="b71df-286">Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b71df-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="b71df-287">Puede encontrar más topologías de ejemplo de Storm en [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b71df-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

