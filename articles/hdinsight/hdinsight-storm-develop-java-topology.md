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
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="852ca-104">Crear una topología de Apache Storm en Java</span><span class="sxs-lookup"><span data-stu-id="852ca-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="852ca-105">Obtenga información acerca de cómo toocreate una topología basada en Java para Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="852ca-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="852ca-106">Vamos a crear una topología de Storm que implemente una aplicación de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="852ca-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="852ca-107">Utilice Maven toobuild y paquete hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="852ca-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="852ca-108">A continuación, aprenderá cómo toodefine Hola topología utilizando Hola framework de un flujo.</span><span class="sxs-lookup"><span data-stu-id="852ca-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="852ca-109">marco de trabajo de un flujo de Hello está disponible en Storm 0.10.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="852ca-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="852ca-110">Storm 0.10.0 está disponible con HDInsight 3.3 y 3.4.</span><span class="sxs-lookup"><span data-stu-id="852ca-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="852ca-111">Después de completar los pasos de hello en este documento, puede implementar Hola topología tooApache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="852ca-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="852ca-112">Una versión completa de ejemplos de topología de Storm Hola creado en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="852ca-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="852ca-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="852ca-113">Prerequisites</span></span>

* [<span data-ttu-id="852ca-114">Kit de desarrolladores de Java (JDK) versión 7</span><span class="sxs-lookup"><span data-stu-id="852ca-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="852ca-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven es un sistema de compilación de proyectos para proyectos de Java.</span><span class="sxs-lookup"><span data-stu-id="852ca-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="852ca-116">Un editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="852ca-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="852ca-117">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="852ca-117">Configure environment variables</span></span>

<span data-ttu-id="852ca-118">Hello siguientes variables de entorno pueden establecerse al instalar hello JDK y Java.</span><span class="sxs-lookup"><span data-stu-id="852ca-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="852ca-119">Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.</span><span class="sxs-lookup"><span data-stu-id="852ca-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="852ca-120">**JAVA_HOME** -debe apuntar el directorio toohello donde está instalado Hola de Java runtime environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="852ca-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="852ca-121">Por ejemplo, en una distribución de Unix o Linux, debe tener un valor similar demasiado`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="852ca-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="852ca-122">En Windows, tendría un valor similar demasiado`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="852ca-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="852ca-123">**Ruta de acceso** -debe contener Hola siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="852ca-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="852ca-124">**JAVA_HOME** (o ruta de acceso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="852ca-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="852ca-125">**JAVA_HOME\bin** (o ruta de acceso equivalente hello)</span><span class="sxs-lookup"><span data-stu-id="852ca-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="852ca-126">directorio de Hola donde está instalado Maven</span><span class="sxs-lookup"><span data-stu-id="852ca-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="852ca-127">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="852ca-127">Create a Maven project</span></span>

<span data-ttu-id="852ca-128">Desde la línea de comandos de hello, use Hola siguiente comando toocreate un proyecto de Maven **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="852ca-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="852ca-129">Si va a usar PowerShell, deberá poner comillas dobles alrededor de los parámetros `-D`.</span><span class="sxs-lookup"><span data-stu-id="852ca-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="852ca-130">Este comando crea un directorio denominado `WordCount` en la ubicación actual de hello, que contiene un proyecto básico de Maven.</span><span class="sxs-lookup"><span data-stu-id="852ca-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="852ca-131">Hola `WordCount` directorio contiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="852ca-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="852ca-132">`pom.xml`: Contiene la configuración para proyectos de Maven Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="852ca-133">`src\main\java\com\microsoft\example`: Contiene el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="852ca-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="852ca-134">`src\test\java\com\microsoft\example`: Contiene pruebas para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="852ca-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="852ca-135">Quitar el código de ejemplo de Hola generado</span><span class="sxs-lookup"><span data-stu-id="852ca-135">Remove hello generated example code</span></span>

<span data-ttu-id="852ca-136">Eliminar pruebas Hola generado y archivos de la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="852ca-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="852ca-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="852ca-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="852ca-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="852ca-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="852ca-139">Agregar repositorios de Maven</span><span class="sxs-lookup"><span data-stu-id="852ca-139">Add Maven repositories</span></span>

<span data-ttu-id="852ca-140">HDInsight se basa en hello Hortonworks Data Platform (HDP), por lo que se recomienda utilizar las dependencias de hello Hortonworks repositorio toodownload para los proyectos de Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="852ca-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="852ca-141">Hola __pom.xml__ , agregue Hola continuación de XML después de hello `<url>http://maven.apache.org</url>` línea:</span><span class="sxs-lookup"><span data-stu-id="852ca-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="852ca-142">Agregar propiedades</span><span class="sxs-lookup"><span data-stu-id="852ca-142">Add properties</span></span>

<span data-ttu-id="852ca-143">Maven permite valores de nivel de proyecto de toodefine denominados propiedades.</span><span class="sxs-lookup"><span data-stu-id="852ca-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="852ca-144">Hola __pom.xml__, agregar Hola después texto después de hello `</repositories>` línea:</span><span class="sxs-lookup"><span data-stu-id="852ca-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="852ca-145">Ahora puede usar este valor en otras secciones de hello `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="852ca-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="852ca-146">Por ejemplo, al especificar la versión de Hola de componentes de Storm, puede utilizar `${storm.version}` en lugar de codificar de forma rígida un valor.</span><span class="sxs-lookup"><span data-stu-id="852ca-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="852ca-147">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="852ca-147">Add dependencies</span></span>

<span data-ttu-id="852ca-148">Agregue una dependencia para componentes de Storm.</span><span class="sxs-lookup"><span data-stu-id="852ca-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="852ca-149">Abra hello `pom.xml` de archivos y agregar Hola después el código de hello `<dependencies>` sección:</span><span class="sxs-lookup"><span data-stu-id="852ca-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="852ca-150">En tiempo de compilación, Maven Utilice esta información toolook `storm-core` en el repositorio de Maven Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="852ca-151">Primero busca en el repositorio de hello en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="852ca-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="852ca-152">Si archivos hello no existe, experto en descarga de repositorio público de Maven de Hola y almacenarlos en el repositorio local de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="852ca-153">Hola aviso `<scope>provided</scope>` línea en esta sección.</span><span class="sxs-lookup"><span data-stu-id="852ca-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="852ca-154">Esta configuración le comunica Maven tooexclude **aluvión de núcleo** de ningún archivo JAR que se crea, dado que se proporciona al sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="852ca-155">Configuración de compilación</span><span class="sxs-lookup"><span data-stu-id="852ca-155">Build configuration</span></span>

<span data-ttu-id="852ca-156">Complementos de maven le permiten fases de compilación de hello toocustomize del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="852ca-157">Por ejemplo, cómo se compila el proyecto de Hola o cómo toopackage en un archivo JAR.</span><span class="sxs-lookup"><span data-stu-id="852ca-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="852ca-158">Abra hello `pom.xml` de archivos y agregar Hola después el código directamente encima de hello `</project>` línea.</span><span class="sxs-lookup"><span data-stu-id="852ca-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="852ca-159">Esta sección es tooadd usa complementos, los recursos y otras opciones de configuración de compilación.</span><span class="sxs-lookup"><span data-stu-id="852ca-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="852ca-160">Para obtener una referencia completa de hello **pom.xml** de archivos, consulte [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="852ca-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="852ca-161">Agregar complementos</span><span class="sxs-lookup"><span data-stu-id="852ca-161">Add plug-ins</span></span>

<span data-ttu-id="852ca-162">Para las topologías de Apache Storm implementadas en Java, Hola [Exec Maven complemento](http://www.mojohaus.org/exec-maven-plugin/) es útil porque permite tooeasily ejecuta topología Hola localmente en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="852ca-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="852ca-163">Agregar Hola después toohello `<plugins>` sección de hello `pom.xml` archivo tooinclude Hola Exec Maven complemento:</span><span class="sxs-lookup"><span data-stu-id="852ca-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

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

<span data-ttu-id="852ca-164">Otro útil es complemento hello [Apache Maven compilador complemento](http://maven.apache.org/plugins/maven-compiler-plugin/), que es usado toochange opciones de compilación.</span><span class="sxs-lookup"><span data-stu-id="852ca-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="852ca-165">cambios de Hola Hola versión de Java que Maven se usa para el origen de Hola y de destino para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="852ca-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="852ca-166">Para HDInsight __3.4 o una versión anterior__, establezca Hola origen y destino too__1.7__ de versión de Java.</span><span class="sxs-lookup"><span data-stu-id="852ca-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="852ca-167">Para HDInsight __3.5__, establezca Hola origen y destino too__1.8__ de versión de Java.</span><span class="sxs-lookup"><span data-stu-id="852ca-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="852ca-168">Agregar Hola después texto Hola `<plugins>` sección de hello `pom.xml` tooinclude Hola Apache Maven compilador complemento de archivos.</span><span class="sxs-lookup"><span data-stu-id="852ca-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="852ca-169">Este ejemplo especifica 1.8, por lo que la versión de HDInsight de destino de hello es 3.5.</span><span class="sxs-lookup"><span data-stu-id="852ca-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="852ca-170">Configure resources</span><span class="sxs-lookup"><span data-stu-id="852ca-170">Configure resources</span></span>

<span data-ttu-id="852ca-171">sección de recursos de Hello permite tooinclude recursos de código como archivos de configuración necesarios para componentes de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="852ca-172">En este ejemplo, agregar Hola después texto Hola `<resources>` sección de hello ' archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="852ca-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="852ca-173">En este ejemplo agrega el directorio de recursos de hello en raíz de Hola de proyecto de hello (`${basedir}`) como una ubicación que contiene recursos e incluye el archivo hello denominado `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="852ca-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="852ca-174">Este archivo es tooconfigure usado topología Hola registra la información.</span><span class="sxs-lookup"><span data-stu-id="852ca-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="852ca-175">Crear topología de Hola</span><span class="sxs-lookup"><span data-stu-id="852ca-175">Create hello topology</span></span>

<span data-ttu-id="852ca-176">Una topología de Apache Storm basada en Java consta de tres componentes que debe crear (o hacer referencia) como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="852ca-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="852ca-177">**Spouts**: lee los orígenes de datos desde externo y emite flujos de datos en la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="852ca-178">**Bolts**: realiza el procesamiento en flujos que emite spouts u otros bolts, y emite uno o varios flujos.</span><span class="sxs-lookup"><span data-stu-id="852ca-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="852ca-179">**Topología**: define el modo spouts hello y tornillos se organizan y proporciona el punto de entrada de hello para la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="852ca-180">Crear pitorro Hola</span><span class="sxs-lookup"><span data-stu-id="852ca-180">Create hello spout</span></span>

<span data-ttu-id="852ca-181">requisitos de tooreduce para configurar orígenes de datos externos, Hola siguiendo pitorro simplemente emite frases aleatorias.</span><span class="sxs-lookup"><span data-stu-id="852ca-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="852ca-182">Es una versión modificada de un pitorro que se proporciona con hello [ejemplos de Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="852ca-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="852ca-183">Para obtener un ejemplo de un pitorro que lee de un origen de datos externo, consulte uno de hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="852ca-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="852ca-184">[TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): un spout de ejemplo que lee desde Twitter.</span><span class="sxs-lookup"><span data-stu-id="852ca-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="852ca-185">[Storm Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): un spout que lee desde Kafka.</span><span class="sxs-lookup"><span data-stu-id="852ca-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="852ca-186">Para pitorro hello, cree un archivo denominado `RandomSentenceSpout.java` en hello `src\main\java\com\microsoft\example` Hola directorio y use después el código Java como contenido de hello:</span><span class="sxs-lookup"><span data-stu-id="852ca-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

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
> <span data-ttu-id="852ca-187">Aunque esta topología usa sola pitorro, otros usuarios pueden tener varios que introducir datos de orígenes diferentes en la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="852ca-188">Crear Hola tornillos</span><span class="sxs-lookup"><span data-stu-id="852ca-188">Create hello bolts</span></span>

<span data-ttu-id="852ca-189">Tornillos controlen el procesamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="852ca-190">Esta topología utiliza dos bolts:</span><span class="sxs-lookup"><span data-stu-id="852ca-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="852ca-191">**SplitSentence**: divide las frases de hello emitidas por **RandomSentenceSpout** en palabras individuales.</span><span class="sxs-lookup"><span data-stu-id="852ca-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="852ca-192">**WordCount**: cuenta cuántas veces se ha repetido cada palabra.</span><span class="sxs-lookup"><span data-stu-id="852ca-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="852ca-193">Tornillos pueden hacer cualquier cosa, por ejemplo, cálculo, persistencia o hablar tooexternal componentes.</span><span class="sxs-lookup"><span data-stu-id="852ca-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="852ca-194">Cree dos nuevos archivos, `SplitSentence.java` y `WordCount.java` en hello `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="852ca-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="852ca-195">Usar hello después de texto como contenido de Hola para archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="852ca-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="852ca-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="852ca-196">SplitSentence</span></span>

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

#### <a name="wordcount"></a><span data-ttu-id="852ca-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="852ca-197">WordCount</span></span>

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

### <a name="define-hello-topology"></a><span data-ttu-id="852ca-198">Definir la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="852ca-198">Define hello topology</span></span>

<span data-ttu-id="852ca-199">topología de Hello une spouts hello y los tornillos juntos en un gráfico, que define cómo fluyen los datos entre los componentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="852ca-200">También proporciona sugerencias de paralelismo que Storm utiliza al crear instancias de componentes de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="852ca-201">Hello imagen siguiente es un diagrama básico de gráfico de Hola de componentes para esta topología.</span><span class="sxs-lookup"><span data-stu-id="852ca-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![Hola de diagrama que muestra spouts y los tornillos de organización](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="852ca-203">tooimplement Hola topología, cree un archivo denominado `WordCountTopology.java` en hello `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="852ca-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="852ca-204">Usar hello después el código Java como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="852ca-204">Use hello following Java code as hello contents of hello file:</span></span>

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

### <a name="configure-logging"></a><span data-ttu-id="852ca-205">registro</span><span class="sxs-lookup"><span data-stu-id="852ca-205">Configure logging</span></span>

<span data-ttu-id="852ca-206">Storm utiliza Apache Log4j toolog información.</span><span class="sxs-lookup"><span data-stu-id="852ca-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="852ca-207">Si no configura el registro, la topología de hello emite información de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="852ca-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="852ca-208">toocontrol lo que se registra, cree un archivo denominado `log4j2.xml` en hello `resources` directory.</span><span class="sxs-lookup"><span data-stu-id="852ca-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="852ca-209">Usar hello continuación de XML como contenido de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="852ca-209">Use hello following XML as hello contents of hello file.</span></span>

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

<span data-ttu-id="852ca-210">Este código XML configura un nuevo registrador para hello `com.microsoft.example` (clase), que incluye componentes de hello en esta topología de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="852ca-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="852ca-211">nivel de Hola se establece tootrace para este registrador, que captura la información de registro de emitidos por componentes en esta topología.</span><span class="sxs-lookup"><span data-stu-id="852ca-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="852ca-212">Hola `<Root level="error">` sección configura el nivel de raíz de Hola de registro (todo lo que no está en `com.microsoft.example`) tooonly información de error de registro.</span><span class="sxs-lookup"><span data-stu-id="852ca-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="852ca-213">Para obtener más información sobre la configuración de registro de Log4j, consulte [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="852ca-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="852ca-214">La versión 0.10.0 y superiores de Storm utilizan Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="852ca-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="852ca-215">Las versiones anteriores de Storm usaban Log4j 1.x, que empleaba otro formato de configuración del registro.</span><span class="sxs-lookup"><span data-stu-id="852ca-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="852ca-216">Para obtener información sobre la configuración anterior de hello, consulte [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="852ca-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="852ca-217">Topología de hello pruebas localmente</span><span class="sxs-lookup"><span data-stu-id="852ca-217">Test hello topology locally</span></span>

<span data-ttu-id="852ca-218">Después de guardar los archivos de hello, utilice Hola después topología localmente de comando tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="852ca-219">Mientras se ejecuta, topología hello muestra información de inicio.</span><span class="sxs-lookup"><span data-stu-id="852ca-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="852ca-220">Hello texto siguiente es un ejemplo de salida de recuento de hello word:</span><span class="sxs-lookup"><span data-stu-id="852ca-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="852ca-221">Este registro de ejemplo indica esa palabra Hola ' y ' se emitió 113 veces.</span><span class="sxs-lookup"><span data-stu-id="852ca-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="852ca-222">Hello recuento continúa toogo hasta como topología Hola se ejecuta porque pitorro Hola continuamente emite Hola mismas frases.</span><span class="sxs-lookup"><span data-stu-id="852ca-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="852ca-223">Hay un intervalo de 5 segundos entre la emisión de las palabras y los recuentos.</span><span class="sxs-lookup"><span data-stu-id="852ca-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="852ca-224">Hola **WordCount** componente está configurado tooonly emitir información cuando llega una tupla de graduación.</span><span class="sxs-lookup"><span data-stu-id="852ca-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="852ca-225">Solicita que esas tuplas se entreguen solo cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="852ca-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="852ca-226">Convertir Hola topología tooFlux</span><span class="sxs-lookup"><span data-stu-id="852ca-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="852ca-227">Un flujo es un nuevo marco disponible con Storm 0.10.0 y versiones posterior, lo que permite tooseparate configuración de implementación.</span><span class="sxs-lookup"><span data-stu-id="852ca-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="852ca-228">Los componentes aún están definidos en Java, pero topología Hola se define utilizando un archivo YAML.</span><span class="sxs-lookup"><span data-stu-id="852ca-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="852ca-229">Puede empaquetar una definición de topología de manera predeterminada con el proyecto, o usar un archivo independiente al enviar la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="852ca-230">Al enviar Hola topología tooStorm, puede utilizar variables de entorno o valores de toopopulate de archivos de configuración en la definición de la topología YAML Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="852ca-231">archivo de Hello YAML define Hola componentes toouse de topología de Hola y Hola de flujo de datos entre ellos.</span><span class="sxs-lookup"><span data-stu-id="852ca-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="852ca-232">Puede incluir un archivo YAML como parte del archivo jar de Hola o puede usar un archivo YAML externo.</span><span class="sxs-lookup"><span data-stu-id="852ca-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="852ca-233">Para más información sobre Flux, vea este documento sobre el [marco de trabajo de Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="852ca-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="852ca-234">Due tooa [error (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) con Storm 1.0.1, puede que necesite tooinstall una [entorno de desarrollo de Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) localmente las topologías de un flujo de toorun.</span><span class="sxs-lookup"><span data-stu-id="852ca-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="852ca-235">Mover hello `WordCountTopology.java` archivo fuera del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="852ca-236">Anteriormente, este archivo define la topología de hello, pero no es necesario con un flujo.</span><span class="sxs-lookup"><span data-stu-id="852ca-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="852ca-237">Hola `resources` directorio, cree un archivo denominado `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="852ca-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="852ca-238">Usar hello después de texto como contenido de Hola de este archivo.</span><span class="sxs-lookup"><span data-stu-id="852ca-238">Use hello following text as hello contents of this file.</span></span>

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

3. <span data-ttu-id="852ca-239">Realizar Hola después cambios toohello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="852ca-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="852ca-240">Agregar Hola después nuevas dependencias en hello `<dependencies>` sección:</span><span class="sxs-lookup"><span data-stu-id="852ca-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="852ca-241">Agregar Hola después complemento toohello `<plugins>` sección.</span><span class="sxs-lookup"><span data-stu-id="852ca-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="852ca-242">Este complemento controla la creación de hello de un paquete (archivo jar) para el proyecto de Hola y aplica algunos tooFlux específico de transformaciones al crear paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="852ca-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
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

   * <span data-ttu-id="852ca-243">Hola **exec-maven-plugin** `<configuration>` sección, cambie el valor de Hola para `<mainClass>` demasiado`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="852ca-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="852ca-244">Esta configuración permite toohandle flujo ejecuta topología Hola localmente en el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="852ca-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="852ca-245">Hola `<resources>` sección, agregue Hola después toohello `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="852ca-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="852ca-246">Este código XML incluye el archivo hello YAML que define la topología de hello como parte del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="852ca-247">Topología de un flujo de Hola de prueba localmente</span><span class="sxs-lookup"><span data-stu-id="852ca-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="852ca-248">Use Hola después toocompile y ejecute la topología de un flujo de hello mediante Maven:</span><span class="sxs-lookup"><span data-stu-id="852ca-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="852ca-249">Si usa PowerShell, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="852ca-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="852ca-250">Este comando produce un error si la topología usa bits de Storm 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="852ca-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="852ca-251">Este error se debe a [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="852ca-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="852ca-252">En su lugar, [instalar Storm en su entorno de desarrollo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) y use Hola siguiendo la información.</span><span class="sxs-lookup"><span data-stu-id="852ca-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="852ca-253">Si tiene [instalado Storm en el entorno de desarrollo](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), puede usar Hola siguientes comandos en su lugar:</span><span class="sxs-lookup"><span data-stu-id="852ca-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="852ca-254">Hola `--local` parámetro topología Hola ejecuta en modo local en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="852ca-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="852ca-255">Hola `-R /topology.yaml` parámetro utiliza hello `topology.yaml` recursos de archivos de topología de hello jar archivo toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="852ca-256">Mientras se ejecuta, topología hello muestra información de inicio.</span><span class="sxs-lookup"><span data-stu-id="852ca-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="852ca-257">Hola después de texto es un ejemplo de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="852ca-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="852ca-258">Hay un retraso de 10 segundos entre los distintos lotes de la información registrada.</span><span class="sxs-lookup"><span data-stu-id="852ca-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="852ca-259">Realizar una copia de hello `topology.yaml` archivo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="852ca-260">Nuevo archivo de nombre hello `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="852ca-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="852ca-261">Hola `newtopology.yaml` de archivos, busque la siguiente Hola sección y cambie el valor Hola de `10` demasiado`5`.</span><span class="sxs-lookup"><span data-stu-id="852ca-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="852ca-262">Este intervalo de saludo de modificación cambios entre la emisión de lotes de word cuenta de too5 de 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="852ca-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

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

    <span data-ttu-id="852ca-263">También puede hacer lo siguiente si tiene Storm en el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="852ca-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="852ca-264">Hola de cambio `/path/to/newtopology.yaml` toohello ruta toohello newtopology.yaml archivo creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="852ca-265">Este comando usa hello newtopology.yaml como definición de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="852ca-266">Puesto que no incluimos hello `compile` parámetro, Maven utiliza Hola versión de Hola proyecto creado en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="852ca-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="852ca-267">Una vez Hola topología se inicia, debe tener en cuenta que tiempo Hola entre los distintos lotes emitidos ha cambiado el valor de Hola de tooreflect en newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="852ca-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="852ca-268">Para que pueda ver que puede cambiar la configuración a través de un archivo YAML sin necesidad de topología de hello toorecompile.</span><span class="sxs-lookup"><span data-stu-id="852ca-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="852ca-269">Para obtener más información sobre estas y otras características del marco de trabajo de un flujo de hello, consulte [flujo (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="852ca-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="852ca-270">Trident</span><span class="sxs-lookup"><span data-stu-id="852ca-270">Trident</span></span>

<span data-ttu-id="852ca-271">Trident es una abstracción de alto nivel que ofrece Storm.</span><span class="sxs-lookup"><span data-stu-id="852ca-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="852ca-272">Admite el procesamiento con estado.</span><span class="sxs-lookup"><span data-stu-id="852ca-272">It supports stateful processing.</span></span> <span data-ttu-id="852ca-273">Hola principal ventaja de Trident es que puede garantizar que cada mensaje que entra en la topología de Hola se procesa solo una vez.</span><span class="sxs-lookup"><span data-stu-id="852ca-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="852ca-274">Si no se usa Trident, la topología solo puede garantizar que los mensajes se procesan al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="852ca-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="852ca-275">También hay otras diferencias, como los componentes integrados que se pueden usar en lugar de crear bolts.</span><span class="sxs-lookup"><span data-stu-id="852ca-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="852ca-276">De hecho, los bolts se reemplazan por componentes menos genéricos, como filtros, proyecciones y funciones.</span><span class="sxs-lookup"><span data-stu-id="852ca-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="852ca-277">Las aplicaciones de Trident se pueden crear mediante proyectos de Maven.</span><span class="sxs-lookup"><span data-stu-id="852ca-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="852ca-278">Usar hello basic mismo pasos tal como se presenta anteriormente en este artículo, solo el código de hello es diferente.</span><span class="sxs-lookup"><span data-stu-id="852ca-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="852ca-279">Trident también no (actualmente) puede utilizarse con marco de trabajo de un flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ca-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="852ca-280">Para obtener más información acerca de Trident, vea hello [Introducción a la API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="852ca-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="852ca-281">Para ver un ejemplo de una aplicación de Trident, consulte [Tendencias de Twitter con Apache Storm en HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="852ca-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="852ca-282">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="852ca-282">Next Steps</span></span>

<span data-ttu-id="852ca-283">Ha aprendido cómo toocreate una topología Storm con Java.</span><span class="sxs-lookup"><span data-stu-id="852ca-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="852ca-284">Ahora obtenga información sobre:</span><span class="sxs-lookup"><span data-stu-id="852ca-284">Now learn how to:</span></span>

* [<span data-ttu-id="852ca-285">Implementación y administración de topologías de Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="852ca-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="852ca-286">Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="852ca-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="852ca-287">Puede encontrar más topologías de ejemplo de Storm en [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="852ca-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

