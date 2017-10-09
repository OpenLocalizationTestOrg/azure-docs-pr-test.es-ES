---
title: temas de Apache Kafka aaaMirror - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo la creación de reflejo de toouse Apache Kafka característica toomaintain una réplica de un Kafka en clúster de HDInsight clúster secundario tooa de temas de creación de reflejo."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="2a199-103">Use los temas de Apache Kafka de tooreplicate de MirrorMaker con Kafka en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2a199-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="2a199-104">Obtenga información acerca de cómo toouse Kafka Apache de la creación de reflejo de clúster secundario de característica tooreplicate temas tooa.</span><span class="sxs-lookup"><span data-stu-id="2a199-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="2a199-105">Creación de reflejo se pueden se ejecutaban como un proceso continuo, o utilizar de forma intermitente como un método de migración de datos de un clúster tooanother.</span><span class="sxs-lookup"><span data-stu-id="2a199-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="2a199-106">En este ejemplo, la creación de reflejo es temas tooreplicate utilizado entre dos clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a199-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="2a199-107">Ambos clústeres están en una red Virtual de Azure en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="2a199-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="2a199-108">Creación de reflejo no debe considerarse como un medio tooachieve la tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="2a199-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="2a199-109">Hola tooitems desplazamiento dentro de un tema son diferentes entre los clústeres de origen y destino de hello, por lo que los clientes no pueden usar indistintamente Hola dos.</span><span class="sxs-lookup"><span data-stu-id="2a199-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="2a199-110">Si le preocupa la tolerancia a errores, debe establecer la replicación para temas de hello dentro de su clúster.</span><span class="sxs-lookup"><span data-stu-id="2a199-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="2a199-111">Para más información, consulte [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introducción a Kafka en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="2a199-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="2a199-112">Funcionamiento de la creación de reflejo de Kafka</span><span class="sxs-lookup"><span data-stu-id="2a199-112">How Kafka mirroring works</span></span>

