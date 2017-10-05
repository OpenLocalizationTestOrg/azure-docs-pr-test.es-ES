---
title: "Configuración de la replicación de clúster de HBase en redes virtuales - Azure | Microsoft Docs"
description: "Aprenda a configurar la replicación de HBase para equilibrio de carga, alta disponibilidad, migración o actualización sin tiempo de inactividad de una versión de HDInsight a otra y recuperación ante desastres."
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
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="5e5f1-103">Configuración de la replicación de clúster de HBase en redes virtuales</span><span class="sxs-lookup"><span data-stu-id="5e5f1-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="5e5f1-104">Aprenda a configurar la replicación de HBase en una red virtual (VNet) o entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="5e5f1-105">La replicación de clúster usa una metodología de inserción de origen.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="5e5f1-106">Un clúster de HBase puede ser un origen, un destino o cumplir ambos roles a la vez.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="5e5f1-107">La replicación es asincrónica y el objetivo de la replicación es la coherencia eventual.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="5e5f1-108">Cuando el origen recibe una edición en una familia de columna con la replicación habilitada, esa edición se propaga a todos los clústeres de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="5e5f1-109">Cuando se replican datos de un clúster a otro, se realiza un seguimiento del clúster de origen y de todos los clústeres que ya han consumido los datos para evitar bucles de replicación.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="5e5f1-110">En este tutorial, configurará una replicación de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="5e5f1-111">Para otras topologías de clúster, consulte [Guía de referencia de HBase Apache](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="5e5f1-112">Casos de uso de replicación de HBase para una única red virtual:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="5e5f1-113">Equilibrio de carga, por ejemplo: ejecutar exámenes o trabajos MapReduce en el clúster de destino e ingerir datos en el clúster de origen</span><span class="sxs-lookup"><span data-stu-id="5e5f1-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="5e5f1-114">Alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="5e5f1-114">High availability</span></span>
* <span data-ttu-id="5e5f1-115">Migración de datos de un clúster de HBase a otro</span><span class="sxs-lookup"><span data-stu-id="5e5f1-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="5e5f1-116">Actualización de un clúster de Azure HDInsight de una versión a otra</span><span class="sxs-lookup"><span data-stu-id="5e5f1-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="5e5f1-117">Casos de uso de replicación de HBase para dos redes virtuales:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="5e5f1-118">Recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="5e5f1-118">Disaster recovery</span></span>
* <span data-ttu-id="5e5f1-119">Equilibrio de carga y creación de particiones de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5e5f1-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="5e5f1-120">Alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="5e5f1-120">High availability</span></span>

