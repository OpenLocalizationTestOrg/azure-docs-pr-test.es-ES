---
title: "Uso de una función definida por el usuario (UDF) de Java con Hive en HDInsight - Azure | Microsoft Docs"
description: "Aprenda cómo crear una función basada en Java y definida por el usuario (UDF) que funcione con Hive. Esta función de ejemplo definida por el usuario convierte una tabla de cadenas de texto en minúsculas."
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="37fe2-104">Utilización de una función definida por el usuario de Java con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="37fe2-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="37fe2-105">Aprenda cómo crear una función basada en Java y definida por el usuario (UDF) que funcione con Hive.</span><span class="sxs-lookup"><span data-stu-id="37fe2-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="37fe2-106">La función de Java definida por el usuario de este ejemplo convierte una tabla de cadenas de texto a caracteres en minúscula.</span><span class="sxs-lookup"><span data-stu-id="37fe2-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="37fe2-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="37fe2-107">Requirements</span></span>

* <span data-ttu-id="37fe2-108">Un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37fe2-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="37fe2-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="37fe2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="37fe2-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="37fe2-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="37fe2-111">La mayoría de los pasos de este documento funcionan tanto en clústeres basados en Windows como en Linux.</span><span class="sxs-lookup"><span data-stu-id="37fe2-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="37fe2-112">Sin embargo, los pasos utilizados para cargar la función definida por el usuario compilada al clúster y ejecutarla son específicos de los clústeres basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="37fe2-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="37fe2-113">Se proporcionan vínculos a información que puede utilizarse con clústeres basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="37fe2-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="37fe2-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o posterior (o un equivalente como OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="37fe2-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="37fe2-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="37fe2-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="37fe2-116">Un editor de texto o IDE de Java</span><span class="sxs-lookup"><span data-stu-id="37fe2-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="37fe2-117">Si crea los archivos de Python en un cliente Windows, debe usar un editor que emplee LF como final de línea.</span><span class="sxs-lookup"><span data-stu-id="37fe2-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="37fe2-118">Si no está seguro de si el editor usa LF o CRLF, vea la sección [Solución de problemas](#troubleshooting) para conocer los pasos a seguir para quitar el carácter CR.</span><span class="sxs-lookup"><span data-stu-id="37fe2-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="37fe2-119">Crear una función de Java definida por el usuario de ejemplo</span><span class="sxs-lookup"><span data-stu-id="37fe2-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="37fe2-120">Desde una línea de comandos, utilice lo siguiente para crear un nuevo proyecto de Maven:</span><span class="sxs-lookup"><span data-stu-id="37fe2-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="37fe2-121">Si va a usar PowerShell, deberá colocar comillas alrededor de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="37fe2-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="37fe2-122">Por ejemplo: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="37fe2-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="37fe2-123">Este comando crea un directorio denominado **exampleudf**, que contiene el proyecto Maven.</span><span class="sxs-lookup"><span data-stu-id="37fe2-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="37fe2-124">Una vez creado el proyecto, elimine el directorio **exampleudf/src/test** que se creó como parte del proyecto.</span><span class="sxs-lookup"><span data-stu-id="37fe2-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="37fe2-125">Abra **exampleudf/pom.xml** y sustituya la entrada `<dependencies>` existente por el XML siguiente:</span><span class="sxs-lookup"><span data-stu-id="37fe2-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="37fe2-126">Estas entradas especifican la versión de Hadoop y Hive incluida con el clúster de HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="37fe2-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="37fe2-127">Puede encontrar información sobre las versiones de Hadoop y Hive proporcionadas con HDInsight en el artículo [¿Cuáles son los diferentes componentes de Hadoop disponibles con HDInsight?](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="37fe2-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="37fe2-128">Agregue una sección `<build>` antes de la línea `</project>` al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="37fe2-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="37fe2-129">Esta sección debe contener el siguiente XML:</span><span class="sxs-lookup"><span data-stu-id="37fe2-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="37fe2-130">Estas entradas definen cómo compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="37fe2-130">These entries define how to build the project.</span></span> <span data-ttu-id="37fe2-131">Específicamente, la versión de Java que el proyecto usa y cómo compilar un archivo uberjar para implementarlo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="37fe2-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="37fe2-132">Guarde el archivo una vez hechos los cambios.</span><span class="sxs-lookup"><span data-stu-id="37fe2-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="37fe2-133">Cambie el nombre de **exampleudf/src/main/java/com/microsoft/examples/App.java** a **ExampleUDF.java** y, después, abra el archivo en el editor.</span><span class="sxs-lookup"><span data-stu-id="37fe2-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="37fe2-134">Reemplace el contenido del archivo **ExampleUDF.java** por el código siguiente y, a continuación, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="37fe2-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="37fe2-135">Este código implementa una función definida por el usuario que acepta un valor de cadena y devuelve una versión en minúsculas de esta.</span><span class="sxs-lookup"><span data-stu-id="37fe2-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="37fe2-136">Compilación e instalación de la función definida por el usuario</span><span class="sxs-lookup"><span data-stu-id="37fe2-136">Build and install the UDF</span></span>

1. <span data-ttu-id="37fe2-137">Utilice el siguiente comando para compilar y empaquetar la función definida por el usuario:</span><span class="sxs-lookup"><span data-stu-id="37fe2-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="37fe2-138">Este comando compila y empaqueta la función definida por el usuario en el archivo `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="37fe2-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="37fe2-139">Utilice el comando `scp` para copiar el archivo en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37fe2-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="37fe2-140">Sustituya `myuser` por la cuenta de usuario SSH del clúster.</span><span class="sxs-lookup"><span data-stu-id="37fe2-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="37fe2-141">Reemplace `mycluster` por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="37fe2-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="37fe2-142">Si usa una contraseña para proteger la cuenta SSH, se le solicita que escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="37fe2-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="37fe2-143">Si utilizó un certificado, tal vez tenga que usar el parámetro `-i` para especificar el archivo de claves privadas.</span><span class="sxs-lookup"><span data-stu-id="37fe2-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="37fe2-144">Conéctese al clúster con SSH.</span><span class="sxs-lookup"><span data-stu-id="37fe2-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="37fe2-145">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="37fe2-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="37fe2-146">Desde la sesión SSH, copie el archivo jar en el almacenamiento de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37fe2-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="37fe2-147">Uso de la función definida por el usuario desde Hive</span><span class="sxs-lookup"><span data-stu-id="37fe2-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="37fe2-148">Use lo siguiente para iniciar el cliente Beeline desde la sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="37fe2-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="37fe2-149">Este comando supone que usó el valor predeterminado de **admin** para la cuenta de inicio de sesión del clúster.</span><span class="sxs-lookup"><span data-stu-id="37fe2-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="37fe2-150">Una vez alcanzado el aviso `jdbc:hive2://localhost:10001/>` , escriba lo siguiente para agregar la función definida por el usuario a Hive y exponerla como una función.</span><span class="sxs-lookup"><span data-stu-id="37fe2-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="37fe2-151">En este ejemplo se da por supuesto que el almacenamiento predeterminado para el clúster es Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="37fe2-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="37fe2-152">Si su clúster utiliza Data Lake Store en su lugar, cambie el valor `wasb:///` a `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="37fe2-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="37fe2-153">Use la función definida por el usuario para convertir los valores recuperados de una tabla a cadenas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="37fe2-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="37fe2-154">Esta consulta seleccionará la plataforma del dispositivo (Android, Windows, iOS, etc.) de la tabla, convertirá la cadena a minúsculas y, a continuación, las mostrará.</span><span class="sxs-lookup"><span data-stu-id="37fe2-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="37fe2-155">La salida es similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="37fe2-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="37fe2-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37fe2-156">Next steps</span></span>

<span data-ttu-id="37fe2-157">Para conocer otras formas de trabajar con Hive, consulte [Usar Hive y HiveQL con Hadoop en HDInsight para analizar un archivo log4j de Apache de muestra](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="37fe2-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="37fe2-158">Para más información sobre las funciones definidas por el usuario de Hive, consulte la sección [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) (Operadores de Hive y funciones definidas por el usuario) de la wiki de Hive en apache.org.</span><span class="sxs-lookup"><span data-stu-id="37fe2-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
