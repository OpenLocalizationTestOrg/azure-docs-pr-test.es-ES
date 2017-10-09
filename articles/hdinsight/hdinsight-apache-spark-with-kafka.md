---
title: aaaApache Spark streaming con Kafka - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse datos de Spark Apache Spark toostream entra y sale Kafka Apache mediante DStreams. En este ejemplo, se transmiten datos con Jupyter Notebook de Spark en HDInsight."
keywords: ejemplo de kafka, kafka zookeeper, spark streaming kafka, ejemplo de spark streaming kafka
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="2ba0b-105">Ejemplo de streaming de Apache Spark (DStream) con Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ba0b-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="2ba0b-106">Obtenga información acerca de cómo toouse datos de Spark Apache Spark toostream entre o salga de Apache Kafka en HDInsight con DStreams.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="2ba0b-107">Este ejemplo utiliza Jupyter notebook que se ejecuta en el clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="2ba0b-108">pasos de Hello en este documento crea un grupo de recursos de Azure que contiene tanto un Spark en HDInsight y un Kafka en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="2ba0b-109">Estos clústeres son ambos ubicados en una red Virtual de Azure, lo que permite hello toodirectly de clúster de Spark comunican con hello clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="2ba0b-110">Cuando haya terminado con pasos de hello en este documento, recuerde toodelete Hola clústeres tooavoid exceso cargos.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="2ba0b-111">Crear clústeres de Hola</span><span class="sxs-lookup"><span data-stu-id="2ba0b-111">Create hello clusters</span></span>

<span data-ttu-id="2ba0b-112">Apache Kafka en HDInsight no ofrece acceso toohello Kafka corredores de bolsa respecto Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="2ba0b-113">Todo lo que tooKafka debe estar en las conversaciones Hola misma red virtual de Azure como nodos de hello en Hola clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="2ba0b-114">En este ejemplo, hello Kafka y clústeres de Spark se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="2ba0b-115">Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:</span><span class="sxs-lookup"><span data-stu-id="2ba0b-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clústeres Spark y Kafka en una red virtual de Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="2ba0b-117">Aunque Kafka propio es limitado toocommunication dentro de la red virtual de hello, otros servicios en clúster de hello como SSH y Ambari pueden tener acceso a través de Hola a internet.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="2ba0b-118">Para obtener más información sobre los puertos públicos de hello disponibles con HDInsight, vea [puertos y URI utilizado por HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="2ba0b-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="2ba0b-119">Si bien puede crear una red virtual de Azure, Kafka y Spark clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="2ba0b-120">Use Hola siguientes pasos le indican una red virtual de Azure, Kafka, toodeploy y Spark clústeres tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="2ba0b-121">Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="2ba0b-122">Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="2ba0b-123">disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="2ba0b-124">Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="2ba0b-125">Esta plantilla crea un clúster de HDInsight 3.6 para Kafka y Spark.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="2ba0b-126">Hola uso seguidas de hello las entradas de información toopopulate hello **implementación personalizada** hoja:</span><span class="sxs-lookup"><span data-stu-id="2ba0b-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="2ba0b-128">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="2ba0b-129">Este grupo contiene clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="2ba0b-130">**Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="2ba0b-131">**Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="2ba0b-132">Por ejemplo, si especifica **hdi**, creará un clúster Spark denominado spark-hdi__ y un clúster Kafka denominado **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="2ba0b-133">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="2ba0b-134">**Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Spark y Kafka de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="2ba0b-135">**Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="2ba0b-136">**Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="2ba0b-137">Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="2ba0b-138">Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="2ba0b-139">Tarda aproximadamente 20 minutos toocreate clústeres Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="2ba0b-140">Una vez que se han creado los recursos de hello, son hoja tooa redirigida Hola grupo de recursos que contiene los clústeres de Hola y el panel de la web.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="2ba0b-142">Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME spark** y **kafka BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="2ba0b-143">Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="2ba0b-144">Utilizar blocs de notas de Hola</span><span class="sxs-lookup"><span data-stu-id="2ba0b-144">Use hello notebooks</span></span>

<span data-ttu-id="2ba0b-145">código de Hello de ejemplo de Hola descrita en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="2ba0b-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="2ba0b-146">Siga los pasos de Hola Hola `README.md` toocomplete de archivos en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="2ba0b-147">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="2ba0b-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="2ba0b-148">Puesto que los pasos de hello en este documento para crear ambos Hola de clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="2ba0b-149">Eliminando grupo de hello quita todos los recursos creados siguiendo este documento, el Hola red Virtual de Azure y la cuenta de almacenamiento usan los clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ba0b-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ba0b-150">Next steps</span></span>

<span data-ttu-id="2ba0b-151">En este ejemplo, ha aprendido cómo toouse inspirará tooread y escribir tooKafka.</span><span class="sxs-lookup"><span data-stu-id="2ba0b-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="2ba0b-152">Utilice Hola siguiendo vínculos toodiscover otro toowork maneras con Kafka:</span><span class="sxs-lookup"><span data-stu-id="2ba0b-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="2ba0b-153">Introducción a Apache Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ba0b-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="2ba0b-154">Usar MirrorMaker toocreate una réplica de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ba0b-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="2ba0b-155">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ba0b-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

