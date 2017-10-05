---
title: Uso de Apache Kafka con Storm en HDInsight - Azure | Microsoft Docs
description: "Apache Kafka se instala con Apache Storm en HDInsight. Vea cómo escribir en Kafka y después leer de él con los componentes KafkaBolt y KafkaSpout proporcionados Storm. Aprenda también a usar el entorno de Flux para definir y enviar topologías de Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="f1a2d-105">Uso de Apache Kafka (versión preliminar) con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a2d-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="f1a2d-106">Obtenga información sobre cómo usar Apache Storm para leer y escribir en Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="f1a2d-107">En este ejemplo también se muestra cómo guardar datos de una topología de Storm en el sistema de archivos compatible con HDFS que usa HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="f1a2d-108">Los pasos que se describen en este documento crean un grupo de recursos de Azure que contiene un clúster Storm en HDInsight y un clúster Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="f1a2d-109">Estos dos clústeres se encuentran en una red virtual de Azure, lo que permite al clúster Storm comunicarse directamente con el clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="f1a2d-110">Cuando haya terminado los pasos indicados en este documento, no olvide eliminar los clústeres para evitar gastos innecesarios.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="f1a2d-111">Obtención del código</span><span class="sxs-lookup"><span data-stu-id="f1a2d-111">Get the code</span></span>

<span data-ttu-id="f1a2d-112">El código del ejemplo que se usa en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="f1a2d-113">Para compilar este proyecto, necesitará la siguiente configuración para su entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="f1a2d-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="f1a2d-115">HDInsight 3.5 y versiones posteriores requieren Java 8.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="f1a2d-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="f1a2d-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="f1a2d-117">Un cliente de SSH (precisa de los comandos `ssh` y `scp`). Para obtener información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="f1a2d-118">Un editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-118">A text editor or IDE.</span></span>

