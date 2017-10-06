---
title: aaaApache Storm escribir tooStorage/Data Lake Store - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola almacenamiento de Apache Storm toowrite toohello HDFS compatible para HDInsight. Almacén de Azure Data Lake o almacenamiento de Azure proporcionan almacenamiento de hello HDFS comptabile para HDInsight. Este documento y un ejemplo de Hola a asociado, muestran cómo se componente de hello HdfsBolt pueden toowrite usado toohello predeterminado almacenamiento de una tormenta en clúster de HDInsight."
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
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="9049a-105">Escribir tooHDFS desde Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9049a-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="9049a-106">Obtenga información acerca de cómo toouse Storm toowrite datos toohello almacenamiento compatible con HDFS utiliza Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9049a-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="9049a-107">HDInsight puede usar tanto Azure Storage como Azure Data Lake como almacenamiento compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="9049a-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="9049a-108">Storm proporciona un [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente que escribe datos tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="9049a-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="9049a-109">Este documento proporciona información sobre cómo escribir tooeither tipo de almacenamiento de hello HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="9049a-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9049a-110">ejemplo de Hola topología utilizada en este documento se basa en los componentes que se incluyen con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9049a-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="9049a-111">Puede requerir toowork modificación con almacén de Azure Data Lake cuando se usa con otros clústeres de Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="9049a-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="9049a-112">Obtener el código de hello</span><span class="sxs-lookup"><span data-stu-id="9049a-112">Get hello code</span></span>

