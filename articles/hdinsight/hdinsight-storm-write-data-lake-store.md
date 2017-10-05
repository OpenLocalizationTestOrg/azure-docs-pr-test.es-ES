---
title: Escritura de Apache Storm en Storage o Data Lake Store - Azure HDInsight | Microsoft Docs
description: "Obtenga más información sobre cómo usar Apache Storm para escribir datos en almacenamiento compatible con HDFS para HDInsight. Azure Storage o Azure Data Lake Store proporcionan almacenamiento compatible con HDFS para HDInsight. En este documento y en el ejemplo relacionado se muestra cómo se puede usar el componente HfdfsBolt para escribir datos en el almacenamiento predeterminado de un clúster de HDInsight en Storm."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="0bef3-105">Escritura de datos en HDFS desde Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bef3-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="0bef3-106">Obtenga más información sobre cómo usar Storm para escribir datos en el almacenamiento compatible con HDFS que usa Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bef3-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="0bef3-107">HDInsight puede usar tanto Azure Storage como Azure Data Lake como almacenamiento compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="0bef3-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="0bef3-108">Storm proporciona un componente [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) que permite escribir datos en HDFS.</span><span class="sxs-lookup"><span data-stu-id="0bef3-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="0bef3-109">En este documento se proporciona información sobre cómo escribir datos en ambos tipos de almacenamiento desde HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="0bef3-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0bef3-110">La topología de ejemplo que se usa en este documento depende de componentes que se incluyen con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bef3-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="0bef3-111">Puede que sea necesario realizar alguna modificación para que funcione con Azure Data Lake Store al usarlo con otros clústeres de Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0bef3-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="0bef3-112">Obtención del código</span><span class="sxs-lookup"><span data-stu-id="0bef3-112">Get the code</span></span>

