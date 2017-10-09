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
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Utilización de una función definida por el usuario de Java con Hive en HDInsight

Obtenga información acerca de cómo toocreate basados en Java definidos por el usuario (función) (UDF) que funciona con Hive. Hola UDF de Java en este ejemplo convierte una tabla de caracteres de tooall minúsculas de las cadenas de texto.

## <a name="requirements"></a>Requisitos

* Un clúster de HDInsight. 

    > [!IMPORTANT]
    > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

    La mayoría de los pasos de este documento funcionan tanto en clústeres basados en Windows como en Linux. Sin embargo, Hola pasos utilizados tooupload Hola compilados de clúster UDF toohello y ejecución son los clústeres de tooLinux-based específicos. Se proporcionan vínculos tooinformation que puede utilizarse con clústeres basados en Windows.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o posterior (o un equivalente como OpenJDK).

* [Apache Maven](http://maven.apache.org/)

* Un editor de texto o IDE de Java

    > [!IMPORTANT]
    > Si crea archivos de Python en un cliente de Windows hello, debe utilizar un editor que utiliza LF como un final de línea. Si no está seguro de si el editor utiliza LF o CRLF, vea hello [solución de problemas](#troubleshooting) sección para pasos acerca de cómo quitar Hola caracteres CR.

## <a name="create-an-example-java-udf"></a>Crear una función de Java definida por el usuario de ejemplo 

1. Desde una línea de comandos, use Hola después toocreate un nuevo proyecto de Maven:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > Si usa PowerShell, debe incluir las comillas alrededor de los parámetros de Hola. Por ejemplo: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Este comando crea un directorio denominado **exampleudf**, que contiene proyectos de Maven Hola.

2. Una vez que se ha creado el proyecto de hello, eliminar hello **exampleudf/src/test** directorio creado como parte del proyecto de Hola.

3. Abra hello **exampleudf/pom.xml**y reemplace Hola existente `<dependencies>` entrada con hello continuación de XML:

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

    Estas entradas especifican versión de Hola de Hadoop y Hive incluido con HDInsight 3.5. Puede encontrar información sobre las versiones de Hadoop y Hive proporcionada con HDInsight de Hola Hola [versiones de componentes de HDInsight](hdinsight-component-versioning.md) documento.

    Agregar un `<build>` sección antes de hello `</project>` línea hello final de archivo hello. Esta sección debe contener Hola continuación de XML:

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

    Estas entradas definen cómo toobuild Hola proyecto. En concreto, la versión de Hola de Java que Hola que usa project y cómo toobuild una uberjar para clúster toohello de implementación.

    Guardar archivo hello una vez que se han realizado cambios de Hola.

4. Cambiar el nombre de **exampleudf/src/main/java/com/microsoft/examples/App.java** demasiado**ExampleUDF.java**y, a continuación, abra el archivo hello en el editor.

5. Reemplazar contenido Hola de hello **ExampleUDF.java** archivos con siguiente hello, a continuación, guarde el archivo hello.

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

    Este código implementa un UDF que acepta un valor de cadena y devuelve una versión en minúsculas de la cadena de Hola.

## <a name="build-and-install-hello-udf"></a>Compilar e instalar Hola UDF

1. Comando toocompile siguiente de Hola de uso y empaquetar Hola UDF:

    ```bash
    mvn compile package
    ```

    Este comando genera y paquetes Hola UDF en hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` archivo.

2. Hola de uso `scp` clúster de HDInsight de toohello de archivo de comandos toocopy Hola.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Reemplace `myuser` con hello cuenta de usuario SSH para el clúster. Reemplace `mycluster` con el nombre del clúster de Hola. Si ha usado un hello toosecure de contraseña SSH cuenta, son contraseña de hello tooenter solicitadas. Si usa un certificado, puede que necesite toouse hello `-i` archivo de clave privada de parámetro toospecify Hola.

3. Conecte el clúster toohello mediante SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

4. Desde la sesión de SSH de hello, copie almacenamiento de tooHDInsight de archivos jar de Hola.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Usar hello UDF de Hive

1. Usar hello después de cliente de Beeline toostart Hola de sesión SSH Hola.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Este comando se da por supuesto que usar valor predeterminado es hello **administrador** para la cuenta de inicio de sesión de hello para el clúster.

2. Una vez que llegan a hello `jdbc:hive2://localhost:10001/>` símbolo del sistema, escriba Hola después tooadd Hola UDF tooHive y exponerlo como una función.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > En este ejemplo se da por supuesto que el almacenamiento de Azure es almacenamiento predeterminado para el clúster de Hola. Si su clúster usa el almacén de Data Lake en su lugar, cambie hello `wasb:///` valor demasiado`adl:///`.

3. Use Hola UDF tooconvert valores recuperados de una tabla toolower caso las cadenas.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    Esta consulta selecciona Hola plataforma de dispositivo (Android, Windows, iOS, etc.) de la tabla de hello, convertir case de toolower la cadena hello y, a continuación, mostrarlas. salida de Hello aparece toohello similar siguiente texto:

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

## <a name="next-steps"></a>Pasos siguientes

Para otro toowork maneras con Hive, consulte [uso de Hive con HDInsight](hdinsight-use-hive.md).

Para obtener más información sobre las funciones de Hive User-Defined, consulte [Hive operadores y funciones definidas por el usuario](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sección de wiki de Hive hello en apache.org.
