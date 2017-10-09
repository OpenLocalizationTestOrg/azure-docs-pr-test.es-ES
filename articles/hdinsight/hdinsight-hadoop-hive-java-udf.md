---
title: "aaaJava definido por el usuario (función) (UDF) con Hive en HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate basados en Java definidos por el usuario (función) (UDF) que funciona con Hive. En este ejemplo UDF convierte una tabla de toolowercase de cadenas de texto."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="67516-104">Utilización de una función definida por el usuario de Java con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="67516-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="67516-105">Obtenga información acerca de cómo toocreate basados en Java definidos por el usuario (función) (UDF) que funciona con Hive.</span><span class="sxs-lookup"><span data-stu-id="67516-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="67516-106">Hola UDF de Java en este ejemplo convierte una tabla de caracteres de tooall minúsculas de las cadenas de texto.</span><span class="sxs-lookup"><span data-stu-id="67516-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="67516-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="67516-107">Requirements</span></span>

* <span data-ttu-id="67516-108">Un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67516-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="67516-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="67516-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="67516-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="67516-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="67516-111">La mayoría de los pasos de este documento funcionan tanto en clústeres basados en Windows como en Linux.</span><span class="sxs-lookup"><span data-stu-id="67516-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="67516-112">Sin embargo, Hola pasos utilizados tooupload Hola compilados de clúster UDF toohello y ejecución son los clústeres de tooLinux-based específicos.</span><span class="sxs-lookup"><span data-stu-id="67516-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="67516-113">Se proporcionan vínculos tooinformation que puede utilizarse con clústeres basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="67516-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="67516-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o posterior (o un equivalente como OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="67516-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="67516-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="67516-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="67516-116">Un editor de texto o IDE de Java</span><span class="sxs-lookup"><span data-stu-id="67516-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="67516-117">Si crea archivos de Python en un cliente de Windows hello, debe utilizar un editor que utiliza LF como un final de línea.</span><span class="sxs-lookup"><span data-stu-id="67516-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="67516-118">Si no está seguro de si el editor utiliza LF o CRLF, vea hello [solución de problemas](#troubleshooting) sección para pasos acerca de cómo quitar Hola caracteres CR.</span><span class="sxs-lookup"><span data-stu-id="67516-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="67516-119">Crear una función de Java definida por el usuario de ejemplo</span><span class="sxs-lookup"><span data-stu-id="67516-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="67516-120">Desde una línea de comandos, use Hola después toocreate un nuevo proyecto de Maven:</span><span class="sxs-lookup"><span data-stu-id="67516-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="67516-121">Si usa PowerShell, debe incluir las comillas alrededor de los parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="67516-122">Por ejemplo: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="67516-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="67516-123">Este comando crea un directorio denominado **exampleudf**, que contiene proyectos de Maven Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="67516-124">Una vez que se ha creado el proyecto de hello, eliminar hello **exampleudf/src/test** directorio creado como parte del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="67516-125">Abra hello **exampleudf/pom.xml**y reemplace Hola existente `<dependencies>` entrada con hello continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="67516-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="67516-126">Estas entradas especifican versión de Hola de Hadoop y Hive incluido con HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="67516-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="67516-127">Puede encontrar información sobre las versiones de Hadoop y Hive proporcionada con HDInsight de Hola Hola [versiones de componentes de HDInsight](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="67516-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="67516-128">Agregar un `<build>` sección antes de hello `</project>` línea hello final de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="67516-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="67516-129">Esta sección debe contener Hola continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="67516-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="67516-130">Estas entradas definen cómo toobuild Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="67516-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="67516-131">En concreto, la versión de Hola de Java que Hola que usa project y cómo toobuild una uberjar para clúster toohello de implementación.</span><span class="sxs-lookup"><span data-stu-id="67516-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="67516-132">Guardar archivo hello una vez que se han realizado cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="67516-133">Cambiar el nombre de **exampleudf/src/main/java/com/microsoft/examples/App.java** demasiado**ExampleUDF.java**y, a continuación, abra el archivo hello en el editor.</span><span class="sxs-lookup"><span data-stu-id="67516-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="67516-134">Reemplazar contenido Hola de hello **ExampleUDF.java** archivos con siguiente hello, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="67516-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="67516-135">Este código implementa un UDF que acepta un valor de cadena y devuelve una versión en minúsculas de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="67516-136">Compilar e instalar Hola UDF</span><span class="sxs-lookup"><span data-stu-id="67516-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="67516-137">Comando toocompile siguiente de Hola de uso y empaquetar Hola UDF:</span><span class="sxs-lookup"><span data-stu-id="67516-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="67516-138">Este comando genera y paquetes Hola UDF en hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` archivo.</span><span class="sxs-lookup"><span data-stu-id="67516-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="67516-139">Hola de uso `scp` clúster de HDInsight de toohello de archivo de comandos toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="67516-140">Reemplace `myuser` con hello cuenta de usuario SSH para el clúster.</span><span class="sxs-lookup"><span data-stu-id="67516-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="67516-141">Reemplace `mycluster` con el nombre del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="67516-142">Si ha usado un hello toosecure de contraseña SSH cuenta, son contraseña de hello tooenter solicitadas.</span><span class="sxs-lookup"><span data-stu-id="67516-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="67516-143">Si usa un certificado, puede que necesite toouse hello `-i` archivo de clave privada de parámetro toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="67516-144">Conecte el clúster toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="67516-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="67516-145">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="67516-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="67516-146">Desde la sesión de SSH de hello, copie almacenamiento de tooHDInsight de archivos jar de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="67516-147">Usar hello UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="67516-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="67516-148">Usar hello después de cliente de Beeline toostart Hola de sesión SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="67516-149">Este comando se da por supuesto que usar valor predeterminado es hello **administrador** para la cuenta de inicio de sesión de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="67516-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="67516-150">Una vez que llegan a hello `jdbc:hive2://localhost:10001/>` símbolo del sistema, escriba Hola después tooadd Hola UDF tooHive y exponerlo como una función.</span><span class="sxs-lookup"><span data-stu-id="67516-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="67516-151">En este ejemplo se da por supuesto que el almacenamiento de Azure es almacenamiento predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="67516-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="67516-152">Si su clúster usa el almacén de Data Lake en su lugar, cambie hello `wasb:///` valor demasiado`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="67516-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="67516-153">Use Hola UDF tooconvert valores recuperados de una tabla toolower caso las cadenas.</span><span class="sxs-lookup"><span data-stu-id="67516-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="67516-154">Esta consulta selecciona Hola plataforma de dispositivo (Android, Windows, iOS, etc.) de la tabla de hello, convertir case de toolower la cadena hello y, a continuación, mostrarlas.</span><span class="sxs-lookup"><span data-stu-id="67516-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="67516-155">salida de Hello aparece toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="67516-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="67516-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67516-156">Next steps</span></span>

<span data-ttu-id="67516-157">Para otro toowork maneras con Hive, consulte [uso de Hive con HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="67516-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="67516-158">Para obtener más información sobre las funciones de Hive User-Defined, consulte [Hive operadores y funciones definidas por el usuario](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sección de wiki de Hive hello en apache.org.</span><span class="sxs-lookup"><span data-stu-id="67516-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