<span data-ttu-id="9049a-113">proyecto de Hola que contiene esta topología está disponible como una descarga desde [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="9049a-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="9049a-114">toocompile este proyecto, deberá Hola siguiente configuración para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="9049a-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="9049a-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9049a-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="9049a-116">HDInsight 3.5 y versiones posteriores requieren Java 8.</span><span class="sxs-lookup"><span data-stu-id="9049a-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="9049a-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="9049a-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="9049a-118">Hello siguientes variables de entorno pueden establecerse cuando se instalación Java y Hola JDK en su estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="9049a-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="9049a-119">Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.</span><span class="sxs-lookup"><span data-stu-id="9049a-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="9049a-120">`JAVA_HOME`-debe apuntar toohello directorio donde hello JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="9049a-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="9049a-121">`PATH`-debe contener Hola siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="9049a-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="9049a-122">`JAVA_HOME`(o la ruta de acceso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="9049a-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="9049a-123">`JAVA_HOME\bin`(o la ruta de acceso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="9049a-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="9049a-124">directorio de Hola donde está instalado Maven.</span><span class="sxs-lookup"><span data-stu-id="9049a-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="9049a-125">¿Cómo toouse Hola HdfsBolt con HDInsight</span><span class="sxs-lookup"><span data-stu-id="9049a-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9049a-126">Antes de usar hello HdfsBolt con Storm en HDInsight, primero debe usar un archivos jar de script acción toocopy necesario en hello `extpath` para Storm.</span><span class="sxs-lookup"><span data-stu-id="9049a-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="9049a-127">Para obtener más información, vea hello [configurar clústeres de hello](#configure) sección.</span><span class="sxs-lookup"><span data-stu-id="9049a-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="9049a-128">Hola HdfsBolt utiliza el esquema de archivo de Hola que proporcione cómo toounderstand toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="9049a-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="9049a-129">Con HDInsight, utilice uno de hello siguientes esquemas:</span><span class="sxs-lookup"><span data-stu-id="9049a-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="9049a-130">`wasb://`: se usa con una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9049a-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="9049a-131">`adl://`: se usa con Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9049a-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="9049a-132">Hello tabla siguiente proporciona ejemplos de uso de archivos de esquema de Hola para diferentes escenarios:</span><span class="sxs-lookup"><span data-stu-id="9049a-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="9049a-133">Esquema</span><span class="sxs-lookup"><span data-stu-id="9049a-133">Scheme</span></span> | <span data-ttu-id="9049a-134">Notas</span><span class="sxs-lookup"><span data-stu-id="9049a-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="9049a-135">cuenta de almacenamiento predeterminada de Hello es un contenedor de blob en una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="9049a-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="9049a-136">cuenta de almacenamiento predeterminada de Hello es un directorio en el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="9049a-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="9049a-137">Durante la creación del clúster, debe especificar el directorio de hello en el almacén de Data Lake es Hola raíz HDFS del clúster de hello.</span><span class="sxs-lookup"><span data-stu-id="9049a-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="9049a-138">Por ejemplo, hello `/clusters/myclustername/` directory.</span><span class="sxs-lookup"><span data-stu-id="9049a-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="9049a-139">Una cuenta de almacenamiento de Azure (adicional) no predeterminado asociada con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="9049a-140">raíz de Hola de hello usa Hola clúster de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="9049a-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="9049a-141">Este esquema permite tooaccess datos que se encuentran fuera del directorio de Hola que contiene el sistema de archivos del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="9049a-142">Para obtener más información, vea hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) referencia en Apache.org.</span><span class="sxs-lookup"><span data-stu-id="9049a-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="9049a-143">Configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9049a-143">Example configuration</span></span>

<span data-ttu-id="9049a-144">Hola YAML siguiente es un extracto de hello `resources/writetohdfs.yaml` archivo incluido en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="9049a-145">Este archivo define la topología de aluvión de hello mediante hello [flujo](https://storm.apache.org/releases/1.1.0/flux.html) framework para Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="9049a-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="9049a-146">Este YAML define Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9049a-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="9049a-147">`syncPolicy`: Defina cuándo archivos de sistema de archivos toohello sincronizado/vaciados.</span><span class="sxs-lookup"><span data-stu-id="9049a-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="9049a-148">En este ejemplo, cada 1000 tuplas.</span><span class="sxs-lookup"><span data-stu-id="9049a-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="9049a-149">`fileNameFormat`: Define toouse de patrón de nombre de ruta de acceso y Hola al escribir archivos.</span><span class="sxs-lookup"><span data-stu-id="9049a-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="9049a-150">En este ejemplo, se proporciona la ruta de acceso de hello en tiempo de ejecución mediante un filtro y extensión de archivo hello es `.txt`.</span><span class="sxs-lookup"><span data-stu-id="9049a-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="9049a-151">`recordFormat`: Define el formato interno de Hola de archivos de hello escritos.</span><span class="sxs-lookup"><span data-stu-id="9049a-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="9049a-152">En este ejemplo, los campos están delimitados por hello `|` caracteres.</span><span class="sxs-lookup"><span data-stu-id="9049a-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="9049a-153">`rotationPolicy`: Define cuándo toorotate archivos.</span><span class="sxs-lookup"><span data-stu-id="9049a-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="9049a-154">En este ejemplo no se realiza ningún giro.</span><span class="sxs-lookup"><span data-stu-id="9049a-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="9049a-155">`hdfs-bolt`: Utiliza Hola componentes anteriores como parámetros de configuración para hello `HdfsBolt` clase.</span><span class="sxs-lookup"><span data-stu-id="9049a-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="9049a-156">Para obtener más información sobre el marco de trabajo de un flujo de hello, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="9049a-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="9049a-157">Configuración de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="9049a-157">Configure hello cluster</span></span>

<span data-ttu-id="9049a-158">De forma predeterminada, Storm en HDInsight no incluye los componentes de hello HdfsBolt utiliza toocommunicate con almacenamiento de Azure o almacén de Data Lake en classpath del aluvión.</span><span class="sxs-lookup"><span data-stu-id="9049a-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="9049a-159">Script de uso Hola siguiente acción tooadd estos toohello componentes `extlib` aluvión de directorio en el clúster:</span><span class="sxs-lookup"><span data-stu-id="9049a-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="9049a-160">| URI de script | Nodos tooapply a | Parámetros || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span><span class="sxs-lookup"><span data-stu-id="9049a-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="9049a-161">Para obtener información sobre el uso de esta secuencia de comandos con el clúster, vea hello [HDInsight personalizar clústeres mediante acciones de script](./hdinsight-hadoop-customize-cluster-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9049a-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="9049a-162">Compilar y empaquetar topología Hola</span><span class="sxs-lookup"><span data-stu-id="9049a-162">Build and package hello topology</span></span>

1. <span data-ttu-id="9049a-163">Descargar el proyecto de ejemplo de Hola de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="9049a-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="9049a-164">Desde un símbolo del sistema, terminal, o una sesión de shell, cambiar directorios toohello raíz de hello descarga proyecto.</span><span class="sxs-lookup"><span data-stu-id="9049a-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="9049a-165">toobuild y paquete Hola topología, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9049a-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="9049a-166">Una vez que se completa la compilación de Hola y el empaquetado, hay un directorio denominado `target`, que contiene un archivo denominado `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="9049a-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="9049a-167">Este archivo contiene la topología de hello compilado.</span><span class="sxs-lookup"><span data-stu-id="9049a-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="9049a-168">Implementar y ejecutar topología Hola</span><span class="sxs-lookup"><span data-stu-id="9049a-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="9049a-169">Usar hello después de clúster de HDInsight de toohello de topología de comando toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="9049a-170">Reemplace **usuario** con el nombre de usuario SSH de Hola que utilizó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="9049a-171">Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="9049a-172">Cuando se le solicite, escriba contraseña de hello usada al crear el usuario SSH de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="9049a-173">Si utiliza una clave pública en lugar de una contraseña, puede que necesite toouse hello `-i` parámetro toospecify Hola ruta de acceso toohello que coinciden con la clave privada.</span><span class="sxs-lookup"><span data-stu-id="9049a-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9049a-174">Para obtener más información sobre cómo usar `scp` con HDInsight, consulte [Conexión a través de SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9049a-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9049a-175">Una vez completada la carga de hello, utilice Hola después de clúster de HDInsight de toohello tooconnect mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="9049a-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="9049a-176">Reemplace **usuario** con el nombre de usuario SSH de Hola que utilizó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="9049a-177">Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="9049a-178">Cuando se le solicite, escriba contraseña de hello usada al crear el usuario SSH de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="9049a-179">Si utiliza una clave pública en lugar de una contraseña, puede que necesite toouse hello `-i` parámetro toospecify Hola ruta de acceso toohello que coinciden con la clave privada.</span><span class="sxs-lookup"><span data-stu-id="9049a-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="9049a-180">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9049a-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="9049a-181">Una vez conectado, use Hola comando siguiente toocreate un archivo denominado `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="9049a-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="9049a-182">Hola de uso después de texto como contenido de Hola de hello `dev.properties` archivo:</span><span class="sxs-lookup"><span data-stu-id="9049a-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="9049a-183">En este ejemplo se da por supuesto que su clúster usa una cuenta de almacenamiento de Azure como almacenamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="9049a-184">Si el clúster usa Azure Data Lake Store, use `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="9049a-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="9049a-185">archivo de hello toosave, use __Ctrl + X__, a continuación, __Y__y, finalmente, __ENTRAR__.</span><span class="sxs-lookup"><span data-stu-id="9049a-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="9049a-186">valores de Hello en este archivo establecen URL de almacén de Data Lake de Hola y el nombre del directorio de Hola que se escriben datos en.</span><span class="sxs-lookup"><span data-stu-id="9049a-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="9049a-187">Usar hello después de la topología de hello toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="9049a-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="9049a-188">Este comando inicia la topología de hello mediante el marco de un flujo de hello mediante el envío de nodo de Nimbus toohello de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="9049a-189">topología de Hello está definida por hello `writetohdfs.yaml` los archivos incluidos en el archivo jar de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="9049a-190">Hola `dev.properties` archivo se pasa como un filtro y se leen los valores de hello contenidos en el archivo hello topología Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="9049a-191">Visualización de datos de salida</span><span class="sxs-lookup"><span data-stu-id="9049a-191">View output data</span></span>

<span data-ttu-id="9049a-192">datos de hello tooview, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9049a-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="9049a-193">Se muestra una lista de archivos de hello creados por esta topología.</span><span class="sxs-lookup"><span data-stu-id="9049a-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="9049a-194">Hello lista siguiente es un ejemplo de datos de hello devuelto por los comandos anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="9049a-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="9049a-195">Detener la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="9049a-195">Stop hello topology</span></span>

<span data-ttu-id="9049a-196">Topologías de Storm ejecutan hasta que detenga o se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9049a-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="9049a-197">toostop Hola topología, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9049a-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="9049a-198">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="9049a-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="9049a-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9049a-199">Next steps</span></span>

<span data-ttu-id="9049a-200">Ahora que ha aprendido cómo toouse Storm toowrite tooAzure almacenamiento y almacén de Azure Data Lake, detectar otros [Storm ejemplos para HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9049a-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

