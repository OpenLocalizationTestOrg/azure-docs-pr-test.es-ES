---
title: Alta disponibilidad de Hadoop - Azure HDInsight | Microsoft Docs
description: "Obtenga información sobre cómo los clústeres de HDInsight mejoran la confiabilidad y la disponibilidad gracias al uso de un nodo principal extra. Obtenga información sobre cómo esto afecta a los servicios de Hadoop como Ambari y Hive, y cómo conectarse individualmente a cada nodo principal mediante SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: hadoop alta disponibilidad
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="efc18-105">Disponibilidad y fiabilidad de clústeres de Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="efc18-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="efc18-106">Los clústeres de HDInsight proporcionan dos nodos principales para aumentar la disponibilidad y la confiabilidad de los servicios y trabajos de Hadoop en ejecución.</span><span class="sxs-lookup"><span data-stu-id="efc18-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="efc18-107">Hadoop logra una alta disponibilidad y confiabilidad al replicar datos y servicios en varios nodos de un clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="efc18-108">Sin embargo, las distribuciones estándar de Hadoop suelen tener un único nodo principal.</span><span class="sxs-lookup"><span data-stu-id="efc18-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="efc18-109">Cualquier interrupción de ese nodo principal puede causar que el clúster deje de funcionar.</span><span class="sxs-lookup"><span data-stu-id="efc18-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="efc18-110">HDInsight proporciona dos nodos principales para mejorar la disponibilidad y la confiabilidad de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="efc18-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efc18-111">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="efc18-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="efc18-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="efc18-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="efc18-113">Disponibilidad y confiabilidad de los nodos</span><span class="sxs-lookup"><span data-stu-id="efc18-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="efc18-114">Los nodos de un clúster de HDInsight se implementan mediante Máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="efc18-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="efc18-115">En las secciones siguientes se describen los tipos de nodo individuales usados con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="efc18-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="efc18-116">No todos los tipos de nodo se utilizan para un tipo de clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="efc18-117">Por ejemplo, un tipo de clúster de Hadoop no tiene ningún nodo Nimbus.</span><span class="sxs-lookup"><span data-stu-id="efc18-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="efc18-118">Para más información sobre los nodos usados por los tipos de clúster de HDInsight, vea la sección Tipos de clúster en el documento [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="efc18-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="efc18-119">Nodos principales</span><span class="sxs-lookup"><span data-stu-id="efc18-119">Head nodes</span></span>

<span data-ttu-id="efc18-120">HDInsight proporciona dos nodos principales para garantizar una alta disponibilidad de los servicios de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="efc18-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="efc18-121">Ambos nodos principales están activos y en ejecución dentro del clúster de HDInsight al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="efc18-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="efc18-122">Algunos servicios, como HDFS o YARN, solo están “activos” en un nodo principal en un determinado momento.</span><span class="sxs-lookup"><span data-stu-id="efc18-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="efc18-123">Otros servicios como HiveServer2 o MetaStore de Hive están activos en ambos nodos principales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="efc18-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="efc18-124">Los nodos principales y otros nodos de HDInsight tienen un valor numérico como parte del nombre de host del nodo.</span><span class="sxs-lookup"><span data-stu-id="efc18-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="efc18-125">Por ejemplo, `hn0-CLUSTERNAME` o `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="efc18-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efc18-126">No asocie el valor numérico a si un nodo es principal o secundario.</span><span class="sxs-lookup"><span data-stu-id="efc18-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="efc18-127">El valor numérico solo está presente para proporcionar un nombre único para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="efc18-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="efc18-128">Nodos Nimbus</span><span class="sxs-lookup"><span data-stu-id="efc18-128">Nimbus Nodes</span></span>

<span data-ttu-id="efc18-129">Los nodos Nimbus están disponibles con los clústeres de Storm.</span><span class="sxs-lookup"><span data-stu-id="efc18-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="efc18-130">Los nodos Nimbus proporcionan una funcionalidad similar a la de JobTracker de Hadoop al distribuir y supervisar el procesamiento a través de nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="efc18-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="efc18-131">HDInsight proporciona dos nodos Nimbus de clústeres de Storm.</span><span class="sxs-lookup"><span data-stu-id="efc18-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="efc18-132">Nodos Zookeeper</span><span class="sxs-lookup"><span data-stu-id="efc18-132">Zookeeper nodes</span></span>

