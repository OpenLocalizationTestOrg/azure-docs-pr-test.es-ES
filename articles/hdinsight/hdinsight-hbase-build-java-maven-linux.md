---
title: cliente de HBase aaaJava - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse aplicación de Apache HBase de Apache Maven toobuild basados en Java, a continuación, implementarlo tooHBase en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="1633e-103">Compilar aplicaciones Java para Apache HBase</span><span class="sxs-lookup"><span data-stu-id="1633e-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="1633e-104">Obtenga información acerca de cómo toocreate una [HBase Apache](http://hbase.apache.org/) aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="1633e-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="1633e-105">A continuación, usar aplicación hello con HBase en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="1633e-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="1633e-106">Hola los pasos de este documento se usa [Maven](http://maven.apache.org/) proyecto hello toocreate y compilación.</span><span class="sxs-lookup"><span data-stu-id="1633e-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="1633e-107">Maven es una herramienta de comprensión que permite el software de toobuild, documentación e informes para los proyectos de Java y la administración de proyectos de software.</span><span class="sxs-lookup"><span data-stu-id="1633e-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="1633e-108">Hello pasos de este documento se más recientemente probaron con 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1633e-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1633e-109">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="1633e-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="1633e-110">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="1633e-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1633e-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1633e-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="1633e-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1633e-112">Requirements</span></span>

