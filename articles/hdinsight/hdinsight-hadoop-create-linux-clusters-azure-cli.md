---
title: "Creación de clústeres de Hadoop mediante la línea de comandos - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear clústeres de HDInsight con la CLI multiplataforma de Azure 1.0."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="09a5d-103">Creación de clústeres de HDInsight mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="09a5d-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="09a5d-104">Los pasos de este tutorial describen la creación de un clúster de HDInsight 3.5 mediante la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="09a5d-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09a5d-105">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="09a5d-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="09a5d-106">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="09a5d-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="09a5d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="09a5d-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="09a5d-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="09a5d-108">**An Azure subscription**.</span></span> <span data-ttu-id="09a5d-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="09a5d-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="09a5d-110">**CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="09a5d-110">**Azure CLI**.</span></span> <span data-ttu-id="09a5d-111">Los pasos de este documento se probaron por última vez en la versión 0.10.14 de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="09a5d-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="09a5d-112">Los pasos descritos en este documento no funcionan con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="09a5d-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="09a5d-113">La CLI de Azure 2.0 no admite la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09a5d-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="09a5d-114">Inicio de sesión en la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="09a5d-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="09a5d-115">Siga los pasos que se documentan en [Conexión a una suscripción de Azure desde la interfaz de la línea de comandos de Azure (CLI de Azure)](../xplat-cli-connect.md) y conéctese a su suscripción con el método **login** .</span><span class="sxs-lookup"><span data-stu-id="09a5d-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="09a5d-116">Crear un clúster</span><span class="sxs-lookup"><span data-stu-id="09a5d-116">Create a cluster</span></span>

