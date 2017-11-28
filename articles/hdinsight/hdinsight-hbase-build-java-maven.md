---
title: "Compilación de una aplicación de Java HBase para clústeres de Azure HDInsight basados en Windows | Microsoft Docs"
description: "Aprenda a usar Apache Maven para compilar una aplicación de Apache HBase basada en Java e implementarla después en un clúster de HDInsight de Azure basado en Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 59c9af5a91b107e68a676f02fe5a936f955b22fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="1a924-103">Uso de Maven para compilar aplicaciones Java que utilicen HBase con HDInsight basado en Windows (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="1a924-103">Use Maven to build Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="1a924-104">Aprenda a crear y compilar una aplicación de [Apache HBase](http://hbase.apache.org/) en Java con Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="1a924-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="1a924-105">Luego use la aplicación con Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="1a924-105">Then use the application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="1a924-106">[Maven](http://maven.apache.org/) es una herramienta de administración y comprensión de proyectos de software que le permite compilar software, documentación e informes para proyectos Java.</span><span class="sxs-lookup"><span data-stu-id="1a924-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="1a924-107">En este artículo, aprenderá a usarla para crear una aplicación Java básica que crea, consulta y elimina una tabla de HBase en un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a924-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a924-108">Los pasos de este documento requieren un clúster de HDInsight con Windows.</span><span class="sxs-lookup"><span data-stu-id="1a924-108">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="1a924-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="1a924-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1a924-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1a924-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="1a924-111">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1a924-111">Requirements</span></span>
* <span data-ttu-id="1a924-112">[JDK de la plataforma Java 7](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior</span><span class="sxs-lookup"><span data-stu-id="1a924-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="1a924-113">Maven</span><span class="sxs-lookup"><span data-stu-id="1a924-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="1a924-114">Un clúster de HDInsight basado en Windows con HBase</span><span class="sxs-lookup"><span data-stu-id="1a924-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a924-115">Los pasos descritos en este documento se han probado con las versiones 3.2 y 3.3 del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-115">The steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="1a924-116">Los valores predeterminados proporcionados en los ejemplos corresponden a la versión 3.3 de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-116">The default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="1a924-117">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="1a924-117">Create the project</span></span>
1. <span data-ttu-id="1a924-118">Desde la línea de comandos de su entorno de desarrollo, cambie los directorios por la ubicación en la que desea crear el proyecto, por ejemplo, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="1a924-118">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="1a924-119">Use el comando **mvn** , que se instala con Maven, para generar el scaffolding del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1a924-119">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="1a924-120">Esta acción creará un directorio en el directorio actual, con el nombre especificado por el parámetro **artifactID** (**hbaseapp** en este ejemplo). Este directorio raíz contiene los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1a924-120">This command creates a directory in the current location, with the name specified by the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="1a924-121">**pom.xml**: el modelo de objetos de proyectos ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene la información y los detalles de configuración usados para compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1a924-121">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="1a924-122">**src**: directorio que a su vez contiene el directorio **main\java\com\microsoft\examples**, donde creará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a924-122">**src**: The directory that contains the **main\java\com\microsoft\examples** directory, where you will author the application.</span></span>
3. <span data-ttu-id="1a924-123">Elimine el archivo **src\test\java\com\microsoft\examples\apptest.java**, puesto que no se usará en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1a924-123">Delete the **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="1a924-124">Actualización del modelo de objetos de proyectos</span><span class="sxs-lookup"><span data-stu-id="1a924-124">Update the Project Object Model</span></span>
1. <span data-ttu-id="1a924-125">Edite el archivo **pom.xml** y agregue lo siguiente dentro de la sección `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="1a924-125">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="1a924-126">Esta sección le indica a Maven que el proyecto requiere la versión **1.1.2** de **hbase-client**.</span><span class="sxs-lookup"><span data-stu-id="1a924-126">This section tells Maven that the project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="1a924-127">En tiempo de compilación, esta dependencia se descarga del repositorio de Maven predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1a924-127">At compile time, this dependency is downloaded from the default Maven repository.</span></span> <span data-ttu-id="1a924-128">Puede usar la [búsqueda del repositorio central de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) para ver más información sobre esta dependencia.</span><span class="sxs-lookup"><span data-stu-id="1a924-128">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1a924-129">El número de versión debe coincidir con la versión de HBase que se proporciona con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-129">The version number must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="1a924-130">Utilice la siguiente tabla para buscar el número de versión correcto.</span><span class="sxs-lookup"><span data-stu-id="1a924-130">Use the following table to find the correct version number.</span></span>
   >
   >

   | <span data-ttu-id="1a924-131">Versión del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a924-131">HDInsight cluster version</span></span> | <span data-ttu-id="1a924-132">Versión de HBase que se va a utilizar</span><span class="sxs-lookup"><span data-stu-id="1a924-132">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="1a924-133">3.2</span><span class="sxs-lookup"><span data-stu-id="1a924-133">3.2</span></span> |<span data-ttu-id="1a924-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="1a924-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="1a924-135">3.3</span><span class="sxs-lookup"><span data-stu-id="1a924-135">3.3</span></span> |<span data-ttu-id="1a924-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="1a924-136">1.1.2</span></span> |

    <span data-ttu-id="1a924-137">Para obtener más información sobre las versiones de HDInsight y los componentes, consulte [¿Cuáles son los diferentes componentes de Hadoop disponibles con HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="1a924-137">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="1a924-138">Si está usando la versión 3.3 de un clúster de HDInsight, también debe agregar lo siguiente a la sección `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="1a924-138">If you are using an HDInsight 3.3 cluster, you must also add the following to the `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="1a924-139">Esta dependencia cargará los componentes principales de Phoenix, que utilizan la versión 1.1.x de Hbase.</span><span class="sxs-lookup"><span data-stu-id="1a924-139">This dependency will load the phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="1a924-140">Agregue el siguiente código al archivo **pom.xml**.</span><span class="sxs-lookup"><span data-stu-id="1a924-140">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="1a924-141">Esta sección debe estar dentro de las etiquetas `<project>...</project>` en el archivo; por ejemplo, entre `</dependencies>` y `</project>`.</span><span class="sxs-lookup"><span data-stu-id="1a924-141">This section must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="1a924-142">La sección `<resources>` configura un recurso (**conf\hbase-site.xml**) que contiene información de configuración para HBase.</span><span class="sxs-lookup"><span data-stu-id="1a924-142">The `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a924-143">También puede establecer los valores de configuración mediante código.</span><span class="sxs-lookup"><span data-stu-id="1a924-143">You can also set configuration values via code.</span></span> <span data-ttu-id="1a924-144">Vea los comentarios del ejemplo **CreateTable** que sigue para ver cómo hacer esto.</span><span class="sxs-lookup"><span data-stu-id="1a924-144">See the comments in the **CreateTable** example that follows for how to do this.</span></span>
   >
   >

    <span data-ttu-id="1a924-145">Esta sección `<plugins>` configura [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) y [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="1a924-145">This `<plugins>` section configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="1a924-146">El complemento compiler se usa para compilar la topología.</span><span class="sxs-lookup"><span data-stu-id="1a924-146">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="1a924-147">El complemento shade se usa para evitar la duplicación de licencias en el paquete JAR compilado por Maven.</span><span class="sxs-lookup"><span data-stu-id="1a924-147">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="1a924-148">La razón de usar este complemento es que los archivos de licencia duplicados pueden provocar un error en tiempo de ejecución en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-148">The reason this is used is that the duplicate license files cause an error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="1a924-149">El uso del complemento maven-shade-plugin con la implementación de `ApacheLicenseResourceTransformer` evita este error.</span><span class="sxs-lookup"><span data-stu-id="1a924-149">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="1a924-150">El complemento maven-shade-plugin también producirá un uberjar (o fatjar), que contiene todas las dependencias que necesita la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a924-150">The maven-shade-plugin also produces an uber jar (or fat jar) that contains all the dependencies required by the application.</span></span>
4. <span data-ttu-id="1a924-151">Guarde el archivo **pom.xml** .</span><span class="sxs-lookup"><span data-stu-id="1a924-151">Save the **pom.xml** file.</span></span>
5. <span data-ttu-id="1a924-152">Cree un nuevo directorio llamado **conf** en el directorio **hbaseapp**.</span><span class="sxs-lookup"><span data-stu-id="1a924-152">Create a new directory named **conf** in the **hbaseapp** directory.</span></span> <span data-ttu-id="1a924-153">En el directorio **conf**, cree un archivo llamado **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="1a924-153">In the **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="1a924-154">Use lo siguiente como contenido del archivo:</span><span class="sxs-lookup"><span data-stu-id="1a924-154">Use the following as the contents of the file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 The Apache Software Foundation
          *
          * Licensed to the Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See the NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  The ASF licenses this file
          * to you under the Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with the License.  You may obtain a copy of the License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed to in writing, software
          * distributed under the License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See the License for the specific language governing permissions and
          * limitations under the License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="1a924-155">Este archivo se usará para cargar la configuración de HBase de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-155">This file will be used to load the HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a924-156">Este es un archivo hbase-site.xml mínimo, que contiene la configuración básica elemental del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-156">This is a minimal hbase-site.xml file, and it contains the bare minimum settings for the HDInsight cluster.</span></span>

6. <span data-ttu-id="1a924-157">Guarde el archivo **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="1a924-157">Save the **hbase-site.xml** file.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="1a924-158">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1a924-158">Create the application</span></span>
1. <span data-ttu-id="1a924-159">Vaya al directorio **hbaseapp\src\main\java\com\microsoft\examples** y cambie el nombre del archivo app.java a **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="1a924-159">Go to the **hbaseapp\src\main\java\com\microsoft\examples** directory and rename the app.java file to **CreateTable.java**.</span></span>
2. <span data-ttu-id="1a924-160">Abra el archivo **CreateTable.java** y reemplace el contenido existente por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a924-160">Open the **CreateTable.java** file and replace the existing contents with the following code:</span></span>

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
            // The following sets the znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

            // create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // create the table...
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

            // Add each person to the table
            //   Use the `name` column family for the name
            //   Use the `contactinfo` column family for the email
            for (int i = 0; i< people.length; i++) {
              Put person = new Put(Bytes.toBytes(people[i][0]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
              person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
              table.put(person);
            }
            // flush commits and close the table
            table.flushCommits();
            table.close();
          }
        }

    <span data-ttu-id="1a924-161">Esta es la clase **CreateTable**, que creará una tabla llamada **people** y la rellenará con algunos usuarios predefinidos.</span><span class="sxs-lookup"><span data-stu-id="1a924-161">This is the **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="1a924-162">Guarde el archivo **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="1a924-162">Save the **CreateTable.java** file.</span></span>
4. <span data-ttu-id="1a924-163">En el directorio **hbaseapp\src\main\java\com\microsoft\examples**, cree un nuevo archivo denominado **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="1a924-163">In the **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="1a924-164">Use el siguiente código como contenido de este archivo:</span><span class="sxs-lookup"><span data-stu-id="1a924-164">Use the following code as the contents of this file:</span></span>

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

            // Use GenericOptionsParser to get only the parameters to the class
            // and not all the parameters passed (when using WebHCat for example)
            String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
            if (otherArgs.length != 1) {
              System.out.println("usage: [regular expression]");
              System.exit(-1);
            }

            // Open the table
            HTable table = new HTable(config, "people");

            // Define the family and qualifiers to be used
            byte[] contactFamily = Bytes.toBytes("contactinfo");
            byte[] emailQualifier = Bytes.toBytes("email");
            byte[] nameFamily = Bytes.toBytes("name");
            byte[] firstNameQualifier = Bytes.toBytes("first");
            byte[] lastNameQualifier = Bytes.toBytes("last");

            // Create a new regex filter
            RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
            // Attach the regex filter to a filter
            //   for the email column
            SingleColumnValueFilter filter = new SingleColumnValueFilter(
              contactFamily,
              emailQualifier,
              CompareOp.EQUAL,
              emailFilter
            );

            // Create a scan and set the filter
            Scan scan = new Scan();
            scan.setFilter(filter);

            // Get the results
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

    <span data-ttu-id="1a924-165">La clase **SearchByEmail** se puede usar para consultar filas por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1a924-165">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="1a924-166">Dado que esta clase usa un filtro de expresiones regulares, puede proporcionar una cadena o una expresión regular cuando la utilice.</span><span class="sxs-lookup"><span data-stu-id="1a924-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>
5. <span data-ttu-id="1a924-167">Guarde el archivo **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="1a924-167">Save the **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="1a924-168">En el directorio **hbaseapp\src\main\hava\com\microsoft\examples**, cree un nuevo archivo denominado **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="1a924-168">In the **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="1a924-169">Use el siguiente código como contenido de este archivo:</span><span class="sxs-lookup"><span data-stu-id="1a924-169">Use the following code as the contents of this file:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;

        public class DeleteTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // Disable, and then delete the table
            admin.disableTable("people");
            admin.deleteTable("people");
          }
        }

    <span data-ttu-id="1a924-170">Esta clase es solo para limpiar este ejemplo. Para ello, primero se deshabilita y luego se elimina la tabla creada por la clase **CreateTable**.</span><span class="sxs-lookup"><span data-stu-id="1a924-170">This class is for cleaning up this example by disabling and dropping the table created by the **CreateTable** class.</span></span>
7. <span data-ttu-id="1a924-171">Guarde el archivo **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="1a924-171">Save the **DeleteTable.java** file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="1a924-172">Compilación y empaquetado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1a924-172">Build and package the application</span></span>
1. <span data-ttu-id="1a924-173">Abra un símbolo del sistema y cambie los directorios por el directorio **hbaseapp**.</span><span class="sxs-lookup"><span data-stu-id="1a924-173">Open a command prompt and change directories to the **hbaseapp** directory.</span></span>
2. <span data-ttu-id="1a924-174">Use el siguiente comando para compilar un archivo JAR que contenga la aplicación:</span><span class="sxs-lookup"><span data-stu-id="1a924-174">Use the following command to build a JAR file that contains the application:</span></span>

        mvn clean package

    <span data-ttu-id="1a924-175">Esta acción eliminará los artefactos de compilación anteriores, descargará las dependencias que no se hayan instalado aún y luego compilará y empaquetará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a924-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span></span>
3. <span data-ttu-id="1a924-176">Cuando el comando termine de ejecutarse, el directorio **hbaseapp\target** contendrá un archivo llamado **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="1a924-176">When the command completes, the **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a924-177">El archivo **hbaseapp-1.0-SNAPSHOT.jar** es un uberjar (en ocasiones llamado fatjar) que contiene todas las dependencias necesarias para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a924-177">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all the dependencies required to run the application.</span></span>

## <a name="upload-the-jar-file-and-start-a-job"></a><span data-ttu-id="1a924-178">Carga del archivo JAR e inicio de un trabajo</span><span class="sxs-lookup"><span data-stu-id="1a924-178">Upload the JAR file and start a job</span></span>
<span data-ttu-id="1a924-179">Existen muchas formas de cargar un archivo en el clúster de HDInsight, tal y como se describe en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1a924-179">There are many ways to upload a file to your HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="1a924-180">En los siguientes pasos se usa Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a924-180">The following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="1a924-181">Tras instalar y configurar Azure PowerShell, cree un nuevo archivo llamado **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="1a924-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="1a924-182">Use el siguiente contenido para este archivo:</span><span class="sxs-lookup"><span data-stu-id="1a924-182">Use the following as the contents of this file:</span></span>

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
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
        #The class to run
        [Parameter(Mandatory = $true)]
        [String]$className,

        #The name of the HDInsight cluster
        [Parameter(Mandatory = $true)]
        [String]$clusterName,

        #Only used when using SearchByEmail
        [Parameter(Mandatory = $false)]
        [String]$emailRegex,

        #Use if you want to see stderr output
        [Parameter(Mandatory = $false)]
        [Switch]$showErr
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get the login for the HDInsight cluster
        $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

        # The JAR
        $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

        # The job definition
        $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
            -JarFile $jarFile `
            -ClassName $className `
            -Arguments $emailRegex

        # Get the job output
        $job = Start-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobDefinition $jobDefinition `
            -HttpCredential $creds
        Write-Host "Wait for the job to complete ..." -ForegroundColor Green
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
        Write-Host "Display the standard output ..." -ForegroundColor Green
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds
        }

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
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
                #The path to the local file.
                [Parameter(Mandatory = $true)]
                [String]$localPath,

                #The destination path and file name, relative to the root of the container.
                [Parameter(Mandatory = $true)]
                [String]$destinationPath,

                #The name of the HDInsight cluster
                [Parameter(Mandatory = $true)]
                [String]$clusterName,

                #If specified, overwrites existing files without prompting
                [Parameter(Mandatory = $false)]
                [Switch]$force
            )

            Set-StrictMode -Version 3

            # Is the Azure module installed?
            FindAzure

            # Get authentication for the cluster
            $creds=Get-Credential

            # Does the local path exist?
            if (-not (Test-Path $localPath))
            {
                throw "Source path '$localPath' does not exist."
            }

            # Get the primary storage container
            $storage = GetStorage -clusterName $clusterName

            # Upload file to storage, overwriting existing files if -force was used.
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
                throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
            }
        }

        function GetStorage {
            param(
                [Parameter(Mandatory = $true)]
                [String]$clusterName
            )
            $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
            # Does the cluster exist?
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
            # Get the resource group, in case we need that
            $return.resourceGroup = $resourceGroup
            # Get the storage context, as we can't depend
            # on using the default storage context
            $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
            # Get the container, so we know where to
            # find/store blobs
            $return.container = $container
            # Return storage accounts to support finding all accounts for
            # a cluster
            $return.storageAccount = $storageAccountName
            $return.storageAccountKey = $storageAccountKey

            return $return
        }
        # Only export the verb-phrase things
        export-modulemember *-*

    <span data-ttu-id="1a924-183">Este archivo contiene dos módulos:</span><span class="sxs-lookup"><span data-stu-id="1a924-183">This file contains two modules:</span></span>

   * <span data-ttu-id="1a924-184">**Add-HDInsightFile**: se usa para cargar archivos en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-184">**Add-HDInsightFile** - used to upload files to HDInsight</span></span>
   * <span data-ttu-id="1a924-185">**Start-HBaseExample**: se usa para ejecutar las clases creadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1a924-185">**Start-HBaseExample** - used to run the classes created earlier</span></span>
2. <span data-ttu-id="1a924-186">Guarde el archivo **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="1a924-186">Save the **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="1a924-187">Abra una nueva ventana de Azure PowerShell, cambie los directorios por el directorio **hbaseapp** y luego ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="1a924-187">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="1a924-188">Cambie la ruta de acceso a la ubicación del archivo **hbase-runner.psm1** creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1a924-188">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="1a924-189">Esta acción registrará el módulo para esta sesión de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a924-189">This registers the module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="1a924-190">Use el comando siguiente para cargar el archivo **hbaseapp-1.0-SNAPSHOT.jar** en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-190">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="1a924-191">Reemplace **hdinsightclustername** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-191">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="1a924-192">El comando cargará a continuación el archivo **hbaseapp-1.0-SNAPSHOT.jar** en la ubicación **example/jars** del almacenamiento principal del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-192">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="1a924-193">Una vez cargados los archivos, use el comando siguiente para crear una tabla con **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="1a924-193">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="1a924-194">Reemplace **hdinsightclustername** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-194">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="1a924-195">Este comando creará una nueva tabla llamada **people** en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="1a924-196">Este comando no muestra ninguna salida en la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="1a924-196">This command does not show any output in the console window.</span></span>
6. <span data-ttu-id="1a924-197">Para buscar entradas en la tabla, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1a924-197">To search for entries in the table, use the following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="1a924-198">Reemplace **hdinsightclustername** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-198">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="1a924-199">Este comando usa la clase **SearchByEmail** para buscar filas donde la familia de columnas **contactinformation** y la columna **email** contengan la cadena **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1a924-199">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span></span> <span data-ttu-id="1a924-200">Debe recibir los siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="1a924-200">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="1a924-201">Si se usa **fabrikam.com** como valor de `-emailRegex` se devolverán los usuarios que tienen **fabrikam.com** en el campo de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1a924-201">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="1a924-202">Dado que esta búsqueda se implementa usando un filtro basado en una expresión regular, también puede escribir expresiones regulares como **^r**, lo cual devuelve entradas en las que el correo electrónico empiece por la letra "r".</span><span class="sxs-lookup"><span data-stu-id="1a924-202">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where the email begins with the letter 'r'.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="1a924-203">Eliminación de la tabla</span><span class="sxs-lookup"><span data-stu-id="1a924-203">Delete the table</span></span>
<span data-ttu-id="1a924-204">Cuando haya terminado con el ejemplo, use el siguiente comando desde la sesión de Azure PowerShell para eliminar la tabla **people** usada en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1a924-204">When you are done with the example, use the following command from the Azure PowerShell session to delete the **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="1a924-205">Reemplace **hdinsightclustername** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a924-205">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1a924-206">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="1a924-206">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="1a924-207">Sin resultados o resultados inesperados al usar Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="1a924-207">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="1a924-208">Use el parámetro `-showErr` para ver el error estándar (STDERR) producido mientras se ejecutaba el trabajo.</span><span class="sxs-lookup"><span data-stu-id="1a924-208">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>
