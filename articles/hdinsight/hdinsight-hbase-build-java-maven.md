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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Utilizar aplicaciones de Java de toobuild de Maven que usan HBase con HDInsight basados en Windows (Hadoop)
Obtenga información acerca de cómo toocreate y generar un [HBase Apache](http://hbase.apache.org/) aplicación en Java con Apache Maven. A continuación, usar aplicación hello con Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) es una herramienta proyectos de software de administración y comprensión que le permite toobuild software, documentación e informes para los proyectos de Java. En este artículo, aprenderá cómo toouse se toocreate una aplicación básica de Java que crea, consulta y elimina un HBase de tabla en un clúster de HDInsight de Azure.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Windows. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Requisitos
* [JDK de la plataforma Java 7](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior
* [Maven](http://maven.apache.org/)
* Un clúster de HDInsight basado en Windows con HBase

    > [!NOTE]
    > pasos de Hello en este documento se han probado con las versiones de clúster de HDInsight 3.2 y 3.3. valores predeterminados de Hello proporcionados en los ejemplos son para un clúster de HDInsight 3.3.

## <a name="create-hello-project"></a>Crear proyecto de Hola
1. Desde la línea de comandos de hello en el entorno de desarrollo, cambiar directorios toohello ubicación donde desea que project de hello toocreate, por ejemplo, `cd code\hdinsight`.
2. Hola de uso **mvn** comando, que se instala con Maven, hello toogenerate scaffolding para proyecto de Hola.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Este comando crea un directorio en la ubicación actual de hello, con nombre de hello especificado por hello **artifactID** parámetro (**hbaseapp** en este ejemplo.) Este directorio contiene Hola siguientes elementos:

   * **pom.XML**: Hola modelo de objetos de proyecto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene información y configuración detalles usados toobuild hello en el proyecto.
   * **src**: directorio de Hola que contiene Hola **main\java\com\microsoft\examples** directorio, donde creará la aplicación hello.
3. Eliminar hello **src\test\java\com\microsoft\examples\apptest.java** el archivo porque no se utiliza en este ejemplo.

## <a name="update-hello-project-object-model"></a>Actualizar Hola modelo de objetos de proyecto
1. Editar hello **pom.xml** de archivos y agregar Hola siguiente código dentro de hello `<dependencies>` sección:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    Esta sección se explica Maven que Hola proyecto requiere **hbase cliente** versión **1.1.2**. En tiempo de compilación, esta dependencia se descarga del repositorio de Maven de Hola de forma predeterminada. Puede usar hello [búsqueda de repositorio Central de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn más información acerca de esta dependencia.

   > [!IMPORTANT]
   > número de versión de Hola debe coincidir con la versión de Hola de HBase que se proporciona con el clúster de HDInsight. Usar hello siguiendo el número de versión correcto de tabla toofind Hola.
   >
   >

   | Versión del clúster de HDInsight | HBase versión toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Para obtener más información sobre los componentes y las versiones de HDInsight, vea [¿qué componentes de Hadoop diferentes de hello disponibles con HDInsight](hdinsight-component-versioning.md).
2. Si está usando un clúster de HDInsight 3.3, también debe agregar Hola después toohello `<dependencies>` sección:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Esta dependencia cargará los componentes de núcleo de phoenix hello, que son usados por la versión de Hbase 1.1.x.
3. Agregar Hola después código toohello **pom.xml** archivo. Esta sección debe estar dentro de hello `<project>...</project>` hello las etiquetas de archivos, por ejemplo, entre `</dependencies>` y `</project>`.

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

    Hola `<resources>` sección configura un recurso (**conf\hbase-site.xml**) que contiene información de configuración de HBase.

   > [!NOTE]
   > También puede establecer los valores de configuración mediante código. Vea los comentarios de Hola Hola **CreateTable** ejemplo siguiente para saber cómo toodo esto.
   >
   >

    Esto `<plugins>` sección configura hello [Maven compilador complemento](http://maven.apache.org/plugins/maven-compiler-plugin/) y [Maven tono complemento](http://maven.apache.org/plugins/maven-shade-plugin/). compilador de saludo complemento es toocompile usado Hola topología. sombra de Hello complemento es duplicación de licencia tooprevent usado en paquete de archivo JAR de hello Maven compilada. motivo de Hola se utiliza es que los archivos de licencia duplicados de hello producirá un error en tiempo de ejecución en el clúster de HDInsight Hola. Mediante el complemento de sombreado de maven con hello `ApacheLicenseResourceTransformer` implementación evita que este error.

    Hello complemento de sombreado de maven también genera una misma jar (o jar fat) que contiene todas las dependencias de hello requeridas por la aplicación hello.
4. Guardar hello **pom.xml** archivo.
5. Crear un nuevo directorio denominado **conf** en hello **hbaseapp** directory. Hola **conf** directorio, cree un archivo denominado **hbase-site.xml**. Utilice el siguiente de hello como contenido de Hola de archivo hello:

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

    Este archivo será la configuración de HBase de hello tooload usado para un clúster de HDInsight.

   > [!NOTE]
   > Este es un archivo de hbase-site.xml mínimo y contiene valores mínimos reconstrucción de hello para el clúster de HDInsight de Hola.

6. Guardar hello **hbase-site.xml** archivo.

## <a name="create-hello-application"></a>Crear aplicación hello
1. Vaya toohello **hbaseapp\src\main\java\com\microsoft\examples** directorio y el nombre hello app.java archivo demasiado**CreateTable.java**.
2. Abra hello **CreateTable.java** archivo y reemplazar contenido existente de Hola con hello siguiente código:

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

    Se trata de hello **CreateTable** (clase), lo cual creará una tabla denominada **personas** y rellenarlo con algunos usuarios predefinidos.
3. Guardar hello **CreateTable.java** archivo.
4. Hola **hbaseapp\src\main\java\com\microsoft\examples** directorio, cree un nuevo archivo denominado **SearchByEmail.java**. Usar hello siguiente código como contenido de Hola de este archivo:

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

    Hola **SearchByEmail** clase puede ser tooquery usado para las filas por dirección de correo electrónico. Porque utiliza un filtro de expresión regular, puede proporcionar una cadena o una expresión regular cuando se usa la clase hello.
5. Guardar hello **SearchByEmail.java** archivo.
6. Hola **hbaseapp\src\main\hava\com\microsoft\examples** directorio, cree un nuevo archivo denominado **DeleteTable.java**. Usar hello siguiente código como contenido de Hola de este archivo:

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

    Esta clase es para limpiar en este ejemplo, al deshabilitar y quitar tabla Hola creó hello **CreateTable** clase.
7. Guardar hello **DeleteTable.java** archivo.

## <a name="build-and-package-hello-application"></a>Compilación y paquete de aplicación hello
1. Abra un símbolo del sistema y cambie los directorios toohello **hbaseapp** directory.
2. Usar hello después comando toobuild un archivo JAR que contiene la aplicación hello:

        mvn clean package

    Esto limpia los artefactos de compilación anterior, descarga las dependencias que todavía no se ha instalado, a continuación, compila y empaqueta la aplicación hello.
3. Cuando Hola comando finalice, hello **hbaseapp\target** directorio contiene un archivo denominado **hbaseapp-1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > Hola **hbaseapp-1.0-SNAPSHOT.jar** archivo es una misma jar (también conocido como un archivo jar fat,) que contiene todas las dependencias de hello necesario aplicación hello de toorun.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Cargar archivo JAR de hello e iniciar un trabajo
Hay muchas tooupload formas un clúster de HDInsight tooyour de archivos, como se describe en [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md). Hello pasos siguientes utilizan Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Tras instalar y configurar Azure PowerShell, cree un nuevo archivo llamado **hbase-runner.psm1**. Utilice el siguiente de hello como contenido de Hola de este archivo:

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

    Este archivo contiene dos módulos:

   * **Agregar-HDInsightFile** -usa tooupload archivos tooHDInsight
   * **Start-HBaseExample** -toorun Hola clases creadas anteriormente usadas
2. Guardar hello **hbase runner.psm1** archivo.
3. Abra una nueva ventana de PowerShell de Azure, cambie los directorios toohello **hbaseapp** directory, y, a continuación, Hola ejecución siguiente comando.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Cambiar ubicación de toohello de ruta de acceso de Hola de hello **hbase runner.psm1** archivo creado anteriormente. Esto registra el módulo de Hola para esta sesión de PowerShell de Azure.
4. Siguiente Hola de uso del comando hello tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour clúster de HDInsight.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight. comando Hello carga hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **ejemplo/JAR** ubicación de almacenamiento principal de hello para el clúster de HDInsight.
5. Una vez cargados los archivos de hello, use Hola de código siguiente toocreate una tabla mediante hello **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.

    Este comando creará una nueva tabla llamada **people** en el clúster de HDInsight. Este comando no muestra ningún resultado en la ventana de la consola de Hola.
6. toosearch para las entradas de tabla de hello, Hola de uso siguiente comando:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.

    Este comando usa hello **SearchByEmail** clase toosearch para todas las filas donde hello **contactinformation** hello y familia de columna **correo electrónico** columna contiene la cadena de Hola **contoso.com**. Debería recibir Hola siguientes resultados:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Usando **fabrikam.com** para hello `-emailRegex` valor devuelve los usuarios de Hola que tienen **fabrikam.com** en el campo de correo electrónico de Hola. Puesto que esta búsqueda se implementa mediante un filtro basado en expresiones regular, también puede escribir expresiones regulares, como **^ r**, las entradas que devuelve donde correo electrónico Hola comienza con hello letra "r".

## <a name="delete-hello-table"></a>Eliminar tabla de Hola
Cuando haya terminado con el ejemplo hello, comando siguiente de Hola de uso de Hola Hola de toodelete de sesión de PowerShell de Azure **personas** tabla utilizada en este ejemplo:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Reemplace **hdinsightclustername** con el nombre de Hola de su clúster de HDInsight.

## <a name="troubleshooting"></a>Solución de problemas
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Sin resultados o resultados inesperados al usar Start-HBaseExample
Hola de uso `-showErr` parámetro tooview Hola los errores estándar (STDERR) que se genera al trabajo en ejecución Hola.