<span data-ttu-id="5e5f1-121">Puede replicar clústeres mediante scripts de [acción de script](hdinsight-hadoop-customize-cluster-linux.md) que se encuentran en [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e5f1-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5e5f1-122">Prerequisites</span></span>
<span data-ttu-id="5e5f1-123">Antes de comenzar este tutorial, debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5e5f1-124">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="5e5f1-125">Configuración de los entornos</span><span class="sxs-lookup"><span data-stu-id="5e5f1-125">Configure the environments</span></span>

<span data-ttu-id="5e5f1-126">Hay tres opciones de configuración posibles:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-126">There are three possible configurations:</span></span>

- <span data-ttu-id="5e5f1-127">Dos clústeres de HBase en una única red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="5e5f1-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="5e5f1-128">Dos clústeres de HBase en dos redes virtuales diferentes de la misma región</span><span class="sxs-lookup"><span data-stu-id="5e5f1-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="5e5f1-129">Dos clústeres de HBase en dos redes virtuales diferentes de dos regiones distintas (replicación geográfica)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="5e5f1-130">Para que sea más fácil configurar los entornos, hemos creado algunas [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5e5f1-131">Si prefiere configurar los entornos mediante otros métodos, consulte:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="5e5f1-132">Creación de clústeres de Hadoop basados en Linux en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e5f1-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- <span data-ttu-id="5e5f1-133">[Create HBase clusters in Azure Virtual Network](hdinsight-hbase-provision-vnet.md) (Creación de clústeres de HBase en Azure Virtual Network)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-133">[Create HBase clusters in Azure Virtual Network](hdinsight-hbase-provision-vnet.md)</span></span>

### <a name="configure-one-virtual-network"></a><span data-ttu-id="5e5f1-134">Configuración de una única red virtual</span><span class="sxs-lookup"><span data-stu-id="5e5f1-134">Configure one virtual network</span></span>

<span data-ttu-id="5e5f1-135">Haga clic en la imagen siguiente para crear dos clústeres de HBase en la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="5e5f1-136">La plantilla se encuentra en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="5e5f1-137">Configuración de dos redes virtuales en la misma región</span><span class="sxs-lookup"><span data-stu-id="5e5f1-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="5e5f1-138">Haga clic en la imagen siguiente para crear dos redes virtuales con emparejamiento de VNet y dos clústeres de HBase en la misma región.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="5e5f1-139">La plantilla se encuentra en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="5e5f1-140">Este escenario requiere [emparejamiento de VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="5e5f1-141">La plantilla permite el emparejamiento de VNet.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="5e5f1-142">La replicación de HBase utiliza direcciones IP de las máquinas virtuales ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="5e5f1-143">Debe configurar las direcciones IP estáticas para los nodos ZooKeeper de HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="5e5f1-144">**Para configurar las direcciones IP estáticas**</span><span class="sxs-lookup"><span data-stu-id="5e5f1-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="5e5f1-145">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5e5f1-146">En el menú de la izquierda, haga clic en **Resource groups** (Grupos de recursos).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="5e5f1-147">Haga clic en el grupo de recursos que contiene el clúster de HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="5e5f1-148">Este es el grupo de recursos que especificó al usar la plantilla de Resource Manager para crear el entorno.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="5e5f1-149">Puede utilizar el filtro para restringir la lista.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="5e5f1-150">Puede ver una lista de recursos que incluye las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="5e5f1-151">Haga clic en la red virtual que contiene el clúster de HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="5e5f1-152">Por ejemplo, haga clic en **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="5e5f1-153">Puede ver tres dispositivos con nombres que empiezan por **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="5e5f1-154">Estos dispositivos son las tres máquinas virtuales ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="5e5f1-155">Haga clic en una de las máquinas virtuales ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="5e5f1-156">Haga clic en **IP configurations** (Configuraciones IP).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="5e5f1-157">En la lista, haga clic en **ipConfig1**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="5e5f1-158">Haga clic en **Static** (Estático) y anote la dirección IP real.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="5e5f1-159">Necesitará la dirección IP al ejecutar la acción de script para habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![Dirección IP estática ZooKeeper de replicación de HBase para HDInsight](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="5e5f1-161">Repita el paso 6 para establecer la dirección IP estática para los otros dos nodos ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="5e5f1-162">En el escenario entre redes virtuales, debe usar el modificador **-ip** al llamar a la acción de script **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="5e5f1-163">Configuración de dos redes virtuales en dos regiones distintas</span><span class="sxs-lookup"><span data-stu-id="5e5f1-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="5e5f1-164">Haga clic en la imagen siguiente para crear dos redes virtuales en dos regiones distintas.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="5e5f1-165">La plantilla se encuentra almacenada en un contenedor de blobs de Azure público.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="5e5f1-166">Cree una puerta de enlace de VPN entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="5e5f1-167">Para obtener instrucciones, consulte [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) (Creación de una red virtual con una conexión de sitio a sitio).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="5e5f1-168">La replicación de HBase utiliza direcciones IP de las máquinas virtuales ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="5e5f1-169">Debe configurar las direcciones IP estáticas para los nodos ZooKeeper de HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="5e5f1-170">Para configurar la dirección IP estática, consulte la sección "Configuración de dos redes virtuales en la misma región" en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="5e5f1-171">En el escenario entre redes virtuales, debe usar el modificador **-ip** al llamar a la acción de script **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="5e5f1-172">Carga de datos de prueba</span><span class="sxs-lookup"><span data-stu-id="5e5f1-172">Load test data</span></span>

<span data-ttu-id="5e5f1-173">Cuando replica un clúster, debe especificar las tablas que se van a replicar.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="5e5f1-174">En esta sección, cargará algunos datos en el clúster de origen.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="5e5f1-175">En la siguiente sección, habilitará la replicación entre los dos clústeres.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="5e5f1-176">Siga las instrucciones de [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) (Tutorial de HBase: Introducción al uso de Apache HBase con Hadoop basado en Linux en HDInsight) para crear una tabla **Contacts** e insertar algunos datos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="5e5f1-177">Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="5e5f1-177">Enable replication</span></span>

<span data-ttu-id="5e5f1-178">Los pasos siguientes muestran cómo llamar al script de acción de script desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="5e5f1-179">Para ejecutar una acción de script mediante Azure PowerShell y la interfaz de línea de comandos (CLI) de Azure, consulte [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md) (Personalización de clústeres de HDInsight basado en Linux mediante acciones de script).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="5e5f1-180">**Para habilitar la replicación de HBase desde Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="5e5f1-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="5e5f1-181">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5e5f1-182">Abra el clúster de HBase de origen.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="5e5f1-183">En el menú del clúster, haga clic en **Script Actions** (Acciones de script).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="5e5f1-184">Haga clic en **Submit New** (Enviar nueva) en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="5e5f1-185">Seleccione o escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="5e5f1-186">**Nombre** especifique **Enable replication** (Habilitar replicación).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="5e5f1-187">**URL de script de Bash**: escriba **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="5e5f1-188">**Principal**: seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-188">**Head**: Selected.</span></span> <span data-ttu-id="5e5f1-189">Borre los demás tipos de nodo.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-189">Clear the other node types.</span></span>
  - <span data-ttu-id="5e5f1-190">**Parámetros**: los siguientes parámetros de ejemplo habilitan la replicación de todas las tablas existentes y copian todos los datos del clúster de origen en el clúster de destino:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="5e5f1-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-191">Click **Create**.</span></span> <span data-ttu-id="5e5f1-192">El script puede tardar algún tiempo, especialmente cuando se usa el argumento -copydata.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="5e5f1-193">Argumentos necesarios:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-193">Required arguments:</span></span>

|<span data-ttu-id="5e5f1-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="5e5f1-194">Name</span></span>|<span data-ttu-id="5e5f1-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="5e5f1-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="5e5f1-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="5e5f1-196">-s, --src-cluster</span></span> | <span data-ttu-id="5e5f1-197">Especifica el nombre DNS del clúster de HBase de origen.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="5e5f1-198">Por ejemplo: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="5e5f1-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="5e5f1-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="5e5f1-199">-d, --dst-cluster</span></span> | <span data-ttu-id="5e5f1-200">Especifica el nombre DNS del clúster de HBase de destino (réplica).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="5e5f1-201">Por ejemplo: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="5e5f1-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="5e5f1-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="5e5f1-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="5e5f1-203">Especifica la contraseña de administrador para Ambari en el clúster de HBase de origen.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="5e5f1-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="5e5f1-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="5e5f1-205">Especifica la contraseña de administrador para Ambari en el clúster de HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="5e5f1-206">Argumentos opcionales:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-206">Optional arguments:</span></span>

|<span data-ttu-id="5e5f1-207">Nombre</span><span class="sxs-lookup"><span data-stu-id="5e5f1-207">Name</span></span>|<span data-ttu-id="5e5f1-208">Descripción</span><span class="sxs-lookup"><span data-stu-id="5e5f1-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="5e5f1-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="5e5f1-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="5e5f1-210">Especifica el nombre de usuario de administrador para Ambari en el clúster de HBase de origen.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="5e5f1-211">El valor predeterminado es **admin**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="5e5f1-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="5e5f1-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="5e5f1-213">Especifica el nombre de usuario de administrador para Ambari en el clúster de HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="5e5f1-214">El valor predeterminado es **admin**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="5e5f1-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="5e5f1-215">-t, --table-list</span></span> | <span data-ttu-id="5e5f1-216">Especifica las tablas que se van a replicar.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="5e5f1-217">Por ejemplo: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="5e5f1-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="5e5f1-218">Si no se especifica unas tablas determinadas, se replican todas las tablas de HBase existentes.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="5e5f1-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="5e5f1-219">-m, --machine</span></span> | <span data-ttu-id="5e5f1-220">Especifica el nodo principal en el que se ejecutará la acción de script.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="5e5f1-221">El valor es hn1 o hn0.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="5e5f1-222">Dado que hn0 suele estar más ocupado, se recomienda utilizar hn1.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="5e5f1-223">Esta opción se utiliza si se está ejecutando el script $0 como acción de script desde el portal de HDInsight o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="5e5f1-224">-ip</span><span class="sxs-lookup"><span data-stu-id="5e5f1-224">-ip</span></span> | <span data-ttu-id="5e5f1-225">Este argumento es necesario cuando se habilita la replicación entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="5e5f1-226">Este argumento actúa como un conmutador para utilizar las direcciones IP estáticas de los nodos ZooKeeper de los clústeres de réplica en lugar de los nombres FQDN.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="5e5f1-227">Las direcciones IP estáticas deben configurarse antes de habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="5e5f1-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="5e5f1-228">-cp, -copydata</span></span> | <span data-ttu-id="5e5f1-229">Habilita la migración de datos existentes en las tablas en las que está habilitada la replicación.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="5e5f1-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="5e5f1-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="5e5f1-231">Habilita la replicación en las tablas del sistema Phoenix.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="5e5f1-232">*Esta opción se debe utilizar con precaución.*</span><span class="sxs-lookup"><span data-stu-id="5e5f1-232">*Use this option with caution.*</span></span> <span data-ttu-id="5e5f1-233">Se recomienda volver a crear tablas de Phoenix en clústeres de réplica antes de utilizar este script.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="5e5f1-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="5e5f1-234">-h, --help</span></span> | <span data-ttu-id="5e5f1-235">Muestra información de uso.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-235">Display usage information.</span></span> |

<span data-ttu-id="5e5f1-236">La sección print_usage() del [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) proporciona una explicación detallada de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="5e5f1-237">Una vez implementada la acción de script correctamente, puede utilizar SSH para conectarse al clúster de HBase de destino y comprobar que los datos se hayan replicado.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="5e5f1-238">Escenarios de replicación</span><span class="sxs-lookup"><span data-stu-id="5e5f1-238">Replication scenarios</span></span>

<span data-ttu-id="5e5f1-239">En la lista siguiente se muestran algunos casos de uso general y la configuración de parámetros:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="5e5f1-240">**Habilitar la replicación en todas las tablas entre los dos clústeres**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="5e5f1-241">Este escenario no requiere la copia o migración de datos existentes en las tablas y no utiliza tablas de Phoenix.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="5e5f1-242">Utilice los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="5e5f1-243">**Habilitar la replicación en tablas específicas**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="5e5f1-244">Use los parámetros siguientes para habilitar la replicación en table1, table2 y table3:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="5e5f1-245">**Habilitar la replicación en tablas específicas y copiar los datos existentes**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="5e5f1-246">Use los parámetros siguientes para habilitar la replicación en table1, table2 y table3:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="5e5f1-247">**Habilitar la replicación en todas las tablas con replicación de metadatos de Phoenix de origen a destino**.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="5e5f1-248">La replicación de metadatos de Phoenix no es perfecta, así que debe habilitarse con precaución.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="5e5f1-249">Copia y migración de datos</span><span class="sxs-lookup"><span data-stu-id="5e5f1-249">Copy and migrate data</span></span>

<span data-ttu-id="5e5f1-250">Hay dos scripts de acción de script independientes para copiar o migrar datos después de habilitar la replicación:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="5e5f1-251">[Script para tablas pequeñas](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (unos pocos gigabytes de tamaño y una copia general deberían finalizar en menos de una hora)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="5e5f1-252">[Script para tablas grandes](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (se espera que tarden más de una hora en copiarse)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="5e5f1-253">Puede seguir el mismo procedimiento que aparece en [Habilitar replicación](#enable-replication) para llamar a la acción de script con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="5e5f1-254">La sección print_usage() del [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) proporciona una descripción detallada de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="5e5f1-255">Escenarios</span><span class="sxs-lookup"><span data-stu-id="5e5f1-255">Scenarios</span></span>

- <span data-ttu-id="5e5f1-256">**Copiar tablas específicas (test1, test2 y test3) para todas las filas editadas hasta ahora (marca de tiempo actual)**:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="5e5f1-257">o</span><span class="sxs-lookup"><span data-stu-id="5e5f1-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="5e5f1-258">**Copiar tablas específicas con el intervalo de tiempo especificado**:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="5e5f1-259">Deshabilitar replicación</span><span class="sxs-lookup"><span data-stu-id="5e5f1-259">Disable replication</span></span>

<span data-ttu-id="5e5f1-260">Para deshabilitar la replicación, utilice otro script de acción de script que se encuentra en [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="5e5f1-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="5e5f1-261">Puede seguir el mismo procedimiento que aparece en [Habilitar replicación](#enable-replication) para llamar a la acción de script con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="5e5f1-262">La sección print_usage() del [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) proporciona una explicación detallada de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="5e5f1-263">Escenarios</span><span class="sxs-lookup"><span data-stu-id="5e5f1-263">Scenarios</span></span>

- <span data-ttu-id="5e5f1-264">**Deshabilitar la replicación en todas las tablas**:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="5e5f1-265">o</span><span class="sxs-lookup"><span data-stu-id="5e5f1-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="5e5f1-266">**Deshabilitar la replicación en las tablas especificadas (table1, table2 y table3)**:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="5e5f1-267">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e5f1-267">Next steps</span></span>

<span data-ttu-id="5e5f1-268">En este tutorial, ha aprendido cómo configurar la replicación de HBase entre dos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="5e5f1-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="5e5f1-269">Para obtener más información acerca de HDInsight y HBase, consulte:</span><span class="sxs-lookup"><span data-stu-id="5e5f1-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="5e5f1-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started] (Introducción a HBase Apache en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="5e5f1-271">[HDInsight HBase overview][hdinsight-hbase-overview] (Información general de HBase de HDInsight)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="5e5f1-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet] (Creación de clústeres de HBase en Azure Virtual Network)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="5e5f1-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment] (Análisis de opinión en Twitter en tiempo real con HBase)</span><span class="sxs-lookup"><span data-stu-id="5e5f1-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="5e5f1-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data] [Análisis de los datos de sensor con Storm y HBase en HDInsight (Hadoop)]</span><span class="sxs-lookup"><span data-stu-id="5e5f1-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

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
