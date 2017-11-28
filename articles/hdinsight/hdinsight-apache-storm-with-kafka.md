---
title: aaaUse Kafka Apache con Storm en HDInsight - Azure | Documentos de Microsoft
description: "Apache Kafka se instala con Apache Storm en HDInsight. Obtenga información acerca de cómo toowrite tooKafka y, a continuación, leer de él, con Hola KafkaBolt y KafkaSpout componentes suministrados con Storm. También Obtenga información acerca cómo toouse Hola toodefine del marco de trabajo de un flujo y enviar las topologías de Storm."
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
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="fbeea-105">Uso de Apache Kafka (versión preliminar) con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="fbeea-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="fbeea-106">Obtenga información acerca de cómo toouse Apache Storm tooread de y escribir tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="fbeea-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="fbeea-107">En este ejemplo también muestra cómo sistema utilizado por HDInsight del archivo de datos de toosave de un toohello de topología de Storm HDFS compatible.</span><span class="sxs-lookup"><span data-stu-id="fbeea-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="fbeea-108">pasos de Hello en este documento crea un grupo de recursos de Azure que contiene tanto una tormenta de HDInsight y un Kafka en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbeea-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="fbeea-109">Estos clústeres son ambos ubicados en una red Virtual de Azure, lo que permite hello toodirectly de clúster de Storm comunican con hello clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="fbeea-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="fbeea-110">Cuando haya terminado con pasos de hello en este documento, recuerde toodelete Hola clústeres tooavoid exceso cargos.</span><span class="sxs-lookup"><span data-stu-id="fbeea-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="fbeea-111">Obtener el código de hello</span><span class="sxs-lookup"><span data-stu-id="fbeea-111">Get hello code</span></span>

<span data-ttu-id="fbeea-112">código de Hello de ejemplo de Hola usado en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="fbeea-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="fbeea-113">toocompile este proyecto, deberá Hola siguiente configuración para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="fbeea-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="fbeea-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="fbeea-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="fbeea-115">HDInsight 3.5 y versiones posteriores requieren Java 8.</span><span class="sxs-lookup"><span data-stu-id="fbeea-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="fbeea-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="fbeea-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="fbeea-117">Un cliente de SSH (necesita hello `ssh` y `scp` comandos): para obtener información, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fbeea-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="fbeea-118">Un editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="fbeea-118">A text editor or IDE.</span></span>

