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
# <a name="build-java-applications-for-apache-hbase"></a>Compilar aplicaciones Java para Apache HBase

Obtenga información acerca de cómo toocreate una [HBase Apache](http://hbase.apache.org/) aplicación de Java. A continuación, usar aplicación hello con HBase en HDInsight de Azure.

Hola los pasos de este documento se usa [Maven](http://maven.apache.org/) proyecto hello toocreate y compilación. Maven es una herramienta de comprensión que permite el software de toobuild, documentación e informes para los proyectos de Java y la administración de proyectos de software.

> [!NOTE]
> Hello pasos de este documento se más recientemente probaron con 3.6 de HDInsight.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Requisitos

* [JDK de la plataforma Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior.

    > [!NOTE]
    > HDInsight 3.5 y las versiones posteriores necesitan Java 8. Las versiones anteriores de HDInsight requieren Java 7.

* [Maven](http://maven.apache.org/)

* [Un clúster de Azure HDInsight basado en Linux con HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > pasos de Hello en este documento se han probado con las versiones de clúster de HDInsight 3.4 y 3.5. valores predeterminados de Hello proporcionados en los ejemplos son para un clúster de HDInsight 3.5.

## <a name="create-hello-project"></a>Crear proyecto de Hola

1. Desde la línea de comandos de hello en el entorno de desarrollo, cambiar directorios toohello ubicación donde desea que project de hello toocreate, por ejemplo, `cd code\hbase`.

2. Hola de uso **mvn** comando, que se instala con Maven, hello toogenerate scaffolding para proyecto de Hola.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Si usa PowerShell, debe encerrar hello `-D` parámetros entre comillas dobles.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Este comando crea un directorio con el mismo nombre como Hola de hello **artifactID** parámetro (**hbaseapp** en este ejemplo.) Este directorio contiene Hola siguientes elementos:

   * **pom.XML**: Hola modelo de objetos de proyecto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contiene información y configuración detalles usados toobuild hello en el proyecto.
   * **src**: directorio de Hola que contiene Hola **principal/java/com/microsoft/ejemplos** directorio, donde crear aplicación hello.

3. Eliminar hello `src/test/java/com/microsoft/examples/apptest.java` archivo. No lo vamos a usar en este ejemplo.

## <a name="update-hello-project-object-model"></a>Actualizar Hola modelo de objetos de proyecto

1. Editar hello `pom.xml` de archivos y agregar Hola siguiente código dentro de hello `<dependencies>` sección:

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

    Esta sección indica dicho proyecto Hola debe **hbase cliente** y **phoenix core** componentes. En tiempo de compilación, estas dependencias se descargan del repositorio de Maven Hola predeterminado. Puede usar hello [búsqueda de repositorio Central de Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn más información acerca de esta dependencia.

   > [!IMPORTANT]
   > número de versión de Hola de hello hbase-cliente debe coincidir con la versión de Hola de HBase que se proporciona con el clúster de HDInsight. Usar hello siguiendo el número de versión correcto de tabla toofind Hola.

   | Versión del clúster de HDInsight | HBase versión toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 y 3.6 |1.1.2 |

    Para obtener más información sobre los componentes y las versiones de HDInsight, vea [¿qué componentes de Hadoop diferentes de hello disponibles con HDInsight](hdinsight-component-versioning.md).

3. Agregar Hola después código toohello **pom.xml** archivo. Este texto debe estar dentro de hello `<project>...</project>` hello las etiquetas de archivos, por ejemplo, entre `</dependencies>` y `</project>`.

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

    Esta sección configura un recurso (`conf/hbase-site.xml`) que contiene información de configuración de HBase.

   > [!NOTE]
   > También puede establecer los valores de configuración mediante código. Vea los comentarios de Hola Hola `CreateTable` ejemplo.

    En esta sección también configura hello [Maven compilador complemento](http://maven.apache.org/plugins/maven-compiler-plugin/) y [Maven tono complemento](http://maven.apache.org/plugins/maven-shade-plugin/). compilador de saludo complemento es toocompile usado Hola topología. sombra de Hello complemento es duplicación de licencia tooprevent usado en paquete de archivo JAR de hello Maven compilada. Este complemento es un error "Duplicar archivos de licencia" de tooprevent utilizado en tiempo de ejecución en el clúster de HDInsight Hola. Mediante el complemento de sombreado de maven con hello `ApacheLicenseResourceTransformer` implementación evita que el error de Hola.

    Hola maven-sombra-plugin también genera un archivo jar de misma que contiene todas las dependencias de hello requeridas por la aplicación hello.

4. Guardar hello `pom.xml` archivo.

5. Cree un directorio denominado `conf` en hello `hbaseapp` directory. Este directorio es la información de configuración de toohold usado para conectar tooHBase.

6. Siguiente Hola de uso del comando toocopy configuración de HBase Hola de toohello de clúster de HBase Hola `conf` directory. Reemplace `USERNAME` con el nombre de Hola de su inicio de sesión SSH. Reemplace `CLUSTERNAME` por el nombre del clúster de HDInsight:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Para más información sobre cómo usar `ssh` y `scp`, vea [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Crear aplicación hello

1. Vaya toohello `hbaseapp/src/main/java/com/microsoft/examples` directorio y el nombre hello app.java archivo demasiado`CreateTable.java`.

2. Abra hello `CreateTable.java` archivo y reemplazar contenido existente de hello con hello después de texto:

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

    Este código es hello **CreateTable** (clase), que crea una tabla denominada **personas** y rellenarlo con algunos usuarios predefinidos.

3. Guardar hello `CreateTable.java` archivo.

4. Hola `hbaseapp/src/main/java/com/microsoft/examples` directorio, cree un archivo denominado `SearchByEmail.java`. Usar hello después de texto como contenido de Hola de este archivo:

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

    Hola **SearchByEmail** clase puede ser tooquery usado para las filas por dirección de correo electrónico. Porque utiliza un filtro de expresión regular, puede proporcionar una cadena o una expresión regular cuando se usa la clase hello.

5. Guardar hello `SearchByEmail.java` archivo.

6. Hola `hbaseapp/src/main/hava/com/microsoft/examples` directorio, cree un archivo denominado `DeleteTable.java`. Usar hello después de texto como contenido de Hola de este archivo:

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

    Esta clase limpia Hola tablas HBase creadas en este ejemplo, al deshabilitar y quitar tabla Hola creadas por hello `CreateTable` clase.

7. Guardar hello `DeleteTable.java` archivo.

## <a name="build-and-package-hello-application"></a>Compilación y paquete de aplicación hello

1. De hello `hbaseapp` directorio, el comando de uso Hola siguiente toobuild un archivo JAR que contiene la aplicación hello:

    ```bash
    mvn clean package
    ```

    Este comando genera y paquetes de aplicación en un archivo .jar de Hola.

2. Cuando Hola comando finalice, hello `hbaseapp/target` directorio contiene un archivo denominado `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Hola `hbaseapp-1.0-SNAPSHOT.jar` archivo es un archivo jar de la misma. Contiene todos los Hola dependencias toorun requiere la aplicación hello.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Hola JAR de cargar y ejecutar trabajos (SSH)

Hola a consecuencia del uso de pasos `scp` toocopy Hola JAR toohello principal nodo principal de su HBase en clúster de HDInsight. Hola `ssh` comando es, a continuación, usa tooconnect toohello clúster y ejecutar el ejemplo de Hola directamente en el nodo principal de Hola.

1. tooupload Hola jar toohello clúster Hola de uso siguiente comando:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Reemplace `USERNAME` con el nombre de Hola de su inicio de sesión SSH. Reemplace `CLUSTERNAME` por el nombre del clúster de HDInsight.

2. clúster de HBase de toohello tooconnect, Hola de uso siguiente comando:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Reemplace `USERNAME` nombre hello del inicio de sesión SSH. Reemplace `CLUSTERNAME` por el nombre del clúster de HDInsight.

3. toocreate una tabla HBase mediante Hola aplicación Java, Hola de uso siguiente comando:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    Este comando crea una tabla HBase denominada **people**, que se rellenará con datos.

4. toosearch para las direcciones de correo electrónico almacenado en tabla hello, Hola de uso siguiente comando:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Recepción Hola siguientes resultados:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. tabla de hello toodelete, Hola de uso siguiente comando:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Hola JAR de cargar y ejecutar trabajos (PowerShell)

Hola pasos usa almacenamiento de Azure PowerShell tooupload Hola JAR toohello predeterminado para el clúster de HBase. Cmdlets de HDInsight son toorun usado Hola ejemplos de forma remota.

1. Tras instalar y configurar Azure PowerShell, cree un archivo denominado `hbase-runner.psm1`. Usar hello después de texto como contenido de Hola de este archivo:

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

    Este archivo contiene dos módulos:

   * **HDInsightFile agregar** : se usan clústeres de tooupload archivos toohello
   * **Start-HBaseExample** -toorun Hola clases creadas anteriormente usadas

2. Guardar hello `hbase-runner.psm1` archivo.

3. Abra una nueva ventana de PowerShell de Azure, cambie los directorios toohello `hbaseapp` directory, y, a continuación, Hola ejecución siguiente comando:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Cambiar ubicación de toohello de ruta de acceso de Hola de hello `hbase-runner.psm1` archivo creado anteriormente. Este comando registra el módulo de hello con Azure PowerShell.

4. Siguiente Hola de uso del comando hello tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour clúster.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Reemplace `hdinsightclustername` con nombre hello del clúster. comando Hello carga hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` ubicación de almacenamiento principal de hello para el clúster.

5. Hola toocreate una tabla mediante `hbaseapp`, usar hello siguiente comando:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Reemplace `hdinsightclustername` con nombre hello del clúster.

    Con este comando se crea una tabla denominada **people** en HBase en el clúster de HDInsight. Este comando no muestra ningún resultado en la ventana de la consola de Hola.

6. toosearch para las entradas de tabla de hello, Hola de uso siguiente comando:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Reemplace `hdinsightclustername` con nombre hello del clúster.

    Este comando usa hello `SearchByEmail` clase toosearch para todas las filas donde hello `contactinformation` hello y familia de columna `email` columna, contiene la cadena hello `contoso.com`. Debería recibir Hola siguientes resultados:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Usando **fabrikam.com** para hello `-emailRegex` valor devuelve los usuarios de Hola que tienen **fabrikam.com** en el campo de correo electrónico de Hola. También puede utilizar expresiones regulares como término de búsqueda de Hola. Por ejemplo, **^ r** devuelve las direcciones que comienzan con la letra "r" de Hola de correo electrónico.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Sin resultados o resultados inesperados al usar Start-HBaseExample

Hola de uso `-showErr` parámetro tooview Hola los errores estándar (STDERR) que se genera al trabajo en ejecución Hola.

## <a name="delete-hello-table"></a>Eliminar tabla de Hola

Cuando haya terminado con el ejemplo hello, usar hello después hello toodelete **personas** tabla utilizada en este ejemplo:

__Desde una sesión `ssh`__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Desde Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Pasos siguientes

[Obtenga información acerca de cómo toouse ardilla SQL con HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
