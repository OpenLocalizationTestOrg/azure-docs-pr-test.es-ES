---
title: "replicación de clúster de HBase aaaConfigure dentro de redes virtuales - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure HBase replicación equilibrio de carga, alta disponibilidad, sin tiempos de inactividad migración o actualización de una tooanother de versión de HDInsight y recuperación ante desastres."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="d6e35-103">Configuración de la replicación de clúster de HBase en redes virtuales</span><span class="sxs-lookup"><span data-stu-id="d6e35-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="d6e35-104">Obtenga información acerca de cómo tooconfigure HBase replicación en una red virtual (VNet) o entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d6e35-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="d6e35-105">La replicación de clúster usa una metodología de inserción de origen.</span><span class="sxs-lookup"><span data-stu-id="d6e35-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="d6e35-106">Un clúster de HBase puede ser un origen, un destino o cumplir ambos roles a la vez.</span><span class="sxs-lookup"><span data-stu-id="d6e35-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="d6e35-107">La replicación es asincrónica y objetivo de Hola de replicación es coherencia definitiva.</span><span class="sxs-lookup"><span data-stu-id="d6e35-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="d6e35-108">Cuando el origen de Hola recibe una familia de columna de tooa de edición con la replicación habilitada, editar es tooall propagado clústeres de destino.</span><span class="sxs-lookup"><span data-stu-id="d6e35-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="d6e35-109">Cuando se replican datos desde un tooanother de clúster, clúster de origen de Hola y todos los clústeres que ya se han utilizado datos Hola son sometidos a seguimiento tooprevent replicación bucles.</span><span class="sxs-lookup"><span data-stu-id="d6e35-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="d6e35-110">En este tutorial, configurará una replicación de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="d6e35-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="d6e35-111">Para otras topologías de clúster, consulte [Guía de referencia de HBase Apache](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="d6e35-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="d6e35-112">Casos de uso de replicación de HBase para una única red virtual:</span><span class="sxs-lookup"><span data-stu-id="d6e35-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="d6e35-113">Equilibrio de carga, por ejemplo, ejecutando exámenes o trabajos MapReduce en clúster de destino de hello e introducción de datos en clúster de origen Hola</span><span class="sxs-lookup"><span data-stu-id="d6e35-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="d6e35-114">Alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d6e35-114">High availability</span></span>
* <span data-ttu-id="d6e35-115">Migrar datos desde un tooanother de clúster de HBase</span><span class="sxs-lookup"><span data-stu-id="d6e35-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="d6e35-116">Actualizar un clúster de HDInsight de Azure desde una tooanother de versión</span><span class="sxs-lookup"><span data-stu-id="d6e35-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="d6e35-117">Casos de uso de replicación de HBase para dos redes virtuales:</span><span class="sxs-lookup"><span data-stu-id="d6e35-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="d6e35-118">Recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="d6e35-118">Disaster recovery</span></span>
* <span data-ttu-id="d6e35-119">Creación de particiones de aplicación hello y equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="d6e35-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="d6e35-120">Alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d6e35-120">High availability</span></span>

