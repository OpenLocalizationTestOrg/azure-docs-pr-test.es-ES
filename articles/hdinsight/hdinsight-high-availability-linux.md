---
title: disponibilidad de aaaHigh para Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información sobre cómo los clústeres de HDInsight mejoran la confiabilidad y la disponibilidad gracias al uso de un nodo principal extra. Obtenga información acerca de cómo esto afecta a los servicios Hadoop como Ambari y subárbol, así como la tooindividually conectar tooeach nodo principal mediante SSH."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="3755c-105">Disponibilidad y fiabilidad de clústeres de Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="3755c-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="3755c-106">Clústeres de HDInsight proporcionan dos nodos principales tooincrease Hola confiabilidad y disponibilidad de servicios de Hadoop y trabajos que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="3755c-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="3755c-107">Hadoop logra una alta disponibilidad y confiabilidad al replicar datos y servicios en varios nodos de un clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="3755c-108">Sin embargo, las distribuciones estándar de Hadoop suelen tener un único nodo principal.</span><span class="sxs-lookup"><span data-stu-id="3755c-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="3755c-109">Cualquier interrupción del nodo principal de hello único puede provocar trabajo toostop de hello clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="3755c-110">HDInsight proporciona dos headnodes tooimprove Hadoop disponibilidad y confiabilidad.</span><span class="sxs-lookup"><span data-stu-id="3755c-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3755c-111">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="3755c-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3755c-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3755c-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="3755c-113">Disponibilidad y confiabilidad de los nodos</span><span class="sxs-lookup"><span data-stu-id="3755c-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="3755c-114">Los nodos de un clúster de HDInsight se implementan mediante Máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3755c-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="3755c-115">Hello siguientes secciones describen los tipos de nodos individuales de hello usa con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3755c-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="3755c-116">No todos los tipos de nodo se utilizan para un tipo de clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="3755c-117">Por ejemplo, un tipo de clúster de Hadoop no tiene ningún nodo Nimbus.</span><span class="sxs-lookup"><span data-stu-id="3755c-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="3755c-118">Para obtener más información sobre nodos utilizados por tipos de clúster de HDInsight, vea la sección de tipos de clúster de Hola de hello [Hadoop basado en Linux crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="3755c-119">Nodos principales</span><span class="sxs-lookup"><span data-stu-id="3755c-119">Head nodes</span></span>