<span data-ttu-id="fbeea-119">Hello siguientes variables de entorno pueden establecerse cuando se instalación Java y Hola JDK en su estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="fbeea-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="fbeea-120">Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.</span><span class="sxs-lookup"><span data-stu-id="fbeea-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="fbeea-121">`JAVA_HOME`-debe apuntar toohello directorio donde hello JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="fbeea-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="fbeea-122">`PATH`-debe contener Hola siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="fbeea-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="fbeea-123">`JAVA_HOME`(o la ruta de acceso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="fbeea-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="fbeea-124">`JAVA_HOME\bin`(o la ruta de acceso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="fbeea-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="fbeea-125">directorio de Hola donde está instalado Maven.</span><span class="sxs-lookup"><span data-stu-id="fbeea-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="fbeea-126">Crear clústeres de Hola</span><span class="sxs-lookup"><span data-stu-id="fbeea-126">Create hello clusters</span></span>

<span data-ttu-id="fbeea-127">Apache Kafka en HDInsight no ofrece acceso toohello Kafka corredores de bolsa respecto Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="fbeea-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="fbeea-128">Todo lo que tooKafka debe estar en las conversaciones Hola misma red virtual de Azure como nodos de hello en Hola clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="fbeea-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="fbeea-129">En este ejemplo, hello Kafka y clústeres de Storm se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbeea-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="fbeea-130">Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:</span><span class="sxs-lookup"><span data-stu-id="fbeea-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clústeres Storm y Kafka en una red virtual de Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="fbeea-132">Otros servicios en clúster de Hola Hola a como SSH y Ambari pueden tener acceso a través de internet.</span><span class="sxs-lookup"><span data-stu-id="fbeea-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="fbeea-133">Para obtener más información sobre los puertos públicos de hello disponibles con HDInsight, vea [puertos y URI utilizado por HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="fbeea-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="fbeea-134">Aunque puede crear una red virtual de Azure, Kafka, y aluvión de clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fbeea-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="fbeea-135">Use Hola siguientes pasos le indican una red virtual de Azure, Kafka, toodeploy y aluvión de clústeres tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbeea-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="fbeea-136">Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbeea-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="fbeea-137">Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="fbeea-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="fbeea-138">Se crea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbeea-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="fbeea-139">Grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="fbeea-139">Azure resource group</span></span>
    * <span data-ttu-id="fbeea-140">Red virtual</span><span class="sxs-lookup"><span data-stu-id="fbeea-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="fbeea-141">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="fbeea-141">Azure Storage account</span></span>
    * <span data-ttu-id="fbeea-142">Kafka en HDInsight versión 3.6 (tres nodos de trabajo)</span><span class="sxs-lookup"><span data-stu-id="fbeea-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="fbeea-143">Storm en HDInsight versión 3.6 (tres nodos de trabajo)</span><span class="sxs-lookup"><span data-stu-id="fbeea-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="fbeea-144">disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="fbeea-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="fbeea-145">Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fbeea-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="fbeea-146">Hola de uso después de las entradas de orientación toopopulate hello en hello **implementación personalizada** hoja:</span><span class="sxs-lookup"><span data-stu-id="fbeea-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="fbeea-148">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="fbeea-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="fbeea-149">Este grupo contiene clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="fbeea-150">**Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.</span><span class="sxs-lookup"><span data-stu-id="fbeea-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="fbeea-151">**Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Storm y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="fbeea-152">Por ejemplo, si especifica **hdi**, creará un clúster Storm llamado **storm-hdi** y un clúster Kafka llamado **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="fbeea-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="fbeea-153">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Storm y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="fbeea-154">**Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Storm y Kafka de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="fbeea-155">**Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Storm y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="fbeea-156">**Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Storm y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="fbeea-157">Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="fbeea-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="fbeea-158">Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**.</span><span class="sxs-lookup"><span data-stu-id="fbeea-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="fbeea-159">Tarda aproximadamente 20 minutos toocreate clústeres Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="fbeea-160">Una vez que se han creado los recursos de hello, se muestra la hoja de hello para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="fbeea-162">Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME storm** y **kafka BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="fbeea-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="fbeea-163">Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.</span><span class="sxs-lookup"><span data-stu-id="fbeea-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="fbeea-164">Comprensión del código de hello</span><span class="sxs-lookup"><span data-stu-id="fbeea-164">Understanding hello code</span></span>

<span data-ttu-id="fbeea-165">Este proyecto contiene dos topologías:</span><span class="sxs-lookup"><span data-stu-id="fbeea-165">This project contains two topologies:</span></span>

* <span data-ttu-id="fbeea-166">**KafkaWriter**: definido por hello **writer.yaml** archivo, esta topología escribe tooKafka frases aleatorio con hello KafkaBolt proporcionada con Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="fbeea-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="fbeea-167">Esta topología utiliza un personalizado **SentenceSpout** frases aleatorio de toogenerate de componente.</span><span class="sxs-lookup"><span data-stu-id="fbeea-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="fbeea-168">**KafkaReader**: definido por hello **reader.yaml** archivo, esta topología lee datos del Kafka con hello KafkaSpout proporcionada con Apache Storm después registros Hola toostdout de datos.</span><span class="sxs-lookup"><span data-stu-id="fbeea-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="fbeea-169">Esta topología utiliza el Hola Storm HdfsBolt toowrite datos toodefault almacenamiento de clúster de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="fbeea-170">Flux</span><span class="sxs-lookup"><span data-stu-id="fbeea-170">Flux</span></span>

<span data-ttu-id="fbeea-171">topologías de saludo se definen mediante [flujo](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="fbeea-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="fbeea-172">Un flujo se introdujo en Storm 0.10.x y permite la configuración de la topología tooseparate Hola desde el código de hello.</span><span class="sxs-lookup"><span data-stu-id="fbeea-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="fbeea-173">Para las topologías que utilizan el marco de trabajo de un flujo de hello, topología Hola se define en un archivo YAML.</span><span class="sxs-lookup"><span data-stu-id="fbeea-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="fbeea-174">archivo de Hello YAML puede incluirse como parte de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="fbeea-175">También puede ser un archivo independiente que se usa al enviar topología Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="fbeea-176">Flux también admite la sustitución de variables en tiempo de ejecución, que se usa en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fbeea-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="fbeea-177">Hola se establecen los parámetros siguientes en tiempo de ejecución para estas topologías:</span><span class="sxs-lookup"><span data-stu-id="fbeea-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="fbeea-178">`${kafka.topic}`: nombre de Hola de hello tema Kafka que topologías Hola lectura/escritura para.</span><span class="sxs-lookup"><span data-stu-id="fbeea-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="fbeea-179">`${kafka.broker.hosts}`: Hola hospeda esa hello Kafka establece ejecutar en.</span><span class="sxs-lookup"><span data-stu-id="fbeea-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="fbeea-180">información de agente de Hola se usa por hello KafkaBolt al escribir tooKafka.</span><span class="sxs-lookup"><span data-stu-id="fbeea-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="fbeea-181">`${kafka.zookeeper.hosts}`: hosts de Hola que Zookeeper se ejecuta en Hola clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="fbeea-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="fbeea-182">Para más información sobre las topologías de Flux, vea [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="fbeea-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="fbeea-183">Descargar y compile el proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="fbeea-183">Download and compile hello project</span></span>

1. <span data-ttu-id="fbeea-184">En el entorno de desarrollo, descargue el proyecto de Hola de [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra una línea de comandos y cambie la ubicación de toohello de directorios que descargó el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="fbeea-185">De hello **hdinsight-storm-java-kafka** directorio comando proyecto de hello toocompile siguiente de Hola de uso y crea un paquete de implementación:</span><span class="sxs-lookup"><span data-stu-id="fbeea-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="fbeea-186">proceso de paquetes de saludo crea un archivo denominado `KafkaTopology-1.0-SNAPSHOT.jar` en hello `target` directory.</span><span class="sxs-lookup"><span data-stu-id="fbeea-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="fbeea-187">Usar hello siguiente comandos toocopy Hola paquete tooyour aluvión de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbeea-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="fbeea-188">Reemplace **nombre de usuario** con nombre de usuario SSH de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="fbeea-189">Reemplace **BASENAME** con el nombre de base de Hola que utilizó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="fbeea-190">Cuando se le solicite, escriba contraseña Hola que utilizó al crear clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="fbeea-191">Configurar topología Hola</span><span class="sxs-lookup"><span data-stu-id="fbeea-191">Configure hello topology</span></span>

1. <span data-ttu-id="fbeea-192">Utilice uno de hello siguiendo métodos toodiscover Hola hosts de agente de Kafka:</span><span class="sxs-lookup"><span data-stu-id="fbeea-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="fbeea-193">Hello intensiva de ejemplo se da por supuesto que `$CLUSTERNAME` contiene el nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbeea-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="fbeea-194">También se supone que [jq](https://stedolan.github.io/jq/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="fbeea-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="fbeea-195">Cuando se le solicite, escriba la contraseña de hello para la cuenta de inicio de sesión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="fbeea-196">valor de Hello devuelto es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="fbeea-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="fbeea-197">Aunque puede haber más de dos hosts de agente para el clúster, no es necesario tooprovide una lista completa de todos los tooclients de hosts.</span><span class="sxs-lookup"><span data-stu-id="fbeea-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="fbeea-198">Con uno o dos es suficiente.</span><span class="sxs-lookup"><span data-stu-id="fbeea-198">One or two is enough.</span></span>

2. <span data-ttu-id="fbeea-199">Use uno de hello siguientes hosts de métodos toodiscover hello Kafka Zookeeper:</span><span class="sxs-lookup"><span data-stu-id="fbeea-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="fbeea-200">Hello intensiva de ejemplo se da por supuesto que `$CLUSTERNAME` contiene el nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbeea-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="fbeea-201">También se supone que [jq](https://stedolan.github.io/jq/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="fbeea-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="fbeea-202">Cuando se le solicite, escriba la contraseña de hello para la cuenta de inicio de sesión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="fbeea-203">valor de Hello devuelto es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="fbeea-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="fbeea-204">Aunque hay más de dos nodos de Zookeeper, no es necesario tooprovide una lista completa de todos los tooclients de hosts.</span><span class="sxs-lookup"><span data-stu-id="fbeea-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="fbeea-205">Con uno o dos es suficiente.</span><span class="sxs-lookup"><span data-stu-id="fbeea-205">One or two is enough.</span></span>

    <span data-ttu-id="fbeea-206">Guarde este valor, porque se usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="fbeea-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="fbeea-207">Editar hello `dev.properties` archivo en hello raíz del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="fbeea-208">Agregar Hola Broker y líneas coincidentes del toohello Zookeeper hosts información en este archivo.</span><span class="sxs-lookup"><span data-stu-id="fbeea-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="fbeea-209">Hello en el ejemplo siguiente se se configura con los valores de ejemplo de Hola de los pasos anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="fbeea-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="fbeea-210">Guardar hello `dev.properties` archivo y después usar Hola siguientes comando tooupload, clúster de Storm toohello:</span><span class="sxs-lookup"><span data-stu-id="fbeea-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="fbeea-211">Reemplace **nombre de usuario** con nombre de usuario SSH de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="fbeea-212">Reemplace **BASENAME** con el nombre de base de Hola que utilizó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="fbeea-213">Escritor de Hola de inicio</span><span class="sxs-lookup"><span data-stu-id="fbeea-213">Start hello writer</span></span>

1. <span data-ttu-id="fbeea-214">Usar hello después de clúster de Storm toohello tooconnect mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="fbeea-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="fbeea-215">Reemplace **nombre de usuario** con nombre de usuario SSH Hola utilizado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="fbeea-216">Reemplace **BASENAME** con el nombre de base de hello usado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="fbeea-217">Cuando se le solicite, escriba contraseña Hola que utilizó al crear clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="fbeea-218">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fbeea-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="fbeea-219">Desde Hola conexión SSH, use Hola después comando toocreate hello tema Kafka utilizado por la topología de hello:</span><span class="sxs-lookup"><span data-stu-id="fbeea-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="fbeea-220">Reemplace `$KAFKAZKHOSTS` con hello Zookeeper hospedar la información recuperada en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="fbeea-221">Desde el clúster de Storm de hello SSH conexión toohello, usar hello después de la topología de sistema de escritura de comando toostart hello:</span><span class="sxs-lookup"><span data-stu-id="fbeea-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="fbeea-222">parámetros de Hello utilizados con este comando son:</span><span class="sxs-lookup"><span data-stu-id="fbeea-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="fbeea-223">`org.apache.storm.flux.Flux`: Se usa un flujo tooconfigure y ejecutar esta topología.</span><span class="sxs-lookup"><span data-stu-id="fbeea-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="fbeea-224">`--remote`: Enviar Hola topología tooNimbus.</span><span class="sxs-lookup"><span data-stu-id="fbeea-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="fbeea-225">topología de Hola se distribuye entre los nodos de trabajador de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="fbeea-226">`-R /writer.yaml`: Hola usar `writer.yaml` topología de hello tooconfigure de archivos.</span><span class="sxs-lookup"><span data-stu-id="fbeea-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="fbeea-227">`-R`indica que este recurso se incluye en el archivo jar de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="fbeea-228">Está en la raíz Hola jar de hello, por lo que `/writer.yaml` es hello tooit de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="fbeea-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="fbeea-229">`--filter`: Rellenar las entradas de hello `writer.yaml` topología con valores de hello `dev.properties` archivo.</span><span class="sxs-lookup"><span data-stu-id="fbeea-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="fbeea-230">Hola por ejemplo, el valor de hello `kafka.topic` entrada de archivo hello es tooreplace usado hello `${kafka.topic}` entrada en la definición de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="fbeea-231">Una vez que ha iniciado la topología de hello, utilice Hola después tooverify de comando que está escribiendo datos toohello tema Kafka:</span><span class="sxs-lookup"><span data-stu-id="fbeea-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="fbeea-232">Reemplace `$KAFKAZKHOSTS` con hello Zookeeper hospedar la información recuperada en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="fbeea-233">Este comando usa un script incluido con el tema de Kafka toomonitor Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="fbeea-234">Tras unos instantes, debe iniciar devolver frases aleatorias que se han escrito toohello tema.</span><span class="sxs-lookup"><span data-stu-id="fbeea-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="fbeea-235">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fbeea-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="fbeea-236">Utilice Ctrl + c toostop script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="fbeea-237">Lector de Hola de inicio</span><span class="sxs-lookup"><span data-stu-id="fbeea-237">Start hello reader</span></span>

1. <span data-ttu-id="fbeea-238">Desde el clúster de Storm del toohello Hola de sesión SSH, use Hola después de la topología de lector de comando toostart hello:</span><span class="sxs-lookup"><span data-stu-id="fbeea-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="fbeea-239">Una vez que se inicia la topología de hello, abra Hola aluvión de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="fbeea-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="fbeea-240">Esta interfaz de usuario web se encuentra en https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="fbeea-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="fbeea-241">Reemplace __BASENAME__ con el nombre de base de Hola utilizada cuando se creó el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="fbeea-242">Cuando se le pida, use el nombre de inicio de sesión de administrador de hello (de forma predeterminada, `admin`) y la contraseña que utilizó al crea el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="fbeea-243">Vea un toohello similar de página web después de imagen:</span><span class="sxs-lookup"><span data-stu-id="fbeea-243">You see a web page similar toohello following image:</span></span>

    ![UI de Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="fbeea-245">En hello aluvión de interfaz de usuario, seleccione hello __kafka lector__ vínculo Hola __resumen de la topología__ sección toodisplay saber hello __kafka lector__ topología.</span><span class="sxs-lookup"><span data-stu-id="fbeea-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Sección Resumen de topología de interfaz de usuario de web de Storm Hola](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="fbeea-247">toodisplay información acerca de las instancias de hello del componente de registrador rayo hello, seleccione hello __registrador rayo__ vínculo Hola __tornillos (todo tiempo)__ sección.</span><span class="sxs-lookup"><span data-stu-id="fbeea-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Vínculo de rayo de registrador en hello tornillos sección](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="fbeea-249">Hola __ejecutor__ sección, seleccione un vínculo en hello __puerto__ información de registro de toodisplay de columna acerca de esta instancia de componente de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbeea-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Vínculo Executors](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="fbeea-251">registro de Hello contiene un registro de datos de hello leídos de hello tema Kafka.</span><span class="sxs-lookup"><span data-stu-id="fbeea-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="fbeea-252">información de Hello en el registro de hello es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="fbeea-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="fbeea-253">Detener las topologías de Hola</span><span class="sxs-lookup"><span data-stu-id="fbeea-253">Stop hello topologies</span></span>

<span data-ttu-id="fbeea-254">Desde un clúster de Storm toohello de sesión SSH, use Hola siguiendo las topologías de comandos toostop Hola Storm:</span><span class="sxs-lookup"><span data-stu-id="fbeea-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="fbeea-255">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="fbeea-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="fbeea-256">Puesto que los pasos de hello en este documento para crear ambos Hola de clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbeea-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="fbeea-257">Eliminando grupo de recursos de hello quita todos los recursos creados siguiendo este documento.</span><span class="sxs-lookup"><span data-stu-id="fbeea-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbeea-258">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbeea-258">Next steps</span></span>

<span data-ttu-id="fbeea-259">Para ver más ejemplos de topologías que pueden utilizarse con Storm en HDInsight, consulte [Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fbeea-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="fbeea-260">Para más información sobre la implementación y supervisión de topologías en HDInsight basado en Linux, consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fbeea-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>