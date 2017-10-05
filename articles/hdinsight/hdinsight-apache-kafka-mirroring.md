---
title: Temas de Apache Kafka en Azure HDInsight | Microsoft Docs
description: "Aprenda a usar la característica de creación de reflejo de Apache Kafka para mantener una réplica de un Kafka en un clúster de HDInsight mediante el reflejo de temas en un clúster secundario."
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
ms.openlocfilehash: e418cb01e1a9168e3662e8d6242903e052b6047b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="f5598-103">Uso de MirrorMaker para replicar temas de Apache Kafka con Kafka en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="f5598-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="f5598-104">Obtenga información sobre cómo usar la característica de creación de reflejo de Apache Kafka para replicar temas a un clúster secundario.</span><span class="sxs-lookup"><span data-stu-id="f5598-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="f5598-105">La creación de reflejo se puede ejecutar como proceso continuo, o utilizar de forma intermitente como método de migración de datos de un clúster a otro.</span><span class="sxs-lookup"><span data-stu-id="f5598-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="f5598-106">En este ejemplo, la creación de reflejo se usa para replicar temas entre dos clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5598-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="f5598-107">Ambos clústeres están en una red virtual de Azure en la misma región.</span><span class="sxs-lookup"><span data-stu-id="f5598-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="f5598-108">La creación de reflejo no debe considerarse como un medio para conseguir tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="f5598-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="f5598-109">El desplazamiento a los elementos de un tema es diferentes entre los clústeres de origen y de destino, por lo que los clientes no puede usar los dos indistintamente.</span><span class="sxs-lookup"><span data-stu-id="f5598-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="f5598-110">Si le preocupa la tolerancia a errores, establezca la replicación para los temas en el clúster.</span><span class="sxs-lookup"><span data-stu-id="f5598-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="f5598-111">Para más información, consulte [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introducción a Kafka en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="f5598-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="f5598-112">Funcionamiento de la creación de reflejo de Kafka</span><span class="sxs-lookup"><span data-stu-id="f5598-112">How Kafka mirroring works</span></span>

<span data-ttu-id="f5598-113">La creación de reflejo se realiza mediante la herramienta MirrorMaker (parte de Apache Kafka), que consume registros de temas del clúster de origen y crea una copia local en el clúster de destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="f5598-114">MirrorMaker usa uno o más *consumidores* que leen desde el clúster de origen y un *productor* que escribe en el clúster local (de destino).</span><span class="sxs-lookup"><span data-stu-id="f5598-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="f5598-115">En el siguiente diagrama se ilustra el proceso de reflejo:</span><span class="sxs-lookup"><span data-stu-id="f5598-115">The following diagram illustrates the Mirroring process:</span></span>