<span data-ttu-id="3755c-120">tooensure servicios de alta disponibilidad Hadoop, HDInsight proporciona dos nodos principales.</span><span class="sxs-lookup"><span data-stu-id="3755c-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="3755c-121">Ambos nodos principales están activo y en ejecución en el clúster de HDInsight de hello simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="3755c-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="3755c-122">Algunos servicios, como HDFS o YARN, solo están “activos” en un nodo principal en un determinado momento.</span><span class="sxs-lookup"><span data-stu-id="3755c-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="3755c-123">Otros servicios como HiveServer2 o tienda de metadatos de Hive están activos en ambos nodos principales en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="3755c-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="3755c-124">Los nodos principales (y otros nodos en HDInsight) tienen un valor numérico como parte del nombre de host de hello del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="3755c-125">Por ejemplo, `hn0-CLUSTERNAME` o `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="3755c-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3755c-126">No asocie valor numérico de Hola a si un nodo es principal ni secundario.</span><span class="sxs-lookup"><span data-stu-id="3755c-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="3755c-127">valor numérico de Hello es solo está presente tooprovide un nombre único para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="3755c-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="3755c-128">Nodos Nimbus</span><span class="sxs-lookup"><span data-stu-id="3755c-128">Nimbus Nodes</span></span>

<span data-ttu-id="3755c-129">Los nodos Nimbus están disponibles con los clústeres de Storm.</span><span class="sxs-lookup"><span data-stu-id="3755c-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="3755c-130">los nodos de Nimbus Hola proporcionar similar funcionalidad toohello Hadoop JobTracker, distribuir y supervisar el procesamiento a través de nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="3755c-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="3755c-131">HDInsight proporciona dos nodos Nimbus de clústeres de Storm.</span><span class="sxs-lookup"><span data-stu-id="3755c-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="3755c-132">Nodos Zookeeper</span><span class="sxs-lookup"><span data-stu-id="3755c-132">Zookeeper nodes</span></span>

<span data-ttu-id="3755c-133">Los nodos [ZooKeeper](http://zookeeper.apache.org/) sirven para seleccionar el líder de los servicios principales en los nodos principales.</span><span class="sxs-lookup"><span data-stu-id="3755c-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="3755c-134">También son utilizado tooinsure que servicios, los nodos de datos (trabajo) y las puertas de enlace saber qué nodo principal está activo en un servicio principal.</span><span class="sxs-lookup"><span data-stu-id="3755c-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="3755c-135">De forma predeterminada, HDInsight proporciona tres nodos ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="3755c-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="3755c-136">Nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="3755c-136">Worker nodes</span></span>

<span data-ttu-id="3755c-137">Nodos de trabajador realizan análisis de datos reales de hello cuando un trabajo está clúster toohello enviado.</span><span class="sxs-lookup"><span data-stu-id="3755c-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="3755c-138">Si se produce un error en un nodo de trabajo, tarea hello que estaba llevando a cabo es el nodo de trabajo tooanother enviado.</span><span class="sxs-lookup"><span data-stu-id="3755c-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="3755c-139">De forma predeterminada, HDInsight crea cuatro nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3755c-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="3755c-140">Puede cambiar este número toosuit sus necesidades durante y después de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="3755c-141">Nodo perimetral</span><span class="sxs-lookup"><span data-stu-id="3755c-141">Edge node</span></span>

<span data-ttu-id="3755c-142">Un nodo del borde no participar activamente en el análisis de datos en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="3755c-143">sino que lo usan desarrolladores o científicos de datos al trabajar con Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3755c-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="3755c-144">Hello borde nodo vida en Hola misma red Virtual de Azure como Hola otros nodos de clúster de Hola y puede tener acceso directamente a todos los demás nodos.</span><span class="sxs-lookup"><span data-stu-id="3755c-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="3755c-145">nodo de Hello borde puede utilizarse sin consumen recursos fuera de los servicios esenciales de Hadoop o los trabajos de análisis.</span><span class="sxs-lookup"><span data-stu-id="3755c-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="3755c-146">Actualmente, servidor de R en HDInsight es el único tipo de clúster de Hola que proporciona un nodo del borde de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3755c-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="3755c-147">Para servidor de R de HDInsight, se usa el nodo del borde Hola código de prueba R localmente en el nodo de hello antes del envío toohello clúster para el procesamiento distribuido.</span><span class="sxs-lookup"><span data-stu-id="3755c-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="3755c-148">Para obtener información sobre el uso de un nodo del borde con tipos de clúster que no sea servidor de R, vea hello [usar nodos perimetrales en HDInsight](hdinsight-apps-use-edge-node.md) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="3755c-149">Obtener acceso a los nodos de Hola</span><span class="sxs-lookup"><span data-stu-id="3755c-149">Accessing hello nodes</span></span>

<span data-ttu-id="3755c-150">Clúster de toohello de acceso a través de hello internet se proporciona a través de una puerta de enlace pública.</span><span class="sxs-lookup"><span data-stu-id="3755c-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="3755c-151">El acceso se nodos principales del toohello tooconnecting limitado y (si existe) Hola nodo del borde.</span><span class="sxs-lookup"><span data-stu-id="3755c-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="3755c-152">Tooservices de acceso que se ejecutan en nodos principales de hello no se realiza al tener varios nodos principales.</span><span class="sxs-lookup"><span data-stu-id="3755c-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="3755c-153">Hola pública de la puerta de enlace rutas solicitudes toohello nodo principal que hospeda Hola servicio solicitado.</span><span class="sxs-lookup"><span data-stu-id="3755c-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="3755c-154">Por ejemplo, si Ambari se hospede actualmente en el nodo principal secundario de hello, puerta de enlace de hello enruta las solicitudes entrantes de nodo de toothat de Ambari.</span><span class="sxs-lookup"><span data-stu-id="3755c-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="3755c-155">Acceso a través de puerta de enlace pública hello es limitado tooport 443 (HTTPS), 22 y 23.</span><span class="sxs-lookup"><span data-stu-id="3755c-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="3755c-156">Puerto __443__ es tooaccess usado Ambari y otros web API de REST hospedada en nodos principales de Hola o interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="3755c-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="3755c-157">Puerto __22__ es nodo principal de tooaccess usado Hola principal o perimetral mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="3755c-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="3755c-158">Puerto __23__ es tooaccess usado Hola secundario del nodo principal mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="3755c-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="3755c-159">Por ejemplo, `ssh username@mycluster-ssh.azurehdinsight.net` conecta toohello, principal, nodo principal del clúster Hola denominado **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="3755c-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="3755c-160">Para obtener más información sobre el uso de SSH, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="3755c-161">Nombres completos de dominio (FQDN) internos</span><span class="sxs-lookup"><span data-stu-id="3755c-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="3755c-162">Nodos en un clúster de HDInsight tienen una dirección IP y los FQDN que solo puede tener acceso desde el clúster de hello interno.</span><span class="sxs-lookup"><span data-stu-id="3755c-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="3755c-163">Al obtener acceso a servicios en un clúster de hello mediante Hola interna FQDN o dirección IP, debe usar Ambari tooverify Hola IP o FQDN toouse al tener acceso a servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="3755c-164">Por ejemplo, hello Oozie servicio solo puede ejecutarse en un nodo principal y el uso de hello `oozie` comando desde una sesión de SSH requiere el servicio de toohello de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="3755c-165">Esta dirección URL se puede recuperar desde Ambari mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3755c-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="3755c-166">Este comando devuelve un toohello similar valor siguiente comando, que contiene hello toouse de dirección URL interna con hello `oozie` comando:</span><span class="sxs-lookup"><span data-stu-id="3755c-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="3755c-167">Para obtener más información sobre cómo trabajar con hello Ambari API de REST, consulte [supervisar y administrar HDInsight con hello API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="3755c-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="3755c-168">Acceso a otros tipos de nodos</span><span class="sxs-lookup"><span data-stu-id="3755c-168">Accessing other node types</span></span>

<span data-ttu-id="3755c-169">Puede conectarse toonodes que están no directamente accesible over Hola internet utilizando Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="3755c-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="3755c-170">**SSH**: una vez conectado el nodo principal de tooa mediante SSH, a continuación, puede utilizar SSH desde Hola nodo principal tooconnect tooother nodos Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="3755c-171">Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="3755c-172">**Túnel SSH**: si necesita tooaccess un servicio web hospedado en uno de los nodos de Hola que no expone toohello internet, debe usar un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="3755c-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="3755c-173">Para obtener más información, vea hello [utilizar un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="3755c-174">**Red Virtual de Azure**: si HDInsight clúster forma parte de una red Virtual de Azure, cualquier recurso de Hola misma red Virtual puede acceder directamente a todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="3755c-175">Para obtener más información, vea hello [HDInsight extender mediante la red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="3755c-176">¿Cómo toocheck en un estado del servicio</span><span class="sxs-lookup"><span data-stu-id="3755c-176">How toocheck on a service status</span></span>

<span data-ttu-id="3755c-177">estado de hello toocheck de servicios que se ejecutan en nodos principales de hello, usar hello Ambari Web UI u Hola API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="3755c-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="3755c-178">Interfaz de usuario web de Ambari</span><span class="sxs-lookup"><span data-stu-id="3755c-178">Ambari Web UI</span></span>

<span data-ttu-id="3755c-179">Hola Ambari Web IU sea visible en https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3755c-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="3755c-180">Reemplace **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="3755c-181">Si se le solicite, escriba las credenciales de usuario HTTP de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="3755c-182">nombre de usuario HTTP de Hello predeterminado es **administración** y Hola contraseña es Hola que especificó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="3755c-183">Cuando llegan en la página de Ambari hello, aparecerán los servicios de hello instalado izquierda Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Servicios instalados](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="3755c-185">Hay una serie de iconos que pueden aparecer el siguiente estado de tooindicate del servicio de tooa.</span><span class="sxs-lookup"><span data-stu-id="3755c-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="3755c-186">Las alertas relacionadas con servicio tooa puede verse mediante hello **alertas** vínculo situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="3755c-187">Puede seleccionar cada servicio tooview más información sobre él.</span><span class="sxs-lookup"><span data-stu-id="3755c-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="3755c-188">Mientras la página del servicio Hola proporciona información sobre estado de Hola y la configuración de cada servicio, no proporciona información en el que se está ejecutando servicios de Hola de nodo principal.</span><span class="sxs-lookup"><span data-stu-id="3755c-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="3755c-189">tooview esta información, use hello **Hosts** vínculo situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="3755c-190">Esta página muestra los hosts en clúster de hello, incluidos los nodos principales de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![lista de hosts](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="3755c-192">Seleccionar vínculo de Hola de uno de los nodos principales de hello muestra servicios de Hola y componentes que se ejecutan en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="3755c-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Estado del componente](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="3755c-194">Para obtener más información sobre el uso de Ambari, consulte [Monitor y administrar HDInsight con Ambari Web UI hello](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="3755c-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="3755c-195">API de REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="3755c-195">Ambari REST API</span></span>

<span data-ttu-id="3755c-196">Hola Ambari REST API está disponible a través de hello internet.</span><span class="sxs-lookup"><span data-stu-id="3755c-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="3755c-197">puerta de enlace de Hello HDInsight pública controla las solicitudes toohello principal el nodo de enrutamiento que hospeda actualmente Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="3755c-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="3755c-198">Puede usar Hola después de estado de hello toocheck de comandos de un servicio a través de la API de REST de Ambari hello:</span><span class="sxs-lookup"><span data-stu-id="3755c-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="3755c-199">Reemplace **contraseña** con la contraseña de cuenta de usuario (admin) Hola HTTP.</span><span class="sxs-lookup"><span data-stu-id="3755c-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="3755c-200">Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="3755c-201">Reemplace **SERVICENAME** por nombre de hello del servicio de hello desea toocheck estado de Hola de.</span><span class="sxs-lookup"><span data-stu-id="3755c-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="3755c-202">Por ejemplo, toocheck estado Hola de hello **HDFS** servicio en un clúster denominado **mycluster**, con una contraseña de **contraseña**, usaría Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3755c-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="3755c-203">respuesta de Hello es toohello similar después de JSON:</span><span class="sxs-lookup"><span data-stu-id="3755c-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="3755c-204">Hello URL nos indica que el servicio de Hola se está ejecutando actualmente en un nodo principal denominado **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="3755c-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="3755c-205">Hello estado nos indica que se está ejecutando actualmente el servicio de hello, o **iniciado**.</span><span class="sxs-lookup"><span data-stu-id="3755c-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="3755c-206">Si no sabe qué servicios están instalados en el clúster de hello, puede usar Hola después tooretrieve una lista de comandos:</span><span class="sxs-lookup"><span data-stu-id="3755c-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="3755c-207">Para obtener más información sobre cómo trabajar con hello Ambari API de REST, consulte [supervisar y administrar HDInsight con hello API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="3755c-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="3755c-208">Componentes de servicio</span><span class="sxs-lookup"><span data-stu-id="3755c-208">Service components</span></span>

<span data-ttu-id="3755c-209">Los servicios pueden contener componentes que desee toocheck estado de Hola de forma individual.</span><span class="sxs-lookup"><span data-stu-id="3755c-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="3755c-210">Por ejemplo, HDFS contiene componentes de NameNode Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="3755c-211">tooview información en un componente, Hola comando sería:</span><span class="sxs-lookup"><span data-stu-id="3755c-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="3755c-212">Si no sabe qué componentes se proporcionan por un servicio, puede usar Hola después tooretrieve una lista de comandos:</span><span class="sxs-lookup"><span data-stu-id="3755c-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="3755c-213">¿Cómo tooaccess archivos de registro en nodos principales Hola</span><span class="sxs-lookup"><span data-stu-id="3755c-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="3755c-214">SSH</span><span class="sxs-lookup"><span data-stu-id="3755c-214">SSH</span></span>

<span data-ttu-id="3755c-215">Al nodo principal de tooa conectado a través de SSH, archivos de registro pueden encontrarse en **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="3755c-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="3755c-216">Por ejemplo, **/var/log/hadoop-yarn/yarn** contiene registros de YARN.</span><span class="sxs-lookup"><span data-stu-id="3755c-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="3755c-217">Cada nodo principal puede tener entradas del registro único, por lo que debe comprobar Hola inicia sesión en ambos.</span><span class="sxs-lookup"><span data-stu-id="3755c-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="3755c-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="3755c-218">SFTP</span></span>

<span data-ttu-id="3755c-219">También puede conectarse mediante Hola SSH File Transfer Protocol o protocolo de transferencia de archivo seguro (SFTP) del nodo principal toohello y descargar archivos de registro de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="3755c-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="3755c-220">Toousing similar un cliente de SSH, cuando se conecta el clúster toohello debe proporcionar Hola SSH usuario cuenta hello y nombre SSH dirección Hola del clúster de.</span><span class="sxs-lookup"><span data-stu-id="3755c-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="3755c-221">Por ejemplo: `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="3755c-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="3755c-222">Proporcionar contraseña hello para la cuenta de hello cuando se le solicite, o proporcionar una clave pública mediante hello `-i` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3755c-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="3755c-223">Una vez conectado, se le presentará un símbolo del sistema `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="3755c-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="3755c-224">Desde este símbolo del sistema, puede cambiar los directorios, cargar y descargar archivos.</span><span class="sxs-lookup"><span data-stu-id="3755c-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="3755c-225">Por ejemplo, hello siga los comandos cambia directorios toohello **/var/log/hadoop/hdfs** directorio y, a continuación, descarga todos los archivos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="3755c-226">Para obtener una lista de comandos disponibles, escriba `help` en hello `sftp>` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="3755c-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="3755c-227">También hay interfaces gráficas que le permiten el sistema de archivos de hello toovisualize cuando se conecta mediante SFTP.</span><span class="sxs-lookup"><span data-stu-id="3755c-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="3755c-228">Por ejemplo, [MobaXTerm](http://mobaxterm.mobatek.net/) le permite el sistema de archivos de hello toobrowse mediante un explorador de tooWindows similar de interfaz.</span><span class="sxs-lookup"><span data-stu-id="3755c-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="3755c-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="3755c-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="3755c-230">con Ambari de archivos de registro de tooaccess, debe utilizar un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="3755c-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="3755c-231">interfaces de Hello web para los servicios individuales de hello no se exponen públicamente en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="3755c-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="3755c-232">Para obtener información sobre el uso de un túnel SSH, vea hello [uso de SSH túnel](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="3755c-233">Desde la interfaz de usuario de Ambari Web hello, seleccione servicio de hello desea tooview registros (por ejemplo, YARN).</span><span class="sxs-lookup"><span data-stu-id="3755c-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="3755c-234">A continuación, utilice **vínculos rápidos** tooselect registra qué hello tooview de nodo principal para.</span><span class="sxs-lookup"><span data-stu-id="3755c-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Usar rápida vincula tooview registros](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="3755c-236">¿Cómo tooconfigure Hola tamaño de nodo</span><span class="sxs-lookup"><span data-stu-id="3755c-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="3755c-237">tamaño de Hola de un nodo solo puede seleccionarse durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="3755c-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="3755c-238">Se pueden encontrar una lista de Hola disponibles diferentes tamaños de máquina virtual de HDInsight en hello [HDInsight página de precios](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3755c-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="3755c-239">Al crear un clúster, puede especificar el tamaño de Hola de nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3755c-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="3755c-240">Hello siguiente información proporciona instrucciones sobre cómo toospecify Hola tamaño con Hola [portal de Azure][preview-portal], [Azure PowerShell][azure-powershell], hello y [CLI de Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="3755c-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="3755c-241">**Portal de Azure**: al crear un clúster, puede establecer tamaño de Hola de nodos de hello usado Hola clúster:</span><span class="sxs-lookup"><span data-stu-id="3755c-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Imagen del asistente para creación de clústeres con selección del tamaño del nodo](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="3755c-243">**CLI de Azure**: al usar hello `azure hdinsight cluster create` comando, puede establecer tamaño de Hola de head hello, trabajo y sus nodos ZooKeeper mediante hello `--headNodeSize`, `--workerNodeSize`, y `--zookeeperNodeSize` parámetros.</span><span class="sxs-lookup"><span data-stu-id="3755c-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="3755c-244">**Azure PowerShell**: al usar hello `New-AzureRmHDInsightCluster` cmdlet, puede establecer tamaño de Hola de hello head, trabajo y nodos de ZooKeeper mediante hello `-HeadNodeVMSize`, `-WorkerNodeSize`, y `-ZookeeperNodeSize` parámetros.</span><span class="sxs-lookup"><span data-stu-id="3755c-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3755c-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3755c-245">Next steps</span></span>

<span data-ttu-id="3755c-246">Usar hello siguiendo vínculos toolearn más sobre lo que se mencionan en este documento.</span><span class="sxs-lookup"><span data-stu-id="3755c-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="3755c-247">Referencia de REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="3755c-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="3755c-248">Instalar y configurar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3755c-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="3755c-249">Instalación y configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3755c-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="3755c-250">Administración de HDInsight mediante Ambari</span><span class="sxs-lookup"><span data-stu-id="3755c-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="3755c-251">Aprovisionamiento de clústeres de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="3755c-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