<span data-ttu-id="2a199-113">Creación de reflejo funciona mediante registros de hello MirrorMaker herramienta (parte de Apache Kafka) tooconsume de temas en Hola clúster de origen y, a continuación, crear una copia local en el clúster de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="2a199-114">MirrorMaker usa uno (o más) *consumidores* que leen de clúster de origen de hello y un *productor* que escribe el clúster de toohello local (destino).</span><span class="sxs-lookup"><span data-stu-id="2a199-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="2a199-115">Hola siguiente diagrama ilustra el proceso de creación de reflejo de hello:</span><span class="sxs-lookup"><span data-stu-id="2a199-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Diagrama del proceso de creación de reflejo de Hola](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="2a199-117">Apache Kafka en HDInsight no proporciona acceso toohello servicio Kafka sobre Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="2a199-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="2a199-118">Los productores Kafka o los consumidores deben estar en hello misma red virtual de Azure como nodos de Hola Hola clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="2a199-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="2a199-119">En este ejemplo, hello origen Kafka y clústeres de destino se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a199-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="2a199-120">Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:</span><span class="sxs-lookup"><span data-stu-id="2a199-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clústeres Kafka de origen y destino en una red virtual de Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="2a199-122">clústeres de origen y destino de Hola pueden ser diferentes en el número de Hola de nodos y las particiones y desplazamientos dentro de los temas de hello también son diferentes.</span><span class="sxs-lookup"><span data-stu-id="2a199-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="2a199-123">Creación de reflejo mantiene el valor de clave de Hola que se utiliza para crear particiones, por lo que se conserva el orden de los registros en una base de cada clave.</span><span class="sxs-lookup"><span data-stu-id="2a199-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="2a199-124">Creación de reflejo en los límites de red</span><span class="sxs-lookup"><span data-stu-id="2a199-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="2a199-125">Si necesita toomirror entre clústeres de Kafka en distintas redes, hay Hola siguientes consideraciones adicionales:</span><span class="sxs-lookup"><span data-stu-id="2a199-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="2a199-126">**Las puertas de enlace**: redes Hola deben ser capaz de toocommunicate en hello nivel de TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="2a199-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="2a199-127">**La resolución de nombres**: Hola Kafka clústeres en cada red debe ser capaz de tooconnect tooeach otros mediante el uso de los nombres de host.</span><span class="sxs-lookup"><span data-stu-id="2a199-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="2a199-128">Esto puede requerir un servidor de sistema de nombres de dominio (DNS) en cada red que esté configurado tooforward solicitudes toohello otras redes.</span><span class="sxs-lookup"><span data-stu-id="2a199-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="2a199-129">Al crear una red Virtual de Azure, en lugar de usar Hola que DNS automática proporcionada con la red de hello, debe especificar un DNS hello y servidor dirección IP personalizada para servidor hello.</span><span class="sxs-lookup"><span data-stu-id="2a199-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="2a199-130">Después de Hola que se ha creado la red Virtual, a continuación, debe crear una máquina Virtual de Azure que usa esa dirección IP, a continuación, instalar y configurar software DNS en él.</span><span class="sxs-lookup"><span data-stu-id="2a199-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="2a199-131">Crear y configurar el servidor DNS personalizado de hello antes de instalar HDInsight en hello red Virtual.</span><span class="sxs-lookup"><span data-stu-id="2a199-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="2a199-132">No hay ninguna configuración adicional necesaria para el servidor DNS de hello HDInsight toouse configurado para hello red Virtual.</span><span class="sxs-lookup"><span data-stu-id="2a199-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="2a199-133">Para más información sobre cómo conectar dos redes virtuales de Azure, consulte [Configuración de una conexión de red virtual a red virtual](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2a199-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="2a199-134">Creación de clústeres Kafka</span><span class="sxs-lookup"><span data-stu-id="2a199-134">Create Kafka clusters</span></span>

<span data-ttu-id="2a199-135">Aunque puede crear una red virtual de Azure y Kafka clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2a199-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="2a199-136">Usar hello siguiendo los pasos toodeploy una red virtual de Azure y tooyour de clústeres de dos Kafka suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a199-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="2a199-137">Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a199-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="2a199-138">Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="2a199-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="2a199-139">disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="2a199-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="2a199-140">Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2a199-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="2a199-141">Hola uso seguidas de hello las entradas de información toopopulate hello **implementación personalizada** hoja:</span><span class="sxs-lookup"><span data-stu-id="2a199-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="2a199-143">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="2a199-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="2a199-144">Este grupo contiene clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="2a199-145">**Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.</span><span class="sxs-lookup"><span data-stu-id="2a199-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="2a199-146">**Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para hello Kafka clústeres.</span><span class="sxs-lookup"><span data-stu-id="2a199-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="2a199-147">Por ejemplo, si se especifica **hdi**, se crean clústeres denominados **source-hdi** y **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="2a199-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="2a199-148">**Nombre de usuario de inicio de sesión del clúster**: clústeres de Kafka de nombre de usuario de administrador de hello para el origen de Hola y de destino.</span><span class="sxs-lookup"><span data-stu-id="2a199-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="2a199-149">**Contraseña de inicio de sesión del clúster**: clústeres de Kafka de contraseña de usuario de administrador de Hola para hello origen y destino.</span><span class="sxs-lookup"><span data-stu-id="2a199-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="2a199-150">**Nombre de usuario SSH**: Hola toocreate de usuario SSH como Hola origen y destino Kafka clústeres.</span><span class="sxs-lookup"><span data-stu-id="2a199-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="2a199-151">**Contraseña SSH**: clústeres de Kafka de contraseña de hello para el usuario SSH de hello para el origen de Hola y de destino.</span><span class="sxs-lookup"><span data-stu-id="2a199-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="2a199-152">Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="2a199-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="2a199-153">Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**.</span><span class="sxs-lookup"><span data-stu-id="2a199-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="2a199-154">Tarda aproximadamente 20 minutos toocreate clústeres Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="2a199-155">Una vez que se han creado los recursos de hello, son hoja tooa redirigida Hola grupo de recursos que contiene los clústeres de Hola y el panel de la web.</span><span class="sxs-lookup"><span data-stu-id="2a199-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="2a199-157">Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **origen BASENAME** y **BASENAME dest**, donde BASENAME es el nombre hello proporcionado toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="2a199-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="2a199-158">Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.</span><span class="sxs-lookup"><span data-stu-id="2a199-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="2a199-159">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="2a199-159">Create topics</span></span>

1. <span data-ttu-id="2a199-160">Conectar toohello **origen** mediante SSH de clúster:</span><span class="sxs-lookup"><span data-stu-id="2a199-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2a199-161">Reemplace **sshuser** con nombre de usuario SSH Hola utilizado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="2a199-162">Reemplace **BASENAME** con el nombre de base de hello usado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="2a199-163">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2a199-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2a199-164">Siguiente de hello use comandos hosts de Zookeeper toofind hello para el clúster de origen de hello:</span><span class="sxs-lookup"><span data-stu-id="2a199-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="2a199-165">Se ha creado Hola de uso después de tooverify de comando que Hola tema:</span><span class="sxs-lookup"><span data-stu-id="2a199-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="2a199-166">respuesta de Hello contiene `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="2a199-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="2a199-167">Hola de uso siguiente tooview hello Zookeeper host información de este (hello **origen**) clúster:</span><span class="sxs-lookup"><span data-stu-id="2a199-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="2a199-168">Esto devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="2a199-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="2a199-169">Guarde esta información.</span><span class="sxs-lookup"><span data-stu-id="2a199-169">Save this information.</span></span> <span data-ttu-id="2a199-170">Se utiliza en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="2a199-171">Configuración del reflejo</span><span class="sxs-lookup"><span data-stu-id="2a199-171">Configure mirroring</span></span>

1. <span data-ttu-id="2a199-172">Conectar toohello **destino** mediante una sesión SSH diferente del clúster:</span><span class="sxs-lookup"><span data-stu-id="2a199-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2a199-173">Reemplace **sshuser** con nombre de usuario SSH Hola utilizado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="2a199-174">Reemplace **BASENAME** con el nombre de base de hello usado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="2a199-175">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2a199-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2a199-176">Siguiente Hola de uso del comando toocreate un `consumer.properties` archivo que describe cómo toocommunicate con hello **origen** clúster:</span><span class="sxs-lookup"><span data-stu-id="2a199-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="2a199-177">Hola de uso después de texto como contenido de Hola de hello `consumer.properties` archivo:</span><span class="sxs-lookup"><span data-stu-id="2a199-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="2a199-178">Reemplace **SOURCE_ZKHOSTS** con hello Zookeeper hospeda información de hello **origen** clúster.</span><span class="sxs-lookup"><span data-stu-id="2a199-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="2a199-179">Este archivo describe Hola consumidor información toouse al leer desde el origen de hello clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="2a199-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="2a199-180">Para más información sobre la configuración de los consumidores, consulte [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configuraciones de consumidor) en kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="2a199-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="2a199-181">archivo de hello toosave, use **Ctrl + X**, **Y**y, a continuación, **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="2a199-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="2a199-182">Antes de configurar el productor de Hola que se comunica con el clúster de destino de hello, debe buscar broker Hola hosts para hello **destino** clúster.</span><span class="sxs-lookup"><span data-stu-id="2a199-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="2a199-183">Utilice esta información de hello después tooretrieve de comandos:</span><span class="sxs-lookup"><span data-stu-id="2a199-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="2a199-184">Reemplace `$PASSWORD` con la contraseña de cuenta (Administrador) de inicio de sesión de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="2a199-185">Reemplace `$CLUSTERNAME` con nombre de hello del clúster de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="2a199-186">Estos comandos devuelven siguiente toohello similar de información:</span><span class="sxs-lookup"><span data-stu-id="2a199-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="2a199-187">Hola de uso después de toocreate un `producer.properties` archivo que describe cómo toocommunicate con hello **destino** clúster:</span><span class="sxs-lookup"><span data-stu-id="2a199-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="2a199-188">Hola de uso después de texto como contenido de Hola de hello `producer.properties` archivo:</span><span class="sxs-lookup"><span data-stu-id="2a199-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="2a199-189">Reemplace **DEST_BROKERS** con información de broker de hello del paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="2a199-190">Para más información sobre la configuración del productor, consulte [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configuraciones de productor) en kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="2a199-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="2a199-191">Inicio de MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="2a199-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="2a199-192">De hello SSH conexión toohello **destino** de clúster, use Hola siguiendo comando toostart hello MirrorMaker proceso:</span><span class="sxs-lookup"><span data-stu-id="2a199-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="2a199-193">parámetros de Hello utilizados en este ejemplo son:</span><span class="sxs-lookup"><span data-stu-id="2a199-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="2a199-194">**--consumer.config**: especifica el archivo hello que contiene propiedades de consumidor.</span><span class="sxs-lookup"><span data-stu-id="2a199-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="2a199-195">Estas propiedades son toocreate usado un consumidor que lee de hello *origen* clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="2a199-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="2a199-196">**--producer.config**: especifica el archivo hello que contiene las propiedades del productor.</span><span class="sxs-lookup"><span data-stu-id="2a199-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="2a199-197">Estas propiedades son toocreate usado un productor que escribe toohello *destino* clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="2a199-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="2a199-198">**lista blanca de direcciones--**: una lista de temas que se replica MirrorMaker de hello origen clúster toohello el destino.</span><span class="sxs-lookup"><span data-stu-id="2a199-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="2a199-199">**--num.streams**: Hola número de toocreate de subprocesos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="2a199-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="2a199-200">En el inicio, MirrorMaker devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="2a199-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="2a199-201">De hello SSH conexión toohello **origen** de clúster, use Hola después comando toostart un productor y enviar tema toohello de mensajes:</span><span class="sxs-lookup"><span data-stu-id="2a199-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="2a199-202">Reemplace `$PASSWORD` con la contraseña de inicio de sesión (admin) hello para el clúster de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="2a199-203">Reemplace `$CLUSTERNAME` con el nombre de Hola de clúster de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="2a199-204">Cuando llegue a una línea en blanco con un cursor, escriba algunos mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="2a199-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="2a199-205">Estos se envían toohello tema en hello **origen** clúster.</span><span class="sxs-lookup"><span data-stu-id="2a199-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="2a199-206">Cuando haya terminado, use **Ctrl + C** proceso productor de tooend Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="2a199-207">De hello SSH conexión toohello **destino** de clúster, use **Ctrl + C** tooend hello MirrorMaker proceso.</span><span class="sxs-lookup"><span data-stu-id="2a199-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="2a199-208">A continuación, siguiente de hello use comandos tooverify ese hello `testtopic` tema se creó, y esos datos en el tema de hello eran toothis replicada reflejado:</span><span class="sxs-lookup"><span data-stu-id="2a199-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="2a199-209">Reemplace `$PASSWORD` con la contraseña de inicio de sesión (admin) hello para el clúster de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="2a199-210">Reemplace `$CLUSTERNAME` con nombre de hello del clúster de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="2a199-211">Hello lista de temas ahora incluye `testtopic`, que se crea al MirrorMaster refleja tema Hola de hello origen clúster toohello el destino.</span><span class="sxs-lookup"><span data-stu-id="2a199-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="2a199-212">mensajes de Hola recuperados de tema de hello son igual al escribir en el clúster de origen Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="2a199-213">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="2a199-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="2a199-214">Puesto que los pasos de hello en este documento para crear ambos Hola de clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a199-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="2a199-215">Eliminando grupo de recursos de hello quita todos los recursos creados siguiendo este documento, el Hola red Virtual de Azure y la cuenta de almacenamiento usan los clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a199-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a199-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a199-216">Next Steps</span></span>

<span data-ttu-id="2a199-217">En este documento, aprendió cómo toouse MirrorMaker toocreate una réplica de un Kafka de clúster.</span><span class="sxs-lookup"><span data-stu-id="2a199-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="2a199-218">Utilice Hola siguiendo vínculos toodiscover otro toowork maneras con Kafka:</span><span class="sxs-lookup"><span data-stu-id="2a199-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="2a199-219">[Documentación de Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) en cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="2a199-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="2a199-220">Introducción a Apache Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a199-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="2a199-221">Uso de Apache Spark con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a199-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="2a199-222">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a199-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="2a199-223">Conectar tooKafka a través de una red Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="2a199-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