<span data-ttu-id="f1a2d-119">Pueden establecer las siguientes variables de entorno al instalar Java y el JDK en la estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="f1a2d-120">Sin embargo, debe comprobar que existen y que contienen los valores correctos para su sistema.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="f1a2d-121">`JAVA_HOME`: debe apuntar al directorio en el que esté instalado JDK.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="f1a2d-122">`PATH`: debe contener las rutas de acceso siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="f1a2d-123">`JAVA_HOME` (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="f1a2d-124">`JAVA_HOME\bin` (o la ruta de acceso equivalente).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="f1a2d-125">Directorio en el que esté instalado Maven.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="f1a2d-126">Creación de los clústeres</span><span class="sxs-lookup"><span data-stu-id="f1a2d-126">Create the clusters</span></span>

<span data-ttu-id="f1a2d-127">Apache Kafka en HDInsight no proporciona acceso a los agentes de Kafka a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="f1a2d-128">Cualquier comunicación con Kafka debe realizarse en la misma red virtual de Azure que utilizan los nodos del clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="f1a2d-129">En este ejemplo, los clústeres Kafka y Storm se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="f1a2d-130">En el diagrama siguiente, se muestra cómo fluye la comunicación entre los clústeres:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-130">The following diagram shows how communication flows between the clusters:</span></span>

![Diagrama de clústeres Storm y Kafka en una red virtual de Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="f1a2d-132">Se puede tener acceso a otros servicios del clúster, como SSH y Ambari, a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="f1a2d-133">Para más información sobre los puertos públicos disponibles en HDInsight, consulte [Puertos e identificadores URI usados en HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="f1a2d-134">Aunque puede crear manualmente la red virtual de Azure y los clústeres Kafka y Storm, resulta más sencillo utilizar una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="f1a2d-135">Siga los pasos que se indican a continuación para implementar una red virtual de Azure y los clústeres Kafka y Storm en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="f1a2d-136">Utilice el siguiente botón para iniciar sesión en Azure y abrir la plantilla en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="f1a2d-137">La plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="f1a2d-138">Crea estos recursos:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="f1a2d-139">Grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="f1a2d-139">Azure resource group</span></span>
    * <span data-ttu-id="f1a2d-140">Red virtual</span><span class="sxs-lookup"><span data-stu-id="f1a2d-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="f1a2d-141">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f1a2d-141">Azure Storage account</span></span>
    * <span data-ttu-id="f1a2d-142">Kafka en HDInsight versión 3.6 (tres nodos de trabajo)</span><span class="sxs-lookup"><span data-stu-id="f1a2d-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="f1a2d-143">Storm en HDInsight versión 3.6 (tres nodos de trabajo)</span><span class="sxs-lookup"><span data-stu-id="f1a2d-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="f1a2d-144">Para garantizar la disponibilidad de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="f1a2d-145">Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="f1a2d-146">Utilice la guía siguiente para rellenar las entradas de la hoja **Implementación personalizada**:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="f1a2d-148">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="f1a2d-149">Este grupo contiene el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="f1a2d-150">**Ubicación**: seleccione una ubicación geográfica próxima a usted.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="f1a2d-151">**Nombre base del clúster**: este valor se utiliza como nombre base para los clústeres Storm y Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="f1a2d-152">Por ejemplo, si especifica **hdi**, creará un clúster Storm llamado **storm-hdi** y un clúster Kafka llamado **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="f1a2d-153">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario del administrador de los clústeres Storm y Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="f1a2d-154">**Contraseña de inicio de sesión de clúster**: contraseña del usuario administrador para los clústeres Storm y Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="f1a2d-155">**Nombre de usuario SSH**: usuario SSH que se va a crear para los clústeres Storm y Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="f1a2d-156">**Contraseña SSH**: contraseña del usuario SSH para los clústeres Storm y Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="f1a2d-157">Consulte los **Términos y condiciones** y seleccione **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="f1a2d-158">Por último, active **Anclar al panel** y seleccione **Adquirir**.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="f1a2d-159">Se tarda aproximadamente 20 minutos en crear los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="f1a2d-160">Cuando se hayan creado los recursos, se muestra la hoja del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![Hoja de grupo de recursos de la red virtual y clústeres](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="f1a2d-162">Observe que los nombres de los clústeres de HDInsight son **storm-BASENAME** y **kafka-BASENAME**, donde BASENAME es el nombre que indicó en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="f1a2d-163">Estos nombres se utilizarán más adelante al establecer la conexión con los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="f1a2d-164">Descripción del código</span><span class="sxs-lookup"><span data-stu-id="f1a2d-164">Understanding the code</span></span>

<span data-ttu-id="f1a2d-165">Este proyecto contiene dos topologías:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-165">This project contains two topologies:</span></span>

* <span data-ttu-id="f1a2d-166">**KafkaWriter**: definida por el archivo **writer.yaml**, esta topología escribe frases aleatorias en Kafka con el KafkaBolt proporcionado con Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="f1a2d-167">Esta topología usa un componente **SentenceSpout** personalizado para generar frases aleatorias.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="f1a2d-168">**KafkaReader**: definida por el archivo **reader.yaml**, esta topología lee los datos de Kafka con el KafkaSpout proporcionado con Apache Storm y, después, registra los datos en stdout.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="f1a2d-169">Esta topología usa HdfsBolt de Storm para escribir datos en el almacenamiento predeterminado para el clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="f1a2d-170">Flux</span><span class="sxs-lookup"><span data-stu-id="f1a2d-170">Flux</span></span>

<span data-ttu-id="f1a2d-171">Las topologías se definen mediante [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="f1a2d-172">Flux se incorporó por primera vez a Storm 0.10.x y permite separar la configuración de la topología del código.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="f1a2d-173">Para las topologías que usan el entorno Flux, la topología se define en un archivo YAML.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="f1a2d-174">El archivo YAML se puede incluir como parte de la topología.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="f1a2d-175">También puede ser un archivo independiente que se usa al enviar la topología.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="f1a2d-176">Flux también admite la sustitución de variables en tiempo de ejecución, que se usa en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="f1a2d-177">Los siguientes parámetros se establecen en tiempo de ejecución para estas topologías:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="f1a2d-178">`${kafka.topic}`: el nombre del tema de Kafka donde las topologías leen y escriben.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="f1a2d-179">`${kafka.broker.hosts}`: los hosts donde se ejecutan los agentes de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="f1a2d-180">KafkaBolt usa la información de los agentes al escribir en Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="f1a2d-181">`${kafka.zookeeper.hosts}`: los hosts donde se ejecuta Zookeeper en el clúster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="f1a2d-182">Para más información sobre las topologías de Flux, vea [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="f1a2d-183">Descarga y compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="f1a2d-183">Download and compile the project</span></span>

1. <span data-ttu-id="f1a2d-184">En el entorno de desarrollo, descargue el proyecto de [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra una línea de comandos y cambie los directorios a la ubicación en la que descargó el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="f1a2d-185">Desde el directorio **hdinsight-storm-java-kafka**, use el siguiente comando para compilar el proyecto y crear un paquete de implementación:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="f1a2d-186">El proceso de empaquetado crea un archivo llamado `KafkaTopology-1.0-SNAPSHOT.jar` en el directorio `target`.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="f1a2d-187">Use los siguientes comandos para copiar el paquete en el clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="f1a2d-188">Reemplace **USERNAME** por el nombre de usuario SSH para el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="f1a2d-189">Reemplace **BASENAME** por el nombre base que utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="f1a2d-190">Cuando se le solicite, escriba la contraseña que utilizó al crear los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="f1a2d-191">Configurar la topología</span><span class="sxs-lookup"><span data-stu-id="f1a2d-191">Configure the topology</span></span>

1. <span data-ttu-id="f1a2d-192">Use uno de los métodos siguientes para detectar los hosts de agente de Kafka:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f1a2d-193">En el ejemplo de Bash se da por supuesto que `$CLUSTERNAME` contiene el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="f1a2d-194">También se supone que [jq](https://stedolan.github.io/jq/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="f1a2d-195">Cuando se le solicite, escriba la contraseña de la cuenta de inicio de sesión del clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="f1a2d-196">El valor que se devuelve es similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="f1a2d-197">Aunque puede haber más de dos hosts de agente para el clúster, no es necesario proporcionar una lista completa de los hosts a los clientes.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="f1a2d-198">Con uno o dos es suficiente.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-198">One or two is enough.</span></span>

2. <span data-ttu-id="f1a2d-199">Use uno de los métodos siguientes para detectar los hosts de Zookeeper de Kafka:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f1a2d-200">En el ejemplo de Bash se da por supuesto que `$CLUSTERNAME` contiene el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="f1a2d-201">También se supone que [jq](https://stedolan.github.io/jq/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="f1a2d-202">Cuando se le solicite, escriba la contraseña de la cuenta de inicio de sesión del clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="f1a2d-203">El valor que se devuelve es similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="f1a2d-204">Aunque haya más de dos nodos de Zookeeper, no es necesario proporcionar una lista completa de los hosts a los clientes.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="f1a2d-205">Con uno o dos es suficiente.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-205">One or two is enough.</span></span>

    <span data-ttu-id="f1a2d-206">Guarde este valor, porque se usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="f1a2d-207">Edite el archivo `dev.properties` en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="f1a2d-208">Agregue la información de hosts de agente y Zookeeper a las líneas correspondientes en este archivo.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="f1a2d-209">El siguiente ejemplo se configura con los valores de ejemplo de los pasos anteriores:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="f1a2d-210">Guarde el archivo `dev.properties` y, después, use el siguiente comando para cargarlo en el clúster de Storm:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="f1a2d-211">Reemplace **USERNAME** por el nombre de usuario SSH para el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="f1a2d-212">Reemplace **BASENAME** por el nombre base que utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="f1a2d-213">Inicio del escritor</span><span class="sxs-lookup"><span data-stu-id="f1a2d-213">Start the writer</span></span>

1. <span data-ttu-id="f1a2d-214">Para conectarse al clúster de Storm mediante SSH, utilice lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="f1a2d-215">Reemplace **USERNAME** por el nombre de usuario SSH que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="f1a2d-216">Reemplace **BASENAME** por el nombre base que se utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="f1a2d-217">Cuando se le solicite, escriba la contraseña que utilizó al crear los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="f1a2d-218">Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f1a2d-219">Desde la conexión SSH, use el comando siguiente para crear el tema de Kafka que se usa en la topología:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="f1a2d-220">Reemplace `$KAFKAZKHOSTS` con la información del host de Zookeeper que ha recuperado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="f1a2d-221">Desde la conexión de SSH al clúster Storm, use el siguiente comando para iniciar la topología del escritor:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="f1a2d-222">Los parámetros que se usan en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="f1a2d-223">`org.apache.storm.flux.Flux`: use Flux para configurar y ejecutar esta topología.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="f1a2d-224">`--remote`: envíe la topología a Nimbus.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="f1a2d-225">La topología se distribuye entre los nodos de trabajo del clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="f1a2d-226">`-R /writer.yaml`: use el archivo `writer.yaml` para configurar la topología.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="f1a2d-227">`-R` indica que este recurso está incluido en el archivo jar.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="f1a2d-228">Se encuentra en la raíz de jar, por lo que `/writer.yaml` es la ruta de acceso a él.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="f1a2d-229">`--filter`: rellene las entradas de la topología `writer.yaml` mediante los valores del archivo `dev.properties`.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="f1a2d-230">Por ejemplo, el valor de la entrada `kafka.topic` del archivo se usa para reemplazar la entrada `${kafka.topic}` en la definición de topología.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="f1a2d-231">Una vez que se ha iniciado la topología, use el siguiente comando para comprobar que está escribiendo datos en el tema de Kafka:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="f1a2d-232">Reemplace `$KAFKAZKHOSTS` con la información del host de Zookeeper que ha recuperado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="f1a2d-233">Este comando usa un script incluido con Kafka para supervisar el tema.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="f1a2d-234">Tras unos instantes, empezará a devolver frases aleatorias que se han escrito en el tema.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="f1a2d-235">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="f1a2d-236">Use Ctrl+C para detener el script.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="f1a2d-237">Inicio del lector</span><span class="sxs-lookup"><span data-stu-id="f1a2d-237">Start the reader</span></span>

1. <span data-ttu-id="f1a2d-238">Desde la sesión de SSH al clúster Storm, use el siguiente comando para iniciar la topología del lector:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="f1a2d-239">Cuando se inicie la topología, abra la interfaz de usuario de Storm.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="f1a2d-240">Esta interfaz de usuario web se encuentra en https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="f1a2d-241">Reemplace __BASENAME__ por el nombre base que utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="f1a2d-242">Cuando se le pida, use el nombre de inicio de sesión de administrador (de forma predeterminada, `admin`) y la contraseña que utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="f1a2d-243">Verá una página web similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-243">You see a web page similar to the following image:</span></span>

    ![UI de Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="f1a2d-245">En la interfaz de usuario de Storm, seleccione el vínculo __kafka-reader__ en la sección __Resumen de la topología__ para mostrar información sobre la topología __kafka-reader__.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Sección Resumen de la topología en la interfaz de usuario web de Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="f1a2d-247">Para mostrar información sobre las instancias del componente logger-bolt, seleccione el vínculo __logger-bolt__ en la sección __Bolts (All time)__.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Vínculo Logger-bolt en la sección Bolt](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="f1a2d-249">En la sección __Executors__ (Ejecutores), seleccione un vínculo en la columna __Port__ (Puerto) para mostrar la información de registro de esta instancia del componente.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![Vínculo Executors](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="f1a2d-251">El registro contiene un registro de los datos leídos desde el tema de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="f1a2d-252">La información del registro es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="f1a2d-253">Detención de las topologías</span><span class="sxs-lookup"><span data-stu-id="f1a2d-253">Stop the topologies</span></span>

<span data-ttu-id="f1a2d-254">Desde una sesión de SSH al clúster Storm, use los siguientes comandos para detener las topologías de Storm:</span><span class="sxs-lookup"><span data-stu-id="f1a2d-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="f1a2d-255">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="f1a2d-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f1a2d-256">Como el procedimiento descrito en este documento crea los dos clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="f1a2d-257">Al eliminar el grupo de recursos, se quitan todos los recursos creados siguiendo este documento.</span><span class="sxs-lookup"><span data-stu-id="f1a2d-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1a2d-258">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1a2d-258">Next steps</span></span>

<span data-ttu-id="f1a2d-259">Para ver más ejemplos de topologías que pueden utilizarse con Storm en HDInsight, consulte [Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="f1a2d-260">Para más información sobre la implementación y supervisión de topologías en HDInsight basado en Linux, consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f1a2d-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>