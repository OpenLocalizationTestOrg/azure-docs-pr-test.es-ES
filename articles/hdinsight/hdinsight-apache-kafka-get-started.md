---
title: aaaStart con Apache Kafka - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una Kafka Apache de clúster de HDInsight de Azure. Obtenga información acerca de cómo toocreate temas, los suscriptores y los consumidores."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="f4641-104">Introducción a Apache Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4641-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f4641-105">Obtenga información acerca de cómo toocreate y utilizar una [Kafka Apache](https://kafka.apache.org) clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4641-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="f4641-106">Kafka es una plataforma de streaming distribuida de código abierto que está disponible con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4641-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="f4641-107">A menudo se usa como un agente de mensajes, ya que proporciona una funcionalidad similar tooa publicación / suscripción cola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="f4641-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="f4641-108">Actualmente hay dos versiones de Kafka disponibles con HDInsight; 0.9.0 (HDInsight 3.4) y 0.10.0 (HDInsight 3.5 y 3.6).</span><span class="sxs-lookup"><span data-stu-id="f4641-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="f4641-109">Hola en este documento da por sentado que está usando a Kafka en 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4641-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="f4641-110">Creación de un clúster de Kafka</span><span class="sxs-lookup"><span data-stu-id="f4641-110">Create a Kafka cluster</span></span>

<span data-ttu-id="f4641-111">Usar hello siguiendo los pasos toocreate un Kafka en clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f4641-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="f4641-112">De hello [portal de Azure](https://portal.azure.com), seleccione **+ nuevo**, **Intelligence + análisis**y, a continuación, seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f4641-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Creación de un clúster de HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="f4641-114">De **Fundamentos**, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="f4641-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="f4641-115">**Nombre del clúster**: nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4641-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="f4641-116">**Suscripción**: seleccione Hola suscripción toouse.</span><span class="sxs-lookup"><span data-stu-id="f4641-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="f4641-117">**Nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión de clúster**: inicio de sesión de hello al tener acceso a los clústeres de Hola a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f4641-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="f4641-118">Utilice estos servicios de tooaccess de credenciales como Hola interfaz de usuario de Ambari Web o API de REST.</span><span class="sxs-lookup"><span data-stu-id="f4641-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="f4641-119">**Secure Shell (SSH) username**: inicio de sesión de hello usado al acceder a clúster hello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="f4641-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="f4641-120">De forma predeterminada contraseña hello es Hola igual que la contraseña de inicio de sesión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="f4641-121">**Grupo de recursos**: clúster hello toocreate de grupo de recursos de hello en.</span><span class="sxs-lookup"><span data-stu-id="f4641-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="f4641-122">**Ubicación**: Hola región de Azure toocreate Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="f4641-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Seleccione la suscripción.](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="f4641-124">Seleccione **clúster tipo**, y, a continuación, conjunto Hola siguiendo los valores de **configuración de clúster**:</span><span class="sxs-lookup"><span data-stu-id="f4641-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="f4641-125">**Tipo de clúster**: Kafka</span><span class="sxs-lookup"><span data-stu-id="f4641-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="f4641-126">**Versión**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="f4641-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="f4641-127">**Nivel de clúster**: estándar</span><span class="sxs-lookup"><span data-stu-id="f4641-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="f4641-128">Por último, utilice hello **seleccione** botón toosave configuración.</span><span class="sxs-lookup"><span data-stu-id="f4641-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Seleccionar el tipo de clúster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="f4641-130">Después de seleccionar el tipo de clúster de hello, usar hello __seleccione__ tooset Hola clúster tipo de botón.</span><span class="sxs-lookup"><span data-stu-id="f4641-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="f4641-131">A continuación, usar hello __siguiente__ configuración básica del botón toofinish.</span><span class="sxs-lookup"><span data-stu-id="f4641-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="f4641-132">Desde **Storage**, seleccione o cree una cuenta de Storage.</span><span class="sxs-lookup"><span data-stu-id="f4641-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="f4641-133">Para conocer los pasos hello en este documento, deje Hola otros campos en los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="f4641-134">Hola de uso __siguiente__ configuración de almacenamiento de toosave de botón.</span><span class="sxs-lookup"><span data-stu-id="f4641-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Establecer la configuración de cuenta de almacenamiento de Hola para HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="f4641-136">De __aplicaciones (opcionales)__, seleccione __siguiente__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4641-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="f4641-137">Para este ejemplo no se requieren aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f4641-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="f4641-138">De __tamaño de clúster__, seleccione __siguiente__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4641-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f4641-139">disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="f4641-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Hola de conjunto de tamaño de clúster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="f4641-141">Hola **discos por nodo de trabajo** controles de entrada de Hola escalabilidad de Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4641-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="f4641-142">Para más información, consulte [Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Configuración del almacenamiento y escalabilidad de Apache Kafka en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="f4641-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="f4641-143">De __configuración avanzada__, seleccione __siguiente__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4641-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="f4641-144">De hello **resumen**, revisar configuración de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="f4641-145">Hola de uso __editar__ vincula toochange cualquier configuración que no sean correcta.</span><span class="sxs-lookup"><span data-stu-id="f4641-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="f4641-146">Por último, utilice el clúster de the__Create__ botón toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Resumen de configuración del clúster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="f4641-148">Puede durar de clúster de too20 minutos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="f4641-149">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="f4641-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4641-150">Al realizar Hola pasos, debe utilizar a un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="f4641-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="f4641-151">Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4641-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="f4641-152">Desde el cliente, use SSH tooconnect toohello clúster:</span><span class="sxs-lookup"><span data-stu-id="f4641-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="f4641-153">Reemplace **SSHUSER** con nombre de usuario SSH de hello proporcionado durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="f4641-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="f4641-154">Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="f4641-155">Cuando se le solicite, escriba contraseña de hello destinadas Hola SSH cuenta.</span><span class="sxs-lookup"><span data-stu-id="f4641-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="f4641-156">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f4641-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="f4641-157"><a id="getkafkainfo"></a>Obtener información de hello Zookeeper y agente de host</span><span class="sxs-lookup"><span data-stu-id="f4641-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="f4641-158">Cuando se trabaja con Kafka, debe conocer los dos valores de host; Hola *Zookeeper* hello y hosts *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="f4641-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="f4641-159">Estos hosts se usan con hello Kafka API y muchas de las utilidades de Hola que se suministran con Kafka.</span><span class="sxs-lookup"><span data-stu-id="f4641-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="f4641-160">Use Hola siguientes pasos le indican las variables de entorno de toocreate que contienen información de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="f4641-161">Estas variables de entorno se utilizan en los pasos de hello en este documento.</span><span class="sxs-lookup"><span data-stu-id="f4641-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="f4641-162">Desde un clúster de toohello de conexión de SSH, comando hello tooinstall siguiente de Hola de uso `jq` utilidad.</span><span class="sxs-lookup"><span data-stu-id="f4641-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="f4641-163">Esta utilidad es tooparse usado documentos JSON y es útil para recuperar la información de host de agente de hello:</span><span class="sxs-lookup"><span data-stu-id="f4641-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="f4641-164">variables de entorno de hello tooset con la información se recuperan de Ambari, Hola de uso después de comandos:</span><span class="sxs-lookup"><span data-stu-id="f4641-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f4641-165">Establecer `CLUSTERNAME=` toohello nombre de clúster Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="f4641-166">Establecer `PASSWORD=` toohello contraseña de inicio de sesión (admin) que utilizó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="f4641-167">Hello texto siguiente es un ejemplo de contenido de Hola de `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="f4641-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="f4641-168">Hello texto siguiente es un ejemplo de contenido de Hola de `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="f4641-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="f4641-169">Hola `cut` comando es la lista de Hola de tootrim uso de entradas de host de hosts tootwo.</span><span class="sxs-lookup"><span data-stu-id="f4641-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="f4641-170">No es necesario lista completa de hello tooprovide de hosts al crear un productor o consumidor de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f4641-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="f4641-171">No confíe en la información de hello devuelta por esta sesión tooalways sea exacto.</span><span class="sxs-lookup"><span data-stu-id="f4641-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="f4641-172">Si ajusta el clúster de hello, corredores de bolsa nuevos se agregan o se quitan.</span><span class="sxs-lookup"><span data-stu-id="f4641-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="f4641-173">Si se produce un error y se reemplaza un nodo, puede cambiar el nombre de host de hello para el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="f4641-174">Debe recuperar la información de hosts de Zookeeper y agente de hello poco antes de usarlo tooensure tiene información válida.</span><span class="sxs-lookup"><span data-stu-id="f4641-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="f4641-175">de un tema</span><span class="sxs-lookup"><span data-stu-id="f4641-175">Create a topic</span></span>

<span data-ttu-id="f4641-176">Kafka almacena los flujos de datos en categorías denominadas *temas*.</span><span class="sxs-lookup"><span data-stu-id="f4641-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="f4641-177">Desde un SSH conexión tooa clúster nodo principal, use una secuencia de comandos proporcionada con Kafka toocreate un tema:</span><span class="sxs-lookup"><span data-stu-id="f4641-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="f4641-178">Este comando conecta tooZookeeper utilizando información de host de hello almacenada en `$KAFKAZKHOSTS`y, a continuación, crear tema Kafka llamado **probar**.</span><span class="sxs-lookup"><span data-stu-id="f4641-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="f4641-179">También puede comprobar que ese tema Hola se creó mediante Hola script toolist temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4641-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="f4641-180">Hello resultado de este comando enumera temas Kafka, que contiene Hola **probar** tema.</span><span class="sxs-lookup"><span data-stu-id="f4641-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="f4641-181">Generación y consumo de registros</span><span class="sxs-lookup"><span data-stu-id="f4641-181">Produce and consume records</span></span>

<span data-ttu-id="f4641-182">Kafka almacena *registros* en temas.</span><span class="sxs-lookup"><span data-stu-id="f4641-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="f4641-183">Los registros se generan mediante *productores* y se consumen mediante *consumidores*.</span><span class="sxs-lookup"><span data-stu-id="f4641-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="f4641-184">Los productores recuperan registros de *agentes* de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f4641-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="f4641-185">Cada nodo de trabajo del clúster de HDInsight es un agente de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f4641-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="f4641-186">Usar hello siguientes registros de toostore de pasos en el tema de prueba de Hola que creó anteriormente y, a continuación, leerlos mediante un consumidor:</span><span class="sxs-lookup"><span data-stu-id="f4641-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="f4641-187">Desde la sesión de SSH de hello, use un script que se proporciona con el tema de Kafka toowrite registros toohello:</span><span class="sxs-lookup"><span data-stu-id="f4641-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="f4641-188">No se devuelven toohello símbolo del sistema después de este comando.</span><span class="sxs-lookup"><span data-stu-id="f4641-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="f4641-189">En su lugar, escriba algunos mensajes de texto y, a continuación, utilice **Ctrl + C** toostop enviar toohello tema.</span><span class="sxs-lookup"><span data-stu-id="f4641-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="f4641-190">Cada línea se envía como un registro independiente.</span><span class="sxs-lookup"><span data-stu-id="f4641-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="f4641-191">Utilice una secuencia de comandos con registros de tooread de Kafka de tema de hello:</span><span class="sxs-lookup"><span data-stu-id="f4641-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="f4641-192">Este comando recupera los registros de Hola de tema de Hola y mostrarlos.</span><span class="sxs-lookup"><span data-stu-id="f4641-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="f4641-193">Usar `--from-beginning` indica Hola consumidor toostart desde principio Hola de secuencia de hello, por lo que se recuperan todos los registros.</span><span class="sxs-lookup"><span data-stu-id="f4641-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="f4641-194">Use __Ctrl + C__ consumidor de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="f4641-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="f4641-195">API de productor y consumidor</span><span class="sxs-lookup"><span data-stu-id="f4641-195">Producer and consumer API</span></span>

<span data-ttu-id="f4641-196">Mediante programación puede generar y consumir los registros mediante hello [Kafka API](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="f4641-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="f4641-197">toobuild un productor de Java y el consumidor, utilice Hola siguiendo los pasos de su entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f4641-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4641-198">Debe tener Hola instalados en el entorno de desarrollo de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4641-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="f4641-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, como OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f4641-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="f4641-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="f4641-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="f4641-201">Un cliente de SSH y hello `scp` comando.</span><span class="sxs-lookup"><span data-stu-id="f4641-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="f4641-202">Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4641-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="f4641-203">Descargar ejemplos de hello de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="f4641-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="f4641-204">Por ejemplo de productores y consumidores de hello, utilice el proyecto de hello en hello `Producer-Consumer` directory.</span><span class="sxs-lookup"><span data-stu-id="f4641-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="f4641-205">Este ejemplo contiene Hola siguientes clases:</span><span class="sxs-lookup"><span data-stu-id="f4641-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="f4641-206">**Ejecute** -inicia el consumidor de Hola o productor.</span><span class="sxs-lookup"><span data-stu-id="f4641-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="f4641-207">**Productor** -almacenes 1.000.000 registros toohello tema.</span><span class="sxs-lookup"><span data-stu-id="f4641-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="f4641-208">**Consumidor** -lee los registros de tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="f4641-209">toocreate un paquete jar, cambiar la ubicación de toohello de directorios de hello `Producer-Consumer` Hola de directorio y el uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f4641-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="f4641-210">Este comando crea un directorio denominado `target`, que contiene un archivo denominado `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f4641-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="f4641-211">Siguiente de hello use comandos hello toocopy `kafka-producer-consumer-1.0-SNAPSHOT.jar` clúster de HDInsight de tooyour de archivo:</span><span class="sxs-lookup"><span data-stu-id="f4641-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="f4641-212">Reemplace **SSHUSER** con el usuario SSH de hello para el clúster y reemplazar **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="f4641-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="f4641-213">Cuando se le solicite escribir contraseña de hello para el usuario SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="f4641-214">Una vez Hola `scp` comando termina de copiar el archivo hello, conecte el clúster toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="f4641-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="f4641-215">Usar hello comando toowrite registros toohello prueba tema siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4641-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="f4641-216">Una vez que ha finalizado el proceso de hello, utilice Hola siguientes tooread de comando de tema de hello:</span><span class="sxs-lookup"><span data-stu-id="f4641-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="f4641-217">registros de Hello leídos, junto con un recuento de registros, se muestra.</span><span class="sxs-lookup"><span data-stu-id="f4641-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="f4641-218">Puede ver algunas más de 1.000.000 registran como enviados tema de toohello varios registros mediante un script en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="f4641-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="f4641-219">Use __Ctrl + C__ consumidor de hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="f4641-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="f4641-220">Varios consumidores</span><span class="sxs-lookup"><span data-stu-id="f4641-220">Multiple consumers</span></span>

<span data-ttu-id="f4641-221">Los consumidores de Kafka usan un grupo de consumidores al leer los registros.</span><span class="sxs-lookup"><span data-stu-id="f4641-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="f4641-222">Con hello misma grupo con varios consumidores resultados en la carga equilibrada las lecturas de un tema.</span><span class="sxs-lookup"><span data-stu-id="f4641-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="f4641-223">Cada consumidor en grupo Hola recibe una parte de los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="f4641-224">toosee este proceso en acción, Hola uso siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="f4641-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="f4641-225">Abra un nuevo clúster de toohello de sesión SSH, para que tenga dos de ellos.</span><span class="sxs-lookup"><span data-stu-id="f4641-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="f4641-226">En cada sesión, use Hola siguientes toostart un consumidor con Hola mismo Id. de grupo de consumidor:</span><span class="sxs-lookup"><span data-stu-id="f4641-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="f4641-227">Este comando inicia un consumidor con el Id. de grupo de hello `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="f4641-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f4641-228">Usar comandos de hello en hello [obtener información de hello Zookeeper y agente host](#getkafkainfo) tooset sección `$KAFKABROKERS` para esta sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="f4641-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="f4641-229">Observe cómo cada sesión recuentos Hola los registros que recibe de tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="f4641-230">total de Hola de ambas sesiones debe Hola mismo tal y como se ha recibido previamente de un consumidor.</span><span class="sxs-lookup"><span data-stu-id="f4641-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="f4641-231">Consumo de los clientes dentro de hello mismo grupo se controla a través de las particiones de hello para el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="f4641-232">Para hello `test` tema creado anteriormente, tiene ocho particiones.</span><span class="sxs-lookup"><span data-stu-id="f4641-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="f4641-233">Si abre las sesiones SSH ocho e iniciar un consumidor en todas las sesiones, cada consumidor lee los registros de una única partición para el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4641-234">No puede haber más instancias de consumidor en un grupo de consumidores que particiones.</span><span class="sxs-lookup"><span data-stu-id="f4641-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="f4641-235">En este ejemplo, un grupo de consumidor puede contener una tooeight consumidores ya que es el número de Hola de particiones en el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="f4641-236">O bien, puede tener varios grupos de consumidores, los cuales no tengan más de ocho consumidores cada uno.</span><span class="sxs-lookup"><span data-stu-id="f4641-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="f4641-237">Registros guardados en Kafka se almacenan en orden de Hola se reciben dentro de una partición.</span><span class="sxs-lookup"><span data-stu-id="f4641-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="f4641-238">tooachieve ordenada de entrega para los registros *dentro de una partición*, cree un grupo de consumidores donde hello número de instancias de consumidor coincide con hello de particiones.</span><span class="sxs-lookup"><span data-stu-id="f4641-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="f4641-239">tooachieve ordenada de entrega para los registros *en el tema de hello*, cree un grupo de consumidores con instancia de un solo consumidor.</span><span class="sxs-lookup"><span data-stu-id="f4641-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="f4641-240">API de streaming</span><span class="sxs-lookup"><span data-stu-id="f4641-240">Streaming API</span></span>

<span data-ttu-id="f4641-241">Hola API de transmisión por secuencias se agregó tooKafka en versión 0.10.0; las versiones anteriores se basan en Apache Spark o aluvión de para el procesamiento de la secuencia.</span><span class="sxs-lookup"><span data-stu-id="f4641-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="f4641-242">Si aún no lo ha hecho, descargue los ejemplos de hello de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f4641-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="f4641-243">Para la transmisión por secuencias de ejemplo de Hola, utilice el proyecto de hello en hello `streaming` directory.</span><span class="sxs-lookup"><span data-stu-id="f4641-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="f4641-244">Este proyecto contiene solo una clase, `Stream`, que lee los registros de hello `test` tema creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f4641-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="f4641-245">Recuentos de palabras de hello leer y emite cada tema tooa word y recuento llamado `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="f4641-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="f4641-246">Hola `wordcounts` tema se crea en un paso más adelante en esta sección.</span><span class="sxs-lookup"><span data-stu-id="f4641-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="f4641-247">Desde la línea de comandos de hello en el entorno de desarrollo, cambiar la ubicación de toohello de directorios de hello `Streaming` directorio y, a continuación, Hola use después el comando toocreate un paquete jar:</span><span class="sxs-lookup"><span data-stu-id="f4641-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="f4641-248">Este comando crea un directorio denominado `target`, que contiene un archivo denominado `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f4641-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="f4641-249">Siguiente de hello use comandos hello toocopy `kafka-streaming-1.0-SNAPSHOT.jar` clúster de HDInsight de tooyour de archivo:</span><span class="sxs-lookup"><span data-stu-id="f4641-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="f4641-250">Reemplace **SSHUSER** con el usuario SSH de hello para el clúster y reemplazar **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="f4641-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="f4641-251">Cuando se le solicite escribir contraseña de hello para el usuario SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="f4641-252">Una vez Hola `scp` comando termina de copiar el archivo hello, conéctese clúster toohello mediante SSH y, a continuación, usar hello después comando toocreate hello `wordcounts` tema:</span><span class="sxs-lookup"><span data-stu-id="f4641-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="f4641-253">A continuación, inicie Hola streaming proceso mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f4641-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="f4641-254">Este comando inicia Hola proceso en segundo plano de Hola de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="f4641-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="f4641-255">Siguiente Hola de uso del comando toosend mensajes toohello `test` tema.</span><span class="sxs-lookup"><span data-stu-id="f4641-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="f4641-256">Estos mensajes se procesan por hello transmisión por secuencias de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f4641-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="f4641-257">Hola de uso después de la salida del comando tooview Hola escrita toohello `wordcounts` tema por hello streaming proceso:</span><span class="sxs-lookup"><span data-stu-id="f4641-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="f4641-258">datos de hello tooview, debe indicar clave hello tooprint Hola y Hola deserializador toouse para hello clave y valor.</span><span class="sxs-lookup"><span data-stu-id="f4641-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="f4641-259">nombre de clave de Hello es palabra Hola y clave-valor hello contiene el recuento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4641-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="f4641-260">Hola de salida es toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="f4641-260">hello output is similar toohello following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="f4641-261">recuento de Hola incrementa cada vez que se encuentra una palabra.</span><span class="sxs-lookup"><span data-stu-id="f4641-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="f4641-262">Usar hello __Ctrl + C__ tooexit Hola consumidor, a continuación, usar hello `fg` comando toobring Hola transmisión por secuencias de primer plano de back-toohello de tareas de fondo.</span><span class="sxs-lookup"><span data-stu-id="f4641-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="f4641-263">Use __Ctrl + C__ tooexit también.</span><span class="sxs-lookup"><span data-stu-id="f4641-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="f4641-264">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="f4641-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="f4641-265">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f4641-265">Troubleshoot</span></span>

<span data-ttu-id="f4641-266">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f4641-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4641-267">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4641-267">Next steps</span></span>

<span data-ttu-id="f4641-268">En este documento, ha aprendido los conceptos básicos de hello sobre cómo trabajar con Apache Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4641-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="f4641-269">Usar hello después toolearn más acerca de cómo trabajar con Kafka:</span><span class="sxs-lookup"><span data-stu-id="f4641-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="f4641-270">Alta disponibilidad de los datos con Apache Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4641-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="f4641-271">Aumento de la escalabilidad mediante la configuración de discos administrados con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4641-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="f4641-272">[Documentación de Apache Kafka](http://kafka.apache.org/documentation.html) en kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="f4641-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="f4641-273">Usar MirrorMaker toocreate una réplica de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4641-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="f4641-274">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4641-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="f4641-275">Uso de Apache Spark con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4641-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="f4641-276">Conectar tooKafka a través de una red Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="f4641-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