<span data-ttu-id="efc18-133">Los nodos [ZooKeeper](http://zookeeper.apache.org/) sirven para seleccionar el líder de los servicios principales en los nodos principales.</span><span class="sxs-lookup"><span data-stu-id="efc18-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="efc18-134">También sirven para garantizar que los servicios, los nodos de datos (trabajo) y las puertas de enlace saben en qué nodo principal está activo un servicio principal.</span><span class="sxs-lookup"><span data-stu-id="efc18-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="efc18-135">De forma predeterminada, HDInsight proporciona tres nodos ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="efc18-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="efc18-136">Nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="efc18-136">Worker nodes</span></span>

<span data-ttu-id="efc18-137">Los nodos de trabajo realizan el análisis de los datos reales cuando se envía un trabajo al clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="efc18-138">Si se produce un error en un nodo de trabajo, la tarea que estaba realizando se envía a otro nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="efc18-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="efc18-139">De forma predeterminada, HDInsight crea cuatro nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="efc18-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="efc18-140">Puede cambiar este número para satisfacer sus necesidades durante y después de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="efc18-141">Nodo perimetral</span><span class="sxs-lookup"><span data-stu-id="efc18-141">Edge node</span></span>

<span data-ttu-id="efc18-142">El nodo perimetral no participa activamente en el análisis de datos dentro del clúster,</span><span class="sxs-lookup"><span data-stu-id="efc18-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="efc18-143">sino que lo usan desarrolladores o científicos de datos al trabajar con Hadoop.</span><span class="sxs-lookup"><span data-stu-id="efc18-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="efc18-144">El nodo perimetral se encuentra en la misma Red virtual de Azure como los demás nodos del clúster y puede acceder directamente a todos los demás nodos.</span><span class="sxs-lookup"><span data-stu-id="efc18-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="efc18-145">El nodo perimetral se puede usar sin tener que quitar recursos a los trabajos de análisis o servicios críticos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="efc18-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="efc18-146">Actualmente, el servidor de R en HDInsight es el único tipo de clúster que proporciona un nodo perimetral de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="efc18-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="efc18-147">Para el servidor de R en HDInsight, se usa el nodo perimetral para probar el código de R localmente en el nodo antes de enviarlo al clúster para su procesamiento distribuido.</span><span class="sxs-lookup"><span data-stu-id="efc18-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="efc18-148">Para más información sobre el uso de un nodo perimetral con tipos de clúster que no sean de R Server, consulte el documento [Uso de nodos perimetrales en HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="efc18-149">Acceso a los nodos</span><span class="sxs-lookup"><span data-stu-id="efc18-149">Accessing the nodes</span></span>

<span data-ttu-id="efc18-150">Se proporciona acceso al clúster a través de Internet mediante una puerta de enlace pública.</span><span class="sxs-lookup"><span data-stu-id="efc18-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="efc18-151">El acceso está limitado a la conexión a los nodos principales y, si existe, al nodo perimetral.</span><span class="sxs-lookup"><span data-stu-id="efc18-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="efc18-152">El hecho de contar con varios nodos principales no afecta al acceso a servicios que se ejecutan en los nodos principales.</span><span class="sxs-lookup"><span data-stu-id="efc18-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="efc18-153">La puerta de enlace pública enruta las solicitudes al nodo principal que hospeda el servicio solicitado.</span><span class="sxs-lookup"><span data-stu-id="efc18-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="efc18-154">Por ejemplo, si Ambari está hospedado en el nodo principal secundario, la puerta de enlace enruta las solicitudes entrantes de Ambari a ese nodo.</span><span class="sxs-lookup"><span data-stu-id="efc18-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="efc18-155">El acceso a través de la puerta de enlace pública se limita a los puertos 443 (HTTPS), 22 y 23.</span><span class="sxs-lookup"><span data-stu-id="efc18-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="efc18-156">El puerto __443__ se usa para acceder a Ambari y a otra interfaz de usuario web o API de REST hospedadas en los nodos principales.</span><span class="sxs-lookup"><span data-stu-id="efc18-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="efc18-157">El puerto __22__ se usa para acceder al nodo principal primario o al nodo perimetral mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="efc18-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="efc18-158">El puerto __23__ se usa para acceder al nodo principal secundario mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="efc18-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="efc18-159">Por ejemplo, `ssh username@mycluster-ssh.azurehdinsight.net` se conecta al nodo principal primario del clúster llamado **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="efc18-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="efc18-160">Para más información sobre cómo usar SSH, vea el documento [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="efc18-161">Nombres completos de dominio (FQDN) internos</span><span class="sxs-lookup"><span data-stu-id="efc18-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="efc18-162">Los nodos de un clúster de HDInsight tienen una dirección IP interna y el FQDN al que solo se puede acceder desde el clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="efc18-163">Al obtener acceso a servicios en el clúster mediante la dirección IP o FQDN interna, debe usar Ambari para comprobar la dirección IP o FQDN que se usará al obtener acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="efc18-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="efc18-164">Por ejemplo, el servicio de Oozie solo puede ejecutarse en un nodo principal y el uso del comando `oozie` desde una sesión de SSH requiere la dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="efc18-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="efc18-165">La dirección URL puede conseguirse en Ambari mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="efc18-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="efc18-166">Este comando devuelve un valor similar al siguiente comando, que contiene la dirección URL interna para usarla con el comando `oozie`:</span><span class="sxs-lookup"><span data-stu-id="efc18-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="efc18-167">Para más información sobre cómo trabajar con la API de REST de Ambari, vea [Supervisión y administración de HDInsight con la API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="efc18-168">Acceso a otros tipos de nodos</span><span class="sxs-lookup"><span data-stu-id="efc18-168">Accessing other node types</span></span>

<span data-ttu-id="efc18-169">Puede conectarse a los nodos que no son accesibles directamente a través de Internet mediante los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="efc18-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="efc18-170">**SSH**: una vez conectado a un nodo principal mediante SSH, puede usar SSH desde el nodo principal para conectarse a otros nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="efc18-171">Para más información, vea el documento [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="efc18-172">**Túnel SSH**: si tiene que acceder a un servicio web hospedado en uno de los nodos que no está expuesto a Internet, debe usar un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="efc18-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="efc18-173">Para más información, vea el documento [Uso de un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="efc18-174">**Azure Virtual Network**: si el clúster de HDInsight forma parte de una red de Azure Virtual Network, cualquier recurso en la misma red virtual puede acceder directamente a todos los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="efc18-175">Para más información, vea el documento [Extensión de las funcionalidades de HDInsight con Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="efc18-176">Cómo comprobar el estado del servicio</span><span class="sxs-lookup"><span data-stu-id="efc18-176">How to check on a service status</span></span>

<span data-ttu-id="efc18-177">Para comprobar el estado de los servicios que se ejecutan en el nodo principal, use la interfaz de usuario web de Ambari o la API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="efc18-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="efc18-178">Interfaz de usuario web de Ambari</span><span class="sxs-lookup"><span data-stu-id="efc18-178">Ambari Web UI</span></span>

<span data-ttu-id="efc18-179">La interfaz de usuario web de Ambari es visible en https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="efc18-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="efc18-180">Reemplace **CLUSTERNAME** por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="efc18-181">Si se le solicita, introduzca las credenciales de usuario HTTP de su clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="efc18-182">El nombre de usuario HTTP predeterminado es **admin** y la contraseña es la contraseña que especificó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="efc18-183">Cuando llegue a la página de Ambari, se enumeran los servicios instalados a la izquierda de la página.</span><span class="sxs-lookup"><span data-stu-id="efc18-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Servicios instalados](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="efc18-185">Hay una serie de iconos que pueden aparecer junto a un servicio para indicar el estado.</span><span class="sxs-lookup"><span data-stu-id="efc18-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="efc18-186">Las alertas relacionadas con un servicio se pueden ver mediante el vínculo **Alertas** que se encuentra en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="efc18-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="efc18-187">Puede seleccionar cada servicio para ver más información sobre él.</span><span class="sxs-lookup"><span data-stu-id="efc18-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="efc18-188">Mientras que la página del servicio proporciona información sobre el estado y la configuración de cada servicio, no proporciona información sobre en qué nodo principal se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="efc18-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="efc18-189">Para ver esta información, use el vínculo **Hosts** de la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="efc18-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="efc18-190">En esta página se muestran los hosts del clúster, incluidos los nodos principales.</span><span class="sxs-lookup"><span data-stu-id="efc18-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![lista de hosts](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="efc18-192">Al seleccionar el vínculo de uno de los nodos principales se muestran los servicios y componentes que se ejecutan en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="efc18-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Estado del componente](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="efc18-194">Para más información sobre el uso de Ambari, vea [Supervisión y administración de HDInsight con la interfaz de usuario web de Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="efc18-195">API de REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="efc18-195">Ambari REST API</span></span>

<span data-ttu-id="efc18-196">La API de REST de Ambari está disponible en Internet.</span><span class="sxs-lookup"><span data-stu-id="efc18-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="efc18-197">La puerta de enlace pública de HDInsight controla las solicitudes de enrutamiento dirigidas al nodo principal que hospeda actualmente la API de REST.</span><span class="sxs-lookup"><span data-stu-id="efc18-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="efc18-198">Puede usar el siguiente comando para comprobar el estado de un servicio a través de la API de REST de Ambari:</span><span class="sxs-lookup"><span data-stu-id="efc18-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="efc18-199">Reemplace **PASSWORD** por la contraseña de la cuenta del usuario (admin) HTTP.</span><span class="sxs-lookup"><span data-stu-id="efc18-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="efc18-200">Reemplace **CLUSTERNAME** por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="efc18-201">Reemplace **SERVICENAME** por el nombre del servicio cuyo estado quiere conocer.</span><span class="sxs-lookup"><span data-stu-id="efc18-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="efc18-202">Por ejemplo, para comprobar el estado del servicio **HDFS** en un clúster denominado **mycluster**, con la contraseña **password**, debería usar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="efc18-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="efc18-203">La respuesta es similar al siguiente formato JSON:</span><span class="sxs-lookup"><span data-stu-id="efc18-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="efc18-204">La dirección URL nos indica que el servicio se está ejecutando en el nodo principal **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="efc18-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="efc18-205">El estado nos indica que el servicio se está ejecutando o se ha **INICIADO**.</span><span class="sxs-lookup"><span data-stu-id="efc18-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="efc18-206">Si no sabe qué servicios están instalados en el clúster, puede usar el comando siguiente para recuperar una lista:</span><span class="sxs-lookup"><span data-stu-id="efc18-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="efc18-207">Para más información sobre cómo trabajar con la API de REST de Ambari, vea [Supervisión y administración de HDInsight con la API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="efc18-208">Componentes de servicio</span><span class="sxs-lookup"><span data-stu-id="efc18-208">Service components</span></span>

<span data-ttu-id="efc18-209">Los servicios pueden contener componentes cuyo estado desea comprobar de forma individual.</span><span class="sxs-lookup"><span data-stu-id="efc18-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="efc18-210">Por ejemplo, HDFS contiene el componente NameNode.</span><span class="sxs-lookup"><span data-stu-id="efc18-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="efc18-211">Para ver información sobre un componente, el comando sería:</span><span class="sxs-lookup"><span data-stu-id="efc18-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="efc18-212">Si no sabe qué componentes proporciona un servicio, puede usar el comando siguiente para recuperar una lista:</span><span class="sxs-lookup"><span data-stu-id="efc18-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="efc18-213">Acceso a los archivos de registro en los nodos principales</span><span class="sxs-lookup"><span data-stu-id="efc18-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="efc18-214">SSH</span><span class="sxs-lookup"><span data-stu-id="efc18-214">SSH</span></span>

<span data-ttu-id="efc18-215">Mientras está conectado a un nodo principal a través de SSH, los archivos de registro pueden encontrarse en **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="efc18-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="efc18-216">Por ejemplo, **/var/log/hadoop-yarn/yarn** contiene registros de YARN.</span><span class="sxs-lookup"><span data-stu-id="efc18-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="efc18-217">Cada nodo principal puede tener entradas de registro único, por lo que debe comprobar los registros en ambos.</span><span class="sxs-lookup"><span data-stu-id="efc18-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="efc18-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="efc18-218">SFTP</span></span>

<span data-ttu-id="efc18-219">También se puede conectar con el nodo principal mediante el protocolo SSH File Transfer Protocol o el protocolo seguro de transferencia de archivos (SFTP) y descargar los archivos de registro directamente.</span><span class="sxs-lookup"><span data-stu-id="efc18-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="efc18-220">De igual forma a utilizar un cliente SSH, al conectarse al clúster debe proporcionar el nombre de cuenta de usuario SSH y la dirección SSH del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="efc18-221">Por ejemplo: `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="efc18-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="efc18-222">Especifique la contraseña de la cuenta cuando se le solicite o proporcione una clave pública con el parámetro `-i`.</span><span class="sxs-lookup"><span data-stu-id="efc18-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="efc18-223">Una vez conectado, se le presentará un símbolo del sistema `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="efc18-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="efc18-224">Desde este símbolo del sistema, puede cambiar los directorios, cargar y descargar archivos.</span><span class="sxs-lookup"><span data-stu-id="efc18-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="efc18-225">Por ejemplo, los siguientes comandos cambian los directorios al directorio **/var/log/hadoop/hdfs** y después descargan todos los archivos en el directorio.</span><span class="sxs-lookup"><span data-stu-id="efc18-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="efc18-226">Para ver una lista de comandos disponibles, escriba `help` en el símbolo del sistema `sftp>`.</span><span class="sxs-lookup"><span data-stu-id="efc18-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="efc18-227">También hay interfaces gráficas que le permiten visualizar el sistema de archivos cuando se conecta mediante SFTP.</span><span class="sxs-lookup"><span data-stu-id="efc18-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="efc18-228">Por ejemplo, [MobaXTerm](http://mobaxterm.mobatek.net/) le permite examinar el sistema de archivos mediante una interfaz similar al Explorador de Windows.</span><span class="sxs-lookup"><span data-stu-id="efc18-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="efc18-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="efc18-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="efc18-230">Para acceder a archivos de registro mediante Ambari, debe usar un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="efc18-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="efc18-231">Las interfaces web de los servicios individuales no se exponen públicamente en Internet.</span><span class="sxs-lookup"><span data-stu-id="efc18-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="efc18-232">Para más información sobre cómo usar el túnel SSH, vea el documento [Uso de la tunelación SSH](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="efc18-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="efc18-233">En la interfaz de usuario web de Ambari, seleccione el servicio para el que desea consultar los registros (por ejemplo, YARN).</span><span class="sxs-lookup"><span data-stu-id="efc18-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="efc18-234">Después, utilice **Vínculos rápidos** para seleccionar de qué nodo principal desea consultar los registros.</span><span class="sxs-lookup"><span data-stu-id="efc18-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Uso de vínculos rápidos para ver los registros](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="efc18-236">Configuración del tamaño del nodo</span><span class="sxs-lookup"><span data-stu-id="efc18-236">How to configure the node size</span></span>

<span data-ttu-id="efc18-237">El tamaño de un nodo solo se puede seleccionar durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="efc18-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="efc18-238">Puede encontrar una lista de los diferentes tamaños de máquina virtual disponibles para HDInsight en la [página de precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="efc18-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="efc18-239">Al crear un clúster, puede especificar el tamaño de los nodos.</span><span class="sxs-lookup"><span data-stu-id="efc18-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="efc18-240">A continuación se ofrece información sobre cómo especificar el tamaño mediante [Azure Portal][preview-portal], [Azure PowerShell][azure-powershell] y la [CLI de Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="efc18-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="efc18-241">**Azure Portal**: al crear un clúster, puede establecer el tamaño de los nodos que usa el clúster:</span><span class="sxs-lookup"><span data-stu-id="efc18-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Imagen del asistente para creación de clústeres con selección del tamaño del nodo](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="efc18-243">**CLI de Azure**: cuando se usa el comando `azure hdinsight cluster create`, puede establecer el tamaño de los nodos principal, de trabajo y ZooKeeper mediante los parámetros `--headNodeSize`, `--workerNodeSize` y `--zookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="efc18-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="efc18-244">**Azure PowerShell**: cuando se usa el cmdlet `New-AzureRmHDInsightCluster`, puede establecer el tamaño de los nodos principal, de trabajo y ZooKeeper mediante los parámetros `-HeadNodeVMSize`, `-WorkerNodeSize` y `-ZookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="efc18-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efc18-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efc18-245">Next steps</span></span>

<span data-ttu-id="efc18-246">Use los siguientes vínculos para obtener más información sobre los aspectos que se mencionan en este documento.</span><span class="sxs-lookup"><span data-stu-id="efc18-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="efc18-247">Referencia de REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="efc18-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="efc18-248">Instalación y configuración de la interfaz de la línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="efc18-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="efc18-249">Instale y configure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efc18-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="efc18-250">Administración de HDInsight mediante Ambari</span><span class="sxs-lookup"><span data-stu-id="efc18-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="efc18-251">Aprovisionamiento de clústeres de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="efc18-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