<span data-ttu-id="0bef3-113">El proyecto que contiene esta topología está disponible como descarga en [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="0bef3-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="0bef3-114">Para compilar este proyecto, necesitará la siguiente configuración para su entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="0bef3-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="0bef3-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="0bef3-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="0bef3-116">HDInsight 3.5 y versiones posteriores requieren Java 8.</span><span class="sxs-lookup"><span data-stu-id="0bef3-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="0bef3-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="0bef3-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="0bef3-118">Pueden establecer las siguientes variables de entorno al instalar Java y el JDK en la estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="0bef3-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="0bef3-119">Sin embargo, debe comprobar que existen y que contienen los valores correctos para su sistema.</span><span class="sxs-lookup"><span data-stu-id="0bef3-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="0bef3-120">`JAVA_HOME`: debe apuntar al directorio en el que esté instalado JDK.</span><span class="sxs-lookup"><span data-stu-id="0bef3-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="0bef3-121">`PATH`: debe contener las rutas de acceso siguientes:</span><span class="sxs-lookup"><span data-stu-id="0bef3-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="0bef3-122">`JAVA_HOME` (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="0bef3-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="0bef3-123">`JAVA_HOME\bin` (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="0bef3-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="0bef3-124">Directorio en el que esté instalado Maven.</span><span class="sxs-lookup"><span data-stu-id="0bef3-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="0bef3-125">Cómo usar HdfsBolt con HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bef3-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bef3-126">Antes de usar HdfsBolt con Storm en HDInsight, debe usar una acción de script para copiar los archivos .jar necesarios en `extpath` para Storm.</span><span class="sxs-lookup"><span data-stu-id="0bef3-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="0bef3-127">Para obtener más información, consulte la sección [Configuración del clúster](#configure).</span><span class="sxs-lookup"><span data-stu-id="0bef3-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="0bef3-128">HdfsBolt usa el esquema de archivo que usted proporcione para comprender cómo escribir datos en HDFS.</span><span class="sxs-lookup"><span data-stu-id="0bef3-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="0bef3-129">Con HDInsight, use uno de los siguientes esquemas:</span><span class="sxs-lookup"><span data-stu-id="0bef3-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="0bef3-130">`wasb://`: se usa con una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0bef3-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="0bef3-131">`adl://`: se usa con Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0bef3-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="0bef3-132">En la siguiente tabla se proporcionan ejemplos de cómo usar el esquema de archivos en diferentes casos:</span><span class="sxs-lookup"><span data-stu-id="0bef3-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="0bef3-133">Esquema</span><span class="sxs-lookup"><span data-stu-id="0bef3-133">Scheme</span></span> | <span data-ttu-id="0bef3-134">Notas</span><span class="sxs-lookup"><span data-stu-id="0bef3-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="0bef3-135">La cuenta de almacenamiento predeterminada es un contenedor de blobs de una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0bef3-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="0bef3-136">La cuenta de almacenamiento predeterminada es un directorio de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0bef3-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="0bef3-137">Durante la creación del clúster, especifique el directorio de Data Lake Store que sea la raíz del HDFS del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="0bef3-138">Por ejemplo, el directorio `/clusters/myclustername/`.</span><span class="sxs-lookup"><span data-stu-id="0bef3-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="0bef3-139">Cuenta de Azure Storage no predeterminada (adicional) asociada al clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="0bef3-140">Raíz de Data Lake Store que usa el clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="0bef3-141">El uso de este esquema permite acceder a datos que se encuentren fuera del directorio que contiene el sistema de archivos del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="0bef3-142">Para obtener más información, consulte la referencia de [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) en Apache.org.</span><span class="sxs-lookup"><span data-stu-id="0bef3-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="0bef3-143">Configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0bef3-143">Example configuration</span></span>

<span data-ttu-id="0bef3-144">El siguiente YAML es un fragmento del archivo `resources/writetohdfs.yaml` incluido en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0bef3-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="0bef3-145">Este archivo define la topología de Storm mediante el marco [Flux](https://storm.apache.org/releases/1.1.0/flux.html) para Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0bef3-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="0bef3-146">En este YAML se definen los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0bef3-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="0bef3-147">`syncPolicy`: define cuándo se sincronizan o vacían los archivos en el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="0bef3-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="0bef3-148">En este ejemplo, cada 1000 tuplas.</span><span class="sxs-lookup"><span data-stu-id="0bef3-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="0bef3-149">`fileNameFormat`: define la ruta de acceso y el patrón del nombre de archivo que se usarán al escribir archivos.</span><span class="sxs-lookup"><span data-stu-id="0bef3-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="0bef3-150">En este ejemplo, la ruta de acceso se proporciona durante el tiempo de ejecución con un filtro, y la extensión de archivo es `.txt`.</span><span class="sxs-lookup"><span data-stu-id="0bef3-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="0bef3-151">`recordFormat`: define el formato interno de los archivos escritos.</span><span class="sxs-lookup"><span data-stu-id="0bef3-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="0bef3-152">En este ejemplo, los campos están delimitados por el carácter `|`.</span><span class="sxs-lookup"><span data-stu-id="0bef3-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="0bef3-153">`rotationPolicy`: define cuándo se giran los archivos.</span><span class="sxs-lookup"><span data-stu-id="0bef3-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="0bef3-154">En este ejemplo no se realiza ningún giro.</span><span class="sxs-lookup"><span data-stu-id="0bef3-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="0bef3-155">`hdfs-bolt`: usa los componentes anteriores como parámetros de configuración para la clase `HdfsBolt`.</span><span class="sxs-lookup"><span data-stu-id="0bef3-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="0bef3-156">Para obtener más información sobre el marco Flux, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="0bef3-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="0bef3-157">Configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="0bef3-157">Configure the cluster</span></span>

<span data-ttu-id="0bef3-158">De manera predeterminada, Storm en HDInsight no incluye los componentes que usa HdfsBolt para la comunicación con Azure Storage o Data Lake Store en el parámetro classpath de Storm.</span><span class="sxs-lookup"><span data-stu-id="0bef3-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="0bef3-159">Use la siguiente acción de script para agregar dichos componentes al directorio `extlib` de Storm en su clúster:</span><span class="sxs-lookup"><span data-stu-id="0bef3-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="0bef3-160">| URI de script | Nodos en los que se aplicará| Parámetros | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, supervisor | Ninguno |</span><span class="sxs-lookup"><span data-stu-id="0bef3-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="0bef3-161">Para obtener más información sobre cómo usar este script con su clúster, consulte el documento [Personalización de clústeres de HDInsight mediante la acción de scripts](./hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0bef3-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="0bef3-162">Compilación y empaquetado de la topología</span><span class="sxs-lookup"><span data-stu-id="0bef3-162">Build and package the topology</span></span>

1. <span data-ttu-id="0bef3-163">Descargue el proyecto de ejemplo de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) en su entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="0bef3-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="0bef3-164">Desde un símbolo del sistema, un terminal o una sesión de shell, cambie los directorios a la raíz del proyecto descargado.</span><span class="sxs-lookup"><span data-stu-id="0bef3-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="0bef3-165">Para compilar y empaquetar la topología, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0bef3-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="0bef3-166">Al finalizar la compilación y el empaquetado, habrá un nuevo directorio denominado `target` con el archivo `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="0bef3-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="0bef3-167">Este archivo contiene la topología compilada.</span><span class="sxs-lookup"><span data-stu-id="0bef3-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="0bef3-168">Implementación y ejecución de la topología</span><span class="sxs-lookup"><span data-stu-id="0bef3-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="0bef3-169">Use el siguiente comando para copiar la topología en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bef3-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="0bef3-170">Reemplace **USER** por el nombre de usuario SSH que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="0bef3-171">Reemplace **CLUSTERNAME** por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="0bef3-172">Cuando se le solicite, escriba la contraseña que se usó al crear el usuario SSH del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="0bef3-173">Si usó una clave pública en lugar de una contraseña, tal vez tenga que usar el parámetro `-i` para especificar la ruta de acceso a la correspondiente clave privada.</span><span class="sxs-lookup"><span data-stu-id="0bef3-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0bef3-174">Para obtener más información sobre cómo usar `scp` con HDInsight, consulte [Conexión a través de SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0bef3-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0bef3-175">Una vez finalizada la carga, use lo siguiente para conectarse al clúster de HDInsight con SSH.</span><span class="sxs-lookup"><span data-stu-id="0bef3-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="0bef3-176">Reemplace **USER** por el nombre de usuario SSH que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="0bef3-177">Reemplace **CLUSTERNAME** por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="0bef3-178">Cuando se le solicite, escriba la contraseña que se usó al crear el usuario SSH del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="0bef3-179">Si usó una clave pública en lugar de una contraseña, tal vez tenga que usar el parámetro `-i` para especificar la ruta de acceso a la correspondiente clave privada.</span><span class="sxs-lookup"><span data-stu-id="0bef3-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="0bef3-180">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0bef3-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="0bef3-181">Una vez conectado, use el comando siguiente para crear un archivo denominado `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="0bef3-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="0bef3-182">Use el texto siguiente como contenido del archivo `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="0bef3-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="0bef3-183">En este ejemplo se da por supuesto que su clúster usa una cuenta de Azure Storage como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0bef3-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="0bef3-184">Si el clúster usa Azure Data Lake Store, use `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="0bef3-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="0bef3-185">Para guardar el archivo, use __Ctrl+X__, después __Y__ y, finalmente, presione __Intro__.</span><span class="sxs-lookup"><span data-stu-id="0bef3-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="0bef3-186">Los valores de este archivo establecen la URL de Data Lake Store y el nombre del directorio en el que se escriben los datos.</span><span class="sxs-lookup"><span data-stu-id="0bef3-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="0bef3-187">Use el comando siguiente para iniciar la topología:</span><span class="sxs-lookup"><span data-stu-id="0bef3-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="0bef3-188">Este comando inicia la topología con el marco de Flux enviándolo al nodo Nimbus del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="0bef3-189">La topología la define el archivo `writetohdfs.yaml` incluido en el jar.</span><span class="sxs-lookup"><span data-stu-id="0bef3-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="0bef3-190">El archivo `dev.properties` se pasa como un filtro y la topología lee los valores contenidos en el archivo.</span><span class="sxs-lookup"><span data-stu-id="0bef3-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="0bef3-191">Visualización de datos de salida</span><span class="sxs-lookup"><span data-stu-id="0bef3-191">View output data</span></span>

<span data-ttu-id="0bef3-192">Para ver los datos, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0bef3-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="0bef3-193">Se muestra una lista de los archivos que ha creado la topología.</span><span class="sxs-lookup"><span data-stu-id="0bef3-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="0bef3-194">La lista siguiente es un ejemplo de los datos devueltos por los comandos anteriores:</span><span class="sxs-lookup"><span data-stu-id="0bef3-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="0bef3-195">Detención de la topología</span><span class="sxs-lookup"><span data-stu-id="0bef3-195">Stop the topology</span></span>

<span data-ttu-id="0bef3-196">Las topologías de Storm se ejecutarán hasta que se detengan o se elimine el clúster.</span><span class="sxs-lookup"><span data-stu-id="0bef3-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="0bef3-197">Para detener la topología, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0bef3-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="0bef3-198">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="0bef3-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="0bef3-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0bef3-199">Next steps</span></span>

<span data-ttu-id="0bef3-200">Ahora que ya sabe usar Storm para escribir datos en Azure Storage y Azure Data Lake Store, descubra otros [ejemplos de Storm para HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0bef3-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