![Diagrama del proceso de creación de reflejo](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="f5598-117">Apache Kafka en HDInsight no proporciona acceso a los servicios de Kafka a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="f5598-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="f5598-118">Los productores o consumidores de Kafka deben estar en la misma red virtual de Azure que utilizan los nodos del clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="f5598-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="f5598-119">En este ejemplo, los clústeres Kafka de origen y destino se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5598-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="f5598-120">En el diagrama siguiente, se muestra cómo fluye la comunicación entre los clústeres:</span><span class="sxs-lookup"><span data-stu-id="f5598-120">The following diagram shows how communication flows between the clusters:</span></span>

![Diagrama de clústeres Kafka de origen y destino en una red virtual de Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="f5598-122">Los clústeres de origen y destino pueden ser diferentes en el número de nodos y las particiones; los desplazamientos dentro de los temas también son diferentes.</span><span class="sxs-lookup"><span data-stu-id="f5598-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="f5598-123">La creación de reflejos conserva el valor de la clave que se utiliza para crear particiones, por lo que se mantiene el orden de los registros en una base por claves.</span><span class="sxs-lookup"><span data-stu-id="f5598-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="f5598-124">Creación de reflejo en los límites de red</span><span class="sxs-lookup"><span data-stu-id="f5598-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="f5598-125">Si tiene que crear un reflejo entre los clústeres Kafka en distintas redes, existen las siguientes consideraciones adicionales:</span><span class="sxs-lookup"><span data-stu-id="f5598-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="f5598-126">**Puertas de enlace**: las redes deben ser capaces de comunicarse en el nivel de TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="f5598-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="f5598-127">**Resolución de nombres**: los clústeres Kafka en cada red deben ser capaces de conectarse entre sí mediante nombres de host.</span><span class="sxs-lookup"><span data-stu-id="f5598-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="f5598-128">Esto puede requerir un servidor de sistema de nombres de dominio (DNS) en cada red que se configure para reenviar solicitudes a las demás redes.</span><span class="sxs-lookup"><span data-stu-id="f5598-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="f5598-129">Al crear una red virtual de Azure, en lugar de usar el DNS automático proporcionado con la red, debe especificar un servidor DNS personalizado y la dirección IP para el servidor.</span><span class="sxs-lookup"><span data-stu-id="f5598-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="f5598-130">Una vez creada la red virtual, debe crear una máquina virtual de Azure que use esa dirección IP, y en ella instalar y configurar el software DNS.</span><span class="sxs-lookup"><span data-stu-id="f5598-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f5598-131">Cree y configure el servidor DNS personalizado antes de instalar HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f5598-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="f5598-132">No es necesaria ninguna configuración adicional para que HDInsight use el servidor DNS configurado para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f5598-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="f5598-133">Para más información sobre cómo conectar dos redes virtuales de Azure, consulte [Configuración de una conexión de red virtual a red virtual](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f5598-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="f5598-134">Creación de clústeres Kafka</span><span class="sxs-lookup"><span data-stu-id="f5598-134">Create Kafka clusters</span></span>

<span data-ttu-id="f5598-135">Aunque puede crear manualmente la red virtual de Azure y los clústeres Kafka, resulta más sencillo con una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5598-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="f5598-136">Siga los pasos que se indican a continuación para implementar una red virtual de Azure y dos clústeres Kafka en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5598-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="f5598-137">Utilice el siguiente botón para iniciar sesión en Azure y abrir la plantilla en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5598-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="f5598-138">La plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="f5598-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f5598-139">Para garantizar la disponibilidad de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f5598-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="f5598-140">Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f5598-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="f5598-141">Utilice los datos siguientes para rellenar las entradas de la hoja **Implementación personalizada**:</span><span class="sxs-lookup"><span data-stu-id="f5598-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="f5598-143">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="f5598-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="f5598-144">Este grupo contiene el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5598-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="f5598-145">**Ubicación**: seleccione una ubicación geográfica próxima a usted.</span><span class="sxs-lookup"><span data-stu-id="f5598-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="f5598-146">**Nombre base del clúster**: este valor se utiliza como nombre base en los clústeres Kafka.</span><span class="sxs-lookup"><span data-stu-id="f5598-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="f5598-147">Por ejemplo, si se especifica **hdi**, se crean clústeres denominados **source-hdi** y **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="f5598-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="f5598-148">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario del administrador de los clústeres Kafka de origen y destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="f5598-149">**Contraseña de inicio de sesión del clúster**: contraseña del administrador de los clústeres Kafka de origen y destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="f5598-150">**Nombre de usuario de SSH**: usuario de SSH para crear los clústeres Kafka de origen y destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="f5598-151">**Contraseña SSH**: contraseña del usuario de SSH para los clústeres Kafka de origen y destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="f5598-152">Consulte los **Términos y condiciones** y seleccione **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="f5598-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="f5598-153">Por último, active **Anclar al panel** y seleccione **Adquirir**.</span><span class="sxs-lookup"><span data-stu-id="f5598-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="f5598-154">Se tarda aproximadamente 20 minutos en crear los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f5598-154">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="f5598-155">Una vez creados los recursos, se le redirigirá a una hoja del grupo de recursos que contiene los clústeres y el panel web.</span><span class="sxs-lookup"><span data-stu-id="f5598-155">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Hoja de grupo de recursos de la red virtual y clústeres](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="f5598-157">Observe que los nombres de los clústeres de HDInsight son **source-BASENAME** y **dest-BASENAME**, donde BASENAME es el nombre proporcionado a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f5598-157">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="f5598-158">Estos nombres se utilizarán más adelante al establecer la conexión con los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f5598-158">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="f5598-159">Creación de temas</span><span class="sxs-lookup"><span data-stu-id="f5598-159">Create topics</span></span>

1. <span data-ttu-id="f5598-160">Conéctese al clúster **de origen**con SSH:</span><span class="sxs-lookup"><span data-stu-id="f5598-160">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="f5598-161">Reemplace **sshuser** por el nombre de usuario de SSH que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f5598-161">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="f5598-162">Reemplace **BASENAME** por el nombre base que se utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f5598-162">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="f5598-163">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f5598-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f5598-164">Use los comandos siguientes para buscar los hosts de Zookeeper para el clúster de origen:</span><span class="sxs-lookup"><span data-stu-id="f5598-164">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with the password for the cluster.

    Replace `$CLUSTERNAME` with the name of the source cluster.

3. To create a topic named `testtopic`, use the following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="f5598-165">Use el siguiente comando para comprobar que se creó el tema:</span><span class="sxs-lookup"><span data-stu-id="f5598-165">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="f5598-166">La respuesta contiene `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="f5598-166">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="f5598-167">Use lo siguiente para ver la información de host de Zookeeper para este clúster (de **origen**):</span><span class="sxs-lookup"><span data-stu-id="f5598-167">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="f5598-168">Esto devuelve información similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5598-168">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="f5598-169">Guarde esta información.</span><span class="sxs-lookup"><span data-stu-id="f5598-169">Save this information.</span></span> <span data-ttu-id="f5598-170">Se usa en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="f5598-170">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="f5598-171">Configuración del reflejo</span><span class="sxs-lookup"><span data-stu-id="f5598-171">Configure mirroring</span></span>

1. <span data-ttu-id="f5598-172">Conéctese al clúster de **destino** mediante una sesión SSH diferente:</span><span class="sxs-lookup"><span data-stu-id="f5598-172">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="f5598-173">Reemplace **sshuser** por el nombre de usuario de SSH que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f5598-173">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="f5598-174">Reemplace **BASENAME** por el nombre base que se utilizó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="f5598-174">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="f5598-175">Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f5598-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f5598-176">Use el siguiente comando para crear un archivo `consumer.properties` que describa cómo comunicarse con el clúster de **origen**:</span><span class="sxs-lookup"><span data-stu-id="f5598-176">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="f5598-177">Use el texto siguiente como contenido del archivo `consumer.properties`:</span><span class="sxs-lookup"><span data-stu-id="f5598-177">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="f5598-178">Reemplace **SOURCE_ZKHOSTS** con la información de hosts de Zookeeper del clúster de **origen**.</span><span class="sxs-lookup"><span data-stu-id="f5598-178">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="f5598-179">Este archivo describe la información de consumidor que se utilizará al leer desde clúster Kafka de origen.</span><span class="sxs-lookup"><span data-stu-id="f5598-179">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="f5598-180">Para más información sobre la configuración de los consumidores, consulte [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configuraciones de consumidor) en kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="f5598-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="f5598-181">Para guardar el archivo, presione **Ctr+X**, luego, **Y** y **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f5598-181">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="f5598-182">Antes de configurar el productor que se comunica con el clúster de destino, debe encontrar el agente de hosts para el clúster de **destino**.</span><span class="sxs-lookup"><span data-stu-id="f5598-182">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="f5598-183">Use los siguientes comandos para recuperar esta información:</span><span class="sxs-lookup"><span data-stu-id="f5598-183">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="f5598-184">Reemplace `$PASSWORD` por la contraseña de la cuenta de inicio de sesión (del administrador) del clúster.</span><span class="sxs-lookup"><span data-stu-id="f5598-184">Replace `$PASSWORD` with the login account (admin) password for the cluster.</span></span>

    <span data-ttu-id="f5598-185">Reemplace `$CLUSTERNAME` por el nombre del clúster de destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-185">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="f5598-186">Estos comandos devuelven información similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5598-186">These commands return information similar to the following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="f5598-187">Use lo siguiente para crear un archivo `producer.properties` que describa cómo comunicarse con el clúster de **destino**:</span><span class="sxs-lookup"><span data-stu-id="f5598-187">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="f5598-188">Use el texto siguiente como contenido del archivo `producer.properties`:</span><span class="sxs-lookup"><span data-stu-id="f5598-188">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="f5598-189">Reemplace **DEST_BROKERS** con la información de agente del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="f5598-189">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="f5598-190">Para más información sobre la configuración del productor, consulte [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configuraciones de productor) en kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="f5598-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="f5598-191">Inicio de MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="f5598-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="f5598-192">En la conexión SSH al clúster de **destino**, use el siguiente comando para iniciar el proceso de MirrorMaker:</span><span class="sxs-lookup"><span data-stu-id="f5598-192">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="f5598-193">Parámetros que se utilizan en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5598-193">The parameters used in this example are:</span></span>

    * <span data-ttu-id="f5598-194">**--consumer.config**: especifica el archivo que contiene las propiedades de consumidor.</span><span class="sxs-lookup"><span data-stu-id="f5598-194">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="f5598-195">Estas propiedades se utilizan para crear un consumidor que se lea desde el clúster Kafka de *origen*.</span><span class="sxs-lookup"><span data-stu-id="f5598-195">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="f5598-196">**--producer.config**: especifica el archivo que contiene las propiedades de productor.</span><span class="sxs-lookup"><span data-stu-id="f5598-196">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="f5598-197">Estas propiedades se utilizan para crear un productor que escriba en el clúster Kafka de *destino*.</span><span class="sxs-lookup"><span data-stu-id="f5598-197">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="f5598-198">**--whitelist**: lista de temas que MirrorMaker replica desde el clúster de origen al de destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-198">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="f5598-199">**--num.streams**: número de subprocesos de consumidor para crear.</span><span class="sxs-lookup"><span data-stu-id="f5598-199">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="f5598-200">Al inicio, MirrorMaker devuelve información similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5598-200">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="f5598-201">En la conexión SSH al clúster de **origen**, use el siguiente comando para iniciar un productor y enviar mensajes al tema:</span><span class="sxs-lookup"><span data-stu-id="f5598-201">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="f5598-202">Reemplace `$PASSWORD` por la contraseña de inicio de sesión (del administrador) del clúster de origen.</span><span class="sxs-lookup"><span data-stu-id="f5598-202">Replace `$PASSWORD` with the login (admin) password for the source cluster.</span></span>

    <span data-ttu-id="f5598-203">Reemplace `$CLUSTERNAME` por el nombre del clúster de origen.</span><span class="sxs-lookup"><span data-stu-id="f5598-203">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span>

     <span data-ttu-id="f5598-204">Cuando llegue a una línea en blanco con un cursor, escriba algunos mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="f5598-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="f5598-205">Estos se envían al tema en el clúster de **origen**.</span><span class="sxs-lookup"><span data-stu-id="f5598-205">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="f5598-206">Cuando haya terminado, use **Ctrl + C** para finalizar el proceso de productor.</span><span class="sxs-lookup"><span data-stu-id="f5598-206">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="f5598-207">En la conexión SSH al clúster de **destino**, use **Ctrl + C** para iniciar el proceso de MirrorMaker.</span><span class="sxs-lookup"><span data-stu-id="f5598-207">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="f5598-208">A continuación, use los siguientes comandos para comprobar que el tema `testtopic` se creó y que los datos de dicho tema se han replicado a este reflejo:</span><span class="sxs-lookup"><span data-stu-id="f5598-208">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="f5598-209">Reemplace `$PASSWORD` por la contraseña de inicio de sesión (del administrador) del clúster de destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-209">Replace `$PASSWORD` with the login (admin) password for the destination cluster.</span></span>

    <span data-ttu-id="f5598-210">Reemplace `$CLUSTERNAME` por el nombre del clúster de destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-210">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="f5598-211">La lista de temas ahora incluye `testtopic`, que se crea cuando MirrorMaster refleja el tema desde el clúster de origen al destino.</span><span class="sxs-lookup"><span data-stu-id="f5598-211">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="f5598-212">Los mensajes que se recuperan desde el tema son los mismos que se introdujeron en el clúster de origen.</span><span class="sxs-lookup"><span data-stu-id="f5598-212">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="f5598-213">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="f5598-213">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f5598-214">Como el procedimiento descrito en este documento crea los dos clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5598-214">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="f5598-215">Al eliminar el grupo de recursos se eliminan también todos los recursos creados con el procedimiento descrito en este documento, Azure Virtual Network y la cuenta de almacenamiento que utilizan los clústeres.</span><span class="sxs-lookup"><span data-stu-id="f5598-215">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5598-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5598-216">Next Steps</span></span>

<span data-ttu-id="f5598-217">En este documento, aprendió a utilizar MirrorMaker para crear una réplica de un clúster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="f5598-217">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="f5598-218">Utilice los vínculos siguientes para conocer otras formas de trabajar con Kafka:</span><span class="sxs-lookup"><span data-stu-id="f5598-218">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="f5598-219">[Documentación de Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) en cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="f5598-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="f5598-220">Introducción a Apache Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5598-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="f5598-221">Uso de Apache Spark con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5598-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="f5598-222">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5598-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="f5598-223">Conexión a Kafka a través de una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="f5598-223">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
