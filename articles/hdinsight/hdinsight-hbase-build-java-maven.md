---
title: "una aplicación de Java HBase para HDInsight de Azure basado en Windows aaaBuild | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse aplicación de Apache HBase de Apache Maven toobuild basados en Java, a continuación, implementarlo tooa clúster de HDInsight de Azure basado en Windows."
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
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="bd9b9-103">Utilizar aplicaciones de Java de toobuild de Maven que usan HBase con HDInsight basados en Windows (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="bd9b9-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="bd9b9-104">Obtenga información acerca de cómo toocreate y generar un [HBase Apache](http://hbase.apache.org/) aplicación en Java con Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="bd9b9-105">A continuación, usar aplicación hello con Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="bd9b9-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="bd9b9-106">[Maven](http://maven.apache.org/) es una herramienta proyectos de software de administración y comprensión que le permite toobuild software, documentación e informes para los proyectos de Java.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="bd9b9-107">En este artículo, aprenderá cómo toouse se toocreate una aplicación básica de Java que crea, consulta y elimina un HBase de tabla en un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd9b9-108">pasos de Hello en este documento requieren un clúster de HDInsight que usa Windows.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="bd9b9-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bd9b9-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bd9b9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="bd9b9-111">Requisitos</span><span class="sxs-lookup"><span data-stu-id="bd9b9-111">Requirements</span></span>
* <span data-ttu-id="bd9b9-112">[JDK de la plataforma Java 7](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior</span><span class="sxs-lookup"><span data-stu-id="bd9b9-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="bd9b9-113">Maven</span><span class="sxs-lookup"><span data-stu-id="bd9b9-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="bd9b9-114">Un clúster de HDInsight basado en Windows con HBase</span><span class="sxs-lookup"><span data-stu-id="bd9b9-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd9b9-115">pasos de Hello en este documento se han probado con las versiones de clúster de HDInsight 3.2 y 3.3.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="bd9b9-116">valores predeterminados de Hello proporcionados en los ejemplos son para un clúster de HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="bd9b9-117">Crear proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="bd9b9-117">Create hello project</span></span>
1. <span data-ttu-id="bd9b9-118">Desde la línea de comandos de hello en el entorno de desarrollo, cambiar directorios toohello ubicación donde desea que project de hello toocreate, por ejemplo, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="bd9b9-119">Hola de uso **mvn** comando, que se instala con Maven, hello toogenerate scaffolding para proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="bd9b9-120">Este comando crea un directorio en la ubicación actual de hello, con nombre de hello especificado por hello **artifactID** parámetro (**hbaseapp** en este ejemplo.) Este directorio contiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="bd9b9-121">**pom.XML**: Hola modelo de objetos de proyecto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene información y configuración detalles usados toobuild hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="bd9b9-122">**src**: directorio de Hola que contiene Hola **main\java\com\microsoft\examples** directorio, donde creará la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="bd9b9-123">Eliminar hello **src\test\java\com\microsoft\examples\apptest.java** el archivo porque no se utiliza en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="bd9b9-124">Actualizar Hola modelo de objetos de proyecto</span><span class="sxs-lookup"><span data-stu-id="bd9b9-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="bd9b9-125">Editar hello **pom.xml** de archivos y agregar Hola siguiente código dentro de hello `<dependencies>` sección:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="bd9b9-126">Esta sección se explica Maven que Hola proyecto requiere **hbase cliente** versión **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="bd9b9-127">En tiempo de compilación, esta dependencia se descarga del repositorio de Maven de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="bd9b9-128">Puede usar hello [búsqueda de repositorio Central de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn más información acerca de esta dependencia.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="bd9b9-129">número de versión de Hola debe coincidir con la versión de Hola de HBase que se proporciona con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="bd9b9-130">Usar hello siguiendo el número de versión correcto de tabla toofind Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="bd9b9-131">Versión del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd9b9-131">HDInsight cluster version</span></span> | <span data-ttu-id="bd9b9-132">HBase versión toouse</span><span class="sxs-lookup"><span data-stu-id="bd9b9-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="bd9b9-133">3.2</span><span class="sxs-lookup"><span data-stu-id="bd9b9-133">3.2</span></span> |<span data-ttu-id="bd9b9-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="bd9b9-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="bd9b9-135">3.3</span><span class="sxs-lookup"><span data-stu-id="bd9b9-135">3.3</span></span> |<span data-ttu-id="bd9b9-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="bd9b9-136">1.1.2</span></span> |

    <span data-ttu-id="bd9b9-137">Para obtener más información sobre los componentes y las versiones de HDInsight, vea [¿qué componentes de Hadoop diferentes de hello disponibles con HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bd9b9-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="bd9b9-138">Si está usando un clúster de HDInsight 3.3, también debe agregar Hola después toohello `<dependencies>` sección:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="bd9b9-139">Esta dependencia cargará los componentes de núcleo de phoenix hello, que son usados por la versión de Hbase 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="bd9b9-140">Agregar Hola después código toohello **pom.xml** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="bd9b9-141">Esta sección debe estar dentro de hello `<project>...</project>` hello las etiquetas de archivos, por ejemplo, entre `</dependencies>` y `</project>`.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="bd9b9-142">Hola `<resources>` sección configura un recurso (**conf\hbase-site.xml**) que contiene información de configuración de HBase.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd9b9-143">También puede establecer los valores de configuración mediante código.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-143">You can also set configuration values via code.</span></span> <span data-ttu-id="bd9b9-144">Vea los comentarios de Hola Hola **CreateTable** ejemplo siguiente para saber cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="bd9b9-145">Esto `<plugins>` sección configura hello [Maven compilador complemento](http://maven.apache.org/plugins/maven-compiler-plugin/) y [Maven tono complemento](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="bd9b9-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="bd9b9-146">compilador de saludo complemento es toocompile usado Hola topología.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="bd9b9-147">sombra de Hello complemento es duplicación de licencia tooprevent usado en paquete de archivo JAR de hello Maven compilada.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="bd9b9-148">motivo de Hola se utiliza es que los archivos de licencia duplicados de hello producirá un error en tiempo de ejecución en el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="bd9b9-149">Mediante el complemento de sombreado de maven con hello `ApacheLicenseResourceTransformer` implementación evita que este error.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="bd9b9-150">Hello complemento de sombreado de maven también genera una misma jar (o jar fat) que contiene todas las dependencias de hello requeridas por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="bd9b9-151">Guardar hello **pom.xml** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="bd9b9-152">Crear un nuevo directorio denominado **conf** en hello **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="bd9b9-153">Hola **conf** directorio, cree un archivo denominado **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="bd9b9-154">Utilice el siguiente de hello como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
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

    <span data-ttu-id="bd9b9-155">Este archivo será la configuración de HBase de hello tooload usado para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd9b9-156">Este es un archivo de hbase-site.xml mínimo y contiene valores mínimos reconstrucción de hello para el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="bd9b9-157">Guardar hello **hbase-site.xml** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="bd9b9-158">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bd9b9-158">Create hello application</span></span>
1. <span data-ttu-id="bd9b9-159">Vaya toohello **hbaseapp\src\main\java\com\microsoft\examples** directorio y el nombre hello app.java archivo demasiado**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="bd9b9-160">Abra hello **CreateTable.java** archivo y reemplazar contenido existente de Hola con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="bd9b9-161">Se trata de hello **CreateTable** (clase), lo cual creará una tabla denominada **personas** y rellenarlo con algunos usuarios predefinidos.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="bd9b9-162">Guardar hello **CreateTable.java** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="bd9b9-163">Hola **hbaseapp\src\main\java\com\microsoft\examples** directorio, cree un nuevo archivo denominado **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="bd9b9-164">Usar hello siguiente código como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-164">Use hello following code as hello contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="bd9b9-165">Hola **SearchByEmail** clase puede ser tooquery usado para las filas por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="bd9b9-166">Porque utiliza un filtro de expresión regular, puede proporcionar una cadena o una expresión regular cuando se usa la clase hello.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="bd9b9-167">Guardar hello **SearchByEmail.java** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="bd9b9-168">Hola **hbaseapp\src\main\hava\com\microsoft\examples** directorio, cree un nuevo archivo denominado **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="bd9b9-169">Usar hello siguiente código como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="bd9b9-170">Esta clase es para limpiar en este ejemplo, al deshabilitar y quitar tabla Hola creó hello **CreateTable** clase.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="bd9b9-171">Guardar hello **DeleteTable.java** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="bd9b9-172">Compilación y paquete de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bd9b9-172">Build and package hello application</span></span>
1. <span data-ttu-id="bd9b9-173">Abra un símbolo del sistema y cambie los directorios toohello **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="bd9b9-174">Usar hello después comando toobuild un archivo JAR que contiene la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="bd9b9-175">Esto limpia los artefactos de compilación anterior, descarga las dependencias que todavía no se ha instalado, a continuación, compila y empaqueta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="bd9b9-176">Cuando Hola comando finalice, hello **hbaseapp\target** directorio contiene un archivo denominado **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd9b9-177">Hola **hbaseapp-1.0-SNAPSHOT.jar** archivo es una misma jar (también conocido como un archivo jar fat,) que contiene todas las dependencias de hello necesario aplicación hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="bd9b9-178">Cargar archivo JAR de hello e iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="bd9b9-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="bd9b9-179">Hay muchas tooupload formas un clúster de HDInsight tooyour de archivos, como se describe en [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="bd9b9-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="bd9b9-180">Hello pasos siguientes utilizan Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="bd9b9-181">Tras instalar y configurar Azure PowerShell, cree un nuevo archivo llamado **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="bd9b9-182">Utilice el siguiente de hello como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="bd9b9-183">Este archivo contiene dos módulos:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-183">This file contains two modules:</span></span>

   * <span data-ttu-id="bd9b9-184">**Agregar-HDInsightFile** -usa tooupload archivos tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="bd9b9-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="bd9b9-185">**Start-HBaseExample** -toorun Hola clases creadas anteriormente usadas</span><span class="sxs-lookup"><span data-stu-id="bd9b9-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="bd9b9-186">Guardar hello **hbase runner.psm1** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="bd9b9-187">Abra una nueva ventana de PowerShell de Azure, cambie los directorios toohello **hbaseapp** directory, y, a continuación, Hola ejecución siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="bd9b9-188">Cambiar ubicación de toohello de ruta de acceso de Hola de hello **hbase runner.psm1** archivo creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="bd9b9-189">Esto registra el módulo de Hola para esta sesión de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="bd9b9-190">Siguiente Hola de uso del comando hello tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="bd9b9-191">Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="bd9b9-192">comando Hello carga hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **ejemplo/JAR** ubicación de almacenamiento principal de hello para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="bd9b9-193">Una vez cargados los archivos de hello, use Hola de código siguiente toocreate una tabla mediante hello **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="bd9b9-194">Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="bd9b9-195">Este comando creará una nueva tabla llamada **people** en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="bd9b9-196">Este comando no muestra ningún resultado en la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="bd9b9-197">toosearch para las entradas de tabla de hello, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="bd9b9-198">Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="bd9b9-199">Este comando usa hello **SearchByEmail** clase toosearch para todas las filas donde hello **contactinformation** hello y familia de columna **correo electrónico** columna contiene la cadena de Hola **contoso.com**. Debería recibir Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="bd9b9-200">Usando **fabrikam.com** para hello `-emailRegex` valor devuelve los usuarios de Hola que tienen **fabrikam.com** en el campo de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="bd9b9-201">Puesto que esta búsqueda se implementa mediante un filtro basado en expresiones regular, también puede escribir expresiones regulares, como **^ r**, las entradas que devuelve donde correo electrónico Hola comienza con hello letra "r".</span><span class="sxs-lookup"><span data-stu-id="bd9b9-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="bd9b9-202">Eliminar tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="bd9b9-202">Delete hello table</span></span>
<span data-ttu-id="bd9b9-203">Cuando haya terminado con el ejemplo hello, comando siguiente de Hola de uso de Hola Hola de toodelete de sesión de PowerShell de Azure **personas** tabla utilizada en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd9b9-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="bd9b9-204">Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bd9b9-205">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="bd9b9-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="bd9b9-206">Sin resultados o resultados inesperados al usar Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="bd9b9-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="bd9b9-207">Hola de uso `-showErr` parámetro tooview Hola los errores estándar (STDERR) que se genera al trabajo en ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9b9-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
