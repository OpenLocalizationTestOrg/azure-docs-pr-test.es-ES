---
title: "clústeres de HBase aaaCreate en una red Virtual - Azure | Documentos de Microsoft"
description: "Introducción al uso de HBase en HDInsight de Azure Obtenga información acerca de cómo se agrupa toocreate HBase para HDInsight en red Virtual de Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="0186b-104">Creación de clústeres de HBase en HDInsight en Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0186b-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="0186b-105">Obtenga información acerca de cómo los clústeres de toocreate HDInsight HBase de Azure en un [red Virtual de Azure][1].</span><span class="sxs-lookup"><span data-stu-id="0186b-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="0186b-106">Con la integración de red virtual, clústeres de HBase pueden ser implementado toohello mismo virtual de red así como las aplicaciones que las aplicaciones pueden comunicarse directamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="0186b-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="0186b-107">Hola ventajas se incluyen:</span><span class="sxs-lookup"><span data-stu-id="0186b-107">hello benefits include:</span></span>

* <span data-ttu-id="0186b-108">Conectividad directa de hello web aplicación toohello los nodos de clúster de HBase hello, que permite la comunicación a través de procedimientos remotos de HBase Java llamar a las API (RPC).</span><span class="sxs-lookup"><span data-stu-id="0186b-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="0186b-109">Rendimiento mejorado gracias a que el tráfico ya no tiene que examinar varias puertas de enlace y equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="0186b-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="0186b-110">Hola capacidad tooprocess información confidencial de forma más segura sin exponer un extremo público.</span><span class="sxs-lookup"><span data-stu-id="0186b-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0186b-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0186b-111">Prerequisites</span></span>
<span data-ttu-id="0186b-112">Antes de comenzar este tutorial, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0186b-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="0186b-113">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0186b-113">**An Azure subscription**.</span></span> <span data-ttu-id="0186b-114">Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0186b-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0186b-115">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0186b-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="0186b-116">Consulte [Install and use Azure PowerShell (Instalación y uso de Azure PowerShell)](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="0186b-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="0186b-117">Creación de un clúster de HBase en red virtual</span><span class="sxs-lookup"><span data-stu-id="0186b-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="0186b-118">En esta sección, se crea un clúster de HBase basados en Linux con cuenta de almacenamiento de Azure dependiente de hello en una red virtual de Azure con un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0186b-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="0186b-119">Para otros métodos de creación de clúster y descripción de la configuración de hello, consulte [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0186b-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="0186b-120">Para obtener más información sobre el uso de un toocreate plantilla Hadoop los clústeres de HDInsight, vea [Hadoop crear clústeres de HDInsight con plantillas del Administrador de recursos de Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="0186b-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="0186b-121">Algunas propiedades están codificados en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="0186b-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0186b-122">For example:</span></span>
>
> * <span data-ttu-id="0186b-123">**Ubicación**: este de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="0186b-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="0186b-124">**Versión del clúster**: 3.5</span><span class="sxs-lookup"><span data-stu-id="0186b-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="0186b-125">**Número de nodos de trabajo en el clúster**: 2</span><span class="sxs-lookup"><span data-stu-id="0186b-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="0186b-126">**Nombre de la cuenta de almacenamiento predeterminada**: una cadena única</span><span class="sxs-lookup"><span data-stu-id="0186b-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="0186b-127">**Nombre de la red virtual**: &lt;Nombre del clúster&gt;-vnet</span><span class="sxs-lookup"><span data-stu-id="0186b-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="0186b-128">**Espacio de direcciones de red virtual**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="0186b-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="0186b-129">**Nombre de subred**: subnet1</span><span class="sxs-lookup"><span data-stu-id="0186b-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="0186b-130">**Intervalo de direcciones de subred**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="0186b-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="0186b-131">&lt;Nombre del clúster > se reemplaza con el nombre de clúster de hello proporcionan cuando se usa la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="0186b-132">Haga clic en hello después de la plantilla de imagen tooopen Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0186b-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="0186b-133">plantilla de Hola se encuentra en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="0186b-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="0186b-134">De hello **implementación personalizada** hoja, escriba Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="0186b-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="0186b-135">**Suscripción**: seleccione un clúster de HDInsight de suscripción de Azure usada toocreate hello, Hola dependiente cuenta de almacenamiento y Hola red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="0186b-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="0186b-136">**Grupo de recursos**: seleccione **Crear nuevo** y especifique un nuevo nombre al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0186b-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="0186b-137">**Ubicación**: seleccione una ubicación para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="0186b-138">**ClusterName**: escriba un nombre para toobe de clúster de Hadoop de hello creado.</span><span class="sxs-lookup"><span data-stu-id="0186b-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="0186b-139">**Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es **administración**.</span><span class="sxs-lookup"><span data-stu-id="0186b-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="0186b-140">**SSH username y password**: nombre de usuario de hello predeterminada es **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="0186b-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="0186b-141">Puede cambiarlo.</span><span class="sxs-lookup"><span data-stu-id="0186b-141">You can rename it.</span></span>
   * <span data-ttu-id="0186b-142">**Muestro mi conformidad toohello términos y condiciones de hello indicadas anteriormente**: (seleccione)</span><span class="sxs-lookup"><span data-stu-id="0186b-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="0186b-143">Haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="0186b-143">Click **Purchase**.</span></span> <span data-ttu-id="0186b-144">Se tarda aproximadamente toocreate de aproximadamente 20 minutos de un clúster.</span><span class="sxs-lookup"><span data-stu-id="0186b-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="0186b-145">Una vez creado el clúster de hello, haga clic en hoja de clúster de hello en tooopen portal Hola se.</span><span class="sxs-lookup"><span data-stu-id="0186b-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="0186b-146">Después de completar el tutorial de hello, conviene clúster de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="0186b-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="0186b-147">Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso.</span><span class="sxs-lookup"><span data-stu-id="0186b-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="0186b-148">También se le cargará por un clúster de HDInsight aunque no esté en uso.</span><span class="sxs-lookup"><span data-stu-id="0186b-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="0186b-149">Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso.</span><span class="sxs-lookup"><span data-stu-id="0186b-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="0186b-150">Para obtener instrucciones de hello de la eliminación de un clúster, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="0186b-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="0186b-151">toobegin trabajar con el nuevo clúster de HBase, puede usar los procedimientos de Hola que se encuentran en [empezar a utilizar HBase con Hadoop en HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0186b-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="0186b-152">Conectar el clúster de HBase toohello mediante las API de RPC de Java de HBase</span><span class="sxs-lookup"><span data-stu-id="0186b-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="0186b-153">Crear una infraestructura como servicio (IaaS) virtual máquina en Hola misma red virtual de Azure y Hola la misma subred.</span><span class="sxs-lookup"><span data-stu-id="0186b-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="0186b-154">Para obtener instrucciones sobre cómo crear una nueva máquina virtual de IaaS consulte el tutorial sobre la [creación de una máquina virtual que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0186b-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="0186b-155">Al seguir los pasos de hello en este documento, debe utilizar Hola después de valores de configuración de red de hello:</span><span class="sxs-lookup"><span data-stu-id="0186b-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="0186b-156">**Red virtual**: &lt;Nombre del clúster&gt;-vnet</span><span class="sxs-lookup"><span data-stu-id="0186b-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="0186b-157">**Subred**: subnet1</span><span class="sxs-lookup"><span data-stu-id="0186b-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0186b-158">Reemplace &lt;nombre del clúster > con el nombre de Hola que utilizó al crear el clúster de HDInsight de hello en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0186b-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="0186b-159">Con estos valores, Hola máquina virtual se coloca en hello misma red virtual y subred que el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="0186b-160">Esta configuración permite toodirectly comunicarse entre sí.</span><span class="sxs-lookup"><span data-stu-id="0186b-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="0186b-161">Hay un toocreate forma un clúster de HDInsight con un nodo del borde vacío.</span><span class="sxs-lookup"><span data-stu-id="0186b-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="0186b-162">nodo del borde Hola puede ser clúster de hello toomanage usado.</span><span class="sxs-lookup"><span data-stu-id="0186b-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="0186b-163">Para obtener más información, consulte [Uso de nodos perimetrales vacíos en HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="0186b-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="0186b-164">Al utilizar un tooHBase de tooconnect de aplicación de Java de forma remota, debe usar el nombre de dominio completo (FQDN) de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="0186b-165">toodetermine esto, debe tener el sufijo DNS específico de la conexión de Hola de clúster de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="0186b-166">toodo, que puede usar uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="0186b-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="0186b-167">Use un toomake de explorador Web una llamada Ambari:</span><span class="sxs-lookup"><span data-stu-id="0186b-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="0186b-168">Examinar toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hospeda? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="0186b-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="0186b-169">Convierte un archivo JSON con los sufijos DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="0186b-170">Use el sitio Web de hello Ambari:</span><span class="sxs-lookup"><span data-stu-id="0186b-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="0186b-171">Examinar demasiado https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0186b-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="0186b-172">Haga clic en **Hosts** de menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="0186b-173">Utilizar llamadas a REST Curl toomake:</span><span class="sxs-lookup"><span data-stu-id="0186b-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="0186b-174">Hola devuelven datos JavaScript Object Notation (JSON), busque la entrada de "host_name" Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="0186b-175">Contiene Hola FQDN para los nodos de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="0186b-176">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0186b-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="0186b-177">parte de Hola de hello dominio nombre que comienza con el nombre del clúster de hello es sufijo DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="0186b-178">Por ejemplo, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="0186b-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="0186b-179">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0186b-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="0186b-180">Hola de uso después de hello de tooregister de secuencia de comandos de PowerShell de Azure **ClusterDetail Get** función, que puede ser el sufijo DNS de hello tooreturn usado:</span><span class="sxs-lookup"><span data-stu-id="0186b-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="0186b-181">Después de ejecutar script de PowerShell de Azure de hello, comando siguiente de Hola de uso sufijo DNS de hello tooreturn mediante el uso de hello **ClusterDetail Get** función.</span><span class="sxs-lookup"><span data-stu-id="0186b-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="0186b-182">Especifique el nombre del clúster de HBase de HDInsight, el nombre y la contraseña de administrador cuando use este comando.</span><span class="sxs-lookup"><span data-stu-id="0186b-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="0186b-183">Este comando devuelve el sufijo DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="0186b-184">Por ejemplo, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="0186b-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="0186b-185">tooverify que Hola máquina virtual puede comunicarse con hello clúster de HBase, use comandos de hello `ping headnode0.<dns suffix>` de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0186b-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="0186b-186">Por ejemplo, haga ping a headnode0.mycluster.b1.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="0186b-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="0186b-187">toouse esta información en una aplicación Java, puede seguir los pasos de hello en [aplicaciones de Java de toobuild usar Maven que utilizar HBase con HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0186b-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="0186b-188">aplicación de hello toohave conectar el servidor remoto de HBase de tooa, modifique hello **hbase-site.xml** archivo esta Hola de toouse FQDN de ejemplo para Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="0186b-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="0186b-189">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0186b-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="0186b-190">Para obtener más información acerca de la resolución de nombres en redes virtuales de Azure, incluida la forma toouse su propio servidor DNS, consulte [resolución de nombres (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="0186b-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0186b-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0186b-191">Next steps</span></span>
<span data-ttu-id="0186b-192">En este tutorial, se habrá aprendido cómo toocreate un clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="0186b-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="0186b-193">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="0186b-193">toolearn more, see:</span></span>

* [<span data-ttu-id="0186b-194">Introducción a HDInsight</span><span class="sxs-lookup"><span data-stu-id="0186b-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="0186b-195">Uso de nodos perimetrales vacíos en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0186b-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="0186b-196">Configuración de la replicación geográfica de HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0186b-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="0186b-197">Consulte Creación de clústeres de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0186b-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="0186b-198">Introducción al uso de HBase con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0186b-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="0186b-199">Análisis de opiniones de Twitter con HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0186b-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="0186b-200">[Información general sobre redes virtuales][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="0186b-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalles de aprovisionamiento para el nuevo clúster de HBase Hola"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Use la acción de secuencia de comandos toocustomize un clúster de HBase"

[azure-preview-portal]: https://portal.azure.com