<span data-ttu-id="09a5d-117">Los siguientes pasos deben realizarse desde una línea de comandos como PowerShell o Bash.</span><span class="sxs-lookup"><span data-stu-id="09a5d-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="09a5d-118">Use el siguiente comando para autenticarse en su suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="09a5d-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="09a5d-119">Se le solicitará que escriba su nombre y contraseña.</span><span class="sxs-lookup"><span data-stu-id="09a5d-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="09a5d-120">Si tiene varias suscripciones de Azure, puede usar `azure account set <subscriptionname>` para establecer la suscripción que usarán los comandos de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="09a5d-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="09a5d-121">Cambie al modo de Administrador de recursos de Azure con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="09a5d-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="09a5d-122">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09a5d-122">Create a resource group.</span></span> <span data-ttu-id="09a5d-123">Este grupo de recursos contiene el clúster de HDInsight y la cuenta de almacenamiento asociada.</span><span class="sxs-lookup"><span data-stu-id="09a5d-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="09a5d-124">Sustituya `groupname` por un nombre único para el grupo.</span><span class="sxs-lookup"><span data-stu-id="09a5d-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="09a5d-125">Sustituya `location` por la región geográfica en la que quiere crear el grupo.</span><span class="sxs-lookup"><span data-stu-id="09a5d-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="09a5d-126">Para obtener una lista de ubicaciones válidas, use el comando `azure location list` y luego una de las ubicaciones de la columna `Name`.</span><span class="sxs-lookup"><span data-stu-id="09a5d-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="09a5d-127">Cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09a5d-127">Create a storage account.</span></span> <span data-ttu-id="09a5d-128">Esta cuenta de almacenamiento se usa como almacenamiento predeterminado del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09a5d-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="09a5d-129">Sustituya `groupname` por el nombre del grupo creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="09a5d-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="09a5d-130">Sustituya `location` por la misma ubicación usada en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="09a5d-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="09a5d-131">Sustituya `storagename` por un nombre único para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09a5d-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="09a5d-132">Si desea obtener más información sobre los parámetros utilizados en este comando, use `azure storage account create -h` para ver la ayuda correspondiente.</span><span class="sxs-lookup"><span data-stu-id="09a5d-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="09a5d-133">Recupere la clave utilizada para tener acceso a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09a5d-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="09a5d-134">Sustituya `groupname` por el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09a5d-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="09a5d-135">Sustituya `storagename` por el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09a5d-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="09a5d-136">En los datos que se devuelven, guarde el valor `key` de `key1`.</span><span class="sxs-lookup"><span data-stu-id="09a5d-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="09a5d-137">Cree un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09a5d-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="09a5d-138">Sustituya `groupname` por el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09a5d-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="09a5d-139">Sustituya `Hadoop` por el tipo de clúster que quiere crear.</span><span class="sxs-lookup"><span data-stu-id="09a5d-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="09a5d-140">Por ejemplo, `Hadoop`, `HBase`, `Kafka`, `Spark` o `Storm`.</span><span class="sxs-lookup"><span data-stu-id="09a5d-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="09a5d-141">Los clústeres de HDInsight incluyen diversos tipos, que corresponden a la carga de trabajo o la tecnología para los que el clúster está optimizado.</span><span class="sxs-lookup"><span data-stu-id="09a5d-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="09a5d-142">No hay ningún método admitido para crear un solo clúster que combine varios tipos, como Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="09a5d-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="09a5d-143">Sustituya `location` por la misma ubicación usada en pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="09a5d-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="09a5d-144">Sustituya `storagename` por el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09a5d-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="09a5d-145">Sustituya `storagekey` por la clave obtenida en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="09a5d-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="09a5d-146">Para el parámetro `--defaultStorageContainer` , use el mismo nombre que utiliza para el clúster.</span><span class="sxs-lookup"><span data-stu-id="09a5d-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="09a5d-147">Sustituya `admin` y `httppassword` por el nombre y la contraseña que quiere usar en el acceso al clúster mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="09a5d-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="09a5d-148">Sustituya `sshuser` y `sshuserpassword` por el nombre de usuario y la contraseña que quiere usar en el acceso al clúster mediante SSH</span><span class="sxs-lookup"><span data-stu-id="09a5d-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="09a5d-149">En este ejemplo se crea un clúster con dos nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="09a5d-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="09a5d-150">Si quiere cambiar el número de nodos de trabajo después de la creación del clúster, realice operaciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="09a5d-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="09a5d-151">Si planea usar más de 32 nodos de trabajo, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="09a5d-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="09a5d-152">Durante la creación del clúster, puede establecer el tamaño del nodo principal mediante el parámetro `--headNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="09a5d-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="09a5d-153">Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="09a5d-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="09a5d-154">Pueden pasar varios minutos (por lo general, unos quince) hasta que finalice el proceso</span><span class="sxs-lookup"><span data-stu-id="09a5d-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="09a5d-155">de creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="09a5d-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="09a5d-156">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="09a5d-156">Troubleshoot</span></span>

<span data-ttu-id="09a5d-157">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="09a5d-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09a5d-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09a5d-158">Next steps</span></span>

<span data-ttu-id="09a5d-159">Una vez creado correctamente un clúster de HDInsight correctamente mediante la CLI de Azure, use los siguientes vínculos para aprender a trabajar con él:</span><span class="sxs-lookup"><span data-stu-id="09a5d-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="09a5d-160">Clústeres Hadoop</span><span class="sxs-lookup"><span data-stu-id="09a5d-160">Hadoop clusters</span></span>

* [<span data-ttu-id="09a5d-161">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="09a5d-162">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="09a5d-163">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="09a5d-164">Clústeres HBase</span><span class="sxs-lookup"><span data-stu-id="09a5d-164">HBase clusters</span></span>

* [<span data-ttu-id="09a5d-165">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="09a5d-166">Desarrollo de aplicaciones de Java para HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="09a5d-167">Clústeres Storm</span><span class="sxs-lookup"><span data-stu-id="09a5d-167">Storm clusters</span></span>

* [<span data-ttu-id="09a5d-168">Desarrollo de topologías de Java para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="09a5d-169">Uso de componentes de Python en Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="09a5d-170">Implementación y supervisión de topologías con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="09a5d-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