<span data-ttu-id="d6e35-121">Puede replicar clústeres mediante scripts de [acción de script](hdinsight-hadoop-customize-cluster-linux.md) que se encuentran en [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="d6e35-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6e35-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6e35-122">Prerequisites</span></span>
<span data-ttu-id="d6e35-123">Antes de comenzar este tutorial, debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="d6e35-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="d6e35-124">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d6e35-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="d6e35-125">Configurar entornos de Hola</span><span class="sxs-lookup"><span data-stu-id="d6e35-125">Configure hello environments</span></span>

<span data-ttu-id="d6e35-126">Hay tres opciones de configuración posibles:</span><span class="sxs-lookup"><span data-stu-id="d6e35-126">There are three possible configurations:</span></span>

- <span data-ttu-id="d6e35-127">Dos clústeres de HBase en una única red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="d6e35-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="d6e35-128">Dos clústeres de HBase en dos redes virtuales diferentes en Hola misma región</span><span class="sxs-lookup"><span data-stu-id="d6e35-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="d6e35-129">Dos clústeres de HBase en dos redes virtuales diferentes de dos regiones distintas (replicación geográfica)</span><span class="sxs-lookup"><span data-stu-id="d6e35-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="d6e35-130">toomake lo más fácil de entornos de hello tooconfigure, hemos creado algunos [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6e35-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d6e35-131">Si prefiere entornos de hello tooconfigure mediante otros métodos, consulte:</span><span class="sxs-lookup"><span data-stu-id="d6e35-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="d6e35-132">Creación de clústeres de Hadoop basados en Linux en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6e35-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- <span data-ttu-id="d6e35-133">[Create HBase clusters in Azure Virtual Network](hdinsight-hbase-provision-vnet.md) (Creación de clústeres de HBase en Azure Virtual Network)</span><span class="sxs-lookup"><span data-stu-id="d6e35-133">[Create HBase clusters in Azure Virtual Network](hdinsight-hbase-provision-vnet.md)</span></span>

### <a name="configure-one-virtual-network"></a><span data-ttu-id="d6e35-134">Configuración de una única red virtual</span><span class="sxs-lookup"><span data-stu-id="d6e35-134">Configure one virtual network</span></span>

<span data-ttu-id="d6e35-135">Haga clic en hello después imagen toocreate dos HBase clústeres Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="d6e35-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="d6e35-136">Hola plantilla se almacena en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="d6e35-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="d6e35-137">Configurar dos redes virtuales en hello misma región</span><span class="sxs-lookup"><span data-stu-id="d6e35-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="d6e35-138">Haga clic en hello después imagen toocreate dos redes virtuales con intercambio de tráfico de red virtual y dos clústeres de HBase en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="d6e35-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="d6e35-139">Hola plantilla se almacena en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="d6e35-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="d6e35-140">Este escenario requiere [emparejamiento de VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6e35-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="d6e35-141">plantilla de Hello permite el intercambio de tráfico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="d6e35-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="d6e35-142">Replicación de HBase utiliza direcciones IP de hello ZooKeeper las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d6e35-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="d6e35-143">Debe configurar las direcciones IP estáticas para los nodos de HBase ZooKeeper de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="d6e35-144">**direcciones IP estáticas tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="d6e35-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="d6e35-145">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6e35-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6e35-146">Hola menú izquierdo, haga clic en **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="d6e35-147">Haga clic en el grupo de recursos que contiene el clúster de HBase de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="d6e35-148">Se trata de un grupo de recursos de Hola que especificó cuando se usa el entorno hello toocreate plantillas de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="d6e35-149">Puede usar Hola filtro toonarrow hacia abajo de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="d6e35-150">Puede ver una lista de recursos que contiene las dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="d6e35-151">Haga clic en la red virtual de Hola que contiene el clúster de HBase de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="d6e35-152">Por ejemplo, haga clic en **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="d6e35-153">Puede ver tres dispositivos con nombres que empiezan por **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="d6e35-154">Los dispositivos están las máquinas virtuales de hello tres ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="d6e35-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="d6e35-155">Haga clic en uno de hello ZooKeeper las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d6e35-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="d6e35-156">Haga clic en **IP configurations** (Configuraciones IP).</span><span class="sxs-lookup"><span data-stu-id="d6e35-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="d6e35-157">Haga clic en **ipConfig1** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="d6e35-158">Haga clic en **estático**y anote la dirección IP real de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="d6e35-159">Necesitará la dirección IP de hello cuando ejecuta la replicación de tooenable de acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![Dirección IP estática ZooKeeper de replicación de HBase para HDInsight](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="d6e35-161">Repita el paso 6 tooset Hola IP estática para hello otros dos nodos ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="d6e35-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="d6e35-162">Para el escenario de red virtual entre hello, debe usar hello **- ip** cambiar al llamar a hello **hdi_enable_replication.sh** acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d6e35-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="d6e35-163">Configuración de dos redes virtuales en dos regiones distintas</span><span class="sxs-lookup"><span data-stu-id="d6e35-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="d6e35-164">Haga clic en hello después imagen toocreate dos redes virtuales en dos regiones diferentes.</span><span class="sxs-lookup"><span data-stu-id="d6e35-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="d6e35-165">plantilla de Hola se almacena en un contenedor de blobs de Azure público.</span><span class="sxs-lookup"><span data-stu-id="d6e35-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="d6e35-166">Crear una puerta de enlace VPN entre las dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="d6e35-167">Para obtener instrucciones, consulte [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) (Creación de una red virtual con una conexión de sitio a sitio).</span><span class="sxs-lookup"><span data-stu-id="d6e35-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="d6e35-168">Replicación de HBase utiliza direcciones IP de hello ZooKeeper las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d6e35-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="d6e35-169">Debe configurar las direcciones IP estáticas para los nodos de HBase ZooKeeper de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="d6e35-170">tooconfigure dirección IP estática, consulte la sección "configurar dos redes virtuales en Hola misma región" de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="d6e35-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="d6e35-171">Para el escenario de red virtual entre hello, debe usar hello **- ip** cambiar al llamar a hello **hdi_enable_replication.sh** acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d6e35-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="d6e35-172">Carga de datos de prueba</span><span class="sxs-lookup"><span data-stu-id="d6e35-172">Load test data</span></span>

<span data-ttu-id="d6e35-173">Cuando se replica un clúster, debe especificar Hola tablas tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d6e35-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="d6e35-174">En esta sección, se cargará algunos datos en clúster de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="d6e35-175">En la siguiente sección hello, permitirá que la replicación entre dos clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="d6e35-176">Siga las instrucciones de hello en [HBase tutorial: Introducción al uso de HBase de Apache con basado en Linux, Hadoop en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate un **contactos** tabla e insertar algunos datos en la tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="d6e35-177">Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="d6e35-177">Enable replication</span></span>

<span data-ttu-id="d6e35-178">Hola siguientes pasos muestra cómo toocall Hola acción de script de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6e35-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="d6e35-179">Para ejecutar una acción de secuencia de comandos mediante el uso de hello interfaz de línea de comandos (CLI) de Azure y Azure PowerShell, consulte [clústeres de HDInsight basados en Linux personalizar mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d6e35-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="d6e35-180">**replicación de HBase tooenable de hello portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="d6e35-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="d6e35-181">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6e35-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6e35-182">Abra el clúster de HBase de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="d6e35-183">En el menú de clúster de hello, haga clic en **acciones de Script**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="d6e35-184">Haga clic en **Enviar nueva** de arriba Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="d6e35-185">Seleccione o escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d6e35-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="d6e35-186">**Nombre** especifique **Enable replication** (Habilitar replicación).</span><span class="sxs-lookup"><span data-stu-id="d6e35-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="d6e35-187">**URL de script de Bash**: escriba **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="d6e35-188">**Principal**: seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d6e35-188">**Head**: Selected.</span></span> <span data-ttu-id="d6e35-189">Desactive Hola otros tipos de nodos.</span><span class="sxs-lookup"><span data-stu-id="d6e35-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="d6e35-190">**Parámetros**: siguiente Hola parámetros Habilitar replicación para todas las tablas existentes de Hola de ejemplo y copiar todos los datos de Hola Hola origen clúster toohello destino clúster:</span><span class="sxs-lookup"><span data-stu-id="d6e35-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="d6e35-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-191">Click **Create**.</span></span> <span data-ttu-id="d6e35-192">script de Hola puede tardar algún tiempo, especialmente cuando se usa el argumento - copydata de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="d6e35-193">Argumentos necesarios:</span><span class="sxs-lookup"><span data-stu-id="d6e35-193">Required arguments:</span></span>

|<span data-ttu-id="d6e35-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="d6e35-194">Name</span></span>|<span data-ttu-id="d6e35-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="d6e35-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="d6e35-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="d6e35-196">-s, --src-cluster</span></span> | <span data-ttu-id="d6e35-197">Especifique el nombre DNS de hello del clúster de HBase de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="d6e35-198">Por ejemplo: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="d6e35-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="d6e35-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="d6e35-199">-d, --dst-cluster</span></span> | <span data-ttu-id="d6e35-200">Especifique el nombre DNS de hello del destino de hello (réplica) de clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="d6e35-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="d6e35-201">Por ejemplo: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="d6e35-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="d6e35-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="d6e35-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="d6e35-203">Especifique la contraseña de administrador de Hola para Ambari en clúster de HBase de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="d6e35-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="d6e35-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="d6e35-205">Especifique la contraseña de administrador de Hola para Ambari en clúster de HBase de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="d6e35-206">Argumentos opcionales:</span><span class="sxs-lookup"><span data-stu-id="d6e35-206">Optional arguments:</span></span>

|<span data-ttu-id="d6e35-207">Nombre</span><span class="sxs-lookup"><span data-stu-id="d6e35-207">Name</span></span>|<span data-ttu-id="d6e35-208">Descripción</span><span class="sxs-lookup"><span data-stu-id="d6e35-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="d6e35-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="d6e35-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="d6e35-210">Especificar nombre de usuario de administrador de Hola para Ambari en clúster de HBase de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="d6e35-211">es el valor predeterminado de Hello **administración**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="d6e35-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="d6e35-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="d6e35-213">Especificar nombre de usuario de administrador de Hola para Ambari en clúster de HBase de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="d6e35-214">es el valor predeterminado de Hello **administración**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="d6e35-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="d6e35-215">-t, --table-list</span></span> | <span data-ttu-id="d6e35-216">Especifique hello toobe de tablas replicada.</span><span class="sxs-lookup"><span data-stu-id="d6e35-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="d6e35-217">Por ejemplo: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="d6e35-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="d6e35-218">Si no se especifica unas tablas determinadas, se replican todas las tablas de HBase existentes.</span><span class="sxs-lookup"><span data-stu-id="d6e35-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="d6e35-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="d6e35-219">-m, --machine</span></span> | <span data-ttu-id="d6e35-220">Especificar el nodo principal de Hola donde se ejecutará la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6e35-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="d6e35-221">valor de Hello es hn1 o hn0.</span><span class="sxs-lookup"><span data-stu-id="d6e35-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="d6e35-222">Dado que hn0 suele estar más ocupado, se recomienda utilizar hn1.</span><span class="sxs-lookup"><span data-stu-id="d6e35-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="d6e35-223">Utilice esta opción si estás ejecutando script de Hola $0 como una acción de secuencia de comandos desde el portal de HDInsight de Hola o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6e35-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="d6e35-224">-ip</span><span class="sxs-lookup"><span data-stu-id="d6e35-224">-ip</span></span> | <span data-ttu-id="d6e35-225">Este argumento es necesario cuando se habilita la replicación entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d6e35-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="d6e35-226">Este argumento actúa como un conmutador toouse Hola estático direcciones IP de ZooKeeper los nodos de clústeres de réplica en lugar de nombres FQDN.</span><span class="sxs-lookup"><span data-stu-id="d6e35-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="d6e35-227">Hola toobe de direcciones IP estática necesidad preconfigurado antes de habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="d6e35-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="d6e35-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="d6e35-228">-cp, -copydata</span></span> | <span data-ttu-id="d6e35-229">Habilite la migración de Hola de los datos existentes en las tablas de Hola donde está habilitada la replicación.</span><span class="sxs-lookup"><span data-stu-id="d6e35-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="d6e35-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="d6e35-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="d6e35-231">Habilita la replicación en las tablas del sistema Phoenix.</span><span class="sxs-lookup"><span data-stu-id="d6e35-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="d6e35-232">*Esta opción se debe utilizar con precaución.*</span><span class="sxs-lookup"><span data-stu-id="d6e35-232">*Use this option with caution.*</span></span> <span data-ttu-id="d6e35-233">Se recomienda volver a crear tablas de Phoenix en clústeres de réplica antes de utilizar este script.</span><span class="sxs-lookup"><span data-stu-id="d6e35-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="d6e35-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="d6e35-234">-h, --help</span></span> | <span data-ttu-id="d6e35-235">Muestra información de uso.</span><span class="sxs-lookup"><span data-stu-id="d6e35-235">Display usage information.</span></span> |

<span data-ttu-id="d6e35-236">Hola print_usage() sección de hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) proporciona una explicación detallada de parámetros.</span><span class="sxs-lookup"><span data-stu-id="d6e35-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="d6e35-237">Después de acción de secuencia de comandos de hello correctamente implementado, puede usar clúster de HBase SSH tooconnect toohello destino y comprobar datos Hola se han replicado.</span><span class="sxs-lookup"><span data-stu-id="d6e35-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="d6e35-238">Escenarios de replicación</span><span class="sxs-lookup"><span data-stu-id="d6e35-238">Replication scenarios</span></span>

<span data-ttu-id="d6e35-239">Hello lista siguiente muestra algunos casos de uso general y sus valores de parámetro:</span><span class="sxs-lookup"><span data-stu-id="d6e35-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="d6e35-240">**Habilitar la replicación en todas las tablas entre clústeres de hello dos**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="d6e35-241">Este escenario no requiere Hola copia/migración de datos existentes en las tablas de hello y no utiliza tablas de Phoenix.</span><span class="sxs-lookup"><span data-stu-id="d6e35-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="d6e35-242">Usar hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6e35-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="d6e35-243">**Habilitar la replicación en tablas específicas**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="d6e35-244">Usar hello después de la replicación de tooenable parámetros en table1, table2 y table3:</span><span class="sxs-lookup"><span data-stu-id="d6e35-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="d6e35-245">**Habilitar la replicación en tablas específicas y copie los datos existentes de hello**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="d6e35-246">Usar hello después de la replicación de tooenable parámetros en table1, table2 y table3:</span><span class="sxs-lookup"><span data-stu-id="d6e35-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="d6e35-247">**Habilitar la replicación en todas las tablas con replicar phoenix metadatos de origen toodestination**.</span><span class="sxs-lookup"><span data-stu-id="d6e35-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="d6e35-248">La replicación de metadatos de Phoenix no es perfecta, así que debe habilitarse con precaución.</span><span class="sxs-lookup"><span data-stu-id="d6e35-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="d6e35-249">Copia y migración de datos</span><span class="sxs-lookup"><span data-stu-id="d6e35-249">Copy and migrate data</span></span>

<span data-ttu-id="d6e35-250">Hay dos scripts de acción de script independientes para copiar o migrar datos después de habilitar la replicación:</span><span class="sxs-lookup"><span data-stu-id="d6e35-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="d6e35-251">[Secuencia de comandos para tablas pequeñas](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (unos pocos gigabytes de tamaño y general copia es toofinish esperado en menos de una hora)</span><span class="sxs-lookup"><span data-stu-id="d6e35-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="d6e35-252">[Secuencia de comandos para tablas grandes](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (se esperaba tootake más de una hora toocopy)</span><span class="sxs-lookup"><span data-stu-id="d6e35-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="d6e35-253">Puede seguir Hola mismo procedimiento en [habilitar la replicación](#enable-replication) toocall Hola Generar script de acción con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6e35-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="d6e35-254">Hola print_usage() sección de hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) ofrece una descripción detallada de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="d6e35-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="d6e35-255">Escenarios</span><span class="sxs-lookup"><span data-stu-id="d6e35-255">Scenarios</span></span>

- <span data-ttu-id="d6e35-256">**Copiar tablas específicas (test1, test2 y test3) para todas las filas editadas hasta ahora (marca de tiempo actual)**:</span><span class="sxs-lookup"><span data-stu-id="d6e35-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="d6e35-257">o</span><span class="sxs-lookup"><span data-stu-id="d6e35-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="d6e35-258">**Copiar tablas específicas con el intervalo de tiempo especificado**:</span><span class="sxs-lookup"><span data-stu-id="d6e35-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="d6e35-259">Deshabilitar replicación</span><span class="sxs-lookup"><span data-stu-id="d6e35-259">Disable replication</span></span>

<span data-ttu-id="d6e35-260">replicación de toodisable, usa otro script de acción de secuencia de comandos situada [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="d6e35-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="d6e35-261">Puede seguir Hola mismo procedimiento en [habilitar la replicación](#enable-replication) toocall Hola Generar script de acción con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6e35-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="d6e35-262">Hola print_usage() sección de hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) proporciona una explicación detallada de parámetros.</span><span class="sxs-lookup"><span data-stu-id="d6e35-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="d6e35-263">Escenarios</span><span class="sxs-lookup"><span data-stu-id="d6e35-263">Scenarios</span></span>

- <span data-ttu-id="d6e35-264">**Deshabilitar la replicación en todas las tablas**:</span><span class="sxs-lookup"><span data-stu-id="d6e35-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="d6e35-265">o</span><span class="sxs-lookup"><span data-stu-id="d6e35-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="d6e35-266">**Deshabilitar la replicación en las tablas especificadas (table1, table2 y table3)**:</span><span class="sxs-lookup"><span data-stu-id="d6e35-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="d6e35-267">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6e35-267">Next steps</span></span>

<span data-ttu-id="d6e35-268">En este tutorial, se habrá aprendido cómo tooconfigure HBase replicación entre dos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="d6e35-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="d6e35-269">toolearn más información acerca de HDInsight y HBase, consulte:</span><span class="sxs-lookup"><span data-stu-id="d6e35-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="d6e35-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started] (Introducción a HBase Apache en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d6e35-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="d6e35-271">[HDInsight HBase overview][hdinsight-hbase-overview] (Información general de HBase de HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d6e35-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="d6e35-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet] (Creación de clústeres de HBase en Azure Virtual Network)</span><span class="sxs-lookup"><span data-stu-id="d6e35-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="d6e35-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment] (Análisis de opinión en Twitter en tiempo real con HBase)</span><span class="sxs-lookup"><span data-stu-id="d6e35-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="d6e35-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data] [Análisis de los datos de sensor con Storm y HBase en HDInsight (Hadoop)]</span><span class="sxs-lookup"><span data-stu-id="d6e35-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