* <span data-ttu-id="1633e-113">[JDK de la plataforma Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior.</span><span class="sxs-lookup"><span data-stu-id="1633e-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1633e-114">HDInsight 3.5 y las versiones posteriores necesitan Java 8.</span><span class="sxs-lookup"><span data-stu-id="1633e-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="1633e-115">Las versiones anteriores de HDInsight requieren Java 7.</span><span class="sxs-lookup"><span data-stu-id="1633e-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="1633e-116">Maven</span><span class="sxs-lookup"><span data-stu-id="1633e-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="1633e-117">Un clúster de Azure HDInsight basado en Linux con HBase</span><span class="sxs-lookup"><span data-stu-id="1633e-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="1633e-118">pasos de Hello en este documento se han probado con las versiones de clúster de HDInsight 3.4 y 3.5.</span><span class="sxs-lookup"><span data-stu-id="1633e-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="1633e-119">valores predeterminados de Hello proporcionados en los ejemplos son para un clúster de HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="1633e-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="1633e-120">Crear proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="1633e-120">Create hello project</span></span>

1. <span data-ttu-id="1633e-121">Desde la línea de comandos de hello en el entorno de desarrollo, cambiar directorios toohello ubicación donde desea que project de hello toocreate, por ejemplo, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="1633e-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="1633e-122">Hola de uso **mvn** comando, que se instala con Maven, hello toogenerate scaffolding para proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="1633e-123">Si usa PowerShell, debe encerrar hello `-D` parámetros entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="1633e-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="1633e-124">Este comando crea un directorio con el mismo nombre como Hola de hello **artifactID** parámetro (**hbaseapp** en este ejemplo.) Este directorio contiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1633e-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="1633e-125">**pom.XML**: Hola modelo de objetos de proyecto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene información y configuración detalles usados toobuild hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1633e-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="1633e-126">**src**: directorio de Hola que contiene Hola **principal/java/com/microsoft/ejemplos** directorio, donde crear aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1633e-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="1633e-127">Eliminar hello `src/test/java/com/microsoft/examples/apptest.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="1633e-128">No lo vamos a usar en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1633e-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="1633e-129">Actualizar Hola modelo de objetos de proyecto</span><span class="sxs-lookup"><span data-stu-id="1633e-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="1633e-130">Editar hello `pom.xml` de archivos y agregar Hola siguiente código dentro de hello `<dependencies>` sección:</span><span class="sxs-lookup"><span data-stu-id="1633e-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="1633e-131">Esta sección indica dicho proyecto Hola debe **hbase cliente** y **phoenix core** componentes.</span><span class="sxs-lookup"><span data-stu-id="1633e-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="1633e-132">En tiempo de compilación, estas dependencias se descargan del repositorio de Maven Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1633e-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="1633e-133">Puede usar hello [búsqueda de repositorio Central de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn más información acerca de esta dependencia.</span><span class="sxs-lookup"><span data-stu-id="1633e-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1633e-134">número de versión de Hola de hello hbase-cliente debe coincidir con la versión de Hola de HBase que se proporciona con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1633e-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="1633e-135">Usar hello siguiendo el número de versión correcto de tabla toofind Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="1633e-136">Versión del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1633e-136">HDInsight cluster version</span></span> | <span data-ttu-id="1633e-137">HBase versión toouse</span><span class="sxs-lookup"><span data-stu-id="1633e-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="1633e-138">3.2</span><span class="sxs-lookup"><span data-stu-id="1633e-138">3.2</span></span> |<span data-ttu-id="1633e-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="1633e-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="1633e-140">3.3, 3.4, 3.5 y 3.6</span><span class="sxs-lookup"><span data-stu-id="1633e-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="1633e-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="1633e-141">1.1.2</span></span> |

    <span data-ttu-id="1633e-142">Para obtener más información sobre los componentes y las versiones de HDInsight, vea [¿qué componentes de Hadoop diferentes de hello disponibles con HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1633e-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="1633e-143">Agregar Hola después código toohello **pom.xml** archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="1633e-144">Este texto debe estar dentro de hello `<project>...</project>` hello las etiquetas de archivos, por ejemplo, entre `</dependencies>` y `</project>`.</span><span class="sxs-lookup"><span data-stu-id="1633e-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
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
        </plugins>
    </build>
   ```

    <span data-ttu-id="1633e-145">Esta sección configura un recurso (`conf/hbase-site.xml`) que contiene información de configuración de HBase.</span><span class="sxs-lookup"><span data-stu-id="1633e-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1633e-146">También puede establecer los valores de configuración mediante código.</span><span class="sxs-lookup"><span data-stu-id="1633e-146">You can also set configuration values via code.</span></span> <span data-ttu-id="1633e-147">Vea los comentarios de Hola Hola `CreateTable` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1633e-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="1633e-148">En esta sección también configura hello [Maven compilador complemento](http://maven.apache.org/plugins/maven-compiler-plugin/) y [Maven tono complemento](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="1633e-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="1633e-149">compilador de saludo complemento es toocompile usado Hola topología.</span><span class="sxs-lookup"><span data-stu-id="1633e-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="1633e-150">sombra de Hello complemento es duplicación de licencia tooprevent usado en paquete de archivo JAR de hello Maven compilada.</span><span class="sxs-lookup"><span data-stu-id="1633e-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="1633e-151">Este complemento es un error "Duplicar archivos de licencia" de tooprevent utilizado en tiempo de ejecución en el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="1633e-152">Mediante el complemento de sombreado de maven con hello `ApacheLicenseResourceTransformer` implementación evita que el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="1633e-153">Hola maven-sombra-plugin también genera un archivo jar de misma que contiene todas las dependencias de hello requeridas por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1633e-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="1633e-154">Guardar hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="1633e-155">Cree un directorio denominado `conf` en hello `hbaseapp` directory.</span><span class="sxs-lookup"><span data-stu-id="1633e-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="1633e-156">Este directorio es la información de configuración de toohold usado para conectar tooHBase.</span><span class="sxs-lookup"><span data-stu-id="1633e-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="1633e-157">Siguiente Hola de uso del comando toocopy configuración de HBase Hola de toohello de clúster de HBase Hola `conf` directory.</span><span class="sxs-lookup"><span data-stu-id="1633e-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="1633e-158">Reemplace `USERNAME` con el nombre de Hola de su inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="1633e-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="1633e-159">Reemplace `CLUSTERNAME` por el nombre del clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1633e-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="1633e-160">Para más información sobre cómo usar `ssh` y `scp`, vea [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1633e-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="1633e-161">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="1633e-161">Create hello application</span></span>

1. <span data-ttu-id="1633e-162">Vaya toohello `hbaseapp/src/main/java/com/microsoft/examples` directorio y el nombre hello app.java archivo demasiado`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="1633e-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="1633e-163">Abra hello `CreateTable.java` archivo y reemplazar contenido existente de hello con hello después de texto:</span><span class="sxs-lookup"><span data-stu-id="1633e-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="1633e-164">Este código es hello **CreateTable** (clase), que crea una tabla denominada **personas** y rellenarlo con algunos usuarios predefinidos.</span><span class="sxs-lookup"><span data-stu-id="1633e-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="1633e-165">Guardar hello `CreateTable.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="1633e-166">Hola `hbaseapp/src/main/java/com/microsoft/examples` directorio, cree un archivo denominado `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="1633e-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="1633e-167">Usar hello después de texto como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="1633e-167">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="1633e-168">Hola **SearchByEmail** clase puede ser tooquery usado para las filas por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1633e-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="1633e-169">Porque utiliza un filtro de expresión regular, puede proporcionar una cadena o una expresión regular cuando se usa la clase hello.</span><span class="sxs-lookup"><span data-stu-id="1633e-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="1633e-170">Guardar hello `SearchByEmail.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="1633e-171">Hola `hbaseapp/src/main/hava/com/microsoft/examples` directorio, cree un archivo denominado `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="1633e-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="1633e-172">Usar hello después de texto como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="1633e-172">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="1633e-173">Esta clase limpia Hola tablas HBase creadas en este ejemplo, al deshabilitar y quitar tabla Hola creadas por hello `CreateTable` clase.</span><span class="sxs-lookup"><span data-stu-id="1633e-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="1633e-174">Guardar hello `DeleteTable.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="1633e-175">Compilación y paquete de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="1633e-175">Build and package hello application</span></span>

1. <span data-ttu-id="1633e-176">De hello `hbaseapp` directorio, el comando de uso Hola siguiente toobuild un archivo JAR que contiene la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="1633e-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="1633e-177">Este comando genera y paquetes de aplicación en un archivo .jar de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="1633e-178">Cuando Hola comando finalice, hello `hbaseapp/target` directorio contiene un archivo denominado `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="1633e-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1633e-179">Hola `hbaseapp-1.0-SNAPSHOT.jar` archivo es un archivo jar de la misma.</span><span class="sxs-lookup"><span data-stu-id="1633e-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="1633e-180">Contiene todos los Hola dependencias toorun requiere la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1633e-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="1633e-181">Hola JAR de cargar y ejecutar trabajos (SSH)</span><span class="sxs-lookup"><span data-stu-id="1633e-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="1633e-182">Hola a consecuencia del uso de pasos `scp` toocopy Hola JAR toohello principal nodo principal de su HBase en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1633e-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="1633e-183">Hola `ssh` comando es, a continuación, usa tooconnect toohello clúster y ejecutar el ejemplo de Hola directamente en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="1633e-184">tooupload Hola jar toohello clúster Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="1633e-185">Reemplace `USERNAME` con el nombre de Hola de su inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="1633e-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="1633e-186">Reemplace `CLUSTERNAME` por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1633e-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="1633e-187">clúster de HBase de toohello tooconnect, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="1633e-188">Reemplace `USERNAME` nombre hello del inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="1633e-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="1633e-189">Reemplace `CLUSTERNAME` por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1633e-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="1633e-190">toocreate una tabla HBase mediante Hola aplicación Java, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="1633e-191">Este comando crea una tabla HBase denominada **people**, que se rellenará con datos.</span><span class="sxs-lookup"><span data-stu-id="1633e-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="1633e-192">toosearch para las direcciones de correo electrónico almacenado en tabla hello, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="1633e-193">Recepción Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="1633e-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="1633e-194">tabla de hello toodelete, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="1633e-195">Hola JAR de cargar y ejecutar trabajos (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="1633e-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="1633e-196">Hola pasos usa almacenamiento de Azure PowerShell tooupload Hola JAR toohello predeterminado para el clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="1633e-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="1633e-197">Cmdlets de HDInsight son toorun usado Hola ejemplos de forma remota.</span><span class="sxs-lookup"><span data-stu-id="1633e-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="1633e-198">Tras instalar y configurar Azure PowerShell, cree un archivo denominado `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="1633e-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="1633e-199">Usar hello después de texto como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="1633e-199">Use hello following text as hello contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="1633e-200">Este archivo contiene dos módulos:</span><span class="sxs-lookup"><span data-stu-id="1633e-200">This file contains two modules:</span></span>

   * <span data-ttu-id="1633e-201">**HDInsightFile agregar** : se usan clústeres de tooupload archivos toohello</span><span class="sxs-lookup"><span data-stu-id="1633e-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="1633e-202">**Start-HBaseExample** -toorun Hola clases creadas anteriormente usadas</span><span class="sxs-lookup"><span data-stu-id="1633e-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="1633e-203">Guardar hello `hbase-runner.psm1` archivo.</span><span class="sxs-lookup"><span data-stu-id="1633e-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="1633e-204">Abra una nueva ventana de PowerShell de Azure, cambie los directorios toohello `hbaseapp` directory, y, a continuación, Hola ejecución siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="1633e-205">Cambiar ubicación de toohello de ruta de acceso de Hola de hello `hbase-runner.psm1` archivo creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1633e-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="1633e-206">Este comando registra el módulo de hello con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1633e-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="1633e-207">Siguiente Hola de uso del comando hello tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour clúster.</span><span class="sxs-lookup"><span data-stu-id="1633e-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="1633e-208">Reemplace `hdinsightclustername` con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="1633e-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="1633e-209">comando Hello carga hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` ubicación de almacenamiento principal de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="1633e-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="1633e-210">Hola toocreate una tabla mediante `hbaseapp`, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="1633e-211">Reemplace `hdinsightclustername` con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="1633e-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="1633e-212">Con este comando se crea una tabla denominada **people** en HBase en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1633e-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="1633e-213">Este comando no muestra ningún resultado en la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="1633e-214">toosearch para las entradas de tabla de hello, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1633e-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="1633e-215">Reemplace `hdinsightclustername` con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="1633e-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="1633e-216">Este comando usa hello `SearchByEmail` clase toosearch para todas las filas donde hello `contactinformation` hello y familia de columna `email` columna, contiene la cadena hello `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="1633e-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="1633e-217">Debería recibir Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="1633e-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="1633e-218">Usando **fabrikam.com** para hello `-emailRegex` valor devuelve los usuarios de Hola que tienen **fabrikam.com** en el campo de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="1633e-219">También puede utilizar expresiones regulares como término de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="1633e-220">Por ejemplo, **^ r** devuelve las direcciones que comienzan con la letra "r" de Hola de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1633e-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="1633e-221">Sin resultados o resultados inesperados al usar Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="1633e-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="1633e-222">Hola de uso `-showErr` parámetro tooview Hola los errores estándar (STDERR) que se genera al trabajo en ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="1633e-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="1633e-223">Eliminar tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="1633e-223">Delete hello table</span></span>

<span data-ttu-id="1633e-224">Cuando haya terminado con el ejemplo hello, usar hello después hello toodelete **personas** tabla utilizada en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1633e-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="1633e-225">__Desde una sesión `ssh`__:</span><span class="sxs-lookup"><span data-stu-id="1633e-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="1633e-226">__Desde Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="1633e-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="1633e-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1633e-227">Next steps</span></span>

[<span data-ttu-id="1633e-228">Obtenga información acerca de cómo toouse ardilla SQL con HBase</span><span class="sxs-lookup"><span data-stu-id="1633e-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
